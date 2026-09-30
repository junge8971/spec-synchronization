## Why

MOS-1022: подключение уже читается из API, но его нельзя редактировать. Требуется настроить реализацию навыка и определения параметров для конфигуратора поверхности без жёсткой привязки к kb_section.

## What Changes

- Отдельная форма connection: endpoint, contract_version, auth_required, auth_type и parameters.
- Только контрактный type=select: key, title, required, options, default; сохранить различие string/integer/null для default.
- PATCH с expected_version и Idempotency-Key, отмена и сохранение ввода при ошибке.
- Исправить смысл connection=null: настройка не задана, а не «API не поддерживает подключение».
- Ссылка на существующую статью skill-params; без редактирования секрета токена и без реализации нового конфигуратора поверхности.

## Capabilities

### New Capabilities

- `skill-connection-settings`: редактирование подключения и определений параметров навыка.

### Modified Capabilities

Нет. Дополняет существующее чтение DTO.

## Impact

- `app/widgets/skill-details/ui/tabs/connection-tab.tsx`, `app/entities/skill/`, предметная feature формы.
- `docs/api/contracts/openapi.json`: существующий UpdateSkillRequest.connection и SkillConnectionSchema. Нельзя добавлять неподдержанные типы параметров.
- Рекомендуется после MOS-944 для переиспользования PATCH в entities; формы не импортируют друг друга.
- Согласована полная замена connection: frontend проверяет типы по OpenAPI, бизнес-ограничения проверяет backend; ошибки сохраняют ввод. Удаление всего connection через null не добавляется. Новые библиотеки не нужны.
