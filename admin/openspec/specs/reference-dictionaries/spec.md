# reference-dictionaries Specification

## Purpose

Provide one unified Dictionaries administration section for registry selection, ordinary and attachment-rule values, settings, validation, lifecycle, exports and documented consumers without confusing stored data with effective downstream policy.

## Requirements

### Requirement: Acceptance follows explicit revised API scope

The Dictionaries section SHALL follow the latest explicit user/backend decisions recorded in design.md: physical dictionary deletion, computed API mutation permissions, published read-only dictionary checks, stored lifecycle status, published filters/sorts and attachment CRUD/schema only. Historic Wiki/prototype coverage SHALL remain attributed evidence, not conflicting normative requirements. Scope revision or artifact completeness MUST NOT be reported as feature delivery or deployed validation. Unsupported capabilities SHALL NOT send invented requests or display simulated success. Comment-to-journal SHALL remain specifically unavailable/unresolved, without blocking supported settings/editor/status/delete work.

#### Scenario: Requirement revision is not implementation evidence

- **WHEN** a previously required server-check or consumer-enforcement feature is removed from scope
- **THEN** no implementation task is marked complete merely because the prerequisite disappeared, and actual UI/test changes remain subject to acceptance review

### Requirement: Isolated section with portal presentation

The section SHALL remain independently removable like KB, exposing only descriptors to application composition and native route entrypoints. Its domain/UI code and specialized mocks SHALL remain isolated from other optional modules; shared services and public entity APIs SHALL be reused without taking ownership of consumer lookup storage. The section SHALL use portal shared UI and preserve prototype scenario parity, not reproduce the standalone demo shell or fake persistence.

#### Scenario: Remove the administration section

- **WHEN** the section descriptors, module and specialized mocks are removed from composition
- **THEN** other sections and their shared lookup storage remain independent of the administration UI

### Requirement: Unified registry and truthful states

The section SHALL provide a title/purpose, three-type explanation, create/export actions and a navigable registry showing name with service code, rules-kind badge, type, value count, owner and status. System, informational and user types SHALL remain distinct from list and rules-attachments kinds, with textual labels in addition to blue/green/purple identification. Counts and pagination SHALL use server results. Loading, valid empty, failure/retry, unavailable and existing access-denied states SHALL be distinguishable; detail navigation SHALL not depend on a row being on the loaded page.

#### Scenario: Open a direct detail link

- **WHEN** a valid dictionary ID is opened outside the current registry page
- **THEN** detail is loaded independently; absent resource, invalid identifier and other request errors are not replaced by a synthetic dictionary

#### Scenario: Failed list request

- **WHEN** the registry request fails
- **THEN** the interface preserves the failure and a retry action rather than showing demo rows or a successful empty count

### Requirement: Complete selection and sorting

Registry selection SHALL include name/code/description search from two characters, type/status multiselects with service-code hints, AND/OR condition groups, visible applied conditions/count and reset. Empty multiselects SHALL mean all; members within a dimension combine as alternatives and dimensions combine with search/conditions through AND. Sorting SHALL use only published ±name/code/kind/status/owner/values_count/created_at/updated_at, with default name. Supported sort/search SHALL operate over the server collection, not the loaded page.

The constructor SHALL use published fields name/code/description/owner/kind/status/group, text operators contains/not_contains/eq/ne/starts_with/ends_with/is_empty/is_not_empty and enum in/not_in as permitted by metadata. Numeric count conditions and group/type sorting SHALL NOT be offered or sent using guessed wire values or substituted with kind. Invalid/blank required operands SHALL prevent Apply without changing the applied selection; empty condition lists SHALL explicitly clear conditions on Apply.

#### Scenario: Short search and multiple types

- **WHEN** one character is entered and two types are selected
- **THEN** no invalid short query is sent and the type selection continues to filter server results without a fabricated empty result

#### Scenario: Missing type sorting contract

