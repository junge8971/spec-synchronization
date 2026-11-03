# API-MOS-717-r2 — backend contract versus local module wiring

## Result and scope

**MOS-717 has concrete local contract artifacts and registered mock operations; backend delivery and integration acceptance remain unverified.** This report deepens an already-P member: **zero new U→P**.

Only the assigned backend-contract seam was inspected. No frontend audit was repeated. No files were written, candidates published, tests executed, servers started, network accessed or git operations performed. This report is returned for runtime persistence at the assigned authoritative output path.

`A` = `openspec/changes/reconcile-control-center-backlog/audit`.

## Prior evidence and controlling decisions

Read before current evidence:

- `A/reports/SCENARIO-MOS-920.md`;
- `A/reviews/R-SCENARIO-MOS-920.md`;
- `A/reports/IMPL-MOS-920.md`;
- `A/reviews/R-D093-EIGHT.md`;
- `A/decisions.md`, D-011 and D-093.

Their corrections remain controlling:

1. Schema defaults and missing constraints do not prove backend acceptance of empty messages or false confirmation.
2. Accepted local mock conventions are not production semantics.
3. MOS-717’s «Неактуально» comment has unresolved scope; neither closure nor publication resolves module-specific approval.
4. Historical general auth approval is neither reopened nor extended into module delivery.
5. Index state is uninspected and is not attested.

The prior requirement extraction and frontend findings were used as discovery maps, not rerun.

## Exact source and historical limits

Primary source: `A/sources/jira-operations-details/r1/content.json#/items/0`, lines 12–40:

- Key: **MOS-717**.
- Summary: **[B] Подготовить контракты управления глобальными модулями ассистента**.
- Item retrieval: `2026-10-16T13:02:57.486Z`.
- Collection cutoff: `2026-10-16T13:02:57.872Z`.
- Recorded status: **CLOSED**.
- Recorded update: `2026-10-15T15:13:58.701+0800`.
- `/description`: list state, disable eligibility, user text and last-change information; global disable, consequence confirmation and nonempty user message; contracts with request/response/error examples.
- `/comments/items/0`: comment `1131251` links wiki page **241088180**.
- `/comments/items/1`: comment `1131293` says **«Неактуально»**, without identifying what is retired.

Adjacent `metadata.json` records uncollected custom fields/attachment bodies and explicitly distinguishes publication from runtime or approval. These are saved historical records, not freshly verified Jira status.

Supplemental historical source pointer: `A/sources/wiki-241088180/r1/content.json#/bodyView`, business rules and §§2.1–2.6. Its requirement/example analysis remains the accepted prior report/review evidence; this lane did not repeat that analysis.

## New evidence delta

### 1. Current standalone and merged contracts are structurally aligned

Read-only JSON comparison inspected the module section of:

- `docs/api/contracts/assistant-modules.openapi.json`;
- `docs/api/contracts/openapi.json`;
- `A/sources/api-live/r1/content.json`.

Let `B=/api/control/api/assistant-modules/v1/modules`.

| Operation | Current standalone versus merged | Current versus saved r1 operation |
|---|---|---|
| GET B | Equal | Only `security` differs |
| GET B/summary | Equal | Only `security` differs |
| GET B/preview | Equal | Only `security` differs |
| POST B/{module_id}/disable | Equal | Only `security` differs |
| POST B/{module_id}/enable | Equal | Only `security` differs |

All **26 schemas present in the standalone module document** equal their corresponding schemas in both the current merged contract and saved r1 document.

Exact locators: each document’s `#/paths` entries above and `#/components/schemas/{schemaName}`. Literal JSON pointers escape path slashes as `~1`.

The current operation security is one object containing both `AdminToken` and `AccessToken`. This is the already-agreed AND normalization, not a new auth discrepancy or evidence of runtime enforcement.

**Delta:** the current module contract has not silently repaired the previously identified request-schema limitations. Its module operations and schema definitions remain structurally consistent with the saved source, apart from the accepted security correction.

### 2. Supplemental documentation already states the contract boundary

`docs/api/contracts/assistant-modules.md`:

