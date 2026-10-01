## 1. Дополнение контракта и совместимость

- [x] 1.1 Объединить новую выгрузку с текущим OpenAPI: status/filter/status-operation и Analytics, сохранив PUT intents, required SkillResponse.intents и девять схем; обновить самостоятельные Skills/Domains и Analytics, документацию происхождения/счётчиков и generated-типы штатным `yarn api:generate`. Проверка: 40 операций/156 схем, все ссылки разрешаются, прежние несвязанные определения сохранены, standalone соответствуют полному контракту, `yarn api:check` PASS без зависимости от Downloads.
- [x] 1.2 Обновить status в mock seed/list/detail/create и серверный фильтр до пагинации; добавить опубликованную status operation с контрактной валидацией, версией/ключом и документированными mock-конвенциями. Проверка: server-тесты сочетания фильтров, второй страницы/total, invalid status, версии/ключа, последующего GET и сохранения intents.
- [x] 1.3 Дополнить существующий mock API пятью Analytics операциями по опубликованным схемам без UI аналитики и auth; сохранить stateful board и restart isolation. Проверка: server/contract-тесты всех 39 бизнес-операций, мутаций/readback и невалидного входа; исключён только прежний Access, coverage не ослаблен.

### Промежуточная проверка после 1.1

- PASS: `yarn api:generate`, `yarn api:check`, `yarn lint`, `node --test mocks/contract-documents.test.mjs` (7 тестов), `git diff --check`. Сравнение с прежним контрактом подтвердило сохранение несвязанных схем/операций; проверены все шесть standalone-разделов.
- FAIL: `yarn typecheck` — runtime-схемы Skill и fixtures ещё не содержат обязательный status (предстоящая задача 2.1).
- INCOMPLETE/FAIL: `yarn test` — 353 Vitest-теста прошли; server-тесты уже фиксируют несовместимость seed/обработчиков с новым контрактом (предстоящие 1.2–1.3), общий запуск остановлен таймаутом команды 120 секунд, итогового результата Node suite нет.
- FAIL вне изменений: `yarn format:check` — два существующих файла `docs/tasks/control-center/{analysis,existing-jira}.md` и три архивных документа OpenSpec. Эти файлы не менялись.
- NOT RUN: `yarn build` (конфигурация сборки не менялась); browser/E2E и визуальные проверки не выполнялись.
- Решение пользователя после паузы: формальные response schemas приоритетны, расхождение Analytics документируется без правки источника. Реализованы 1.2–1.3; server/contract/validation-тесты (6) и ESLint mocks — PASS. Обязательное пустое HTTP body различается от явно присланного `{}` на общей границе JSON-парсинга.

## 2. Статус и фильтр каталога

- [x] 2.1 Добавить тип/enum/подписи SkillStatus у entities/skill, обновить list/detail runtime-валидацию, request и Query key; проверить всех потребителей Skill/SkillDetails и обновить fixtures. Проверка: client-тесты status query, всех enum, missing/unknown status без подмены draft и регрессии карточки/регистрации поверхностей.
- [x] 2.2 Добавить статусную колонку и доступный status-фильтр; обновить URL parse/normalize/update, reset page, empty/reset и счётчики. Проверка: unit/component-тесты сочетаний с query/domain/team, page=2, back/forward, сброса/неизвестного status, сохранения посторонних query и прежнего sort allowlist; никаких новых lifecycle-команд и неподдержанных метрик.
- [x] 2.3 Учесть согласованное ревью: сохранять неизвестный строковый status в read-model списка и показывать «Неизвестный статус» только в этой строке, сохранив остальные записи, ссылки, серверные total и пагинацию. Missing/null/нестроковые значения остаются ошибками; фильтр, карточка и OpenAPI не расширяются. Проверка: client-тест смешанного списка и повреждённых значений, component-тест известных/неизвестных статусов (включая совпадение с именами свойств Object.prototype), регрессии фильтра, карточки и потребителей списка.

## 3. Исправление фраз после 422