- **WHEN** the local contract supports kind sorting but not group/type sorting
- **THEN** group/type sorting is not offered, kind sorting is labeled as kind, and no missing group-sort backend feature is required for acceptance

### Requirement: Durable saved selections and share links

Named selections SHALL use the published managed-resource saved-filter operations for resource catalogs, preserving search, multiselects and conditions. Users SHALL be able to save, apply and delete selections; failed requests SHALL not change the UI as though persistence succeeded. Search replacement SHALL follow the published whole-object replacement semantics. Shared links SHALL restore the complete approved selection rather than only q. Full selection URLs SHALL include filters, conditions, sort, limit and offset. Applying a saved selection SHALL start from the first page while retaining its sort and limit. Duplicate-name replacement SHALL require explicit confirmation. Multiple exact-name matches SHALL require selection/confirmation of a concrete record ID. Invalid links SHALL show an explicit error rather than silently searching defaults. Registry reset SHALL clear query/filters/conditions/offset while retaining sort/limit and saved records.

#### Scenario: Saved filter update fails

- **WHEN** the server rejects a replacement search
- **THEN** the previous saved record remains authoritative and the user's unsaved selection and error remain available

#### Scenario: Share complete selection

- **WHEN** a selection containing search, multiple statuses and conditions is copied and restored under the full-selection URL policy
- **THEN** all approved selection dimensions roundtrip and a clipboard failure is not reported as successful copying

### Requirement: Detail information and type boundaries

The card SHALL show name, description, status text/indicator, code, type and server update date, a type/kind explanation and Values, Settings and Checks tabs. Export and Close SHALL be available for all types under existing UI access policy. System editing SHALL remain read-only, with disabled fields/toggles/delete and no add or reorder control. Save and lifecycle controls SHALL belong to informational/user workflows and whole-dictionary Delete only to user workflows; value actions SHALL obey computed API flags and backend restrictions. Dictionary code and type SHALL remain immutable in this UI.

#### Scenario: System rules dictionary

- **WHEN** a rules-attachments dictionary has system group
- **THEN** the special column layout does not bypass system read-only behavior or create a fourth permission group

### Requirement: Ordinary value editing and defaults

Ordinary values SHALL display order, code, display label, description, default, enabled and deletion controls. Allowed addition SHALL start an empty row, not seeded business values. Editing/reordering/deletion SHALL obey the published group/flag matrix; reorder SHALL not bypass allow_rename and code edits SHALL require value_code_editable. Counts SHALL respond to draft add/delete without being confused with persisted registry counts. Zero or one default SHALL be supported; an active default selected through the published single-value operation clears the previous default atomically within that operation. Disabling a default SHALL require explicit clearing of that default, never a hidden reassignment. Whole-card Save SHALL use sequential staged persistence, show confirmed partial outcomes and retain the remaining draft without automatic retry or fake rollback. Operation ordering and code identities SHALL respect rename/collision/default/reorder/delete dependencies. Unknown outcomes SHALL remain unconfirmed until reconciled, without automatic replay; no journal submission SHALL be fabricated.

#### Scenario: Select another default

- **WHEN** an allowed active value becomes default
- **THEN** the resulting server state has at most one default, while a failure is not represented as a committed switch

#### Scenario: Row sequence partly succeeds

- **WHEN** one row mutation succeeds and another fails
- **THEN** the UI does not claim whole-card atomic success or rollback, preserves unconfirmed input and distinguishes confirmed committed subsets from failed or unknown operations before manual continuation

### Requirement: Attachment rule representation and enforcement boundary

Rules SHALL display order, code, category, extensions, MIME, max size MB, max count, zones, enabled and deletion controls, applying group/mutation restrictions independently of kind. Wire integer bounds and required strings SHALL be validated without treating stored rows as proof of upload enforcement. The scope SHALL be published rule CRUD/schema only: extensions and zones require nonblank bounded strings, MIME permits an empty string, and size/count require positive bounded integers. No MIME/extension evaluator, priority/overlap/order policy, zone vocabulary or unmatched-file denial SHALL be specified or claimed effective. Scope labels auth/anon MUST NOT introduce authentication or permission behavior.

