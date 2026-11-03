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

Объединённый OpenAPI SHALL следовать текущему live-снимку с сохранением всех опубликованных бизнес-операций, включая PUT intents, обязательные SkillResponse.intents/status, status-фильтр, POST status, Assistant modules, Analytics и API диалогов. Исторический auth-фрагмент message (1).txt и локальное дополнение экспорта SHALL NOT замещать актуальные опубликованные определения. SkillPhraseRequest.weight SHALL сохранять minimum 0, UpdateSkillIntentRequest.id SHALL допускать nullable UUID вместо ограничения UUIDv7, пока это соответствует live API. Security SHALL описывать обязательную пару AdminToken/AccessToken в одном объекте требования, фиксируя исправление формального OR исходной выгрузки по явному требованию обоих raw-заголовков.

Документация SHALL различать происхождение снимка, сохранённые нормализации и противоречия дополнительных источников. Самостоятельные разделы SHALL совпадать с объединённым контрактом и содержать замыкание зависимых схем. Generated-типы SHALL соответствовать контракту. Минимальный используемый контракт refresh MPMM SHALL храниться отдельно с result envelope; генерация и проверки MUST NOT зависеть от Downloads, untracked auth-openapi.json или соседнего checkout. Локальное бизнес-покрытие SHALL сохраняться без credentials; runtime mock /me и каталог fixtures SHALL сохранять local-session-demo; реальные токены и backend RBAC в mock server MUST NOT добавляться.

#### Scenario: Add modules without losing skill APIs

- **WHEN** потребитель использует контракт после обновления снимка
- **THEN** сохранены модули, status/Analytics, PUT intents и обязательные поля карточки; опубликованные бизнес-пути диалогов не исчезают

#### Scenario: Standalone contract consistency

- **WHEN** проверяется самостоятельный раздел
- **THEN** его операции и схемы совпадают с объединённым контрактом, все ссылки разрешаются и security отражает принятую пару заголовков

#### Scenario: Repository-only contract checks

- **WHEN** генерация и проверки выполняются без файлов Downloads и соседнего MPMM
- **THEN** используются только repo-контракты, рассинхронизация разделов/generated-типов обнаруживается

#### Scenario: Mock principal belongs to the dedicated change

- **WHEN** локальный mock server получает запрос /api/control/api/auth/v1/me
- **THEN** mock principal определяется local-session-demo; бизнес-операции по-прежнему тестируются без реальных credentials и серверной ролевой модели

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

### Requirement: Knowledge base mock contract fidelity

Существующий Express mock SHALL предоставлять согласованные HTTP-сценарии KB: metadata с data.entries и bindings, шесть KB lookup-наборов только для соответствующего section, CRUD/search/export и managed saved-filters с resource=knowledge-base-entries. KB fixtures SHALL быть обособлены и согласованы с существующими навыками/пользователями. Сервер SHALL сохранять link IDs, порядок массива, replacement links/skill_ids, rules defaults и очистку nullable полей по CRUD-контракту. Search/sort SHALL предшествовать pagination; display names и links_count SHALL соответствовать данным. Валидация URL, references, inactive values и field errors SHALL позволять проверить ошибки UI без credentials и ролевого enforcement.

Metadata SHALL публиковать type и допустимые операторы каждого поля, включая numeric links_count и string skill_names. Поиск, CSV и сохранённый search SHALL поддерживать их по текущему контракту. Mock MUST NOT добавлять archived-переход или вложенный экспорт, отсутствующие в принятом API. DELETE SHALL скрывать запись из поиска и чтения, сохраняя занятость кода по контракту. Runtime fixtures MUST NOT попадать в production. Проверки SHALL отличать локальное подтверждение поведения от реальной backend-интеграции.

#### Scenario: Metadata and lookup ready for editor

- **WHEN** запрошены KB metadata и lookup
- **THEN** data.entries содержит bindings/condition_fields с типами и операторами/export_fields/export_max_rows, lookup содержит KB-наборы с display_name и is_active, не выдавая справочники других разделов

