## Context

Мотивация и источники — proposal.md. На этапе explore прочитаны весь HTML, извлечённый текст PDF, A/B OpenAPI DTO, раздел 20 CRUD-документа и текущие KB specs/design/integration guide. Реальный backend и браузер не запускались. Пользователь принял границу редактора настроек без исполнения трафика, расписания, автостопа и расчёта результатов.

Приложение уже использует React Router Framework, TanStack Query, React Hook Form, Zod, shared UI и transport. `app/application/constants/application-routes.constants.ts` объединяет base routes с публичным KB descriptor. Этот уровень композиции позволяет добавить второй модуль без повторного переноса реестра. `useSurfacesRegistryQuery` опубликован через entities/surface, но работает с конкретной страницей, а не полным каталогом. Поиск бизнес-пользователей существует; ID ответственного не является principal.

A/B DTO уже сгенерированы. Generic managed mocks предоставляют базовый CRUD, но metadata использует ab_experiment вместо experiments и пустые bindings; summaries содержат UUID поверхностей вместо названий; предметные проверки агрегата отсутствуют. Реальное наличие generic handlers не доказывает контрактную полноту. Основная mock-spec сохраняет правило unavailable для ещё не принятых операций; delta адресно принимает A/B, не откатывая чужие реализации.

## Goals / Non-Goals

**Goals:** удаляемое владение предметным кодом; реальная работа с поддержанными API; структура и сценарии прототипа с явными ограничениями; сохранность draft/IDs; проверяемые HTTP mocks и production isolation.

**Non-Goals:** execution engine, связь групп с версиями алгоритмов, назначение контрольной группы, статистические тесты, аналитическая панель, scheduler, backend migrations, новая auth/permission модель, редактор справочников/поверхностей, кнопка DELETE эксперимента, платформа плагинов и универсальный managed-resource UI framework. Опубликованный DELETE покрывается контрактными моками, но не добавляет пользовательский сценарий сверх прототипа.

## Decisions

### 1. Один change и адресное optional-владение

Реестр, редактор и экспорт реализуются одним change с отдельными capabilities: это один агрегат и единая граница удаления. Предметный код размещается в `app/optional/ab-testing/` с сегментами routes/ui/api/model/types/constants/handlers и локальными тестами; не создавать пустые сегменты заранее. Моки — `mocks/ab-testing/`.

Публичный index экспортирует только лёгкий descriptor маршрутов/вкладок без runtime UI. Framework route entrypoints импортируют локальные страницы напрямую. Только application composition импортирует публичный API; разрешены shared и публичные entities, запрещены application internals, чужие features/pages/widgets и KB. Аналогичный запрет действует от KB к A/B. Нужны адресные lint rules/tests и согласование формулировки AGENTS.md при реализации, а не исключение всей optional-папки из проверок.

Альтернативы: глобальные FSD-слайсы усложняют удаление; workspace/микрофронтенд требуют лишней инфраструктуры; импорт редакторов KB связывает сроки жизни модулей. Существующие shared helpers переиспользуются, но перенос большой части KB в shared ради этого change не нужен.

### 2. Подключение без feature flag

Как KB, A/B подключён по умолчанию независимо от mock/real режима. Предложенные маршруты `/ab-testing`, `/ab-testing/new`, `/ab-testing/:experimentId`, вкладки main/groups/surfaces/rules и группа меню «Контент» фиксируются specs. Общие shell/header не копируются из HTML. Public descriptor не импортирует UI и остаётся пригодным для Node typegen без Vite aliases.

Существующие session/access boundaries оборачивают бизнес-загрузки. Новые grants, transport ACL и permissions constants не вводятся; сохраняется текущая консервативная политика непокрытых операций. Production использует реальные API, dev следует существующей конфигурации.

Проверка manifest и emitted module graph подтверждает runtime A/B и отсутствие mocks. Существующую KB-проверку не перепрофилировать в A/B; при необходимости выделить только уже востребованную техническую часть анализа графа без зависимости одного optional-модуля от другого. Минимальные внешние подключения и команды проверки перечислить в отдельной application integration guide.

### 3. API — граница допустимых действий, прототип — структура UX

