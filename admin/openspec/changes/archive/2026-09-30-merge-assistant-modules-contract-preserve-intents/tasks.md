## 1. Объединённые контракты и типы

- [x] 1.1 Проверить исходный staged/unstaged diff и структурные различия рабочего OpenAPI с `/home/user/Загрузки/message.txt`; подтвердить пять новых операций / 22 схемы модулей и наличие PUT intents / девяти схем / обязательного SkillResponse.intents, не сбрасывая текущие изменения.
- [x] 1.2 Аддитивно перенести Assistant modules в `docs/api/contracts/openapi.json`; структурным сравнением подтвердить неизменность всех прежних paths/schemas, совпадение добавлений с выгрузкой, сохранение security и итог 34 операции / 124 схемы.
- [x] 1.3 Добавить самостоятельный `assistant-modules.openapi.json`, актуализировать `skills-domains.openapi.json` с intents и полными транзитивными зависимостями; добавить node:test проверки совпадения операций/схем с полным OpenAPI и разрешимости ссылок обоих разделов без обращения к Downloads.
- [x] 1.4 Обновить README контрактов, Assistant modules и Skills/Domains Markdown; сверить таблицы с JSON (34 операции всего, пять заполненных разделов, девять операций Skills/Domains) и явно указать объединённое происхождение вместо точной копии message.txt.
- [x] 1.5 Выполнить `yarn api:generate`; проверить сохранение типов intents и добавление Module DTO/paths командой `yarn api:check`, без ручного редактирования generated-файла.

## 2. Mock API модулей и общие helpers

- [x] 2.1 Добавить коллекцию modules в seed, пять handlers в `mocks/assistant-modules.mjs` и регистрацию в app; подтвердить успешное создание mock app и schema-valid HTTP-ответы всех пяти операций без Bearer, сохранив PUT intents и исключение Access.
- [x] 2.2 Нормализовать одиночные array query-параметры перед AJV, сохранив повторённые значения; server-тестами проверить одиночный/множественный sort, невалидный enum (422), прежние scalar sort и integer limit/offset.
- [x] 2.3 Проверить все вызовы общего sort и исправить default accessor для descending; регрессионными тестами подтвердить сортировку строк/дат/чисел/nullable, стабильность, неизменность входа и сохранение custom accessor API.
- [x] 2.4 Реализовать фильтры, упорядоченную многополевую сортировку и пагинацию модулей через существующие helpers; HTTP-тестами проверить defaults, query по code/name/description, точный status, неизвестный status, фильтрацию до среза и offset за концом.
- [x] 2.5 Реализовать enable/disable по основной спецификации и design: expected_version, disable_allowed, confirm_impact, user_message, version/updated_at/by; тестами проверить успех и повтор целевого состояния, 404/409/422 и неизменность состояния при каждом отказе.
- [x] 2.6 Вычислять summary/preview из общей коллекции; тестами цепочки disable/read/enable/read проверить totals, healthy/degraded, tone, fallback-карточки, заданный/default текст, сброс user_message и изоляцию нового экземпляра сервера.

## 3. Сохранение intents и контрактное покрытие

- [x] 3.1 Сохранить существующие handlers/state/idempotency intents; дополнить HTTP-регрессию запись/GET/повтор с тем же ключом/очистка, невалидная группа, отсутствующий ключ и устаревшая версия с новым ключом. Проверить версию и отсутствие изменений при отказах, не ослабляя существующие утверждения.
- [x] 3.2 Обновить контрактное покрытие до 34 операций / 33 бизнес-операций; тест должен сравнивать множество реально исполненных операций с OpenAPI, падать при пропуске любой бизнес-операции и отдельно подтверждать 404 `/auth/v1/me`.
- [x] 3.3 Обновить `mocks/README.md`: матрица 33 бизнес-операций, Assistant modules, сохранённый intents и локальные конвенции поиска/сортировки/переходов/ошибок/preview; сверить с тестами и не приписывать backend недокументированные правила.

## 4. Интеграционная проверка и границы change

- [x] 4.1 Запустить `yarn typecheck`, `yarn lint` без предупреждений, `yarn test`, `yarn format:check`, `yarn api:check` и `yarn build`; отдельно подтвердить existing unit/component-сценарии редактора фраз и production isolation, записать пройденные/упавшие/не запущенные проверки и причины без ослабления правил. E2E/browser-тесты не создавать, не редактировать и не запускать.
- [x] 4.2 Просмотреть итоговый diff относительно исходного рабочего дерева и выполнить `git diff --check`; подтвердить сохранение прежних изменений intents, отсутствие изменений UI/auth, новых зависимостей, runtime-зависимости от Downloads и случайных файлов вне задачи.

## Результаты проверок

- Пройдены `yarn typecheck`, `yarn lint` (0 warnings), `yarn api:check`, `yarn build`, `git diff --check` и строгая OpenSpec-валидация change.
- Финальный `yarn test`: 231 Vitest unit/component-тест (36 файлов), включая редактор обучающих фраз, и 24 node:test server/tooling-теста, включая dev/prod isolation. Первый запуск одновременно со сборкой/typecheck завершился пятью ошибками ожиданий/таймаутов в прежних UI-тестах; два отдельных полных повторных запуска прошли без изменений тестов или таймаутов.
- `yarn format:check` выполнен, но падает на четырёх файлах вне change: `openspec/changes/archive/2026-09-23-connect-control-center-http-client/design.md`, `openspec/changes/archive/2026-09-23-improve-code-quality/specs/code-quality-gates/spec.md`, `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md`, `openspec/changes/mos-1015-report-constructor/specs/dialog-selection-draft/spec.md`. Эти файлы не изменялись. Отдельный `yarn prettier --check mocks docs/api/contracts app/shared/api/schema.d.ts openspec/changes/merge-assistant-modules-contract-preserve-intents` пройден.
- Сравнение с копией рабочего дерева до реализации подтвердило сохранение всех прежних paths/schemas и seed-коллекций, точный перенос модулей, неизменность security metadata и отсутствие правок UI/auth/зависимостей. Контрактные проверки и генерация работают с файлами репозитория. Mock-маркеры модулей отсутствуют в production client bundle.
- E2E/browser-тесты не создавались, не редактировались и не запускались.
