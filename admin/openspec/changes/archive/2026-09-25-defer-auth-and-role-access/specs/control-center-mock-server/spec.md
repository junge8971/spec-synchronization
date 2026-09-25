## MODIFIED Requirements

### Requirement: Development proxy rewrite

Dev-сервер SHALL проксировать только API-префикс `/api/control/api` в mock server с rewrite этого префикса в `/api`. Метод, query string, body и переданные HTTP-заголовки, включая Idempotency-Key, SHALL сохраняться. Прокси MUST NOT добавлять credentials или требовать сессию для бизнес-запросов к локальному mock server.

#### Scenario: Request through browser origin

- **WHEN** клиент отправляет POST `/api/control/api/skills/v1/domains?query=test` с JSON и обязательным заголовком идемпотентности без Authorization
- **THEN** mock server получает POST `/api/skills/v1/domains?query=test` с теми же телом и заголовками без добавленного токена

#### Scenario: Non-API routes

- **WHEN** запрашивается `/tsam-panel/`, ассет либо `/api/control/apix`
- **THEN** запрос не попадает под mock API rewrite

### Requirement: Production isolation and opt-out

Production build/start, preview и dev с `CONTROL_API_MOCKS=false` MUST NOT запускать mock server или активировать mock rewrite. Клиентская production-сборка MUST NOT содержать server handlers или runtime mock fixtures. Dev и production MUST NOT подставлять mock token. Mock-порт SHALL настраиваться через `CONTROL_API_MOCK_PORT` с default 3001; локальный mock server SHALL оставаться на loopback и MUST NOT использоваться как production backend.

#### Scenario: Build without mock listener

- **WHEN** выполняется production build и запускается production/preview приложение
- **THEN** mock-порт не открывается, runtime seed не включён в клиентский bundle, запросы используют настроенный backend URL без mock credentials

#### Scenario: Explicitly disabled mocks

- **WHEN** `yarn dev` запущен с `CONTROL_API_MOCKS=false`
- **THEN** приложение не обращается к локальному mock target и не подставляет mock Bearer

### Requirement: Complete supplied operation coverage

Mock API SHALL реализовать 27 бизнес-операций поставленного OpenAPI: Domains/Skills — 8, Surfaces — 11, Teams — 8. Ответы SHALL соответствовать описанным status codes, envelope, схемам, nullable/required полям, enum и форматам. Access-операция `GET /api/control/api/auth/v1/me` SHALL быть явно исключена из текущего покрытия и MUST NOT обслуживаться mock server. Отсутствие Bearer MUST NOT препятствовать чтению или мутациям бизнес-данных. Это SHALL документироваться как ограничение локального mock server, а не изменение требований безопасности backend. Непредоставленные семь разделов MUST NOT выдаваться за реализованный контракт.

#### Scenario: Contract coverage check

- **WHEN** контрактные тесты перечисляют операции исходного OpenAPI
- **THEN** для каждой из 27 бизнес-операций имеется исполняемый сценарий без Authorization с проверкой ответа по схеме; единственное явное исключение — указанная Access-операция, а пропуск любой бизнес-операции вызывает падение проверки

#### Scenario: Invalid contract input

- **WHEN** без Authorization передан невалидный UUID/UUIDv7, enum, limit/offset, обязательное тело или отсутствует обязательный Idempotency-Key
- **THEN** mock server возвращает предусмотренный validation response, а не 401 или успешные данные; тело 422 соответствует HTTPValidationError там, где он описан

#### Scenario: Unknown resource or absent credentials

- **WHEN** без Bearer запрошен отсутствующий корректный ID бизнес-сущности
- **THEN** сервер возвращает 404 по документированной mock error convention без изменения исходного OpenAPI

#### Scenario: Retired current principal endpoint

- **WHEN** запрошен `/api/auth/v1/me` у локального mock server
- **THEN** возвращается 404 как для отсутствующей операции, без фиктивного пользователя или запуска сессии

### Requirement: Stateful coherent fixtures

Все runtime mock-данные существующих навыков, карточек и справочников бизнес-сущностей, поверхностей, команд и участников SHALL обслуживаться на сервере. Связанные team/domain/skill/surface/user ID SHALL согласовываться. Мутации SHALL влиять на последующие чтения; restart SHALL восстанавливать исходный seed. Недокументированные business rules SHALL явно обозначаться mock-конвенциями. Данные текущего авторизованного пользователя MUST NOT синтезироваться; записи пользователей как контактов и участников команд SHALL сохраняться независимо от отсутствия сессии.

#### Scenario: Mutation followed by reads

- **WHEN** создаётся или обновляется сущность, участник команды либо конфигурация/набор навыков поверхности без Authorization
- **THEN** последующие соответствующие list/detail запросы отражают изменение и не содержат противоречивых связанных ID

#### Scenario: Surface actions

- **WHEN** выполняется одна из операций sandbox, publish, disable, enable, archive или restore
- **THEN** ответ и последующее чтение содержат согласованный статус из SurfaceStatus согласно опубликованной mock-конвенции

#### Scenario: Idempotent domain or skill mutation

- **WHEN** одна и та же мутация домена/навыка повторена с тем же ключом и телом
- **THEN** возвращается прежний результат без второго изменения; другой body с тем же method/path/key даёт документированный mock conflict 409

#### Scenario: Isolated test data

- **WHEN** запускается новый экземпляр mock server для теста или после restart
- **THEN** состояние возвращается к seed и не наследует мутации другого тестового экземпляра

#### Scenario: Business users are not session principals

- **WHEN** читаются контакт навыка или участники команды
- **THEN** возвращаются согласованные бизнес-данные пользователей, но они не назначают посетителю роль, сессию или права
