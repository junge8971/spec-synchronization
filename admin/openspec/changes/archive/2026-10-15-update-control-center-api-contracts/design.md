## Context

См. proposal.md — Why. Исследование выполнено до создания плана: сравнены все paths/components локального aggregate и live JSON, содержательное отличие CRUD Markdown, четыре скриншота, затронутые клиенты/формы/моки/тесты и существующие specs.

### Sources and baseline

- Live Swagger: https://nchat-a-tech.mos.ru/api/control/docs, источник JSON: https://nchat-a-tech.mos.ru/api/control/openapi.json.
- Повторное чтение при планировании: 2026-10-15T10:33:36Z, SHA-256 исходных байтов `2f3c48d3542e4486f7c1a501c4a1a4a0b813c662af26079a1e98c9f09d6ea26d`. Live: 94 пути / 128 операций / 380 схем. Локальный aggregate: 82 / 112 / 353. Этот hash фиксирует наблюдение, не означает, что снимок уже импортирован.
- `/home/user/Загрузки/crud-api.md`, SHA-256 `91c8dc68fc1b602a64428d1d6f1d9c44a0e6a89eced226e4773853badf13954a`. Дополняет бизнес-семантику, не превосходит live.
- Четыре переданных PNG: MOS-1336 (домены, optional configuration, ID ответственных и view), сообщение о backend embed_code/authorization, сообщение о новых managed-разделах и условиях.
- При apply сохранить источники/provenance в репозитории, не делать проверки зависимыми от временных PNG/Downloads. Если live изменится после планирования — повторить структурную сверку и отразить дополнительную дельту до импорта, не молча расширять план.

### Observed implementation

| Область               | Текущее состояние                                                                           | Последствие обновления только JSON                                 |
| --------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Surface               | `responsibles-step.tsx` вводит ФИО, mapper отправляет строки; runtime detail ожидает строки | Создание отправляет не ID, новый GET не проходит Zod               |
| Registration failures | `getRegistrationRejection` принимает только 422 detail[].loc/msg                            | Бизнес-отказ может стать unknown и заблокировать исправление       |
| Configuration         | Draft не содержит конфигурацию; mock всегда использует defaults                             | Новое optional поле игнорируется mock handler                      |
| KB/A/B                | Поля/операторы заданы константами, value string/string[], metadata enum без numeric         | Metadata целиком отклоняется до открытия конструктора              |
| Managed search        | `mocks/managed-search.mjs` преобразует значения в строки                                    | Числовые операторы отсутствуют, сравнения неверны                  |
| Mock registration     | `mocks/app.mjs` требует handler для каждого operationId                                     | Новые операции и переименованные exports останавливают сервер      |
| Dialog export         | `DialogExportField`, локальные exportDialog/exportDialogs                                   | Новые DTO/operationId требуют миграции; защитные проверки уже есть |
| Contract tests        | Counts, fingerprints, split closure, security assertions                                    | Нужно обоснованное обновление ожиданий, не удаление проверок       |

## Goals / Non-Goals

**Goals:** атомарно обновить контракт и все существующие потребители, обеспечить реалистичное локальное HTTP-покрытие и воспроизводимую регрессионную проверку. Поддержать расширенные типы без потери прежней семантики или безопасного поведения ошибок.

**Non-Goals:** новые UI-разделы API/шаблонов, самостоятельный конфигуратор и редизайн мастера поверхностей, новая auth/session модель, изменения UI permission-policy, backend-миграции, исполнение описанных API/плейсхолдеров/экспериментов. Наличие нового DTO не является основанием строить универсальный CRUD renderer. Browser/E2E не создаются, не меняются и не запускаются.

## Decisions

### 1. One snapshot with explicit semantic supplements

Приоритет: live DTO/пути и описания операций; затем дополнительные backend-документы для неописанных деталей; затем прежние локальные решения. Сохранить исходные байты/хеш снимка и машинно проверяемую согласованность aggregate/splits, а generated schema.d.ts получать только `yarn api:generate`.

Нормализация security AND остаётся: сама документация live требует два заголовка. Нельзя механически перенести формальный OR. Отдельный mpmm-auth контракт не заменяется control API.

Новая дельта должна включать не только 16 новых методов, но и все изменения схем: CatalogLookupSectionName, ManagedResourceConditionField.type/operators, values у fb_survey/ref_dictionary/kb_entry/ab_experiment conditions, field/operator enum KB/A/B, ManagedResourceSavedFilterCreate.resource, ManagedCatalogResponse.code, CreateSurfaceRequest.configuration, SurfaceResponsibleRequest/Response и новый SurfaceResponsibleUserResponse, а также export DTO. Числовой union у feedback/catalogs сам по себе не разрешает числовые операции на строковых полях.

Альтернатива «скопировать JSON и поправить compilation errors» отвергнута: не выявляет runtime Zod, metadata, handler dispatch и бизнес-ограничения.

### 2. Surface assignments are references, not names

