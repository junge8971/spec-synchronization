# IMPL-MOS-1323-r2 — статические доказательства реализации

## Результат и границы

Новое тело **MOS-1323** позволяет сопоставить точные backend-требования с локальным кодом и текстами тестов. Найдены существенные **mock/client evidence**, включая partial PUT, замену коллекций, сохранение идентификаторов групп и запрет изменения тегов вне черновика. **Реализация production backend, миграции, транзакции, серверная авторизация и deployment неизвестны.**

Это additive-продолжение `JOIN-MOS-1323.md`, а не пересмотр его исторического вывода. Прочитаны D-091 в `audit/decisions.md`, `work-items/RECOVERY-D091.md` и `reviews/R-D091-RECOVERY.md`: прежнее отсутствие тела относилось к старому пакету; failed runtime provenance сохраняется. Изменения coverage принимает только parent после review. Полный аудит модуля, API-сравнение и owner mapping здесь не выполнялись.

Обозначения:
- `A` = `openspec/changes/reconcile-control-center-backlog/audit`.
- `S` = `A/sources/jira-optional-backend-details/r1/content.json#/items/1/description`.
- `S:L<n>` — строка декодированного description, нумерация с 1 через `splitlines()`.
- `M` = `mocks/ab-testing`; `F` = `app/optional/ab-testing`.
- Имена функций и точные названия тестов ниже — локаторы внутри указанных файлов.

## Источник

`content.json#/items/1`: ключ MOS-1323, статус Hold, updated `2026-10-14T14:03:53.543+0800`. Сбор `2026-10-20T14:35:05.335Z`.

`metadata.json#/limitations` ограничивает доказательства: комментарии, вложения и custom acceptance fields не собраны; `parent:null` не отменяет модульную принадлежность; linked MOS-1142 не открывался. Статус и timestamp не доказывают состояние реализации.

## Requirement → observed → unknown

