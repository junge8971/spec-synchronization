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

### Requirement: Server-side collection behavior

Фильтрация и сортировка SHALL выполняться до пагинации по контрактным query-параметрам. Списки SHALL возвращать `items` и согласованный `pagination` с limit, offset, current_page, total_items и total_pages. Сервер MUST NOT подменять offset за концом списка последней непустой страницей.

#### Scenario: Filtered paginated list

- **WHEN** запрошен отфильтрованный список с limit 10 и offset 10
- **THEN** возвращается соответствующий срез отсортированной выборки, а total_items учитывает фильтры до среза

#### Scenario: Offset beyond the result

- **WHEN** offset больше числа подходящих записей
- **THEN** items пуст, total_items остаётся достоверным, а сервер не возвращает записи другой страницы

### Requirement: Module registry query behavior

Mock API SHALL предоставлять список по `GET /assistant-modules/v1/modules` с query, status, sort и limit/offset согласно поставленной схеме. Локальная конвенция SHALL определять query как регистронезависимый поиск по code/name/description, status как точное строковое совпадение (неизвестное значение даёт пустую выборку), отсутствие sort как сортировку по name. Один и несколько повторённых query-параметров sort SHALL поддерживаться как упорядоченный список критериев. Фильтры и сортировки SHALL применяться до пагинации; семантика SHALL быть документирована как mock-конвенция, а не расширение backend-контракта.

#### Scenario: Multiple sort criteria

- **WHEN** переданы `sort=status&sort=-name` и limit/offset
- **THEN** список сортируется по status, затем по убыванию name внутри одинакового status, после чего возвращается запрошенный срез и согласованные totals

#### Scenario: Single sort and invalid input

- **WHEN** передан один `sort=-updated_at` либо недопустимый `sort=unknown`
- **THEN** первый запрос принимается как массив одного критерия, второй возвращает контрактный 422

#### Scenario: Empty results

- **WHEN** фильтр не имеет совпадений или offset выходит за конец выборки
- **THEN** items пуст; pagination описывает отфильтрованную выборку и не подменяет страницу непустой

### Requirement: Stateful module actions and derived views

Mock API SHALL предоставлять `GET /assistant-modules/v1/modules/summary`, `GET /assistant-modules/v1/modules/preview`, `POST /assistant-modules/v1/modules/{module_id}/enable` и `POST /assistant-modules/v1/modules/{module_id}/disable`. Все представления SHALL отражать одно состояние модулей; restart SHALL восстанавливать seed. Поле by SHALL обозначать фиксированного автора mock-изменения, не сессию посетителя.

Обе мутации SHALL требовать expected_version >= 1. По локальной конвенции несовпадение версии SHALL возвращать 409 без изменений. Отключение с disable_allowed=false SHALL возвращать 409; при непустом disable_impact_message отсутствие confirm_impact=true SHALL возвращать 409. Успешная мутация SHALL увеличивать version на 1, обновлять updated_at/by и задавать целевой status, включая повтор целевого состояния с актуальной версией. Disable SHALL сохранять user_message (default пустая строка), enable SHALL сбрасывать его в null. Эти правила ошибок и переходов SHALL документироваться только как mock-конвенции, без изменения OpenAPI.

#### Scenario: Disable and enable affect every view

- **WHEN** разрешённый модуль отключён с актуальной версией и необходимым подтверждением, затем включён с новой версией
- **THEN** ответы соответствуют ModuleResponse; список, summary и preview после каждого действия согласованы; отключённый модуль появляется и затем исчезает из disabled_modules и fallback-карточек

#### Scenario: Summary and preview states

- **WHEN** запрошены summary и preview
- **THEN** totals вычисляются по всей коллекции, независимо от фильтра списка; при наличии отключённых модулей состояние degraded и banner tone warning, иначе healthy и success; preview содержит по одной fallback-карточке на отключённый модуль и ни одной для включённых

