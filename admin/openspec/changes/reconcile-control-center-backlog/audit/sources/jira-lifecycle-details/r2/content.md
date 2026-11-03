# MOS-1119 — selected documentary extraction

Source: https://task.mos-team.ru/browse/MOS-1119
Retrieved: 2026-10-19T07:06:01.008Z
Updated: 2026-10-16T19:22:39.728+0800
Summary: [B] Хранение статусов и истории переходов навыка
Status: Ready for test

This is a selected extraction, not the original JSON or complete issue. Parent read selected fields using same-origin GET `/rest/api/2/issue/MOS-1119?fields=summary,description,status,updated,subtasks,attachment,comment` on verified task.mos-team.ru page 5. Historical r1 timeout is preserved. No linked MR or external issue was opened. No application tests or business operations were executed.

## Description — opening (verbatim)

Добавить хранение справочника статусов навыка, разрешённых переходов и неизменяемой истории фактически выполненных переходов.

## Description — skill_statuses (normalized table)

| Field | Type | Constraints | Description |
| --- | --- | --- | --- |
| code | varchar(32) | Primary key | Стабильный системный код статуса: draft, review, prod |
| display_name | varchar(100) | NOT NULL | Отображаемое название статуса |
| sort_order | smallint | NOT NULL, UNIQUE | Порядок отображения статусов |
| is_active | boolean | NOT NULL, default true | Доступен ли статус для использования |
| created_at | timestamptz | NOT NULL, default now() | Дата создания записи |
| updated_at | timestamptz | NOT NULL, default now() | Дата последнего изменения |

Initial rows: draft / Черновик / 10; checking / Проверка / 20; training / Обучение модели / 30; autotest / Автотесты / 40; sandbox / Песочница / 50; review / Ревью / 60; whitelist / Белые списки / 70; prod / Прод / 80.

## Description — skill_status_transitions (normalized table)

Справочник разрешённых переходов между статусами.

| Field | Type | Constraints | Description |
| --- | --- | --- | --- |
| from_status | varchar(32) | Composite primary key part, FK skill_statuses.code, NOT NULL | Исходный статус |
| to_status | varchar(32) | Composite primary key part, FK skill_statuses.code, NOT NULL | Разрешённый целевой статус |
| is_active | boolean | NOT NULL, default true | Активен ли переход |
| created_at | timestamptz | NOT NULL, default now() | Дата создания перехода |
| updated_at | timestamptz | NOT NULL, default now() | Дата последнего изменения |

Composite primary key: (from_status, to_status).
Initial transitions: draft → checking; checking → training; training → autotest; autotest → sandbox; sandbox → review; review → draft; review → whitelist; whitelist → review; whitelist → prod.

## Description — skill_status_history (normalized table)

Неизменяемая история фактически выполненных изменений статуса навыка.

| Field | Type | Constraints | Description |
| --- | --- | --- | --- |
| id | uuid | Primary key, default gen_random_uuid() | Идентификатор записи истории |
| skill_id | uuid | NOT NULL, FK skills.id, ON DELETE RESTRICT | Навык, у которого изменился статус |
| old_status | varchar(32) | FK skill_statuses.code, ON DELETE RESTRICT, nullable | Статус до изменения, NULL при создании навыка |
| new_status | varchar(32) | NOT NULL, FK skill_statuses.code, ON DELETE RESTRICT | Статус после изменения |
| changed_at | timestamptz | NOT NULL, default now() | Момент фактического изменения статуса |
| actor_sso_id | varchar(200) | nullable | Кто изменил статус, NULL для автоматического изменения |
| reason | text | nullable | Причина изменения, если она предусмотрена сценарием |

## Other selected fields

- Subtasks: empty returned list.
- Attachment metadata: 833803, TEST_PLAN_MOS_1119.md, text/markdown, 7410 bytes, https://task.mos-team.ru/secure/attachment/833803/TEST_PLAN_MOS_1119.md. Body not collected.
- Comments returned: total 2, startAt 0, maxResults 2; both read. Selected non-personal extraction only:
  - 1122856, created/updated 2026-10-02T17:32:15.262+0800: mentions backend merge request 16, branch MOS-1119-status-history, quote `Draft: feat: MOS-1119 Добавить хранение истории статусов навыка`. Personal attribution and outbound MR links omitted; no MR inspected.
  - 1125304, created 2026-10-06T20:17:50.512+0800, updated 2026-10-06T20:39:47.213+0800: `Тестирование: [^TEST_PLAN_MOS_1119.md]` (whitespace normalized).

## Limits

Custom fields, changelog, attachment body and linked MR were not collected. MOS-782/909/1120 were not fetched in this revision. Source state is newer than the original index; no original snapshot overwritten. Status, comment and attachment metadata do not establish implementation or test execution. Compare with D-015 only as supplemental evidence; no automatic precedence or frontend lifecycle authorization.
