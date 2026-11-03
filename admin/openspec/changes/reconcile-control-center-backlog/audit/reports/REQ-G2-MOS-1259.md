# Code Context

## Result and scope

REQ-G2-MOS-1259: extracted server-side personal saved-filter requirements only. Pending independent review and parent acceptance; no API, product-spec or implementation audit, delivery claim, or feature closure.

`C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `C/audit`. Paths below expand literally from these bases. MOS-1259 belongs to MOS-1246 per accepted membership report; Jira status Backlog is not acceptance evidence.

## Files Retrieved

- `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`: governing process only, fully read.
- `A/work-items/G2-FEEDBACK-REQUIREMENTS-WAVE.md:1–25`: common contract and assigned MOS-1259 section; other assignments visible but not executed.
- `A/decisions.md:1–9`: D-063, bounded register acceptance, not full lane completion.
- `A/reports/JIRA-MOS-1246.md:1–53`: accepted membership and packet limitations.
- `A/reports/G2-JIRA-MEMBER-JOINS.md:1–200` plus targeted grep passages at 277–286 and 318–320: known ownership/gap only. MOS-1259 row285 is unresolved own persistence acceptance, not evidence of missing implementation. No repeat register/audience audit.
- `A/sources/jira-feedback/r1/content.json:95–103`, JSON pointer `/items/10`, complete assigned record only; `metadata.json:1–11` complete.
- `A/sources/wiki-247734813/r1/content.json`, `/text` selective decoded excerpts and `/links` all31 entries; `metadata.json:1–11` complete. Exact deliberate text reads: Unicode zero-based half-open slices `[0:869]` (§§1–2), `[1366:3145]` (§§3.2–3.6), `[8496:8707]` (§6.1), `[10514:11134]` (§8). Earlier keyword-context extraction for сохран/фильтр/URL/localStorage produced overlapping incidental excerpts (including card/model sections), with truncated output; it is not a complete wiki read or evidence for unrelated scenarios. The narrower second extraction above supplied complete relevant sections. Tables remain flattened.
- Supervisor-directed adjacent-owner check: `A/reports/REQ-MOS-1250.md` targeted grep passages 43–58, 70–74, 95–107; `A/reviews/R-MOS-1250.md:1–110` read, with findings1 and6 used solely for accepted URL boundary. Other review contents are attributed historical claims, not a fresh API/spec/code assessment; referenced files were not opened.

### Provenance and hash verification

Both SHA-256 values were recomputed over retained content bytes using Python hashlib and match metadata:

| Source | Saved identity/time | SHA-256 |
|---|---|---|
| Jira feedback r1 | fetched `2026-10-16T11:17:16.813Z`; MOS-1259 updated `2026-10-12T20:50:17.071+0800`; issue `https://task.mos-team.ru/browse/MOS-1259` | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| Wiki247734813 r1 | `https://wiki.mos-team.ru/spaces/KR/pages/247734813/`; fetched `2026-10-16T11:17:53.564Z`; v11, versionWhen `2026-10-12T17:21:31.204+08:00` | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |

Hashes establish saved-extraction identity, not original page completeness or live freshness. Jira omitted comments, attachments and custom acceptance fields. Wiki `/links/0` is the HTML prototype attachment (version1); not fetched/read/executed. Remaining links are field-name autolinks, not external evidence; none visited. No other primary packets read.

## Key Code — primary requirement locators (no application code)

`J-D1/D2/D3` mean successive paragraphs under `h3. Описание` in `A/sources/jira-feedback/r1/content.json#/items/10/description` (physical line102). `J-A1` through `J-A6` mean its six ordered `#` acceptance bullets. `W§n` means the named section of `A/sources/wiki-247734813/r1/content.json#/text` (physical line8), located by exact heading/quote, not invented table rows.

J-D1: “персональные именованные отборы на сервере: создание, список, применение, явное обновление выбранного фильтра и удаление”. J-D2 names prefix `/api/control/api/v1/managed-resources`, `POST/GET /saved-filters`, `GET/PATCH/DELETE /saved-filters/{filter_id}`, `resource=feedback-surveys`. These are source-stated operation requirements, not verified published transport or backend availability.

### Atomic requirements

Actor throughout: user of Feedback saved filters, with UI action permission as R22; backend determines ownership, not a client-supplied identity. Verification column describes future unit/component checks, none executed. All R rows are explicit Jira requirements; wiki correlations do not create a precedence rule.

