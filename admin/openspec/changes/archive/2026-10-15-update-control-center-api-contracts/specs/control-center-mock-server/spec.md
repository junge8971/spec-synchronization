## REMOVED Requirements

### Requirement: Explicit unavailable coverage for imported managed resources

**Reason**: Текущие managed handlers уже исполняются, пользователь согласовал полное mock-покрытие новой дельты. Исторический список 43 unavailable операций не описывает требуемое поведение.

**Migration**: Сохранить существующие handlers и добавить новые по требованию Current managed-resource operation coverage. Отсутствие handler остаётся ошибкой запуска, не скрывается fallback 501.

## MODIFIED Requirements

### Requirement: Merged contract preserves accepted skill intents

Объединённый OpenAPI SHALL следовать текущему live-снимку с сохранением всех опубликованных бизнес-операций, включая PUT intents, обязательные SkillResponse.intents/status, status-фильтр, POST status, Assistant modules, Analytics и API диалогов. Исторический auth-фрагмент message (1).txt и локальное дополнение экспорта SHALL NOT замещать актуальные опубликованные определения. SkillPhraseRequest.weight SHALL сохранять minimum 0, UpdateSkillIntentRequest.id SHALL допускать nullable UUID вместо ограничения UUIDv7, пока это соответствует live API. Security SHALL описывать обязательную пару AdminToken/AccessToken в одном объекте требования, фиксируя исправление формального OR исходной выгрузки по явному требованию обоих raw-заголовков.

Документация SHALL различать происхождение снимка, сохранённые нормализации и противоречия дополнительных источников. Самостоятельные разделы SHALL совпадать с объединённым контрактом и содержать замыкание зависимых схем. Generated-типы SHALL соответствовать контракту. Минимальный используемый контракт refresh MPMM SHALL храниться отдельно с result envelope; генерация и проверки MUST NOT зависеть от Downloads, untracked auth-openapi.json или соседнего checkout. Локальное бизнес-покрытие SHALL сохраняться без credentials; runtime mock /me и каталог fixtures SHALL сохранять local-session-demo; реальные токены и backend RBAC в mock server MUST NOT добавляться.

#### Scenario: Add modules without losing skill APIs

- **WHEN** потребитель использует контракт после обновления снимка
- **THEN** сохранены модули, status/Analytics, PUT intents и обязательные поля карточки; опубликованные бизнес-пути диалогов не исчезают

#### Scenario: Standalone contract consistency

- **WHEN** проверяется самостоятельный раздел
- **THEN** его операции и схемы совпадают с объединённым контрактом, все ссылки разрешаются и security отражает принятую пару заголовков

#### Scenario: Repository-only contract checks

- **WHEN** генерация и проверки выполняются без файлов Downloads и соседнего MPMM
- **THEN** используются только repo-контракты, рассинхронизация разделов/generated-типов обнаруживается

#### Scenario: Mock principal belongs to the dedicated change

- **WHEN** локальный mock server получает запрос /api/control/api/auth/v1/me
- **THEN** mock principal определяется local-session-demo; бизнес-операции по-прежнему тестируются без реальных credentials и серверной ролевой модели

### Requirement: Knowledge base mock contract fidelity

Существующий Express mock SHALL предоставлять согласованные HTTP-сценарии KB: metadata с data.entries и bindings, шесть KB lookup-наборов только для соответствующего section, CRUD/search/export и managed saved-filters с resource=knowledge-base-entries. KB fixtures SHALL быть обособлены и согласованы с существующими навыками/пользователями. Сервер SHALL сохранять link IDs, порядок массива, replacement links/skill_ids, rules defaults и очистку nullable полей по CRUD-контракту. Search/sort SHALL предшествовать pagination; display names и links_count SHALL соответствовать данным. Валидация URL, references, inactive values и field errors SHALL позволять проверить ошибки UI без credentials и ролевого enforcement.

Metadata SHALL публиковать type и допустимые операторы каждого поля, включая numeric links_count и string skill_names. Поиск, CSV и сохранённый search SHALL поддерживать их по текущему контракту. Mock MUST NOT добавлять archived-переход или вложенный экспорт, отсутствующие в принятом API. DELETE SHALL скрывать запись из поиска и чтения, сохраняя занятость кода по контракту. Runtime fixtures MUST NOT попадать в production. Проверки SHALL отличать локальное подтверждение поведения от реальной backend-интеграции.

#### Scenario: Metadata and lookup ready for editor

- **WHEN** запрошены KB metadata и lookup
- **THEN** data.entries содержит bindings/condition_fields с типами и операторами/export_fields/export_max_rows, lookup содержит KB-наборы с display_name и is_active, не выдавая справочники других разделов

#### Scenario: Aggregate HTTP round trip

- **WHEN** материал создан, ссылки переставлены с прежними ID и список навыков очищен
- **THEN** последующие detail/search отражают новый порядок и пустые связи, DTO и totals проходят контрактную проверку

#### Scenario: Invalid mutation preserves data

