## Purpose

Подключить API опросников, справочных значений и метаданных в разделе обратной связи ЦАМ по опубликованному API, с отдельной приёмкой и сохранением ограничений первого этапа.

## ADDED Requirements

### Requirement: Contract aligned feedback operations

Раздел SHALL использовать `/api/control/api/v1/managed-resources`: CRUD `/feedback/surveys`, POST `/feedback/surveys/search`, lookup `/catalogs/lookups/feedback`, metadata `/feedback/metadata`; клиенты saved-filters и CSV добавляются отдельными changes на том же transport. JSON-ответы SHALL проверяться с сохранением HTTP status, code, message и всех errors, включая вложенные JSON Pointer. После создания SHALL выполняться GET по data.id; PUT SHALL возвращать новый baseline полной карточки. Системные поля, sort_order, FK и локальные ключи MUST NOT отправляться. Чтение SHALL поддерживать отмену; мутации MUST NOT автоматически повторяться.

#### Scenario: Created survey receives server identifiers

- **WHEN** POST опросника вернул 201 и data.id
- **THEN** отдельный GET получает сохранённую карточку и ID её вопросов/вариантов; повторный POST ради получения detail не выполняется

#### Scenario: Validation and inactive references

- **WHEN** сохранение вернуло 409 NOT_UNIQUE/REFERENCE_NOT_FOUND/REFERENCE_INACTIVE либо 422 с несколькими вложенными ошибками
- **THEN** клиент сохраняет status/code/message и все JSON Pointer для потребителя; ошибочный ответ не превращается в успех, а отображение и сохранение draft проверяются в MOS-1251/MOS-1254

#### Scenario: Unknown mutation outcome

- **WHEN** ответ мутации потерян или устарел относительно текущей сессии
- **THEN** UI не объявляет гарантированный успех/отмену и не повторяет мутацию автоматически; актуальное состояние можно перечитать явным действием

### Requirement: Published feature permissions

Раздел SHALL использовать существующую общую сессию и UI-only policy. Чтение раздела/lookup/metadata/сохранённых фильтров SHALL требовать `TSAM.ManagedResource:read`; создание, изменение, удаление и CSV SHALL дополнительно требовать соответственно `TSAM.ManagedResource:create/update/delete/export`. Изменение статуса SHALL использовать update. Эти же действия применяются к персональным фильтрам. Сопоставление точного action/resource/`*`, отказ прямого URL, скрытие недоступных действий и owner/generation isolation SHALL сохранять `control-center-permissions` и `mpmm-session`. Backend SHALL определять глобальный scope и владельца фильтра; клиент MUST NOT вводить request ACL или grants по имени роли.

#### Scenario: Read only user

- **WHEN** подтверждённый principal имеет только ManagedResource:read
- **THEN** общая policy разрешает read и запрещает create/update/delete/export; каждый UI change отдельно проверяет применение этой policy к своим элементам

#### Scenario: Server scope denial

- **WHEN** сервер вернул 403 при наличии функционального права
- **THEN** UI показывает отказ, не пытается расширить scope и не заменяет ответ локальными данными