| ID | Trigger → expected behavior | Primary locator / exact clause | Verification need / boundary |
|---|---|---|---|
| R01 | Save a named selection → personal server persistence. | J-D1 “персональные именованные отборы на сервере” | Persisted record, not browser-only success. No shared/team catalog inferred. |
| R02 | Enter title → accept length1–150, reject whitespace-only title. | J-A1 “Имя 1–150 символов, не только пробелы” | Empty, whitespace,1,150,151; trimming, Unicode counting and case normalization unspecified. |
| R03 | Save search → preserve query. | J-A1 “search содержит query” | Round-trip query, not new search matching rules. |
| R04 | Save search → preserve multiselect filters. | J-A1 “мультифильтры” | Multiple selected values survive; supported fields belong to basic-search owner. |
| R05 | Save search → preserve conditions. | J-A1 “conditions” | Conditions round-trip; condition editing is MOS-1258. |
| R06 | Save search → preserve sort. | J-A1 “sort” | Non-default sort survives. No new sorting options. |
| R07 | Save search → include limit and offset. | J-A1 “limit/offset” | Persist both; apply offset exception is R17, not omission from storage. |
| R08 | Create → receive record ID. | J-A1 “POST возвращает ID”; J-D2 | Distinguish created IDs even for same title; ID format unspecified. |
| R09 | Read saved detail → GET by filter identity. | J-A1 “detail читается GET”; J-D2 `/saved-filters/{filter_id}` | Detail retrieval, not deriving identity from name. |
| R10 | Request list → scope to `resource=feedback-surveys`. | J-A2 “Список запрашивается с resource=feedback-surveys”; J-D2 | Resource isolation; not all saved-filter consumers. |
| R11 | Browse saved-filter list → its own server pagination. | J-A2 “собственной серверной пагинацией” | Paging independent of survey-result paging; defaults/order unspecified. |
| R12 | Access record → backend determines owner. | J-A2 “Владельца определяет backend” | Do not infer/set authority from frontend profile; no new auth model. |
| R13 | Access another user's or absent filter → same404 outcome. | J-A2 “чужой/отсутствующий фильтр одинаково 404” | Both cases; no existence-disclosing distinction required. |
| R14 | Create with same name → create new record, allow duplicates. | J-A3 “Одинаковые имена допустимы: создание создаёт новую запись” | Two distinct IDs; no name-based overwrite. |
| R15 | Explicitly update selected filter → separate PATCH of selected ID. | J-D1; J-A3 “отдельный PATCH выбранного ID” | Choose duplicate-name record by ID and update only it; selection widget unspecified. |
| R16 | Update → send full search without changing resource. | J-A3 “с полным search, без смены resource” | Full replacement input and fixed resource; wire merge/concurrency semantics not audited. |
| R17 | Apply → restore entire selection and limit, start at offset0. | J-A4 “восстанавливает весь отбор и limit, начинает с offset=0” | Query/multifilters/conditions/sort/limit together; nonzero stored offset does not restore current result page. |
| R18 | Apply obsolete/unsupported parameters → no unexplained partial application. | J-A4 “не применяются частично без пояснения” | Stale and unsupported search; wording does not select total rejection versus explained recovery. |
| R19 | Storage/validation failure → no false success. | J-A5 “Ошибки хранения/валидации, включая /search/... и пустой PATCH, не вызывают ложный успех” | Storage failure, nested validation path and empty PATCH; no invented HTTP status mapping. |
| R20 | Same failures → preserve user input. | J-A5 “потерю ввода” | Input survives each failure; retry workflow unspecified. |
| R21 | Same failures → no localStorage fallback. | J-A5 “или fallback в localStorage” | Failure remains honest; no offline persistence substitution. |
| R22 | User invokes action → UI uses matching ManagedResource read/create/update/delete permission. | J-A6 “ManagedResource:read/create/update/delete по действию” | Action-level UI checks; backend authorization remains separate, not a new role editor. |
| R23 | User deletes saved filter → delete operation exists for filter ID. | J-D1 “удаление”; J-D2 `DELETE /saved-filters/{filter_id}`; W§3.5 “применить или удалить (крестик)” | Correct record deleted; confirmation, active-selection aftermath and pagination recovery unspecified. |
| R24 | Acceptance verification → unit/component coverage for duplicate names, full restoration, PATCH by ID, pagination,404 and stale search. | J-A6 final sentence | Six named required scenarios; not E2E and not a claim of existing/passing tests. |

### Wiki clauses, example-only UI and explicit deferral

- W§3.5 `“Сохранить текущий фильтр … сохраняет поиск, мультиселекты и расширенные условия под именем”` corroborates named search persistence; next sentence `“Дубликат по имени перезаписывается”` conflicts with J-A3. J-D3 explicitly states `“Автоматическая перезапись по имени из прототипа не входит в первый этап”`: preserve that first-stage exclusion, without a general Jira-over-wiki rule or promise of later delivery.
- W§3.5 `“Сохранённые фильтры — список с возможностью применить или удалить (крестик)”` corroborates list/apply/delete. Ellipsis-menu and cross affordances are prototype UI detail, not automatically adopted production acceptance requirements.
- W§6.1 describes bottom-right two-second toasts, including save/apply. This is example UI detail; J-A5's honest success/error behavior is explicit, but exact toast placement/duration is not confirmed product scope.
- W§8 `“Серверная валидация — всё выполняется на клиенте, данные живут в памяти браузера и теряются при перезагрузке”` describes prototype limitations, contrasting with J-D1 server persistence and J-A5. It does not authorize production browser-memory persistence or establish saved-filter-specific localStorage implementation.
- W§3.2–3.4 contextualize search/multifilters/conditions only; do not repeat their registry/audience audit or automatically import every prototype field/operator into saved search.