#### Scenario: Aggregate HTTP round trip

- **WHEN** материал создан, ссылки переставлены с прежними ID и список навыков очищен
- **THEN** последующие detail/search отражают новый порядок и пустые связи, DTO и totals проходят контрактную проверку

#### Scenario: Invalid mutation preserves data

- **WHEN** отправлен небезопасный URL, несуществующий skill_id или новый выбор inactive-кода
- **THEN** возвращается контрактная ошибка соответствующего поля без изменения сохранённого материала

#### Scenario: Unsupported operation is not simulated

- **WHEN** отправлен payload неподдержанного архива или вложенного экспорта
- **THEN** mock не возвращает фиктивный успешный результат

#### Scenario: Deleted code remains reserved

- **WHEN** материал удалён и затем создаётся другой с тем же code
- **THEN** чтение удалённого ID возвращает 404, создание получает конфликт кода

#### Scenario: Mock regression safety

- **WHEN** обновлены общие managed helpers ради KB
- **THEN** прежние тесты других ресурсов сохраняются, новые KB server-тесты входят в yarn test, production не содержит их fixtures

#### Scenario: Numeric and skill-name search

- **WHEN** links_count between [0, 2.5] объединён с skill_names contains в OR-группе
- **THEN** поиск/total/CSV применяют одну семантику до пагинации; skill_names содержит только названия связанных неудалённых навыков, сохранённый search сохраняет числа

### Requirement: A/B testing mock contract fidelity

Существующий Express mock SHALL предоставлять metadata с data.experiments и bindings, четыре section-scoped ab_* lookup-набора, CRUD/search/export и managed saved-filters с resource=ab-experiments. Изолированные fixtures SHALL ссылаться на существующие поверхности и бизнес-пользователей. Создание/PUT SHALL проверять name/code uniqueness, группы 2–100, целые проценты 0–100 и сумму 100, непустые уникальные теги, уникальные IDs, поверхности 1–100 и их существование, даты, scheduled/segment требования, inactive references и nullability. PUT SHALL сохранять пропущенные поля, заменять переданные коллекции целиком и сохранять IDs/порядок групп. Изменение тега существующей группы при сохранённом non-draft статусе SHALL давать документированный конфликт без мутации.

Search/sort SHALL предшествовать pagination и соответствовать документированным полям и семантике; summaries SHALL содержать названия поверхностей и групп. Metadata SHALL включать типы и операторы каждого поля, в том числе numeric groups_count. Поиск, сохранённые фильтры и CSV SHALL поддерживать числовые условия groups_count. CSV SHALL соответствовать общему контракту и A/B полям, именам файлов и пределу 10000. DELETE SHALL выполнять документированное мягкое удаление, без UI-кнопки удаления. Saved search SHALL проверяться до сохранения/применения. Ошибки SHALL сохранять прежнее состояние и использовать соответствующие HTTP/schema/field paths. Бизнес-запросы SHALL работать без credentials и role enforcement. Restart SHALL восстанавливать seed.

Mock MUST NOT поддерживать archived, priority/surface-условия внутри conditions, вложенный экспорт, исполнение расписания, распределение трафика, сбор метрик или автостоп вопреки контракту. Runtime fixtures MUST NOT попадать в production; проверки SHALL отличать локальное поведение от реального backend.

#### Scenario: Metadata and lookup

- **WHEN** запрошены metadata и lookup ab-testing
- **THEN** возвращены data.experiments с bindings/typed conditions/export fields/limit и только четыре A/B-набора с display_name/is_active; KB lookup остаётся независимым

#### Scenario: Aggregate round trip

- **WHEN** эксперимент создан, группы переставлены с прежними IDs и набор поверхностей заменён
- **THEN** detail/search/CSV отражают один агрегат, порядок и корректные summaries; ответы проходят контрактную схему

#### Scenario: Rejected aggregate preserves state

