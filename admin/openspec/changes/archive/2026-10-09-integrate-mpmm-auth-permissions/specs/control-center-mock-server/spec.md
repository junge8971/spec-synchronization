## MODIFIED Requirements

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
