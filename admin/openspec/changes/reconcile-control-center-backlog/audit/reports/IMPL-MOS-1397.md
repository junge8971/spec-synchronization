# IMPL-MOS-1397 — global metric-settings boundary

## Result

**No global monitoring-settings editor, client, schema or mock operation was established in the inspected local implementation.** The global Analytics API supports dashboard composition—not MOS-1397 threshold settings. Its board-save and dashboard-refresh assertions must not be credited as monitoring-settings persistence or dependency synchronization.

MOS-1397 itself requests **skill-scoped** settings and conditionally approved writes; it does not establish a global-settings product requirement. Preserve that distinction rather than inventing a global editor.

This is supplemental evidence for an already-P member: **zero U→P transitions**, no task closure, no publication or queue mutation. Parent acceptance and independent review remain required.

## Scope and prior evidence

Assignment: `openspec/changes/reconcile-control-center-backlog/audit/work-items/WAVE-D094-LOCAL-EIGHT.md`, row **IMPL-MOS-1397** only.

Prior discovery inputs:

- `audit/reports/SCENARIO-MOS-1397.md`: fourteen documentary mappings, requested backend semantics and conditional writes.
- `audit/reviews/R-SCENARIO-MOS-1397.md`: accepted without mandatory corrections.
- `audit/reports/IMPL-SKILL-MONITORING.md`: accepted per-skill implementation no-op; not re-audited here.
- `audit/decisions.md:585–597`, **D-014**: conditional settings/refresh remain unapproved UI work; requested errors already include 422 and existing 401/403/404.
- `audit/decisions.md:89–95`, **D-082**, and `audit/reviews/R-SKILL-OBSERVABILITY-BATCH.md`: preserve monitoring no-op and earlier documentary questions.
- D-093/current assignment supplies the existing population baseline; no independent population census performed.

The scenario report/review, implementation report and controlling decision excerpts were read before current implementation inspection. The observability batch review was located and read subsequently as corroboration.

No repeated per-skill mounted-tab analysis or wiki requirement audit was undertaken.

## Exact primary source

Prefix `A = openspec/changes/reconcile-control-center-backlog/audit/`.

Source: `A/sources/jira-monitoring-details/r1/content.json`.

| Pointer | Observed saved evidence |
|---|---|
| `/sourceId`, `/revision`, `/retrievedAt` | `jira-monitoring-details`, revision 1, captured `2026-10-16T13:48:06.559Z` |
| `/items/2/key`, `/items/2/summary` | MOS-1397, `[B] Мониторинг навыка` |
| `/items/2/updated`, `/items/2/status/name` | `2026-10-16T19:24:19.539+0800`, `Development` |
| `/items/2/description`, “Хранение” | One settings row per skill; four thresholds, optional fallback and coherent maintenance window |
| Same description, “API чтения” | GET `/api/control/api/skills/v1/skills/{skill_id}/monitoring`; settings may be null; reading creates no rows |
| Same description, “Операции записи после подтверждения сценария подключения” | Conditional PUT settings and bodyless POST refresh |
| `/items/2/attachment`, `/items/2/comment` | No attachments; zero comments, total zero |

The complete selected description was inspected. These saved requirements and issue status do not establish delivery or current external freshness.

## New evidence delta

The earlier scenario audit inspected no application code. The per-skill implementation audit explicitly excluded operational/global settings and did not recensus the current OpenAPI. This report adds:

1. The actual global `/ops` and `/metrics` route boundaries.
2. Current combined contract and generated-type identifier searches.
3. The distinction between board composition writes and monitoring threshold writes.
4. Connected mock registration and concrete board/dashboard assertions.
5. Bounded absence findings without promoting them into backend nonexistence.

### Expected / observed / unknown