- **WHEN** PUT имеет сумму 99, дублирующийся тег, отсутствующую поверхность, невалидные даты или изменение тега сохранённой non-draft группы
- **THEN** возвращается соответствующая ошибка без изменения карточки, timestamps и результатов поиска

#### Scenario: Full selection export

- **WHEN** search имеет limit/offset и числовое условие groups_count, а CSV экспортируется с тем же отбором
- **THEN** поиск возвращает страницу, CSV весь отбор до документированного лимита, без вложенных таблиц и фиктивных результатов

#### Scenario: Isolation and regression

- **WHEN** обновлены A/B handlers и запускается yarn test
- **THEN** вложенные A/B HTTP-тесты выполняются, существующие KB/managed tests сохранены, разделы не импортируют предметные mocks друг друга и production не содержит fixtures

### Requirement: Current managed-resource operation coverage

Mock SHALL обслуживать все текущие managed-resource операции, включая восемь операций API registry и восемь response templates, без общего 501 или отсутствующих handlers. Для новых ресурсов SHALL предоставляться CRUD, metadata с ключами endpoints и response-templates, search и CSV списка/карточки. Девять новых системных справочников SHALL читаться через section-scoped lookups и центральный реестр значений/экспорт; изменение их значений SHALL запрещаться. Сохранённые фильтры SHALL принимать api-endpoints и response-templates по live enum, проверяя и сохраняя полный search соответствующего ресурса. Несовпадение Markdown SHALL документироваться без заявления о проверенном deployment. Общие envelope, ошибки полей, пагинация, частичный PUT, мягкое удаление, inactive references и CSV ограничения SHALL сохраняться по актуальным источникам.

API endpoint SHALL проверять обязательность source_code для incoming/outgoing, валидность JSON-текста с сохранением форматирования, уникальность имени/кода/(method,path,version), параметры и ответы. PUT коллекций SHALL заменять их атомарно, сохранять переданные ID и порядок, генерировать ID новых строк. Описанные запросы MUST NOT исполняться.

Response template SHALL проверять обязательные type_code/scope_code/text, непустое имя/текст, уникальность имени/кода, существование и уникальность skill_ids/surface_ids. PUT SHALL заменять только переданные наборы связей; scope_code MUST NOT искусственно ограничивать связи. Активность SHALL определяться status, плейсхолдеры SHALL храниться без подстановки. Недокументированные проверки внешнего ответственного MUST NOT выводиться из поведения поверхностей.

#### Scenario: New API aggregate round trip

- **WHEN** эндпоинт создан, его параметры переставлены с прежними ID, responses очищены, затем выполнены GET/search/export
- **THEN** ответы согласованы, сохранены JSON-текст и порядок, очищена только переданная коллекция; запрос к описанному base_url не выполняется

#### Scenario: New resource validation is atomic

- **WHEN** отправлен incoming без source_code, повтор method/path/version либо шаблон с отсутствующим skill_id
- **THEN** возвращается ошибка без изменения карточки и вложенных коллекций

#### Scenario: Saved filters accept current enum

- **WHEN** сохранён и применён фильтр api-endpoints или response-templates
- **THEN** resource и полный search проходят соответствующую схему, чтение/PUT/delete работают по общему контракту; ошибочный search не сохраняется

#### Scenario: Section lookups and system values

- **WHEN** запрошены lookups/api и lookups/response-templates и предпринята запись системного значения
- **THEN** возвращаются соответственно шесть api_* и три tpl_* набора, запись отклоняется, чужие справочники не смешиваются

#### Scenario: Missing handler remains an error

- **WHEN** операция снимка не имеет handler или осталась привязана к старому operationId экспорта
- **THEN** запуск/проверка покрытия завершается ошибкой, общий fallback не скрывает пропуск

### Requirement: Numeric conditions preserve typed semantics