## Architecture — requirement ownership, not implementation

MOS-1259 consumes the selection model: save/list/detail → select a record ID → explicit apply/update/delete. Persisted search contains offset, but apply resets result offset to0. Saved-filter list has separate pagination. Duplicate title is not identity. Ownership is backend-controlled; UI permissions are action-dependent.

J-D3 explicitly names prerequisites MOS-1250 and MOS-1258. Basic search/common search-URL model remains MOS-1250; conditions editor remains MOS-1258. Transport review is a separate lane. Accepted member register row285 already says shared MOS-1249 contract/client delegation does not constitute this consumer's persistence acceptance; this report adds no duplicate finding and certifies no shared consumers delivered.

### URL boundary resolved by attributed accepted evidence

W§3.5 says `“Скопировать ссылку на отбор — формирует URL с параметрами q, status, type и копирует в буфер”`. Material ownership question was raised to supervisor; supervisor directed reuse of accepted adjacent evidence rather than inventing scope. `reports/REQ-MOS-1250.md:45–49,58,74` identifies REQ-1250-24–28 and quotes MOS-1250 description ownership of basic filters/common search-URL. `reviews/R-MOS-1250.md` findings1 and6 accept complete applied-search URL/history/copy requirements, future conditions qualification, malformed-URL explanation and honest clipboard success; they retain the narrower wiki wording as mismatch, not downgrade authority. This is attributed adjacent-owner evidence, not a fresh read of MOS-1250's primary record or its plan.

Thus copy-link delivery is not assigned to MOS-1259 merely because it shares the wiki menu. Whether applying a saved filter pushes/replaces history, encodes a filter ID, or restores selected-filter identity from URL remains unspecified in the inspected MOS-1259 clauses. Do not invent such integration mechanics or reopen known URL ownership.

## Unknowns and verification boundaries

- No saved-search schema version field, version numbering, migration algorithm, optimistic lock/ETag, or concurrent-update rule is specified in the inspected assigned description/wiki clauses. R18 is compatibility behavior, not proof that version metadata exists or is absent in an API.
- Exact supported search structure, request/response DTOs, title normalization, sorting of saved-filter list, pagination bounds, rename semantics, delete confirmation/undo, applying after404, and effect of deleting an active selection are not established here. These are bounded source-detail unknowns, not confirmed missing requirements or permission to invent defaults.
- Preserve R18's precise question for an owning-plan/product follow-up if a design choice is needed: reject incompatible search entirely, or allow explained partial recovery? The source only forbids unexplained partial application; this extraction does not select a recovery policy.
- Omitted Jira comments/custom acceptance fields and unread attachment structure are **unavailable evidence**, not evidence that requirements do not exist. No selection layout, accessibility flow or version field may be reconstructed from an unexecuted prototype.
- Unit/component checks in R rows are verification needs, not executed tests. No network/browser, tests/build, API/schema/product-spec/code reading, nested delegation, source-example execution, or changes outside this report.

## Start Here

Open `A/sources/jira-feedback/r1/content.json:95–103` (`/items/10/description`) first: its six AC bullets are the primary bounded contract. Compare W§3.5 and §8 using saved locators, and reuse the accepted MOS-1250 URL boundary. Independent reviewer and parent decide acceptance; no R/A/S/I completeness asserted.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Extracted 24 stable MOS-1259 requirement rows with primary description/AC locators, relevant wiki clauses, explicit first-stage exclusion, ownership and source limits."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1259.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find/grep and narrow Python JSON/hashlib inspection","result":"passed","summary":"Both retained source hashes match metadata; complete assigned description and targeted wiki sections inspected."},{"command":"Tests/build/browser/network","result":"not-run","summary":"Prohibited in requirements-only task."}],
  "validationOutput": ["Jira SHA-256 890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685 matched.","Wiki SHA-256 d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7 matched."],
  "residualRisks": ["Jira selected fields omit comments/attachments/custom acceptance fields; wiki is flattened and attachment unread.","Incompatible-search recovery and saved-filter-to-URL mechanics remain unspecified; no behavior chosen.","Independent review/parent acceptance and separate API/spec/implementation lanes remain pending."],
  "noStagedFiles": false,
  "diffSummary": "Only configured requirements report written; no project/source modifications.",
  "reviewFindings": ["Prototype name-overwrite and in-memory behavior differ from explicit first-stage Jira saved-filter contract; no generalized source precedence selected."],
  "manualNotes": "Index state not inspected (noStagedFiles=false is not evidence of staged changes). Material URL ownership question was resolved via supervisor-directed accepted adjacent report/review, without new product semantics. No runtime validation performed."
}
```
