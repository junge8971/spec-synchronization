# skill-card-editing Specification

## Purpose

Обеспечить просмотр и безопасное редактирование анкеты существующего навыка с серверным сохранением и защитой пользовательского ввода.

## Requirements

### Requirement: Skill questionnaire overview

Карточка SHALL показывать service_id, name, purpose, expected_result, description, type, domain, zones, team, contact, limitations, comments, related_materials, integer version и даты из ответа. Отсутствующие nullable значения SHALL обозначаться как незаданные; неподдержанные lifecycle статусы MUST NOT синтезироваться. Ссылки материалов MUST NOT исполнять произвольный код.

#### Scenario: Nullable questionnaire fields

- **WHEN** карточка содержит null service_id/description и пустой related_materials
- **THEN** обзор показывает незаданные значения без ошибки, вымышленного статуса или фиктивных ссылок

### Requirement: Separate questionnaire editing

Пользователь SHALL редактировать анкету в отдельной форме с сохранением и отменой. Даты и version SHALL оставаться серверными read-only данными. Изменения анкеты MUST NOT перезаписывать connection. Выбор связей SHALL использовать согласованные серверные ID и справочники; интерфейс MUST NOT самовольно ограничивать contact_user_id участниками команды.

#### Scenario: Save questionnaire

- **WHEN** пользователь сохраняет валидные изменения
- **THEN** отправляется PATCH навыка с expected_version и Idempotency-Key, а после подтверждённого успеха карточка, крошки и реестр отражают серверный результат

#### Scenario: Cancel editing

- **WHEN** пользователь меняет анкету и отменяет редактирование
- **THEN** мутация не отправляется и показаны последние сохранённые данные

### Requirement: Safe mutation lifecycle

Форма SHALL предотвращать повторную отправку во время сохранения, показывать ошибки в доступном виде и сохранять введённые данные при ошибке. Повтор той же логической операции SHALL сохранять Idempotency-Key; изменённое тело SHALL иметь новый ключ. Конфликт версии MUST NOT приводить к автоматической перезаписи новой версии. Фоновое чтение MUST NOT молча стирать dirty-ввод.

#### Scenario: Validation failure

- **WHEN** сервер отклоняет изменения с ошибкой валидации
- **THEN** форма остаётся с введёнными значениями и понятной ошибкой, сообщение об успехе отсутствует

#### Scenario: Concurrent update

- **WHEN** сервер сообщает конфликт исходной версии
- **THEN** пользователь видит необходимость обновить данные, draft сохранён и PATCH с новой expected_version автоматически не выполняется

#### Scenario: Keyboard editing

- **WHEN** пользователь работает с формой клавиатурой
- **THEN** поля имеют подписи, ошибки связаны с полями, сохранение и отмена доступны, после закрытия фокус возвращается к действию открытия
