# JOIN-MOS-914 — lifecycle, publication and recovery

## Result and scope

**Bounded static join; parent acceptance and queue integration pending.** Current implementation substantially maps to the agreed surface MVP, not the full historical MOS-914 description. Sandbox exclusion, deferred configuration editing and server-owned restore results remain controlling. Two publication-recovery discrepancies warrant narrow reviewer verification; neither authorizes sandbox activation or policy changes.

Only **MOS-914**, fresh packet `/items/8`, is assessed. MOS-911 owns skill-selection semantics; MOS-913 owns overview/connection presentation; MOS-959 owns the deferred configurator; MOS-960–962 retain sandbox context/chat/synchronization ownership. Shared files do not transfer those members’ coverage.

No files were written with tools. This report is returned for runtime persistence at the assigned output path.

## Sources and prior dispositions

Abbreviations:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `M` = `openspec/changes/archive/2026-10-12-mos-914-surface-lifecycle-mvp`
- `W` = `app/widgets/surface-details/ui`
- `E` = `app/entities/surface`

### Exact fresh source

`A/sources/jira-surface-details-d095/r1/content.json#/items/8`:

- Key: MOS-914; status: **Ready for test**.
- Updated: `2026-10-20T14:31:20.954+0800`.
- Item retrieved: `2026-10-20T16:56:26.548Z`; packet cutoff: `2026-10-20T16:56:26.589Z`.
- `/description`: all described commands; save changed configuration before sandbox; sandbox prerequisite for publication; preserve status on `SANDBOX_CHECK_REQUIRED`; archive prohibits editing; restore returns configured without automatic publication; immediate application of saved Prod settings.
- `/comments/items/0`, ID **1128839**: MR31 reference, not inspected.
- `/comments/items/1`, ID **1128861**: MR32 reference, not inspected.
- `/comments/items/2`, ID **1130795**: historical implementation/testing instructions for five non-sandbox actions, save-before-publication, 409 handling, archive and restore. This is not an executed-test receipt.
- `/comments/total = 3`, with three returned items; `/attachments = []`.
- Adjacent `metadata.json` documents parent-only retrieval, saved MOS-783 membership verification and remaining freshness limitations.

Historical ledger `A/reports/G2-JIRA-MEMBER-JOINS.md:254` records MOS-914 as **U**. Parent alone determines eligibility and any analytical coverage transition.

### Prior evidence consulted

Before implementation inspection, consulted:

- `A/decisions.md`, D-090–D-093;
- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md` and `A/reviews/R-SURFACE-CONFIG.md`;
- `A/publication/DRAFT-SURFACE-D091.md`;
- `A/reports/SCENARIO-MOS-960.md`;
- `A/reviews/R-D093-EIGHT.md`;
- `A/reports/JOURNAL-SURFACE-MVP.md`.

D-004/D-005 were subsequently read directly in `decisions.md`, retaining their configurator corrections: publication of validation rules is not activation; combined wiki persistence and separate API operations remain distinct; immediate Prod application is documentary intent, not a measured deployment SLA.

Read the complete main lifecycle specification and `M/proposal.md`, `design.md`, `tasks.md`, and both capability deltas. Archived checked tasks are historical records, not current test execution.

D090/D091 text-feedback and geometry candidates are outside MOS-914. D093’s sandbox status-versus-session distinction is preserved, not re-audited as additional member coverage.

## Contract locators and source tension

Primary contract evidence:

1. `A/sources/wiki-241082009/r2/content.json#/bodyView`, page revision **5**, body v1.0 dated 08.09.2026:
   - §1: immediate Prod application without republishing/replacing code.
   - §2.5: configuration save, unchanged status, archive rejection `409 SURFACE_ARCHIVED`.
   - §§2.6–2.7: bodyless sandbox/publish; sandbox prerequisite and `409 SANDBOX_CHECK_REQUIRED`.
   - §§2.8–2.11: disable, enable, archive, restore; configured restore and no automatic publication.
   - §2.13: historical named error vocabulary.
2. `A/sources/api-live/r2/content.json`, captured **2026-10-19T08:11:44.238Z**.
3. Local `docs/api/contracts/surfaces.openapi.json`, supplemented by `surfaces.md`.

For exact OpenAPI pointers, define:

`P = /paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}`

Then inspect `P~1{action}/post`, where action is `sandbox`, `publish`, `disable`, `enable`, `archive`, or `restore`; skill save is `P~1enabled-skills/put`.