| Требование точного issue | Наблюдаемое локальное доказательство | Ограничение |
|---|---|---|
| CRUD через managed-resources, включая мягкое удаление — S:L7,L19 | `M/handlers.mjs`: `save`, `detail`, `experiments`, `abTestingHandlers`; `mocks/managed-model.mjs#managedResources` регистрирует `ab_experiment`. `M/aggregate.test.mjs`, тест `A/B aggregate roundtrip preserves group IDs/order, replaces collections and soft deletes; restart resets seed`: создание, чтение, PUT, DELETE, 404 после удаления, исключение из поиска/экспорта при сохранении записи в массиве. | Это in-memory mock. Исполнение backend CRUD и соответствие реализации MOS-1142 неизвестны. |
| Таблицы карточки, групп, связей; модель и миграции — S:L8,L18 | `M/seed.mjs#initializeAbTesting` создаёт состояние; `M/model.mjs#experimentResponse` формирует агрегат. | Эти структуры не являются таблицами или миграциями. Доказательств схемы БД и согласованной серверной модели в изученных входах нет. |
| Настройки аудитории, метрики, запуска, дат, статуса — S:L3,L9 | `F/api/ab-testing-schema.ts#abTestingFieldsSchema`; `M/model.mjs#catalogBindings`; `M/validation.mjs#validateRules`. Тест `A/B boundaries accept 100 groups, zero percent and full rules, and immutable tag uses saved status` сохраняет scheduled/start date/segment/status. | Сохранение параметров не означает распределение реального трафика, scheduler или исполнение эксперимента. |
| Начальные справочники и metadata — S:L10–11 | `M/seed.mjs#catalogs`, `M/model.mjs#metadata`, `M/handlers.mjs#abTestingHandlers`; тест `A/B metadata and section lookup registrations coexist with KB and generic catalogs` проверяет четыре набора и bindings. `F/api/ab-testing-client.ts#getAbTestingMetadata,getAbTestingLookups` использует общий API. | Это локальные fixtures и клиент API, не доказательство централизованного backend-реестра. |
| Централизованное изменение значений через «Справочники» — S:L24 | A/B lookup читает `state.managed.abTesting.catalogs`; generic `mocks/managed-catalogs.mjs#saveValue` изменяет `state.values[parent.id]`. | В прочитанной реализации не показана связь этих хранилищ. Тест metadata проверяет чтение, не изменение через общий CRUD справочников. Централизованная изменяемость A/B значений не подтверждена даже представленными mock-тестами. Это не установленный production-дефект. |
| Поиск, обычные/сложные/сохранённые фильтры — S:L12,L19,L25 | `M/handlers.mjs#search` использует общий `searchManaged`; `M/validation.mjs#validateSearch,savedAbTestingSearch`. `M/search-export.test.mjs`: тесты `A/B query, AND/OR, exact equality, quick filters and sorting run before pagination` и `A/B search and saved filters reject unsupported/malformed selection atomically and persist complete search by ID`. `M/saved-filter-interoperability.test.mjs` содержит roundtrip через frontend codec. | Наличие утверждений в тестах не означает их прохождение; долговечное серверное хранение фильтров неизвестно. |
| CSV всего отбора и карточки с выбранными полями — S:L13,L25 | `M/handlers.mjs#exportExperiments` и ветка `export_ab_experiment` передают полный результат поиска, без `page`. Тест `A/B both CSV endpoints deliver genuine UTF-8 BOM, ordered Russian headers, summaries and formula-safe full selection` проверяет обе операции, порядок полей, выборку сверх страницы, невалидные поля и лимит. | Это локальная модель поведения CSV; реальный backend-экспорт неизвестен. Число 10000 и форматирование не извлекаются как новые требования из MOS-1323. |
| Валидация долей, тегов, аудитории, дат, связей и уникальности; ошибки по полям — S:L14,L21 | `M/validation.mjs#validateGroups,validateRules,validateReferences,validateExperiment,fieldFailure`: сумма 100, уникальные теги/ID, segment, даты, существование поверхностей/справочных значений, уникальность name/code. Тест `A/B invalid aggregates leave all state and timestamps unchanged` проверяет invalid patches и неизменность состояния; boundary-тесты проверяют `/groups`, `/surface_ids/0`. | Покрытие доступных mock-правил не устанавливает полноту согласованной backend-валидации. Все параметры возможных аудиторий новым телом не перечислены. |
| Атомарность карточки/групп/поверхностей; порядок и IDs — S:L20 | `M/handlers.mjs#save` валидирует candidate и response до `push/Object.assign`; `M/model.mjs#experimentResponse` сохраняет переданные ID, генерирует отсутствующие, использует порядок массива. Roundtrip-тест разворачивает группы, проверяет точное равенство коллекций и GET; invalid-aggregate тест сравнивает полный snapshot. | Это атомарность синхронного изменения памяти, не транзакция БД и не доказательство поведения при конкурентных запросах/сбоях. |
| Запрет изменения тегов существующих групп вне черновика — S:L22 | `M/validation.mjs#validateGroups` использует **сохранённый** `existing.status` и сопоставление по ID. Boundary-тест запрещает одновременные `status:'draft'` и изменение тега из active, проверяет `IMMUTABLE_FIELD` и отсутствие мутации; разрешает перестановку и изменение после отдельного перехода в draft. `F/model/ab-testing-form.ts#isAbTestingGroupTagReadonly` отражает правило в клиенте. | Производственная enforcement неизвестна. Семантика замены/пропуска ID требует отдельного уточнения, см. ниже. |
| PUT частичен сверху; переданные коллекции заменяются — S:L23 | `M/handlers.mjs#save`: `{ ...existing, ...req.body }` без слияния элементов коллекций. `F/api/ab-testing-client.ts#updateAbTestingExperiment` отправляет PUT; `F/api/ab-testing-schema.ts#abTestingPatchSchema` делает поля optional. Roundtrip-тест заменяет поверхности, переставляет группы, затем обнуляет nullable-поля и сохраняет name. Клиентский тест `uses POST 201 and partial PUT preserving null and server group identity` проверяет точное тело `{owner:null, groups}`, отклонение пустого patch и `status:null`. | Клиентский fetch подменён. Проверки всей семантики backend PUT нет. |
| Общий префикс, envelope, доступ; OpenAPI и тесты — S:L26–27 | `M/test-helpers.mjs#base` задаёт `/v1/managed-resources/ab-testing/experiments`; handlers вызывают `sendSuccess`. Metadata-тест извлекает восемь operationId из локального `spec.paths`. Клиентский тест `validates envelope, detail and status without treating malformed responses as success` проверяет malformed responses. | Mock-тест `A/B business requests do not enforce the demo principal permissions` явно допускает CRUD при пустых permissions. Это согласованная mock-граница, не backend-проверка доступа. Наличие локальных OpenAPI-зависимых тестов не доказывает актуальность серверного OpenAPI или пройденные backend-тесты. |

## Существенные lane findings

### Partial PUT подтверждён только статически для mock/client

Верхнеуровневое слияние сохраняет отсутствующие поля; переданные `groups` и `surface_ids` заменяют прежние массивы. Явный `null` не превращается в отсутствие поля: `mocks/managed-model.mjs#managedRecord,populate` заполняет defaults только для `undefined`. Тесты содержат positive и negative assertions для этих сценариев.

### Group identities: положительное доказательство и открытая граница

Сохранение переданного ID и порядка подтверждается кодом и roundtrip assertions. Однако `validateGroups` проверяет дубликаты внутри входного агрегата, а запрет изменения тега сопоставляет группы только по совпадающему ID. Отсутствующий ID приводит к генерации нового; проверка принадлежности каждого предоставленного ID прежнему агрегату в этой функции отсутствует.

Поэтому сценарий «убрать/заменить ID и передать другой tag» не равнозначен доказанному изменению **существующей** группы: backend может трактовать его как удаление и создание. Новое тело не определяет правила для чужих ID и замены группы вне draft. Нельзя объявить обход или требовать запрета добавления/удаления групп без уточнения. Соответствующий backend-negative evidence неизвестен.