Mock SHALL валидировать field/operator/value совместно по metadata, не разрешая все операторы на всех полях только из-за общего enum. Numeric eq/ne/gt/gte/lt/lte/between SHALL сравнивать конечные числа без строкового преобразования и исключать NULL. between SHALL включать обе границы; пустая группа SHALL не ограничивать отбор при любой логике. Ошибки search, export и saved-filter search SHALL иметь соответствующий вложенный путь и не менять данные.

#### Scenario: Numeric edge cases

- **WHEN** переданы ноль, дробный порог, равные границы, обратный диапазон, boolean или строка вместо числа
- **THEN** первые три значения принимаются, остальные отклоняются; numeric ne не включает записи с NULL

#### Scenario: Metadata cannot enable invalid combinations

- **WHEN** gt применён к name либо contains к groups_count
- **THEN** mock отклоняет сочетание, а metadata не предлагает такой оператор

### Requirement: Surface mock follows current responsible and creation contracts

Mock SHALL хранить назначения по ID бизнес-пользователей и выдавать responsible как объекты id/full_name/email. При отсутствии сведений о ранее назначенном пользователе SHALL сохраняться ID с nullable сведениями, а не вымышленное имя. До создания SHALL проверяться занятость всех доменов, существование обоих пользователей и переданная конфигурация. Любая ошибка SHALL оставлять коллекцию поверхностей и связи команд неизменными; параллельные попытки занять один домен MUST NOT обе завершаться созданием. configuration absent/null SHALL использовать прежние defaults. Переданная конфигурация SHALL сохраняться без второго запроса.

Локальные embed_code/authorization SHALL быть согласованными демонстрационными серверными значениями без реальных credentials; клиент MUST NOT генерировать их или исполнять embed script. Неописанные wire-форматы ошибок SHALL явно маркироваться mock convention до подтверждения backend-примером, без изменения published OpenAPI.

#### Scenario: Domain or user conflict preserves state

- **WHEN** хотя бы один домен занят либо один ответственный отсутствует
- **THEN** создание отклоняется с диагностикой домена или назначения, поверхность и связь команды не появляются

#### Scenario: Atomic configuration

- **WHEN** передана валидная конфигурация либо невалидная конфигурация
- **THEN** первая читается после создания, вторая не оставляет поверхности; absent/null сохраняют defaults

#### Scenario: Existing missing user

- **WHEN** ранее назначенный пользователь отсутствует в текущем локальном справочнике
- **THEN** чтение сохраняет его ID с full_name=null/email=null, новое назначение этого ID отклоняется

#### Scenario: Concurrent domain creation

- **WHEN** две попытки создания используют один занятый ими домен
- **THEN** создаётся не более одной поверхности, другая попытка получает подтверждённый конфликт

### Requirement: System-state managed resource mock fidelity

Существующий Express mock SHALL обслуживать опубликованные system-state metadata, summary, search, create, detail, PUT, delete, list/detail CSV и section-scoped lookups, заменяя адресные unavailable handlers. Он SHALL возвращать согласованные DTO, серверные счётчики обоих видов по неудалённым записям, metadata, фильтрацию и сортировку до пагинации. Create SHALL выдавать custom/enabled/noncritical запись; предопределённым записям SHALL разрешаться только изменение состояния, пользовательские SHALL поддерживать согласованную редакцию и мягкое удаление. Код SHALL проверяться глобально между видами. Валидные изменения SHALL отражаться в последующих detail/search/summary/export; ошибки MUST NOT менять состояние.

Saved-filters SHALL принимать `resource=system-state-toggles` и валидировать полный сохранённый search. Повторное сохранение одного имени для фиксированного локального mock-владельца SHALL обновлять отбор с прежним ID, не меняя поведение фильтров других ресурсов. Моки SHALL оставаться credential-free без вычисления permissions, ролевого enforcement или реальной изоляции пользователей; фиксированный mock-владелец не является подтверждённым principal. Фикстуры и handlers MUST NOT входить в production, а другие непокрытые операции SHALL сохранять честный unavailable.

#### Scenario: Toggle and search round trip