- [x] 3.1 Различить rejected PUT 422 и неопределённый исход; переиспользовать чистое loc/msg-сопоставление у нижележащего владельца без feature-to-feature импорта. Разрешить редактирование только фраз после 422, сохранить ID/expected_version и отображать неизвестные пути общей ошибкой. Проверка: component-тест нескольких field/general ошибок, сохранения ввода, заблокированных анкеты/connection, отсутствия второго POST и регрессии редактора карточки.
- [x] 3.2 Пересобирать PUT после исправления и локальной валидации, менять ключ только при изменённом теле; при неизменённом повторе и сетевом отказе сохранять тело/ключ/версию. Проверка: 422 → исправление → новый PUT → успех, невалидное исправление не отправляется, 409 не запускает автоматический GET+новую версию, network/204/невалидный ответ не открывают редактирование неопределённой попытки.

## 4. Локальное восстановление

- [x] 4.1 Добавить versioned localStorage snapshot со структурной Zod-проверкой сырого draft, шага и состояния попытки, scoped к приложению/API; восстановить RHF один раз до автосохранения defaults. Проверка: unit/component remount восстанавливает все шаги, неполные/невалидные поля, фразы и connection; чужая версия/повреждённая запись/ошибка чтения не затираются молча, токены/кэш/URL не используются.
- [x] 4.2 Сохранять ввод и шаг штатной подпиской формы; синхронно фиксировать create-pending перед POST, ID перед GET, версию/тело/ключ перед PUT. Проверка: remount pending POST становится unknown без второго создания; подтверждённый ID продолжает только GET/PUT по явному действию; прежний ключ/версия PUT переживают reload, запись при открытии не запускается, сбой storage перед мутацией блокирует её.
- [x] 4.3 Добавить пояснение общего браузерного хранения, ошибки чтения/записи/очистки, подтверждаемое удаление только локального draft, terminal marker/очистку после успеха и защиту от молчаливой перезаписи внешнего обновления вкладки. Проверка: quota/disabled storage, clear cancel/confirm, завершённая запись не создаётся повторно при ошибке очистки, unknown reset предупреждает о дубле, storage event предлагает перечитать запись, восстановленный контакт перепроверяется после полной загрузки участников; dirty-guard остаётся правдивым.

## 5. Приёмка

- [x] 5.1 Проверить связанный сценарий регистрации: POST → PUT 422 → исправление → закрытие/remount → явный PUT → карточка → отфильтрованный по status реестр. Проверка: один созданный ID, новый ключ исправленного PUT, сохранённая версия, серверный status/total и отсутствие auth/нового POST. Отдельно проверить unknown POST и частичный GET при remount без browser/E2E.
- [x] 5.2 Выполнить `yarn typecheck`, `yarn lint` без предупреждений, `yarn test`, `yarn format:check`, `yarn api:check`; при изменениях сборки — `yarn build`. Проверить diff/FSD, документы/типы, отсутствие изменений архива и новых зависимостей; записать PASS/FAIL/not run с причинами. Browser/E2E не запускать и не менять; новые состояния визуально не считать проверенными.

## Результаты проверок до уточнения ревью

