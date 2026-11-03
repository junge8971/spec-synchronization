# API-MOS-1322-r2 — API-доказательства точного backend issue

## Результат и границы

Новое тело **MOS-1322** позволяет выполнить точный requirement→API join. В сохранённом live OpenAPI r2 и локальном контракте представлены требуемые семейства операций KB, DTO агрегата, поиска, справочников, сохранённых фильтров и CSV. **Это частичное контрактное доказательство, не подтверждение выполнения backend DoD.**

Обнаружено расхождение security: live описывает альтернативные схемы авторизации, local — совместное требование двух схем. Схемы данных проверенного среза совпадают. Мягкое удаление, атомарность, сохранение порядка ссылок, уникальность, миграции, начальное заполнение справочников и backend-тесты остаются **unknown**.

Прочитаны D-091 и `R-D091-RECOVERY`: прежний missing-body вывод сохраняется как исторический; новый пакет снимает только эту предпосылку для нового анализа. Прежний `JOIN-MOS-1322` использован как карта путей, не как доказательство требований. Frontend/module coverage не присваивается backend issue.

## Обозначения и provenance

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`.
- `J` = `A/sources/jira-optional-backend-details/r1/content.json`.
- `L` = `A/sources/api-live/r2/content.json`.
- `C` = `docs/api/contracts/managed-resources.openapi.json`.
- `M` = `/api/control/api/v1/managed-resources`.
- `K` = `M/knowledge-base`.
- `S(X)` = `#/components/schemas/X`; пути ниже — точные ключи `#/paths` в L и C.
- W1–W7 и D1–D7 — порядковые пункты разделов «Что делаем» и DoD строки `J#/items/0/description`, начиная с 1.

`J#/items/0`: MOS-1322, `[B] Реализовать раздел "База знаний"`, Hold, updated `2026-10-14T14:03:51.688+0800`. Пакет получен `2026-10-20T14:35:05.335Z`. Metadata ограничивает состав: без comments, attachments и custom acceptance fields; `parent:null` не отрицает модульную принадлежность. MOS-1142 — только зависимость из W1, её тело не открывалось.

L — сохранённая публикация OpenAPI 3.1.0 от `2026-10-19T08:11:44.238Z`, не текущая проверка сервиса. Business endpoints не вызывались.

## Атомарная сверка требований

