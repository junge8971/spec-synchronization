## MODIFIED Requirements

### Requirement: Existing screens consume HTTP data

Реестры навыков и поверхностей, карточка навыка и справочники фильтров SHALL получать серверные данные через общий HTTP transport. Runtime-клиенты MUST NOT возвращать встроенные fixtures, генерировать дополнения карточки или заменять ошибки локальным успехом. В real mode оболочка SHALL выполнять bootstrap согласно mpmm-session, получать `/auth/v1/me` и не монтировать/запускать бизнес-загрузки до подтверждения сессии и доступа. В mock mode оболочка SHALL получать mock principal согласно add-local-session-demo без реальных MPMM credentials; режим MUST NOT определяться hostname. Статические статьи справки, навигация, локализация и test doubles не относятся к runtime mock API. При замене/утрате контекста SHALL удаляться пользовательский кэш и нейтрализоваться поздние ответы прежнего контекста.

#### Scenario: Registry request failure

- **WHEN** разрешённый запрос реестра завершается сетевой ошибкой
- **THEN** пользователь видит error/retry, а не встроенные mock-записи

#### Scenario: Detail outside a loaded page

- **WHEN** разрешён переход на корректный skill UUID, отсутствующий на загруженной странице
- **THEN** выполняется отдельный detail-запрос, карточка не зависит от локальной полной выборки

#### Scenario: Missing or malformed detail identifier

- **WHEN** сервер разрешённого запроса возвращает 404 либо ссылка содержит невалидный slug-ID
- **THEN** интерфейс показывает отсутствие/некорректность ресурса без синтетической карточки; другие HTTP-ошибки не маскируются как 404

#### Scenario: Shell starts without authentication requests

- **WHEN** приложение запущено через yarn dev с mocksEnabled
- **THEN** оболочка не делает реальных authentication-запросов к MPMM; выбранный mock principal загружается по add-local-session-demo, неявный администратор не создаётся

#### Scenario: Protected shell starts with principal bootstrap

- **WHEN** приложение открывается в real mode с пригодными токенами, независимо от hostname
- **THEN** сначала подтверждается `/me`, затем загружаются только разрешённые бизнес-экраны и справочники

#### Scenario: Account replacement discards old data

- **WHEN** общая сессия заменена во время загрузки списка/карточки/файла
- **THEN** старые query results и file/object URL данные не показываются новому пользователю, поздний ответ старого контекста не восстанавливает их

#### Scenario: Server cache reset preserves same-user local work

- **WHEN** refresh сбрасывает пользовательский query/mutation cache, затем `/me` подтверждает прежнего пользователя и необходимые права
- **THEN** серверные результаты и файлы не переиспользуются из старого контекста, но черновик и параметры незавершённой логической операции сохраняются согласно mpmm-session; автоматического replay нет

#### Scenario: Late mutation cannot persist into a replacement context

- **WHEN** общая сессия инвалидирована до завершения мутации или автосохранения прежней формы
- **THEN** позднее завершение не записывает черновик и не меняет состояние нового контекста, даже если AbortSignal проигнорирован; отсутствие подтверждённого ответа не считается доказательством отмены серверной операции

### Requirement: User-visible network states and integration verification

Существующие экраны SHALL различать loading, error с повтором, empty, unavailable и отказ по permissions. В защищённом режиме SHALL дополнительно различаться bootstrap, ошибка подтверждения сессии и переход на вход. Сценарии UI SHALL проверяться unit/component-тестами, бизнес-операции локального mock server — server-тестами по HTTP без токена; конфигурация dev proxy/rewrite SHALL проверяться без обязательного браузерного запуска. Auth-сценарии SHALL использовать test doubles storage/fetch/clock/location, а runtime mock `/me` описан отдельным add-local-session-demo. Production build SHALL проверяться независимо от dev-моков. E2E/browser-тесты MUST NOT создаваться, редактироваться или запускаться без отдельного явного разрешения пользователя.

#### Scenario: Empty data versus failed request

- **WHEN** API разрешённой операции возвращает валидный пустой список либо ошибку
- **THEN** первый случай показывает empty, второй — error/retry; повтор действительно выполняет новый запрос при действующей сессии и праве

#### Scenario: Browser smoke test

- **WHEN** проверяются оболочка, сессия и бизнес-сценарии без разрешения на browser-тесты
- **THEN** unit/component/server-проверки подтверждают real и mock режимы, permissions, HTTP, refresh и cache isolation; браузерные тесты не запускаются и не меняются

#### Scenario: Backend denies a business request

- **WHEN** реальный backend отвечает 401 или 403
- **THEN** экран не показывает фиктивный успех; защищённый 401 обрабатывается согласно mpmm-session без replay, 403 остаётся отказом без refresh, в mock mode сохраняется штатная ошибка без real session recovery
