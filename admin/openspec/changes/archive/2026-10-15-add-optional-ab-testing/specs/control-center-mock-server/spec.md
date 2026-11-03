## MODIFIED Requirements

### Requirement: Explicit unavailable coverage for imported managed resources

Для 43 новых managed-resource операций этой выгрузки, пока не реализованных отдельными changes, локальный mock API SHALL явно возвращать HTTP 501 с сообщением о недоступности реализации после штатной валидации запроса. Принятые в add-optional-knowledge-base операции KB, её lookup и используемые managed saved-filters SHALL обслуживаться по требованию Knowledge base mock contract fidelity и MUST NOT возвращать общий 501. Принятые в add-optional-ab-testing восемь A/B-операций, lookup ab-testing и managed saved-filters с resource=ab-experiments SHALL обслуживаться по требованию A/B testing mock contract fidelity ниже и MUST NOT возвращать общий 501. Прочие отдельно принятые реализации SHALL сохраняться; это изменение MUST NOT откатывать существующий managed CRUD к 501. Ответ 501 для оставшихся нереализованных операций SHALL документироваться как mock convention и MUST NOT добавляться в backend OpenAPI как подтверждённый ответ сервера. Нереализованные операции MUST NOT возвращать успешные вымышленные CRUD-данные. Исключение SHALL ограничиваться явным перечнем method/path этой поставки; отсутствие handler любой другой операции MUST оставаться ошибкой полноты покрытия. Уже принятые handlers и особое поведение `/me` SHALL сохраняться.

#### Scenario: Imported CRUD operation is not implemented

- **WHEN** валидный запрос вызывает одну из явно перечисленных новых CRUD-операций без отдельно принятой реализации со штатным demo-сценарием
- **THEN** локальный сервер отвечает 501 без изменения состояния; сервер запускается, существующие API продолжают работать

#### Scenario: Invalid imported CRUD request

- **WHEN** запрос новой CRUD-операции нарушает опубликованную схему
- **THEN** запрос отклоняется штатной контрактной валидацией, а не превращается в успешный fixture

#### Scenario: Lost handler is not hidden

- **WHEN** у прежней поддержанной операции или новой операции вне явного перечня отсутствует handler
- **THEN** проверка покрытия или запуск mock API завершается ошибкой; общий fallback не скрывает пропуск

#### Scenario: New contract keeps local demo and production isolation

- **WHEN** загружается каталог demo-сценариев либо собирается production-приложение
- **THEN** PUT и явно недоступные операции корректно представлены в локальном каталоге, прежние 403/500/delay сценарии сохраняются, production не содержит mock handlers или fixtures

## ADDED Requirements

### Requirement: A/B testing mock contract fidelity

Существующий Express mock SHALL предоставлять metadata с data.experiments и bindings, четыре section-scoped ab_* lookup-набора, CRUD/search/export и managed saved-filters с resource=ab-experiments. Изолированные fixtures SHALL ссылаться на существующие поверхности и бизнес-пользователей. Создание/PUT SHALL проверять name/code uniqueness, группы 2–100, целые проценты 0–100 и сумму 100, непустые уникальные теги, уникальные IDs, поверхности 1–100 и их существование, даты, scheduled/segment требования, inactive references и nullability. PUT SHALL сохранять пропущенные поля, заменять переданные коллекции целиком и сохранять IDs/порядок групп. Изменение тега существующей группы при сохранённом non-draft статусе SHALL давать документированный конфликт без мутации.

Search/sort SHALL предшествовать pagination и соответствовать документированным полям и семантике; summaries SHALL содержать названия поверхностей и групп. CSV SHALL соответствовать общему контракту и A/B полям, именам файлов и пределу 10000. DELETE SHALL выполнять документированное мягкое удаление, без UI-кнопки удаления. Saved search SHALL проверяться до сохранения/применения. Ошибки SHALL сохранять прежнее состояние и использовать соответствующие HTTP/schema/field paths. Бизнес-запросы SHALL работать без credentials и role enforcement. Restart SHALL восстанавливать seed.

Mock MUST NOT поддерживать archived, числовые условия и surface-условия внутри conditions, вложенный экспорт, исполнение расписания, распределение трафика, сбор метрик или автостоп вопреки контракту. Runtime fixtures MUST NOT попадать в production; проверки SHALL отличать локальное поведение от реального backend.

#### Scenario: Metadata and lookup

- **WHEN** запрошены metadata и lookup ab-testing
- **THEN** возвращены data.experiments с bindings/conditions/export fields/limit и только четыре A/B-набора с display_name/is_active; KB lookup остаётся прежним

#### Scenario: Aggregate round trip

- **WHEN** эксперимент создан, группы переставлены с прежними IDs и набор поверхностей заменён
- **THEN** detail/search/CSV отражают один агрегат, порядок и корректные summaries; ответы проходят контрактную схему

#### Scenario: Rejected aggregate preserves state

- **WHEN** PUT имеет сумму 99, дублирующийся тег, отсутствующую поверхность, невалидные даты или изменение тега сохранённой non-draft группы
- **THEN** возвращается соответствующая ошибка без изменения карточки, timestamps и результатов поиска

#### Scenario: Full selection export

- **WHEN** search имеет limit/offset и CSV экспортируется с тем же отбором
- **THEN** поиск возвращает страницу, CSV весь отбор до документированного лимита, без вложенных таблиц и фиктивных результатов

#### Scenario: Isolation and regression

- **WHEN** добавлены A/B handlers и запускается yarn test
- **THEN** вложенные A/B HTTP-тесты выполняются, существующие KB/managed tests сохранены, разделы не импортируют предметные mocks друг друга и production не содержит fixtures
