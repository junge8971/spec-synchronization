# Control Center API Integration Specification

## Purpose

Перевести существующие экраны Центра управления на HTTP и актуальные API-данные, сохраняя понятные состояния интерфейса и явно обозначая отсутствующую в контрактах функциональность.

## Requirements

### Requirement: Existing screens consume HTTP data

Реестры навыков и поверхностей, карточка навыка и справочники фильтров SHALL получать серверные данные через общий HTTP transport. Runtime-клиенты MUST NOT возвращать встроенные fixtures, генерировать дополнения карточки или заменять ошибки локальным успехом. Оболочка MUST NOT запрашивать текущего пользователя, выполнять bootstrap сессии или обращаться к auth endpoints. Статические статьи справки, навигация, локализация и test doubles не относятся к runtime mock API.

#### Scenario: Registry request failure

- **WHEN** запрос реестра завершается сетевой ошибкой
- **THEN** пользователь видит error/retry, а не старые встроенные mock-записи

#### Scenario: Detail outside a loaded page

- **WHEN** открыта ссылка на корректный skill UUID, которого нет на загруженной странице списка
- **THEN** выполняется отдельный detail-запрос; карточка не зависит от поиска в текущей или полной локальной выборке

#### Scenario: Missing or malformed detail identifier

- **WHEN** сервер возвращает 404 для detail либо ссылка содержит старый невалидный slug-ID
- **THEN** интерфейс показывает отсутствие/некорректность ресурса без синтетической карточки; прочие HTTP-ошибки не маскируются как 404

#### Scenario: Shell starts without authentication requests

- **WHEN** приложение открывается или пользователь переключает разделы
- **THEN** оболочка не обращается к `/auth/v1/me` или другим auth endpoints, не ожидает профиль и не отображает фиктивного администратора

### Requirement: Contract-compatible filters and pagination

UI SHALL использовать контрактные ID, фильтры и сортировки: UUID domain_id вместо фиксированного slug domain, limit/offset вместо page/pageSize на wire, SurfaceStatus `review`, SurfaceType `mobile_application`, SurfaceListSort с `-field`. Неподдержанный status-фильтр/сортировка навыков MUST NOT отправляться или вычисляться только по загруженной странице. Устаревшие URL filter/sort values SHALL нормализоваться к поддержанным значениям/defaults.

#### Scenario: Selecting a domain and another page

- **WHEN** пользователь выбирает домен и затем страницу 3 с размером 10
- **THEN** API получает выбранный domain_id, limit 10, offset 20; количество записей и страниц берётся из ответа, а не локального seed

#### Scenario: Domain options exceed one API page

- **WHEN** число доменов превышает размер страницы справочника
- **THEN** пользователь может выбрать домен за пределами первой страницы; варианты не ограничены фиксированным массивом

#### Scenario: Surface filter and sorting

- **WHEN** выбраны «Проверка», «мобильное приложение» и убывание даты изменения
- **THEN** API получает status=review, type=mobile_application и sort=-updated_at

#### Scenario: Legacy URL parameters

- **WHEN** открыта ссылка со старым skill status sort, slug домена или устаревшими surface enum
- **THEN** URL-state нормализуется без отправки неподдержанного значения backend и без скрытой локальной фильтрации

### Requirement: Truthful representation of contract fields

UI SHALL отображать integer version, nullable service_id/channel_id/connection, вложенные domain/team/contact, zones и surface stats согласно DTO. Отсутствующие в контракте статусы/готовность/метрики навыков, ревью, интенты, проверки, история и токены MUST NOT синтезироваться или выдаваться за API-данные. Сохраняемые неподдержанные блоки SHALL показывать явное unavailable-состояние, а соответствующие действия/фильтры SHALL быть недоступны или удалены.

#### Scenario: Missing skill lifecycle API

- **WHEN** открыта карточка с валидным SkillResponse без review, intents, checks, history и tokens
- **THEN** поддерживаемые поля отображаются, а неподдержанные блоки сообщают «Не поддерживается текущим API» без mock review, успешных проверок или фиктивных токенов

#### Scenario: Null versus zero

- **WHEN** dialogs_30d равен null, а у другой поверхности равен 0
- **THEN** первая показывает отсутствие данных, вторая — реальный ноль; nullable connection/service_id не ломают карточку

### Requirement: User-visible network states and integration verification

Существующие экраны SHALL различать loading, error с повтором, empty и unavailable. Сценарии UI SHALL проверяться unit/component-тестами, бизнес-операции локального mock server — server-тестами по HTTP без токена; конфигурация dev proxy/rewrite SHALL проверяться без обязательного браузерного запуска. Production build SHALL проверяться независимо от dev-моков. E2E/browser-тесты MUST NOT создаваться, редактироваться или запускаться без отдельного явного разрешения пользователя.

#### Scenario: Empty data versus failed request

- **WHEN** API возвращает валидный пустой список либо завершается ошибкой
- **THEN** первый случай показывает empty, второй — error/retry; повтор ошибки действительно выполняет новый HTTP-запрос

#### Scenario: Browser smoke test

- **WHEN** проверяются навыки, карточка, поверхности и оболочка без разрешения на browser-тесты
- **THEN** unit/component/server-проверки подтверждают навигацию без сессии, отсутствие auth-запросов, работу бизнес-HTTP без Bearer, фильтрацию, пагинацию и detail; браузерные тесты не запускаются и не меняются

#### Scenario: Backend denies a business request

- **WHEN** реальный backend отвечает 401 или 403 на бизнес-запрос
- **THEN** экран показывает ошибку запроса без фиктивного успеха, login/refresh-последовательности или блокирования остальных навигационных ссылок
