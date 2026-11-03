# SCENARIO-MOS-923 — bounded evidence-to-plan findings

## Result and boundary

Maintenance-window requirements are substantially described in wiki page version 4 and represented by five published OpenAPI operations. Publication does **not** establish runtime support, delivery, approval, or authorization to activate a feature. LOCAL001 discovery found an existing shell/access capability, but no dedicated active MOS-923 change or main maintenance-window CRUD capability. The adjacent MOS-1026 change is read-only skill operations information, not this editor. No plan was created, task closed, source precedence chosen, or lifecycle activated.

Only this report was intentionally written. No product/source/code edits, network, MCP, browser, tests, build, generation, or nested delegation. HTML was decoded as inert text, never rendered/executed. No index attestations are made. No blocker prevented this bounded analysis; unresolved implementation decisions are listed below, not silently resolved.

## Evidence and provenance

All paths below are relative to the repository. `A` means `openspec/changes/reconcile-control-center-backlog/audit`; JSON pointers identify exact source locations (more precise than single-line serialized HTML).

| Evidence | Verification and locators |
|---|---|
| `A/sources/jira-operations-details/r1/content.json`, corresponding `metadata.json` | Recomputed SHA-256 `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f`, 9,933 bytes, matching supplied hash and metadata. Read only business items `/items/1` MOS-754 and `/items/4` MOS-923. Metadata capture `2026-10-16T13:02:57.872Z`, reports parent verified-origin GET. MOS-754 status Review, updated `2026-10-16T19:22:17.361+0800`; MOS-923 status Backlog, updated `2026-10-15T14:46:40.107+0800`. Both have zero comments and empty attachments/subtasks in this capture. These statuses are not acceptance or delivery proof. |
| `A/sources/wiki-241092242/r1/content.json`, corresponding `metadata.json` | Recomputed SHA-256 `e7b78965be979f2bd450b25881574cf7e8b94cf424be5d052bb2be9df1995158`, 68,316 bytes, matching supplied hash and metadata. `/url` is `https://wiki.mos-team.ru/rest/api/content/241092242?expand=body.view,version`; saved status 200, capture `2026-10-16T13:03:14.883Z`. `/version/number` 4, `/version/when` `2026-09-25T16:59:13.813+08:00`; page body labels contract v1.0. Page revision 4 is not contract version 4. Metadata attachments status 200/count 0/next null. No attachment evidence is assumed. |
| `A/sources/api-live/r1/content.json`, corresponding `metadata.json` | Recomputed SHA-256 `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`, 413,007 bytes, matching metadata. Saved Swagger-discovered URL `https://nchat-a-tech.mos.ru/api/control/openapi.json`, capture `2026-10-16T11:13:29.451Z`; `/info` title TSAM Assistant Management Service, version `0.1.0`. No ETag/Last-Modified. Capture method is metadata's provenance claim, not an independently repeated network verification. No business operation invoked. |

Wiki references below mean `/bodyView` under the exact numbered headings and named subsections. Reviewed: general business rules/data/envelope; §§1.1, 1.2 and TargetObject, 1.4 and Fields, 1.5; §§2.5–2.10 and their request/response/rules subsections. Stub overlap is only a dependency; stub editing belongs to MOS-922.

## Atomic candidate register

Stable IDs below are **candidates**, not newly approved requirements. “Gap” means missing dedicated planning coverage in the bounded local discovery, not a code defect or verified absence of implementation. `J` = Jira `/items/4/description`; `W` = wiki headings above; `S` = saved OpenAPI `/components/schemas/`.