Переиспользовать существующий HTTP transport и контракт `/users/v1/search`. Сначала проверить имеющиеся реализации поиска/представления бизнес-пользователей (team API, optional editor users); нельзя импортировать internals optional-слайсов. Если нужен общий клиент нескольким владельцам — минимальный публичный entity API бизнес-пользователя, не auth-сервис и не новый permission-контекст. Поиск должен позволять выбрать результаты за пределами первой страницы, отменять устаревшее чтение и сохранять выбранный ID отдельно от подписи.

Уточнить draft и тестовые fixtures: строки произвольных имён нельзя считать ID даже при непустом значении. При восстановлении старого draft очищать только неподтверждённые назначения с видимым запросом перевыбора; не угадывать ID. Не требовать UUID для UserId.

Runtime detail проверяет обязательный объект id/full_name/email с nullable сведениями. Обзор отображает доступные ФИО/email, иначе ID с пояснением. Не поддерживать бессрочный union string|user ради устаревших mocks: это скроет несовместимость.

Optional configuration поддерживается клиентом и mock API, но существующий мастер вправе её не отправлять: там нет редактора. Если поле передано, проверять текущую UpdateSurfaceConfigurationRequest и сохранять в одном POST; не создавать скрытый PUT/default payload. Конфигуратор не проектируется этим change.

### 3. Preserve creation outcome semantics

Существующий attempt state machine сохраняется: confirmed 201 -> сохранённый ID -> GET, read-error -> повтор GET, неизвестный исход -> без replay. Расширить только классификацию доказанного отказа и сопоставление структурированных ошибок с полями, используя существующие API error conventions. Нельзя любую ошибку 409/422 автоматически объявить безопасной для повторного создания или извлекать домен regex из message.

OpenAPI surfaces не описывает DOMAIN_ALREADY_IN_USE и ошибки пользователей. Перед включением real-mode распознавания нового envelope нужен точный backend-пример из документации/ответа команды; это узкий интеграционный gate, не повод блокировать остальные части. Без примера сохраняется общий безопасный error/unknown path. Mock business errors документируются как локальная конвенция, не добавляются в OpenAPI. Проверки доменов/пользователей/конфигурации выполняются до изменения state и связей команды; никакого await между проверкой занятости и фиксацией локального состояния.

Mock хранит ID и разрешает текущие сведения при GET. Для уже сохранённого отсутствующего пользователя локальная конвенция — ID плюс null сведения. Новый выбор отсутствующего ID отклоняется. Backend-миграция прежних ФИО в ID не решается фронтендом.

### 4. Typed conditions without a new shared business framework

В каждом optional-модуле независимо расширить constants/schema/model/UI: type в metadata, numeric operators, value number/[number,number], новый выбор поля, смена оператора и значения, сводка, URL decoding, saved filters и экспорт. Сохранить существующие draft/applied, 50 условий, AND/OR, reset offset, неизвестный URL -> явная ошибка. Поле integer описывает данные, но дробные пороги допустимы по документации.

Native numeric inputs с доступными подписями используются для одного порога и двух границ. Пустое поле не равно 0; изменение field/operator сбрасывает несовместимое значение, но не применяет отбор автоматически. Validation сверяет field/operator/value совместно по metadata. Numeric значения не проходят через `registryValues`, который предназначен для строковых наборов.

На mock server расширить существующий `managed-search` предметно: числовые сравнения с finite numbers и исключением NULL, строковые операторы сохраняют текущую регистрозависимость. Metadata builders выбирают операторы по типу/справочной привязке, а не копируют общий enum всем полям. Повторно использовать этот evaluator в search/export и правила в saved-search validation. KB skill_names уже строится из связанных неудалённых skills — сохранить этот источник, не заменить на IDs.

Альтернатива общего optional engine отвергнута: нарушает независимое удаление модулей и усложняет небольшую дельту. Нейтральные UI-примитивы не запрещены, но новый движок не нужен.

### 5. New managed mocks use the current contract, not generic optimistic success

Сохранить общий Express registration/validation/search/CSV, добавив владельцев state/handlers/validation для API endpoints и response templates. Не помещать бизнес-правила новых ресурсов в optional KB/A/B. Покрыть все восемь операций каждого ресурса и девять системных lookup/catalog наборов; проверить порядок статических metadata/search/export маршрутов до параметризованных ID.

Новые metadata keys: `data.endpoints` и `data["response-templates"]`. Lookup API: api_methods/api_groups/api_sources/api_statuses/api_landing_categories/api_param_locations; templates: tpl_types/tpl_scopes/tpl_statuses. Значения системные, доступны для чтения/экспорта, но не редактируются. is_active влияет на новый выбор, прежние сохранённые значения сохраняются.

API validator проверяет полный объединённый record при PUT: source_code для incoming/outgoing; уникальности; JSON-text и нормализацию пустого текста; HTTP/HTTPS base_url; path; response codes и их уникальность; child ID/order/replacement. Templates validator проверяет текст, ссылки и статусы без вымышленного is_active или ограничения связи через scope_code. Сохранять данные атомарно, timestamps/collections не менять при ошибке. DELETE и повторное использование уникальных значений следуют документированному мягкому удалению.