- **WHEN** отправлен небезопасный URL, несуществующий skill_id или новый выбор inactive-кода
- **THEN** возвращается контрактная ошибка соответствующего поля без изменения сохранённого материала

#### Scenario: Unsupported operation is not simulated

- **WHEN** отправлен payload неподдержанного архива или вложенного экспорта
- **THEN** mock не возвращает фиктивный успешный результат

#### Scenario: Deleted code remains reserved

- **WHEN** материал удалён и затем создаётся другой с тем же code
- **THEN** чтение удалённого ID возвращает 404, создание получает конфликт кода

#### Scenario: Mock regression safety

- **WHEN** обновлены общие managed helpers ради KB
- **THEN** прежние тесты других ресурсов сохраняются, новые KB server-тесты входят в yarn test, production не содержит их fixtures

#### Scenario: Numeric and skill-name search

- **WHEN** links_count between [0, 2.5] объединён с skill_names contains в OR-группе
- **THEN** поиск/total/CSV применяют одну семантику до пагинации; skill_names содержит только названия связанных неудалённых навыков, сохранённый search сохраняет числа

### Requirement: A/B testing mock contract fidelity

Существующий Express mock SHALL предоставлять metadata с data.experiments и bindings, четыре section-scoped ab_* lookup-набора, CRUD/search/export и managed saved-filters с resource=ab-experiments. Изолированные fixtures SHALL ссылаться на существующие поверхности и бизнес-пользователей. Создание/PUT SHALL проверять name/code uniqueness, группы 2–100, целые проценты 0–100 и сумму 100, непустые уникальные теги, уникальные IDs, поверхности 1–100 и их существование, даты, scheduled/segment требования, inactive references и nullability. PUT SHALL сохранять пропущенные поля, заменять переданные коллекции целиком и сохранять IDs/порядок групп. Изменение тега существующей группы при сохранённом non-draft статусе SHALL давать документированный конфликт без мутации.

Search/sort SHALL предшествовать pagination и соответствовать документированным полям и семантике; summaries SHALL содержать названия поверхностей и групп. Metadata SHALL включать типы и операторы каждого поля, в том числе numeric groups_count. Поиск, сохранённые фильтры и CSV SHALL поддерживать числовые условия groups_count. CSV SHALL соответствовать общему контракту и A/B полям, именам файлов и пределу 10000. DELETE SHALL выполнять документированное мягкое удаление, без UI-кнопки удаления. Saved search SHALL проверяться до сохранения/применения. Ошибки SHALL сохранять прежнее состояние и использовать соответствующие HTTP/schema/field paths. Бизнес-запросы SHALL работать без credentials и role enforcement. Restart SHALL восстанавливать seed.

Mock MUST NOT поддерживать archived, priority/surface-условия внутри conditions, вложенный экспорт, исполнение расписания, распределение трафика, сбор метрик или автостоп вопреки контракту. Runtime fixtures MUST NOT попадать в production; проверки SHALL отличать локальное поведение от реального backend.

#### Scenario: Metadata and lookup

- **WHEN** запрошены metadata и lookup ab-testing
- **THEN** возвращены data.experiments с bindings/typed conditions/export fields/limit и только четыре A/B-набора с display_name/is_active; KB lookup остаётся независимым

#### Scenario: Aggregate round trip

- **WHEN** эксперимент создан, группы переставлены с прежними IDs и набор поверхностей заменён
- **THEN** detail/search/CSV отражают один агрегат, порядок и корректные summaries; ответы проходят контрактную схему

#### Scenario: Rejected aggregate preserves state

- **WHEN** PUT имеет сумму 99, дублирующийся тег, отсутствующую поверхность, невалидные даты или изменение тега сохранённой non-draft группы
- **THEN** возвращается соответствующая ошибка без изменения карточки, timestamps и результатов поиска

#### Scenario: Full selection export

- **WHEN** search имеет limit/offset и числовое условие groups_count, а CSV экспортируется с тем же отбором
- **THEN** поиск возвращает страницу, CSV весь отбор до документированного лимита, без вложенных таблиц и фиктивных результатов

#### Scenario: Isolation and regression

- **WHEN** обновлены A/B handlers и запускается yarn test
- **THEN** вложенные A/B HTTP-тесты выполняются, существующие KB/managed tests сохранены, разделы не импортируют предметные mocks друг друга и production не содержит fixtures

## ADDED Requirements

### Requirement: Current managed-resource operation coverage

Mock SHALL обслуживать все текущие managed-resource операции, включая восемь операций API registry и восемь response templates, без общего 501 или отсутствующих handlers. Для новых ресурсов SHALL предоставляться CRUD, metadata с ключами endpoints и response-templates, search и CSV списка/карточки. Девять новых системных справочников SHALL читаться через section-scoped lookups и центральный реестр значений/экспорт; изменение их значений SHALL запрещаться. Сохранённые фильтры SHALL принимать api-endpoints и response-templates по live enum, проверяя и сохраняя полный search соответствующего ресурса. Несовпадение Markdown SHALL документироваться без заявления о проверенном deployment. Общие envelope, ошибки полей, пагинация, частичный PUT, мягкое удаление, inactive references и CSV ограничения SHALL сохраняться по актуальным источникам.

