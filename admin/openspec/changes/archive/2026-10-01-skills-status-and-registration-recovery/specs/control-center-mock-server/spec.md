## MODIFIED Requirements

### Requirement: Complete supplied operation coverage

Mock API SHALL реализовать 39 бизнес-операций объединённого OpenAPI: Domains/Skills — 10, включая PUT intents и POST status, Surfaces — 11, Teams — 8, Assistant modules — 5, Analytics — 5. Ответы SHALL соответствовать описанным status codes, envelope, схемам, nullable/required полям, enum и форматам. Access-операция `GET /api/control/api/auth/v1/me` SHALL быть явно исключена из текущего покрытия и MUST NOT обслуживаться mock server. Отсутствие Bearer MUST NOT препятствовать чтению или мутациям бизнес-данных. Это SHALL документироваться как ограничение локального mock server, а не изменение требований безопасности backend. Непредоставленные разделы MUST NOT выдаваться за реализованный контракт. Mock-семантика аналитики и смены статуса MUST NOT выдаваться за production-гарантию вычислений или допустимых переходов.

#### Scenario: Contract coverage check

- **WHEN** контрактные тесты перечисляют 40 операций объединённого OpenAPI
- **THEN** для каждой из 39 бизнес-операций имеется исполняемый сценарий без Authorization с проверкой ответа по схеме; единственное явное исключение — указанная Access-операция, а пропуск любой бизнес-операции вызывает падение проверки

#### Scenario: Invalid contract input

- **WHEN** передан невалидный UUID/UUIDv7, enum, limit/offset, обязательное тело или отсутствует обязательный Idempotency-Key
- **THEN** mock server возвращает предусмотренный контрактом validation response, а не успешные данные; тело 422 соответствует HTTPValidationError там, где он описан

#### Scenario: Unknown resource or absent credentials

- **WHEN** без Bearer запрошен отсутствующий корректный ID бизнес-сущности
- **THEN** сервер возвращает 404 по документированной mock error convention без изменения исходного OpenAPI

#### Scenario: Retired current principal endpoint

- **WHEN** запрошен `/api/auth/v1/me` у локального mock server
- **THEN** возвращается 404 как для отсутствующей операции, без фиктивного пользователя или запуска сессии

#### Scenario: Filter skills by status

- **WHEN** запрошена страница навыков с status и другими поддерживаемыми фильтрами
- **THEN** фильтрация применяется до пагинации, DTO содержит status, а total соответствует полной отфильтрованной выборке

#### Scenario: New operations preserve coherent mock state

- **WHEN** выполняются опубликованные изменение статуса навыка или сохранение аналитической доски
- **THEN** последующие чтения отражают сохранённое mock-состояние, ответ проходит соответствующую схему; restart восстанавливает seed, а правила, отсутствующие в контракте, документируются как локальная mock-конвенция

### Requirement: Merged contract preserves accepted skill intents

Опубликованный OpenAPI SHALL объединять новую предоставленную выгрузку `message.txt` со всеми принятыми ранее API, включая `PUT /api/control/api/skills/v1/skills/{skill_id}/intents`, обязательное поле `SkillResponse.intents` и девять схем расширения intents. Из новой поставки SHALL быть добавлены SkillStatus, обязательный status list/detail, серверный status-фильтр, POST изменения статуса и пять операций Analytics с зависимыми схемами. Все остальные прежние определения и операции SHALL сохранять семантику. Итог SHALL содержать 40 операций и 156 схем без неразрешимых ссылок. Security metadata источников SHALL сохраняться без добавления runtime auth.

Документация SHALL обозначать полный OpenAPI как объединённый контракт, указывать происхождение новой поставки из `message.txt` и сохранение расширения intents MOS-809, а не заявлять точную копию выгрузки. Самостоятельные контракты Assistant modules, Skills/Domains и Analytics SHALL соответствовать полному контракту и содержать все необходимые локальные зависимости. Опубликованные TypeScript-типы SHALL соответствовать объединённому OpenAPI. Использование контракта, генерация и проверки после обновления MUST NOT требовать файл из личной папки загрузок.

#### Scenario: Add modules without losing skill APIs

- **WHEN** потребитель использует обновлённые контракты и типы
- **THEN** доступны пять операций модулей, новые status/Analytics и прежний PUT intents; карточка навыка по-прежнему требует intents и дополнительно status, а прочие прежние операции и определения сохранены

#### Scenario: Standalone contract consistency

- **WHEN** потребитель открывает самостоятельный контракт Assistant modules, Skills/Domains или Analytics
- **THEN** его операции и зависимые схемы совпадают с полным контрактом, все локальные ссылки разрешаются; Skills/Domains содержит десять операций, включая PUT intents и POST status, Analytics содержит пять опубликованных операций

#### Scenario: Repository-only contract checks

- **WHEN** контрактные проверки и генерация типов выполняются без исходного файла в папке загрузок
- **THEN** используются версионируемые файлы репозитория; расхождение самостоятельного раздела или generated-типов с полным OpenAPI обнаруживается проверками