| Boundary | Expected from selected source or existing owner | Observed local evidence | Unknown / limit |
|---|---|---|---|
| Global settings surface | No global editor is specified by MOS-1397; its settings belong to a skill | `app/shared/config/constants/application-routes.constants.ts` maps `/metrics` to dashboard and `/ops` to operations. `app/routes/dashboard.tsx:1–5` renders `PlaceholderPage`. `app/routes/operations.tsx:1` exports `OperationsPage`; `app/pages/operations/ui/operations-page.tsx:6–29` renders tabs containing “Раздел в разработке” | No conclusion about historical interfaces, uninspected external applications or deployment |
| Global operations tabs | Do not infer a metric editor from a section name | `app/shared/config/constants/section-tabs.constants.ts:21–28`: modules, stubs, maintenance only. The mounted page contains no form, settings query or save mutation | No new tab or product policy proposed |
| Monitoring read/schema | Requested GET returns settings, dependencies, metrics, source, observation time, deviations and evaluation state | Current `docs/api/contracts/openapi.json` has 94 paths and 380 schemas. Exact searches found no `monitoring`, four `threshold_*` names, `evaluation_status` or `dependency_statuses`. Generated `app/shared/api/schema.d.ts` is included in the corresponding app search | Local contract absence does not prove backend absence or external publication absence |
| Monitoring settings write | Conditional PUT fully replaces four required thresholds; omitted optional fields become null; subsequent saves preserve id/created_at | No matching settings endpoint/schema/client identifiers in the bounded app/contract search. Global board PUT instead accepts `version` and `widgets` | No executed validation, durable storage, SQL constraints, identity preservation or authorization evidence for MOS-1397 |
| Refresh | Conditional bodyless monitoring refresh atomically synchronizes dependencies | Analytics refresh is a different operation: POST `/api/control/api/analytics/v1/dashboard/refresh` requires `DashboardFilterRequest`. `mocks/analytics.mjs:70–74` updates `calculatedAt`; it does not synchronize dependencies | No evidence of monitoring locking, rollback, stable dependency IDs or same-snapshot semantics |
| Global board persistence | Analytics composition must not substitute for threshold settings | `/components/schemas/SaveBoardRequest` requires integer `version ≥ 0` and string-array `widgets`; `/components/schemas/BoardResponse` requires version/is_default/widgets. `mocks/analytics.mjs:85–105` replaces in-memory board composition, increments version, rejects stale version/duplicate or unavailable widgets | This is local application-state persistence only, not monitoring settings or durable backend persistence |
| Mock provider | MOS-1397 requests reproducible fixture metrics and explicit `source="mock"` | `mocks/analytics.mjs:3–19,44–68` supplies a demo widget catalog, zero sample, null widget values and calculation time. It is not the requested skill-monitoring provider | No real telemetry, monitoring fixture coverage or backend provider delivery established |
| Tests | MOS-1397 needs its own settings/read/boundary assertions after approval and contract agreement | Existing assertions cover route configuration and Analytics board/dashboard behavior, detailed below | Test execution and MOS-1397 persistence/validation correctness remain unverified |

### Contract locators

Current local combined contract: `docs/api/contracts/openapi.json`.

Exact JSON pointers:

- `/paths/~1api~1control~1api~1analytics~1v1~1board/get`
- `/paths/~1api~1control~1api~1analytics~1v1~1board/put`
- `/paths/~1api~1control~1api~1analytics~1v1~1dashboard~1refresh/post/requestBody`
- `/components/schemas/SaveBoardRequest`
- `/components/schemas/BoardResponse`

`docs/api/contracts/analytics-dashboard.md` explicitly describes five Analytics operations, board optimistic locking, required refresh body and the distinction between a contract and an implemented analytics interface.

`mocks/contract.mjs:6–8` loads this combined contract. `mocks/app.mjs:35–53,61–101` registers handlers against its operations; `:105–106` supplies the unknown-operation 404 fallback. Static wiring was inspected, not executed.

### Actual assertions, not executed

- `app/routes.test.ts:9–20`: every catalog entry is registered with an existing route module. This does not assert a functioning monitoring editor.
- `app/shared/config/application-routes.test.ts:29–36`: valid section-tab selection and default fallback for null/empty/unknown values.
- Same file `:38–65`: global Analytics and Operations navigation entries. Navigation presence is not feature delivery.
- `mocks/contract.test.mjs:427–450`: board defaults, saved composition/version, subsequent GET, catalog `on_board`, dashboard refresh timestamp, no-store and widget count.
- `mocks/skills-status-analytics.test.mjs:218–269`: invalid board bodies and duplicate widgets yield 422; unknown widget yields 400; failed writes preserve board; successful replacement increments version; stale version yields 409; invalid refresh/period inputs yield 422; a fresh app resets board state.