| ID | Candidate and exact primary locator | Coverage / disposition |
|---|---|---|
| MOS923-C01 | List windows with state, target_type, title query and limit/offset; show returned pagination. W §2.5 “Параметры запроса”, “Успешный ответ”; J list requirement. | Published GET collection plus `MaintenanceWindowListResponse`, `MaintenanceWindowListItemResponse`, `PaginationDto`. Gap: dedicated scenario plan. Keep shell entry; defer activation. |
| MOS923-C02 | Explicit title input. J; W §1.4 Fields/title, §2.6 request; S `CreateMaintenanceWindowRequest/properties/title`. | Required string on create; no published nonempty/length constraint. Candidate gap; question limits, do not invent them. |
| MOS923-C03 | Explicit valid timezone. J; W §1.4 Fields/timezone and §2.6 checks; S create/timezone. | Required string, not an enum or encoded timezone validator. Candidate gap; questions Q02. |
| MOS923-C04 | Explicit starts_at. J; W §§1.4, 2.6; S create/starts_at. | Required date-time. Preserve RFC3339 offset semantics from W “Формат данных”; no browser-zone default. |
| MOS923-C05 | Explicit ends_at, strictly later than starts_at. W §2.6 checks; S create/ends_at. | Date-time represented; cross-field order is wiki prose, not schema validation proof. Candidate gap. |
| MOS923-C06 | Explicit warning_ahead_minutes, integer ≥0. J; W §§1.4, 2.6 checks; S create/warning_ahead_minutes. | Schema minimum 0 agrees. Upper limit / warning already in past unanswered, Q02. |
| MOS923-C07 | At least one scope.targets entry, each type/id/name; assistant stable key `assistant`, other target IDs UUIDv7 per wiki. W §1.2 TargetObject, §1.4, §2.6 checks; S `MaintenanceScopeRequest`, `TargetObjectRequest`, `MaintenanceTargetType`. | Four types agree. Schema has neither minItems nor UUIDv7/string-key constraints. Target discovery unresolved, Q05; not permission scopes and not stub editing. |
| MOS923-C08 | banner_text for active work. J; W §1.4 Fields and §2.6 request; S create/banner_text, `MaintenanceWindowResponse`. | Nullable text; create schema optional, detail required-nullable. Preserve distinction; Q04. |
| MOS923-C09 | stub_text for active work. Same locators, field stub_text. | Same requiredness distinction; window-owned text, not ordinary stub editor. |
| MOS923-C10 | warning_banner_text before start. W §1.4 Fields and §2.6 request; S create/warning_banner_text. | Same requiredness distinction; no invented text fallback or random defaults. |
| MOS923-C11 | Explicit integer priority; server owns overlap result. J final sentence; W §§1.5 and 2.6 checks; S create/priority. | Required integer with no bounds/default in schema. Keep server authority; questions Q03. |
| MOS923-C12 | Display API draft/scheduled/active/completed/canceled and is_currently_applied without deriving status locally. J; W §§1.1, 1.4, 2.5–2.9; S `MaintenanceWindowState` and response schemas. | Five states agree; completed automatic, canceled manual in wiki. Draft creation/publication commands unanswered Q01. |
| MOS923-C13 | Create via POST, read detail via GET; required contract inputs visible and deliberate, no hidden random defaults. J; W §§2.6–2.7. | Published operations and create/detail DTOs exist; create returns summary, detail supplies timezone/scope/text/by. Candidate gap, not runtime verification. |
| MOS923-C14 | Before start edit all fields; after start freeze starts_at/timezone/scope.targets; allow ends_at/texts/warning_ahead_minutes. W §2.8 “Правила изменения”. | PUT with `UpdateMaintenanceWindowRequest` published; schema cannot express state restrictions. Active title/priority/application changes unspecified, Q04. |
| MOS923-C15 | Completed and canceled windows cannot be edited. W business rules and §2.8. | Enum represented; operation schema does not prove enforcement. Keep terminal-state boundary. |
| MOS923-C16 | Cancel draft/scheduled/active with reason; completed cannot cancel; canceled window stops affecting output. W §2.9 request/rules; S `CancelMaintenanceWindowRequest`, mutation response. | POST cancel requires reason string. Race completing during cancel returns conflict and asks refresh; preserve, do not report success. Repeated cancel semantics Q06. |
| MOS923-C17 | Server chooses text winner: active maintenance over ordinary stub; greater priority; then specificity surface > skill > module > assistant; then later updated_at. Completed window no longer affects text. W §1.5; J server authority. | Keep documented rules as explanations, not frontend scheduling/overlap algorithm. Conflict rule tension Q03. |
| MOS923-C18 | Preserve validation field errors and state/overlap conflicts, distinguish failure from empty/success. W §2.10; S `ErrorItem`, `HTTPValidationError`. | Wiki domain errors and published 422 shape differ in representation; Q06. No runtime guarantees inferred. |

## Published API versus wiki — no precedence decision

Exact operations: saved OpenAPI `/paths` keys `/api/control/api/maintenance/v1/maintenance-windows` (GET, POST), same path plus `/{window_id}` (GET, PUT), plus `/{window_id}/cancel` (POST). Wiki §§2.5–2.9 instead specify `/api/control/api/assistant-ops/v1/maintenance-windows`. This is a concrete namespace discrepancy, **not** “API absent” and not permission to rewrite a contract or choose the newer-looking source.