- PASS: `yarn typecheck`; `yarn lint` (0 warnings); `yarn api:check`; `yarn build`; `git diff --check`; `openspec validate skills-status-and-registration-recovery --strict --json`.
- PASS: `VITEST_MAX_WORKERS=2 yarn test` — 409 unit/component-тестов в 50 файлах и 31 Node server/contract/FSD-тест, включая все 39 бизнес-операций. Ограничена только параллельность запуска через штатную переменную Vitest; конфигурация проекта, таймауты, пороги и утверждения тестов не ослаблялись.
- FAIL: обычный `yarn test` при стандартной параллельности дважды завершился таймаутами 5000 ms в длинных сценариях регистрации навыка/поверхности и связанном route-тесте. Последний такой запуск: 401 PASS, 6 timeout; Node-часть скрипта после этого не запускалась. Полный повтор с двумя воркерами прошёл, включая Node-часть.
- FAIL вне diff: `yarn format:check` сообщает о пяти прежних файлах: `docs/tasks/control-center/analysis.md`, `docs/tasks/control-center/existing-jira.md`, `openspec/changes/archive/2026-09-23-connect-control-center-http-client/design.md`, `openspec/changes/archive/2026-09-23-improve-code-quality/specs/code-quality-gates/spec.md`, `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md`. Чужие документы и архив не менялись; изменённые файлы отформатированы.
- NOT RUN: browser/E2E и визуальная проверка новых состояний (не разрешены). Сборка выполнена дополнительно, без изменения её конфигурации.
- Diff/FSD проверены: новых зависимостей, auth/session/RBAC, lifecycle UI-команд, UI Analytics, отладочного кода и изменений архива нет. Прежние API-схемы/поля/операции и security metadata сверены с HEAD; потерянных определений нет. Generated-типы и все шесть standalone-документов соответствуют объединённому контракту.
- Проверены 422 с несколькими field/general ошибками, исправленный/неизменённый PUT, неизвестный POST/PUT, частичный GET, remount всех шагов, повреждённые/несовместимые записи, сбои storage до POST/GET/PUT и при очистке, terminal marker, подтверждение удаления, внешнее обновление с storage event и без него, полный справочник участников и сохранение контакта через controlled RHF select. Связанный сценарий завершён карточкой и серверным status-фильтром/total без повторного POST.

## Проверки после уточнения ревью (2.3)

- PASS: `yarn typecheck`, `yarn lint` (0 warnings), `yarn api:check`, `git diff --check`, `openspec validate skills-status-and-registration-recovery --strict --json`.
- PASS: целевые client/component-тесты каталога, фильтра, карточки и регистрации поверхностей — 126 тестов в 13 файлах. Проверены смешанный список, сохранение исходных строковых статусов/total/страницы, подписи и ссылки строк, неизвестные строки (включая пустую, `constructor` и `__proto__`), отказ для missing/null/числа/boolean/объекта/массива и неизменный набор вариантов фильтра.
- PASS: `VITEST_MAX_WORKERS=2 yarn test` — 422 unit/component-теста в 50 файлах и 31 Node server/contract/FSD-тест. Таймауты, конфигурация и утверждения тестов не ослаблялись.
- FAIL вне diff: `yarn format:check` — три прежних архивных документа: `openspec/changes/archive/2026-09-23-connect-control-center-http-client/design.md`, `openspec/changes/archive/2026-09-23-improve-code-quality/specs/code-quality-gates/spec.md`, `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md`. Архив не изменялся; изменённые файлы отформатированы.
- NOT RUN: browser/E2E и визуальные проверки (не разрешены); `yarn build` повторно не запускался, конфигурация сборки не менялась.
- Diff проверен: изменены только read-model/валидация списка, подпись неизвестного статуса, регрессионные тесты и согласованные planning artifacts. OpenAPI/generated, запросы/фильтр и строгая валидация карточки не менялись. Основные specs не синхронизированы; change не архивирован.

### Стабилизация component-тестов status-фильтра

- В параметризованной проверке неизвестных статусов Select открывается клавишей ArrowDown после фокусировки вместо pointer-зависимого открытия в JSDOM. Проверяется aria-expanded, затем ожидаются доступный listbox и полный набор его option через waitFor. Утверждения не ослаблены, задержки/ретраи клика и увеличенные таймауты не добавлены; production-код не менялся.
- PASS: десять последовательных запусков `yarn vitest run app/widgets/skills-registry/ui/skills-registry.test.tsx` (16 тестов каждый), `yarn typecheck`, `yarn lint` без предупреждений и итоговый `VITEST_MAX_WORKERS=2 yarn test` (422 Vitest + 31 Node). Первый общий запуск выявил форматирование нового выражения и зависимый lint-gate тест; после Prettier оба прошли повторно.
- FAIL вне изменений: итоговый `yarn format:check` — те же три архивных документа, перечисленные выше. Изменённый тест отформатирован. Browser/E2E не запускались; build и отдельный api:check не повторялись, production-код, сборка и API не менялись.