### Атомарность и централизованные справочники не закрыты mock-покрытием

Проверка snapshot доказывает намерение локальной реализации не менять состояние при ошибке, но не наличие серверных транзакций. Раздельные локальные хранилища справочников и отсутствие теста редактирования A/B значений через generic catalog CRUD оставляют отдельный evidence gap.

## Безопасные предложения

- **keep:** сохранить действующие mock/client-поведения partial PUT, nullable values, порядка/ID групп и проверки сохранённого статуса; сохранить configuration ≠ execution и отсутствие mock role enforcement.
- **update:** добавить точный requirement-to-evidence join для MOS-1323 по новому источнику. Старые отчёты и failed runtime-состояния не переписывать. Не повышать результат до backend delivery.
- **new:** новый feature/change из этой lane не обоснован. Дополнительные тесты принадлежности/замены group ID и централизованного редактирования справочников — возможное усиление evidence после согласования семантики, не уже утверждённый corrective scope.
- **question:** запросить сохранённые серверные доказательства миграций, транзакционного сохранения, partial PUT/identity rules, permission enforcement, централизованных справочников и результатов backend-тестов. MOS-1142 не открывался; его реализация неизвестна. Отдельно уточнить допустимость новых/чужих/отсутствующих group ID при обновлении вне draft.

## SHA256 входов

Вычислены локально по полным байтам; content hash совпал с metadata и WAVE-D092.

| Вход | SHA256 |
|---|---|
| `A/sources/jira-optional-backend-details/r1/content.json` | `3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618` |
| `A/sources/jira-optional-backend-details/r1/metadata.json` | `9357e481e237e04c47258fe4efb4bcc3d8377e2690e75963653d2275885ff4fc` |
| `A/decisions.md` | `fa7cffedb00f4d481efa2b523e8f1a1b4991b2750022c823c30c5370ab5cf945` |
| `A/reviews/R-D091-RECOVERY.md` | `f6fb801733ee223979debb0277de15e8f97448a3a69db6a2fb0f42f35c03e45d` |
| `A/reports/JOIN-MOS-1323.md` | `86a89f81d8b8baa87b6566f85abe71e68b0eebb22d1916229db7339de4ef653b` |
| `M/handlers.mjs` | `93f4ab0853c27c2084cb8b6a655665db324074488e04ce86fc5822572c5d25cf` |
| `M/model.mjs` | `a253ac0f8625dce38ff70b8caecae6576299216217386eaccf948cdf0f1adc74` |
| `M/validation.mjs` | `28b92373bb78af2d2cbe4cf96e4b9a5728f288bbd72c0577850e2768c774ff67` |
| `M/seed.mjs` | `aebfcdb08d66579a636203c5dbcdf483dc49d70068b066b16fd1a2c8a1213931` |
| `M/aggregate.test.mjs` | `ee5d97d28093b014d59e389d193f2e104b689c72e65ea46afb588297c55ce2d3` |
| `M/search-export.test.mjs` | `b122762fa79e6c55de7b0051d25d98852786656413845de9a3860c483986e4e7` |
| `M/saved-filter-interoperability.test.mjs` | `4b458bc9e00abc549aada9b4157c21bf226aa60c0ce6ab6445ddd90dee3fda1f` |
| `M/test-helpers.mjs` | `6fa7e0efa1afdbe136afbd2d5f38de6b167d5d3c294fa4a0487eea68b9b38f0a` |
| `M/README.md` | `eaa5cf2a6706fe21eb15886d6e76c93f8c91ecaf8e537a4f92e357129e2a6d41` |
| `mocks/managed-catalogs.mjs` | `936cdfd5ff9af46048e80c87122ad2a2aed800cf839111f91dcbbf0c85355dad` |
| `mocks/managed-model.mjs` | `472534b1746b60145a8e45d35cd98c141afd3ab59bd1c6ee5194061ea6a95a61` |
| `F/api/ab-testing-client.ts` | `630f104eb85940a59eaee9d2d14ed0479c2803ca7382af33e53dcf84d79ff837` |
| `F/api/ab-testing-client.test.ts` | `7cb9da6526132daf9a744b4d9c529de1105a4fe8d6bdd527edadcb61a466dc9d` |
| `F/api/ab-testing-schema.ts` | `c847ed34deb8ab2dff65f6b90502e6cedef6c3a78b11ae210803d8be57a7caad` |
| `F/model/ab-testing-form.ts` | `ad4279ce8218b7df3796b3ece4d10eed97630c3f9806b24c4ae81eacef403018` |

## Проверки и остаточные риски

Выполнены только локальное чтение, поиск и Python SHA256/декодирование description. Два первоначальных чтения использовали неверную базу `change/sources`; источники затем полностью прочитаны из правильного `audit/sources`, blocker отсутствует.

Тесты не запускались; браузер, сеть, серверы, business requests, Git mutations и делегирование не использовались. Файлы не записывались. Git/staging не проверялись. Успешность тестов, production backend и deployment не заявляются.