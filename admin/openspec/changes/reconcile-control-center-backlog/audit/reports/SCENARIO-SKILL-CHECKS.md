# SCENARIO-SKILL-CHECKS — independent planning reconciliation

## Result

The saved API now publishes five persisted readiness checks and material recalculation/error semantics. This supports a **narrow proposed planning update**, not removal of all readiness gates, approval of new lifecycle commands, or a deployment-readiness conclusion. MOS-1245 is backend work; existing frontend baseline still explicitly defers individual check results. No current active change reviewed owns the complete persisted-check presentation/refresh delta. MOS-1018 owns phrase preflight, not all readiness checks; MOS-1023 retains its separate token/security gate.

Only this report was written. No source/spec changes, tests, generation, network, browser, MCP, git operations, or nested delegation occurred.

# Code Context

## Files Retrieved

All paths are repository-relative. Single-line API sources are cited with exact RFC 6901 pointers below.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-SKILL-CHECKS.md` (lines 1–8): scope and acceptance.
2. `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-API-001.md` (complete report, especially “Material description findings and required scenario follow-ups”): semantic routing input, independently checked against snapshots.
3. `openspec/changes/reconcile-control-center-backlog/audit/reports/API-SCHEMA-001.md` (lines 1–224) and `reports/API-OPS-001.md` under the same audit root (lines 1–134): structural/operation routing inputs; not runtime evidence.
4. `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (complete report, “Active changes and routing evidence” and “Unmatched references and exclusions”): ownership discovery only.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/metadata.json` (lines 1–19), `content.json` (line 1; selected operations/components parsed); `docs/api/contracts/openapi-2026-10-15.raw` (line 1; corresponding operation descriptions and SkillResponse checked).
6. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/metadata.json` (lines 1–8), `content.json` (71-line JSON parsed; **only `/items/0`, MOS-1245**, examined for issue content).
7. `openspec/changes/mos-1018-skill-phrase-conflicts/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-phrase-conflicts/spec.md` (1–47): active preflight ownership and unresolved agreed-send gate.
8. `openspec/changes/mos-1023-skill-environment-tokens/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-environment-tokens/spec.md` (1–47): separate token/sandbox deferral, not a readiness-check implementation target.
9. `openspec/specs/skill-checks-training/spec.md` (1–70), `openspec/specs/skill-lifecycle/spec.md` (1–98): current observation and approved command boundaries.
10. `openspec/specs/skill-registration/spec.md` (1–179), `openspec/specs/skill-card-editing/spec.md` (1–49), `openspec/specs/skill-connection-settings/spec.md` (1–58), `openspec/specs/skill-training-phrases/spec.md` (1–78): existing mutation, refresh, version, and recovery scenarios.

No application implementation was inspected; findings concern planning coverage, not UI defects or completion.

## Key Code / exact evidence keys

For the tables below:

- **A** = `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`, line 1.
- **J** = `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/content.json`, `/items/0/description` (section names identify text within this string).
- **K** = `/paths/~1api~1control~1api~1skills~1v1~1skills`.
- **C** = A at K + `/post/description`.
- **D** = A at K + `~1{skill_id}/get/description`.
- **U** = A at K + `~1{skill_id}/put/description` and `~1{skill_id}/patch/description` (both independently read).
- **I** = A at K + `~1{skill_id}~1intents/put/description`.
- **T** = A at K + `~1{skill_id}~1status/post/description`.
- **P** = A at K + `~1{skill_id}~1phrase-conflicts~1check/post/description`.

These seven descriptions are absent at the corresponding historical raw pointers. Historical qualified SkillResponse lacks `checks`; A adds it to `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/{properties/checks,required}`. This establishes publication change only.

A `/components/schemas/SkillCheckResponse` requires `check_type`, `status`, `blocking`, nullable `message`, and date-time `checked_at`. `/components/schemas/SkillCheckType/enum` is `[anketa, phrases, exact_conflicts, semantic_conflicts, endpoint]`; `/components/schemas/SkillCheckStatus/enum` is `[passed, failed, warning, blocked]`. Schema alone does not encode the cross-field invariants or lifecycle side effects below.

### Five checks: requirements, publication, ownership

