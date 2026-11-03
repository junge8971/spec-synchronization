## MODIFIED Requirements

### Requirement: Explicit unavailable coverage for imported managed resources

Для 43 новых managed-resource операций этой выгрузки, пока не реализованных отдельными changes, локальный mock API SHALL явно возвращать HTTP 501 с сообщением о недоступности реализации после штатной валидации запроса. Принятые в add-optional-knowledge-base операции KB, её lookup и используемые managed saved-filters SHALL обслуживаться по требованию Knowledge base mock contract fidelity ниже и MUST NOT возвращать общий 501. Прочие отдельно принятые реализации SHALL сохраняться; это изменение MUST NOT откатывать существующий managed CRUD к 501. Ответ 501 для оставшихся нереализованных операций SHALL документироваться как mock convention и MUST NOT добавляться в backend OpenAPI как подтверждённый ответ сервера. Нереализованные операции MUST NOT возвращать успешные вымышленные CRUD-данные. Исключение SHALL ограничиваться явным перечнем method/path этой поставки; отсутствие handler любой другой операции MUST оставаться ошибкой полноты покрытия. Уже принятые handlers и особое поведение `/me` SHALL сохраняться.

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

### Requirement: Knowledge base mock contract fidelity

Существующий Express mock SHALL предоставлять согласованные HTTP-сценарии KB: metadata с `data.entries` и bindings, шесть KB lookup-наборов только для соответствующего section, CRUD/search/export и managed saved-filters с resource=knowledge-base-entries. KB fixtures SHALL быть обособлены и согласованы с существующими навыками/пользователями. Сервер SHALL сохранять link IDs, порядок массива, replacement links/skill_ids, rules defaults и очистку nullable полей по CRUD-контракту. Search/sort SHALL предшествовать pagination; display names и links_count SHALL соответствовать данным. Валидация URL, references, inactive values и field errors SHALL позволять проверить ошибки UI без credentials и ролевого enforcement.

Mock MUST NOT добавлять поддержку archived-перехода, числовых KB conditions или вложенного экспорта, отсутствующих в принятом API. DELETE SHALL скрывать запись из поиска и чтения, сохраняя занятость кода по контракту. Runtime fixtures MUST NOT попадать в production. Проверки SHALL отличать локальное подтверждение поведения от реальной backend-интеграции.

#### Scenario: Metadata and lookup ready for editor

- **WHEN** запрошены KB metadata и lookup
- **THEN** data.entries содержит bindings/condition_fields/export_fields/export_max_rows, lookup содержит KB-наборы с display_name и is_active, не выдавая все справочники других разделов

#### Scenario: Aggregate HTTP round trip

- **WHEN** материал создан, ссылки переставлены с прежними ID и список навыков очищен
- **THEN** последующие detail/search отражают новый порядок и пустые связи, DTO и totals проходят контрактную проверку

#### Scenario: Invalid mutation preserves data

- **WHEN** отправлен небезопасный URL, несуществующий skill_id или новый выбор inactive-кода
- **THEN** возвращается контрактная ошибка соответствующего поля без изменения сохранённого материала

#### Scenario: Unsupported operation is not simulated

- **WHEN** UI работает с локальным API и отображает архив/числовые условия/вложенный экспорт
- **THEN** моки не делают эти функции доступными вопреки контракту; неподдержанные payload не получают фиктивного успешного результата

#### Scenario: Deleted code remains reserved

- **WHEN** материал удалён и затем создаётся другой с тем же code
- **THEN** чтение удалённого ID возвращает 404, создание получает конфликт кода

#### Scenario: Mock regression safety

- **WHEN** обновлены общие managed helpers ради KB
- **THEN** прежние тесты других ресурсов сохраняются, новые KB server-тесты действительно входят в yarn test, production не содержит их fixtures
