# API-MOS-1323-r2 — операции, DTO и ошибки

## Результат и границы

Новое тело **MOS-1323** позволяет выполнить предметный API-join: сохранённый live OpenAPI r2 и локальный контракт содержат операции и DTO для управления **настройками** экспериментов. Это не доказательство выполнения backend DoD.

Выявлены:
- совпадение 38 достижимых схем DTO в проверенной области;
- единственное различие 14 проверенных операций — `security`: **OR в live r2 против AND локально**;
- недостаточная документированность серверных бизнес-инвариантов и ошибок, прямо требуемых новым body.

Прочитаны `decisions.md`, раздел D-091, `work-items/RECOVERY-D091.md` и `reviews/R-D091-RECOVERY.md`. Прежний missing-body вывод исторически корректен; новый пакет снимает только этот source gap. Исторические отчёты, failed provenance и coverage не изменяются. Configuration ≠ execution: статистика, распределение реального трафика и запуск эксперимента этим API-join не подтверждаются и не добавляются в scope.

## Источники и адресация

`A` = `openspec/changes/reconcile-control-center-backlog/audit/`.

- **J** = `A/sources/jira-optional-backend-details/r1/content.json`, `$.items[1]`: MOS-1323, Hold, updated `2026-10-14T14:03:53.543+0800`.
- В `J:$.items[1].description` обозначения **W1–W8** — последовательные пункты «Что делаем», **D1–D10** — последовательные пункты DoD. Это атомарные локаторы внутри строки description.
- **L** = `A/sources/api-live/r2/content.json`.
- **C** = `docs/api/contracts/managed-resources.openapi.json`.
- **B** = `docs/api/contracts/openapi.json`.
- **P** = `/api/control/api/v1/managed-resources`.
- `S(Name)` = `$.components.schemas.Name`; операция адресуется как `$.paths["полный путь"].method`.

Metadata J: selected-field extraction от `2026-10-20T14:35:05.335Z`; комментарии, вложения и custom acceptance не собраны. `parent:null` не отрицает модульную принадлежность. Зависимость MOS-1142 указана в W1; её задача не открывалась.

Metadata L: сохранённая публикация OpenAPI от `2026-10-19T08:11:44.238Z`, не текущий сетевой ответ и не deployment evidence.

## Атомарный requirement → API join

