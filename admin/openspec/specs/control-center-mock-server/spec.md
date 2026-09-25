# Control Center Mock Server Specification

## Purpose

Предоставить воспроизводимый локальный HTTP API Центра управления, который автоматически доступен при разработке и соответствует предоставленным контрактам без включения моков в production.

## Requirements

### Requirement: Automatic development lifecycle

Команда `yarn dev` SHALL автоматически запускать mock HTTP server на loopback и делать его доступным до готовности приложения принимать API-запросы. Остановка или перезапуск dev-сервера SHALL закрывать mock listener и его соединения. При конфликте порта запуск SHALL завершаться понятной ошибкой, а не обращаться к постороннему процессу.

#### Scenario: One-command startup and restart

- **WHEN** разработчик запускает `yarn dev`, останавливает его и запускает снова
- **THEN** API доступен без второй команды, а mock-порт повторно используется без оставшегося listener

#### Scenario: Occupied mock port

- **WHEN** настроенный mock-порт занят другим процессом
- **THEN** dev-запуск сообщает конфликт и не объявляет API готовым

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

- **WHEN** передан невалидный UUID/UUIDv7, enum, limit/offset, обязательное тело или отсутствует обязательный Idempotency-Key
- **THEN** mock server возвращает предусмотренный контрактом validation response, а не успешные данные; тело 422 соответствует HTTPValidationError там, где он описан

#### Scenario: Unknown resource or absent credentials

- **WHEN** без Bearer запрошен отсутствующий корректный ID бизнес-сущности
- **THEN** сервер возвращает 404 по документированной mock error convention без изменения исходного OpenAPI

#### Scenario: Retired current principal endpoint

- **WHEN** запрошен `/api/auth/v1/me` у локального mock server
- **THEN** возвращается 404 как для отсутствующей операции, без фиктивного пользователя или запуска сессии

### Requirement: Stateful coherent fixtures

Все runtime mock-данные существующих навыков, карточек и справочников бизнес-сущностей, поверхностей, команд и участников SHALL обслуживаться на сервере. Связанные team/domain/skill/surface/user ID SHALL согласовываться. Мутации SHALL влиять на последующие чтения; restart SHALL восстанавливать исходный seed. Недокументированные business rules SHALL явно обозначаться mock-конвенциями. Данные текущего авторизованного пользователя MUST NOT синтезироваться; записи пользователей как контактов и участников команд SHALL сохраняться независимо от отсутствия сессии.

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
- **THEN** возвращаются согласованные бизнес-данные пользователей, но они не назначают посетителю роль, сессию или права

### Requirement: Server-side collection behavior

Фильтрация и сортировка SHALL выполняться до пагинации по контрактным query-параметрам. Списки SHALL возвращать `items` и согласованный `pagination` с limit, offset, current_page, total_items и total_pages. Сервер MUST NOT подменять offset за концом списка последней непустой страницей.

#### Scenario: Filtered paginated list

- **WHEN** запрошен отфильтрованный список с limit 10 и offset 10
- **THEN** возвращается соответствующий срез отсортированной выборки, а total_items учитывает фильтры до среза

#### Scenario: Offset beyond the result

- **WHEN** offset больше числа подходящих записей
- **THEN** items пуст, total_items остаётся достоверным, а сервер не возвращает записи другой страницы
