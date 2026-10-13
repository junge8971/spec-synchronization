## Purpose

Подключить фронтенд ЦАМ в real mode к существующей сессии MPMM, безопасно обновлять общие токены и получать подтверждённый пользовательский контекст без собственной системы входа.

## ADDED Requirements

### Requirement: Configured real mode shared session entry

Real mode SHALL включать MPMM auth независимо от hostname. Режим SHALL задаваться dev/build конфигурацией: yarn dev по умолчанию использует mocksEnabled, CONTROL_API_MOCKS=false выбирает real mode; production build/start/preview SHALL всегда использовать real mode, даже при CONTROL_API_MOCKS=true. До доступа к бизнес-экранам приложение SHALL прочитать `localStorage["token"]`, проверить наличие непустых строк access_token, admin_token, refresh_token и строкового id_token, затем загрузить текущего пользователя. Отсутствующий или повреждённый набор SHALL приводить к document navigation на настроенный login URL MPMM (текущий default `https://mobile-t-tech.mos.ru/sa-admin`) без передачи токенов или произвольного return URL. Исключение доступа к storage SHALL показывать блокирующую ошибку с повтором, а не бесконечный redirect. Mock mode SHALL работать без MPMM token/refresh/login, с mock principal по add-local-session-demo. Query/storage/hostname MUST NOT отключать auth. Сборка SHALL оставаться безопасной без browser globals, чтения пользовательской сессии и сетевых auth/business-запросов. Real mode SHALL применяться во время работы собранного приложения; start/preview SHALL обслуживать production-артефакты без изменения встроенного режима.

#### Scenario: Direct protected link without credentials

- **WHEN** в real mode открыт `/tsam-panel/skills/123` без пригодного набора токенов
- **THEN** бизнес-запросы не выполняются и браузер переходит на настроенный MPMM login URL, без добавления SPA basename

#### Scenario: Development mocks and production auth

- **WHEN** запущен yarn dev с mocksEnabled либо production build/start на произвольном hostname
- **THEN** dev использует mock principal без реальных credentials; production подтверждает реальную MPMM-сессию независимо от hostname

#### Scenario: Storage denied

- **WHEN** браузер запрещает чтение storage
- **THEN** защищённое содержимое не открывается, доступна понятная ошибка с повтором без удаления storage и redirect-loop

### Requirement: Shared token refresh

Приложение SHALL декодировать Base64URL payload admin_token и использовать конечный числовой exp только для планирования refresh, не как доказательство подлинности JWT. При exp <= текущему времени плюс 30 секунд SHALL выполняться POST на настроенный refresh URL MPMM (текущий default `https://mobile-t-tech.mos.ru/gateway/admin/api/v1/auth/refresh`) с четырьмя полями access_token, refresh_token, admin_token, id_token. Успех SHALL требовать валидного result без прикладной ошибки; полный набор SHALL сохраняться под прежним ключом с сохранением дополнительных серверных полей. Параллельные запросы одного экземпляра приложения SHALL ожидать один refresh и читать заголовки после него. Отмена одного ожидающего запроса MUST NOT отменять обновление для остальных. Некорректный JWT/exp SHALL считаться непригодной сессией, а не бессрочным токеном.

#### Scenario: Concurrent expired requests

- **WHEN** несколько запросов одновременно обнаруживают истекающий admin_token
- **THEN** выполняется один refresh и каждый продолжающийся запрос использует новый набор токенов

#### Scenario: Refresh protocol error

- **WHEN** refresh возвращает 200 с невалидным result либо error_code/error_message
- **THEN** старый token не перезаписывается, защищённые запросы не продолжаются как успешные и показывается различимая ошибка

#### Scenario: Refresh storage write failure

- **WHEN** успешный refresh не удаётся сохранить в storage
- **THEN** запросы не продолжаются со старым набором и показывается ошибка сохранения сессии

### Requirement: Validated current principal

После подготовки токенов приложение SHALL получать GET `/api/control/api/auth/v1/me` из настроенного допустимого Control API. Ответ SHALL проверяться как envelope data с обязательными user_id, sso_id, email, full_name, roles:string[], permissions:string[] и assignments[]. Назначение SHALL содержать id, role_id, role_name, scopes:string[], permissions:string[]. Старые display_name и одиночный scope MUST NOT требоваться или синтезироваться как серверные поля. До подтверждения principal бизнес-содержимое и его запросы SHALL оставаться закрытыми. Пустой permissions SHALL означать отсутствие выданных полномочий, а не администратора.