| Check | MOS-1245 rule (J, “Типы и правила проверок”, “Статусы и инварианты”) | Publication and reconciliation |
|---|---|---|
| `anketa` | Requires name, purpose, expected_result, domain_id, **zones**, team_id, contact_user_id; missing → blocked/true. | U lists six triggering questionnaire fields, not zones. A `/components/schemas/CreateSkillRequest/properties` and `/components/schemas/UpdateSkillRequest/properties` contain no zones. This is unresolved source alignment, not permission to add a zones field or decide its derivation. |
| `phrases` | At least one active undeleted group containing an undeleted nonempty phrase; otherwise blocked/true. | C starts blocked because creation has no phrases. I recalculates on group replacement; no-op does not recalculate. An empty group collection can be saved without making the skill ready. |
| `exact_conflicts` | Global normalized exact matches with participating other skills block. | I/P document global active-group comparison regardless of team/domain; I additionally says regardless of skill status. Exact and semantic are distinct; C starts passed without phrases. Backend owns matching, not local registry-page comparison. |
| `semantic_conflicts` | Existing matching algorithm, threshold 0.75, warning/false. | I/P document configurable `SKILLS__SEMANTIC_SIMILARITY_THRESHOLD`, default 0.75. T expressly permits promotion with semantic warnings. Do not hard-code the threshold or implement a client classifier. |
| `endpoint` | Both endpoint and nonempty contract_version, otherwise blocked/true; **no network probe**. | C/U describe field-completeness checks and dependent recalculation. Endpoint readiness is not service health, a token, or sandbox availability. |

J requires passed/false/null; all non-passed results have a nonempty corrective message; only blocked has blocking=true. `failed` is supported but none of these five rules currently emits it. D documents the status/message/blocking invariants, but schema permits combinations the prose forbids. Planning should cover a returned failed state without inventing a sixth check or treating it as a blocker. A technical failure must not become passed (J).

J additionally excludes deleted skills/domains/groups/phrases, reuses normalization, and excludes exact matches from semantic results. I/P do not exhaustively describe every deletion/normalization detail: these are **documentation omissions/open verification**, not evidence those requirements were removed.

### Description-only flow and concurrency map