None of those inspected assertions tests monitoring threshold ranges/precision, all-or-null maintenance windows, settings identity retention, monitoring GET nonmutation, threshold equality, or atomic dependency refresh. The fresh-app reset assertion specifically prevents treating the board mock as durable storage evidence.

### Bounded search method

Read-only Python inspected text files with extensions `.ts`, `.tsx`, `.mjs`, `.json`, `.md`, `.raw` under:

- `app`: 921 files;
- `mocks`: 89 files;
- `docs/api/contracts`: 33 files.

Each root returned zero exact matches for:

```text
monitoring
threshold_availability
threshold_rating
threshold_response_seconds
threshold_data_age_days
evaluation_status
dependency_statuses
```

This is an identifier-bound search, not a semantic proof that no differently named implementation exists. Complete mounted global route/page reads and contract inspection strengthen the conclusion for this assigned seam. Unrelated A/B metrics and dashboard fixture names were not treated as monitoring settings.

## Spec and approval boundaries

Existing owner files were read completely:

- `openspec/changes/mos-1025-skill-monitoring/proposal.md`: explicitly excludes threshold editing.
- `design.md:7–16`: read-only goals, editing excluded, API agreement gate retained.
- `specs/skill-monitoring/spec.md:7–19`: per-skill measurements and agreed threshold comparisons; global dashboard aggregates must not substitute.
- `tasks.md:1–17`: all seven tasks remain open; unavailable presentation does not close MOS-1025.

Preserve D-014 qualifications without re-deriving them:

- Equality does not violate thresholds; maintenance interval is `[start,end)`.
- Evaluation suppression is not proof of aggregate exclusion.
- Observation time is not external-data freshness or last invocation.
- Requested conditional-write errors already exist in Jira; absent exact schemas is not absence of error requirements.
- Backend mock provenance is not frontend demo mode or real telemetry.
- Existing historical auth approval remains closed in its original scope. This report introduces no grants, credentials, auth interpretation or write approval.

## Bounded candidate dispositions

These are **recommendations for parent consideration**, not accepted or queued entries.

| ID | Disposition | Recommendation |
|---|---|---|
| IMPL1397-01 | **Keep** | Retain MOS1397-C10/C11 and D-014 conditional-write gates. No editor activation or task completion follows. |
| IMPL1397-02 | **Update evidence only** | Attach current global-route, contract, generated-type and mock-registration findings to MOS-1397 traceability. Preserve historical source identities rather than overwriting the earlier API snapshot findings. |
| IMPL1397-03 | **New bounded evidence note** | Explicitly distinguish Analytics board PUT/dashboard refresh and their tests from monitoring settings PUT/dependency refresh. This is not a new product backlog item. |
| IMPL1397-04 | **Question, nonblocking for this audit** | If “global settings” is intended as a future product surface, obtain explicit ownership/scope and write approval: the selected source specifies skill-scoped settings, not a global threshold policy. Do not infer that policy from the wave label. |
| IMPL1397-05 | **Justified plan no-op** | Existing MOS-1025 read-only scope and open API gate remain accurate. No implementation-driven owner-plan replacement or duplicate monitoring plan is justified. |

## Input hashes

SHA-256 of current full-file bytes. Paths below are repository-relative; `A` is defined above and `M = openspec/changes/mos-1025-skill-monitoring/`.

