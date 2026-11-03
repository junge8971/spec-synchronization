## MODIFIED Requirements

### Requirement: Export uses the accepted synchronous business API

UI SHALL использовать опубликованные в текущем live API POST `/api/control/api/dialogs/v1/dialogs/export` для selection либо chat_ids и GET `/api/control/api/dialogs/v1/dialogs/{chat_id}/export` для карточки. Live operationId и DTO SHALL заменить историческое локальное дополнение; правило ровно одного непустого источника состава, игнорирование неприменимых опций и безопасная передача CSV SHALL сохраняться согласно описаниям операций. null состава SHALL означать отсутствие; при chat_ids опции формата/колонок/параметров SHALL игнорироваться, fields SHALL применяться только к selection формата dialogs. UI MUST NOT собирать CSV из реестра, обходить страницы/detail для экспорта, создавать job API или собственные auth/session/RBAC. Запросы экспорта SHALL использовать общий транспорт по control-center-http и mpmm-session: real mode с общей MPMM-сессией, mock mode без credentials. HTTP fixtures SHALL проверять интеграцию; недоступный backend MUST NOT подменяться локальным успешным файлом.

#### Scenario: Backend is unavailable

- **WHEN** сервер возвращает 503
- **THEN** UI показывает ошибку и сохраняет параметры для повтора без CSV и сообщения успеха

#### Scenario: Published export replaces supplement

- **WHEN** клиент и моки используют обновлённый контракт
- **THEN** оба экспорта работают по опубликованным операциям без старых operationId и без потери проверок файла и бизнес-ограничений

#### Scenario: Mutually exclusive scopes

- **WHEN** переданы оба selection/chat_ids либо ни одного непустого поля
- **THEN** запрос отклоняется без файла, несмотря на недостаточную выразительность формальной схемы

#### Scenario: Irrelevant options

- **WHEN** API получает chat_ids с неприменимыми опциями либо messages с fields
- **THEN** неприменимые опции игнорируются по описанию операции, а применимые поля продолжают валидироваться
