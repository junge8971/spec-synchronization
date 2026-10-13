## Why

Новая backend-выгрузка `newcontract.json` добавляет PUT-алиасы существующих мутаций и CRUD managed resources. Текущие клиенты навыков и доменов используют PATCH, который, по сообщению backend-команды, блокируется WAF на тестовых контурах. Простая замена общего OpenAPI также потеряет принятое дополнение экспорта диалогов и нарушит ссылки на тип сохранённых фильтров.

## What Changes

- Обновить объединённый OpenAPI и секционные JSON из новой выгрузки, сохранить два метода и четыре схемы дополнения экспорта диалогов, а также действующую нормализацию security AND.
- Добавить в документацию и generated DTO контракты feedback, catalogs, knowledge-base, ab-testing и общих saved filters. Сохранить скачанное CRUD-описание в проекте с источником и контрольной суммой.
- Перевести существующие клиентские изменения навыков и доменов на PUT; адаптировать потребителя переименованного DTO saved filters диалогов.
- Добавить четыре PUT-алиаса в существующие Express-моки, сохранив PATCH и бизнес-семантику. Для новых managed-resource операций явно обозначить отсутствие реализации без успешных фиктивных ответов и без отключения проверки полноты существующих handlers.
- Согласовать источники и упоминания PATCH в затронутых feedback changes с новой выгрузкой. Их продуктовый scope и состояние выполнения не менять.

Новые CRUD-экраны, бизнес-клиенты и полноценные CRUD-моки не входят. Они остаются отдельными поставками; feedback API принадлежит `mos-1249-feedback-api`. Auth/session/permissions, Jira, зависимости и backend не меняются.

## Capabilities

### New Capabilities

Нет.

### Modified Capabilities

- `control-center-http`: воспроизводимый обновлённый контракт с принятыми дополнениями и PUT для существующих редакторов.
- `skill-card-editing`: сохранение анкеты через PUT с прежней защитой ввода.
- `skill-connection-settings`: независимое сохранение полного connection через PUT.
- `skill-domain-management`: версионное редактирование домена через PUT.
- `control-center-mock-server`: эквивалентные PUT/PATCH handlers и явная недоступность новых managed-resource операций без ослабления покрытия прежних API.

## Impact

`docs/api/contracts/`, `app/shared/api/schema.d.ts`, клиенты `entities/skill` и `entities/skill-domain`, тип saved filters в `features/dialog-saved-filters`, `mocks/` и связанные unit/component/server-тесты. Генератор `scripts/generate-api-types.mjs` остаётся штатным источником DTO.

При реализации согласовать planning artifacts `mos-1249-feedback-api`, `mos-1251-feedback-editor`, `mos-1254-feedback-questions`, `mos-1256-feedback-lifecycle`, `mos-1259-feedback-saved-filters`; при необходимости исправить ссылки других feedback changes только на эти же источники. Архивные документы не переписывать.

Проверки реализации: typecheck, lint без предупреждений, test, format:check, api:check и build для сохранения production isolation моков. E2E/browser-тесты не входят. Выгрузка и локальные проверки не подтверждают работоспособность deployment или снятие WAF-блокировки.