| Input | SHA-256 |
|---|---|
| `A/work-items/WAVE-D094-LOCAL-EIGHT.md` | `da5e3681c7b882ef8fc6a44a50e7dd8562068f43ac4a74c71a8f5b82e61fd0e0` |
| `A/sources/jira-monitoring-details/r1/content.json` | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` |
| `A/reports/SCENARIO-MOS-1397.md` | `ac69f23cba0bd2a2bf906a529342d2b756ae7fa5e4d80aaf7a7896b1c914a2c1` |
| `A/reviews/R-SCENARIO-MOS-1397.md` | `54831f61478ee162f591a2e5977ff5f04cf92f11297312b9a0459cd1d00f346c` |
| `A/reports/IMPL-SKILL-MONITORING.md` | `d2ff692b363d56cc015efb0bd5e8e7b3e5f530f6cbcc9437d9ac2d7cfff3ea92` |
| `A/reviews/R-SKILL-OBSERVABILITY-BATCH.md` | `d20ba6ed0e64cc53b3bfbf1d8f5a1b8c124031089864ca66411b7b49c6a1ce4b` |
| `A/decisions.md` | `dbf814a620a9ee1ff1435e912db50efb4672c3e40712f684855a14cc91df796e` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `docs/api/contracts/analytics-dashboard.md` | `c49786db40cb2c9fe841c47924ef93a0d0b65a8adb0f24141f5a4b1276e01fc2` |
| `app/shared/api/schema.d.ts` | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |
| `app/shared/config/constants/application-routes.constants.ts` | `bf50517737722446a5999e1c09ba3b2c603cc837cee23a8ab871e6418c29a21d` |
| `app/shared/config/constants/section-tabs.constants.ts` | `7a4d0a0172e5a5d10f2d209462584399831f97ab7d2563b9bbbb37a650411b1f` |
| `app/application/constants/application-routes.constants.ts` | `53bc9d61287ea25e292f5410f1905d1718adbefe3f44d6422a6447a183b3230c` |
| `app/routes.ts` | `3b7d7a026d0f73baa121d33407f155cadf9a18ffe5f0a618ad74bc02481594c4` |
| `app/routes/operations.tsx` | `2041de44a524f1ddc86469ecddf128efc8ae8e6fecb0589c81040d04f032dffc` |
| `app/routes/dashboard.tsx` | `7877f2227b2f961f6094cb3314d9092a578779f6c03f96b85dd60d3c16533570` |
| `app/pages/operations/ui/operations-page.tsx` | `6100902a8833602c9d6fcc461429b9185079b7cdb6893829f30d588ee74753e9` |
| `app/pages/placeholder/ui/placeholder-page.tsx` | `e39b58ae268a8ef3eb906326cba5cb4e7fc21dba97589fec52090b6b745c5e69` |
| `app/routes.test.ts` | `7426b300a490367adc6c1f541126ea4d5ac77ddb39b77b5bf50b58d2bd690e8e` |
| `app/shared/config/application-routes.test.ts` | `6201e05d2d1c5fc9606896bcf8dd2782389796dc5a129bb62bbb24cb4fd29213` |
| `mocks/app.mjs` | `b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0` |
| `mocks/contract.mjs` | `ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371` |
| `mocks/analytics.mjs` | `af2a3e2b4b3932bb5f4874024f3443cf812ae8fc7a9f0c24c52b1a03195efe7c` |
| `mocks/skills-status-analytics.test.mjs` | `d66a0b5f507db5670dfb7f7dd3166be6b907fdc4b2d0799736e32aba26b3f1ec` |
| `mocks/contract.test.mjs` | `a7096b8cf8ff74a162245ae96260cb282b09cdb21e278ccafaca298406c441d0` |
| `M/proposal.md` | `1056c3c2d4d63e86828856b43113d8d121e42275c77ee2c6fbb10daf8de5ef37` |
| `M/design.md` | `705131c4ba33d553c2dbae6edb90afea8da28208bb50398a09e602175ce24c81` |
| `M/tasks.md` | `069e9a4f274aa0355b063502338bdf90a04e6d10639d012feaa97f2b4745c9c1` |
| `M/specs/skill-monitoring/spec.md` | `07d874d8fe439797c8a0b7d0efe6db455f970a73f4fd574929ba0426b631cdee` |

These hashes establish inspected local bytes only. The selected source hash matches the previously recorded scenario/review hash.

## Validation and limits

- Performed local reads, directory enumeration, identifier searches, JSON pointer extraction and SHA-256 computation.
- No mandatory input was missing; no infrastructure failure occurred.
- No writes, publication, queue changes, Git commands/mutations, network, browser, business API, tests, builds, lint, typecheck, generators or nested agents.
- No test files were executed; test outcomes are unknown.
- HEAD and index were not inspected. The assignment’s baseline is contextual, not independently attested here.
- Backend implementation, migrations, SQL constraints, runtime access checks, deployed endpoints and durable persistence remain unverified.
- Current bytes do not establish historical implementation equivalence or external freshness.
- Returned for runtime persistence at the authoritative assigned output; no output file was written directly.