| Evidence | Actual published semantics | Existing coverage and minimal planning delta |
|---|---|---|
| C; J “Автоматическое выполнение” | Create persists all five, blocked does not prevent draft creation; request `checks` ignored; response contains only ID. | Registration already uses POST → GET version → PUT intents (`skill-registration/spec.md:90–104`). Extend “Completed registration” (116–119) to present refreshed checks, never infer readiness from creation. Keep input/domain validation and partial-registration recovery. Do not send client-authored results. |
| D; J “API” | GET returns persisted results in fixed order, performs no calculation, may return `[]` for uncomputed skills. | `skill-checks-training/spec.md:9–21,63–70` still explicitly says results unavailable. Proposed narrow amendment: show actual results/messages/timestamps; empty ≠ passed, refresh ≠ recalculate. Preserve error/stale handling (49–61) and draft protection (23–47). |
| U; J “Автоматическое выполнение” | Partial update; connection:null removes connection. Submitted dependent fields recalculate even unchanged; name/domain also refresh conflict messages for peers. Data/checks one transaction. Peer version and updated_at do not change. | Extend “Save questionnaire” and “Concurrent update” (`skill-card-editing/spec.md:22–25,41–44`) and “Connection save” (`skill-connection-settings/spec.md:36–39`) to consume checks from response. Add same-value recalculation and peer-check freshness scenarios; do not use unchanged peer version/updated_at as proof checks are current. Connection deletion remains backend capability, **not** a new UI action: baseline explicitly forbids it in that form (32–34). |
| U | Name/domain serialized with phrase writes, wait ≤10s; `409 PHRASE_REGISTRY_BUSY`: nothing saved, explicit repeat possible. Other fields do not wait. `VERSION_CONFLICT`: neither data nor checks saved. | Separate busy, stale-version, and uncertain transport outcomes; preserve local edits and existing version/idempotency protocol, no silent overwrite. Add bounded-contention handling rather than a local countdown pretending to know queue position. |
| I; J “Автоматическое выполнение” | Entire intent-group replacement; omitted groups deleted. Recalculate current phrases/conflicts and old/new peers; last conflict removal unblocks both. Concurrent identical phrases block both. No-op changes neither checks nor version. Response has no checks. | Extend “Save and reopen groups” (`skill-training-phrases/spec.md:23–26`) with post-save detail read, no-op and conflict-resolution cases. Refresh failure means saved phrases with unread latest checks, not failed save/retry PUT. Backend owns transaction/serialization and peer consistency; frontend must not fabricate peer results. |
| T; J “Интеграция с жизненным циклом” | Recalculate five before forward checking→training→autotest→sandbox→review→whitelist→prod; missing rows ≠ success; semantic warning nonblocking. Draft→checking and review→draft / whitelist→review skip recalculation. | Extend checks/lifecycle scenarios for backend rejection and warning-only success **within already approved UI commands**. Do not add every published transition: `skill-lifecycle/spec.md:9–16,47–49` deliberately limits commands. Transition dictionary remains server authority. |
| T | On `409 SKILL_CHECKS_BLOCKED`, status/version/history unchanged **but recalculated checks persist**, checked_at changes. Error entries ordered by check display order: field `/checks/{check_type}`, code `BLOCKED`, corrective message. | Extend “Cancel and rejected transition” (66–69) to display all blockers and GET detail after rejection. Preserve unchanged status while refreshing checks; do not discard changes solely because mutation failed/version is unchanged. Failed follow-up GET must preserve last-loaded data and show read error, not retry POST. |
| T | Queue for target training onward, not draft/checking/disabled; busy timeout saves nothing. Invalid transition is `422 VALIDATION_ERROR` with `/status`; stale expected_version is `409 VERSION_CONFLICT`; idempotency reuse is separate. | Extend “Concurrent state change” (51–54) with distinct busy/blocker/version/validation cases. Keep “Unknown transition result” (56–59), no automatic POST retry, fresh explicit confirmation when appropriate. Do not lump all 409s into a version-conflict message. |
| P | Single-phrase preflight is read-only and does not persist readiness; excludes self, returns percent similarity, exact then descending semantic; exposes other-team names. | MOS-1018 task 1.1 can record newly published method/scope/score evidence, but preflight cannot substitute for persisted checks or prove the whole current input ready. Keep freshness/race tasks 2.2–2.4 and unresolved agreed-send/security review. No new client auth policy is implied. |

A response-map check independently confirmed creation uses `TsamResponseSchema_EntityCreatedResponse_`, intents uses `TsamResponseSchema_UpdateSkillIntentsResponse_`, and detail/update/status use `TsamResponseSchema_SkillResponse_`. A `/components/schemas/UpdateSkillIntentsResponse/properties` contains only skill_id/version/intents/updated_at. The status operation’s `/responses` documents only 200 and 422 despite the detailed description’s 409 codes: error-envelope integration needs examples/contract confirmation, not an invented typed 409 payload guarantee.

## Source disagreements, omissions, and open questions

