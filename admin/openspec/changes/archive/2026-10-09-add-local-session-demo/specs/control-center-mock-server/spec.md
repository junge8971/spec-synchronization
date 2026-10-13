## MODIFIED Requirements

### Requirement: Production isolation and opt-out

Production build/start, preview и dev с `CONTROL_API_MOCKS=false` MUST NOT запускать mock server или активировать mock rewrite. Клиентская production-сборка MUST NOT содержать server handlers, runtime mock fixtures, каталог тестовых пользователей или рабочий demo-switcher даже при CONTROL_API_MOCKS=true. Dev и production MUST NOT подставлять mock token. Mock-порт SHALL настраиваться через `CONTROL_API_MOCK_PORT` с default 3001; локальный mock server SHALL оставаться на loopback и MUST NOT использоваться как production backend. Local-session-demo SHALL включаться вместе с бизнес-моками по существующему mocksEnabled в локальном dev; CONTROL_API_MOCKS=false SHALL отключать все моки.

#### Scenario: Build without mock listener

- **WHEN** выполняется production build, в том числе с CONTROL_API_MOCKS=true, и запускается production/preview приложение
- **THEN** mock-порт не открывается, runtime seed/test users не включены в клиентский bundle, запросы используют штатный backend без mock credentials и demo API

#### Scenario: Explicitly disabled mocks

- **WHEN** обычный dev запущен с `CONTROL_API_MOCKS=false`
- **THEN** приложение не обращается к локальному mock target и не подставляет mock Bearer; opt-out отключает также demo principal и выбирает настроенные real API/auth; отсутствие обязательной конфигурации даёт явную ошибку, а не полный доступ

### Requirement: Complete supplied operation coverage

Mock API SHALL сохранять все ранее принятые бизнес-операции объединённого OpenAPI: Domains/Skills, включая PUT intents и POST status, Surfaces, Teams, Assistant modules, Analytics и принятые dialog handlers. Ответы SHALL соответствовать описанным status codes, envelope, схемам, nullable/required полям, enum и форматам. Access-операция `GET /api/control/api/auth/v1/me` SHALL оставаться исключением из обычного бизнес-покрытия и обслуживаться только при явно включённом local-session-demo. Отсутствие Bearer MUST NOT препятствовать чтению или мутациям бизнес-данных. Это SHALL документироваться как ограничение mock server, а не изменение требований backend. Непредоставленные разделы MUST NOT выдаваться за реализованный контракт; принятые ответы unavailable для отсутствующих реализаций SHALL сохраняться. Mock-семантика аналитики и смены статуса MUST NOT выдаваться за production-гарантию вычислений или допустимых переходов.

#### Scenario: Contract coverage check

- **WHEN** контрактные тесты перечисляют операции текущего объединённого OpenAPI
- **THEN** все ранее проверяемые бизнес-операции сохраняют исполняемые сценарии без Authorization с проверкой схемы, пропуск handler вызывает падение; `/me` отдельно проверяется как 404 у standalone test app без sessionDemo и контрактный principal в demo

#### Scenario: Invalid contract input

- **WHEN** передан невалидный UUID/UUIDv7, enum, limit/offset, обязательное тело или отсутствует обязательный Idempotency-Key
- **THEN** mock server возвращает предусмотренный контрактом validation response, а не успешные данные; тело 422 соответствует HTTPValidationError там, где он описан

#### Scenario: Unknown resource or absent credentials

- **WHEN** без Bearer запрошен отсутствующий корректный ID бизнес-сущности
- **THEN** сервер возвращает 404 по документированной mock error convention без изменения исходного OpenAPI

#### Scenario: Retired current principal endpoint

- **WHEN** запрошен `/api/auth/v1/me` у локального mock server без local-session-demo
- **THEN** возвращается 404 как для отсутствующей операции, без фиктивного пользователя или запуска сессии

#### Scenario: Explicit demo current principal

- **WHEN** у явно настроенного demo mock server запрошен `/api/auth/v1/me`
- **THEN** возвращается выбранный тестовый principal по текущей схеме, без требования токенов; каталог профилей доступен только в этом же режиме

#### Scenario: Filter skills by status

- **WHEN** запрошена страница навыков с status и другими поддерживаемыми фильтрами
- **THEN** фильтрация применяется до пагинации, DTO содержит status, а total соответствует полной отфильтрованной выборки

#### Scenario: New operations preserve coherent mock state

- **WHEN** выполняются опубликованные изменение статуса навыка или сохранение аналитической доски
- **THEN** последующие чтения отражают сохранённое mock-состояние, ответ проходит соответствующую схему; restart восстанавливает seed, а правила, отсутствующие в контракте, документируются как локальная mock-конвенция

## ADDED Requirements

### Requirement: Local response scenario selection

Только sessionDemo mock server SHALL предоставлять каталог операций и фиксированных сценариев для простой локальной панели «Моки». Выбор SHALL передаваться несекретным header конкретного запроса, без глобального server state. Неизвестный сценарий SHALL возвращать 400. Сценарии SHALL применяться после проверки контрактного ввода и до handler/idempotency: фиксированные HTTP 403/500 не меняют данные; задержка 1500 мс сохраняет штатные бизнес-проверки и не выполняет handler после отмены запроса. Штатный сценарий SHALL сохранять прежнее покрытие и существующие unavailable ответы. Сценарий 403 SHALL быть фиксированным ответом для проверки обработки backend-отказа; он MUST NOT вычисляться из roles/permissions. Mock server MUST NOT добавлять ролевую авторизацию бизнес-операций. Каталоги SHALL оставаться доступны независимо от сценария `/me`. Вне sessionDemo каталог SHALL возвращать 404, scenario headers MUST NOT менять бизнес-поведение.

#### Scenario: Invalid mutation under a scenario

- **WHEN** запрос содержит невалидное тело или не содержит обязательного Idempotency-Key и выбран сценарий
- **THEN** сохраняется контрактный validation response, операция не выполняется

#### Scenario: Scenario does not mutate server data

- **WHEN** корректная мутация получает выбранный HTTP 403 либо 500
- **THEN** handler не вызывается, последующее штатное чтение видит прежнее состояние

## MODIFIED Requirements

### Requirement: Stateful coherent fixtures

Все runtime mock-данные существующих навыков, карточек и справочников бизнес-сущностей, поверхностей, команд и участников SHALL обслуживаться на сервере. Связанные team/domain/skill/surface/user ID SHALL согласовываться. Мутации SHALL влиять на последующие чтения; restart SHALL восстанавливать исходный seed. Недокументированные business rules SHALL явно обозначаться mock-конвенциями. Данные текущего пользователя SHALL обслуживаться отдельными серверными fixtures local-session-demo в dev; standalone test app без sessionDemo MUST NOT синтезировать principal. Записи пользователей как контактов и участников команд SHALL сохраняться независимо от demo principal, выбор которого MUST NOT сбрасывать business seed или менять назначения бизнес-сущностей.

#### Scenario: Mutation followed by reads

- **WHEN** создаётся или обновляется сущность, участник команды либо конфигурация/набор навыков поверхности
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
- **THEN** возвращаются согласованные бизнес-данные пользователей, но они не назначают посетителю роль, сессию или права; demo fixtures не выводятся из этих записей

#### Scenario: Profile selection preserves business fixtures

- **WHEN** после mock-мутации пользователь меняет demo-профиль
- **THEN** подтверждённое business-состояние сохраняется на сервере, сбрасывается только клиентский контекст; mock не обещает фильтрацию данных по object scopes
