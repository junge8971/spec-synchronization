# dialog-registry Specification

## Purpose

Предоставить серверный реестр диалогов с единым отбором, достоверными счётчиками и устойчивым последовательным просмотром результатов.

## Requirements

### Requirement: Registry uses an accepted business contract

Реестр SHALL подключать поиск и справочники только после принятия бизнес-контракта. До этого UI MUST NOT обращаться к предположительным endpoints, заменять сервер локальными fixtures или показывать фиктивные результаты. Принятый поиск SHALL использовать POST `/api/control/api/dialogs/v1/dialogs/search`; справочники — GET `/api/control/api/dialogs/v1/dictionaries`.

#### Scenario: Contract is still a draft

- **WHEN** проект PDF ещё не принят для интеграции
- **THEN** раздел не имитирует работающий реестр и не отправляет запросы по предположительному API

### Requirement: Registry represents server rows faithfully

Реестр SHALL показывать шесть колонок: обращение/участники, начало, завершение, поверхность, оценка работы оператора, длительность. Строка SHALL использовать chat_id, first_user_message, skills, has_operator, has_failure, user_authorization, started_at, ended_at, duration_sec, channel_id, channel_name, operator_rating. Первые два навыка и число остальных SHALL отображаться без потери независимых признаков оператора и сбоя. Пометка «без авторизации» SHALL соответствовать unauthorized и authorized_in_dialog. Переход SHALL адресовать карточку по chat_id с сохранением UI basename.

#### Scenario: Unfinished and unrated dialog

- **WHEN** ended_at и operator_rating равны null
- **THEN** строка показывает «не завершён» и отсутствие оценки, а не фиктивную дату и нулевую оценку

#### Scenario: Multiple participants and failure

- **WHEN** диалог содержит пять навыков, оператора и сбой
- **THEN** видны первые два навыка, «ещё 3», пометка оператора и доступно обозначенный сбой; текст обращения безопасно сокращён только в представлении

### Requirement: Search shares one versioned selection

Поиск SHALL передавать selection с schema_version=1, q, period, channel_ids, skill_ids, condition_group и time_zone. Все части отбора SHALL соединяться AND; пустые быстрые фильтры не ограничивают выдачу. По умолчанию период SHALL быть all_time в пределах глубины хранения. Presets today, last_7_days, last_30_days, previous_month, all_time и custom SHALL передаваться серверу без клиентского вычисления UTC-границ. Custom SHALL содержать обе календарные даты включительно с date_from не позже date_to. UI MUST NOT отфильтровывать только загруженные строки или молча удалять неизвестные справочные IDs.

#### Scenario: Basic and advanced criteria together

- **WHEN** применены q, две поверхности, навык и группа условий
- **THEN** они отправляются одним selection, а total и строки соответствуют серверному результату всего отбора

#### Scenario: One-day custom interval

- **WHEN** date_from равна date_to
- **THEN** поиск передаёт один календарный день в согласованном time_zone; обратный диапазон блокируется с ошибкой поля

### Requirement: Cursor pagination preserves request identity

Реестр SHALL поддерживать sort по started_at, ended_at, channel, operator_rating, duration в обоих направлениях, default -started_at. Колонка обращения MUST NOT предлагать неподдержанную сортировку. Страницы SHALL запрашиваться с limit 1–100, default 25, и непрозрачным cursor. «Показать ещё» SHALL сохранять selection/sort; изменение отбора или сортировки SHALL сбрасывать цепочку страниц. UI SHALL сохранять серверный порядок с nulls-last и MUST NOT пересортировывать отдельную страницу.

#### Scenario: Filter changes during next-page request

- **WHEN** пользователь меняет отбор во время загрузки следующей страницы
- **THEN** новый запрос начинается без старого cursor, а поздний ответ не добавляется в новую выдачу

#### Scenario: Continuation fails

- **WHEN** загрузка следующей страницы завершается ошибкой
- **THEN** ранее загруженные строки остаются, доступен повтор той же страницы без повторного добавления уже показанных строк

#### Scenario: Invalid cursor

- **WHEN** сервер возвращает 422 с ошибкой /cursor
- **THEN** интерфейс предлагает начать поиск заново и не запускает бесконечные повторы невалидного курсора

### Requirement: Counts and request states remain truthful

UI SHALL использовать серверный total и data_updated_at; null timestamp SHALL скрывать подпись обновления. Loading, успешный empty и error/retry SHALL различаться. Отказ справочников SHALL оставлять доступными поиск q/period и не превращать справочники в успешные пустые списки. Ошибки SHALL сохранять status/code и адресные field/code/message, а 401/403 MUST NOT запускать auth-последовательность. Текст, подсветка и управление таблицей SHALL оставаться безопасными и доступными с клавиатуры.

#### Scenario: Total changes between pages

- **WHEN** следующая страница содержит другой total и data_updated_at=null
- **THEN** показан новый серверный total, не длина массива строк, а подпись времени обновления отсутствует

#### Scenario: Search service unavailable

- **WHEN** поиск возвращает 503 ESK_CORE_UNAVAILABLE
- **THEN** отображается ошибка с повтором, а не «Диалоги не найдены» или локальные демонстрационные записи
