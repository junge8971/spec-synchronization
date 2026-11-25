## Why

MOS-944: завершить обзор и редактирование карточки навыка. Чтение анкеты уже работает, фиктивные «Отклонён» и этап «Проверка» уже удалены; недостающая ценность — сохранение изменений через существующий API.

## What Changes

- Сохранить отображение service_id, name, purpose, expected_result, description, type, domain, zones, team, contact, limitations, comments, related_materials и дат.
- Добавить отдельную форму анкеты с отменой, валидацией и PATCH; обновлять карточку, крошки и реестр после успеха.
- Сохранить ввод при ошибке и исключить молчаливую перезапись при конфликте версии.
- Не включать создание навыка, подключение (MOS-1022), lifecycle и аналитику.

## Capabilities

### New Capabilities

- `skill-card-editing`: редактирование анкеты существующего навыка.

### Modified Capabilities

Нет. Дополняет truthful representation из `control-center-api-integration`, не возвращает неподдержанные статусы.

## Impact

- `app/widgets/skill-details/`, `app/entities/skill/`, новая предметная feature формы; существующие справочники доменов/команд и Query cache.
- Источник истины: `docs/api/contracts/openapi.json`; GET/PATCH `/api/control/api/skills/v1/skills/{skill_id}`, `UpdateSkillRequest`, обязательные expected_version и Idempotency-Key.
- API имеется; до полной приёмки нужно согласовать источник выбора contact_user_id, семантику null и ответ при конфликте версии. Mock-конвенции не являются backend-контрактом.
- Самостоятельная приёмка MOS-944; рекомендуемый первый change. Новые библиотеки не требуются.
