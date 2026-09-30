## 1. Уточнения connection API

- [x] 1.1 Зафиксировать merge/replace и очистку connection, совместимость auth_required/auth_type, ограничения key/options и default string/integer/null; проверка: design содержит принятые правила и примеры, не выведенные из mock-конвенций.
- [x] 1.2 Переиспользовать PATCH из MOS-944 либо добавить его в entities/skill без дублирования, сохраняя expected_version/Idempotency-Key; проверка: API-тест тела только connection и версии, ошибки и ответа.

## 2. Форма подключения

- [x] 2.1 Исправить null-state и добавить отдельную форму endpoint/contract_version/auth_required/auth_type; проверка: component-тест настройки connection=null без поля для секрета.
- [x] 2.2 Добавить редактор списка select-параметров key/title/required/options/default по принятым ограничениям; проверка: тест нескольких ключей, отсутствующих optional полей, default=0 и строкового/null default без изменения типа.
- [x] 2.3 Реализовать отмену, pending, сохранение draft при ошибке/конфликте и обновление detail; проверка: component-тест успешного повторного чтения и ошибки без перезаписи анкеты.
- [x] 2.4 Добавить ссылку на skill-params и проверить отсутствие kb_section-only поведения; проверка: component-тест href под basename и отображения произвольных параметров.

## Реализация по запросу пользователя

- Пользователь разрешил реализовать доступную часть максимально близко к шаблону по визуалу и логике. Источник визуала: `/home/user/Загрузки/Прототип. Центр управления.html`, изучен как текст без браузера.
- Вкладка использует карточку «Реализация навыка», параметры с badge и адаптивные две колонки. Фиктивные токены/версии контракта из прототипа не перенесены.
- После частичной UI-реализации пользователь согласовал полную замену connection и frontend-валидацию типов по OpenAPI; бизнес-ограничения проверяет backend. Удаление всего подключения через null не добавляется.
- Реализованы сохранение полного connection через существующий PATCH, expected_version, стабильный Idempotency-Key для повторной отправки неизменённого тела, pending-защита от повторной отправки/закрытия, отмена, отображение серверного результата и сохранение ввода при ошибке/конфликте/refetch.
- Редактор поддерживает произвольные select-параметры/варианты и явные типы default, сохраняет optional поля, null, пустые списки, строки и integer 0. Общая схема connection используется для чтения ответа и проверки сериализованной формы; integer вне точного диапазона JavaScript отклоняется.
- Целевые 58 unit/component/API-тестов проходят. Новые типы параметров, секреты и auth-контекст посетителя не добавлены; mock и generated-контракт не изменены.
- Проверки: `yarn typecheck` и `yarn lint` без предупреждений — пройдены; `yarn test` — 276 unit/component и 25 Node-тестов пройдены; `openspec validate mos-1022-skill-connection-settings --strict` и `git diff --check` — пройдены.
- `yarn format:check` падает только на пяти неизменённых файлах: `docs/tasks/control-center/{analysis,existing-jira}.md`, `openspec/changes/archive/2026-09-23-connect-control-center-http-client/design.md`, `openspec/changes/archive/2026-09-23-improve-code-quality/specs/code-quality-gates/spec.md`, `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md`. Затронутые файлы проверены отдельно.
- `yarn api:check` пройден после расширения локального UpdateSkillRequest до существующего generated-контракта. `yarn build` не запускался: сборочная конфигурация не изменялась. E2E/browser и визуальное сравнение в браузере не выполнялись. Diff просмотрен, посторонний `docs/tasks/` не изменён.

## Предупреждение при архивировании

- Пользователь подтвердил архивирование с известным дефектом P2: при ответе HTTP 422 с `detail[].msg` форма подключения показывает только «Ошибка HTTP 422», не отображая причину валидации из `ApiError.details`. Черновик сохраняется. Дефект воспроизведён отдельным временным component-тестом при ревью после обновления dev; исправление в этот change не внесено.
- После обновления dev прошли `yarn typecheck`, `yarn lint`, `yarn api:check`, 283 unit/component-теста и 25 Node-тестов. `yarn format:check` по-прежнему падает на пяти указанных выше неизменённых файлах. Browser/E2E не выполнялись.

## 3. Самостоятельная приёмка MOS-1022

- [x] 3.1 Проверить spec unit/component-тестами, включая клавиатуру/подписи/ошибки и границу integer default; при изменении mock добавить HTTP server-тест; проверка: согласованные сценарии проходят независимо от остальных вкладок. E2E/browser не выполнять.
- [x] 3.2 Запустить yarn typecheck, yarn lint без предупреждений, yarn test, yarn format:check; при изменении API-типов yarn api:check, сборки — yarn build; проверка: результаты сохранены, diff не содержит новых parameter types и секретов.
