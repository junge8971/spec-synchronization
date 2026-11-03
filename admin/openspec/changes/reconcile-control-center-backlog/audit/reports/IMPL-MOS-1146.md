# IMPL-MOS-1146 — bounded incident read implementation evidence

## Result

**Existing owner retained: `mos-1026-skill-operations-info`. No new plan, publication, task closure or U→P transition.**

The current frontend does not mount an incident reader. Generated API declarations and local Express incident handlers exist, but do not establish frontend integration or backend delivery.

New evidence is limited to two mock/test discrepancies: incident reads preserve insertion order rather than the requested ordering; fixtures use non-seed dictionary codes without demonstrating dictionary validation. Previously accepted UI absence and partial-contract findings remain unchanged.

## Authority and prior evidence

Repository-relative aliases:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit/`
- `O` = `openspec/changes/mos-1026-skill-operations-info/`

Controlling inputs:

- `A/work-items/WAVE-D094-LOCAL-EIGHT.md`, **IMPL-MOS-1146 only**.
- `A/reports/SCENARIO-MOS-1146.md` and `A/reviews/R-SCENARIO-MOS-1146.md`.
- `A/decisions.md`, D-014: retain the percent-union correction and documentary-only acceptance.
- `A/reports/IMPL-SKILL-OPERATIONS-INFO.md`, `A/reviews/R-SKILL-OBSERVABILITY-BATCH.md`, D-082: incident GET/mock already established; owner wording already corrected.

**Read-order qualification:** the named scenario report, review and D-014 were read before current implementation inspection. The additional D-082 implementation packet was discovered and read afterward. Consequently, this run did not fully satisfy the instruction to discover/read *all* prior implementation evidence before inspecting current evidence. No repeated finding is presented as new evidence.

Current proposal/design/tasks hashes match the D-082 reviewer’s installed-after values. The old MON1146-002 blanket-contract-absence correction is therefore already addressed; do not queue it again.

## Exact source and contract pointers

Primary source:

`A/sources/jira-monitoring-details/r1/content.json#/items/1`

- `/key`: MOS-1146.
- `/description`, headings «Цель», «API», «Справочники», «Синхронизация»: view-only incidents, empty-list success, status-group/time ordering, dictionary-backed codes and internal upsert.
- `/status/name`: `Ready for test`.
- `/comment/comments/0`: MR mention, not inspected delivery evidence.
- `/updated`: `2026-10-16T19:22:41.378+0800`.

Metadata records capture `2026-10-16T13:48:06.559Z`, one captured comment of one, no attachments returned, and uncollected custom fields. Local source digest matches metadata. These are historical saved bytes, not external freshness.

Both saved `A/sources/api-live/r1/content.json` and `docs/api/contracts/openapi.json` contain:

- `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1incidents/get`
- `/components/schemas/SkillIncidentResponse`
- `/components/schemas/TsamResponseSchema_list_SkillIncidentResponse__`
- `/components/schemas/UpsertSkillIncidentRequest`

The inspected GET has only the required skill-ID parameter and an array-valued success envelope; no pagination query. Incident response/request schemas compare equal between saved publication and local aggregate. This does not establish equality of operation security or deployment.

**D-014 correction preserved:** at `/components/schemas/{SkillIncidentResponse,UpsertSkillIncidentRequest}/properties/affected_percent/anyOf/0`, nonstandard `ge:0`/`le:100` annotate the **non-null number-or-patterned-string union**, not its number branch. They do not establish generic JSON Schema range enforcement.

## Expected / observed / unknown