Счётчики API групп получаются обычным search с одинаковым отбором и разным group_code, не новым endpoint. CSV должен использовать display_name, выбор и порядок разрешённых полей, весь отбор и лимит; generic CSV с кодами/техническими заголовками не считается готовым покрытием.

Новые saved-filter resource IDs принять согласно live. Каждый search валидируется собственной схемой, включая defaults и вложенные ошибки. Поведение поддержано локально, но не объявляется проверенным backend из одного enum. Противоречие Markdown фиксируется. Ни новые формы фильтров, ни новые UI-разделы ради этого не добавляются.

### 6. Published dialog exports replace the supplement, not its safety

Перепривязать handlers к live operationId, обновить alias ExportField и зависимые тесты/fixtures. Generated DialogExportRequest отражает live; runtime parser сохраняет ровно один scope и игнорирование неприменимых опций. Особое внимание mock AJV: формальная схема не должна отклонять игнорируемые по описанию опции до business handler; узкая operation-specific нормализация/валидация допустима вместо общего ослабления AJV.

Сохранить проверку bytes/BOM/MIME/filename/length/nosniff/no-store и отсутствие частичного скачивания. Исторические DialogErrorEnvelope/ValidationDetail не сохранять только ради старого supplement; использовать общие error representations и тестировать documented envelope отдельно там, где live responses описывает ошибки неполно. Не удалять assertions просто ради нового hash.

### 7. Reconcile specifications, not history indiscriminately

Delta-specs заменяют запреты numeric KB/A/B, старый unavailable managed coverage и происхождение exports. При apply адресно обновить активный `mos-1249-feedback-api/design.md`: provenance/counts, происхождение экспорта, предположение о generic unavailable handlers. Не переписывать архивные решения задним числом и не отмечать feedback implementation завершённой.

Изменения descriptions permissions и ошибок аналитики/диалогов входят в контрактную документацию. Текущая таблица UI permissions не содержит TSAM.Dialog actions; новый mapping/разрешение маршрутов здесь не вводится. Это отдельный явно зафиксированный follow-up с согласованием, а не скрытый auth-refactor или обещание готовности этих прав на UI. Перед любой будущей auth/mock работой читать archived integrate-mpmm-auth-permissions/add-local-session-demo artifacts согласно правилам проекта.

## Risks / Trade-offs

- [Live изменится между планом и apply] -> зафиксировать raw snapshot/hash, повторно сверить дельту, не обращаться к сети из тестов.
- [Markdown расходится с live] -> live приоритет, таблица конфликтов в docs, runtime гарантии не выводятся из одного enum.
- [Недостаточно описаны surface errors] -> точный backend-пример как release gate для распознавания; безопасный общий путь и явно маркированные mock conventions до подтверждения.
- [Старые сохранённые ФИО/данные backend] -> не мигрировать по имени; перевыбор draft, строгий ответ, проверка backend-миграции перед rollout.
- [Числовые операторы ломают загрузку metadata] -> tests полноценного metadata response, не только isolated search validator; единая поставка UI/mocks/contracts.
- [Общие mock helpers регрессируют feedback/catalogs] -> regression tests всех старых ресурсов, числовой union не расширяет их поля автоматически.
- [Optional modules перестают удаляться независимо] -> существующие FSD/build-graph checks, отсутствие взаимных импортов.
- [Mock success принимается за реальный backend] -> отдельно отмечать unit/component/server results и внешние интеграционные gates; credentials и role enforcement в mock не добавлять.

## Migration Plan

1. Зафиксировать источники и delta, обновить aggregate/splits/generated types и контрактные ожидания; затем согласованно исправить handlers и consumers до зелёных проверок. Не выпускать промежуточную смесь старых runtime-схем и нового DTO.
2. Реализовать surface compatibility, typed KB/A/B, новые managed mocks, dialog export mapping, тесты и документацию. Проверки старых сценариев не ослаблять.
3. Выполнить typecheck/lint/test/format/api-check/build и optional isolation checks. Browser/E2E не запускать.
4. До real rollout подтвердить backend-форматы отказов поверхностей, сохранённые назначения старых данных, новые saved-filter resource IDs и доступность экспортов/заголовков. Не выполнять мутирующие запросы на общем стенде без согласованных тестовых данных и разрешения.
5. Rollback требует совместимого backend/frontend сочетания: старый bundle не умеет новый responsible DTO. Нельзя обещать безопасный откат только frontend. Локальный mock restart восстанавливает новый seed, не мигрирует production данные.

## Open Questions

- Точный HTTP status/envelope/field pointer у DOMAIN_ALREADY_IN_USE и неизвестного ответственного: нужен для узкого real-error adapter, остальные задачи независимы.
- Как backend читает старые назначения и недоступных внешних пользователей: live допускает nullable сведения; frontend использует именно этот DTO без вымышленных записей.
- Реально ли развёрнуты saved-filters для двух новых ресурсов: локальная поддержка следует live enum, несовпадение deployment фиксируется как backend contract issue.
- Конкретные значения demo embed/authorization и отсутствующие в OpenAPI детали ошибок остаются явными mock conventions до получения backend-примеров; реальных секретов не использовать.