1. **Initial backfill versus empty read:** J acceptance requires initial calculation for existing skills without status changes; D permits empty uncomputed results. These can coexist during migration, but evidence does not establish migration completion or intended compatibility duration. Keep empty-state coverage and backend backfill acceptance separate; do not call empty successful readiness or a proven backend defect.
2. **Questionnaire zones alignment:** J includes zones; U triggers and create/update DTOs omit it. Main registration still names zones (`skill-registration/spec.md:28–30,52–55`). Ask contract/product owners whether readiness derives it through domain or whether documentation needs correction. This audit selects neither source as precedence and does not expand into domain feature review.
3. **Fixed/default threshold:** J says 0.75; publication says configurable default. Record the distinction, request accepted threshold configuration semantics and normalization boundary examples. No client threshold decision follows.
4. **Persist-on-rejection is an added detail, not a demonstrated contradiction:** J prohibits changing status/adding successful history on blocking but does not specify rollback of check rows. T explicitly persists recalculated checks. Plan refresh accordingly after contract acceptance; do not assume all failed mutations roll everything back.
5. **Preflight send gate remains unresolved:** MOS-1018 proposal 25–26/design 13 assert API absence and require choosing which send is blocked. Published P now provides a method and some semantics; I allows saving conflicting phrases with blocked checks, while T blocks promotion. This narrows evidence but does not authorize selecting “save phrases” or “send for review” as the preflight-required action. Update obsolete absence wording only with a qualified publication statement; task 1.1 remains open for whole-input binding, exact normalization, disclosure approval, and agreed action.
6. **Peer freshness:** J/I/U establish automatic peer recalculation, but no event/invalidation feed or processed-input-version field is evidenced. The frontend can reread a detail and use existing observation/manual refresh; it cannot promise real-time freshness across every open non-processing card. Proposed scenario should explicitly retain last-read semantics. Do not broaden polling to all statuses without approval.
7. **Backend-only acceptance:** uniqueness/FKs, stable check ID/created_at, UTC storage, deletion cascade, deletion-triggered peer updates, transaction isolation and technical failure behavior remain MOS-1245 backend responsibilities (J “Хранение”, “Автоматическое выполнение”, “Критерии приёмки”). Response DTO does not expose storage IDs/created_at. These are not missing frontend tasks and were not verified here.

## Exact artifact ownership and proposed task/scenario targets

These are suggestions for planning publication, **not edits or newly approved task IDs**. Do not reopen archived tasks or place product implementation in the managing audit change. No active readiness-specific tasks artifact was identified in LOCAL-001’s product inventory; a separately approved follow-up change must own amendments to the main baselines below. Its change ID/path remains an approval decision, not invented by this report.

| Owner / exact artifact | Proposed target |
|---|---|
| Future approved readiness follow-up → `openspec/specs/skill-checks-training/spec.md` | Amend “Server-owned current processing status” and “Status observation does not establish readiness” narrowly to permit actual persisted-check display. New scenarios: five ordered results; empty/uncomputed; failed/nonblocking and warning; stale read; same-version/new checked_at; refresh is read-only. Retain all observation/process/sandbox restrictions. Suggested task: decode and display check results with unit/component cases, not process simulation. |
| Same follow-up → `openspec/specs/skill-lifecycle/spec.md` | Extend “Safe single-skill transitions” / “Cancel and rejected transition”, “Concurrent state change”, “Unknown transition result”. Suggested task: structured blocker mapping plus follow-up read on `SKILL_CHECKS_BLOCKED`, separate busy/version/422 handling; test blocked rejection, warning-only allowed transition, refresh failure and no auto-retry. No expanded command matrix. |
| Same follow-up → `openspec/specs/skill-registration/spec.md` | Extend “Completed registration” and “Skill created but detail loading failed”; new scenario “Creation with blocked checks is saved, not ready”. Suggested task: preserve POST→GET→PUT recovery and refresh after final phrase save without second creation or false process success. |
| Same follow-up → `openspec/specs/skill-card-editing/spec.md`, `openspec/specs/skill-connection-settings/spec.md` | Extend “Save questionnaire”, “Concurrent update”, “Connection save”, “Save fails”. Suggested task: consume returned checks, preserve edits on busy/version failures; test unchanged submitted values and endpoint-incomplete result. Do not add deletion UI. |
| Same follow-up → `openspec/specs/skill-training-phrases/spec.md` | Extend “Save and reopen groups”, “Failed save stays editable”, retain “Saved version only”. Suggested task: refresh detail after saved replacement, distinguish no-op and read failure, add old/new-peer conflict-clear examples; backend tests own concurrent transaction correctness. |
| Existing `openspec/changes/mos-1018-skill-phrase-conflicts/proposal.md:25–26`, `design.md:3,13–16,21–26`, `tasks.md:5–13`, `specs/skill-phrase-conflicts/spec.md:7–47` | Proposed task 1.1 clarification: replace blanket method-absence claim with saved publication evidence and unresolved acceptance gates. Tasks 1.2/2.1 may use percent/order documentation once accepted; tasks 2.2–2.4 retain preflight staleness/current-input and agreed-send requirements. Add scenario “Preflight does not persist readiness”; preserve “Restricted conflict details” rather than assuming cross-team disclosure approval. |
| Existing `openspec/changes/mos-1023-skill-environment-tokens/tasks.md:3–5`, `specs/skill-environment-tokens/spec.md:35–47` | **No readiness-driven task closure or scope change.** Endpoint completeness and sandbox status do not satisfy metadata/disclosure/rotation/security gate or enable sandbox dialogue. |
| MOS-1245 `/items/0/description` | Backend acceptance remains storage/backfill/recalculation/concurrency. Clarify zones, migration/empty-state and threshold details against published contract; obtain error examples and attachment evidence, not a frontend schema invention. |