#### Scenario: Save rule limits

- **WHEN** a proposed rule has zero, fractional or out-of-range size/count
- **THEN** it cannot be sent as a valid rule; saving valid limits alone does not announce that upload policy has been enforced

### Requirement: Settings persist published fields only

Settings SHALL edit name, description, owner, public_api, values_required and cache_seconds for allowed workflows. System settings SHALL be read-only; dictionary code/type SHALL remain immutable in this UI. Cache seconds SHALL be an integer from 0 to 2147483647. Only documented description/owner clearing SHALL use null. Mutation flags SHALL be displayed as computed API capabilities, never writable preferences. Publication/cache/required fields SHALL be described as stored settings, not proof of external effects. Change-journal comment SHALL be explicitly identified as unavailable/unresolved and SHALL NOT appear as an editable persisted field or enter save payloads; its missing contract SHALL NOT block saving supported fields.

#### Scenario: Computed flags returned by API

- **WHEN** detail returns allow flags
- **THEN** the interface derives allowed value actions from them without submitting edits to computed fields

#### Scenario: Journal unavailable

- **WHEN** supported settings are saved without a published journal contract
- **THEN** the supported changes can succeed while comment persistence remains explicitly unavailable, with no dropped editable comment or journal-success claim

### Requirement: Published server diagnostics independent of input validation

The section SHALL retain immediate schema/business input validation and backend error handling, including field paths and draft retention. The Checks tab SHALL load GET /catalogs/{entity_id}/checks using the existing session-owned transport and expose Перепроверить as a repeat GET, not a mutation or client-side evaluator. It SHALL show server summary counts passed/failed/skipped, ordered check display_name, textual status, message and JSON Pointer fields. Results SHALL be validated against the published contract and matching dictionary UUID. No fabricated success, severity conversion or local substitute for server diagnostics is permitted.

Checks SHALL explicitly describe saved server data, including inactive values, not the current dirty draft. Dirty inputs SHALL be retained during checks/refetch and tab navigation. Confirmed saves SHALL invalidate previous check results; read failures SHALL remain distinguishable from diagnostic failed results and stale results SHALL NOT be represented as freshly verified. Loading, retry, access/request errors and malformed responses SHALL be handled without losing draft state. Busy/refetch behavior SHALL prevent duplicate user-triggered requests; cancellation and session replacement SHALL suppress late response effects.

Diagnostics SHALL NOT block saving, activation or other lifecycle actions, modify card timestamps, or claim attachment-rule enforcement. Local validation SHALL remain input feedback, not server results. Journal persistence remains unavailable.

#### Scenario: Invalid draft input

- **WHEN** an edited value violates published length, format, default or integer constraints
- **THEN** the field error prevents the invalid mutation without pretending to have executed a server check

#### Scenario: Repeat checks for saved data

- **WHEN** the user clicks Перепроверить while the card has unsaved edits
- **THEN** the client repeats the checks GET, retains the draft, and labels results as diagnostics of saved data without sending a save request

#### Scenario: Diagnostic failure is a successful read

- **WHEN** HTTP 200 SUCCESS contains failed and skipped check results
- **THEN** the tab displays those statuses and messages without reporting a transport failure or disabling Save/activation

#### Scenario: Failed or stale diagnostic request

- **WHEN** the request fails, returns another dictionary UUID, or completes after session replacement
- **THEN** no new successful verification is announced and the current user's draft is not replaced by that response

#### Scenario: Optional fields at creation

- **WHEN** a new empty draft omits optional description or has no values
- **THEN** no prototype warning/check severity or nonempty-values readiness requirement is invented

### Requirement: User dictionary creation

