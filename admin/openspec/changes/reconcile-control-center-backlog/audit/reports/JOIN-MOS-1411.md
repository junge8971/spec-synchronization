# JOIN-MOS-1411 — видимость и семантика сброса фильтров диалогов

## Результат

**Рекомендация: new — узкая корректировка планирования для `dialog-registry`.** Дефект подтверждается статически: кнопка «Сбросить» безусловно присутствует даже при исходном пустом отборе. Семантика общего сброса реализована; существующие тесты частично её проверяют, но не проверяют скрытие кнопки.

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`.

Проверен только MOS-1411, без пересмотра остальных дефектов модуля. Изменений проекта, ledger и feature-checkboxes нет.

## Источники и атомарные требования

Пути ниже относительно корня проекта; `audit/` означает `openspec/changes/reconcile-control-center-backlog/audit/`.

- **J:** `audit/sources/jira-subtasks/r1/content.json`, `$.items[2]`, строки 52–59: MOS-1411, parent MOS-1037, Backlog; описание содержит шаги, ожидаемое/фактическое поведение и СПС-25.
- **W:** `audit/sources/wiki-243776365/r1/content.json`, `$.text` / `$.bodyView`: «Бизнес-анализ: Диалоги», version 13. Точные текстовые локаторы: `СПС-25`; `Сценарий 1. Сброс отбора`; `Отображение кнопки "Сбросить"` с условием наличия активного отбора.
- **A:** `audit/sources/api-live/r1/content.json`, `$.paths["/api/control/api/dialogs/v1/dialogs/search"].post`.

| ID | Expected — требование и источник | Observed — текущая реализация |
|---|---|---|
| R1 | При исходном состоянии без отбора кнопка скрыта. J `description`, ОР; W СПС-25 | **Не соответствует:** `app/pages/dialogs/ui/dialog-filters.tsx:82–94` безусловно рендерит Button. |
| R2 | При активном поиске, периоде, поверхностях, навыках или условиях кнопка доступна в строке фильтров. J СПС-25; W блок «Отображение кнопки…» | Кнопка расположена в общей строке быстрых фильтров рядом с условиями. Доступна всегда, следовательно положительная ветвь есть, условность отсутствует. |
| R3 | Один общий сброс снимает поиск, период, поверхности, навыки и условия. J СПС-25; W «Сценарий 1. Сброс отбора» | `dialog-filters.tsx:88–90` сбрасывает форму и применяет `initialDialogSelection`; `constants/dialogs.constants.ts:3–11`: `q:''`, `all_time`, пустые IDs, `condition_group:null`. |
| R4 | После сброса, когда сбрасывать нечего, кнопка снова скрыта. J шаги 1–3 + ОР; W СПС-25 | **Не соответствует:** рендер не зависит от результата сброса. |

Отдельное действующее локальное обязательство, не новое требование Jira: общий сброс должен очищать также неприменённые быстрые изменения. Оно закреплено в main spec и должно сохраниться при исправлении видимости.

## API: применимость и границы

Для **видимости кнопки** API-изменение не требуется: это вычисление состояния UI.

Для **сброса применённого отбора** применим существующий POST search:

- A `post.description`: пустой `q` эквивалентен отсутствию; пустые массивы IDs не ограничивают выдачу; части отбора соединяются AND; предусмотрен `all_time`.
- Изменённый selection требует новой цепочки без старого cursor: cursor связан с selection/sort.
- `all_time` не означает обход retention, разрешений или области видимости сотрудника.
- `app/entities/dialog/api/dialog-client.ts:49–56` отправляет валидированный selection через существующий search.
- `app/entities/dialog/model/use-dialogs-query.ts:24–33`: selection входит в query key, начальный cursor — `null`.

Контракт согласуется с текущим набором сбрасываемых значений. Для исправления не нужны новый reset endpoint, изменение DTO, backend mutation или новая auth-модель. Фактическая работа внешнего backend не проверялась; сохранённый OpenAPI — свидетельство контракта, не доступности сервиса.

## OpenSpec ownership и покрытие

1. **Основной текущий owner:** `openspec/specs/dialog-registry/spec.md`.
   - Строка 34: единый selection, исходный период `all_time`.
   - Строки 79–101, `Quick filter application is visibly explicit` / `Reset pending changes`: общий сброс draft и применённого отбора.
   - **Пробел:** отсутствует явное обязательство скрывать общий сброс, когда сбрасывать нечего.

2. **Связанный owner:** `openspec/specs/dialog-selection-builder/spec.md:41–53`.
   - `Draft changes require explicit application`: общий сброс очищает все пять частей отбора; очистка только группы отличается от общего сброса.
   - Семантика R3 покрыта; условная видимость R1/R4 не задана.

3. **Исторические владельцы:**
   - `openspec/changes/archive/2026-10-05-mos-1037-dialog-registry/specs/dialog-registry/spec.md`, `Search shares one versioned selection`.
   - `openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/dialog-registry/spec.md:3–25` содержит нынешнее обязательство сбрасывать pending changes, но не скрывать кнопку.
   - Архивы не исправлять.

4. Активного delta `openspec/changes/*/specs/dialog-registry/spec.md` при локальном просмотре не найдено.

`audit/coverage.json` остаётся `complete:false`, `acceptedEvidenceThrough:D-089`; overlay для MOS-1411 отсутствует. Исторический `audit/reports/G2-JIRA-MEMBER-JOINS.md:298` хранит MOS-1411 как U. Этот отчёт не меняет историческое состояние и не объявляет delivery.

## Доказательства кода и тестов

- `app/pages/dialogs/ui/dialogs-page.tsx:16`: при отсутствии восстановленной ссылки используется `initialDialogSelection`.
- `app/pages/dialogs/ui/dialog-filters.tsx:29–31`: вычисляется только `hasPendingChanges`; это не условие рендера сброса.
- `app/pages/dialogs/ui/dialog-registry.tsx:38–49`: reset увеличивает `editorVersion`, перемонтируя редактор условий; применяет новый selection и исходную сортировку.
- `app/pages/dialogs/model/quick-filter-key.ts`: уже существует нормализация быстрых фильтров — trim строки, пустые IDs, порядок/дубли IDs, период. Она **не учитывает `condition_group`**, поэтому сама по себе недостаточна для всей кнопки.

Прочитанные тесты, **без запуска**:

- `app/pages/dialogs/ui/dialogs-page.test.tsx:203–247`: при отказе справочников проверены поиск/custom period, неприменённый draft, общий сброс, пустой `q`, `all_time`, cursor `null`, очистка контролов и сообщения pending.
- Там же `:366–455`: быстрые фильтры вместе с условиями, отдельная очистка группы, общий сброс IDs/поиска/периода, закрытие редактора.
- В последнем сценарии группа очищена **до** общего сброса. Поэтому этот тест не доказывает одним действием очистку одновременно непустых всех пяти частей selection.
- В просмотренных reset-сценариях нет assertions отсутствия кнопки до фильтрации и после сброса.

## Findings и минимальные planning corrections

### F1 — подтверждённый UI-дефект

`app/pages/dialogs/ui/dialog-filters.tsx:82–94`: безусловная кнопка нарушает R1/R4. Planning no-op не обоснован.

### F2 — спецификация и регрессионное покрытие неполны

Семантика сброса есть, но условная видимость не закреплена и не проверена.

**Предлагаемый новый change:** `fix-dialog-filter-reset-visibility` — название кандидат, не существующий owner.

Минимальные артефакты для последующего решения parent:

- `proposal.md`: MOS-1411, СПС-25, только видимость общего сброса и сохранение существующей семантики.
- `design.md`: использовать имеющуюся нормализацию быстрых фильтров; отдельно учитывать применённую группу условий и возможность сброса неприменённых быстрых изменений. Не ограничивать условие только `hasPendingChanges`: применённый активный отбор тоже должен позволять сброс.
- `specs/dialog-registry/spec.md`: добавить requirement условной доступности общего сброса в строке фильтров; сценарии «исходный пустой отбор», «единственный активный критерий», «после общего сброса», «неприменённые быстрые изменения».
- `tasks.md`: оставить все новые задачи unchecked:
  1. Уточнить предикат «есть что сбрасывать», не потеряв условия и pending draft.
  2. Условно показывать существующую кнопку без изменения search API и обработки ошибок.
  3. Добавить component/unit-проверки начального скрытия, отдельных пяти видов отбора, скрытия после сброса, одновременной очистки всех пяти частей и pending draft.
  4. Запустить штатные небраузерные проверки при реализации.

**Keep:** existing `dialog-selection-builder` semantics, API, архивы, исторические отчёты и feature-checkboxes.

**Ограниченное уточнение:** источники не формализуют видимость общего сброса для исключительно неприменённого draft сложных условий. Не выдавать выбранную трактовку за требование Jira; отдельно зафиксировать её в design, если реализация затронет этот случай. Это не блокирует устранение подтверждённого дефекта исходного состояния.

## SHA256 ключевых входов

Хеши вычислены по локальным байтам; три content-хеша совпадают с соответствующими metadata.

| Файл | SHA256 |
|---|---|
| `audit/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `audit/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `audit/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `audit/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `audit/sources/wiki-243776365/r1/content.json` | `2f659b5423fa7203dcd4f70743e59aabfb571452144394621091ff2cd58cab55` |
| `audit/sources/wiki-243776365/r1/metadata.json` | `fc250c2633f28f6a8f408835145a59aa4cb8612606b40cb8bf79cf088ea256b8` |
| `audit/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `audit/sources/api-live/r1/metadata.json` | `3d92a2024209edecf98eaa1095e40a565611c9eb6ccc4de312ed900165b9f8ff` |
| `openspec/specs/dialog-registry/spec.md` | `ef9e52b7dba2ff4f0fa1dd1a9fa3d7cfaa78890277c376d70ed0301423bf6f83` |
| `openspec/specs/dialog-selection-builder/spec.md` | `87d9ad1687832a1f1eb54a69b65d168cfe04a94fdc5bed1f95ea25983afc8ca6` |
| `openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/dialog-registry/spec.md` | `3590e25793853406e9b0fd6ff9c4c094d4c4f7f8cd52f0dd119c96527ad8ed24` |
| `app/pages/dialogs/ui/dialog-filters.tsx` | `72d95c6383ec7ffc36a7fa638f8fc3b2fa562008bea94e0c9c0fd13d6fb0f66d` |
| `app/pages/dialogs/ui/dialog-registry.tsx` | `5e487284416e43ae82a20fe43a20546bb327e44e8c8f0f95e77ba427b52aa801` |
| `app/pages/dialogs/ui/dialogs-page.test.tsx` | `3dba3eb88505d29a2ed80dab6c301e0496007e85a26749d74b80a747824d2fec` |
| `app/pages/dialogs/constants/dialogs.constants.ts` | `ff44d72901017a14b4271601c080fa98c7cbc51026a4fa4b896fc7ce4cf315f9` |
| `app/entities/dialog/model/use-dialogs-query.ts` | `109de3d9131739c6aae881a59d3a43db7b46939fbc54cc9be4a05f6a3ff0d850` |
| `app/entities/dialog/api/dialog-client.ts` | `cbcf7ab8deebf1dd6dc211042d3fb0e820a36bb99081e93596138e1a087484b1` |
| `docs/api/contracts/dialogs.md` | `70ffb101d6e4dcb71c4a217d1d0e7b3aec444919404d65ff7d3a3aeb206dd84a` |

## Ограничения

Jira snapshot не содержит комментарии/custom acceptance fields; вложение `$.items[2].attachments[0]`, ID `839653`, представлено только metadata, видео не просмотрено. Актуальность внешних источников после сохранения неизвестна. Браузер, сеть, business API, тесты и сборка не запускались. Статический дефект не является утверждением о состоянии deployment.