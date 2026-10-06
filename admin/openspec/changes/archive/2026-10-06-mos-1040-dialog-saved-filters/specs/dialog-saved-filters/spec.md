## Purpose

Обеспечить серверное сохранение именованного отбора диалогов и безопасное воспроизведение тех же критериев из версионированной ссылки.

## ADDED Requirements

### Requirement: Saved filters use server persistence

После принятия бизнес-контракта UI SHALL читать GET /saved-filters и создавать POST /saved-filters относительно `/api/control/api/dialogs/v1`. Список SHALL отражать серверные filter_id, name, selection, created_at в порядке сохранения. UI MUST NOT заменять серверное хранение localStorage или подставлять сотрудника. Удаление и переименование MUST NOT предлагаться без соответствующего контракта. Ошибка списка SHALL отличаться от успешного пустого списка и не блокировать базовый поиск.

#### Scenario: Filters load while search is unavailable

- **WHEN** сохранённые фильтры загружены, но ЕСК недоступен
- **THEN** чипы доступны; применение может показать ошибку поиска, но список не превращается в пустой

### Requirement: Save only the applied selection

Сохранение SHALL отправлять name и применённый selection со schema_version=1, периодом, time_zone, q, быстрыми фильтрами и condition_group. Сортировка, cursor, отмеченные строки и draft MUST NOT сохраняться. Имя SHALL обрезаться по краям и содержать 1–100 символов. UI SHALL различать SAVED_FILTER_NAME_CONFLICT и SAVED_FILTER_LIMIT_REACHED и показывать успех только по подтверждённому результату.

#### Scenario: Relative filter saved

- **WHEN** сотрудник сохраняет отбор last_7_days при неприменённых изменениях редактора
- **THEN** сервер получает прежний применённый selection с preset last_7_days, а не фиксированными датами или draft

#### Scenario: Network outcome is ambiguous

- **WHEN** ответ создания потерян, а повтор сообщает конфликт имени
- **THEN** UI перечитывает список для проверки результата и не объявляет произвольный одноимённый фильтр успешно созданным текущим действием

### Requirement: Applying a filter replaces selection without losing criteria

Нажатие чипа SHALL восстанавливать полный selection и запускать общий поиск с новым cursor chain. Неизвестные справочные IDs SHALL сохраняться, поскольку они допустимы в поиске. Неподдержанная версия SHALL показывать ошибку, а не частично применять понятные поля и расширять выборку. Относительные периоды SHALL оставаться относительными при каждом новом поиске.

#### Scenario: Missing dictionary option

- **WHEN** сохранённый фильтр содержит ID навыка, которого больше нет в справочнике
- **THEN** ID остаётся критерием; фильтр не превращается в поиск по всем навыкам

### Requirement: Selection links require privacy and format agreement

Пользователь согласовал передачу q/user_sso_id через fragment с риском истории браузера и доступа скриптов. Ссылка SHALL иметь формат `#selection=<URLSearchParams-encoded JSON>` и максимум 8192 байта UTF-8 JSON до URL-кодирования. Fragment SHALL ограничиваться максимальным percent-encoded представлением этого объёма. Ссылка SHALL восстанавливать тот же versioned selection и содержать только origin, basename-aware путь реестра и selection, без query, credentials или указаний прав получателя. UI SHALL предупреждать о чувствительных критериях и копировать ссылку только явным действием. UI MUST NOT считать кодирование защитой или изобретать сервер коротких ссылок.

#### Scenario: Sensitive criteria are copied explicitly

- **WHEN** пользователь копирует применённый отбор с q/user_sso_id
- **THEN** критерии помещены только во fragment, UI предупреждает о риске истории и доступа скриптов; текущий адрес не изменяется автоматически

#### Scenario: Valid round trip after agreement

- **WHEN** получатель открывает корректную ссылку с периодом, быстрыми фильтрами, time_zone и all/any условиями
- **THEN** все критерии восстановлены без потери типов, а запрос не содержит cursor или credentials отправителя

### Requirement: Invalid links and clipboard failures are explicit

Разбор ссылки SHALL предшествовать поиску. Повреждённые данные, неподдержанная schema_version, лишние/дублированные параметры, потеря полей при валидации и превышение согласованного размера SHALL показывать понятную ошибку с явным сбросом; UI MUST NOT молча запускать неограниченный поиск или обрезать условия. Подтверждение копирования SHALL появляться только после успешной записи в буфер.

#### Scenario: Unsupported schema version

- **WHEN** открыта ссылка с неизвестной версией selection
- **THEN** поиск по частично восстановленным критериям не выполняется; предложено исправить ссылку или явно сбросить отбор

#### Scenario: Clipboard permission denied

- **WHEN** запись ссылки в буфер завершается отказом
- **THEN** нет сообщения «Ссылка скопирована», показана доступная ошибка или возможность ручного копирования согласованного адреса
