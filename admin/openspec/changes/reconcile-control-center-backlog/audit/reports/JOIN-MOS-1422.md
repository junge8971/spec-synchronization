# JOIN-MOS-1422 — кнопки сортировки реестра диалогов

## Граница и результат

Проверена только сохранённая подзадача **MOS-1422**, родитель MOS-1037. HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`.

**Вывод: keep / обоснованный no-op для реализации и OpenSpec.** В текущем коде все пять требуемых кнопок предусмотрены; поля сортировки соответствуют сохранённому API. Подтверждения исправления на указанном в Jira окружении нет. Тестовое доказательство частичное: найдены проверки действий для «Начало» и «Поверхность», но не полная матрица пяти кнопок и обоих направлений.

Изменений файлов, исторических ledger и feature-checkboxes не выполнялось. Тесты, браузер, сеть и API не запускались.

## 1. Источник и атомарные требования

Обозначения:
- **S**: `audit/sources/jira-subtasks/r1/content.json`, относительно `openspec/changes/reconcile-control-center-backlog/`.
- **W**: `audit/sources/wiki-241085439/r1/content.json`.

S `$.items[6]`, строки 128–152: статус `Backlog`, обновление `2026-10-16T18:39:35.845+0800`; описание — строка 135. Шаги: открыть «Диалоги», проверить кнопки сортировки таблицы. Заявленный ФР: отсутствуют четыре кнопки, кроме «Начало».

| Атом | Expected — S `$.items[6].description`, ОР | Уточнение W `$.bodyView`, §3.1.3 | Observed |
|---|---|---|---|
| R1 | Кнопка «Начало» | `started_at`, `-started_at`; default `-started_at` | Есть в конфигурации колонок |
| R2 | Кнопка «Завершение» | `ended_at`, `-ended_at` | Есть |
| R3 | Кнопка «Поверхность» | `channel`, `-channel`; по отображаемому названию | Есть |
| R4 | Кнопка «Оценка работы оператора» | `operator_rating`, `-operator_rating`; числовая оценка | Есть |
| R5 | Кнопка «Время» | `duration`, `-duration`; по `duration_sec` | Есть |

Общий точный кодовый локатор: `app/pages/dialogs/constants/dialogs.constants.ts:19–25`, массив `dialogColumns`. Для каждой записи `app/pages/dialogs/ui/dialog-table.tsx:49–68` создаёт `Button` с соответствующим текстом и обработчиком `onSort`.

Из источника **не следует** требование отдельной постоянно видимой иконки для неактивной сортировки: ОР требует кнопки. В коде стрелка показывается только у активного поля; этого недостаточно для объявления нового дефекта.

## 2. API: применимость и ограничения

API применим непосредственно: кнопки выбирают серверный `sort`, а не сортируют загруженную страницу.

- W `$.bodyView`, §§3.1.1, 3.1.3–3.1.4: `POST /api/control/api/dialogs/v1/dialogs/search`, пять полей в обоих направлениях, default `-started_at`.
- `docs/api/contracts/dialogs.openapi.json#/components/schemas/DialogListSort` (строки 1013–1028): все десять соответствующих значений enum.
- Там же `#/components/schemas/DialogSearchRequest/properties/sort`: ссылка на `DialogListSort`, default `-started_at`.
- `docs/api/contracts/dialogs.md:73–84`: тот же endpoint и семантика сортировки.
- `app/entities/dialog/api/dialog-selection-schema.ts:130–146`: клиентская схема допускает те же десять значений.
- `app/entities/dialog/api/dialog-client.ts`, `searchDialogs`: POST через общий клиент после валидации тела.

Сохранённые правила: дополнительный ключ `chat_id` в том же направлении, nulls-last независимо от направления, сравнение `channel` без регистра. Cursor связан с selection/sort; смена сортировки требует новой цепочки страниц. Неизвестный или пустой `sort` — `422 VALIDATION_ERROR`.

Эти правила серверного упорядочивания не доказываются наличием фронтенд-кнопок. Реальный backend и доступность ЕСК не проверялись. Публикация wiki v15 также сама по себе не доказывает runtime или принятие всех её разделов; для рассматриваемого поля расхождения с локальным опубликованным контрактом не обнаружены.

## 3. OpenSpec owner

**Текущий owner:** `openspec/specs/dialog-registry/spec.md`, requirement **“Cursor pagination preserves request identity”**:

- все пять полей, оба направления, default `-started_at`;
- запрет неподдержанной сортировки обращения;
- сброс цепочки при смене сортировки;
- сохранение серверного порядка.

Requirement **“Registry represents server rows faithfully”** определяет соответствующие колонки. Requirement **“Counts and request states remain truthful”** требует доступного управления таблицей.

**Исторический владелец реализации:**  
`openspec/changes/archive/2026-10-05-mos-1037-dialog-registry/specs/dialog-registry/spec.md:44–46` — то же требование сортировок. В `tasks.md`, пункты 2.3 и 3.2, уже отмечены реализация курсорного состояния и сортировок. Эти отметки — исторические сведения, не результат данного аудита.

Другой найденный delta для этой capability —  
`openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/dialog-registry/spec.md` — относится к явному применению быстрых фильтров; отдельным owner MOS-1422 не является.

**Spec coverage:** поведенческое требование покрыто. Отдельного сценария «одновременно доступны пять кнопок с указанными подписями» нет, но это не основание создавать дублирующий функциональный change при существующих требовании и реализации.