| Расхождение                                  | Решение                                                                                                          |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| archived в HTML/PDF, disabled в API          | Archived виден недоступным с локальным пояснением; disabled отображается по lookup, не переименовывается в архив |
| return_to_control_on_stop                    | В модели формы/DTO использовать контрактное return_to_control                                                    |
| surfaces, sort_order                         | surface_ids; порядок groups определяется массивом, sort_order не отправляется                                    |
| Число групп, priority, surfaces в conditions | Видимые недоступные пункты; не заменять AND-фильтром внутри OR и не фильтровать страницу                         |
| Дробные проценты в JS                        | Строго целые 0–100, сумма 100, группы 2–100                                                                      |
| min_sample_size=0 по умолчанию               | Пустой ввод/null; при задании минимум 1                                                                          |
| scheduled без отдельного datetime            | Обязательная started_on date; не создавать scheduled_at, timezone или client timer                               |
| responsible_user_id как UUID в PDF           | Внешняя строка по API, без связи с auth principal                                                                |
| Экспорт разделов                             | Группировка поддержанных плоских fields, group_distribution/surface_names как сводки, без вложенных таблиц       |
| HTML «успешно» без сетевого результата       | Успех только после валидного API-ответа или реальной доставки файла                                              |
| Предпросмотр нормализует сумму до 100        | Остаток для суммы <100, явная ошибка вместо корректной диаграммы при сумме >100/невалидном вводе                 |

Справочники загружаются через catalogs/lookups/ab-testing, metadata читается из data.experiments. Доступность ограничена одновременно принятым контрактом и metadata; permissive mock или случайный ответ не расширяет scope. 403/500 означают ошибку, не отсутствие поддержки. Неактивные сохранённые значения не теряются; новый выбор запрещён. Unknown read code показывается как код без скрытой подмены.

Defaults — сознательно сохраняем UX HTML: draft, resolution_rate, immediate, all, priority=50, stable/log=true, return_to_control=false, auto_stop=false, control/variant 50/50. Отличия от API defaults manual/0/true отправляются явно. Размер выборки null; поверхности пусты. Наличие default в активном lookup обязательно, иначе требуется явный выбор. Не генерировать name/code, даты создания или обновления.

### 4. Клиенты, загрузка и реестр

Локальные API-клиенты ссылаются на generated DTO и проверяют runtime responses в существующем стиле проекта. Не создавать второй transport/query client. Query keys имеют namespace A/B и используют штатную session-owner очистку/отмену; поздние ответы не попадают в новый контекст.

Реестр использует POST search. URL — источник применённого отбора; редактор условий имеет отдельный draft. Кодек проверяет поля/операторы/форматы/размеры и лимит 50 условий. Unsupported URL/saved search не применяется частично молча. Поиск 0–1 символ не отправляет query; placeholder не ограничивает фактическую серверную семантику поиска. Sort трёхпозиционный, снятие возвращает -updated_at; status сортируется сервером по его семантике, не локализованной подписи.

Сохранённые фильтры используют общий managed endpoint и resource=ab-experiments, пагинацию списка, ID-based delete, полный search. Одинаковые имена не означают upsert. Ошибки clipboard/save/delete сохраняют ввод и не показывают успех. Не добавлять дополнительные быстрые фильтры метрик/аудиторий сверх прототипа только из-за наличия DTO-полей; они доступны в поддержанных условиях.

Поверхности выбирать через публичный paginated entities API с доступом к последующим страницам. По согласованному уточнению UI поиск на вкладке поверхностей удалён; выбранные и невыбранные значения показаны общими чипсами `shared/ui/selection-chips.tsx` + `selection-chip.tsx`, также используемыми KB. Shared владеет только представлением; RHF, лимит 1–100, загрузка страниц и разрешение выбранных ID с retry остаются в A/B. Общие компоненты и их тест сохраняются при удалении любого из optional-модулей. Сохранённые выбранные IDs доступны независимо от текущей страницы. Имена чипсов разрешаются по ID, не split surface_names; неизвестный ID остаётся видимым. Ответственный — существующий поиск пользователей, включая pagination; неизвестный сохранённый ID не назначает первый результат. Не требовать несуществующего GET пользователя по ID и не строить локальный индекс всех пользователей.

### 5. Агрегат редактора

Одна React Hook Form на четыре вкладки, Zod для локальных ограничений, useFieldArray для групп. Локальная идентичность строки отделена от server group id. Snapshot сервера отделён от draft; refetch не сбрасывает dirty форму. Nullable значения не превращаются в false/0 при простом открытии карточки; UI сохраняет исходный null до явного изменения, особенно nullable auto_stop/priority/launch_mode.