- **Методы** lists all five operations and their response data schemas.
- **Список** documents repeated `sort` parameters, nullable string query/status and pagination bounds.
- **Модуль и мутации** documents required bodies and `expected_version >= 1`; optional confirmation/message defaults; optional nullable actor; no required Idempotency-Key.
- **Ограничения источника** explicitly states that OpenAPI does not define complete search, sorting-priority, transition, confirmation, version-conflict or preview-calculation semantics; 404/409 are not described.
- The same section separates mock conventions from backend contract and distinguishes the module-state summary banner from banner/maintenance management.

**Delta:** these are not wholly undocumented semantics awaiting a new documentation owner. Current supplemental documentation already records the limitations. It does not settle the stronger historical business requirement or constitute backend approval.

### 3. Local implementation provides a contract-validation chain, not backend proof

Positive registration chain:

1. `mocks/contract.mjs:6–8` loads the current merged contract.
2. `mocks/app.mjs:35–77` includes `assistantModulesHandlers(state)`, resolves operations by `operationId`, and runs request validation before handlers.
3. `mocks/contract.mjs:71–73` translates contract paths.
4. `mocks/assistant-modules.mjs:77–94` supplies all five named handlers.
5. `mocks/contract.mjs:139–178` checks required bodies and request schemas.
6. `mocks/contract.mjs:180–197` validates declared successful response envelopes before sending them.

The handler implementation is local state manipulation:

- `assistant-modules.mjs:4–14`: list search/filter/order/pagination.
- `:16–51`: summary and fallback preview derived from the module collection.
- `:53–75`: eligibility, conditional impact confirmation, version conflict, mutation metadata and user-message handling.

This corroborates existing local wiring evidence. It does **not** establish deployed backend code, persistence, global surface propagation or actual assistant behavior.

## Expected / observed / unknown

| Expected from MOS-717 | Observed current evidence | Unknown / boundary |
|---|---|---|
| Contract for module list with state, eligibility, message and last change | `ModuleResponse` and GET B; supplemental document **Модуль и мутации**; list handler `:4–14` | Backend data completeness and accessible-object filtering |
| Enable/disable contracts | Required request bodies reference `EnableModuleRequest` / `DisableModuleRequest`; both require expected_version | Business interpretation of “no additional input” does not remove concurrency input |
| Nonempty disable user text and confirmation of consequences | Schema requires only expected_version; message defaults empty and confirmation false. Local handler stores empty text and requires confirmation only with nonempty impact text | Backend business validation; no inference that production permits weaker inputs |
| Disable eligibility enforced | Handler `:53–57` rejects `disable_allowed=false`; tests `:225–235` assert protected-module conflict | Production enforcement; no name-based core/classifier policy inferred |
| Changes reflected globally | One local collection drives list/summary/preview | Real propagation across surfaces, assistant responses and durable backend persistence |
| Last-change information | Handler `:65–73` sets timestamp and fixed fixture actor; tests `:145–150` assert metadata | Actual authenticated actor provenance; fixture actor is not visitor identity |
| Request/response/error documentation | Current docs and schema provide wire shapes; historical wiki examples remain prior accepted evidence | Approval/completeness of examples and business-error semantics are not established by local shape parity |
| Rejected writes preserve state | Handler rejects before mutation; tests `:182–246` assert errors and unchanged collection/views | Concurrent backend transactions and deployed error envelopes |

Normative local owner: `openspec/specs/control-center-mock-server/spec.md:138–191`. Its `:161` expressly owns the weaker local message/confirmation and repeated-transition conventions. Its `:193–219` owns merged/standalone consistency and security normalization.

Read the archived local-session-demo proposal, design and mock-server delta before interpreting local mock semantics. Credential-free business mocks and absence of role enforcement remain approved boundaries, not missing production authorization.

## Test evidence — read, not executed

`mocks/assistant-modules.test.mjs` contains these concrete assertions:

- `:35–92`: search, single/repeated sort, pagination and empty-result boundaries.
- `:102–131`: coherent totals, disabled IDs and fallback-card content.
- `:133–180`: version/time/actor changes, repeated target transitions, omitted user message, no-impact disable without confirmation, and fresh-server seed reset.
- `:182–246`: malformed inputs, missing IDs, stale versions, protected modules, confirmation failures and unchanged state/views.

