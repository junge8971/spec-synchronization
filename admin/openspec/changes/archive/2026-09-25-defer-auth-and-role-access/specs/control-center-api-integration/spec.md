## MODIFIED Requirements

### Requirement: Existing screens consume HTTP data

Реестры навыков и поверхностей, карточка навыка и справочники фильтров SHALL получать серверные данные через общий HTTP transport. Runtime-клиенты MUST NOT возвращать встроенные fixtures, генерировать дополнения карточки или заменять ошибки локальным успехом. Оболочка MUST NOT запрашивать текущего пользователя, выполнять bootstrap сессии или обращаться к auth endpoints. Статические статьи справки, навигация, локализация и test doubles не относятся к runtime mock API.

#### Scenario: Registry request failure

- **WHEN** запрос реестра завершается сетевой ошибкой
- **THEN** пользователь видит error/retry, а не старые встроенные mock-записи

#### Scenario: Detail outside a loaded page

- **WHEN** открыта ссылка на корректный skill UUID, которого нет на загруженной странице списка
- **THEN** выполняется отдельный detail-запрос; карточка не зависит от поиска в текущей или полной локальной выборки

#### Scenario: Missing or malformed detail identifier

- **WHEN** сервер возвращает 404 для detail либо ссылка содержит старый невалидный slug-ID
- **THEN** интерфейс показывает отсутствие/некорректность ресурса без синтетической карточки; прочие HTTP-ошибки не маскируются как 404

#### Scenario: Shell starts without authentication requests

- **WHEN** приложение открывается или пользователь переключает разделы
- **THEN** оболочка не обращается к `/auth/v1/me` или другим auth endpoints, не ожидает профиль и не отображает фиктивного администратора

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

## REMOVED Requirements

### Requirement: Current principal in the header

**Reason**: Авторизационный API и роли не определены и исключены из текущего этапа.
**Migration**: Удалить загрузку current principal, её runtime-клиент и отображение имени/ролей/scope; не заменять их фикстурой, гостевой сессией или назначением административных прав.