Creation SHALL expose required name/code, optional description/owner and a labelled «Тип справочника» selector. The selector SHALL offer «Список значений» (`list`) and «Правила вложений» (`rules-attachments`), with `list` selected by default. This selection represents the value format `kind`, not the system/informational/user `group`. Only user dictionaries SHALL be created, with the selected kind and explicit draft status; the returned dictionary SHALL be opened without demo IDs or timestamps. The UI SHALL allow selection of `rules-attachments` even when another dictionary of that kind exists; backend rejection SHALL remain an error, not simulated success. The kind SHALL NOT be editable after creation in this UI.

Required/format feedback SHALL be immediate; available advisory uniqueness feedback SHALL not be represented as race-safe approval. Server conflicts SHALL preserve input and identify the code conflict. Owner SHALL default to Команда ЦАМ. Code SHALL obey the lowercase wire constraints without silent transformation; no unsupported uppercase request or guessed uniqueness endpoint is allowed. Dismissal with dirty input, including a changed kind, SHALL preserve input on cancellation and require confirmation before discard. The selector SHALL be keyboard accessible and disabled during a pending creation request. Errors and late responses SHALL retain existing session ownership and cancellation safeguards.

The created card SHALL display its returned server data and use the editor for the returned kind; it SHALL NOT fabricate the selected kind if the subsequent read fails or returns a different kind. Creating either kind SHALL NOT automatically attach it to other resource fields or claim that attachment rules are enforced on uploads.

#### Scenario: Default list creation

- **WHEN** the user opens the form and creates a dictionary without changing its kind
- **THEN** the selector displays «Список значений» and the request carries `group: user`, `kind: list` and `status: draft`

#### Scenario: Create additional attachment rules

- **WHEN** another rules dictionary already exists and the user selects «Правила вложений» and submits valid data
- **THEN** the request carries `group: user`, `kind: rules-attachments` and `status: draft`, and a confirmed creation opens the returned ID for the server-backed card

#### Scenario: Returned card is authoritative

- **WHEN** creation returns an ID but the subsequent card read fails or reports a kind different from the selection
- **THEN** the UI preserves the read error or displays the returned kind instead of fabricating a matching card, and does not repeat the creation request automatically

#### Scenario: Concurrent duplicate code

- **WHEN** advisory feedback found no collision but creation returns a uniqueness conflict
- **THEN** creation is not reported successful and the dialog retains the user's values, selected kind and server error

#### Scenario: Reject an unsupported kind

- **WHEN** an unsupported kind is submitted
- **THEN** no creation request is sent and the form does not report success

#### Scenario: Backend rejects a supported kind

- **WHEN** the backend rejects a selected supported kind
- **THEN** the error is shown and the selection and other input are retained without a false success

#### Scenario: Dismiss a changed kind

- **WHEN** the user changes the kind and tries to close the form, then cancels the discard confirmation
- **THEN** the form and the chosen kind remain available without creating a dictionary

#### Scenario: Pending creation

- **WHEN** creation is pending
- **THEN** the kind cannot be changed and a duplicate submission is not sent

#### Scenario: Stale creation response

- **WHEN** a creation response arrives after dismissal or session replacement
- **THEN** it cannot navigate or update the new context

### Requirement: Distinct server exports

Registry export SHALL export the complete current supported server selection, not just its loaded page, with configurable ordered fields and default name/code/type/owner/count/status selected and description/update date unselected. Card export SHALL use the distinct published detail-fields export; Values CSV SHALL export all saved values with ordinary or attachment-specific columns including attachment note. Dirty drafts SHALL not be advertised as exported. UTF-8 BOM, semicolon quoting/escaping, formula safety, server filename and row-limit errors SHALL be preserved. Invalid binary responses or missing filename MUST NOT be announced as successful exports.

#### Scenario: More results than one page

- **WHEN** registry export is requested from a paginated filtered result
- **THEN** the complete search is exported using server export semantics, or its limit failure is shown without truncated-success substitution