| Источник требования | Наблюдаемое API-доказательство L и C | Граница / unknown |
|---|---|---|
| W1, D2: создание | `K/entries` POST: `KnowledgeBaseEntryCreate` → 201, envelope `EntityCreatedResponse` | Сохранение в backend не проверено |
| W1, D2: просмотр | `K/entries/{entity_id}` GET: UUID → 200, `KnowledgeBaseEntryResponse` | Реальные данные и not-found поведение неизвестны |
| W1, D2: изменение | Тот же путь PUT: `KnowledgeBaseEntryPatch` → 200, полный response DTO | Название операции `Patch Kb Entry`; семантика null/omitted и замены коллекций из одного DTO не устанавливается |
| D2: мягкое удаление | Тот же путь DELETE → 200, `ManagedResourceDeletedResponse` с `id` | Декларация DELETE не доказывает soft delete; соответствующей гарантии в операции нет |
| W2, D3: карточка, ссылки, связи с навыками | `S(KnowledgeBaseEntryCreate/Patch/Response)`: `links`, `skill_ids`, `display_rules`; ссылки представлены отдельными DTO | Один aggregate request не доказывает транзакционность. Модель таблиц, миграции и rollback неизвестны |
| D3: порядок ссылок | `links` — массив; `KnowledgeBaseLinkResponse` возвращает `id` | Массив позволяет передать порядок, но гарантии сохранения порядка при записи/чтении нет |
| W3, D4: централизованные справочники | `M/catalogs/lookups/{section}` GET; `CatalogLookupSectionName` включает `knowledge-base`. Есть `catalogs/{entity_id}/values` GET/POST и `.../values/{value_code}` PUT/DELETE | Наличие общего API не доказывает регистрацию конкретных KB-справочников и их seed-значения |
| W4: метаданные привязок формы | `K/metadata` GET → словарь `ManagedResourceMetadata`; `catalog_bindings` → `ManagedResourceCatalogBindingMetadata` с `catalog`, `value_field`, `multiple` | Конкретные bindings и содержимое metadata ответа не сохранены |
| W5, D2: поиск | `K/entries/search` POST, `S(kb_entryListQuery).properties.query`: nullable string 2–200; ответ items + pagination | Полнотекстовая семантика и фактическая выдача неизвестны |
| W5: обычные фильтры | `kb_entryListQuery`: `status`, `category_code`, `skill_ids`; scalar либо массив через общие filter DTO | Реальная композиция фильтров не доказана |
| W5: сложные условия | `kb_entryConditions`: `logic=and/or`, до 50 `kb_entryCondition`; enum полей/операторов и типизированный `value` | Это плоская группа условий; Jira не задаёт обязательную рекурсивную вложенность. Недостаточность модели из body не следует |
| W5, D5: сохранение условий | `M/saved-filters` POST/GET; `M/saved-filters/{filter_id}` GET/PUT/DELETE. `ManagedResourceSavedFilterCreate`: `resource=knowledge-base-entries`, `name`, `search` | `search` — свободный object: контракт не фиксирует соответствие `kb_entryListQuery`, правила доступа/валидации содержимого неизвестны |
| W6, D5: CSV всего отбора | `K/entries/export` POST: `kb_entryExportRequest` с `fields` и `search` → 200 `text/csv`, binary | `search` ссылается на DTO с limit/offset; игнорирование пагинации при экспорте всего отбора декларацией не гарантировано |
| W6, D5: CSV карточки с выбором полей | `K/entries/{entity_id}/export` POST: `kb_entryDetailExportRequest.fields` → 200 `text/csv` | Фактический CSV, порядок колонок и содержимое не проверены |
| W7: валидация полей | Ограничения DTO и 422 `HTTPValidationError` у операций с входными данными | Понятность фактических сообщений не установлена |
| W7: связи и уникальность | `skill_ids` — UUID, ссылки имеют URI и ограничения длины; общий `ErrorItem` допускает field/code/message | Существование связанных объектов, уникальность и конкретные domain-error codes не описаны этими ограничениями |
| D6: prefix, общий формат, доступ | KB-пути под K; JSON success envelopes содержат `code/data/message/errors`; CSV отдельно. У операций объявлен security | Проверка permissions backend неизвестна; security L/C расходится, см. ниже |
| D7: OpenAPI и тесты | Операции и DTO присутствуют в обоих OpenAPI | Полнота документирования ошибок и backend-покрытие тестами не доказаны |
| D1: согласованная storage-модель и миграции | API представляет предметный агрегат | OpenAPI не является storage/migration evidence; вне API lane, unknown |

## DTO и errors: существенные детали

Точные локаторы — `L/C# /components/schemas` без пробела, имена ниже:

- `KnowledgeBaseEntryCreate.required`: `name`, `code`, `category_code`. Ограничения: name 1–255; code ≤100 и `^[a-z][a-z0-9_]*$`; category_code 1–50; links/skill_ids максимум 100. `additionalProperties=false`.
- `KnowledgeBaseEntryPatch`: поля необязательны, большинство допускают null; это описание формы запроса, не доказанная persistence-семантика.
- `KnowledgeBaseLink`: обязательны title и url; id необязателен. `KnowledgeBaseLinkResponse`: id обязателен. URL — string `format=uri`, 1–1024; конкретная разрешённая схема URL здесь не определена.
- `kb_entryDetailExportRequest.properties.fields`: 1–100 элементов из enum `name`, `code`, `category_code`, `skill_names`, `links_count`, `status`, `description`, `owner`, `tags`, `material_type`, `language`, `valid_until`.
- `ManagedResourceMetadata.properties.export_max_rows`: default 10000. Это декларация настройки, не подтверждённый фактический лимит сервиса.
- `HTTPValidationError.properties.detail` → `ValidationError` с обязательными `loc`, `msg`, `type`.
- Общий `ErrorItem` содержит nullable `field`, `code`, `details` и обязательный `message`; `ResponseCode` — свободная строка.
- У KB-операций заявлены success и, кроме metadata, 422; явных response entries для 401/403/404/409/500 нет. Отсутствие в OpenAPI не означает отсутствие этих ответов в backend.
- Код `EXPORT_LIMIT_EXCEEDED` и конкретные ошибки уникальности/связей не закреплены в рассмотренных operation responses. Нельзя вывести их наличие либо отсутствие в runtime из свободного `ResponseCode`.

