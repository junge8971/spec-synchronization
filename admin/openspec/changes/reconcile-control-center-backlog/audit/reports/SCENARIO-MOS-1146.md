# Code Context

## SCENARIO-MOS-1146 — incident publication and existing frontend ownership

**Designated artifact:** `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1146.md`

Read-only analysis; returned for parent persistence. No direct writes, product changes, tests, builds, network access, endpoint execution or nested delegation. Repository index remains **uninspected/unverified**.

### Result

MOS-1146 has an existing frontend planning owner: **`mos-1026-skill-operations-info`**, not a missing-plan case. Its read-only, independent-loading and truthful-error requirements already cover important incident behavior. Its assertion that the contract lacks incidents is outdated: both saved published OpenAPI and the local aggregate contain the incident GET and DTO.

Publication does **not** complete that plan or authorize activation. Remaining reconciliation includes dictionary lookup/historical labels, `team` versus `owner`, nullable fields, ordering, and requested external links/resolution deadlines absent from the published incident DTO.

## Files Retrieved

Paths below are repository-relative. JSON evidence is cited by exact pointers rather than misleading physical line numbers.

### Plans and main specifications

Fully read:
- `openspec/changes/mos-1026-skill-operations-info/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-operations-info/spec.md` (1–47): existing incident owner and blocked continuation.
- `openspec/changes/mos-1025-skill-monitoring/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–17), `specs/skill-monitoring/spec.md` (1–47): adjacent metrics owner explicitly excludes MOS-1026 incidents.
- `openspec/specs/skill-catalog-experience/spec.md` (1–112): truthful warnings and source-failure safeguards.
- `openspec/specs/control-center-api-integration/spec.md` (1–149): session boundary, contract-backed fields and error distinctions.
- `openspec/specs/control-center-http/spec.md` (1–138): transport errors, credentials and publication-versus-activation boundary.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (1–194): discovery routing only; its index attestation is not adopted.
- `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (1–109): D-001–D-013 applied.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MONITORING-WAVE.md`: complete assignment.

### Mandatory auth/demo prerequisites

Fully read under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`:
- `proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52).
- `specs/control-center-api-integration/spec.md` (1–64).
- `specs/control-center-http/spec.md` (1–71).
- `specs/control-center-mock-server/spec.md` (1–27).
- `specs/control-center-permissions/spec.md` (1–89).
- `specs/control-center-shell/spec.md` (1–101).
- `specs/mpmm-session/spec.md` (1–138).

Fully read under `openspec/changes/archive/2026-10-09-add-local-session-demo/`:
- `proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26).
- `specs/control-center-mock-server/spec.md` (1–106).
- `specs/control-center-shell/spec.md` (1–55).
- `specs/local-session-demo/spec.md` (1–123).

Also fully read `docs/mpmm-auth-rollout.md` (1–58). Truncated tool output was recovered through subsequent reads before conclusions.

### Primary publications and contracts

- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-monitoring-details/r1/content.json`: `/items/0` and `/items/1` completely; corresponding `metadata.json` completely. Other issue descriptions were not interpreted.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`: incident operations, incident schemas/envelopes, relevant catalog operations/schemas; `metadata.json` completely.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json`: `/bodyView`, incident requirements МОН-13/14, ПРТ-МОН-6, model §4.7, dictionary rows in §7, incident references T-35/T-59; metadata/version.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r2/content.json`: `/bodyView`, general information, skill catalog reference and version history; metadata/version.
- `docs/api/contracts/skill-incidents-internal.openapi.json` (1–346): complete local internal contract.
- `docs/api/contracts/openapi.json`: incident operation presence and exact incident request/response schema comparison with saved publication.

## Integrity and version checks

SHA-256 was recomputed from local saved bytes.

