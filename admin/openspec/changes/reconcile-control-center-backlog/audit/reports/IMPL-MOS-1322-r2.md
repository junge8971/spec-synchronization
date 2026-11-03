# IMPL-MOS-1322-r2 — code/mock/test evidence точного backend issue

## Результат и границы

Новое тело MOS-1322 позволяет выполнить предметный join требований с **локальными моками и написанными тестами**. Они подтверждают наличие соответствующей локальной реализации, но не выполнение backend DoD.

**Неизвестны:** реальные таблицы и миграции, транзакционная атомарность, серверная авторизация, централизованное управление справочниками, результаты backend-тестов и deployment. Отсутствие этих доказательств здесь не означает отсутствие реализации.

Прочитаны D-091 в `audit/decisions.md` и `audit/reviews/R-D091-RECOVERY.md`. Исторический missing-body вывод `JOIN-MOS-1322.md` сохраняет силу для прежнего пакета; новый источник снимает только этот прежний source gap. Failed runtime provenance не пересматривается. Предыдущие JOIN/IMPL-KB-EDITOR использованы как карта, не как доказательство выполнения MOS-1322.

Ниже:
- `A` = `openspec/changes/reconcile-control-center-backlog/audit`;
- `B` = `mocks/knowledge-base`;
- `K` = `app/optional/knowledge-base`;
- `S` = `A/sources/jira-optional-backend-details/r1/content.json#/items/0`.
- `W1…W7` — пункты «Что делаем», `D1…D7` — пункты DoD внутри `S/description`, нумерация с единицы. Это точные атомарные локаторы, не новые требования.

## Источник

`S/key=MOS-1322`, `summary=[B] Реализовать раздел "База знаний"`, `status=Hold`, `updated=2026-10-14T14:03:51.688+0800`.

`metadata.json#/retrievedAt`: `2026-10-20T14:35:05.335Z`. Сохранена selected-field extraction; комментарии, вложения и custom acceptance fields не собраны. `parent:null` не доказывает отсутствие модульной принадлежности. Зависимость MOS-1142 взята только из W1; связанная задача не открывалась.

## Требования → наблюдаемая реализация → неизвестность