#### Scenario: Export with unsaved values

- **WHEN** a card has unsaved edits and values export succeeds
- **THEN** the UI identifies it as saved server values, not the dirty draft, and starts download only after validating the file response

### Requirement: Dictionary registry and card exports show a scoped result

После успешной проверки CSV-файла и передачи его браузеру экспорт реестра и экспорт карточки справочника SHALL показывать результат в том же модальном окне вместо формы. Результат SHALL содержать заголовок, визуальный признак успеха, безопасное имя файла как текст, формат CSV и число выбранных полей из именно завершившегося запроса. Признак успеха MUST NOT быть единственным обозначением результата. UI SHALL сообщать о передаче файла браузеру, а не утверждать, что он сохранён на диск.

Результат SHALL предоставлять «Назад к параметрам» и «Закрыть». Возврат SHALL сохранять выбранные поля и их порядок в рамках текущего открытия формы и MUST NOT повторять запрос или скачивание; новая выгрузка требует явного действия. Закрытие и повторное открытие SHALL показывать форму без устаревшего результата. Заголовок, фокус, клавиатурное закрытие и возврат фокуса к доступному элементу запуска SHALL соответствовать общему контракту `operation-feedback`; второй диалог и дублирующее успешное уведомление MUST NOT появляться.

Число выбранных полей SHALL относиться к параметрам успешно завершившегося экспорта и MUST NOT выдаваться за число выгруженных справочников. Число записей в файле MUST NOT подменяться счётчиком ранее загруженного реестра или вычисляться дополнительным разбором CSV. При ошибке API, ограничении выгрузки, невалидном файле, ошибке передачи браузеру, отмене или смене владельца сессии UI MUST NOT показывать успешный результат; существующее сообщение ошибки, сохранение параметров и запрет автоматического повтора SHALL сохраняться. Существующие правила запросов, проверки файла и отмены SHALL оставаться неизменными.

Это представление SHALL применяться только к экспорту реестра и карточки справочника. Отдельный CSV значений и результаты выгрузки других разделов SHALL сохранять прежнее поведение и оформление.

#### Scenario: Registry export finishes

- **WHEN** пользователь экспортирует реестр с тремя выбранными полями и сервер возвращает валидный CSV с безопасным именем файла
- **THEN** после передачи файла браузеру одно окно показывает имя, формат CSV и «выбрано полей: 3» с доступным обозначением успеха, без неподтверждённого числа справочников или утверждения о сохранении на диск

#### Scenario: Card export finishes

- **WHEN** пользователь экспортирует карточку с выбранными полями и сервер подтверждает выгрузку карточки валидным CSV
- **THEN** тот же тип результата показывает имя файла и число полей этого запроса, не объявляя выгруженными несохранённые изменения или значения справочника

#### Scenario: Return and export with different fields

- **WHEN** пользователь возвращается к параметрам, изменяет выбранные поля и явно запускает новую успешную выгрузку
- **THEN** возврат сохраняет предыдущие выбор и порядок без запроса или скачивания, а новый результат показывает число полей нового запроса

#### Scenario: Invalid or failed export

- **WHEN** сервер возвращает ошибку или превышение лимита, файл не проходит проверку либо браузеру не удалось начать передачу
- **THEN** успешный результат не показывается, объяснение ошибки и выбранные параметры остаются доступны для явного повтора

#### Scenario: Dismiss pending export or replace session

- **WHEN** пользователь закрывает диалог во время выгрузки либо владелец сессии меняется до завершения запроса
- **THEN** поздний ответ не передаёт файл другому контексту и не показывает успешный результат

#### Scenario: Keyboard dismissal and fresh opening

- **WHEN** пользователь закрывает результат клавишей Escape и снова открывает экспорт
- **THEN** фокус возвращается к доступной кнопке запуска, а новое открытие показывает форму, не прошлый результат

#### Scenario: Other export results stay unchanged

