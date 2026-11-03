# JOIN-MOS-901 — backend DoD versus inspectable frontend boundaries

## Result

**Partial analytical join only. MOS-901 backend delivery cannot be established from this frontend repository.** Current clients, local handlers and test assertions provide inspectable integration boundaries, not proof of durable storage, team ACL enforcement, production transitions or deployed test coverage.

No mandatory input failure occurred. Attachment **824049 / TEST_PLAN.md** is explicitly uncollected in the assignment; its absence limits test-plan reconciliation rather than authorizing reconstruction or external retrieval.

Parent retains acceptance, coverage and publication decisions. No issue closure, product-policy selection, implementation authorization or publication is proposed automatically.

`A` below means `openspec/changes/reconcile-control-center-backlog/audit`.

## 1. Exact source and historical assertions

Primary source: `A/sources/jira-surface-details-d095/r1/content.json#/items/4`.

- `/key`: **MOS-901**.
- `/summary`: `[B] Реализовать модуль "Поверхности"`.
- `/status`: **Require improvement**.
- `/updated`: `2026-10-16T19:22:20.757+0800`.
- `/retrievedAt`: `2026-10-20T16:56:26.378Z`.
- Packet collection cutoff: `2026-10-20T16:56:26.589Z`.
- `/description`: backend creation/list/detail, appearance and enabled skills, search/filter/sort/pagination, sandbox/publication/disable/archive, surface and status-history storage, data validation and team access checks.
- `/description`, **DoD**: contract-conforming API; storage and principal business scenarios; access/input/status-transition validation; principal scenarios covered by tests.
- Direct dependency: `https://wiki.mos-team.ru/spaces/KR/pages/241082009/…`, available locally as `A/sources/wiki-241082009/r2/content.json`.

Historical comment inventory is complete for the selected packet: `/comments/total = 4`, four returned entries.

| Exact pointer | Source assertion | Evidentiary boundary |
|---|---|---|
| `/items/4/comments/items/0`, id `1112439` | Testing instructions reference `TEST_PLAN.md`, 18 September | Reference, not recovered plan or test execution |
| `/items/4/comments/items/1`, id `1112461` | Testing blocked until database creation, 18 September | Historical blocker; neither current database absence nor later migration success follows |
| `/items/4/comments/items/2`, id `1126093` | Successful testing claimed on `https://mobile-a-tech.mos.ru/tsam-panel/`; follow-up MOS-1237 created, 7 October | Attributed historical report, not independently executed or deployment-bound acceptance |
| `/items/4/comments/items/3`, id `1126377` | Task moved because of follow-up work, 7 October | Workflow history, not evidence that remaining defects were resolved |
| `/items/4/attachments/0` | id `824049`, `TEST_PLAN.md`, Markdown, **13,709 bytes** | Metadata only; no cases, results, fixtures or coverage inferred |

The later improvement status and earlier success comment are retained together, without resolving them into delivery acceptance.

## 2. Prior dispositions and ownership preserved

Read before implementation inspection:

- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md`.
- `A/reports/JOURNAL-SURFACE-MVP.md`.
- `A/reviews/RECON-MOS-959-CONTRACT.md`.
- `A/reviews/R-D093-EIGHT.md`.
- Relevant D-004/005/090/091/093 entries in `A/decisions.md`.
- Scope and evidence sections of `A/publication/DRAFT-SURFACE-D091.md`.

Consequences retained:

1. **D-004/005:** published configuration constraints do not activate the configurator. Wiki/OpenAPI differences in enums, fallback nullability, defaults and combined versus separate persistence remain versioned disagreements; this report selects no precedence.
2. **D-090/091:** registration text presentation/domain-input reflection candidates remain separately owned and unpublished. They do not establish MOS-901 backend completion.
3. **D-093:** sandbox/session/conversation/token analyses remain distinct MOS-960/961/962 evidence. Ordinary lifecycle endpoints are not sandbox-session or synchronization proof.
4. Frontend registry, selection, connection, lifecycle and registration detail remain respectively with **MOS-910/911/913/914/958**. Contract-preparation completeness remains **MOS-712**. This report uses those boundaries only to assess the four MOS-901 DoD claims; it does not count or reassign their member coverage.

## 3. Expected / observed / unknown matrix

API pointer notation:

- **S** = `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces`
- In `A/sources/api-live/r2/content.json`, append `/post`, `/get`, or `~1{surface_id}~1configuration/put`, etc.
- Each description claim below refers to the operation’s `/description`, not an executed response.

| MOS-901 obligation | Expected | Observed locally | Unknown / limitation |
|---|---|---|---|
| **API conforms to contract** | Backend implements the agreed surface contract | `app/entities/surface/api/surface-registry-client.ts:128–214` supplies list/detail/create, separate configuration/enabled-skills PUTs and six bodyless lifecycle POSTs. Saved r2 OpenAPI contains all eleven corresponding operations. | Client availability and response parsing do not prove backend conformance. Wiki/OpenAPI disagreements remain; successful-response schemas alone do not describe all prose-listed errors. |
| Create/list/detail and query scenarios | Persistent records and usable registry/detail operations | Client maps list request to query/status/type/sort/limit/offset; parses `items` and pagination. `mocks/surfaces.mjs`, `surfacesHandlers`, implements creation, list filtering/sorting/paging and detail lookup. | Mock implementation is not the deployed service. Query parity, tenant visibility, real channel generation and real connection provisioning are not established. Detailed registry discrepancies belong to MOS-910. |
| Appearance and connected skills | Save complete configuration and per-skill parameters | Client has separate PUT functions. Mock assigns configuration or enabled-skills arrays. r2 `S~1{surface_id}~1configuration/put/description` documents full replacement, trimming, conditional fallback, card validation and unchanged embed token/code. Enabled-skills description documents full replacement and parameter validation. | No evidence of backend execution, atomic persistence, downstream propagation or full semantic validation from this code. Configurator UI remains deferred. MOS-1237 coverage cannot be inferred from the comment or missing plan. |
| **Storage and business scenarios implemented** | Durable surface storage and status history | `mocks/state.mjs:13–33` clones seed into process state and creates `surfacePreviousStatuses` and `surfaceActionFailures` maps. `mocks/surfaces.mjs`, `surfaceAction`, remembers a previous status for disable/archive and consumes it on enable/restore. | A previous-status map is **not an append-only status history**. No inspected surface client/handler provides history retrieval. Database schema, migrations, transactions, restart persistence, history attribution and retention remain unverified. This is not a claim that the backend lacks them. |
| **Access rights checked** | Backend enforces operation permissions and team scope | Saved r2 descriptions expressly require `TSAM.Surface:*` operation permissions; list is team-scoped; inaccessible detail/update targets appear absent. Linked wiki `/bodyView`, heading `APIконтрактуправленияповерхностями-2.12Доступ`, describes role access and inaccessible-target 404. | These are published claims, not enforcement evidence. Business mocks intentionally do not authorize from role/permissions. No role mapping, grant or ACL policy is selected here. |
| **Input validated** | Backend enforces request structure and business rules | `mocks/app.mjs:62–78` applies `createRequestValidator` before handler execution. Surface creation additionally checks team, skills, responsible users and case-insensitive occupied domains before pushing state. | Structural validation plus these checks does not prove complete business validation. Inspected enabled-skills handler checks existence, not the complete published parameter semantics; configuration handler assigns the body. Backend error fidelity remains unexecuted. |
| **Status transitions checked** | Agreed transitions reject invalid operations without corrupting state | Saved r2 descriptions distinguish publish/sandbox permissiveness and constrained disable/enable/archive/restore. Local `surfaceAction` performs lookup, injected failure and target/previous-status assignment, but no source-status eligibility check. | Mock permissiveness cannot certify backend transitions. It is already accepted as a bounded MVP limitation, not a newly authorized mock defect fix. External-service failure rollback is described by API prose but not proven. |
| **Principal scenarios covered by tests** | Backend tests cover principal scenarios, including boundaries | Local mock and frontend tests contain concrete assertions listed below. | They are not backend tests or executions here. Missing TEST_PLAN824049 prevents case-by-case reconciliation. No real ACL, persistence/restart, migration or production-transition test result is available. |

### Approved scope versus broader backend task

`openspec/specs/surface-lifecycle-publication/spec.md`, **Lifecycle status and actions**, **Archived surface is read-only**, and **MVP editing and deferred functionality boundaries**, explicitly retain:

- no visible or hidden sandbox launch;
- actual server statuses rather than locally manufactured `configured`;
- no fake/default configuration PUT;
- no invented history API or history completion claim.

The owning archive was inspected at:

`openspec/changes/archive/2026-10-12-mos-914-surface-lifecycle-mvp/{proposal,design,tasks}.md`.

Its design excludes backend transactions, mock repair, sandbox and audit; tasks §4.2 explicitly say the original sandbox/history task is not closed by the MVP. Historical checked tasks are not fresh execution evidence.

`openspec/specs/surface-registration/spec.md`, **Creation supports an atomic optional configuration** and **Rejections are distinct from unknown creation outcomes**, governs safe frontend creation/readback/retry. These requirements do not prove backend atomicity.

## 4. Test evidence: assertions read, not run

| Locator | Actual assertions inspected | What they do not establish |
|---|---|---|
| `mocks/surfaces.test.mjs`, `surface creation stores IDs and optional configuration atomically; GET resolves current users` | Configuration readback; external string user ID; team relation; removed user retains ID/null details; rejected unknown user leaves surface/team state unchanged | Database transactions or production directory behavior |
| Same file, `absent and null configurations use defaults; invalid input never mutates surfaces or team relations` | Omitted/null equality; invalid configuration/user and domain conflict leave cloned state unchanged | Agreement of mock default values with live service, complete configuration validation or real error envelopes |
| Same file, `concurrent domain claims create exactly one surface and team relation` | Two local requests yield one surface/relation; explicitly synchronous handler check-and-push | Cross-process/database uniqueness, isolation or deployed concurrency safety |
| Same file, `server multiline embed and nullable connection are returned literally` | Literal fixture connection readback and null support | Issued token validity, operational widget connectivity or secret lifecycle |
| `app/entities/surface/api/surface-registry-client.test.ts:389–437` | Exact enabled-skills PUT payload; parsed response; preservation of 422 status | Server parameter validation |
| Same file `:440–520` | All six actions use bodyless POST; invalid status/time rejected; 409 preserved | Valid transition matrix: fixtures return `prod` for every action |
| Same file `:522–559` | Exact configuration PUT payload and response parsing | Backend normalization, storage, authorization or MOS-1237 resolution |

No test, server listener, business API, build or browser was executed.

## 5. Publication versus deployment qualification

The saved API r2 capture is dated **2026-10-19T08:11:44.238Z**, distinct from both the October 7 testing comment and October 20 Jira packet.

Its descriptions now explicitly document creation error fields, including `/responsible/product`, `/configuration/...`, and occupied domains under `/domains` with `details.domains`. They also document team access, unchanged timestamps on configuration/skill saves, and duplicate skill IDs resulting in 500.

By contrast:

- `docs/api/contracts/surfaces.md`, **Совместимость снимка 15.10.2026**;
- `docs/api/contracts/surface-error-provenance.md`, **Backend evidence (unresolved)**

describe the earlier October 15 evidence gap and blocked task 3.2.

**Bounded conclusion:** current saved publication contains information absent from those historical local-documentation statements. It does not supply a sanitized executed backend response, close the rollout gate or establish production behavior. Any documentation correction belongs to the existing API/error-provenance owner, coordinated with MOS-712/958—not a new MOS-901 frontend implementation task.

## 6. Queue-only candidates

| ID | Classification | Bounded candidate and ownership |
|---|---|---|
| MOS901-E01 | **KEEP** | Retain backend DoD as unverified delivery; attach the exact MOS-901 source and local client/mock/test boundary mapping. Parent alone decides analytical coverage. |
| MOS901-E02 | **UPDATE evidence** | Record that TEST_PLAN824049 body remains unavailable; preserve the database-blocked, successful-test and improvement comments as separately dated assertions. Do not infer test cases or resolution. |
| MOS901-E03 | **UPDATE existing handoff** | Point the existing API/error-provenance owner to r2 creation/validation/access descriptions when correcting older documentation-absence wording. Preserve execution/rollout gates and D-004/005 disagreements. |
| MOS901-Q01 | **QUESTION, backend evidence** | Before delivery acceptance, obtain backend-owned persistence/migration/status-history and team-scope enforcement evidence tied to a deployed revision. No schema, ACL or retention policy chosen. |
| MOS901-Q02 | **QUESTION, verification evidence** | Parent may separately collect the exact attachment and backend test/run provenance. Required evidence should distinguish contract tests, real storage/ACL scenarios and historical UI testing. No external access delegated here. |
| MOS901-N00 | **NEW product change: none** | No duplicate registry, selection, lifecycle, registration, configurator or sandbox change justified by this bounded join. |

## 7. Verified input fingerprints

SHA-256 calculated locally from the inspected bytes.

| Input | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| `A/sources/api-live/r2/content.json` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `A/sources/wiki-241082009/r2/content.json` | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` |
| `app/entities/surface/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `app/entities/surface/api/surface-registry-client.test.ts` | `4d5f93269521aedb76ce4dd722390c92dfa06e86b63af622f952146ef105c886` |
| `mocks/surfaces.mjs` | `a225bd153667722264514c9cc77e2cf0ea34e84bc26999951bfeed0b67cb7d8f` |
| `mocks/surfaces.test.mjs` | `f593d5787af815c94f2e1711506effdfb0c476503923b4379425e25cff1d114d` |
| `mocks/state.mjs` | `d80532dc6318021afe15c65bb095ebac55876d34e61195e0731604d6af59a93e` |
| `mocks/app.mjs` | `b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0` |
| `docs/api/contracts/surfaces.md` | `04b31f1bbf9a8359f2a8d455080855c006736d11b3628b4666dbb624020b9257` |
| `docs/api/contracts/surface-error-provenance.md` | `4c9dc8882222f9ec0e64a18d05090561d1053ce17498de4f38ab37fb92c90e0a` |
| `openspec/specs/surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| `openspec/specs/surface-lifecycle-publication/spec.md` | `675265a0ba98b45f1d659f6048fe97f2e590a0597d7eda304cdcfe9854ebdd91` |

Jira and API fingerprints match adjacent metadata. Hashes identify saved bytes, not remote currency or implementation correctness.

## 8. Execution limits

Only local read/search, inert JSON/HTML extraction and hashing were performed. No writes, network, browser, business requests, tests/builds, configuration changes, git mutation or nested agents.

The supplied baseline HEAD was not independently checked; index state is uninspected. No clean-tree or no-staged-files assertion is made. Backend storage, ACL, deployment, historical environment identity and missing attachment content remain unknown.

This complete report is returned for runtime persistence at the assigned output path; no tool wrote it.