#### Scenario: Preview fallback text

- **WHEN** отключённый модуль имеет непустой user_message либо пустой user_message
- **THEN** assistant_message содержит соответственно сохранённый текст либо документированный mock-текст по умолчанию

#### Scenario: Rejected actions preserve state

- **WHEN** версия устарела, отключение запрещено или требуется неподтверждённое предупреждение
- **THEN** ответ 409 использует документированный mock error envelope, а status, version, updated_at, by и все производные представления не меняются

#### Scenario: Invalid action and missing module

- **WHEN** отсутствует expected_version, передан 0, невалидный UUID или корректный UUID отсутствующего модуля
- **THEN** первые три случая возвращают контрактный 422, последний — mock 404, без изменения состояния

#### Scenario: Fresh server state

- **WHEN** после мутаций создаётся новый экземпляр mock server
- **THEN** он получает исходные версии и статусы seed, независимо от предыдущего экземпляра

### Requirement: Merged contract preserves accepted skill intents

Опубликованный объединённый OpenAPI SHALL сохранять все принятые бизнес-операции и схемы, включая PUT intents, обязательные SkillResponse.intents/status, status-фильтр, POST status, Assistant modules, Analytics и принятые API диалогов. Auth-обновление SHALL точечно заменить `/api/control/api/auth/v1/me`, его зависимые схемы и security metadata согласно предоставленному контракту ЦАМ `message (1).txt`; отсутствие путей диалогов в этой выгрузке MUST NOT удалять их из объединённого контракта. SkillPhraseRequest.weight SHALL сохранять minimum 0, UpdateSkillIntentRequest.id SHALL допускать nullable UUID вместо ограничения UUIDv7. Остальные бизнес-операции и определения SHALL сохранять семантику. Security SHALL описывать обязательную пару AdminToken/AccessToken в одном объекте требования, фиксируя исправление формального OR исходной выгрузки по явному требованию обоих raw-заголовков.

Документация SHALL различать происхождение бизнес- и auth-фрагментов и известные противоречия описаний аналитики. Самостоятельные разделы SHALL совпадать с объединённым контрактом и содержать замыкание зависимых схем. Generated-типы SHALL соответствовать контракту. Минимальный используемый контракт refresh MPMM SHALL храниться отдельно с result envelope; генерация и проверки MUST NOT зависеть от Downloads, untracked auth-openapi.json или соседнего checkout. Локальное бизнес-покрытие SHALL сохраняться без credentials; runtime mock `/me` и каталог fixtures SHALL задаваться отдельным add-local-session-demo; реальные токены и backend RBAC в mock server MUST NOT добавляться.

#### Scenario: Add modules without losing skill APIs

- **WHEN** потребитель использует контракт после auth-обновления
- **THEN** сохранены модули, status/Analytics, PUT intents и обязательные поля карточки; существующие бизнес-пути диалогов не исчезают

#### Scenario: Standalone contract consistency

- **WHEN** проверяется самостоятельный раздел
- **THEN** его операции и схемы совпадают с объединённым контрактом, все ссылки разрешаются и security отражает принятую пару заголовков

#### Scenario: Repository-only contract checks

- **WHEN** генерация и проверки выполняются без файлов Downloads и соседнего MPMM
- **THEN** используются только repo-контракты, рассинхронизация разделов/generated-типов обнаруживается

#### Scenario: Mock principal belongs to the dedicated change

- **WHEN** локальный mock server получает запрос `/api/control/api/auth/v1/me`
- **THEN** mock principal определяется add-local-session-demo; бизнес-операции по-прежнему тестируются без реальных credentials и серверной ролевой модели

### Requirement: Skill intents mock survives contract refresh