All six local POST operations have **no requestBody**, and their response definitions equal the saved r2 definitions. Local descriptions are absent; saved r2 descriptions supply these additional published statements:

| Topic | Saved r2 publication | Boundary |
|---|---|---|
| Publish | Rejects draft; otherwise permits publication, including without sandbox and repeatedly from prod; requires greeting and a skill | Differs from wiki sandbox prerequisite and is more permissive than agreed UI eligibility. No precedence or UI expansion selected. |
| Sandbox | Accepts any starting status, including prod/archived | Transport publication does not activate excluded UI or establish a test session. |
| Disable/archive | prod→disabled; disabled→archived | Matches MVP action eligibility. |
| Enable/restore | disabled→configured; archived→configured | Published expectation, not observed backend result. |
| Skill save | Replaces selection; status and updated_at unchanged | Does not guarantee draft→configured or immediate deployed propagation. |
| Failure | Lifecycle descriptions say failed external-service transition does not save status; several conflicts use `409 FAILED` | Historical named codes are not universally guaranteed by current publication. |

`/components/schemas/SurfaceStatusResponse` contains only required `surface_id`, `status`, `updated_at`. It is not readiness/session evidence. Generated locators: `app/shared/api/schema.d.ts:3481–3483`, publish operation `:8383`, restore `:8507`.

The agreed main spec explicitly chooses the narrower MVP UI and accepts actual server restore responses, including prod, without client substitution. These are existing agreements, not decisions made by this report.

## Expected / observed / unknown matrix

Main owner: `openspec/specs/surface-lifecycle-publication/spec.md`.

| Obligation | Expected under agreed scope | Observed static implementation and assertions | Unknown / limitation |
|---|---|---|---|
| Commands and eligibility | **Lifecycle status and actions**, lines 37–68: publish configured/review/sandbox; disable prod; enable/archive disabled; restore archived; no sandbox workflow | `W/surface-details/model/surface-details-action-policy.ts:3–28`; table-driven policy test `:9–30`. Client `E/api/surface-registry-client.ts:121–128,193–208` retains all six bodyless transports. Widget test `:143` checks absent sandbox UI | Transport support does not establish command success or sandbox delivery |
| Save before publication | **Publish requires confirmation and truthful success**, lines 70–123: prepare→PUT skills→fresh GET→eligibility→POST→GET | `use-surface-details-operations.ts`, `publishSurface`: prepares, saves, resets confirmed baseline, refreshes, rechecks, publishes. Widget test `:472–511` asserts exact PUT→GET→POST→GET URL order | This is skills/parameters only, not full configuration or server transaction |
| Save/read failure | Stop publication, retain partial success/draft | Exceptions before lifecycle call terminate sequence; failed PUT does not reset draft; successful PUT resets from server before subsequent failure. Entity skill mutation preserves unrelated cached fields | Read assertions, not execution; no measured races |
| Fresh reads/concurrency | No earlier GET authorizes publication; block competing writes | `E/model/refresh-surface-details.ts:10–23` cancels matching queries before fetch; widget coordinator uses synchronous ref lock; lifecycle controller has its own lock | Inspected tests do not establish every archived task’s delayed-response and cross-action scenario |
| Publish rejection and sandbox error | Preserve confirmed state; never auto-send sandbox; 409 requires manual GET/new action | Error handlers recognize `SANDBOX_CHECK_REQUIRED`; controller cache changes only on mutation success. Tests `:513–551`, `:598–636` cover rejection, explicit refresh and no sandbox | Dedicated sandbox-error fixture uses **422**, whereas wiki specifies **409**; generic 409 is separately covered, not the exact combined case |
| Archive | **Archived surface is read-only**, lines 165–177 | Policy blocks editing/publish; save handler rechecks archived state; content disables editor/save. Test `:417–435` asserts read-only controls and available restore/copy | Server enforcement and archive-during-unsaved-edit behavior are not established by that test |
| Restore | Send restore only; show actual server status, do not force configured or claim publish | Lifecycle coordinator sends selected action; test `:688–708` returns prod and asserts only restore, no publish-success modal | Configured restore is documented; inspected component fixture proves only the accepted prod-response branch |
| Save on prod | Save current editable fields without republishing | `canEditSurface` allows prod; save sends enabled-skills PUT and refresh, no publish; content describes application without another release | Full widget configuration editor is a placeholder; live application timing and external service propagation unverified |
| Deferrals | **MVP editing and deferred functionality boundaries**, lines 179–196 | `surface-details-content.tsx` mounts configurator/history placeholders; publication does not issue configuration PUT | Does not close full historical MOS-914 |
| Cache/read recovery | Mutation and refresh outcomes distinct; read retry must not repeat writes | `use-surface-mutation-controller.ts:43–63` returns response independently of refreshError; test `:157–194` verifies this. Widget test `:638–686` covers separate lifecycle refresh retry | Publication-specific issues below remain |

