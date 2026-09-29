## 1. Уточнения connection API

- [ ] 1.1 Зафиксировать merge/replace и очистку connection, совместимость auth_required/auth_type, ограничения key/options и default string/integer/null; проверка: design содержит принятые правила и примеры, не выведенные из mock-конвенций.
- [ ] 1.2 Переиспользовать PATCH из MOS-944 либо добавить его в entities/skill без дублирования, сохраняя expected_version/Idempotency-Key; проверка: API-тест тела только connection и версии, ошибки и ответа.

## 2. Форма подключения

- [ ] 2.1 Исправить null-state и добавить отдельную форму endpoint/contract_version/auth_required/auth_type; проверка: component-тест настройки connection=null без поля для секрета.
- [ ] 2.2 Добавить редактор списка select-параметров key/title/required/options/default по принятым ограничениям; проверка: тест нескольких ключей, отсутствующих optional полей, default=0 и строкового/null default без изменения типа.
- [ ] 2.3 Реализовать отмену, pending, сохранение draft при ошибке/конфликте и обновление detail; проверка: component-тест успешного повторного чтения и ошибки без перезаписи анкеты.
- [ ] 2.4 Добавить ссылку на skill-params и проверить отсутствие kb_section-only поведения; проверка: component-тест href под basename и отображения произвольных параметров.

## 3. Самостоятельная приёмка MOS-1022

- [ ] 3.1 Проверить spec unit/component-тестами, включая клавиатуру/подписи/ошибки и границу integer default; при изменении mock добавить HTTP server-тест; проверка: согласованные сценарии проходят независимо от остальных вкладок. E2E/browser не выполнять.
- [ ] 3.2 Запустить yarn typecheck, yarn lint без предупреждений, yarn test, yarn format:check; при изменении API-типов yarn api:check, сборки — yarn build; проверка: результаты сохранены, diff не содержит новых parameter types и секретов.