#### Scenario: Valid principal without business permissions

- **WHEN** `/me` возвращает валидного пользователя с пустым permissions
- **THEN** сессия подтверждена, но бизнес-действия недоступны; пользователь видит отсутствие прав и может открыть статическую справку

#### Scenario: Malformed principal

- **WHEN** `/me` не содержит обязательного permissions или assignments
- **THEN** отображается ошибка контракта с повтором без fallback-роли и без бизнес-запросов

### Requirement: Session error separation

Сетевые ошибки, 5xx и ошибки протокола refresh или `/me` SHALL блокировать защищённое содержимое с повтором, не удаляя общий token. 403 бизнес-операции SHALL сохраняться как отказ доступа и MUST NOT запускать refresh или вход. 401 refresh либо `/me` SHALL завершать локальный auth-контекст и направлять на вход MPMM без самостоятельного logout всей MPMM-сессии. При 401 бизнес-запроса приложение SHALL сохранить ошибку, приостановить новые бизнес-запросы, выполнить не более одной общей попытки refresh и заново `/me`; исходный запрос MUST NOT автоматически повторяться. Если подтверждение не восстановлено из-за 401, SHALL выполняться переход в MPMM; временный сбой SHALL давать retry-state. Последующий 401 с тем же уже восстановленным набором MUST NOT запускать бесконечный цикл refresh.

#### Scenario: Forbidden mutation

- **WHEN** сервер отклоняет мутацию с 403
- **THEN** показывается отказ, token сохраняется, refresh и replay отсутствуют

#### Scenario: Unauthorized mutation and recovered session

- **WHEN** мутация вернула 401, затем refresh и `/me` успешны
- **THEN** исходная операция не считается выполненной и не повторяется автоматически; пользователь может повторить её явно с сохранением правил идемпотентности

#### Scenario: Temporary service outage

- **WHEN** refresh либо `/me` возвращает 503
- **THEN** доступен повтор, общий storage не очищается и переход на вход не выполняется

### Requirement: Session generation isolation

Изменение или удаление общего token через storage event, а также обнаруженное при возврате фокуса либо перед запросом SHALL приостанавливать доступ, отменять/обезвреживать старые запросы и очищать principal и пользовательские query/file данные до повторного `/me`. Поздние ответы старого контекста MUST NOT восстанавливать старые данные или заменять новые токены. Перед сохранением refresh результат SHALL сравниваться с набором, для которого начат запрос; если storage изменён, результат SHALL отбрасываться в пользу повторной проверки актуальной сессии. После собственного успешного refresh права SHALL перечитываться до продолжения защищённых операций. Смена технического поколения MUST NOT сама по себе считаться сменой пользователя. После подтверждения того же `user_id` локальные черновики и параметры незавершённых логических операций SHALL сохраняться независимо от очистки query/mutation cache; видимость соответствующих форм и действий SHALL определяться актуальными permissions, без повторной permission-проверки в request/mutation handlers. При проверке/ошибке контекста бизнес-содержимое и действия SHALL оставаться заблокированными. При другом `user_id` или утрате сессии локальное состояние предыдущего пользователя MUST NOT переноситься в новый контекст. Поздние ответы MUST NOT инициировать скачивание или перезаписывать пользовательские черновики.

#### Scenario: MPMM account changes in another tab

- **WHEN** token заменён другой вкладкой во время загрузки карточки
- **THEN** карточка и кэш прежнего пользователя удаляются, её поздний ответ игнорируется, новый контекст загружается до бизнес-данных

#### Scenario: Late refresh after token removal

- **WHEN** token удалён до завершения refresh
- **THEN** завершившийся refresh не восстанавливает удалённый token и приложение переходит на вход

#### Scenario: Refresh preserves the same user's logical operation

- **WHEN** refresh и `/me` подтверждают прежний `user_id` и необходимые права после начала редактирования или неудачной мутации
- **THEN** черновик и прежние тело, версия и Idempotency-Key сохраняются для явного продолжения; очистка кэша не создаёт новую попытку и не запускает replay

