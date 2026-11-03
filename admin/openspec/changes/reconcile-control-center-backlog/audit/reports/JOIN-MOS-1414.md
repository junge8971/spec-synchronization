# JOIN-MOS-1414 — время незавершённого диалога

## Результат и границы

**Обнаружен статический разрыв реализации и точного требования:** реестр показывает серверную длительность, но не добавляет «и идёт» для незавершённого диалога. Текущий компонентный тест закрепляет отображение без этой подписи. Main spec реестра содержит поля длительности и завершения, но не точное правило подписи.

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. `git status --short` пуст; ignored OpenSpec этим не проверяется. Только чтение локальных материалов; изменений, запусков тестов, браузера, сетевых запросов и делегирования не было.

Здесь `A` = `openspec/changes/reconcile-control-center-backlog/audit`.

## 1. Атомарные требования

Первичный источник: `A/sources/jira-subtasks/r1/content.json#/items/4`, строки 90–108; ключ `MOS-1414`, родитель `MOS-1037`, статус сохранённой задачи `Backlog`.

| ID | Ожидаемое поведение | Локатор |
|---|---|---|
| R1 | В реестре «Диалоги», в столбце «Время», незавершённый диалог показывает длительность на момент ответа источника. | `/items/4/description`, раздел «ОР», первое предложение |
| R2 | Интерфейс дополняет эту длительность словами **«и идёт»**. | Тот же `/description`, конец «ОР» |
| R3 | Условие незавершённости определяется `ended_at = null`; длительность берётся из `duration_sec`, а не вычисляется по клиентским часам. | `A/sources/wiki-241085439/r1/content.json#/bodyView`, §2.3, строки таблицы `ended_at`, `duration_sec` |

R3 уточняет применение R1–R2 по сохранённому контракту, а не расширяет задачу. Требований о локальном тикающем таймере, частоте опроса или новом API Jira не содержит.

**Историческое наблюдение Jira:** отображается только время диалога. Указанные URL и окружение являются частью сохранённого описания, а не подтверждением текущего состояния стенда.

## 2. API: применимость и ограничения

Сохранённый контракт `wiki-241085439`, версия 15, §2.3 прямо задаёт:

- `ended_at: string | null`; `null` означает незавершённый диалог;
- `duration_sec: integer` — длительность в секундах;
- у незавершённого диалога это снимок на момент ответа источника, интерфейс дополняет его словами «и идёт»;
- §2.5.1 относит `ended_at` и `duration_sec` к выдаче реестра.

Текущая интеграция уже предоставляет необходимые данные:

- `app/entities/dialog/api/dialog-client.ts:14–27`: `ended_at` nullable, `duration_sec` — целое неотрицательное число;
- там же `:48–56`: POST поиска, проверка результата через `dialogPageSchema`;
- `app/shared/api/schema.d.ts:2385–2388`: оба поля присутствуют в сгенерированной модели;
- `openspec/specs/dialog-registry/spec.md:11`: принятый endpoint `/api/control/api/dialogs/v1/dialogs/search`.

**Вывод:** изменение API не требуется. Контракт достаточен для условной текстовой подписи. Схема типов сама по себе не доказывает фактическую корректность серверного снимка; backend и развёртывание не проверялись.

Ограничения источника: metadata Wiki прямо отделяет публикацию от runtime/approval; §8.11 содержит оговорку о происхождении определения длительности. Точное ожидаемое поведение дополнительно независимо сформулировано в Jira, поэтому продуктовый вопрос о самой подписи не нужен.

## 3. OpenSpec ownership и покрытие

| Артефакт / owner | Наблюдение |
|---|---|
| `openspec/specs/dialog-registry/spec.md:19–26`, `Registry represents server rows faithfully` | Перечислены `ended_at`, `duration_sec`; сценарий `Unfinished and unrated dialog` требует «не завершён» и отсутствие оценки. Правила «и идёт» для «Время» нет. Покрытие частичное. |
| `openspec/changes/archive/2026-10-05-mos-1037-dialog-registry/specs/dialog-registry/spec.md`, тот же requirement | Исторический владелец исходного реестра; тот же пробел. Архив не изменять. |
| `openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/dialog-registry/spec.md` | Delta посвящена явному применению быстрых фильтров; эту задачу не покрывает. |
| `openspec/specs/dialog-details/spec.md:23–25` | Для **карточки** требуется серверный снимок с признаком продолжения. Это не покрытие столбца реестра. |
| Текущие активные changes | Отдельного corrective owner для этого дефекта не обнаружено. |

`A/coverage.json` имеет `acceptedEvidenceThrough: D-089`, `complete: false`. Источник вложенных задач — `reports/G2-JIRA-MEMBER-JOINS.md`, строки 296–311; строка 300 содержит MOS-1414 как `U / UN`. В overlays текущего coverage нет перехода MOS-1414. Покрытие родителя MOS-1037 нельзя автоматически считать покрытием этой подзадачи.

## 4. Код и тесты

**Observed:**

