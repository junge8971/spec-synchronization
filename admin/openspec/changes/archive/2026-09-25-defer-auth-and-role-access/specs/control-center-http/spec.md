## MODIFIED Requirements

### Requirement: Authentication and mutation headers

Транспорт MUST NOT получать токены через auth-provider, автоматически добавлять `Authorization`, подставлять dev-токен или реализовывать получение/хранение/обновление сессии. Транспорт SHALL сохранять общий механизм явно переданных заголовков и поддерживать `Idempotency-Key` для операций, требующих его по контракту. Повтор одной логической мутации SHALL сохранять ключ; новая мутация SHALL получать новый ключ. Транспорт MUST NOT автоматически повторять мутации или маскировать ошибки backend.

#### Scenario: Authenticated idempotent mutation

- **WHEN** вызывается создание домена с ключом идемпотентности без явно переданного Authorization
- **THEN** POST содержит исходный `Idempotency-Key` и контрактное JSON-тело, но не содержит автоматически добавленного Authorization

#### Scenario: Production without credentials

- **WHEN** запрос отправляется в mock-dev, dev без моков или production без явно переданного Authorization
- **THEN** ни в одном режиме транспорт не добавляет Bearer или фиктивные credentials

#### Scenario: Explicit request headers

- **WHEN** вызывающий код передаёт допустимые HTTP-заголовки, включая существующий Idempotency-Key
- **THEN** транспорт сохраняет их значения и не заменяет их данными token provider

#### Scenario: Real access error

- **WHEN** backend возвращает 401 или 403
- **THEN** транспорт сохраняет статус и детали ошибки, не подставляет токен, не запускает вход/refresh и не повторяет запрос как авторизованный
