# local-session-demo Specification

## Purpose

Предоставить воспроизводимую локальную демонстрацию пользователя, ролей и ограничений интерфейса без настоящей авторизации, доступа к MPMM или включения тестовых профилей в production.

## Requirements

### Requirement: Configuration selects demo or real session

Приложение SHALL включать demo вместе с бизнес-моками через существующий mocksEnabled при yarn dev, без отдельной команды или demo env-флага. CONTROL_API_MOCKS=false SHALL отключать все моки и выбирать настроенные реальные API/auth. Приложение из production-сборки SHALL использовать реальный API и сессию; build/start/preview MUST NOT включать demo даже с CONTROL_API_MOCKS=true. Build SHALL создавать артефакты без auth/business-запросов и чтения пользовательской сессии; start/preview SHALL обслуживать собранные артефакты без изменения режима. Отсутствие обязательной real API/auth конфигурации SHALL давать явную ошибку, не неподтверждённый полный доступ. Hostname MUST NOT определять режим авторизации: Т является текущим backend deployment. Mock listener SHALL оставаться локальным на loopback. Внешний API override при включённых mocks SHALL давать ошибку конфигурации. URL/storage MUST NOT включать demo вне разрешённого dev запуска.

#### Scenario: Ordinary development and explicit opt-out

- **WHEN** приложение запускают через yarn dev либо CONTROL_API_MOCKS=false yarn dev
- **THEN** первый запуск подтверждает mock principal, второй использует настроенный real API/auth без mock requests

#### Scenario: Invalid backend combination

- **WHEN** mocks включены вместе с внешним API override либо real mode не имеет обязательной конфигурации
- **THEN** запуск или bootstrap показывает явную ошибку конфигурации, без fallback в полный доступ

#### Scenario: Production mode does not depend on hostname

- **WHEN** production build/start/preview открыт на любом hostname, включая локальный, и CONTROL_API_MOCKS=true
- **THEN** приложение использует настроенные real API/auth, тестовые профили и mock controls недоступны

### Requirement: Credential-free demo principal protocol

В demo `/api/control/api/auth/v1/me` SHALL возвращать актуальный ЦАМ principal в стандартном data envelope, выбранный несекретным ID профиля. Dev-only `/api/control/api/__demo/session/profiles` SHALL возвращать каталог фиксированных ID/подписей. Эти запросы SHALL идти только на local same-origin proxy, без token storage, JWT, X-Access-Token, X-Admin-Token, Authorization, MPMM refresh или login redirect. Redirect ответа MUST NOT приводить к внешнему запросу. Неизвестный ID SHALL возвращать 400; отсутствие ID SHALL выбирать viewer. Каталог и выбор профиля MUST NOT расширять production OpenAPI.

#### Scenario: Local bootstrap

- **WHEN** demo открыто с профилем viewer
- **THEN** `/me` соответствует схеме пользователя/roles/permissions/assignments, бизнес-UI ждёт подтверждения, обращения к MPMM и чтение общего token отсутствуют

#### Scenario: Invalid profile and failed principal

- **WHEN** сохранён неизвестный ID либо `/me` отвечает 401/403/5xx, невалидным телом или сетевой ошибкой
- **THEN** бизнес-UI заблокирован, доступны явный retry и выбор известного профиля, нет fallback в неподтверждённый полный доступ или redirect на MPMM

#### Scenario: Independent visitors

- **WHEN** две вкладки запрашивают `/me` с разными профилями
- **THEN** каждая получает своего principal независимо от запросов другой вкладки, без глобального server-selected пользователя

### Requirement: Fixed demonstrative roles and permissions

Demo SHALL иметь четыре профиля с разными устойчивыми user_id, синтетическими ФИО/email и явно демонстрационными roles; assignments SHALL быть пустым массивом. Профиль none SHALL иметь пустые permissions; viewer SHALL иметь только view для Domain, Skill, Surface, Team, Module, Analytics; editor SHALL дополнительно иметь create/update для Domain, Skill, Surface; full SHALL иметь только явный `*`. Default SHALL быть viewer. Выбор SHALL сохранять только ID в отдельном sessionStorage namespace вкладки и заново подтверждаться `/me` после reload. Смена профиля SHALL сохранять ID и выполнять полный reload страницы. При ошибке записи storage SHALL отображаться ошибка без переключения текущего профиля.

Названия ролей MUST NOT давать прав, `TSAM.*` MUST NOT заменять `*`, assignments/scopes MUST NOT объединяться в разрешения. Профили MUST NOT объявляться production-ролями. Редактор ролей, произвольных permissions или команд MUST NOT добавляться.

#### Scenario: Viewer and editor

- **WHEN** выбран viewer либо editor
- **THEN** viewer получает read-only UI, editor дополнительно получает согласованные create/update; у обоих нет wildcard-only разделов и status/lifecycle полномочий без явных grants

#### Scenario: Full demo does not implement missing APIs

- **WHEN** выбран full
- **THEN** wildcard-only UI доступен, но неподдержанные API/заглушки и серверные ошибки не превращаются в успешные бизнес-операции