- `app/pages/dialogs/ui/dialog-table/dialog-table-row.tsx:48–52` различает завершённость только в отдельной колонке «Завершение».
- `:60–62` безусловно выводит:
  `Math.floor(row.duration_sec / 60)` минут и `row.duration_sec % 60` секунд.
  В этой ячейке нет ветки по `ended_at` и нет текста «и идёт».
- Поэтому R1 реализован статически: значение форматируется непосредственно из серверного поля. R2 не реализован.
- `app/pages/dialogs/ui/dialogs-page.test.tsx:12–25` задаёт строку с `ended_at: null`, `duration_sec: 48`.
- Тест `renders all row data, safe text, independent flags and a basename-aware chat link`, строки 143–166, ожидает точный текст `0 мин 48 с`. Это не просто отсутствие нужной проверки: существующее ожидание закрепляет неполную подпись.
- Вариант завершённой строки есть в том же файле, строки 312–342, но проверка отсутствия «и идёт» там не обнаружена.
- Поиск по тестам `app/pages/dialogs` не обнаружил assertion для «и идёт».

Соседние тесты карточки с такой подписью не являются тестами реестра.

**Unknown:** выполнение тестов, фактический рендер на стенде, соответствие ответа реального источника указанной семантике. Статический вывод не является воспроизведением дефекта в браузере.

## 5. Минимальная корректировка планирования

**Рекомендация: `new`, не no-op.** После независимого ревью создать узкий corrective change, например `fix-dialog-registry-unfinished-duration`:

1. `proposal.md`: только MOS-1414; исправление подписи длительности реестра, без новых endpoint, таймера и изменений карточки.
2. `specs/dialog-registry/spec.md`: `MODIFIED Requirements` для `Registry represents server rows faithfully`, сохранив все текущие условия и сценарии. Добавить:
   - при `ended_at = null` ячейка «Время» показывает форматированный `duration_sec` и «и идёт»;
   - значение остаётся серверным снимком;
   - при ненулевом `ended_at` подпись продолжения отсутствует.
3. `tasks.md`: оставить задачи **неотмеченными**:
   - условная подпись в `app/pages/dialogs/ui/dialog-table/dialog-table-row.tsx`;
   - обновление точного ожидания в `app/pages/dialogs/ui/dialogs-page.test.tsx`;
   - компонентные проверки незавершённого и завершённого диалога, нулевой длительности, обновления серверного снимка без клиентского пересчёта;
   - штатные проверки проекта при будущей реализации, без browser/E2E.

**`keep`:** API, main spec до штатного применения corrective delta, архивные changes, исторические ledger и feature-checkboxes.

После принятия отчёта parent может добавить новую доказательную связь MOS-1414 с этим отчётом и планом. Она должна обозначать частичный аналитический результат, а не исправление, доставку или завершение задачи.

## 6. SHA256 ключевых входов

Хеши вычислены по локальным байтам; для обоих `content.json` совпадают с сохранёнными metadata.

| Файл | SHA256 |
|---|---|
| `A/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `A/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `A/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `A/sources/wiki-241085439/r1/content.json` | `974ea35aaf44b9ec7c14c573ba58bdf7ed55397a9ca47d62b37fb39d9886f8bc` |
| `A/sources/wiki-241085439/r1/metadata.json` | `dcaab775172b7e615dfae64184d719f8403cff1fb304650ba21e1532ce577b7d` |
| `A/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `openspec/specs/dialog-registry/spec.md` | `ef9e52b7dba2ff4f0fa1dd1a9fa3d7cfaa78890277c376d70ed0301423bf6f83` |
| `openspec/specs/dialog-details/spec.md` | `25fa6ea2bb92bbcd37ac24d6fb668b6756e7be04dd36d3e23b2abb399d666334` |
| `openspec/changes/archive/2026-10-05-mos-1037-dialog-registry/specs/dialog-registry/spec.md` | `742762a4b4565370424c79645372cfdfe46007423842d88eba20a3376fc1d17d` |
| `openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/dialog-registry/spec.md` | `3590e25793853406e9b0fd6ff9c4c094d4c4f7f8cd52f0dd119c96527ad8ed24` |
| `app/pages/dialogs/ui/dialog-table/dialog-table-row.tsx` | `3096df76cead86dad46f13be6cbde70de0a2c0d009c0842f82087f89ad985de3` |
| `app/pages/dialogs/ui/dialogs-page.test.tsx` | `3dba3eb88505d29a2ed80dab6c301e0496007e85a26749d74b80a747824d2fec` |
| `app/entities/dialog/api/dialog-client.ts` | `cbcf7ab8deebf1dd6dc211042d3fb0e820a36bb99081e93596138e1a087484b1` |
| `app/shared/api/schema.d.ts` | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |

## 7. Ограничения

- Jira revision 1 получена `2026-10-16T11:23:01.951Z`; комментарии и дополнительные acceptance-поля не сохранены.
- Вложение `839675` известно только по metadata `/items/4/attachments/0`; изображение не исследовано.
- Внешняя актуальность источников не проверялась.
- Проверки проекта намеренно не запускались по контракту задания.
- Никаких утверждений о deployment, исправлении backend или выполнении всей функциональности диалогов.