Common ground: five operations, state/target enums, create required title/priority/timezone/start/end/warning/scope, nullable text fields, list pagination and summaries, detail metadata, summary mutation responses. Published list limit is 1–100 with default 20, offset minimum/default 0; these explicit pagination defaults do not justify hidden business-form defaults.

Additional representational differences:
- Wiki TargetObject uses UUIDv7 for module/skill/surface and stable assistant key; OpenAPI target IDs are unconstrained strings, window IDs generic `uuid`, `by.id` string rather than wiki UUID. Missing schema constraints do not prove backend accepts invalid IDs.
- Wiki requires at least one target and valid timezone; OpenAPI does not encode minItems, timezone validity, interval ordering, state-sensitive mutation constraints or overlap rules. No source precedence or runtime enforcement inferred.
- Wiki detail Fields marks all three text properties required-nullable. Published detail agrees; published create omits these from required. The wiki create example supplies them but is not itself a formal required-list for requests.
- PUT schema has all fields optional-nullable, including timezone and is_currently_applied, and no state field. Wiki PUT example includes is_currently_applied and omits timezone; rules—not the example alone—freeze timezone after start. Omission/null semantics and write authority require clarification.
- All five operations document success and 422 `HTTPValidationError` (`detail[].loc/msg/type`), not the wiki's general envelope for every response. Success envelopes reference `ErrorItem`; `ResponseCode` is a string, not a guaranteed success literal. Wiki §2.10 names 400 INVALID_ARGUMENT, 404 NOT_FOUND, 409 MAINTENANCE_WINDOW_CONFLICT / ALREADY_STARTED / FINISHED / CANCELED and 422 VALIDATION_ERROR, plus auth failures. Lack of those responses in OpenAPI is a documentation gap, not proof they never occur.

## Precise open questions

- **MOS923-Q01 — state commands (C12–C13):** Which operation creates a draft or publishes/schedules it? Neither create nor update schema exposes state; wiki create example returns scheduled. How are past/immediate starts handled? Do not manufacture publish/activate endpoints or treat is_currently_applied as a lifecycle command.
- **MOS923-Q02 — time/DST/order (C03–C06):** What timezone identifier set is valid; how must RFC3339 offset agree with named zone? How are DST nonexistent/ambiguous local times rejected or disambiguated? Is interval-end exclusive for adjoining windows? What limits apply to warning horizon and end extension/shortening across server “now”? Strict starts_at < ends_at and nonnegative warnings are already answered; no need to reopen them. Specify server-clock boundary behavior, not a client clock algorithm.
- **MOS923-Q03 — overlap/priority (C11, C17):** Reconcile §2.6/§2.8 same-priority/same-scope conflict with §1.5 updated_at tie-break. Does “same scope” mean equal target set or any intersecting/hierarchical target? How is specificity determined for a mixed target array and what happens on equal updated_at? Which existing states participate in conflict checks? What priority range is valid, and what exactly does explicitly higher priority mean when overlap is allowed? Server remains authoritative throughout.
- **MOS923-Q04 — edit semantics (C08–C10, C14–C15):** Are active title and priority editable (not listed in either active allow/deny set)? Is is_currently_applied writable or informational? Does null clear versus omission preserve each optional PUT property? Are empty texts distinct from null and are any text fields mandatory for scheduling? Is there an explicit transfer operation implied by general business rules, or only pre-start PUT/cancel? Do not invent one.
- **MOS923-Q05 — scope references (C07):** Which agreed read API supplies eligible target IDs/names, especially assistant/module, and how are stale/deleted/duplicate targets handled? List filtering offers target_type, not target_id, so publication does not directly supply a skill-ID maintenance feed for MOS-1026. Stub catalog is a possible dependency to clarify, not assumed complete target directory.
- **MOS923-Q06 — concurrency/errors (C16, C18):** What optimistic concurrency/version/ETag or idempotency contract, if any, applies to create/update/cancel? updated_at is returned but no compare token/header is published here. What response distinguishes concurrent edit, completion race, repeated cancel, and unknown mutation outcome? Confirm actual domain-error envelopes versus published 422 detail. Preserve documented completion-during-cancel conflict and explicit refresh; do not invent automatic replay, last-write-wins, or server idempotency guarantees.
- **MOS923-Q07 — source alignment:** Owners must reconcile namespace and schema/prose differences above before a consumer contract decision. Published API version 0.1.0, wiki contract v1.0/page revision 4 and Jira status carry different meanings; none establishes precedence.

