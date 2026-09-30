## MODIFIED Requirements

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

## ADDED Requirements

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