POST возвращает ID, после чего выполняются переход replace на detail и GET. Подтверждённый ID сохраняется при ошибке GET, повтор не создаёт дубликат. PUT отправляет diff скаляров и полные изменённые коллекции. Верхнеуровневый Patch schema допускает null шире бизнес-документа — builder запрещает null для обязательных полей/переключателей/массивов. Для groups/surface_ids [] невалиден даже в draft; не переносить возможность пустого KB-черновика на A/B.

Ошибки envelope и HTTPValidationError связываются с полями и вкладками. При отправке массива сохранить snapshot порядка: ошибка /groups/{index}/tag относится к отправленной группе, а не перемещённой позже. Во время мутации блокировать изменяющие действия, не теряя draft. Mutation retry выключен; неизвестный сетевой результат требует сверки сервера, не replay. Контракт не предоставляет expected_version/idempotency для этого ресурса — не изобретать их; конкурентное редактирование не объявлять защищённым.

Для group tag readonly используется сохранённый status != draft, а не watched status. Имя/проценты/reorder разрешены. Добавление/удаление остаются штатными операциями коллекции, но UI не использует их автоматически для обхода immutable. Если backend после отдельного сохранения возвращает draft, следуем новому snapshot; истории ever_started в API нет.

Drag-and-drop за ручку дополняется кнопками вверх/вниз с доступными именами. Новые группы не получают fake server UUID. Непустой автоматически предложенный тег не должен дублировать оставшиеся теги после удалений; можно оставить новый тег пустым для явного ввода. Шесть цветов повторяются для больших списков, но имя/тег/процент обеспечивают идентификацию без цвета. Legend показывает 0%; при невалидной сумме не выдавать нормализованную полосу за фактическое распределение.

### 6. Статусы и описание правил

Сохраняется shortcut прототипа: paused -> active («Возобновить»), другие поддержанные статусы -> paused («Приостановить»), completed target у «Выключить» с подтверждением, уже completed не завершается повторно. Это не новая backend state machine; в частности завершённый статус не объявляется терминальным. Для unknown/archived команды недоступны. Новая/dirty карточка должна быть сохранена или изменения отменены до команды. PUT содержит только status, даты не назначаются автоматически.

Селект статуса остаётся частью формы; quick actions отдельны от Save. Уведомления формулируются как сохранение статуса, без обещания фактического изменения трафика. Архив недоступен; DELETE не является заменой.

«Как это сработает» становится описанием настроек: аудитория/сегмент, режим/дата, приоритет и согласованные с переключателями фразы. Нельзя одновременно писать log_group=false и утверждать запись тега в каждом запросе. Рядом постоянно объясняется отсутствие исполнения через текущий API. Поля scheduled/auto_stop редактируемы как сохраняемые настройки, а не disabled: API поддерживает хранение. Ни первая группа, ни тег control не получают скрытой роли контроля.

### 7. Экспорт

Использовать существующий file-response/download механизм и локальную форму выбора полей. Источник доступных колонок — metadata в рамках DTO. Список передаёт весь applied search; pagination не ограничивает CSV, предел 10000/metadata. Ошибка лимита предлагает сузить отбор без скрытого усечения.

Modal карточки группирует плоские колонки по пяти разделам прототипа. В отличие от KB, гипотеза и правила здесь действительно доступны как скаляры. Группы — group_distribution/groups_count, поверхности — surface_names; явно подписать текстовые сводки и недоступность отдельных вложенных таблиц. Не передавать main/groups/surfaces как неподдержанные fields. Порядок выбранных колонок сохраняется. Новая карточка не экспортируется, dirty предупреждает о серверном snapshot. Ошибки и session switch используют штатные гарантии доставки файлов.

### 8. Контрактные моки и проверяемость

Добавить A/B handlers/seed/validation/tests в отдельную папку, подключить в существующий managedResourceHandlers и явно включить вложенные tests в yarn test. До mock-реализации прочитать auth/demo archive artifacts, не меняя эту модель. Общие технические managed helpers переиспользуются; нельзя импортировать предметный код mocks/knowledge-base. Совместная регистрация section lookup обязана сохранять обе секции, а не заменять одну другой; тестировать последовательность запросов KB/A/B/прочих lookup.