| Evidence | Verified SHA-256 | Version/capture |
|---|---|---|
| Jira monitoring r1 | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` | Revision 1; 44,254 bytes; captured `2026-10-16T13:48:06.559Z` |
| API live r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | OpenAPI 3.1.0; service version 0.1.0; captured `2026-10-16T11:13:29.451Z` |
| Skills wiki r1 | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` | Page version 17; modified `2026-10-09T23:32:41.029+08:00`; captured `2026-10-16T11:48:21.710Z` |
| Catalog wiki r2 | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` | Page version 6; modified `2026-10-13T17:56:19.256+08:00`; captured `2026-10-16T12:37:03.295Z` |
| Local internal contract | `3752ad6ac5058d888f75942bccde7487dc340caac1726e4707c0e01d73aaf425` | OpenAPI 3.1.0; service version 0.1.0 |
| Local aggregate | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` | OpenAPI 3.1.0; service version 0.1.0 |

The four source-content hashes match their metadata. Local contract hashes are observations, not assertions of equality to the entire saved API.

Catalog wiki page revision **6** is distinct from its body **v1.0** label and history entry **v1.1 dated 14.09.2026**. Neither chronology nor page revision selects source precedence.

Jira `/items/1/updated` is `2026-10-16T19:22:41.378+0800`; `/items/1/status/name` is **Ready for test**. Comment capture is complete by counts: one of one, `/items/1/comment/comments/0`, comment ID `1126159`. Its MR mention was not followed and is not delivery evidence. Attachments returned are empty; custom fields were not collected.

## Key Code / Contract

Let **P** denote saved `api-live/r1/content.json`.

### Public incident read

Exact pointer:

`P#/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1incidents/get`

- Operation ID: `get_skill_incidents_api_control_api_skills_v1_skills__skill_id__incidents_get`.
- Required path `skill_id`: string, format `uuid7`.
- No published pagination/filter/sort query parameters on this operation.
- `200`: `TsamResponseSchema_list_SkillIncidentResponse__`.
- `422`: `HTTPValidationError`.
- Envelope requires `code`, `data`, `message`; `data` is an array of `SkillIncidentResponse`, not a paginated object.

`P#/components/schemas/SkillIncidentResponse`:

| Shape | Fields |
|---|---|
| Required, non-null | `id`, `skill_id`, `external_id`, `level`, `title`, `side`, `message`, `detected_at`, `postmortem_done`, `status` |
| Required but nullable | `cause`, `acknowledged_at`, `resolved_at`, `postmortem_due_at` |
| Optional and nullable | `affected_percent` |

`id` and response `skill_id` are UUID strings. `level`, `side`, `status`, and `external_id` are strings, not enums. Timestamp fields use `date-time`.

`affected_percent` accepts number or numeric-pattern string, or null. The numeric alternative carries literal `ge: 0`/`le: 100` annotations—not standard JSON Schema `minimum`/`maximum`. Do not claim generic validator enforcement of these annotations.

No declared incident URL, assigned user/contact, resolution deadline, `created_at`, `updated_at`, source-connection status or pagination metadata is present.

### Internal upsert — not frontend editing

Exact pointer:

`P#/paths/~1api~1control~1api~1internal~1incidents~1{external_id}/put`

- Operation ID: `upsert_skill_incident_api_control_api_internal_incidents__external_id__put`.
- Required external ID: string length 1–64.
- Required JSON body: `UpsertSkillIncidentRequest`.
- Required body fields: `skill_id`, `level`, `title`, `side`, `message`, `detected_at`, `postmortem_done`, `status`.
- Nullable fields are optional in this **request**, unlike most nullable fields in the response.
- Codes have length 1–32; title/message have minimum length 1.
- `200` returns entity-created envelope containing UUID `id`; `422` is `HTTPValidationError`.
- No explicit idempotency header, expected version, lowercase pattern or dictionary-membership rule is encoded in this operation/schema.

The saved publication includes this **internal** path; publication alongside public paths does not make it a public frontend command.

Local `UpsertSkillIncidentRequest` exactly matches the saved schema. Local aggregate `SkillIncidentResponse` also exactly matches. Saved operation security uses separate OR objects; the local internal contract has the approved AND pair. This is known normalization, not permission to weaken session requirements.

## Candidate mapping

These stable IDs are audit candidates, not activated requirements.

