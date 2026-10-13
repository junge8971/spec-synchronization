# dialog-details Specification

## Purpose

Предоставить согласованный снимок переписки и сведений диалога с участниками, операторами и безопасными действиями над вложениями.

## Requirements

### Requirement: One accepted detail response serves the card

После принятия бизнес-контракта карточка SHALL загружаться GET `/api/control/api/dialogs/v1/dialogs/{chat_id}` независимо от наличия строки в реестре. Один ответ SHALL предоставлять данные переписки, общей информации и вкладок; смена вкладки MUST NOT сама создавать дополнительное чтение. До принятия контракта MUST сохраняться честная недоступность без вымышленных запросов. Поздний ответ другого chat_id MUST NOT заменять текущую карточку.

#### Scenario: Direct link outside loaded registry

- **WHEN** открыта прямая ссылка на chat_id, отсутствующий в загруженной странице
- **THEN** выполняется detail-запрос этого ID без поиска во всех страницах реестра и без UUID-ограничения навыков

#### Scenario: Switch tabs

- **WHEN** сотрудник переходит между общей информацией и реализованными вкладками карточки
- **THEN** используется тот же detail snapshot без отдельных запросов вкладок

### Requirement: Conversation and metadata preserve contract meaning

Карточка SHALL показывать chat_id/session_id, время начала/завершения, duration_sec, категории, причину/инициатора завершения, поверхность/url, счётчики, user, participants и operators из ответа. Сообщения SHALL сохранять порядок источника при равном времени, безопасно отображать user/skill/subsystem/operator и текст либо вложения. Авторизация жителя SHALL различать authorized, authorized_in_dialog с authorized_at и unauthorized; это MUST NOT становиться сессией сотрудника. Null SHALL отличаться от нуля и пустого массива. Незавершённая длительность SHALL показываться как серверный снимок с признаком продолжения, без вымышленного завершения.

#### Scenario: Attachment-only message

- **WHEN** text=null и есть вложения
- **THEN** сообщение показывает автора, время и вложения без подставного текста и без потери места в переписке

#### Scenario: Multiple operators

- **WHEN** operators содержит двух операторов
- **THEN** показаны обе записи с собственными line, accepted_at и message_count; operator_rating остаётся одной оценкой диалога

#### Scenario: Participant shares

- **WHEN** participants содержит доли, сумма которых из-за округления отличается от 100
- **THEN** показаны серверные message_count/share_percent и знаменатель step_count без клиентского исправления долей

### Requirement: Attachments expose only supported actions

Вложения SHALL показывать имя, размер, состояние и допустимые действия. Для unprocessed UI MUST NOT предлагать view/download или опрашивать обработку. Для ready SHALL быть доступно скачивание; просмотр SHALL зависеть от серверного viewable. Счётчики SHALL использовать только total/to_skill/to_operator; UI MUST NOT вычислять «без адресата» или скрытые вложения из догадок.

#### Scenario: Unprocessed snapshot

- **WHEN** вложение имеет status=unprocessed
- **THEN** видна причина отсутствия действий; запрос содержимого и ожидание будущей обработки не запускаются

#### Scenario: Ready but not viewable

- **WHEN** готовое вложение имеет viewable=false
- **THEN** доступно скачивание, но не просмотр независимо от расширения имени файла

### Requirement: Attachment content is fetched safely and intentionally

Содержимое SHALL запрашиваться только по действию сотрудника через `/dialogs/{chat_id}/attachments/{attachment_id}/content` с mode=view|download относительно базового URL. Файл SHALL обрабатываться как binary, ошибки — как JSON-envelope. Просмотр MUST сохранять изоляцию активного содержимого и защиту, эквивалентную серверным sandbox/nosniff/no-store; URL MUST NOT содержать токен. Ошибка view MUST NOT автоматически скачивать файл. Внешние тексты/URL MUST NOT исполнять HTML или небезопасные схемы.

#### Scenario: Attachment error response

- **WHEN** чтение возвращает ATTACHMENT_NOT_FOUND, ATTACHMENT_NOT_PROCESSED или ATTACHMENT_SOURCE_UNAVAILABLE
- **THEN** показана соответствующая ошибка действия, JSON не сохраняется как файл, а уже загруженная карточка остаётся

#### Scenario: Unsafe preview path

- **WHEN** выбранный способ browser preview не обеспечивает изоляцию содержимого
- **THEN** просмотр не включается до подтверждения безопасного способа; blob URL не считается автоматически защищённым CSP исходного ответа

### Requirement: Detail failures remain distinguishable

Карточка SHALL различать loading, NOT_FOUND, ошибки ЕСК и ошибки сведений о вложениях. При 404 SHALL показываться «Диалог не найден» с переходом к реестру. При 503 MUST NOT показываться пустая успешная переписка. route.available=false SHALL затрагивать только маршрут, не остальные данные. Ошибки 401/403 SHALL показываться без login/refresh. Ссылки на навыки SHALL использовать подтверждённый ID resolver; при его отсутствии название/service_id SHALL оставаться текстом без ложного route UUID.

#### Scenario: Metadata source for attachments fails

- **WHEN** detail возвращает 503 ATTACHMENT_SOURCE_UNAVAILABLE
- **THEN** показана ошибка карточки с повтором, а не сообщение «вложений нет»

#### Scenario: Trace alone is unavailable

- **WHEN** detail успешен, но route.available=false
- **THEN** переписка и общие сведения доступны, маршрут отмечен недоступным