## Live r2 против local

Выполнено структурное сравнение ограниченного среза KB + его общих catalogs/saved-filters dependencies:

- 18 path objects; после исключения `security` различий нет.
- 65 транзитивно достижимых schema objects: различий нет.
- Все path objects C совпадают с соответствующими объектами `docs/api/contracts/openapi.json`.
- **Security drift:** например, `L#/paths[K/entries]/post/security` — `[{"AdminToken":[]},{"AccessToken":[]}]`, то есть альтернативы **OR**. В C и merged local — `[{"AdminToken":[],"AccessToken":[]}]`, то есть **AND**. Аналогичное различие видно у KB metadata/search/detail/export и общих операций.
- Это расхождение декларации контракта; оно не доказывает способ отправки credentials клиентом, backend enforcement или разрешённую auth-модель. Автоматически менять credentials/security на основании этого отчёта нельзя.
- DTO не регенерировались; generated TypeScript и frontend runtime validators не использованы как замена backend evidence.

## Безопасные предложения

**keep**
- Сохранить существующие операции/DTO и исторические отчёты; не создавать дубли CRUD, export или filters по факту нового body.
- Сохранить границу API declaration ≠ backend implementation ≠ deployment.

**update**
- После пакетного review добавить точный member-level API join MOS-1322: новый body доступен, перечисленные требования имеют частичное контрактное подтверждение.
- Зафиксировать security drift и недокументированные backend-семантики как вопросы контрактного согласования, не как доказанные backend-дефекты.
- Решение о coverage принимает parent; данный отчёт сам ledger/status не меняет.

**new**
- Новый feature/corrective change этим API lane не обоснован. Уточнение существующего контракта возможно только после подтверждения неизвестных семантик и проверки уже действующих владельцев.

**question**
- Какова согласованная security-семантика OR/AND и где нормативно закреплены permissions?
- Где сохранены backend-доказательства soft delete, атомарности, порядка links, уникальности и проверки связей?
- Как экспорт обеспечивает весь отбор при наличии limit/offset в search DTO?
- Каковы реальные domain errors и их полевые локаторы, включая uniqueness, invalid relation, not-found и export limit?
- Где подтверждены seed/bindings справочников, миграции и backend-тесты? Зависимость MOS-1142 фиксировать без открытия чужого scope.

## SHA256 входов

Хэши вычислены локально по полным байтам.

| Вход | SHA256 |
|---|---|
| `A/work-items/WAVE-D092-OPTIONAL-BODIES.md` | `c2aed44985c2515b20c54e238d589ab997592c5c3d39d896bb1d3bb3485a15b3` |
| J | `3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618` |
| `A/sources/jira-optional-backend-details/r1/metadata.json` | `9357e481e237e04c47258fe4efb4bcc3d8377e2690e75963653d2275885ff4fc` |
| L | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `A/sources/api-live/r2/metadata.json` | `444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba` |
| C | `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `A/decisions.md` — прочитан D-091 | `fa7cffedb00f4d481efa2b523e8f1a1b4991b2750022c823c30c5370ab5cf945` |
| `A/reviews/R-D091-RECOVERY.md` | `f6fb801733ee223979debb0277de15e8f97448a3a69db6a2fb0f42f35c03e45d` |
| `A/reports/JOIN-MOS-1322.md` | `7a4d665bb17b268b3228a4dbc6d725f8235d7375ab957211a9e8c03b687a87c0` |