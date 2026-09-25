## Purpose

Предоставить воспроизводимый локальный HTTP API Центра управления, который автоматически доступен при разработке и соответствует предоставленным контрактам без включения моков в production.

## ADDED Requirements

### Requirement: Automatic development lifecycle

Команда `yarn dev` SHALL автоматически запускать mock HTTP server на loopback и делать его доступным до готовности приложения принимать API-запросы. Остановка или перезапуск dev-сервера SHALL закрывать mock listener и его соединения. При конфликте порта запуск SHALL завершаться понятной ошибкой, а не обращаться к постороннему процессу.

#### Scenario: One-command startup and restart

- **WHEN** разработчик запускает `yarn dev`, останавливает его и запускает снова
- **THEN** API доступен без второй команды, а mock-порт повторно используется без оставшегося listener

#### Scenario: Occupied mock port

- **WHEN** настроенный mock-порт занят другим процессом
- **THEN** dev-запуск сообщает конфликт и не объявляет API готовым

### Requirement: Development proxy rewrite

Dev-сервер SHALL проксировать только API-префикс `/api/control/api` в mock server с rewrite этого префикса в `/api`. Метод, query string, body, Authorization и Idempotency-Key SHALL сохраняться.

#### Scenario: Request through browser origin

- **WHEN** браузер отправляет POST `/api/control/api/skills/v1/domains?query=test` с JSON и обязательными заголовками
- **THEN** mock server получает POST `/api/skills/v1/domains?query=test` с теми же телом и заголовками

#### Scenario: Non-API routes

- **WHEN** запрашивается `/tsam-panel/`, ассет либо `/api/control/apix`
- **THEN** запрос не попадает под mock API rewrite

### Requirement: Production isolation and opt-out

Production build/start, preview и dev с `CONTROL_API_MOCKS=false` MUST NOT запускать mock server или активировать mock rewrite/token. Клиентская production-сборка MUST NOT содержать server handlers или runtime mock fixtures. Mock-порт SHALL настраиваться через `CONTROL_API_MOCK_PORT` с default 3001.

#### Scenario: Build without mock listener

- **WHEN** выполняется production build и запускается production/preview приложение
- **THEN** mock-порт не открывается, runtime seed не включён в клиентский bundle, запросы используют настроенный backend URL

#### Scenario: Explicitly disabled mocks

- **WHEN** `yarn dev` запущен с `CONTROL_API_MOCKS=false`
- **THEN** приложение не обращается к локальному mock target и не подставляет mock Bearer

### Requirement: Complete supplied operation coverage

Mock API SHALL реализовать все 28 method/path пар полного OpenAPI: Access — 1, Domains/Skills — 8, Surfaces — 11, Teams — 8. Ответы SHALL соответствовать описанным status codes, envelope, схемам, nullable/required полям, enum и форматам. Непредоставленные семь разделов MUST NOT выдаваться за реализованный контракт.

#### Scenario: Contract coverage check

- **WHEN** контрактные тесты перечисляют операции исходного OpenAPI
- **THEN** для каждой из 28 операций имеется исполняемый сценарий с проверкой её ответа по схеме; пропущенная операция вызывает падение проверки

#### Scenario: Invalid contract input

- **WHEN** передан невалидный UUID/UUIDv7, enum, limit/offset, обязательное тело или отсутствует обязательный Idempotency-Key
- **THEN** mock server возвращает предусмотренный контрактом validation response, а не успешные данные; тело 422 соответствует HTTPValidationError там, где он описан

#### Scenario: Unknown resource or absent credentials

- **WHEN** запрошен отсутствующий корректный ID либо отсутствует Bearer
- **THEN** сервер возвращает соответственно 404 либо 401 по документированной mock error convention без изменения исходного OpenAPI

### Requirement: Stateful coherent fixtures

Все runtime mock-данные существующих навыков, карточек, справочников, поверхностей и текущего пользователя SHALL обслуживаться на сервере. Связанные team/domain/skill/surface/user ID SHALL согласовываться. Мутации SHALL влиять на последующие чтения; restart SHALL восстанавливать исходный seed. Недокументированные business rules SHALL явно обозначаться mock-конвенциями.

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

### Requirement: Server-side collection behavior

Фильтрация и сортировка SHALL выполняться до пагинации по контрактным query-параметрам. Списки SHALL возвращать `items` и согласованный `pagination` с limit, offset, current_page, total_items и total_pages. Сервер MUST NOT подменять offset за концом списка последней непустой страницей.

#### Scenario: Filtered paginated list

- **WHEN** запрошен отфильтрованный список с limit 10 и offset 10
- **THEN** возвращается соответствующий срез отсортированной выборки, а total_items учитывает фильтры до среза

#### Scenario: Offset beyond the result

- **WHEN** offset больше числа подходящих записей
- **THEN** items пуст, total_items остаётся достоверным, а сервер не возвращает записи другой страницы