Mock API SHALL сохранять чтение intents в карточке навыка и замену набора через PUT intents с контрактной валидацией, обязательным Idempotency-Key и expected_version. Успешная запись SHALL увеличивать версию навыка и отражаться в последующем GET. Повтор с тем же ключом и телом SHALL возвращать прежний ответ без повторной мутации. Устаревшая версия SHALL давать mock conflict 409 без изменения данных; пустой набор SHALL очищать группы. Локально формируемые normalized/source/created_at SHALL документироваться как mock-данные, а не реальная нормализация, применение или дообучение.

#### Scenario: Save read retry and clear

- **WHEN** набор групп сохранён, прочитан через GET, повторно отправлен с тем же ключом и телом, затем очищен с актуальной версией и новым ключом
- **THEN** GET отражает сохранённые группы; повтор возвращает исходный результат и не увеличивает версию; очистка возвращает пустой набор и новую версию

#### Scenario: Invalid or stale intent write

- **WHEN** PUT intents содержит невалидную группу, не содержит обязательного Idempotency-Key либо отправлен с устаревшей версией и новым ключом
- **THEN** первые два случая возвращают контрактный 422, последний — mock 409, а сохранённые группы и версия не меняются

### Requirement: Updated phrase constraints in mock requests

Mock PUT intents SHALL применять опубликованные minimum weight=0 и UUID группы, сохраняя ID навыка UUIDv7, обязательные expected_version/Idempotency-Key, coherent GET, пустую очистку и replay. Отклонение input SHALL оставлять данные и версию неизменными.

#### Scenario: Zero negative and omitted weight

- **WHEN** отправлены weight=0, weight<0 или запрос без weight
- **THEN** ноль сохраняется, отрицательный даёт 422 без изменений, пропущенный использует 1; успешные ответы проходят контрактную схему

#### Scenario: UUID variants

- **WHEN** передан UUIDv4 группы или malformed UUID
- **THEN** первый сохраняется и читается без замены ID, второй даёт 422 без изменений; некорректный skill_id также отклоняется

### Requirement: Single skill status mock round-trip

Mock SHALL обеспечивать проверяемые POST status и последующие detail/list для переходов draft→checking, sandbox→review и whitelist→prod. Он SHALL сохранять существующую конвенцию приёма любого опубликованного target enum, а не объявлять UI-матрицу production-правилом. Успех SHALL увеличивать version и обновлять updated_at без изменения intents. Replay того же method/path/key/body SHALL возвращать исходный ответ без повторной мутации; иной body с тем же ключом и конфликт expected_version SHALL давать документированный mock 409 без изменения данных. Автоматическое завершение обучения, тестов и ревью MUST NOT моделироваться таймером.

#### Scenario: UI transitions and coherent reads

- **WHEN** каждая из трёх одиночных команд отправлена с актуальной версией и новым ключом
- **THEN** POST, detail и list показывают согласованный target status/version, intents не меняются, ответы соответствуют схеме

#### Scenario: Replay conflicts and invalid target

- **WHEN** повторены прежний запрос, изменённое тело с прежним ключом, новая команда со старой версией или неизвестным enum
- **THEN** соответственно возвращаются исходный результат без новой мутации, 409, 409 и 422; ошибки не меняют данные

#### Scenario: Intermediate state fixtures

- **WHEN** запрашивается seed-навык в checking/training/autotest/review либо mock явно установлен в такое состояние
- **THEN** он остаётся в этом состоянии до явной мутации, а UI не получает вымышленные результаты процесса

### Requirement: Local response scenario selection

Только sessionDemo mock server SHALL предоставлять каталог операций и фиксированных сценариев для простой локальной панели «Моки». Выбор SHALL передаваться несекретным header конкретного запроса, без глобального server state. Неизвестный сценарий SHALL возвращать 400. Сценарии SHALL применяться после проверки контрактного ввода и до handler/idempotency: фиксированные HTTP 403/500 не меняют данные; задержка 1500 мс сохраняет штатные бизнес-проверки и не выполняет handler после отмены запроса. Штатный сценарий SHALL сохранять прежнее покрытие и существующие unavailable ответы. Сценарий 403 SHALL быть фиксированным ответом для проверки обработки backend-отказа; он MUST NOT вычисляться из roles/permissions. Mock server MUST NOT добавлять ролевую авторизацию бизнес-операций. Каталоги SHALL оставаться доступны независимо от сценария `/me`. Вне sessionDemo каталог SHALL возвращать 404, scenario headers MUST NOT менять бизнес-поведение.

