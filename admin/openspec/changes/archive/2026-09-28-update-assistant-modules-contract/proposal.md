## Why

Свежая выгрузка OpenAPI (`/home/user/Загрузки/message (2).txt`) добавляет управление модулями ассистента: пять операций и 22 схемы без изменений существующих контрактов. Проект должен синхронно обновить источник, типы и локальный mock server: простая замена JSON нарушит запуск сервера, требующего обработчик каждой бизнес-операции.

## What Changes

- Обновить полный OpenAPI до 33 операций и 115 схем, сохранив исходные paths, security и DTO.
- Добавить самостоятельный OpenAPI раздела Assistant modules и его Markdown-описание, обновить индекс контрактов (5 заполненных разделов из 11).
- Перегенерировать `app/shared/api/schema.d.ts` существующей командой `yarn api:generate`.
- Расширить mock API с 27 до 32 бизнес-операций: список модулей, summary, preview, enable и disable; сохранить единственное исключение Access `/me`.
- Добавить согласованное in-memory состояние модулей, проверку версии и ограничений отключения, контрактные и негативные server-тесты, документацию mock-конвенций.
- Исправить обнаруженную в общем mock sort ошибку descending-полей и добавить регрессионные тесты; расширение согласовано пользователем при реализации.
- Не менять UI, runtime API-клиенты, авторизацию или dev/prod lifecycle.

## Capabilities

### New Capabilities

Нет.

### Modified Capabilities

- `control-center-mock-server`: расширить полное покрытие поставленного контракта до 32 бизнес-операций и определить согласованное mock-поведение модулей.

## Impact

- `docs/api/contracts/openapi.json`, `README.md`, `assistant-modules.md`, новый `assistant-modules.openapi.json`.
- Generated `app/shared/api/schema.d.ts`; генератор остаётся существующим.
- `mocks/app.mjs`, `seed.json`, обработчики нового раздела, server-тесты и `mocks/README.md`; переиспользование `contract.mjs`, `list.mjs`, `state.mjs`.
- Новых зависимостей и backend endpoint-изменений нет. Уточнения, которых нет в OpenAPI (ошибки конфликтов, переходы и preview), документируются только как локальные mock-конвенции.
