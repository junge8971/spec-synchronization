# IMPL-MOS-1398 — responsibility assignments: implementation boundary

## Result and scope

**Existing API gate retained.** Current local code provides the skill’s primary questionnaire contact, not MOS-1398 responsibility assignments. No assignment endpoint, provenance DTO, assignment client, mock handler or dedicated assertion was found in the inspected implementation boundaries.

This is additional local implementation evidence for an **already-P** member: **zero new U-to-P**. No publication, acceptance, task closure or editor approval is proposed by this report. Parent alone accepts and queues candidates.

## Controlling evidence read first

Before current implementation inspection:

- `audit/reports/SCENARIO-MOS-1398.md` — complete.
- `audit/reviews/R-SCENARIO-MOS-1398.md` — complete.
- `audit/decisions.md:585–597` — D-014 controlling disposition.
- `audit/work-items/WAVE-D094-LOCAL-EIGHT.md` — common contract and exact assigned row.

Paths above are relative to `openspec/changes/reconcile-control-center-backlog/`.

Preserved mandatory corrections:

1. Wiki backup/prod wording versus Jira is a scope/requirements tension, not proof that existing prerequisites are removed.
2. Revalidation exemption concerns unchanged **`(role,user_id)` assignments**, not a user ID already appearing elsewhere.
3. Enrichment permits **at most one** user-service request per unique user per read.
4. Conditional assignment writes remain unapproved; questionnaire update protocols must not be imported by analogy.

The prior requirement audit was not repeated. Its candidate IDs provide the discovery map.

## Exact primary source

`audit/sources/jira-monitoring-details/r1/content.json#/items/3`:

- `/key`: `MOS-1398`.
- `/summary`: `[B] Ответственные по навыку`.
- `/status/name`: `Backlog`.
- `/updated`: `2026-10-16T19:24:17.680+0800`.
- `/comment`: zero captured/total comments.
- `/attachment`: empty.
- `/description`: storage, role lookup, user enrichment, GET, conditional PUT and migration requirements.

The complete item and corresponding `metadata.json` were read. Capture: `2026-10-16T13:48:06.559Z`; custom fields were not collected. Recomputed content size/hash matches metadata: **44,254 bytes**, SHA-256 `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73`.

## New evidence delta: expected / observed / unknown

| Boundary | Expected from MOS-1398 | Current local observation | Unknown / limit |
|---|---|---|---|
| Persistence and assignment identity | Separate assignment identity; unique skill/role; external nonblank string user IDs; contacts not stored in assignments; deletion/migration rules. | Existing detail contact is a nested primary-contact DTO. `app/entities/skill/api/skill-details-client.ts`, `skillDetailsSchema`, validates nonblank string contact IDs and requires name/email. This is not an assignment collection or persistence model. | Backend tables, FK/uniqueness, migration, deletion and transactional behavior are unverified. |
| Public read contract | GET `/api/control/api/skills/v1/skills/{skill_id}/responsibles`, `items`, assignment identity/date, nullable enrichment and provenance. | Parsed current `docs/api/contracts/openapi.json`: 94 paths; no responsibility path. No `responsibles`, `responsible_roles` or `user_data_source` literals in that document, supplemental contract JSON files, or generated `app/shared/api/schema.d.ts`. | Local publication absence does not prove backend nonexistence or deployment absence. |
| Identity versus primary contact | Assignments remain distinct from `contact_user_id`; one user may occupy several roles. | Current OpenAPI `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/properties/contact` references `SkillContactResponse`; that schema requires `id`, `name`, `email`. `app/entities/skill/ui/skill-questionnaire.tsx`, `SkillQuestionnaire`, renders one “Контакт” row from this object. | No basis to relabel this contact owner/tech/backup or derive roles from team membership. |
| Nullable enrichment and provenance | Missing user/service preserves assignment and `user_id`; `user=null`; `external/mock/unavailable`; at-most-once-per-unique-ID enrichment. | Current detail schema requires its primary-contact object; it has no assignment enrichment/provenance schema. Searches of `app` and `mocks` found no assignment-provenance tokens. | No inspected assertion proves unresolved assignment preservation, deduplicated enrichment requests or provenance handling. |
| Read orchestration/UI | Independently loaded read-only assignment block; empty/error/unavailable distinguished. | `app/entities/skill/model/use-skill-details-query.ts`, `useSkillDetailsQuery`, loads the detail endpoint. `skill-details-tabs.tsx` composes overview/intents/checks/connection/history. `tabs/overview-tab.tsx` renders questionnaire editing/display and unavailable readiness/monitoring messages; no responsibility block. | No runtime behavior was exercised. This is bounded static wiring evidence. |
| Role lookup and inactive-role preservation | Active lookup values; existing inactive/deleted-role assignments remain readable. | `mocks/skill-catalogs.mjs` defines only illustrative skill types, training and autotest values. `mocks/skill-operations.mjs`, `skillOperationHandlers`, provides toggles, phrase conflicts and incidents—not assignments. Full `mocks` token search found no responsible-role/provenance implementation. | Generic catalog schemas do not establish deployed keys. Historical-role label resolution remains an existing owner question. |
| Conditional replacement writes | Only after editor confirmation: atomic replacement, unchanged pair identity/date preservation, validation, empty-list removal and service-failure distinction. | No responsibility mutation found. `skill-details-client.ts`, `updateSkill`, is questionnaire PUT with `Idempotency-Key`; `mocks/domains-skills.mjs:323–345` updates questionnaire fields/relations and primary contact. | Those mechanisms prove neither assignment locking nor stable assignment identities. No assignment version/key protocol is authorized by this analogy. |

