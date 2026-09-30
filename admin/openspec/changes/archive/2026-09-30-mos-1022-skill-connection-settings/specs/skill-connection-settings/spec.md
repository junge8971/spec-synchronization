## Purpose

Обеспечить безопасное редактирование подключения реализации навыка и определений параметров, используемых конфигуратором поверхности.

## ADDED Requirements

### Requirement: Connection configuration

Вкладка SHALL показывать и позволять редактировать endpoint, contract_version, auth_required и auth_type по контракту. Null connection SHALL обозначать отсутствие настройки, а не отсутствие поддержки API. Секрет транспортного токена MUST NOT приниматься как текст анкеты или connection.

#### Scenario: Configure absent connection

- **WHEN** сервер вернул connection=null
- **THEN** показано «Подключение не настроено» и доступен вход в форму настройки

### Requirement: Contract-compatible parameter definitions

Редактор SHALL поддерживать список параметров с key, title, type=select, required, options и default. Другие типы MUST NOT добавляться без изменения согласованного контракта. Frontend SHALL проверять типы по OpenAPI и точность integer в JavaScript; дополнительные бизнес-ограничения key/options, default/options и auth_required/auth_type проверяет backend, без произвольных ограничений frontend. UI SHALL сохранять контрактный тип default (string/integer/null), включая 0, и MUST NOT ограничивать ключи одним kb_section.

#### Scenario: Multiple parameter keys

- **WHEN** навык содержит два select-параметра с разными ключами
- **THEN** оба отображаются и редактируются независимо, без специального поведения только для kb_section

#### Scenario: Integer zero default

- **WHEN** пользователь редактирует параметр с default=0, не меняя default
- **THEN** сохранённое значение остаётся integer 0, а не строкой, null или отсутствующим полем

### Requirement: Independent connection save

Сохранение SHALL использовать PATCH навыка с полным connection, expected_version и Idempotency-Key, не перезаписывая поля анкеты. Объект connection SHALL заменяться целиком, а не merge-иться. Удаление всего подключения через connection=null MUST NOT предлагаться в этой форме. Успех SHALL отображать серверный результат; отмена MUST NOT отправлять мутацию; ошибка SHALL сохранять ввод. Конфликт версии MUST NOT автоматически перезаписывать чужое изменение.

#### Scenario: Connection save

- **WHEN** сервер принимает валидную настройку
- **THEN** повторное открытие карточки показывает сохранённое подключение, а поля анкеты не изменены этой операцией

#### Scenario: Preserve optional fields during replacement

- **WHEN** пользователь меняет адрес сервиса, не меняя определения параметров
- **THEN** полный connection содержит прежние параметры с сохранением отсутствующих optional полей, пустых списков и типов default, включая null, строку и integer 0

#### Scenario: Save fails

- **WHEN** сервер отклоняет PATCH
- **THEN** настройка остаётся в форме с доступным сообщением об ошибке без фиктивного успеха

### Requirement: Parameter documentation

Кнопка документации SHALL открывать существующую статью skill-params с сохранением deployment basename.

#### Scenario: Open documentation

- **WHEN** пользователь выбирает документацию параметров
- **THEN** открывается `/docs?article=skill-params` под basename приложения, а не несуществующая статья