- **WHEN** пользователь запускает отдельный CSV значений справочника или выгрузку в другом разделе
- **THEN** их результат сохраняет прежнее поведение и оформление, без новой информации о выбранных полях

### Requirement: Stored lifecycle and confirmed physical deletion

Informational/user activation SHALL store active, pause SHALL store paused and resume SHALL store active through the published partial settings PUT using registry statuses. Draft activation SHALL be explicit, not draft→paused→active. Successful feedback SHALL report stored status only; paused SHALL NOT imply blocked editing or removal from downstream choices. System lifecycle controls SHALL remain read-only.

Whole-dictionary deletion SHALL require user group and explicit confirmation of physical removal of the dictionary and all its values. Only a confirmed 200 response with data.id SHALL establish deletion success; the code becomes reusable per API. System/informational deletion SHALL not be offered (API returns 405). Value/rule deletion SHALL follow user-only API restrictions, use current code and validate data.code. Backend errors including reference conflicts SHALL be preserved without claiming removal or inventing a preflight/reference/restore API. Failed/unknown requests SHALL not automatically replay.

#### Scenario: Status saved without consumer propagation

- **WHEN** a status update succeeds
- **THEN** the returned status and timestamp are shown without a consumer propagation/invalidation or upload-enforcement claim

#### Scenario: Confirm physical dictionary deletion

- **WHEN** the user confirms deletion and the API returns the matching data.id
- **THEN** the card is removed from the registry without a soft-delete or undo claim

#### Scenario: Deletion rejected or cancelled

- **WHEN** deletion is cancelled or the backend rejects it, including a reference conflict
- **THEN** cancellation sends no request and rejection retains the record/error rather than reporting successful deletion

### Requirement: Action-specific dictionary status success notifications

The dictionary card SHALL show one nonblocking success toast for each explicitly requested and server-confirmed lifecycle transition: «Справочник активирован» for draft to active, «Справочник приостановлен» for active to paused, and «Работа справочника возобновлена» for paused to active. The message SHALL distinguish activation from resumption using the status before the operation. A matching dictionary identifier and requested status SHALL be confirmed before announcing success. Feedback SHALL describe stored status only, not propagation to external consumers.

Status actions MUST NOT introduce a pre-request confirmation dialog or a modal success result. Existing dirty Save/Discard/Stay handling, deletion confirmation, mutation restrictions and unknown-outcome safeguards SHALL remain unchanged. Success feedback SHALL follow the existing operation-feedback accessibility and lifecycle rules: no focus stealing, no duplicate inline success, keyboard dismissal, and no replay on rerender, refetch or reopening the card.

#### Scenario: Activate a draft dictionary

- **WHEN** activation of a clean draft informational or user dictionary is requested and the server confirms its identifier and active status
- **THEN** «Справочник активирован» appears once as a toast, the returned status is displayed, and no confirmation dialog or modal result is added

#### Scenario: Pause and resume

- **WHEN** a confirmed active dictionary is successfully paused and subsequently explicitly resumed with matching responses
- **THEN** pause shows «Справочник приостановлен» and resume shows «Работа справочника возобновлена», each once for its operation and without downstream-effect claims

#### Scenario: Pending or unsuccessful transition

- **WHEN** a status request is pending, rejected, has an unknown outcome, or returns a mismatched identifier or status
- **THEN** no success toast for that transition appears, and existing pending, error and reconciliation behavior remains available without automatic mutation replay

#### Scenario: Dirty edits precede the transition

- **WHEN** a status action is requested with unsaved edits
- **THEN** Save/Discard/Stay remains available, Stay or failed/unconfirmed Save sends no status mutation and produces no status-success toast, and successful continuation announces the transition only after its own confirmed result

#### Scenario: Stale completion or refreshed card

- **WHEN** a completion belongs to a replaced session or another card, or the current card is rerendered, refetched or reopened after success
- **THEN** no stale or replayed status-success notification is shown