These assertions validate the intended **local** model if executed successfully; this run did not establish that execution result. Their no-impact/empty-message cases are already accepted evidence, not a newly discovered product defect.

## Bounded candidate dispositions

| Disposition | Candidate |
|---|---|
| **Keep** | MOS-717 remains analytically P. Preserve historical CLOSED/«Неактуально» attribution without treating it as backend delivery or current status. |
| **Update** | Add exact current-contract evidence: all five standalone path objects equal merged equivalents; all 26 standalone schemas equal merged and saved r1 equivalents; operation differences from r1 are limited to the accepted security normalization. |
| **Update** | Attach `docs/api/contracts/assistant-modules.md` as existing supplemental ownership explicitly documenting undeclared business semantics and mock/backend separation. Avoid a duplicate “missing documentation” task. |
| **Question — existing** | What does «Неактуально» retire, and which approved module contract governs nonempty message, confirmation, transition/error and global-effect semantics? No policy selected here. |
| **New task — none** | No new implementation plan, frontend audit, scheduler, auth model or backend-delivery claim is justified by this bounded evidence. |
| **Publication — none** | Parent alone accepts and queues candidates. No register or publication artifact was modified. |

## Input fingerprints

SHA-256 recomputed from local bytes:

| Input | SHA-256 |
|---|---|
| `A/work-items/WAVE-D094-LOCAL-EIGHT.md` | `da5e3681c7b882ef8fc6a44a50e7dd8562068f43ac4a74c71a8f5b82e61fd0e0` |
| `A/reports/SCENARIO-MOS-920.md` | `d1587adf7b366f8c03ac97197f978ca7fab114515d47fb9c80d32571ecfe9883` |
| `A/reviews/R-SCENARIO-MOS-920.md` | `d1efb5f0b29510b6961d04185899c5b92532ff636ee24db3edf18824d8de11a9` |
| `A/reports/IMPL-MOS-920.md` | `c998eae5e2c76d79393acf6b0668f2afcaaffdb1750ef82db361bf6ea2c9ce57` |
| `A/reviews/R-D093-EIGHT.md` | `aee6c464b24662ed9e5396e382ca2e35a3add12ffe47a6c452178f847084e2bc` |
| `A/decisions.md` | `dbf814a620a9ee1ff1435e912db50efb4672c3e40712f684855a14cc91df796e` |
| Jira operations r1 `content.json` | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| Jira operations r1 `metadata.json` | `73e55adae262fba4222f1a701fe3152b001503ff5c0b3c10988a65bc575bbf8e` |
| Wiki 241088180 r1 `content.json` | `e1d5f5320e05d1e65354f2523341cab788adfacac8ac5acf6aaabf31003c18fc` |
| API-live r1 `content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `docs/api/contracts/assistant-modules.md` | `07390fd25dcba4be87387af11a60116a6709afcd559d9214908c2e1945fe4933` |
| `docs/api/contracts/assistant-modules.openapi.json` | `79b96aff9cd84c88c2aee843a5d3f87f83ee999c25ee6e3e361f4bcb7a708052` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `mocks/assistant-modules.mjs` | `0694eaff9bc872fc1fcd252d4fe76bbf7edd158c4495f78d402b311201f9ef23` |
| `mocks/assistant-modules.test.mjs` | `10f817be8e813fa4a03b50fdbbe6e471d0c4cabd729c932e612c816f8cbf5242` |
| `mocks/contract.mjs` | `ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371` |
| `mocks/app.mjs` | `b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0` |

Hashes identify bytes, not external freshness or deployment. Whole-file hashing does not claim whole-file semantic review beyond the stated seam.

## Validation and residual limits

All mandatory inputs were available; no infrastructure failure occurred. Validation consisted only of local reads, scoped discovery, hashing and structural JSON inspection. No test/build/typecheck/lint/format command was run.

Baseline HEAD and index were not independently inspected. Backend implementation, historical delivery, live contract status, durable persistence, authorization, global propagation and actual test success remain unverified. No fallback mode, external collection or publication was attempted.