The client uses `z.looseObject`; absence of assignment validation is **not** a claim that every unexpected response field would be rejected.

## Actual test assertions inspected — not executed

### `app/entities/skill/api/skill-details-client.test.ts`

Complete file read.

- Fixture uses primary-contact ID `alice-global`, demonstrating the inspected test is not restricted to UUID contact IDs.
- `requests the detail endpoint directly and forwards cancellation` asserts the detail URL and signal, **not** `/responsibles`.
- `rejects invalid contact IDs and timestamps in the API response` includes an empty contact ID and malformed timestamps.
- `preserves 404 instead of converting it into an empty detail` asserts primary-detail error preservation.
- `updateSkill` cases assert questionnaire body forwarding, explicit retry-key preservation and response validation.

These are adjacent contact/detail assertions. They do not establish assignment cardinality, nullable enrichment, inactive-role preservation, provenance or conditional replacement.

### `app/widgets/skill-details/ui/skill-details.test.tsx:428–463`

The test titled `edits nullable fields, dictionary IDs, multiple types and materials without changing contact or connection` asserts an exact questionnaire request body containing version, types, service ID, description, domain/team IDs and materials. It does not send contact, connection or assignment fields.

This supports separation of the inspected questionnaire edit scenario; it does not prove every mutation preserves responsibility assignments.

No dedicated assignment test was located by the bounded `app`/`mocks` token searches. No universal claim about every possible test name or external backend suite is made.

## Current specification ownership

Read current:

- `openspec/changes/mos-1026-skill-operations-info/design.md`, especially **Decisions**, **Risks**, **Migration Plan**.
- `.../specs/skill-operations-info/spec.md`, requirements **Operational contacts and maintenance** and **Read-only and honest source states**.
- `.../tasks.md`, tasks **1.1–1.2**, **2.1**, **2.4**, **3.1**.

Current MOS-1026 still owns the read-only operational-contact scenario, excludes contact editors, prohibits inferring contacts from team members and retains an API gate. Tasks remain unchecked. Its current incident clarification is neighboring context, not assignment implementation evidence.

## Bounded candidate dispositions — parent queue only

| Disposition | Candidate | Recommendation |
|---|---|---|
| **Keep** | MOS-1398-C01–C08, C12 read boundaries | Preserve accepted identity, provenance, inactive-role and ownership requirements with D-014 corrections. Existing MOS-1026 remains owner. |
| **Update evidence only** | C05–C07 / MOS-1026 API gate | Attach current contract, generated-type, client, UI and mock findings: assignment integration is not evidenced locally; primary contact must not substitute for assignments. |
| **Keep conditional** | C09–C11 and conditional portions of C12 | No editor activation, mutation task or transport protocol inferred. Questionnaire PUT tests and in-memory mock atomicity are not assignment persistence evidence. |
| **Question retained** | Historical-role labels, exact enrichment/error schema, backup/prod scope and string/UUID prose | Carry forward previously accepted owner questions; this inspection supplies no authority to resolve them. |
| **No new product candidate** | New implementation delta | Evidence fits existing candidates and owner. No duplicate change, new auth policy or additional requirement proposed. |

## Input hashes

