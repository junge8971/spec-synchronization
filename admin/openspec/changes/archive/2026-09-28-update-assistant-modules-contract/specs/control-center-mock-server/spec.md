## MODIFIED Requirements

### Requirement: Complete supplied operation coverage

Mock API SHALL реализовать 32 бизнес-операции поставленного OpenAPI: Domains/Skills — 8, Surfaces — 11, Teams — 8, Assistant modules — 5. Ответы SHALL соответствовать описанным status codes, envelope, схемам, nullable/required полям, enum и форматам. Access-операция `GET /api/control/api/auth/v1/me` SHALL быть явно исключена из текущего покрытия и MUST NOT обслуживаться mock server. Отсутствие Bearer MUST NOT препятствовать чтению или мутациям бизнес-данных. Это SHALL документироваться как ограничение локального mock server, а не изменение требований безопасности backend. Непредоставленные шесть разделов MUST NOT выдаваться за реализованный контракт.

#### Scenario: Contract coverage check

- **WHEN** контрактные тесты перечисляют 33 операции исходного OpenAPI
- **THEN** для каждой из 32 бизнес-операций имеется исполняемый сценарий без Authorization с проверкой ответа по схеме; единственное явное исключение — указанная Access-операция, а пропуск любой бизнес-операции вызывает падение проверки

#### Scenario: Invalid contract input

- **WHEN** передан невалидный UUID/UUIDv7, enum, limit/offset, обязательное тело или отсутствует обязательный Idempotency-Key
- **THEN** mock server возвращает предусмотренный контрактом validation response, а не успешные данные; тело 422 соответствует HTTPValidationError там, где он описан

#### Scenario: Unknown resource or absent credentials

- **WHEN** без Bearer запрошен отсутствующий корректный ID бизнес-сущности
- **THEN** сервер возвращает 404 по документированной mock error convention без изменения исходного OpenAPI

#### Scenario: Retired current principal endpoint

- **WHEN** запрошен `/api/auth/v1/me` у локального mock server
- **THEN** возвращается 404 как для отсутствующей операции, без фиктивного пользователя или запуска сессии

## ADDED Requirements

### Requirement: Module registry query behavior

Mock API SHALL предоставлять список по `GET /assistant-modules/v1/modules` с query, status, sort и limit/offset согласно поставленной схеме. Локальная конвенция SHALL определять query как регистронезависимый поиск по code/name/description, status как точное строковое совпадение (неизвестное значение даёт пустую выборку), отсутствие sort как сортировку по name. Один и несколько повторённых query-параметров sort SHALL поддерживаться как упорядоченный список критериев. Фильтры и сортировки SHALL применяться до пагинации; семантика SHALL быть документирована как mock-конвенция, а не расширение backend-контракта.

#### Scenario: Multiple sort criteria

- **WHEN** переданы `sort=status&sort=-name` и limit/offset
- **THEN** список сортируется по status, затем по убыванию name внутри одинакового status, после чего возвращается запрошенный срез и согласованные totals

#### Scenario: Single sort and invalid input

- **WHEN** передан один `sort=-updated_at` либо недопустимый `sort=unknown`
- **THEN** первый запрос принимается как массив одного критерия, второй возвращает контрактный 422

#### Scenario: Empty results

- **WHEN** фильтр не имеет совпадений или offset выходит за конец выборки
- **THEN** items пуст; pagination описывает отфильтрованную выборку и не подменяет страницу непустой

### Requirement: Stateful module actions and derived views

Mock API SHALL предоставлять `GET /assistant-modules/v1/modules/summary`, `GET /assistant-modules/v1/modules/preview`, `POST /assistant-modules/v1/modules/{module_id}/enable` и `POST /assistant-modules/v1/modules/{module_id}/disable`. Все представления SHALL отражать одно состояние модулей; restart SHALL восстанавливать seed. Поле by SHALL обозначать фиксированного автора mock-изменения, не сессию посетителя.

Обе мутации SHALL требовать expected_version >= 1. По локальной конвенции несовпадение версии SHALL возвращать 409 без изменений. Отключение с disable_allowed=false SHALL возвращать 409; при непустом disable_impact_message отсутствие confirm_impact=true SHALL возвращать 409. Успешная мутация SHALL увеличивать version на 1, обновлять updated_at/by и задавать целевой status, включая повтор целевого состояния с актуальной версией. Disable SHALL сохранять user_message (default пустая строка), enable SHALL сбрасывать его в null. Эти правила ошибок и переходов SHALL документироваться только как mock-конвенции, без изменения OpenAPI.

#### Scenario: Disable and enable affect every view

- **WHEN** разрешённый модуль отключён с актуальной версией и необходимым подтверждением, затем включён с новой версией
- **THEN** ответы соответствуют ModuleResponse; список, summary и preview после каждого действия согласованы; отключённый модуль появляется и затем исчезает из disabled_modules и fallback-карточек

#### Scenario: Summary and preview states

- **WHEN** запрошены summary и preview
- **THEN** totals вычисляются по всей коллекции, независимо от фильтра списка; при наличии отключённых модулей состояние degraded и banner tone warning, иначе healthy и success; preview содержит по одной fallback-карточке на отключённый модуль и ни одной для включённых

#### Scenario: Preview fallback text

- **WHEN** отключённый модуль имеет непустой user_message либо пустой user_message
- **THEN** assistant_message содержит соответственно сохранённый текст либо документированный mock-текст по умолчанию

#### Scenario: Rejected actions preserve state

- **WHEN** версия устарела, отключение запрещено или требуется неподтверждённое предупреждение
- **THEN** ответ 409 использует документированный mock error envelope, а status, version, updated_at, by и все производные представления не меняются

#### Scenario: Invalid action and missing module

- **WHEN** отсутствует expected_version, передан 0, невалидный UUID или корректный UUID отсутствующего модуля
- **THEN** первые три случая возвращают контрактный 422, последний — mock 404, без изменения состояния

#### Scenario: Fresh server state

- **WHEN** после мутаций создаётся новый экземпляр mock server
- **THEN** он получает исходные версии и статусы seed, независимо от предыдущего экземпляра