- **WHEN** разрешённая предопределённая запись переключается через валидный PUT, затем читаются detail, search, summary и CSV
- **THEN** все ответы согласованы по состоянию и счётчикам, проходят контракт и не требуют credentials

#### Scenario: Invalid edit is atomic

- **WHEN** изменяются реквизиты предопределённой записи, удаляется такая запись или создаётся конфликтующий код
- **THEN** mock возвращает обозначенную ошибку без изменения исходных данных или сводки

#### Scenario: Saved-filter name is reused

- **WHEN** для фиксированного mock-владельца дважды сохранён system-state отбор с одинаковым именем и разными валидными параметрами
- **THEN** второй ответ относится к тому же ID, повторное чтение возвращает новый search, и это не означает реализованной backend-авторизации

#### Scenario: Restart and unrelated operations

- **WHEN** после изменений создаётся новый экземпляр mock server или вызывается другая неподключённая операция
- **THEN** system-state возвращается к своему seed, не связанная операция сохраняет свой прежний unavailable, а production не получает mock-файлы

### Requirement: Surface CSV export mock fidelity

Существующий локальный Express mock SHALL обслуживать опубликованные POST экспорта списка и карточки поверхностей вместо адресных `501 NOT_IMPLEMENTED`. Оба обработчика SHALL использовать текущие сохранённые mock-поверхности, одинаковый каталог полей и серверный порядок колонок. Экспорт списка SHALL применять `query`, `status`, `type`, `sort` до пагинации и возвращать весь отбор; mock-реестр и экспорт SHALL использовать согласованную семантику отбора. Экспорт карточки SHALL возвращать заголовок и одну строку по ID либо ошибку отсутствующей карточки. Пустой список SHALL давать CSV только с заголовками.

Мок SHALL возвращать UTF-8 BOM, разделитель `;`, безопасное CSV-экранирование и защиту формульных значений, файловый `Content-Type`, `Content-Disposition` с именем, длину и заголовки, ожидаемые клиентом. `fields` absent SHALL выбирать весь каталог; пустой массив и неизвестные поля SHALL давать ошибку валидации. При превышении локального лимита SHALL возвращаться 413 `EXPORT_TOO_LARGE` без частичного CSV; конкретный локальный лимит SHALL документироваться как mock-конвенция, не как доказанный лимит backend.

Операции SHALL оставаться credential-free, не вычислять permissions и не моделировать серверный доступ по командам. Существующие fixed-response сценарии, остальные обработчики и production-изоляция SHALL сохраняться. Результаты мока MUST NOT представляться подтверждением поведения развёрнутого backend или CORS.

#### Scenario: Filtered full export without credentials

- **WHEN** локальный запрос списка с отбором и сортировкой возвращает одну страницу, а экспорт получает те же условия без credentials
- **THEN** CSV содержит весь соответствующий mock-отбор до пагинации в согласованном порядке; отсутствие credentials не меняет ответ

#### Scenario: Shared fields and an empty registry

- **WHEN** список пуст или карточка выгружается с тем же набором выбранных полей, что список
- **THEN** пустой CSV содержит заголовки выбранных колонок, а оба метода используют одинаковый каталог и порядок полей

#### Scenario: Invalid fields and limit

- **WHEN** `fields` пуст или содержит неизвестный код либо локальный отбор превышает документированный mock-лимит
- **THEN** первые запросы отклоняются валидацией, превышение даёт 413 без файла, а mock-данные не меняются

#### Scenario: CSV quoting and formula safety

- **WHEN** сохранённое mock-значение содержит разделитель, перенос, кавычки или строку, которую таблица могла бы воспринять как формулу
- **THEN** серверный CSV корректно экранирует значение и защищает от формулы; опубликованные заголовки позволяют клиенту проверить файл

#### Scenario: Card is missing or a fixed failure is selected

- **WHEN** ID карточки отсутствует либо для операции выбран фиксированный отказ demo
- **THEN** пользователь получает соответствующий JSON-отказ без CSV или мутации данных; права не вычисляются из demo-профиля
