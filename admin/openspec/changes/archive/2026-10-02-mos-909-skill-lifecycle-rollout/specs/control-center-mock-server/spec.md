## MODIFIED Requirements

### Requirement: Merged contract preserves accepted skill intents

Опубликованный полный OpenAPI SHALL соответствовать актуальной предоставленной выгрузке `message.txt`, уже включающей принятые ранее API, PUT intents, обязательные SkillResponse.intents/status, status-фильтр, POST status, Assistant modules и Analytics. Итог SHALL сохранять 40 операций и 156 схем без неразрешимых ссылок. SkillPhraseRequest.weight SHALL иметь minimum 0, UpdateSkillIntentRequest.id SHALL допускать nullable UUID вместо ограничения UUIDv7. Остальные прежние операции и определения SHALL сохранять семантику. Security metadata источника SHALL сохраняться без runtime auth.

Документация SHALL отличать текущую полную поставку от исторического ручного объединения с MOS-809. Самостоятельные разделы SHALL совпадать с полным контрактом и включать замыкание зависимых схем; Skills/Domains SHALL содержать десять операций, Analytics и Assistant modules — по пять. Generated-типы SHALL соответствовать обновлённому OpenAPI. Генерация и проверки MUST NOT зависеть от личного файла Downloads.

#### Scenario: Add modules without losing skill APIs

- **WHEN** потребитель использует обновлённые контракты и типы
- **THEN** сохранены пять операций модулей, status/Analytics и PUT intents; карточка по-прежнему требует intents/status и все прежние обязательные поля

#### Scenario: Standalone contract consistency

- **WHEN** проверяется любой самостоятельный раздел
- **THEN** его операции и схемы совпадают с полным контрактом, локальные ссылки разрешаются, Skills/Domains отражает новые minimum/UUID

#### Scenario: Repository-only contract checks

- **WHEN** проверки и генерация выполняются без исходного Downloads-файла
- **THEN** используются repo-файлы; рассинхронизация разделов и generated-типов обнаруживается

## ADDED Requirements

### Requirement: Updated phrase constraints in mock requests

Mock PUT intents SHALL применять опубликованные minimum weight=0 и UUID группы, сохраняя ID навыка UUIDv7, обязательные expected_version/Idempotency-Key, coherent GET, пустую очистку и replay. Отклонение input SHALL оставлять данные и версию неизменными.

#### Scenario: Zero negative and omitted weight

- **WHEN** отправлены weight=0, weight<0 или запрос без weight
- **THEN** ноль сохраняется, отрицательный даёт 422 без изменений, пропущенный использует 1; успешные ответы проходят контрактную схему

#### Scenario: UUID variants

- **WHEN** передан UUIDv4 группы или malformed UUID
- **THEN** первый сохраняется и читается без замены ID, второй даёт 422 без изменений; некорректный skill_id также отклоняется

### Requirement: Single skill status mock round-trip

Mock SHALL обеспечивать проверяемые POST status и последующие detail/list для переходов draft→checking, sandbox→review и whitelist→prod. Он SHALL сохранять существующую конвенцию приёма любого опубликованного target enum, а не объявлять UI-матрицу production-правилом. Успех SHALL увеличивать version и обновлять updated_at без изменения intents. Replay того же method/path/key/body SHALL возвращать исходный ответ без повторной мутации; иной body с тем же ключом и конфликт expected_version SHALL давать документированный mock 409 без изменения данных. Автоматическое завершение обучения, тестов и ревью MUST NOT моделироваться таймером.

#### Scenario: UI transitions and coherent reads

- **WHEN** каждая из трёх одиночных команд отправлена с актуальной версией и новым ключом
- **THEN** POST, detail и list показывают согласованный target status/version, intents не меняются, ответы соответствуют схеме

#### Scenario: Replay conflicts and invalid target

- **WHEN** повторены прежний запрос, изменённое тело с прежним ключом, новая команда со старой версией или неизвестным enum
- **THEN** соответственно возвращаются исходный результат без новой мутации, 409, 409 и 422; ошибки не меняют данные

#### Scenario: Intermediate state fixtures

- **WHEN** запрашивается seed-навык в checking/training/autotest/review либо mock явно установлен в такое состояние
- **THEN** он остаётся в этом состоянии до явной мутации, а UI не получает вымышленные результаты процесса
