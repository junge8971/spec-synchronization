## ADDED Requirements

### Requirement: System-state managed resource mock fidelity

Существующий Express mock SHALL обслуживать опубликованные system-state metadata, summary, search, create, detail, PUT, delete, list/detail CSV и section-scoped lookups, заменяя адресные unavailable handlers. Он SHALL возвращать согласованные DTO, серверные счётчики обоих видов по неудалённым записям, metadata, фильтрацию и сортировку до пагинации. Create SHALL выдавать custom/enabled/noncritical запись; предопределённым записям SHALL разрешаться только изменение состояния, пользовательские SHALL поддерживать согласованную редакцию и мягкое удаление. Код SHALL проверяться глобально между видами. Валидные изменения SHALL отражаться в последующих detail/search/summary/export; ошибки MUST NOT менять состояние.

Saved-filters SHALL принимать `resource=system-state-toggles` и валидировать полный сохранённый search. Повторное сохранение одного имени для фиксированного локального mock-владельца SHALL обновлять отбор с прежним ID, не меняя поведение фильтров других ресурсов. Моки SHALL оставаться credential-free без вычисления permissions, ролевого enforcement или реальной изоляции пользователей; фиксированный mock-владелец не является подтверждённым principal. Фикстуры и handlers MUST NOT входить в production, а другие непокрытые операции SHALL сохранять честный unavailable.

#### Scenario: Toggle and search round trip

- **WHEN** разрешённая предопределённая запись переключается через валидный PUT, затем читаются detail, search, summary и CSV
- **THEN** все ответы согласованы по состоянию и счётчикам, проходят контракт и не требуют credentials

#### Scenario: Invalid edit is atomic

- **WHEN** изменяются реквизиты предопределённой записи, удаляется такая запись или создаётся конфликтующий код
- **THEN** mock возвращает обозначенную ошибку без изменения исходных данных или сводки

#### Scenario: Saved-filter name is reused

- **WHEN** для фиксированного mock-владельца дважды сохранён system-state отбор с одинаковым именем и разными валидными параметрами
- **THEN** второй ответ относится к тому же ID, повторное чтение возвращает новый search, и это не означает реализованной backend-авторизации

#### Scenario: Restart and unrelated operations

- **WHEN** после изменений создаётся новый экземпляр mock server или вызывается другая неподключённая операция
- **THEN** system-state возвращается к своему seed, не связанная операция сохраняет свой прежний unavailable, а production не получает mock-файлы