Current components also use existing permission UI and session guards. This report neither audits nor changes the approved auth model; historical lifecycle-only “no auth additions” wording is not treated as authorization to remove current integration.

## Narrow publication-recovery findings

### MOS-914-F1 — success gate checks detail status, not command status

**Expected:** main lifecycle specification, **Publish requires confirmation and truthful success**, requires confirmed prod response and fresh prod detail; an unexpected command status must not produce publication success.

**Observed:**

- `W/surface-details/model/use-surface-details-operations.ts`, end of `publishSurface`, checks `publishResult.refreshError` and `publishResult.detail?.status !== 'prod'`.
- It does **not** check `publishResult.response.status`.
- `W/surface-details/surface-details-publish-action.tsx`, `executePublish`, has the same omission in its fallback branch.
- Client schema accepts every known lifecycle status, not publish-specific prod.

Thus a valid non-prod command response followed by prod detail is statically capable of reaching success. No backend occurrence or runtime reproduction is claimed.

**Test boundary:** `W/surface-details.test.tsx:472–511` supplies prod for both responses. `E/api/surface-registry-client.test.ts:440–520` validates transport and generic response shape, not this mismatch.

**Candidate:** narrow existing-owner correction/regression: independently require both confirmations; no new endpoint or lifecycle policy.

### MOS-914-F2 — publication refresh failures retain a write-oriented retry control

**Expected:** the same requirement and **Accessible errors, retry and scope boundaries** require only GET recovery after a successful write whose refresh failed.

**Observed:**

- `surface-details-publish-action.tsx`, `renderPublishFeedback`, routes every non-409 error to `retryPublish`, label **«Повторить»**.
- `retryPublish` calls publication again; it does not distinguish failed PUT-refresh or failed POST-refresh from a rejected write.
- `publishSurface` reports “Повторите чтение” on refresh errors, but the feedback callback remains the publication callback.
- After successful skills PUT and failed pre-publication GET, a still-publishable cached state can therefore re-enter preparation and PUT when this control is selected.
- After successful POST and failed final GET, cached prod can instead make that control fail eligibility; it still is not GET-only recovery. A separate read-retry control does exist.

**Test boundary:** `W/surface-details.test.tsx:553–596` selects a **«Повторить чтение»** control; it does not exercise the publication error’s **«Повторить»** callback or establish that no write-oriented alternative remains.

**Candidate:** narrow phase-aware recovery correction under existing lifecycle owner; preserve full preparation retry after genuinely rejected publication. No automatic replay or rollback.

Both findings require independent review before parent acceptance or queuing. They are static counterexample paths, not executed failures.

## Bounded publication candidates

| ID | Classification | Candidate and exact ownership |
|---|---|---|
| MOS-914-C01 | **KEEP** | Existing MVP policy, no visible/hidden sandbox, readable historical statuses, deferred configuration/history. No new product requirement. |
| MOS-914-C02 | **UPDATE evidence** | Attach fresh `/items/8` to existing lifecycle owner and journal reconciliation; record description/comment/MVP divergence without declaring source precedence or closure. |
| MOS-914-C03 | **NEW bounded corrective candidate** | F1 command/detail confirmation mismatch; belongs solely to surface publication orchestration and corresponding regression assertions. |
| MOS-914-C04 | **NEW bounded corrective candidate** | F2 GET-only recovery distinction; belongs to the existing lifecycle recovery requirement, not registration recovery or configurator activation. |
| MOS-914-C05 | **QUESTION / evidence gap** | Exact `409 SANDBOX_CHECK_REQUIRED`, configured restore, archive during unsaved edit, and delayed-read/concurrent-action assertions need targeted verification. Existing checked archive tasks are not substitutes. No tests authorized here. |
| MOS-914-C06 | **KEEP existing question** | Backend archive enforcement, restore outcome, actual Prod application and source-contract differences remain unverified. Do not weaken UI policy to match permissive publication. |

