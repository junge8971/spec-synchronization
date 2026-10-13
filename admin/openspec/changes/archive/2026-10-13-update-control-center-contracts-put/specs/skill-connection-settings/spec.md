## MODIFIED Requirements

### Requirement: Independent connection save

Сохранение SHALL использовать PUT навыка с полным connection, expected_version и Idempotency-Key, не перезаписывая поля анкеты. Объект connection SHALL заменяться целиком, а не merge-иться. Удаление всего подключения через connection=null MUST NOT предлагаться в этой форме. Успех SHALL отображать серверный результат; отмена MUST NOT отправлять мутацию; ошибка SHALL сохранять ввод. Конфликт версии MUST NOT автоматически перезаписывать чужое изменение.

#### Scenario: Connection save

- **WHEN** сервер принимает валидную настройку
- **THEN** повторное открытие карточки показывает сохранённое подключение, а поля анкеты не изменены этой операцией

#### Scenario: Preserve optional fields during replacement

- **WHEN** пользователь меняет адрес сервиса, не меняя определения параметров
- **THEN** полный connection содержит прежние параметры с сохранением отсутствующих optional полей, пустых списков и типов default, включая null, строку и integer 0

#### Scenario: Save fails

- **WHEN** сервер отклоняет PUT
- **THEN** настройка остаётся в форме с доступным сообщением об ошибке без фиктивного успеха