API endpoint SHALL проверять обязательность source_code для incoming/outgoing, валидность JSON-текста с сохранением форматирования, уникальность имени/кода/(method,path,version), параметры и ответы. PUT коллекций SHALL заменять их атомарно, сохранять переданные ID и порядок, генерировать ID новых строк. Описанные запросы MUST NOT исполняться.

Response template SHALL проверять обязательные type_code/scope_code/text, непустое имя/текст, уникальность имени/кода, существование и уникальность skill_ids/surface_ids. PUT SHALL заменять только переданные наборы связей; scope_code MUST NOT искусственно ограничивать связи. Активность SHALL определяться status, плейсхолдеры SHALL храниться без подстановки. Недокументированные проверки внешнего ответственного MUST NOT выводиться из поведения поверхностей.

#### Scenario: New API aggregate round trip

- **WHEN** эндпоинт создан, его параметры переставлены с прежними ID, responses очищены, затем выполнены GET/search/export
- **THEN** ответы согласованы, сохранены JSON-текст и порядок, очищена только переданная коллекция; запрос к описанному base_url не выполняется

#### Scenario: New resource validation is atomic

- **WHEN** отправлен incoming без source_code, повтор method/path/version либо шаблон с отсутствующим skill_id
- **THEN** возвращается ошибка без изменения карточки и вложенных коллекций

#### Scenario: Saved filters accept current enum

- **WHEN** сохранён и применён фильтр api-endpoints или response-templates
- **THEN** resource и полный search проходят соответствующую схему, чтение/PUT/delete работают по общему контракту; ошибочный search не сохраняется

#### Scenario: Section lookups and system values

- **WHEN** запрошены lookups/api и lookups/response-templates и предпринята запись системного значения
- **THEN** возвращаются соответственно шесть api_* и три tpl_* набора, запись отклоняется, чужие справочники не смешиваются

#### Scenario: Missing handler remains an error

- **WHEN** операция снимка не имеет handler или осталась привязана к старому operationId экспорта
- **THEN** запуск/проверка покрытия завершается ошибкой, общий fallback не скрывает пропуск

### Requirement: Numeric conditions preserve typed semantics

Mock SHALL валидировать field/operator/value совместно по metadata, не разрешая все операторы на всех полях только из-за общего enum. Numeric eq/ne/gt/gte/lt/lte/between SHALL сравнивать конечные числа без строкового преобразования и исключать NULL. between SHALL включать обе границы; пустая группа SHALL не ограничивать отбор при любой логике. Ошибки search, export и saved-filter search SHALL иметь соответствующий вложенный путь и не менять данные.

#### Scenario: Numeric edge cases

- **WHEN** переданы ноль, дробный порог, равные границы, обратный диапазон, boolean или строка вместо числа
- **THEN** первые три значения принимаются, остальные отклоняются; numeric ne не включает записи с NULL

#### Scenario: Metadata cannot enable invalid combinations

- **WHEN** gt применён к name либо contains к groups_count
- **THEN** mock отклоняет сочетание, а metadata не предлагает такой оператор

### Requirement: Surface mock follows current responsible and creation contracts

Mock SHALL хранить назначения по ID бизнес-пользователей и выдавать responsible как объекты id/full_name/email. При отсутствии сведений о ранее назначенном пользователе SHALL сохраняться ID с nullable сведениями, а не вымышленное имя. До создания SHALL проверяться занятость всех доменов, существование обоих пользователей и переданная конфигурация. Любая ошибка SHALL оставлять коллекцию поверхностей и связи команд неизменными; параллельные попытки занять один домен MUST NOT обе завершаться созданием. configuration absent/null SHALL использовать прежние defaults. Переданная конфигурация SHALL сохраняться без второго запроса.

Локальные embed_code/authorization SHALL быть согласованными демонстрационными серверными значениями без реальных credentials; клиент MUST NOT генерировать их или исполнять embed script. Неописанные wire-форматы ошибок SHALL явно маркироваться mock convention до подтверждения backend-примером, без изменения published OpenAPI.

#### Scenario: Domain or user conflict preserves state

- **WHEN** хотя бы один домен занят либо один ответственный отсутствует
- **THEN** создание отклоняется с диагностикой домена или назначения, поверхность и связь команды не появляются

#### Scenario: Atomic configuration

- **WHEN** передана валидная конфигурация либо невалидная конфигурация
- **THEN** первая читается после создания, вторая не оставляет поверхности; absent/null сохраняют defaults

#### Scenario: Existing missing user

- **WHEN** ранее назначенный пользователь отсутствует в текущем локальном справочнике
- **THEN** чтение сохраняет его ID с full_name=null/email=null, новое назначение этого ID отклоняется

#### Scenario: Concurrent domain creation

- **WHEN** две попытки создания используют один занятый ими домен
- **THEN** создаётся не более одной поверхности, другая попытка получает подтверждённый конфликт