Parent alone accepts, consolidates overlaps and queues candidates. No scaffold, product publication, main-spec synchronization, checkbox closure or coverage mutation is performed.

## Input fingerprints

SHA-256 values computed locally over complete file bytes.

### Primary evidence and owning artifacts

| Path | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| `A/sources/wiki-241082009/r2/content.json` | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` |
| `A/sources/api-live/r2/content.json` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `openspec/specs/surface-lifecycle-publication/spec.md` | `675265a0ba98b45f1d659f6048fe97f2e590a0597d7eda304cdcfe9854ebdd91` |
| `M/proposal.md` | `229e010a89c0fbbd7aa0d44778b070f7e8f7a1824ac11a8a3fe7e510024e30de` |
| `M/design.md` | `86ddcdb9de515531106758ae1ca70fdf0bc278bf1065276e6be7a78968ddd4c3` |
| `M/tasks.md` | `919f0bce3ec3292d3a4ea0be308b8e4f0f3e9f056ca2617a73069e9b16270654` |
| `docs/api/contracts/surfaces.openapi.json` | `9d8ef7ff68e187cebb051e6ee85a9ad333f0af903537a5e181425694c48d9758` |

### Implementation and assertions

| Path | SHA-256 |
|---|---|
| `W/surface-details/model/surface-details-action-policy.ts` | `712c2a86c8c6cb2aa0b34b23d775596a4ae6bce3a3ec8d73b7e0e183a64ea9c4` |
| `W/surface-details/model/surface-details-action-policy.test.ts` | `9c0928758be817cec6cfd81fe43e145d9c53ebb69649806d5c9bf6c5a24c335f` |
| `W/surface-details/model/use-surface-details-operations.ts` | `bd29277f023382cd8559ac486e4175aa96d5a6c3cf6bc32573c934791f4ae3c2` |
| `W/surface-details/surface-details-publish-action.tsx` | `a4fc578042df5d7c14d512c5c3804f9d5edff10ccc3affd9fc8fbc85d806331b` |
| `W/surface-details/surface-details-lifecycle.tsx` | `ff57105794a751a140e2713762ccc40739aa924190d85e3279d9ee063864ea6b` |
| `W/surface-details/surface-details-content.tsx` | `d236139b0cd425670f6f41eadcf2d2bf487d43601bc0ce55a638a8cdd19658a2` |
| `W/surface-details/handlers/surface-details.handlers.ts` | `3ee24d6f3e3c6cd9f67d2c7033ff49b5eb499add63b29370975cd73cc6441e39` |
| `W/surface-details.test.tsx` | `5ff98d3c6e74786075c2060fb207171f56be28a70a9802e13d0fb6e50b9def3c` |
| `E/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `E/api/surface-registry-client.test.ts` | `4d5f93269521aedb76ce4dd722390c92dfa06e86b63af622f952146ef105c886` |
| `E/model/refresh-surface-details.ts` | `dd2687336289fcf99739c193a70c5696791a57ff82b1da0cdd23de553edd7fa8` |
| `E/model/use-surface-mutation-controller.ts` | `bf1ab5b4e2d7c45a285960bcee056661b44001fa5ed6027bdae86381cc672c5e` |
| `E/model/use-surface-mutation-controller.test.tsx` | `4fe9c6b6edf3e19fbf3ca781e49176c2e660208b5dc63b3824a4ffd946ad9c75` |
| `E/model/use-update-surface-enabled-skills-mutation.ts` | `3ea725ae29d746a428e5dcc816ed8a08a846b27c77bcfa62be34ed2762812b9c` |

## Historical and deployment limitations

- Fresh Jira retrieval clears only this packet’s collection gap, not other publication freshness gates.
- Wiki and OpenAPI are saved publications with different dates and semantics, not observed backend behavior.
- MR links were not followed. No attachment body, external service, production propagation, access enforcement or persistence was inspected.
- Tests were **read, not run**. Archived checked tasks and historical comments are not test-pass evidence.
- No browser/network/business API, tests/build/typecheck/lint/format, git mutation, configuration change or nested agent was used.
- Baseline HEAD comes from the assignment; git/index state was not inspected or attested.
- Initial guessed-path lookups found no files; discovery resolved the actual report/code locations. No mandatory source remained missing and no blocking infrastructure failure occurred.