#### Scenario: Revalidated user loses a permission

- **WHEN** после refresh подтверждён прежний `user_id`, но право открытой формы или операции отозвано
- **THEN** запрещённое содержимое и элементы действия скрываются; сохранённое локальное состояние не меняет UI-политику, backend независимо авторизует запросы

### Requirement: Principal-owned registration drafts

В защищённом режиме локальный черновик регистрации навыка, включая состояние восстановления незавершённой операции, SHALL принадлежать подтверждённому `user_id` в текущем окружении. Приложение MUST NOT читать пользовательскую запись до подтверждения principal, использовать токены/техническое поколение как владельца или автоматически присваивать старую запись без владельца. Старые записи без владельца и записи других пользователей MUST NOT автоматически показываться, переноситься либо удаляться. Запись/автосохранение SHALL проверять актуальность контекста; позднее завершение прежней операции MUST NOT менять storage после инвалидирования её контекста. Mock mode SHALL использовать отдельное пространство по add-local-session-demo без чтения общей MPMM-сессии.

#### Scenario: Unowned legacy draft in real mode

- **WHEN** подтверждённый пользователь открывает регистрацию в real mode, а в storage есть только прежний черновик без владельца
- **THEN** этот черновик не открывается, не присваивается текущему пользователю и не удаляется; новая запись получает отдельное пространство владельца

#### Scenario: Account switch isolates durable recovery

- **WHEN** пользователь A имеет сохранённый черновик с незавершённой операцией, затем `/me` подтверждает пользователя B
- **THEN** B не получает данные или ключи операции A; поздний callback A не меняет записи после инвалидирования контекста, а запись A остаётся доступной только после повторного подтверждения A и применимых прав

#### Scenario: Same user restores a draft after refresh

- **WHEN** refresh меняет токены и поколение, но `/me` подтверждает прежний `user_id`
- **THEN** пространство черновика не меняется, параметры восстановления сохраняются и операция не повторяется автоматически

#### Scenario: Mock draft separation

- **WHEN** регистрация открыта в mock mode
- **THEN** используется mock namespace согласно add-local-session-demo без чтения MPMM token и присвоения real-mode записей

### Requirement: Credential destination boundary

Автоматические credentials SHALL отправляться только на настроенный HTTPS Control API с проверкой origin/path boundary, а refresh — только на точный настроенный HTTPS endpoint MPMM. Control API SHALL сохранять существующий resolver, VITE_CONTROL_API_BASE_URL и mobile a/c/t → nchat a/c/t mappings; на Т текущий адрес `https://nchat-t-tech.mos.ru/api/control/api`. MPMM defaults SHALL быть login `https://mobile-t-tech.mos.ru/sa-admin` и refresh `https://mobile-t-tech.mos.ru/gateway/admin/api/v1/auth/refresh`. Доверенная конфигурация окружения SHALL задавать destinations; hostname страницы MUST NOT служить переключателем auth. Валидный HTTPS VITE_CONTROL_API_BASE_URL из build-time конфигурации SHALL задавать доверенный API destination, даже если он отличается от Т; относительный base SHALL разрешаться относительно origin приложения. Конечный URL запроса вне настроенного origin/API path boundary либо недопустимая конфигурация SHALL отклоняться до отправки credentials. Query, storage и аргумент отдельного запроса MUST NOT расширять доверенный destination. Credential-bearing запросы MUST NOT следовать HTTP redirects, передавать токены в URL, логах, telemetry, query keys или произвольных attachment URLs. Доступ к файлам SHALL использовать согласованный backend content endpoint. Эти правила SHALL применяться независимо от наличия `*`.

#### Scenario: Configured API override

- **WHEN** real mode использует валидный HTTPS VITE_CONTROL_API_BASE_URL из build-time конфигурации, отличный от текущего адреса Т
- **THEN** подготовленный запрос к этому API получает актуальную пару auth-заголовков; hostname UI не отключает сессию

#### Scenario: Request outside configured destination or redirect

- **WHEN** отдельный запрос указывает URL вне настроенного API destination либо auth-запрос получает redirect
- **THEN** запрос к конечному чужому адресу с credentials не выполняется, отображается ошибка конфигурации/транспорта