| ID | Primary locator | Coverage / discrepancy | Narrow recommendation |
|---|---|---|---|
| **MON1146-001** | Jira `/items/1/description`, headings «Цель», «API»; wiki `/bodyView`, МОН-14 | Incidents are view-only in Control Center; no public create/edit/delete required. MOS-1026 spec 35–47 and proposal 7–10 already agree. | **No-op** on read-only scope. Never expose internal upsert through a UI editor. |
| **MON1146-002** | Jira «API»; public GET pointer above | GET and DTO are published and present locally. MOS-1026 proposal:25 says incidents absent; design:13/tasks:5 retain an undifferentiated API gate. | Candidate documentation correction: distinguish **published read contract** from unresolved consumer semantics and unverified integration. Do not close task 1.1 wholesale. |
| **MON1146-003** | Jira «Справочники», «Доменная модель» | Database dictionaries, not Python enums, define codes. Seeds: levels p0–p3; sides platform/team; statuses open/acknowledged/resolved. Codes lowercase; used values retained via inactive flag. DTO strings agree with extensibility. | Record dictionary-backed string handling; do not turn seeds into an exhaustive transport enum. DB/model implementation remains backend scope. |
| **MON1146-004** | Jira «Синхронизация» and «Справочники» | Upsert must reject unknown/inactive level/side/status. Existing historical references must not be physically deleted. This is not permission to filter incident reads to active codes. | Preserve historical rows and returned codes. Clarify label resolution/inactive inclusion separately; no frontend mutation selector is needed for this seam. |
| **MON1146-005** | `P#/components/schemas/SkillCatalogsResponse`; catalog lookup paths | `/skills/v1/catalogs` declares only skill_types/training_states/autotest_states. Generic managed-resource lookup supports section `skills` and dictionary-shaped results, but inspected schemas do not name incident keys or establish inactive inclusion. | Ask API/catalog owner for exact incident lookup keys and historical-label behavior. Do not claim dictionaries universally absent or invent keys from table names. |
| **MON1146-006** | Jira «Таблица skill_incidents»; `SkillIncidentResponse` | Published field presence/nullability is precise. MOS-1026's generic incident wording does not yet capture required-nullable versus optional-nullable fields, percent string/number, or false/zero distinctions. | Candidate DTO acceptance examples: null cause/timestamps, absent/null/zero percent, false postmortem flag, malformed required fields. No defaults that fabricate measurements. |
| **MON1146-007** | Jira «Таблица skill_incidents», «Синхронизация» | Internal upsert keyed by unique immutable external_id; skill must exist. Public DTO has both UUID record ID and external ID, but no URL. MOS-1026 design:16 already calls for stable source IDs, not titles. | Preserve both identities; clarify stable row-key choice and future link source. Never construct external URLs from an unspecified external-ID format. |
| **MON1146-008** | Jira «API», ordered list | Required order is open → acknowledged → resolved; detected_at descending within each group. Schema alone does not state order. Existing MOS-1026 delta lacks this precise acceptance scenario. | Candidate ordering scenario for future approved plan update. Do not substitute level sort, resolved_at sort or client status inference. Tie-breaking and additional statuses remain unspecified. |
| **MON1146-009** | Jira «API», empty-list paragraph; public array envelope | Successful no-incidents result is an empty list. MOS-1026 spec 35–47 already distinguishes empty/error/unconnected/unavailable. GET publishes 200/422 only, not a source-status discriminator. | **No-op** on error isolation; record wire shape. Empty array must not be reinterpreted as “not connected”; missing endpoint, malformed success and request failure are not empty success. |
| **MON1146-010** | Jira «Миграция», «Критерии приёмки», «Синхронизация» | Tables, seeds, FKs/indexes, uniqueness, validation and upsert are requested backend acceptance. FK failure must not substitute for user-facing validation. No backend code inspected. | Keep separate from frontend acceptance. Do not declare migration, synchronization, validation or real external ingestion delivered. |
| **MON1146-011** | wiki skills `/bodyView`, §4.7 and §7 dictionary rows versus Jira «Справочники»/table | Wiki uses `skill_incident_*` names and side `owner` (“Владелец навыка”); Jira uses `incident_*` and `team` (“Команда навыка”). Wiki message is optional, level varchar(8), title string(500), and includes created/updated timestamps; Jira/published DTO differ. | Explicit source-reconciliation item. No silent `owner`↔`team` alias, timestamp synthesis or wiki length cap imposed on published DTO. |
| **MON1146-012** | wiki МОН-13/ПРТ-МОН-6/T-59; MOS-1026 spec:23–28/tasks:12; `SkillIncidentResponse` | UI prose requests resolution deadline, responsible party and links. DTO supplies side, resolution timestamp and **postmortem** deadline, but no resolution deadline, contact identity or URL. | Clarify presentation mapping. `postmortem_due_at` is not resolution due time; `resolved_at` is not a deadline; side is not an assigned person. Retain narrower truthful display while decisions remain open. |
| **MON1146-013** | Jira `/items/1/status`, `/comment/comments/0`; auth tasks:52; rollout:5 | Ready-for-test/MR mention is not completion. Historical auth release approval exists independently of incident integration. | No task closure, runtime attestation, reopened general auth gate or extended approval. Backend fake-incident upsert is separate from frontend local demo. |

