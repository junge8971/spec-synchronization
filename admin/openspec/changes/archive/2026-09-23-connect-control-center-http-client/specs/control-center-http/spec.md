## Purpose

Обеспечить единое контрактное HTTP-взаимодействие фронтенда Центра управления с backend и dev-сервером без альтернативного пути через локальные моки.

## ADDED Requirements

### Requirement: Contract-aligned requests

Приложение SHALL отправлять API-запросы относительно настраиваемого базового URL, по умолчанию `/api/control/api`, с методами, параметрами, заголовками и JSON-телами из `docs/api/contracts/openapi.json`. UI base `/tsam-panel/` MUST NOT добавляться к API URL. Неопределённые optional query-параметры MUST NOT передаваться строками `undefined` или `null`.

#### Scenario: Paginated request with search

- **WHEN** запрошены навыки с поиском «Моя Москва», limit 10 и offset 20
- **THEN** запрос направлен на `/api/control/api/skills/v1/skills` с корректно закодированным query, limit и offset, без UI-префикса и отсутствующих фильтров

#### Scenario: Contract source changes

- **WHEN** контракт изменён без обновления производных TypeScript DTO
- **THEN** проверка синхронизации типов завершается ошибкой, а не подтверждает совместимость устаревших типов

### Requirement: Authentication and mutation headers

Транспорт SHALL передавать предоставленный Bearer token и поддерживать `Idempotency-Key` для операций, требующих его по контракту. Повтор одной логической мутации SHALL сохранять ключ; новая мутация SHALL получать новый ключ. Транспорт MUST NOT автоматически повторять мутации, хранить токены в localStorage, логировать их или подставлять mock token вне mock-dev режима.

#### Scenario: Authenticated idempotent mutation

- **WHEN** вызывается создание домена с предоставленными токеном и ключом идемпотентности
- **THEN** POST содержит `Authorization: Bearer …`, исходный `Idempotency-Key` и контрактное JSON-тело

#### Scenario: Production without credentials

- **WHEN** приложение запущено вне mock-dev режима без токена
- **THEN** запрос не получает фиктивный dev-токен и ошибка авторизации не заменяется успешным mock-ответом

### Requirement: Observable response and error handling

Транспорт SHALL проверять успешный envelope и используемые данные, возвращать `data` и сохранять status/message/code/details доступных ошибок. Non-2xx, непустой envelope `errors` и невалидное успешное тело SHALL приводить к различимым ошибкам, а не к пустому результату. `ResponseCode` MUST NOT интерпретироваться как недокументированный enum успеха.

#### Scenario: Valid success envelope

- **WHEN** сервер возвращает 200 с контрактным data и произвольной допустимой строкой code без errors
- **THEN** вызывающий код получает проверенные данные независимо от конкретного литерала code

#### Scenario: Validation and access errors

- **WHEN** сервер возвращает 422 с validation details либо 401/403
- **THEN** ошибка сохраняет HTTP status и доступные детали; приложение не запускает придуманную refresh/login-последовательность и не повторяет 4xx автоматически

#### Scenario: HTML failure or malformed success

- **WHEN** сервер возвращает HTML с 500 либо невалидный JSON/envelope с 200
- **THEN** первый ответ сохраняется как HTTP-ошибка 500, второй — как ошибка протокола; ни один не превращается в успешный пустой список

#### Scenario: Empty response and application error

- **WHEN** получен успешный 204 без тела либо JSON с непустым errors
- **THEN** 204 обрабатывается без JSON parse error, а непустой errors передаётся как ошибка, даже при HTTP 200

### Requirement: Cancellation

API-запросы SHALL поддерживать отмену со стороны потребителя; отменённый запрос MUST NOT подменять результат актуального запроса или отображаться как обычная серверная ошибка.

#### Scenario: Filter changes during a request

- **WHEN** пользователь меняет фильтр до завершения предыдущего запроса и предыдущий запрос отменяется
- **THEN** отмена доходит до HTTP-транспорта, старый результат не заменяет новый и отменённый запрос не повторяется автоматически