#### Scenario: Accessible notification

- **WHEN** a keyboard user completes a supported status action and focuses the toast dismissal control
- **THEN** the success is politely announced without stealing focus, remains available during interaction, and can be dismissed using the keyboard without closing the card

### Requirement: Dirty work and navigation integrity

Any editor change SHALL mark a draft dirty; clean card closure SHALL not prompt unnecessarily. Dirty interactions SHALL offer Save/Discard/Stay rather than unconditional confirmation. Discard MUST NOT silently retain unsaved mutations in shared data. Route/breadcrumb/sidebar/modal and lifecycle boundaries SHALL preserve Save/Discard/Stay semantics: failed or unconfirmed Save SHALL not navigate or launch the next destructive action, Stay SHALL preserve the draft, and Discard SHALL discard only uncommitted edits rather than promise reversal of confirmed staged commits. Page-unload handling SHALL NOT attempt automatic mutation replay; its concrete interaction policy remains a narrow editor-stage decision to record and test. Successful confirmed saves SHALL use server timestamps; failed or unknown outcomes SHALL preserve unconfirmed work and MUST NOT auto-replay mutations.

#### Scenario: Cancel dirty close

- **WHEN** the user cancels a dirty-close confirmation
- **THEN** the card and draft remain intact without saving or navigating

### Requirement: Documented consumers and storage ownership

The historical feedback, knowledge base, response templates, A/B experiments, API, system-state and dictionary-reference consumers enumerated in evidence.md SHALL remain documentary ownership context, not required new integrations in this stage. System/informational data SHALL remain domain-owned rather than duplicated in a frontend registry. Creating a user dictionary SHALL NOT automatically attach it to existing entity fields. Existing historical/inactive/unknown values SHALL remain representable without substitution by defaults. This stage SHALL NOT claim immediate propagation/publication/cache/required enforcement or require a consumer invalidation integration. Optional-module independence and separate skill/dialog lookup ownership SHALL remain unchanged.

#### Scenario: Historical inactive lookup value

- **WHEN** an existing record references an inactive or unknown code
- **THEN** its value is preserved for historical display rather than replaced by the first active choice, without changing the owning consumer's selection rules

### Requirement: Existing security and accessible failure behavior

The section SHALL preserve the existing shell permission fallback and session-owned JSON/binary transport without new permission mappings, grants or request ACL. Backend authorization SHALL remain authoritative. Local business mocks SHALL remain credential-free and absent from production. Keyboard/focus interaction, labels, status text and a non-drag ordering interaction SHALL support the same allowed operations as pointer input. Unit/component/server tests SHALL be the default verification method; browser/E2E work requires separate explicit authorization.

#### Scenario: Session replaced during export

- **WHEN** an export response completes after its session context has been replaced
- **THEN** the old file is not delivered into the new context and no synthetic permission or successful download is created

### Requirement: Dictionary diagnostics resemble the prototype without changing their meaning

Вкладка «Проверка» SHALL сохранять текущую дизайн-систему портала и быть узнаваемо близкой к предоставленному для MOS-1755 прототипу без требования пиксельного совпадения: заголовок «Что проверила система» с пояснением и действием «Перепроверить», заметная сводка и последующий вертикальный список проверок с разделёнными строками и различимыми статусами. Сводка SHALL отражать серверные passed/failed/skipped, а строки — фактические наименования, статусы, сообщения и указатели полей из ответа. Фиксированные 11/11, подписи или проверки из изображения MUST NOT подменять ответ. Успех, ошибка и пропуск SHALL различаться текстом, не только цветом или иконкой.

Возле вкладки SHALL показываться количество неуспешных проверок `failed` только после актуального успешного получения результатов для текущего справочника и владельца; доступное имя счётчика SHALL объяснять, что он относится к сохранённым данным. Пропущенные проверки MUST NOT считаться неуспешными или пройденными. Во время загрузки, ошибки, инвалидированного результата или замены владельца/карточки счётчик MUST NOT показывать неподтверждённый ноль или устаревшее значение как актуальное. При наличии пропусков интерфейс MUST NOT утверждать, что все проверки пройдены.