#### Scenario: Reload and storage failure

- **WHEN** выбран editor и страницу перезагружают с доступным storage либо storage недоступен
- **THEN** в первом случае заново подтверждается editor, во втором показана ошибка сохранения и текущий профиль не меняется

### Requirement: Shared presentation policy without mock backend authorization

Demo SHALL применять общую permissions-policy только к представлению меню, вкладок, страниц и кнопок. Прямой URL SHALL показывать состояние недоступного UI, если страница не разрешена; её бизнес-содержимое не монтируется. При none SHALL оставаться доступны статическая справка и выбор профиля. Transport, mutation handlers и mock business API MUST NOT вычислять авторизацию из роли или permissions. Business mocks SHALL оставаться credential-free и сохранять бизнес-валидацию. Серверный 403 SHALL обрабатываться как отказ backend без автоматического replay; demo MUST NOT считаться проверкой object scopes, CORS или refresh rotation.

#### Scenario: Presentation follows the selected principal

- **WHEN** выбран viewer либо none и открыт прямой URL недоступного раздела
- **THEN** интерфейс показывает недоступность раздела, его бизнес-содержимое не монтируется, справка и mock controls доступны

#### Scenario: Backend refusal remains authoritative

- **WHEN** показанная пользователю операция получает выбранный mock HTTP 403
- **THEN** UI отображает отказ backend, не повторяет мутацию автоматически и не меняет permissions; отказ не вычисляется из demo-роли

### Requirement: Simple mock response scenarios

Local demo SHALL предоставлять простую панель «Моки» без отдельного Devtools framework. Каталог HTTP-операций и сценариев SHALL приходить от mock server. Выбор SHALL относиться к паре method/path template независимо от query и храниться отдельно для каждой вкладки браузера. SHALL поддерживаться штатный ответ, фиксированные HTTP 403/500 без выполнения операции и задержка 1500 мс перед штатным ответом, включая `/me` и binary. Произвольный JSON-редактор MUST NOT добавляться. Панель SHALL предоставлять сброс сценария и всех сценариев без изменения business seed, автоматического refetch или replay мутации. Недоступный каталог SHALL давать error/retry без выдуманных операций. Управление SHALL оставаться доступным при ошибке principal и отказе маршрута. Панель, сценарии и их каталог MUST NOT включаться вне local demo или попадать в production artifacts.

#### Scenario: Select an operation response

- **WHEN** для одной операции выбран HTTP 500, а для другой задержка
- **THEN** первая возвращает ошибку без мутации seed, вторая сохраняет штатный результат и валидацию после задержки; остальные операции не меняются

#### Scenario: Reset and independent tabs

- **WHEN** пользователь сбрасывает сценарии в одной вкладке
- **THEN** следующие её запросы используют штатные handlers, другая вкладка сохраняет собственный выбор; подтверждённые бизнес-данные не сбрасываются

#### Scenario: Recover a failed principal

- **WHEN** `/me` отвечает выбранной ошибкой
- **THEN** пользователь может открыть «Моки», вернуть штатный сценарий и явно повторить подтверждение без MPMM redirect или доступа к старому business UI

### Requirement: Profile reload and draft ownership

Переключение профиля SHALL сохранять выбранный ID и полностью перезагружать документ, заново подтверждая `/me`. UI SHALL предупреждать о reload и потере несохранённого ввода; после начала перехода повторный выбор SHALL блокироваться. Старые React state/cache/callbacks MUST NOT переноситься в новый документ. Живое переключение профиля и demo generation state machine MUST NOT добавляться. Уже отправленная операция может завершиться на сервере; reload MUST NOT объявляться её отменой и MUST NOT сбрасывать business seed или повторять мутации.

Demo-черновики SHALL храниться отдельно по режиму, окружению и подтверждённому user_id. Legacy/MPMM и чужие записи MUST NOT читаться, присваиваться или удаляться. До подтверждения principal пользовательские записи MUST NOT читаться. Storage error при сохранении профиля SHALL оставлять текущий профиль и показывать ошибку; memory-only выбор профиля с последующим reload MUST NOT выдаваться за успешный.

#### Scenario: Profile change reloads the document

- **WHEN** выбран другой профиль и ID сохранён
- **THEN** страница перезагружается, новый `/me` определяет пользователя и UI; старое состояние редактора не переносится

#### Scenario: Draft ownership across reloads

- **WHEN** A сохранил demo-черновик, затем выбраны B и снова A с reload на каждом переходе
- **THEN** B не видит запись A, вернувшийся A восстанавливает собственный сохранённый черновик; записи других режимов нетронуты

#### Scenario: Profile storage failure

- **WHEN** sessionStorage отклоняет запись выбранного ID
- **THEN** показана ошибка, текущий профиль остаётся активным и reload ради неподтверждённого выбора не выполняется

#### Scenario: Uncertain mutation result

- **WHEN** во время reload ранее отправленная мутация имеет неопределённый результат
- **THEN** клиент не выполняет автоматический replay и не заявляет, что серверная операция отменена
