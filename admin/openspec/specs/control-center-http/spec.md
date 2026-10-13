# Control Center HTTP Specification

## Purpose

Обеспечить единое контрактное HTTP-взаимодействие фронтенда Центра управления с backend и dev-сервером без альтернативного пути через локальные моки.

## Requirements

### Requirement: Contract-aligned requests

Приложение SHALL отправлять API-запросы относительно настраиваемого базового URL, по умолчанию `/api/control/api`, с методами, параметрами, заголовками и JSON-телами из `docs/api/contracts/openapi.json`. UI base `/tsam-panel/` MUST NOT добавляться к API URL. Неопределённые optional query-параметры MUST NOT передаваться строками `undefined` или `null`.

#### Scenario: Paginated request with search

- **WHEN** запрошены навыки с поиском «Моя Москва», limit 10 и offset 20
- **THEN** запрос направлен на `/api/control/api/skills/v1/skills` с корректно закодированным query, limit и offset, без UI-префикса и отсутствующих фильтров

#### Scenario: Contract source changes

- **WHEN** контракт изменён без обновления производных TypeScript DTO
- **THEN** проверка синхронизации типов завершается ошибкой, а не подтверждает совместимость устаревших типов

### Requirement: Authentication and mutation headers

В защищённом режиме `mpmm-session` транспорт SHALL подготавливать общую сессию и автоматически добавлять оба raw-заголовка X-Access-Token и X-Admin-Token только для разрешённых адресов. Это SHALL распространяться на JSON и binary/content/export запросы. Эти два заголовка SHALL определяться актуальной сессией, а не устаревшими значениями вызывающего кода. Транспорт MUST NOT автоматически добавлять Authorization/Bearer или dev-токены. В mock mode SHALL отсутствовать чтение MPMM token и автоматические credentials; mock principal SHALL задаваться add-local-session-demo. Общий механизм остальных явно переданных допустимых заголовков SHALL сохраняться, без credentials в mock mode. Idempotency-Key SHALL оставаться неизменным для повтора одной логической мутации; новая мутация SHALL получать новый ключ. Мутации MUST NOT автоматически повторяться после refresh, 401, сетевого сбоя или иной ошибки.

Транспорт MUST NOT вычислять permission по URL/method, требовать wildcard для неизвестного endpoint или создавать локальный 403 из permissions. Проверки назначения credentials, готовности и поколения сессии SHALL сохраняться; backend SHALL владеть авторизацией бизнес-запросов.

#### Scenario: Authenticated idempotent mutation

- **WHEN** в real mode вызывается создание домена с ключом идемпотентности после успешной подготовки сессии
- **THEN** POST содержит исходный Idempotency-Key, контрактное тело и актуальную пару X-токенов без автоматически добавленного Authorization

#### Scenario: Explicit retry after same-user refresh

- **WHEN** мутация завершилась ошибкой, refresh и `/me` подтвердили прежнего пользователя и необходимые права, затем пользователь явно повторяет ту же логическую операцию
- **THEN** тело, версия и Idempotency-Key прежней попытки сохраняются, даже если boundary обновлялся и mutation cache очищался; без явного действия пользователя повтор не отправляется

#### Scenario: Production without credentials

- **WHEN** production build/start открыт без пригодной MPMM-сессии на любом hostname
- **THEN** auth не отключается: бизнес-запрос ждёт подтверждения сессии, отсутствие токенов ведёт на настроенный login URL; mock credentials не подставляются

#### Scenario: Mock request without credentials

- **WHEN** запрос выполняется в yarn dev с mocksEnabled
- **THEN** транспорт не добавляет Bearer или фиктивные credentials и не читает MPMM token; sessionStorage для выбранного mock-профиля и сценария допускается согласно add-local-session-demo

#### Scenario: Explicit request headers

- **WHEN** вызывающий код передаёт допустимые заголовки и существующий Idempotency-Key
- **THEN** их значения сохраняются, кроме session-owned X-токенов в защищённом режиме, которые берутся из актуального набора после refresh

#### Scenario: Real access error

- **WHEN** backend возвращает 401 или 403
- **THEN** транспорт сохраняет статус и детали; в защищённом режиме 401 обрабатывается по mpmm-session без replay исходной операции, 403 не запускает refresh; в mock mode реальные auth-действия отсутствуют

#### Scenario: Binary response after refresh

- **WHEN** авторизованный пользователь с нужными правами скачивает файл при истекающем токене
- **THEN** content/export endpoint вызывается после refresh с актуальной парой заголовков, отмена и проверка binary ошибок сохраняются

### Requirement: Observable response and error handling