Действующий контракт `Published server diagnostics independent of input validation` SHALL сохраняться: проверяются сохранённые данные, не черновик; «Перепроверить» повторяет GET без записи; diagnostics не блокируют сохранение или активацию. UI MUST NOT объявлять справочник готовым к сохранению только на основании этой диагностики, автоматически сохранять изменения или добавлять автоматическую активацию из прототипа. Существующие действия и dirty-обработка SHALL сохраняться.

#### Scenario: Current diagnostics with failures and skips

- **WHEN** сервер возвращает для открытого справочника два passed, одну failed и одну skipped проверку
- **THEN** сводка и строки показывают все три статуса и серверные подписи, возле вкладки отображается одна проблема сохранённых данных и интерфейс не сообщает, что пройдены все проверки

#### Scenario: Results are not yet trustworthy

- **WHEN** проверка загружается, обновление завершилось ошибкой либо успешное сохранение инвалидировало предыдущее чтение
- **THEN** старый счётчик не представлен как актуальный и неподтверждённый ноль не показывается; ожидание или ошибка остаются различимыми

#### Scenario: Unsaved edits and a repeated check

- **WHEN** пользователь меняет черновик и нажимает «Перепроверить»
- **THEN** повторяется только GET сохранённых данных, черновик остаётся неизменным, а ни сохранение, ни активация не запускаются автоматически

#### Scenario: Keyboard and narrow screen

- **WHEN** пользователь открывает вкладку и запускает повтор проверки с клавиатуры на узком экране
- **THEN** действие, статусы, сводка и ошибки доступны и читаемы без требования пиксельного соответствия прототипу

### Requirement: Notification for confirmed added dictionary values

При полностью подтверждённом сохранении карточки справочника, в состав которого входит добавление одного или более значений либо правил, UI SHALL показывать один предметный ненавязчивый toast о сохранённых изменениях и добавленных данных вместо дублирующего общего toast. Сообщение SHALL учитывать, что одна операция Save могла также изменить другие данные. Добавление пустой строки в локальный draft MUST NOT объявляться сохранённым значением. Сохранение SHALL по-прежнему использовать действующую последовательную модель, permission-флаги, валидацию и сохранение черновика при ошибках.

Toast SHALL появляться только для подтверждённого полного результата текущего владельца и соответствовать правилам `operation-feedback`. Частичный отказ, неясный исход, несоответствие ответа желаемому draft или неподтверждённая актуальность метаданных MUST NOT объявляться полным успешным сохранением; существующие объяснения частично подтверждённых операций и дальнейшей сверки SHALL сохраняться. UI MUST NOT утверждать запись комментария в журнал или применение изменений потребителями.

#### Scenario: Save added value

- **WHEN** пользователь заполняет новую строку и сервер подтверждает все операции сохранения и необходимое обновление метаданных
- **THEN** показывается одно предметное уведомление о сохранении и добавленных данных, без дублирующего общего уведомления

#### Scenario: New row is only a draft

- **WHEN** пользователь добавил пустую строку, но не сохранил её либо ввод не прошёл валидацию
- **THEN** успешного уведомления о сохранении нет и серверное добавление не выполняется

#### Scenario: Partial or unknown outcome

- **WHEN** добавление одной строки подтверждено, а последующая операция отклонена или её исход неизвестен
- **THEN** полный успех не объявляется, подтверждённая и оставшаяся части различаются, ввод и существующая сверка сохраняются без автоматического повтора

#### Scenario: Reopen or replace owner

- **WHEN** карточка обновляется или открывается повторно после сохранения либо владелец сменился до ответа
- **THEN** старое уведомление не воспроизводится и не показывается новому владельцу