#### Scenario: Invalid mutation under a scenario

- **WHEN** запрос содержит невалидное тело или не содержит обязательного Idempotency-Key и выбран сценарий
- **THEN** сохраняется контрактный validation response, операция не выполняется

#### Scenario: Scenario does not mutate server data

- **WHEN** корректная мутация получает выбранный HTTP 403 либо 500
- **THEN** handler не вызывается, последующее штатное чтение видит прежнее состояние

### Requirement: Equivalent PUT aliases for existing mutations

Mock API SHALL обслуживать PUT и существующий PATCH для изменения домена, навыка, команды и участника команды по опубликованным адресам. Оба метода SHALL сохранять прежние схемы запроса/ответа, бизнес-валидацию и согласованное состояние. PUT домена и навыка SHALL сохранять идемпотентность в пределах method/path/key и проверки версии. Моки MUST NOT требовать credentials или выполнять ролевую авторизацию бизнес-запросов.

#### Scenario: PUT updates existing resource

- **WHEN** валидный PUT изменяет домен, навык, команду или участника
- **THEN** ответ проходит схему соответствующей операции, последующее чтение отражает изменение, PATCH того же ресурса остаётся доступным

#### Scenario: PUT retry and conflicting reuse

- **WHEN** PUT домена или навыка повторяется с тем же method/path/key и телом, затем с другим телом при том же ключе
- **THEN** первый повтор возвращает прежний результат без второй мутации, изменённое тело получает 409 без изменения данных

#### Scenario: Invalid PUT cannot modify state

- **WHEN** PUT содержит невалидное тело, не содержит обязательного ключа или использует устаревшую версию
- **THEN** возвращается соответствующая ошибка валидации либо конфликта; состояние остаётся прежним

### Requirement: Explicit unavailable coverage for imported managed resources

Для 43 новых managed-resource операций этой выгрузки, пока не реализованных отдельными changes, локальный mock API SHALL явно возвращать HTTP 501 с сообщением о недоступности реализации после штатной валидации запроса. Ответ SHALL документироваться как mock convention и MUST NOT добавляться в backend OpenAPI как подтверждённый ответ сервера. Такие операции MUST NOT возвращать успешные вымышленные CRUD-данные. Исключение SHALL ограничиваться явным перечнем method/path этой поставки; отсутствие handler любой другой операции MUST оставаться ошибкой полноты покрытия. Уже принятые handlers и особое поведение `/me` SHALL сохраняться.

#### Scenario: Imported CRUD operation is not implemented

- **WHEN** валидный запрос вызывает одну из явно перечисленных новых CRUD-операций со штатным demo-сценарием
- **THEN** локальный сервер отвечает 501 без изменения состояния; сервер запускается, существующие API продолжают работать

#### Scenario: Invalid imported CRUD request

- **WHEN** запрос новой CRUD-операции нарушает опубликованную схему
- **THEN** запрос отклоняется штатной контрактной валидацией, а не превращается в успешный fixture

#### Scenario: Lost handler is not hidden

- **WHEN** у прежней поддержанной операции или новой операции вне явного перечня отсутствует handler
- **THEN** проверка покрытия или запуск mock API завершается ошибкой; общий fallback не скрывает пропуск

#### Scenario: New contract keeps local demo and production isolation

- **WHEN** загружается каталог demo-сценариев либо собирается production-приложение
- **THEN** PUT и явно недоступные операции корректно представлены в локальном каталоге, прежние 403/500/delay сценарии сохраняются, production не содержит mock handlers или fixtures