### Dictionary seed detail

Jira specifies:
- `p0` Критический/10, `p1` Высокий/20, `p2` Средний/30, `p3` Низкий/40.
- `platform` Команда ЦАМ/10, `team` Команда навыка/20.
- `open` Открыт/10, `acknowledged` Подтверждён/20, `resolved` Устранён/30.

Each requested dictionary has code varchar(32) PK, display_name varchar(100), sort_order smallint, is_active boolean default true. These are requested storage rules, not proof of deployed data or generic catalog DTO constraints.

## Architecture

The existing plan composes incident and operational read blocks inside `skill-details`, independently of MOS-1025 metrics. Each source retains its own loading/error/retry; failure must not hide the skill questionnaire or other successful blocks.

Data boundaries:
1. Public per-skill GET → validated envelope and incident read model → read-only presentation.
2. Catalog lookup, once agreed → labels without discarding historical incident codes.
3. Internal upsert → backend synchronization/testing boundary, **not** a frontend business editor.
4. Shared session and transport retain normal readiness, credential-destination and stale-context safeguards.

Specs establish agreed behavior and ownership, not inspected implementation.

### Preserved access/mock boundaries

- User approval of auth release gate **09.10.2026** remains recorded and closed in its historical scope. It is neither this agent’s runtime verification nor incident-specific rollout approval.
- Configured dev/mock versus real mode remains distinct from permitted credential destination. Hostname does not activate auth.
- Permissions govern UI visibility; backend authorizes requests. No incident grant, role mapping or frontend request ACL is invented.
- The requested backend fake-incident endpoint is not the Express frontend demo, not evidence of real external synchronization, and not authorization to alter demo fixtures.
- No surrounding monitoring-settings or responsible-editor write scenario is activated. Their explicit conditional gates remain untouched; MOS-1146 itself remains frontend read-only.

## Start Here

Open **`openspec/changes/mos-1026-skill-operations-info/proposal.md:24–27`**, then its complete design/spec/tasks. This is the existing owner whose blanket incident-API absence statement can be narrowly reconciled without creating a duplicate plan.

A future explicitly authorized documentation package could:
1. Correct publication traceability in proposal/design/tasks.
2. Add incident field/nullability, ordering and dictionary-preservation scenarios.
3. Keep external URL/deadline/label and source-status questions explicit.
4. Retain read-only scope, independent source failures and unclosed integration acceptance.

No such edits are authorized by this report.

## Open questions and limits

For future product/API-owner reconciliation—not execution blockers:
- Which lookup keys resolve incident dictionaries, and how are inactive historical values returned?
- Is `team` or `owner` the agreed side code, and is any migration/compatibility behavior intended?
- What supplies a resolution deadline, external URL and any person-level responsibility?
- How should additional statuses and equal detected timestamps be ordered?
- How are missing skill, unconnected source and upstream failure distinguished on the wire?
- What are omitted-field semantics for internal upsert updates? Optional request properties alone do not establish clearing versus preservation.

No missing input blocked this bounded audit. No implementation, database, runtime, production permissions, deployment or test coverage was inspected. Wiki attachments and linked MR content were not read. Publication gaps are not backend-nonexistence claims. Independent review remains required.