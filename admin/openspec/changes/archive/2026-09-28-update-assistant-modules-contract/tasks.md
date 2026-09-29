## 1. Контракты и типы

- [x] 1.1 Импортировать `/home/user/Загрузки/message (2).txt` в `docs/api/contracts/openapi.json`; структурным сравнением подтвердить только пять новых операций и 22 схемы, итог 33/115, неизменность прежних путей, схем и security.
- [x] 1.2 Добавить `assistant-modules.openapi.json` с транзитивными зависимостями, обновить `assistant-modules.md` и индекс контрактов; проверить соответствие всех пяти операций полному источнику и отсутствие неразрешимых локальных $ref автоматическим тестом по существующему node:test подходу.
- [x] 1.3 Выполнить `yarn api:generate`; проверить добавленные Module DTO и paths, отсутствие ручных правок generated-файла и успешный `yarn api:check`.

## 2. Mock API модулей

- [x] 2.1 Добавить modules seed и `mocks/assistant-modules.mjs`, зарегистрировать пять handlers в `mocks/app.mjs`; проверить запуск createMockApp и schema-valid HTTP-ответы всех пяти операций без Bearer, без изменения исключения Access.
- [x] 2.2 Нормализовать одиночные и повторённые array query-параметры перед AJV в общей границе валидации; тестами подтвердить одиночный sort, несколько sort, ошибочный enum и сохранение старых scalar-параметров.
- [x] 2.3 Реализовать поиск, status, приоритетную сортировку и limit/offset с существующими list helpers; тестами проверить фильтрацию до пагинации, defaults, неизвестный status, пустую выборку и offset за концом.
- [x] 2.4 Реализовать проверку expected_version, ограничения disable, обновление status/version/updated_at/by и user_message по design; server-тестами подтвердить успех обеих мутаций, повтор целевого состояния с актуальной версией, 404/409/422 и неизменность данных при отказах.
- [x] 2.5 Вычислять summary/preview из текущего состояния modules; тестами цепочки disable/read/enable/read проверить totals, healthy/degraded, banner tone, fallback-карточки, сохранённый/default текст и сброс состояния новым экземпляром.

- [x] 2.6 Исправить default accessor общего sort в `mocks/list.mjs`; регрессионными тестами подтвердить descending для строк/дат/чисел, nullable-поля, стабильные совпадения, неизменность входа и custom accessor, а HTTP-тестами — прежних потребителей.

## 3. Покрытие и документация

- [x] 3.1 Обновить `mocks/contract.test.mjs` до 33 операций / 32 бизнес-операций и добавить сценарии модулей; проверять равенство множества реально исполненных операций контрактному множеству, сохранив единственное исключение `/auth/v1/me` и его 404.
- [x] 3.2 Обновить `mocks/README.md`: матрица 32 операций/24 business paths, новый раздел handlers, шесть отсутствующих разделов и явные mock-конвенции поиска, сортировки, переходов, ошибок и preview; сверить описания с тестами и исходным OpenAPI, не приписывая backend недокументированные правила.

## 4. Итоговые проверки

- [x] 4.1 Запустить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`, `yarn api:check` и `yarn build`; зафиксировать результаты, не ослабляя проверки и не запуская/редактируя E2E/browser-тесты.
- [x] 4.2 Просмотреть итоговый diff и подтвердить отсутствие изменений UI/auth, новых зависимостей и правок старых самостоятельных контрактов; проверить совместную поставку OpenAPI/типов/моков и отсутствие server fixtures в production по существующим проверкам изоляции.

## Результаты проверок

- Пройдены `yarn typecheck`, `yarn lint` (0 warnings), `yarn test` (203 Vitest + 21 node:test), `yarn api:check`, `yarn build`, `git diff --check`.
- `yarn format:check` выполнен, но падает на пяти ранее существовавших файлах вне change: `docs/tasks/control-center/analysis.md`, `docs/tasks/control-center/existing-jira.md`, `openspec/changes/archive/2026-09-23-connect-control-center-http-client/design.md`, `openspec/changes/archive/2026-09-23-improve-code-quality/specs/code-quality-gates/spec.md`, `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md`. Эти файлы не изменялись. Форматирование файлов change проверяется отдельно.
- Структурное сравнение подтвердило равенство итогового OpenAPI свежей выгрузке и неизменность прежних paths/schemas. Проверены diff и отсутствие новых mock markers в production client bundle; тесты dev/prod isolation проходят.
- E2E/browser-тесты не создавались, не менялись и не запускались.