SHA-256 of current local bytes. `A` = `openspec/changes/reconcile-control-center-backlog`; `O` = `openspec/changes/mos-1026-skill-operations-info`.

| Input | SHA-256 |
|---|---|
| `A/audit/work-items/WAVE-D094-LOCAL-EIGHT.md` | `da5e3681c7b882ef8fc6a44a50e7dd8562068f43ac4a74c71a8f5b82e61fd0e0` |
| `A/audit/reports/SCENARIO-MOS-1398.md` | `8065fad2f964bbf4edc6dc86cbf397a8d038bbfc697be687a18e1e1310236175` |
| `A/audit/reviews/R-SCENARIO-MOS-1398.md` | `aef769ed5e5e958fc6971f0aba8ab9d75dacbf012048f1427a7cfedca7591112` |
| `A/audit/decisions.md` | `dbf814a620a9ee1ff1435e912db50efb4672c3e40712f684855a14cc91df796e` |
| `A/audit/sources/jira-monitoring-details/r1/metadata.json` | `a9703f2bda211111fec222610850560f2c4c1160aa198938e0fcb80e3d5746d5` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `docs/api/contracts/skills-domains.openapi.json` | `b3dd3d314f353e37de5ccc0870c23dd26f531227d70d8ecf8195026a16cb5486` |
| `docs/api/contracts/managed-resources.openapi.json` | `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf` |
| `app/shared/api/schema.d.ts` | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |
| `app/entities/skill/api/skill-details-client.ts` | `de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6` |
| `app/entities/skill/api/skill-details-client.test.ts` | `4a0f96da35d60b0a958b27b0ebcafd140ab052d1de1078ec629546f154823762` |
| `app/entities/skill/ui/skill-questionnaire.tsx` | `0ca3fac768c1e4967d1f2a0436a08498ecc6af8aad720ae8ec3bfc5c3d371981` |
| `app/entities/skill/model/use-skill-details-query.ts` | `88db0ee56655ee10d1dbd6df477679ecaedb838181d8339478214d39a16e1bbe` |
| `app/widgets/skill-details/ui/skill-details-tabs.tsx` | `808cd91920c1d73e4dc002b552cdc35035408220f788d04c13be8e50a9ae8237` |
| `app/widgets/skill-details/ui/tabs/overview-tab.tsx` | `db7b60125f91b671f558321680c2727cccb98227e4f3c84b59ca3d8689e5f292` |
| `app/widgets/skill-details/ui/skill-details.test.tsx` | `a69b0948e9aecf25618b1db83c27d06a804885b61ab8848e55f84d260f1558a5` |
| `mocks/skill-operations.mjs` | `da6e06c335b4949672f2e0176135a4030493e5e00d8195a30ebae02c5f911eda` |
| `mocks/skill-catalogs.mjs` | `e43d354e0d3545b9331800652f5e97e8902d3323715b77da70a560336f735318` |
| `mocks/domains-skills.mjs` | `fc9e67e11fbbfde4412524de8901e659f929f7360c9e1e85ac8b36152e0b868c` |
| `O/design.md` | `ba53d8986784adeb4a7822d552df1c931da6aab4d409599a009036d0fce6ecd0` |
| `O/tasks.md` | `da0ad607376b7e3d7c7f508012f726eecf131f9570cee84c73caa8587e50bf2e` |
| `O/specs/skill-operations-info/spec.md` | `352c91a51f2b01e43ec712c33b0310bd04774011fe156c45621e07a950201488` |

Hashes of whole files do not imply whole-file semantic review: widget tests and `domains-skills.mjs` were inspected only at the identified relevant sections.

## Validation and limits

- Performed local reads, file discovery, literal searches and Python standard-library JSON/SHA-256 inspection only.
- A discovery listing of `tests/` returned “Path not found”; tests are colocated in the inspected `app`/`mocks` boundaries. This was not a missing mandatory input or infrastructure failure.
- No writes, network, browser, business requests, tests, builds, lint, typecheck, Git operations or nested agents.
- Work-item baseline HEAD was supplied context, not independently verified. Index state was not inspected.
- Historical saved sources do not establish external freshness. Current local contracts do not establish deployed APIs.
- Backend storage, migrations, locking, user-service behavior and production authorization remain unverified.
- Historical auth approval remains as accepted in D-014; it is neither reopened nor extended. No auth/mock implementation change or policy review was undertaken.
- Frontend business mocks are not proof of the requested backend fake-user adapter.
- No test execution or feature completion is claimed.