| Boundary | Expected | Observed local evidence | Unknown / limit |
|---|---|---|---|
| Frontend incident read | Read-only incidents, truthful source states and independent retry, per `O/specs/skill-operations-info/spec.md:21–47` | `app/widgets/skill-details/ui/skill-details-tabs.tsx:11–45` mounts overview/intents/checks/connection/history, not incidents. `ui/tabs/overview-tab.tsx:19–27` shows unavailable monitoring text. | No incident rendering, source-state distinction or independent incident retry demonstrated. This confirms prior evidence, not a new gap. |
| Client boundary | Validated incident request/read model after gate 1.1 | `app/entities/skill/api/skill-details-client.ts:15–50,88–93` validates questionnaire/detail GET, not incident GET. Search for `incident|Incident` across `app` returned generated declarations only. | Generated declarations are not a consumer, validation schema or UI integration. Search absence is bounded to inspected local files. |
| Generated contract | Incident DTO and GET available for future integration | `app/shared/api/schema.d.ts:1416–1442,4692–4693,4926–4930,9576–9618` declares read/internal-upsert operations and DTOs. | No inferred authorization to expose internal upsert. |
| Mock read | Skill-specific list; empty when none; requested open → acknowledged → resolved and descending detection time | `mocks/skill-operations.mjs:100–108` rejects missing skill, then returns `state.skillIncidents.filter(...)`. There is **no sorting**. | Actual returned order depends on stored insertion order. Production ordering not inspected. |
| Mock identity/null handling | Preserve identities and truthful nullable values | `mocks/skill-operations.mjs:63–84` preserves existing record ID, takes external ID from path and supplies nullable defaults. | Omitted optional fields are reset to null by this implementation; that is mock behavior, not an agreed backend update contract. |
| Mock dictionaries | Source requests active dictionary-backed level/side/status validation during internal synchronization | `upsertIncident` checks skill existence and percent range but contains no dictionary membership/activity lookup. Tests use `level:'critical'`, `side:'backend'`, unlike requested initial seeds. | Extra codes could be valid in a populated extensible dictionary; their mere difference from seeds is not proof of invalidity. These fixtures do not establish such dictionary provenance or enforcement. |
| Written tests | Identity, empty result, boundaries and ordering evidence | `mocks/api-update.test.mjs:163–201` asserts identity preservation, resolved status, path external ID, null cause, invalid percentages, missing skill rejection, unchanged state, and empty other-skill result. `mocks/contract.test.mjs:378–389` asserts returned record ID matches created ID. | Single incident does not exercise sorting. No dictionary-activity assertion appears in these incident cases. Tests were read, never run. |
| UI tests | Incident-specific behavior once implemented | `app/widgets/skill-details/ui/skill-details.test.tsx:148–166` asserts detail content and unavailable monitoring copy. | This is not incident table/empty/error/link coverage. |

### Per-skill observability separation

`openspec/changes/mos-1025-skill-monitoring/proposal.md`, “What Changes”, explicitly excludes incidents and responsible parties. MOS-1146 remains incident read evidence under MOS-1026, not per-skill metric delivery, global settings, refresh, assignment editing or dashboard observability.

`O/tasks.md:5–18` keeps all eight feature tasks open. Separate loading, safe source links, full contract reconciliation and independent acceptance remain pending.

## New evidence delta and bounded dispositions

These are recommendations for parent disposition only.

| Candidate | Disposition | Evidence delta / boundary |
|---|---|---|
| MON1146-001/009, existing owner and read-only scope | **Keep** | Existing spec/gate already captures read-only and truthful source states. No new frontend editor or duplicate owner. |
| MON1146-002, stale blanket contract absence | **No-op / already addressed** | D-082 and current proposal/design/tasks now distinguish GET/DTO/mock from missing full UI contract. Do not repeat publication. |
| MON1146-008, ordering | **Update existing candidate** | New code-level evidence: mock GET filters without sorting; current incident tests contain only one incident. Queue a bounded mock-ordering/assertion reconciliation, not a backend-delivery allegation. |
| MON1146-003/004/010, dictionaries | **Update existing candidate** | New fixture detail: `critical`/`backend` are used without demonstrated dictionary provenance; handler contains no active-code lookup. Preserve extensible strings and historical reads; do not replace them with exhaustive transport enums. |
| MON1146-006, percent/null semantics | **Keep with implementation annotation** | Explicit mock `Number(percent)` range check supplements nonstandard schema annotations; written invalid-input/state-preservation assertions exist. This does not prove all null/zero/false cases or executed coverage. |
| MON1146-005/011/012 | **Keep questions** | Lookup names/historical labels, `team` versus `owner`, resolution deadline/person/external URL remain unresolved accepted questions. No new source precedence or field substitution. |
| New backlog item | **None** | Existing candidate IDs and MOS-1026 owner suffice. All selected members already P; zero U→P. |