| Атомарный источник | Наблюдаемое code/test evidence | Граница вывода |
|---|---|---|
| **W1:** CRUD через общий managed-resources; **D2:** создание, просмотр, изменение | `B/handlers.mjs::knowledgeBaseHandlers,save,detail`; регистрация overrides в `mocks/managed-resources.mjs::managedResourceHandlers`. Используются общие `managedRecord`, `sendSuccess`, `managedMissing`. `B/aggregate.test.mjs`, тест `KB aggregate PUT preserves IDs…`: POST, GET, PUT и повторное чтение результата. | Есть локальный CRUD и переиспользование общего mock-механизма. Выполнение зависимости MOS-1142 на backend неизвестно. |
| **D2:** мягкое удаление | `B/handlers.mjs::entries,detail`: ID добавляется в `deletedIds`, запись физически остаётся в массиве. `B/search-export.test.mjs`, тест `KB soft delete hides detail, search and export but reserves codes`: GET/PUT/DELETE/export → 404, отсутствие в поиске/CSV, сохранение уникальности кода. | Конкретная soft-delete семантика мока; реальное хранение/backend неизвестны. |
| **W2, D1:** таблицы карточки, ссылок, связей с навыками; согласованная модель и миграции | `B/seed.mjs::initializeKnowledgeBase`: массив объектов, вложенные `links`, `skill_ids`, `deletedIds: Set`. `B/model.mjs::entryResponse` строит response и производные поля. | In-memory агрегат **не является** таблицами или миграциями. Доказательства физической модели БД и её соответствия согласованной модели не представлены. |
| **D3:** атомарное сохранение карточки, ссылок, навыков | `B/handlers.mjs::save`: кандидат валидируется до `push/Object.assign`. `B/aggregate.test.mjs`, тесты `KB business conflicts…never mutate on failure` и `KB request limits…preserve atomic state`: после ошибочного PUT сравнивается прежний snapshot. | Локальная неизменность состояния при отказе подтверждена кодом и утверждениями тестов. Транзакции БД, конкурентные записи и rollback при инфраструктурном сбое неизвестны. |
| **D3:** сохранение порядка ссылок | `B/handlers.mjs::persistedEntry,save`; тест `KB aggregate PUT preserves IDs, array order…` отправляет обратный порядок и проверяет обратный порядок ID, затем GET равен результату PUT. | Написан точный локальный regression. Реальный backend не проверялся. |
| **W3:** подключение справочников к централизованному реестру, начальные значения; **D4:** управление значениями через «Справочники» | `B/seed.mjs::catalogs,initializeKnowledgeBase`: шесть отдельных наборов; `B/handlers.mjs::get_section_catalog_lookups` возвращает `state.managed.knowledgeBase.catalogs`. `B/aggregate.test.mjs`, тест `KB metadata, scoped lookups…`: создание стороннего общего каталога не меняет KB lookup. `B/README.md` прямо называет наборы isolated read-only. | Начальные mock-значения есть. **Централизованное редактирование KB-значений этим evidence не подтверждено:** lookup обслуживается отдельным состоянием. Это граница мока, не установленный production-дефект и не основание добавить редактор справочников во frontend KB. |
| **W4, D4:** API справочников и метаданных, привязка полей формы | `B/model.mjs::catalogBindings,metadata`; `B/handlers.mjs::metadata_knowledge_base,get_section_catalog_lookups`. Тест `KB metadata, scoped lookups…` проверяет шесть bindings, `code`, доступность названий и `is_active`. `K/api/knowledge-base-client.ts::getKnowledgeBaseMetadata,getKnowledgeBaseLookups`; client-тест `requires metadata entries and the six section lookup keys`. | Доказаны локальные выдача/потребление данных и проверки формы DTO; наличие реального централизованного реестра неизвестно. |
| **W5, D2:** поиск, обычные фильтры, сложные условия | `B/handlers.mjs::search,list_kb_entry`; `mocks/managed-search.mjs::searchManaged,matchesFilters,matchesConditions`; `B/validation.mjs::validateSearch`. `B/search-export.test.mjs`, тест `KB search applies AND filters, OR conditions…`: сочетание query/filters/conditions, сортировка до пагинации, ошибочные условия → 422; тест `typed numeric search…` — диапазоны. | Локальная реализация через общий поиск есть; производительность и корректность реального backend неизвестны. |
| **W5, D5:** сохранение условий поиска | `mocks/managed-resources.mjs::saveFilter,savedHandlers,validSavedSearch`; `B/validation.mjs::savedKnowledgeBaseSearch`. Тест `KB saved filters validate searches…`: CRUD фильтра, resource scope, сохранение условий, отказ без изменения state. `B/saved-filter-interoperability.test.mjs` проверяет actual frontend codec на сохранённом mock-поиске. | Общий локальный механизм подтверждён. `user_id: 'local-demo'` не доказывает backend ownership или изоляцию пользователей. |
| **W6, D5:** CSV всего отбора и карточки с выбором полей | `B/handlers.mjs::exportEntries,export_kb_entry,export_detail_kb_entry`; `mocks/managed-search.mjs::sendManagedCsv`. Тест `KB CSV uses BOM…full selection and safe cells`: список экспортируется целиком вопреки `limit:1/offset:1`, карточка отдельно, порядок выбранных полей, недопустимые/повторные поля, лимит 10001. | Есть локальные реализация и существенные boundary assertions. Backend export неизвестен. Конкретные BOM/разделитель/лимит — наблюдаемая реализация, не отдельные требования тела MOS-1322. |
| **W7:** поля, связи, уникальность, понятные ошибки по полям | `B/validation.mjs::fieldFailure,validateEntry,validateReferences,validateLinks`: уникальность `code`, доступность справочных значений/навыков, принадлежность ID ссылок, HTTP(S), nullability. `B/aggregate.test.mjs` проверяет 409/422, пути `/skill_ids/0`, `/links/0/url`, `/code`, неизменность состояния. Schema-errors проверяются как `detail[].loc`. | В mock представлены два формата ошибок: business `errors[].field` и schema `detail[].loc`. Их соответствие требуемому общему backend-формату требует API-lane; backend-покрытие неизвестно. Уникальность названия из общего слова «уникальности» не выводится. |
| **D6:** `/managed-resources/knowledge-base`, общий формат ответов и проверка доступа | `B/test-helpers.mjs::base` задаёт `/v1/managed-resources/knowledge-base/entries`; handlers используют `sendSuccess`. `K/api/knowledge-base-client.ts` реализует соответствующие metadata/search/detail/create/update вызовы. `B/test-helpers.mjs::start` вызывает локальный Express без credentials; `B/README.md` явно исключает role enforcement. | Префикс и общий локальный транспорт наблюдаемы. **Проверка доступа не доказана:** credential-free mock намеренно её не реализует. UI permissions и клиент не заменяют серверную авторизацию. |
| **D7:** OpenAPI, тесты основных сценариев и ошибок | `mocks/contract.mjs::spec,createValidator` читает `docs/api/contracts/openapi.json` и создаёт Ajv validator; `B/model.mjs` извлекает из него metadata, `B/validation.mjs::validateSchema` — схемы поиска. Перечисленные mock-тесты и `K/api/knowledge-base-client.test.ts` содержат positive/negative assertions. | Наличие написанных contract/client/mock-тестов установлено; они **не запускались**. Полнота OpenAPI проверяется отдельной API-lane. Наличие и результаты backend-тестов неизвестны. |