## Architecture

Server mutation → transactional dependent checks (including affected peers) → persisted detail results. GET is observation, never execution. Creation/intent saves require detail reads for checks; update/status success already returns them. A rejected promotion is a special persistence boundary: unchanged lifecycle/version but changed checks. Single-phrase preflight is a separate, transient path. Frontend owns truthful rendering, read refresh/error states, user-input preservation and safe mutation UX; backend owns calculation, matching, storage and transition authorization.

## Start Here

Open `openspec/specs/skill-checks-training/spec.md:9–11,63–70` alongside A/D and A/T. This is the narrow baseline that still defers individual results; then amend lifecycle rejection/refresh planning, without expanding the approved command matrix or merging preflight with readiness.

## Validation and evidence limits

Read-only Python inspection parsed both API snapshots, inspected all seven scoped descriptions in full, selected DTOs/response refs, and extracted only MOS-1245 issue content. Saved API and Jira content SHA-256 values independently matched their metadata. Discovery used targeted `find`; active artifacts and named baselines were read locally with line numbers. No truncated source evidence was used.

Jira `/items/0/status` is “Ready for test”; it is workflow metadata, not a passed test or deployment attestation. `/items/0/attachments/0` lists `mos-1245-test-plan.md` (20881 bytes), but its body was not collected/read. Metadata explicitly excludes comments, attachment bodies and custom fields; Confluence is also unavailable in this evidence set. No final product precedence decision can be derived from these inputs. Saved API metadata records capture on 2026-10-16 and no business operation invocation. No runtime, migration, frontend implementation, complete schema compatibility, or backend deployment was verified. Existing deferrals for applied phrase version/training progress/restart, sandbox readiness/tokens, secret operations, and new lifecycle commands remain intact.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently read MOS-1245 and all seven scoped API descriptions; mapped five checks, refresh, rejection persistence, concurrency, exact baseline/scenario ownership and proposed active task clarifications with explicit unresolved evidence."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-SKILL-CHECKS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python extraction of MOS-1245 only","result":"passed","summary":"Selected /items/0 and retained attachment/comment limitations."},
    {"command":"Read-only Python scoped API/historical description and DTO inspection","result":"passed","summary":"Seven new descriptions read in full; response shapes and missing historical checks confirmed."},
    {"command":"Read-only Python metadata SHA-256 verification","result":"passed","summary":"API and Jira saved bytes match metadata hashes."},
    {"command":"Targeted find and numbered local artifact reads","result":"passed","summary":"Reviewed relevant active changes and six main capability baselines."},
    {"command":"tests / generation / network / browser","result":"not-run","summary":"Prohibited by task."}
  ],
  "validationOutput": ["Five check types and four statuses confirmed; creation/intents lack checks responses; detail/update/status carry checks.","No input or infrastructure blocker; unresolved product matters retained as questions, not decided."],
  "residualRisks": ["Missing Confluence, comments and attachment body; publication is not deployment or migration proof.","Zones, threshold and backfill/empty-state alignment need owner clarification; preflight agreed-send and disclosure gates remain open.","No application implementation audit or runtime verification; no active readiness follow-up task artifact yet identified."],
  "diffSummary":"Only bound audit report written; no source/spec edits or staging operations.",
  "reviewFindings": ["Narrow readiness planning update proposed; preserve approved command matrix and sandbox/process/token deferrals.","Refresh after blocked promotion is essential because checks persist although status/version do not change."],
  "manualNotes":"Read-only independent source reconciliation, not endorsement of prior summaries. No product precedence chosen, no backend readiness inferred, no tests executed. Repository index state was not inspected."
}
```