## Input hashes

SHA-256 recomputed from full local files; hashes do not imply complete semantic review of every line.

| Input | SHA-256 |
|---|---|
| `A/work-items/WAVE-D094-LOCAL-EIGHT.md` | `da5e3681c7b882ef8fc6a44a50e7dd8562068f43ac4a74c71a8f5b82e61fd0e0` |
| `A/reports/SCENARIO-MOS-1146.md` | `f963a783787bd3394da10ba6ee96a7e07f024279873fb150140264fd5743c3f4` |
| `A/reviews/R-SCENARIO-MOS-1146.md` | `551b481b45c3986388c5f8bcbbc9fcca0932326a2d9083b9ab348c932ee776d5` |
| `A/reports/IMPL-SKILL-OPERATIONS-INFO.md` | `75ee46aae14a4bf5068b623eef1de127b6b9f054cdb67933b6cbb60f8c970f0c` |
| `A/reviews/R-SKILL-OBSERVABILITY-BATCH.md` | `d20ba6ed0e64cc53b3bfbf1d8f5a1b8c124031089864ca66411b7b49c6a1ce4b` |
| `A/decisions.md` | `dbf814a620a9ee1ff1435e912db50efb4672c3e40712f684855a14cc91df796e` |
| `A/sources/jira-monitoring-details/r1/content.json` | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` |
| `A/sources/jira-monitoring-details/r1/metadata.json` | `a9703f2bda211111fec222610850560f2c4c1160aa198938e0fcb80e3d5746d5` |
| `A/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `O/proposal.md` | `424da30a249ec345f8f088e817c0afc277ca5913287fa35de64d35fd1eec0fab` |
| `O/design.md` | `ba53d8986784adeb4a7822d552df1c931da6aab4d409599a009036d0fce6ecd0` |
| `O/tasks.md` | `da0ad607376b7e3d7c7f508012f726eecf131f9570cee84c73caa8587e50bf2e` |
| `O/specs/skill-operations-info/spec.md` | `352c91a51f2b01e43ec712c33b0310bd04774011fe156c45621e07a950201488` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `app/shared/api/schema.d.ts` | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |
| `app/widgets/skill-details/ui/skill-details-tabs.tsx` | `808cd91920c1d73e4dc002b552cdc35035408220f788d04c13be8e50a9ae8237` |
| `app/widgets/skill-details/ui/tabs/overview-tab.tsx` | `db7b60125f91b671f558321680c2727cccb98227e4f3c84b59ca3d8689e5f292` |
| `app/widgets/skill-details/ui/skill-details.test.tsx` | `a69b0948e9aecf25618b1db83c27d06a804885b61ab8848e55f84d260f1558a5` |
| `app/entities/skill/api/skill-details-client.ts` | `de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6` |
| `mocks/skill-operations.mjs` | `da6e06c335b4949672f2e0176135a4030493e5e00d8195a30ebae02c5f911eda` |
| `mocks/api-update.test.mjs` | `793fb807cae6203c3d1336c15be1fd0b09d785b949e601a7dca75ee9c1e74ddb` |
| `mocks/contract.test.mjs` | `a7096b8cf8ff74a162245ae96260cb282b09cdb21e278ccafaca298406c441d0` |

## Validation and limits

- Performed local file reads, bounded searches, JSON extraction/comparison and SHA-256 computation only.
- No writes, network, browser, endpoint calls, tests, builds, lint, typecheck, Git commands/mutations or nested agents.
- No mandatory source was missing; no infrastructure failure occurred.
- HEAD, working tree and index were not inspected. Historical clean-index attestations are not adopted.
- No database migrations, deployed dictionaries, backend synchronization, real telemetry or provider integration verified.
- General historical auth approval and credential-free business-mock conventions remain unchanged; no auth implementation or policy decision made.
- Internal fake-incident upsert is not frontend editing or proof of external ingestion.
- Parent alone accepts and queues candidates. This report does not publish anything.