| Требование J | Наблюдение в L и C | Ограничение / unknown |
|---|---|---|
| **W1, D2:** CRUD экспериментов | `P/ab-testing/experiments.post`: `ABExperimentCreate` → 201, envelope с `EntityCreatedResponse.id`. `P/ab-testing/experiments/{entity_id}`: GET/PUT → 200 `ABExperimentResponse`; DELETE → 200 `ManagedResourceDeletedResponse`. | Наличие DELETE не доказывает именно мягкое удаление. Реальное выполнение CRUD неизвестно. |
| **W2, D1:** карточка, группы, связи, модель хранения и миграции | `S(ABExperimentCreate)` и `S(ABExperimentResponse)` содержат карточку, `groups`, `surface_ids`. | DTO не удостоверяют таблицы, миграции или соответствие согласованной модели хранения. |
| **W3:** аудитория, метрика, режим запуска, даты, статус | `S(ABExperimentCreate).properties`: `audience_code`, `segment`, `metric_code`, `launch_mode`, `started_on`, `ended_on`, `status`; defaults соответственно `all`, `manual`, `draft` там, где заданы. Даты имеют format `date`. | Сохранение полей не означает исполнение эксперимента. Допустимые значения справочников и runtime-переходы статусов из этих строковых DTO не устанавливаются. |
| **D3:** атомарность карточки, групп и поверхностей | Один create/PUT request объединяет карточку и обе коллекции. | Транзакционная атомарность из структуры запроса не следует. |
| **D3:** сохранение порядка и идентификаторов групп | `S(ABGroup)` имеет необязательный UUID `id`; `S(ABGroupResponse)` требует `id`. Группы передаются массивом. | Не описаны гарантии сохранения порядка, обработки неизвестного/повторного ID и удержания ID существующих групп. Наличие массива не доказывает серверное сохранение порядка. |
| **D6:** частичный PUT сверху | `P/ab-testing/experiments/{entity_id}.put` использует `S(ABExperimentPatch)`; у схемы нет списка `required`, свойства допускают null. Summary — `Patch Ab Experiment`. | Это структурно совместимо с partial PUT, но operation description отсутствует. Семантика omitted против null не разъяснена. |
| **D6:** переданные группы и поверхности заменяются целиком | `S(ABExperimentPatch).properties.groups/surface_ids` — nullable массивы. | Полная замена коллекций явно не описана. Ограничения массивов сохраняются: groups 2–100, surfaces 1–100; допустимость null в схеме не объясняет его бизнес-смысл. |
| **W8, D4:** распределение, теги, аудитория, даты | `S(ABGroup)`: percent — integer 0–100, name/tag непустые; `S(ABExperimentCreate)` требует name/code/groups/surface_ids, ограничивает формат code и UUID поверхностей. | Нет выраженных cross-field правил суммы долей, уникальности тегов, обязательных параметров выбранной аудитории и порядка дат. Числовой итог суммы body не задаёт — не подменяется догадкой. |
| **W8:** связи и уникальность | DTO определяют UUID связей и формат code. | Проверка существования/доступности поверхностей, уникальность эксперимента и соответствующие ошибки не специфицированы проверенными операциями. |
| **D5:** запрет изменения тегов существующих групп вне «Черновика» | Patch содержит status и groups; группа содержит id/tag. | Stateful-запрет в схемах и описании PUT не отражён. Это gap документации, не установленный дефект backend. |
| **W4–W5, D7:** общие справочники и metadata | GET `P/ab-testing/metadata`; GET `P/catalogs/lookups/{section}`, `S(CatalogLookupSectionName)` включает `ab-testing`. `S(ManagedResourceMetadata)` содержит `catalog_bindings`; binding задаёт catalog/value_field/multiple. Есть общие операции `P/catalogs/{entity_id}/values` GET/POST и `.../{value_code}` PUT/DELETE. | Наличие общих операций не удостоверяет seed-значения, фактическую регистрацию A/B-справочников или содержимое metadata. Ответы этих методов не собраны. |
| **W6, D2:** поиск и обычные фильтры | POST `P/ab-testing/experiments/search` → paginated response. `S(ab_experimentListQuery)`: query, sort, limit/offset; status, metric_code, audience_code, launch_mode, surface_ids. | Реальная корректность отбора неизвестна. |
| **W6:** сложные условия | `S(ab_experimentConditions)` задаёт and/or и до 50 условий; `S(ab_experimentCondition)` — field/operator/value, включая `groups_count`. | Поддержка заявлена структурой DTO; вычисление условий не проверялось. |
| **W6, D8:** сохранение условий | `P/saved-filters`: POST/GET; `P/saved-filters/{filter_id}`: GET/PUT/DELETE. `S(ManagedResourceSavedFilterCreate)` требует resource/name/search, enum resource включает `ab-experiments`. | `search` — произвольный object; его соответствие A/B query и серверная проверка не выражены этой схемой. |
| **W7, D8:** CSV списка и карточки с выбором полей | POST `P/ab-testing/experiments/export` и `.../{entity_id}/export`: 200 `text/csv`, binary. `S(ab_experimentExportRequest)` требует fields и принимает search; detail request требует fields. | Экспорт **всего отбора**, независимо от пагинации внутри search, явно не гарантирован. `ManagedResourceMetadata.export_max_rows` имеет default 10000; поведение при превышении лимита неизвестно. |
| **D9:** общий префикс, формат ответов и доступ | Все перечисленные операции под P; JSON-успехи используют `TsamResponseSchema_*` с code/data/message и errors; CSV имеет отдельный media type. Security присутствует. | Реальный permission enforcement неизвестен; обнаружено различие security между публикацией и local, ниже. |
| **W8, D10:** понятные ошибки по полям, OpenAPI и тесты | `S(ErrorItem)` поддерживает field/code/message/details; в операциях обычно объявлены success и 422 `HTTPValidationError`, у metadata только 200. | Ошибки бизнес-инвариантов и тесты backend не доказаны. Наличие OpenAPI покрывает только документальную часть D10. |

## Live r2 против local: точные результаты

Область сравнения: семь A/B операций плюс metadata, lookup раздела и пять операций общих saved-filters — **9 path items, 14 операций**.

