## Purpose

Обеспечить серверную CSV-выгрузку диалогов по принятому бизнес-контракту v1.0 от 07.10.2026, без подмены результатом загруженной страницы.

## ADDED Requirements

### Requirement: Export uses the accepted synchronous business API

UI SHALL использовать POST `/api/control/api/dialogs/v1/dialogs/export` для selection либо chat_ids и GET `/api/control/api/dialogs/v1/dialogs/{chat_id}/export` для карточки. UI MUST NOT собирать CSV из реестра, обходить страницы/detail для экспорта, создавать job API или собственные auth/session/RBAC. Запросы экспорта SHALL использовать общий транспорт по `control-center-http` и `mpmm-session`: real mode с общей MPMM-сессией, mock mode без credentials. HTTP fixtures SHALL проверять интеграцию; недоступный backend MUST NOT подменяться локальным успешным файлом.

#### Scenario: Backend is unavailable

- **WHEN** сервер возвращает 503
- **THEN** UI показывает ошибку и сохраняет параметры для повтора без CSV и сообщения успеха

### Requirement: Export supports three explicit scopes

Выгрузка отбора SHALL передавать applied selection целиком со сложными условиями, заменяя только period значением формы, без sort/cursor/draft. Выгрузка отмеченных SHALL передавать только chat_ids, без формы и периода, и получать dialogs со всеми 24 колонками без параметров. Карточка SHALL запрашивать отдельный GET с её chat_id и получать пять фиксированных колонок переписки. UI SHALL объяснять возможный пропуск недоступных отмеченных IDs сервером.

#### Scenario: Full selection spans multiple pages

- **WHEN** загружена только первая страница реестра
- **THEN** выгрузка всего отбора передаёт selection, а не IDs загруженных строк, и принимает серверный файл за пределами этой страницы

#### Scenario: Export from a card

- **WHEN** сотрудник выгружает карточку
- **THEN** запрашивается только её chat_id без отметок, периода, формы или selection реестра

### Requirement: Row selection has an explicit boundary

Отметки SHALL идентифицироваться через chat_id, сохраняться при сортировке/догрузке и очищаться при смене применённого отбора. «Отметить показанные» SHALL затрагивать только загруженные строки; снятие показанных MUST NOT удалять скрытые отметки. UI SHALL показывать фактическое число отмеченных, а весь отбор выгружать отдельным действием.

#### Scenario: More results than visible rows

- **WHEN** пользователь отмечает показанные строки при наличии следующей страницы
- **THEN** отмечены только загруженные chat_ids; после догрузки новые строки не отмечены автоматически

#### Scenario: Selection and sorting change

- **WHEN** меняется сортировка или загружается следующая страница
- **THEN** отметки сохраняются, но после изменения applied selection очищаются

### Requirement: Export form follows accepted CSV options

Форма отбора SHALL поддерживать today, last_7_days, last_30_days, previous_month, custom; период заменяет selection.period. При исходном all_time/отсутствующем периоде форма SHALL явно показывать last_30_days. Формат dialogs SHALL иметь все 24 колонки по умолчанию, запрещать пустой выбор; messages SHALL иметь фиксированные восемь колонок, недоступный выбор fields и не отправлять fields. include_parameters SHALL быть доступен обоим форматам и выключен по умолчанию. Счётчик SHALL использовать search с тем же selection и limit=1 и не показывать устаревший total после смены периода.

#### Scenario: Message format

- **WHEN** выбран messages
- **THEN** fields не отправляется, серверный файл принимается без пересборки, а UI объясняет фиксированный состав колонок

#### Scenario: Invalid period or no fields

- **WHEN** custom-период неполон/обратный либо в dialogs сняты все колонки
- **THEN** выгрузка блокируется и ошибка объясняется без запроса экспорта

### Requirement: Export progress and failures are truthful

UI SHALL показывать формирование до получения синхронного ответа, исключать повторный запуск во время запроса, не вводить клиентский timeout/автоповтор и сохранять настройки после ошибок. Сообщение после запуска скачивания SHALL говорить о передаче браузеру, а не подтверждённом сохранении файла. 413, 422, 503 и ошибки карточки SHALL сохраняться как ошибки исходной операции. В real mode обработка 401 SHALL следовать общей `mpmm-session`, включая переход в MPMM при невосстановимой сессии, без автоматического повтора экспорта. 403 MUST NOT запускать refresh. Feature MUST NOT добавлять собственные auth-редиректы; в mock mode auth-действия отсутствуют.

#### Scenario: Oversized export

- **WHEN** сервер отвечает 413 EXPORT_TOO_LARGE
- **THEN** UI показывает серверное объяснение и позволяет изменить параметры, не сохраняет частичный файл

### Requirement: Download preserves and validates the server file

До создания download URL клиент SHALL проверить HTTP 200, CSV MIME/UTF-8, Content-Disposition attachment с UTF-8 filename*, Content-Length, nosniff, no-store, BOM и соответствие размера. JSON вместо CSV MUST NOT сохраняться. Серверные байты SHALL передаваться без изменения; небезопасные части имени SHALL обезвреживаться; Object URL SHALL освобождаться. Сервер SHALL формировать CSV по §2.5–2.11: BOM, `;`, LF, quoting, защита от формул, контрактные параметры/порядок. Клиентские fixtures SHALL проверять сохранность этих байтов, а не реализовывать серверный encoder.

#### Scenario: Error body instead of file

- **WHEN** вместо CSV получен JSON или файл не соответствует заголовкам/длине
- **THEN** отображается ошибка, download URL не создаётся, успех не показывается

#### Scenario: Special CSV content

- **WHEN** серверный файл содержит Unicode, кавычки, переносы строк и защищённый формульный текст
- **THEN** браузеру передаются те же байты, включая BOM, без повторного кодирования