Привести metadata key/bindings, summaries, defaults/nullability, group IDs, replacement, name/code conflicts, inactive/reference validation, saved search, search case semantics и CSV к CRUD-документу. Не ограничиваться проверкой response schema: сумма 100 и immutable — межполевые правила. Восемь A/B-операций, включая DELETE, имеют HTTP round trips; ошибки не мутируют state. Seed с валидными статусами и IDs существующих поверхностей; без runtime archived и автоматических таймеров/результатов. Generic handlers других ресурсов не откатываются к 501.

Component/unit tests проверяют form/diff, hidden-tab errors, keyboard reorder, preview, URI codec, clipboard/file errors, сохранность draft и session reuse. Mock tests проверяют существенный сценарий и границы (1/2/100/101 групп; 99/100/101 сумма; 0% допустим; дроби запрещены; дубли IDs/тегов; scheduled/segment; immutable snapshot; export beyond page). Build/architecture проверки обеспечивают отдельное удаление A/B и сохранение KB. Browser/E2E не создавать/не менять/не запускать без отдельного разрешения.

## Approved image-reference presentation alignment

The five supplied PNGs are approximate composition references, not pixel-perfect acceptance targets:

- `7242f344` and `10fdca0f`: compact wrapping editor header with actions at the right, four line tabs, equal desktop group/preview columns. Group cards put name and accessible reorder/delete controls above percent/unit/tag; total feedback stays below the group list. The preview has a contrasting inset with percent-only segment labels and a complete name/tag/percent legend.
- `d08ddc47`: compact registry heading with export/create at the right, a single primary search/filter toolbar and the existing bordered table with name/code hierarchy, surface chips, counts, status and trailing navigation. Saved selection tools live in a native secondary disclosure below results; pagination and errors remain available.
- `13a9b151`: full-width surfaces card. The subsequent approved shared-chip refinement replaces separate selected chips and unselected checkbox pills with the same controlled selection chips used for KB skills, without a search input. Current-page selected and unselected options appear together; off-page selected IDs remain visible and removable. The actual paginated catalog, missing-ID resolution/retry, selected count and 1–100 validation remain; no fixed six-item catalog.
- `e31fa143`: two-column rules card and ordered explanation of configured settings, not a promise of execution. All contract fields and execution caveats remain.

Server snapshot/reconciliation controls move into a native keyboard-accessible disclosure; mutation feedback remains outside it. Existing DnD is retained with accessible icon buttons, not replaced with decorative drag affordances. Mobile layouts stack; long metadata and tabs still wrap. Shared components, neutral theme and chart tokens are reused without global recoloring, shell changes, dependencies or business/API changes. Consequently prototype red/green hues, exact sizing, typography and shell spacing are intentionally not reproduced. Component assertions establish structure and behavior only; no browser measurement or visual-equivalence claim is made.

## Risks / Trade-offs

- [Настройки выглядят как действующий engine] -> постоянные локальные пояснения и честные уведомления, отсутствие результатов и runtime timers.
- [Удаляемость требует внешних подключений] -> перечислить все регистрации/проверки в integration guide; проверить сборку после отсоединения в временной копии, не удаляя рабочий модуль.
- [Общие managed helpers затрагивают KB] -> минимальные технические изменения, сохранение текущих тестов и отдельные cross-section lookup/regression сценарии.
- [Неизвестные/неактивные references] -> сохранять ID/код и показывать ошибку, не заменять демоданными или первым option.
- [Нет конкурентной версии и истории запуска] -> не обещать optimistic locking или ever-started immutability; применять документированные ограничения snapshot и обрабатывать серверный конфликт.
- [Defaults HTML отличаются от API] -> явно отправлять выбранные значения, проверить их активность, отдельно протестировать null вместо 0.
- [Прототип недоступен в другом checkout] -> существенные требования и расхождения зафиксированы в repo specs/design; сборка и тесты не зависят от Downloads.

## Migration Plan

1. Ввести адресные архитектурные правила и регистрацию A/B через существующую application composition, сохранив KB и базовые маршруты.
2. Реализовать контрактный слой/моки, затем реестр, агрегат редактора, статусы и экспорт с соответствующими тестами.
3. Проверить обычные typegen/build и production graph; выполнить typecheck, lint без warnings, test, format:check, api:check. Отдельно указать, что локальные mocks не подтверждают интеграцию со стендом.
4. Инструкция rollback/removal перечисляет удаление A/B-папок, descriptor import/append, mock registrations, dedicated tests/scripts/globs и адресных lint rules. Общие DTO, technical helpers, KB, чужие seed и серверные данные сохраняются. После удаления в временной копии выполнить typegen/build и проверки границ.