Транспорт SHALL проверять успешный envelope и используемые данные ЦАМ, возвращать data и сохранять status/message/code/details доступных ошибок. Non-2xx, непустой envelope errors и невалидное успешное тело SHALL приводить к различимым ошибкам, а не к пустому результату. ResponseCode MUST NOT интерпретироваться как недокументированный enum успеха. Auth MPMM SHALL обрабатываться отдельным контрактом result/error_code/error_message; его формат MUST NOT менять формат бизнес-клиентов ЦАМ. Session lifecycle при 401 SHALL применяться только в защищённом режиме и MUST NOT превращать отказ исходного запроса в успех.

#### Scenario: Valid success envelope

- **WHEN** сервер ЦАМ возвращает 200 с контрактным data и произвольной допустимой строкой code без errors
- **THEN** вызывающий код получает проверенные данные независимо от конкретного литерала code

#### Scenario: Validation and access errors

- **WHEN** сервер возвращает 422 с validation details либо 401/403
- **THEN** ошибка сохраняет HTTP status и детали; отсутствует автоматический replay 4xx, а только защищённый 401 может инициировать восстановление по mpmm-session

#### Scenario: HTML failure or malformed success

- **WHEN** сервер возвращает HTML с 500 либо невалидный JSON/envelope с 200
- **THEN** первый ответ сохраняется как HTTP-ошибка 500, второй — как ошибка протокола; ни один не превращается в успешный пустой список

#### Scenario: Empty response and application error

- **WHEN** получен успешный 204 без тела либо JSON с непустым errors
- **THEN** 204 обрабатывается без JSON parse error, а непустой errors передаётся как ошибка, даже при HTTP 200

#### Scenario: Cancellation during shared refresh

- **WHEN** потребитель отменил свой запрос во время ожидания общей подготовки сессии
- **THEN** его бизнес-запрос не отправляется, отмена не отображается как серверная ошибка и другие потребители могут завершить подготовку сессии

### Requirement: Cancellation

API-запросы SHALL поддерживать отмену со стороны потребителя; отменённый запрос MUST NOT подменять результат актуального запроса или отображаться как обычная серверная ошибка.

#### Scenario: Filter changes during a request

- **WHEN** пользователь меняет фильтр до завершения предыдущего запроса и предыдущий запрос отменяется
- **THEN** отмена доходит до HTTP-транспорта, старый результат не заменяет новый и отменённый запрос не повторяется автоматически

### Requirement: Updated contract preserves accepted supplements

Поставляемый контракт SHALL включать операции и схемы выгрузки `newcontract.json` от 13.10.2026, включая managed resources, и сохранять принятое дополнение экспорта диалогов. Нормализация security SHALL сохранять требование обоих X-токенов согласно действующему контракту сессии. Секционные контракты и производные DTO SHALL соответствовать объединённому контракту; все локальные ссылки SHALL разрешаться. Публикация новых CRUD-операций в контракте MUST NOT сама по себе включать новые экраны или объявлять интеграцию работающей.

#### Scenario: New snapshot with local export supplement

- **WHEN** новый контракт включён в поставку
- **THEN** все 109 операций выгрузки и два принятых метода экспорта диалогов доступны в контракте; четыре экспортные схемы сохранены, security не ослаблен до выбора одного токена

#### Scenario: Saved dialog filter response renamed upstream

- **WHEN** сервер возвращает прежние wire-поля сохранённого фильтра диалогов после переименования OpenAPI schema
- **THEN** существующие чтение, создание и применение фильтра сохраняют поведение; типы не смешиваются с фильтрами managed resources

#### Scenario: Contract sections and generated types stay consistent

- **WHEN** обновлён общий контракт
- **THEN** секционные документы содержат те же операции и необходимые зависимые схемы, а проверка generated DTO обнаруживает их рассинхронизацию

### Requirement: Existing editors use PUT aliases

Существующие редакторы навыков, подключения навыка и доменов SHALL отправлять изменения через опубликованные PUT-алиасы по прежним адресам. Тело, частичный характер обновления, expected_version, Idempotency-Key, клиентская валидация и обработка ошибок SHALL сохраняться. Создание SHALL оставаться POST. Клиент MUST NOT автоматически повторять мутацию через PATCH при ошибке PUT.

#### Scenario: Save a skill or domain edit

- **WHEN** пользователь сохраняет валидное изменение существующего навыка, его подключения или домена
- **THEN** отправляется PUT с прежним контрактным телом и исходным ключом операции; успешный ответ обновляет UI прежним способом

#### Scenario: Invalid form does not send mutation

- **WHEN** ввод нарушает существующие правила редактора
- **THEN** запрос не отправляется, ошибки и введённые значения сохраняются

#### Scenario: Failed PUT and explicit retry

- **WHEN** PUT завершается конфликтом версии или сетевой ошибкой
- **THEN** UI сохраняет ошибку и ввод, не выполняет PATCH fallback или автоматический replay; явный повтор той же логической операции сохраняет тело и Idempotency-Key