## 4. Код и тестовые доказательства

### Код

- `dialog-table.tsx:49–68`: для всех пяти колонок создаются настоящие кнопки; `aria-sort` отражает состояние. Нажатие активного восходящего поля переключает на `-field`; иначе выбирается `field`.
- `app/pages/dialogs/ui/dialog-registry.tsx:22–26`: default `-started_at`, строки объединяются из серверных страниц без локального пересортирования.
- Там же передача `sort={sort}`, `onSort={setSort}` в `DialogTable`.
- `app/entities/dialog/model/use-dialogs-query.ts:24–36`: sort входит в query key; первая страница использует `cursor: null`; запрос передаёт selection/sort/limit/cursor.
- Таблица выводится при полученных непустых результатах (`dialog-registry.tsx`, ветка `latest` / `rows.length`). В empty/loading её заголовков нет. Jira не задаёт сценарий пустой выдачи, поэтому это **ограничение наблюдения**, а не установленное нарушение R1–R5.

### Существующие тесты — прочитаны, не запущены

- `app/pages/dialogs/ui/dialogs-page.test.tsx:82–121`: нажатие кнопки «Начало»; mock обрабатывает `sort: 'started_at'`, проверяется появление соответствующей строки.
- Там же `:302–347`: нажатие «Поверхность»; проверка тела `{ sort: 'channel', cursor: null }`.
- `app/entities/dialog/model/use-dialogs-query.test.tsx:75–80`: последовательные страницы сохраняют `sort: 'channel'`.
- Там же `:87–122`: смена selection и sort на `duration`, отмена старого continuation и запрос без старого cursor. Это не тест кнопки «Время» и не изолированная смена только sort.

**Unknown:** прохождение тестов на данном HEAD; полноценная проверка пяти кнопок, повторных нажатий и `aria-sort`; реальное серверное упорядочивание; визуальное состояние указанного Jira-контура.

## 5. Findings и минимальная рекомендация

1. **Расхождение исторического ФР с текущим кодом:** отсутствие четырёх кнопок статически не подтверждается. Все пять генерируются единым механизмом.
2. **Частичная регрессионная доказательность:** существующие прочитанные UI-тесты не перечисляют все пять кнопок и оба направления. Это test-evidence gap, не доказанный функциональный дефект.
3. `audit/coverage.json` имеет `complete: false`, `acceptedEvidenceThrough: D-089`; отдельного перехода MOS-1422 нет. Исторический `audit/reports/G2-JIRA-MEMBER-JOINS.md:302` содержит MOS-1422 как `U/UN`. Данный отчёт не меняет population и не объявляет delivery.

**Keep:** текущие main spec, API и реализацию; не создавать отдельный feature-change только ради повторного добавления существующих сортировок.

**Минимальный следующий шаг при необходимости усиления приёмки:** добавить в существующий `app/pages/dialogs/ui/dialogs-page.test.tsx` параметризованный component-тест: непустая серверная выдача → доступны пять именованных кнопок → каждое поле отправляет оба направления и новый `cursor: null`; проверять default `-started_at` и отсутствие сортировки у «Обращение и участники». Это рекомендация будущей проверки, не выполненное изменение.

После независимого ревью родитель может добавить bounded evidence-link на этот отчёт в актуальное продолжение аудита. Исторические строки, архивные tasks и feature-checkboxes сохраняются; закрытие Jira и deployment не выводятся из статического анализа.

## 6. SHA256 прочитанных ключевых входов

Префикс `A` = `openspec/changes/reconcile-control-center-backlog/audit/`.

| Вход | SHA256 |
|---|---|
| `A/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `A/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `A/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `A/sources/wiki-241085439/r1/content.json` | `974ea35aaf44b9ec7c14c573ba58bdf7ed55397a9ca47d62b37fb39d9886f8bc` |
| `A/sources/wiki-241085439/r1/metadata.json` | `dcaab775172b7e615dfae64184d719f8403cff1fb304650ba21e1532ce577b7d` |
| `A/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `openspec/specs/dialog-registry/spec.md` | `ef9e52b7dba2ff4f0fa1dd1a9fa3d7cfaa78890277c376d70ed0301423bf6f83` |
| `openspec/changes/archive/2026-10-05-mos-1037-dialog-registry/specs/dialog-registry/spec.md` | `742762a4b4565370424c79645372cfdfe46007423842d88eba20a3376fc1d17d` |
| `docs/api/contracts/dialogs.openapi.json` | `a0d798f7647f7ed5c66bdf9a39113ab4da25d5d358311068d34baaef5f9ab648` |
| `app/pages/dialogs/constants/dialogs.constants.ts` | `ff44d72901017a14b4271601c080fa98c7cbc51026a4fa4b896fc7ce4cf315f9` |
| `app/pages/dialogs/ui/dialog-table.tsx` | `c0a286d80894f7591bcd9882d25cc8ae87a80faddbe150f26f6f0597588366f3` |
| `app/pages/dialogs/ui/dialogs-page.test.tsx` | `3dba3eb88505d29a2ed80dab6c301e0496007e85a26749d74b80a747824d2fec` |

Хеши content совпали с сохранёнными metadata. Jira-вложения `839906`, `839905` представлены только метаданными: содержимое не скачано и не исследовано. Комментарии/custom acceptance fields отсутствуют в сохранённой выборке. Свежесть внешних источников не проверялась.