1. **Операции:** у каждой из 14 операций L против C отличается только поле `security`. Та же разница подтверждена против B:
   - L: `[{"AdminToken":[]},{"AccessToken":[]}]` — альтернативные способы, **OR**.
   - C и B: `[{"AdminToken":[],"AccessToken":[]}]` — оба способа в одном requirement object, **AND**.

   Локатор-пример: `L/C/B:$.paths[P+"/ab-testing/experiments/{entity_id}"].put.security`. Различие относится к документированию доступа; оно не доказывает, какие credentials реально требует сервер или отправляет клиент.

2. **DTO:** рекурсивно пройдены `$ref` от указанных path items. Все **38 достижимых схем L совпадают с C**, включая create/patch/response, группы, поиск, export, metadata, saved-filters и ошибки. Это структурное сравнение JSON, не генерация DTO и не тест API.

3. **Ошибки:** `responses["422"]` ссылается на `HTTPValidationError` → `ValidationError` (`loc/msg/type`), тогда как общий envelope использует `ErrorItem` (`field/code/message/details`). Наличие обоих типов не определяет фактический формат ошибок распределения, тегов, аудитории, дат, связей и уникальности. У проверенных A/B операций отсутствуют явные ответы 401/403/404/409/500 и бизнес-примеры. Нельзя объявлять отсутствие этих ответов в runtime — обнаружена ограниченность публикации.

## Безопасные рекомендации

- **keep:** существующие операции и DTO как подтверждённый контрактный каркас; configuration-only границу; исторические JOIN/D091 без переписывания. Не выводить завершённость MOS-1323 из frontend/module coverage.
- **update:** после независимого review добавить exact-member API-join к новому body. Отдельно согласовать синхронизацию `security` OR/AND в существующем контрактном/auth owner; это не основание менять модель авторизации по инициативе данного lane.
- **update:** уточнить существующую OpenAPI-документацию partial PUT, omitted/null, полной замены коллекций, group identity/order, stateful-запрета тегов, ошибок cross-field validation и экспорта всего отбора. Сначала установить фактическую серверную семантику; не «исправлять» backend по одному пробелу схемы.
- **question:** нужны сохранённые серверные contract/test evidence для перечисленных инвариантов, error payloads/status codes, soft delete, атомарности, seed/binding metadata и export pagination/limit behavior.
- **new:** новая capability или feature-change из данного сравнения не требуется. При необходимости — узкий доказательный follow-up внутри существующих owners, без статистики, traffic execution и открытия MOS-1142.

## SHA256 входов

Хэши вычислены локально по полным байтам.

| Вход | SHA256 |
|---|---|
| A/sources/jira-optional-backend-details/r1/content.json | `3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618` |
| A/sources/jira-optional-backend-details/r1/metadata.json | `9357e481e237e04c47258fe4efb4bcc3d8377e2690e75963653d2275885ff4fc` |
| A/sources/api-live/r2/content.json | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| A/sources/api-live/r2/metadata.json | `444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba` |
| docs/api/contracts/managed-resources.openapi.json | `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf` |
| docs/api/contracts/openapi.json | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| A/reports/JOIN-MOS-1323.md | `86a89f81d8b8baa87b6566f85abe71e68b0eebb22d1916229db7339de4ef653b` |
| A/reviews/R-D091-RECOVERY.md | `f6fb801733ee223979debb0277de15e8f97448a3a69db6a2fb0f42f35c03e45d` |
| A/work-items/RECOVERY-D091.md | `442463eafea55249074ac3d32e44eae1515c035eb998c781bc337a1e42bbf3f6` |
| A/work-items/WAVE-D092-OPTIONAL-BODIES.md | `c2aed44985c2515b20c54e238d589ab997592c5c3d39d896bb1d3bb3485a15b3` |
| A/decisions.md | `fa7cffedb00f4d481efa2b523e8f1a1b4991b2750022c823c30c5370ab5cf945` |

## Проверки и остаточные риски

Выполнены только локальное чтение, извлечение JSON, структурное сравнение и SHA256. Файлы не записывались. Тесты, браузер, сеть, business API, Git-мутации и вложенные агенты не использовались. Git/staging не проверялись.

Главный остаточный риск — контракт описывает форму данных, но не удостоверяет серверные инварианты, доступ, хранение или deployment. Успешность тестов и полное выполнение MOS-1323 неизвестны.