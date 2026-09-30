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

Mock API SHALL реализовать 33 бизнес-операции объединённого OpenAPI: Domains/Skills — 9, включая PUT intents, Surfaces — 11, Teams — 8, Assistant modules — 5. Ответы SHALL соответствовать описанным status codes, envelope, схемам, nullable/required полям, enum и форматам. Access-операция `GET /api/control/api/auth/v1/me` SHALL быть явно исключена из текущего покрытия и MUST NOT обслуживаться mock server. Отсутствие Bearer MUST NOT препятствовать чтению или мутациям бизнес-данных. Это SHALL документироваться как ограничение локального mock server, а не изменение требований безопасности backend. Непредоставленные шесть разделов MUST NOT выдаваться за реализованный контракт.

#### Scenario: Contract coverage check

- **WHEN** контрактные тесты перечисляют 34 операции объединённого OpenAPI
- **THEN** для каждой из 33 бизнес-операций имеется исполняемый сценарий без Authorization с проверкой ответа по схеме; единственное явное исключение — указанная Access-операция, а пропуск любой бизнес-операции вызывает падение проверки

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

Опубликованный OpenAPI SHALL объединять пять операций Assistant modules и их 22 схемы из предоставленной выгрузки с уже принятым контрактом навыков, включая `PUT /api/control/api/skills/v1/skills/{skill_id}/intents`, обязательное поле `SkillResponse.intents` и девять схем расширения intents. Все прежние операции и определения SHALL сохранять свою семантику. Итог SHALL содержать 34 операции и 124 схемы без неразрешимых ссылок. Security metadata источников SHALL сохраняться без добавления runtime auth.

Документация SHALL обозначать полный OpenAPI как объединённый контракт, указывать происхождение Assistant modules из `message.txt` и сохранение согласованного расширения intents MOS-809, а не заявлять точную копию выгрузки. Самостоятельные контракты Assistant modules и Skills/Domains SHALL соответствовать полному контракту и содержать все необходимые локальные зависимости. Опубликованные TypeScript-типы SHALL соответствовать объединённому OpenAPI. Использование контракта, генерация и проверки после обновления MUST NOT требовать файл из личной папки загрузок.

#### Scenario: Add modules without losing skill APIs

- **WHEN** потребитель использует обновлённые контракты и типы
- **THEN** доступны пять операций модулей и прежний PUT intents; карточка навыка по-прежнему требует intents, а остальные прежние операции и определения не изменены

#### Scenario: Standalone contract consistency

- **WHEN** потребитель открывает самостоятельный контракт Assistant modules или Skills/Domains
- **THEN** его операции и зависимые схемы совпадают с полным контрактом, все локальные ссылки разрешаются, а Skills/Domains содержит девять операций, включая PUT intents

#### Scenario: Repository-only contract checks

- **WHEN** контрактные проверки и генерация типов выполняются без исходного файла в папке загрузок
- **THEN** используются версионируемые файлы репозитория; расхождение самостоятельного раздела или generated-типов с полным OpenAPI обнаруживается проверками

### Requirement: Skill intents mock survives contract refresh

Mock API SHALL сохранять чтение intents в карточке навыка и замену набора через PUT intents с контрактной валидацией, обязательным Idempotency-Key и expected_version. Успешная запись SHALL увеличивать версию навыка и отражаться в последующем GET. Повтор с тем же ключом и телом SHALL возвращать прежний ответ без повторной мутации. Устаревшая версия SHALL давать mock conflict 409 без изменения данных; пустой набор SHALL очищать группы. Локально формируемые normalized/source/created_at SHALL документироваться как mock-данные, а не реальная нормализация, применение или дообучение.

#### Scenario: Save read retry and clear

- **WHEN** набор групп сохранён, прочитан через GET, повторно отправлен с тем же ключом и телом, затем очищен с актуальной версией и новым ключом
- **THEN** GET отражает сохранённые группы; повтор возвращает исходный результат и не увеличивает версию; очистка возвращает пустой набор и новую версию

#### Scenario: Invalid or stale intent write

- **WHEN** PUT intents содержит невалидную группу, не содержит обязательного Idempotency-Key либо отправлен с устаревшей версией и новым ключом
- **THEN** первые два случая возвращают контрактный 422, последний — mock 409, а сохранённые группы и версия не меняются