## LOCAL001: existing coverage and narrow dispositions

Discovery used directory/path enumeration of `openspec/changes` and `openspec/specs`, then scoped text search of active proposal/design/tasks/specs and main specs for MOS-923, maintenance and Russian maintenance-window terms. No dedicated maintenance-window change/main capability found in that bounded surface. This is not an exhaustive code audit.

Files retrieved for local coverage:
- `openspec/specs/control-center-shell/spec.md`, lines 144–218: canonical route/legacy redirect, URL tabs, access and honest unfinished content; search also located breadcrumbs at 266–267.
- `openspec/specs/control-center-permissions/spec.md`, lines 1–91: full current permission policy.
- `openspec/changes/mos-1026-skill-operations-info/proposal.md`, lines 1–27; `design.md`, lines 1–26; `tasks.md`, lines 1–18; `specs/skill-operations-info/spec.md`, lines 1–47: read in full. Its API gate and unchecked tasks remain unchanged.
- Prerequisites read in full: archived `2026-10-09-integrate-mpmm-auth-permissions/{proposal,design}.md` and all six `specs/*/spec.md`; archived `2026-09-28-update-control-center-routing/{proposal,design,tasks}.md` and its shell delta spec. Historical unchecked/checked tasks are recorded history, not this audit's validation. No auth implementation or routing code was audited. Demo behavior and shadcn implementation were not analyzed or proposed, so no demo/shadcn change is inferred.

| Surface | Finding | Disposition |
|---|---|---|
| Shell entry | Main shell lines 144–194 already specify `/ops?tab=maintenance`, `/ops/maintenance` compatibility redirect, basename/query/history/access. Lines 216–218 retain honest unfinished-content boundary. | **KEEP / no-op** on route capability; no duplicate route plan. Any future scoped content correction must preserve this boundary until separately authorized. |
| Permissions | Main permission lines 23–38 explicitly reserve maintenance reads/writes to confirmed explicit `*` pending agreed granular mapping. Lines 60–91 preserve backend authorization and server-owned scopes. | **KEEP / no-op**. Do not invent `TSAM.Maintenance:*`, reuse Module permissions, infer grants from role names or map window scope to authorization scope. |
| MOS-1026 | Proposal read-only works; design line 13 and tasks 1.1 retain API gate for broader skill operational sources. Spec lines 7–19 covers read-only period/reason, not window CRUD. | **KEEP** its gate; **QUESTION** whether a future agreed read projection can reuse maintenance. Do not close it based on these five operations or fold MOS-923 into it. |
| MOS-923 business scenario | C01–C18 have primary-source basis but no dedicated local CRUD planning coverage found. | **DEFER** plan creation/activation. Narrow correction candidate is evidence-backed coverage of these atoms after owner decisions, not a generated plan here. |
| Backend-context wording | MOS-754 requests contract preparation and examples, not delivered behavior. Five operations now have saved publication evidence. | **UPDATE candidate only:** distinguish “published contract exists with discrepancies” from blanket “no API”, while retaining acceptance/runtime gates. Do not mark MOS-754 done or edit other lanes. |
| Stub dependency | Maintenance text overrides ordinary stubs, shared TargetObject vocabulary. | **DEFER** catalog/editor/preview changes to MOS-922; no whole operations audit. |

## Approved gates and residual risks

The auth prerequisite preserves real-mode shared MPMM session, confirmed `/me`, configured credential destination boundary, both raw auth headers, no automatic mutation replay and backend authorization. Saved maintenance operations show separate AdminToken/AccessToken security alternatives; this publication detail does not undo the approved paired-header policy or prove enforcement. Maintenance UI's explicit `*` is not global object access and does not activate missing functionality. No new grants or auth models are proposed.

Runtime/deployment verification, business-contract alignment and independent review remain outstanding. General auth release gates (shared session availability, CORS, refresh behavior and server permission/object-scope enforcement) are not satisfied by this read-only capture. No tests/build/API generation were run; prohibited browser/E2E work remains untouched. No product gap is labeled a verified code defect. No git index or staged-file state was inspected or attested.

## Start here

Read wiki `/bodyView` §2.8 “Правила изменения” alongside saved OpenAPI `UpdateMaintenanceWindowRequest`: it exposes the most consequential active-window/nullable-write ambiguities. Then resolve Q07 namespace alignment and Q01 lifecycle commands without choosing source precedence. Retain the existing shell/access capability unchanged pending a separately authorized plan.