### Существенное различение

`B/test-helpers.mjs::start` создаёт `createMockState()` и `createMockApp()`, а не соединение с production backend. Поэтому даже HTTP-форма этих тестов не превращает их в backend evidence. Client-тесты используют `vi.stubGlobal('fetch', …)`.

Отсутствие удаления материала в прочитанном frontend-клиенте не объявляется дефектом backend issue: серверная операция удаления представлена в mock, а frontend scope не подменяет MOS-1322.

## Безопасные рекомендации

- **keep:** сохранить существующие mock/client/test сценарии и исторические отчёты. Не менять feature checkboxes; не заявлять выполнение MOS-1322.
- **update:** после независимого review добавить точный requirement-to-local-evidence join. Прежний missing-body blocker больше неприменим к новому пакету; вместо него явно зафиксировать backend evidence gaps. Решение о coverage остаётся parent; возможное P означает только частичный анализ.
- **new:** новый corrective change по результату этой lane не обоснован. Не создавать дубликаты CRUD/export/editor работ и не расширять frontend централизованным редактированием справочников или ролевым enforcement моков.
- **question:** запросить сохранённые backend-артефакты миграций/таблиц, транзакций агрегата и порядка ссылок, регистрации/редактирования KB-справочников, серверной проверки доступа и backend-тестов. Нужен также точный допустимый evidence зависимости MOS-1142; самостоятельно её scope не раскрывать.
- **question:** централизованный registry и единый error envelope требуют сверки с API/SPEC lanes. Наблюдаемые отдельные read-only lookup sets и два error shape — границы локальной реализации, не автоматическое доказательство дефекта сервера.

## SHA256 прочитанных входов

Вычислены локально по байтам; source content соответствует объявленному fingerprint.

| Вход | SHA256 |
|---|---|
| `A/sources/jira-optional-backend-details/r1/content.json` | `3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618` |
| `A/sources/jira-optional-backend-details/r1/metadata.json` | `9357e481e237e04c47258fe4efb4bcc3d8377e2690e75963653d2275885ff4fc` |
| `B/handlers.mjs` | `e7fa15ce533690bea5d5a0c506012fa4cf06ca3b3da62e5b09c10b770b2fc497` |
| `B/model.mjs` | `5d87b778dedaccc29b7d0198f221ec308e550300cda1cc532609e4d44b7e9dbb` |
| `B/seed.mjs` | `175703c411a3810895345c11573dc86907991d69654c1053e857618754694c91` |
| `B/validation.mjs` | `d9d2dbe94c6d0202bbbd79a514adf071733a91b241f9abdd2fec396f7631a39e` |
| `B/aggregate.test.mjs` | `6c27c4b6ef06843aae030c741a48a774c60bf6069bab386599f234e5269c06e8` |
| `B/search-export.test.mjs` | `f0aaa5dd3ee407211e17690c1a721107be0985f400cbffd02ba806608fbd406a` |
| `B/saved-filter-interoperability.test.mjs` | `b54c41e09a070b57a4835cf74bcfbee15916b7ed304335aa10c104894973906f` |
| `B/test-helpers.mjs` | `dec0f2038cf473a851575d508c016340de148a9164cb7b31113c0145de0aca9f` |
| `mocks/managed-resources.mjs` | `491ea71f90c4ef4c6b7876450b3f763286ff856e5c9c076eb92cf74570ef6483` |
| `mocks/managed-search.mjs` | `6cdfee3328c75152e18ca7bdf26cdac39652bcc6b122cf182e4c54ab8850d444` |
| `mocks/contract.mjs` | `ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371` |
| `K/api/knowledge-base-client.ts` | `5d2301ed88ce900d775a9c6a6da559b4c45810b7703576ed022c3a75f1cb8971` |
| `K/api/knowledge-base-client.test.ts` | `9fc8a1824ad44bd17c02d6548ecc5aec5eddc1bda777f853a4d837d12fafab75` |