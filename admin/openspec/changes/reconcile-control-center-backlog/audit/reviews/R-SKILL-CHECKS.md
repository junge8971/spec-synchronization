# R-SKILL-CHECKS — independent decision review

## Decision

**Accept the narrow planning reconciliation; revise publication chronology and sharpen recovery wording.** No implementation, backend-readiness declaration, task closure, or additional lifecycle command is authorized. The material five-check, recalculation, persistence-on-rejection, and preflight-boundary claims withstand independent primary-source inspection.

## Code Context / Files Retrieved

Repository-relative paths; JSON evidence uses exact pointers rather than enormous single-line quotations.

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/R-SKILL-CHECKS.md` (1–8): assigned scope.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-SKILL-CHECKS.md`: entire report; evaluated its five-check table, flow/concurrency map, disagreements, and proposed artifact targets.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1): seven scoped operation descriptions, response references, check/request/detail schemas.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/content.json`: only `/items/0` (MOS-1245), especially `/description`, `/status`, `/attachments/0`.
- Both corresponding `metadata.json` files (API 1–19; Jira 1–8): capture limits.
- `docs/api/contracts/openapi-2026-10-15.raw` (line 1): corresponding descriptions, existing preflight operation and historical detail schema. `docs/api/contracts/openapi.json`: exact preflight path/requestBody inspected.
- `openspec/specs/skill-checks-training/spec.md` (1–70), `skill-lifecycle/spec.md` (1–98), `skill-registration/spec.md` (1–179), `skill-card-editing/spec.md` (1–49), `skill-connection-settings/spec.md` (1–58), `skill-training-phrases/spec.md` (1–78), all under `openspec/specs/`: baseline requirements and recovery boundaries.
- `openspec/changes/mos-1018-skill-phrase-conflicts/{proposal.md,design.md,tasks.md}` (1–27, 1–26, 1–18) and `specs/skill-phrase-conflicts/spec.md` (1–47).
- `openspec/changes/mos-1023-skill-environment-tokens/{proposal.md,design.md,tasks.md}` (1–27, 1–26, 1–18) and `specs/skill-environment-tokens/spec.md` (1–47).

No application code or unrelated completed review was inspected. Large combined tool outputs truncated their beginnings; the missing creation description and checks/lifecycle baseline sections were separately retrieved before conclusions.

## Exact evidence notation

**A** = saved api-live content above; **J** = saved Jira content, `/items/0/description` with named heading.

Exact operation pointers in A:

- **C** `/paths/~1api~1control~1api~1skills~1v1~1skills/post/description`
- **D** `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/get/description`
- **U** same detail path with `/put/description` and `/patch/description` (both read).
- **I** `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1intents/put/description`
- **T** `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post/description`
- **P** `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1phrase-conflicts~1check/post/description`

## Findings and dispositions

### 1. Five persisted checks — ACCEPT

A `/components/schemas/SkillCheckType/enum` gives `anketa`, `phrases`, `exact_conflicts`, `semantic_conflicts`, `endpoint`; `/components/schemas/SkillCheckStatus/enum` gives `passed`, `failed`, `warning`, `blocked`. `/components/schemas/SkillCheckResponse/required` requires type, status, blocking, nullable message, checked_at. D and J “Статусы и инварианты” establish blocked-only blocking, passed/null message, corrective messages otherwise. J explicitly says these five rules do not currently generate failed, but it remains supported and nonblocking.

J “Типы и правила проверок” supports the report's per-check rules, including active/nondeleted phrase participation, exact versus semantic separation, endpoint completeness without network probing, and preserving domain validation. Do not invent a technical-error-to-failed mapping or client calculation.

**Smallest planning edit:** amend `skill-checks-training/spec.md:9–21,63–70` only for actual persisted result display, including empty/uncomputed, failed/nonblocking, messages and timestamps. Preserve processing/applied-version/sandbox deferrals. This needs an approved follow-up owner, not implementation in the audit change.

### 2. Recalculation and stale reads — ACCEPT

C persists five results but returns only ID. D reads without recalculation and permits `[]`. U recalculates submitted dependent fields even unchanged, returns checks, and leaves peer version/updated_at unchanged. I replaces groups, recalculates old/new conflict peers, does nothing to checks/version for a no-op, and returns no checks. `/components/schemas/UpdateSkillIntentsResponse/properties` confirms the absence. Detail SkillResponse requires checks at `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/required`.

**Smallest planning edit:** response consumption in `skill-card-editing/spec.md:22–25,41–44` and `skill-connection-settings/spec.md:32–49`; post-intents detail read in `skill-training-phrases/spec.md:23–26,47–50`. Retain existing observation/manual refresh (`skill-checks-training/spec.md:23–61`), last-read semantics, dirty-input protection, and no all-status polling promise. Same version is not proof that checks are unchanged. No peer event feed is evidenced.

### 3. Rejected promotion persists checks — ACCEPT

T expressly preserves recalculated checks/new checked_at while status, version and history remain unchanged on readiness rejection. J “Интеграция с жизненным циклом” forbids successful status/history changes but does not require check rollback: **added detail, not a demonstrated contradiction**.

T documents ordered blockers with `field=/checks/{check_type}`, `code=BLOCKED`, corrective message. However the same operation's `/responses` lists only 200 and 422. Accept semantic blocker handling as a planning requirement; **reject inventing a guaranteed typed 409 envelope, extra correlation fields, or a response containing full refreshed checks**.

**Smallest planning edit:** `skill-lifecycle/spec.md:66–69` gains a detail read after `SKILL_CHECKS_BLOCKED`, retaining unchanged status and displaying all documented blockers. If that read fails, retain last-loaded data with read error, disable commands pending successful refresh per existing lines 23–26, and do not repeat POST. API error examples/contract alignment remain needed.

### 4. Concurrency and approved commands — ACCEPT

U serializes name/domain edits with phrase writes, waits at most ten seconds, and distinguishes `PHRASE_REGISTRY_BUSY` (nothing saved) from `VERSION_CONFLICT` (neither data nor checks saved). I documents serialized writes and both skills becoming blocked for concurrent identical phrases; this is backend acceptance, not something the UI can guarantee by local matching. T separates busy, blockers, invalid transition (422), version conflict and idempotency-key reuse.

**Smallest planning edit:** extend `skill-lifecycle/spec.md:51–59` and edit-save scenarios with distinct known rejection versus unknown outcome handling, preserving input and explicit confirmation. No synthetic countdown/queue position, automatic overwrite, or automatic mutation retry.

Only `draft→checking`, `sandbox→review`, `whitelist→prod` remain approved UI commands (`skill-lifecycle/spec.md:9–16,47–49`). Test blocker/warning behavior on the latter two; draft→checking does not recalculate per T. **Reject expanding commands from the published forward chain, return transitions, or mention of disabled.**

### 5. Registration refresh recovery — REVISE for explicitness

The report correctly preserves POST→GET→PUT and distinguishes phrase-save success from failed checks refresh. Its target “Skill created but detail loading failed” (`skill-registration/spec.md:101–104`) describes the **pre-PUT GET**, not a post-save checks read.

**Smallest planning edit:** add a separate scenario alongside “Completed registration” (116–119): once POST and required PUT are confirmed, a subsequent GET failure means registration writes succeeded but latest checks could not be read. Retry only GET; do not replay PUT/POST or mark confirmed phrase saving incomplete. Keep the existing pre-PUT recovery scenario unchanged. This clarifies the report's intended behavior, not a new product choice.

### 6. MOS-1018 API-absence wording — REVISE chronology; ACCEPT safe correction

P unequivocally documents read-only **single-phrase** preflight, self-exclusion, global active-group comparison, percent similarity, exact-first/descending-semantic order, configurable default threshold, and other-team skill/domain names. It does not persist readiness or establish freshness of an entire edited set.

Independent historical/local inspection adds a precision correction: `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1phrase-conflicts~1check/post` already exists in **both** `docs/api/contracts/openapi.json` and `docs/api/contracts/openapi-2026-10-15.raw`, including requestBody referencing `PhraseConflictCheckRequest`. The historical description is absent. Therefore describe **newly documented semantics**, not a newly introduced method. The report correctly identifies new descriptions but its “newly published method” wording is too broad.

**Safe planning correction:** replace blanket absence in MOS-1018 `proposal.md:25` and `design.md:3`; qualify design line 13 and annotate task 1.1 with publication evidence. Suggested substance: “The saved contract publishes a single-phrase method and documents scope/score/order; accepted normalization examples, whole-input binding, safe disclosure and the concrete send action with server revalidation remain unresolved.”

**Do not close task 1.1 or bypass tasks.md:3.** Preserve proposal line 26, design 14–16/21–22, tasks 2.2–2.4, and spec 30–47. Add a preflight-does-not-persist-readiness scenario. **Reject choosing phrase save versus review submission from API presence alone.** Saving conflicting phrases is supported; promotion blocks; neither decides the product's preflight-required action. Cross-team names in documentation do not constitute disclosure approval or authorize extra detail requests/client RBAC.

### 7. Alleged source disagreements — ACCEPT as open alignment, not precedence decisions

- **Zones:** J questionnaire rule includes zones; A CreateSkillRequest/UpdateSkillRequest properties and U trigger list omit it; baseline registration lines 28–30/52–55 still require it. Preserve the discrepancy. **Reject adding a zones payload or assuming domain derivation.** Owner decision needed.
- **Threshold:** J names 0.75; I/P specify configurable default 0.75. Record qualified difference, not proven runtime conflict or frontend constant.
- **Backfill:** J acceptance requires initial calculation for existing skills; D permits uncomputed empty results. Migration compatibility is plausible, not established completion or duration. Keep empty UI state and separate backend acceptance.
- **Normalization/deletion:** J has more exhaustive rules than descriptions. Omission is not cancellation; ask for boundary examples rather than implementing guesses.

### 8. Token/sandbox deferrals and ownership — ACCEPT, bounded

MOS-1023 `tasks.md:3–5`, `design.md:13–17`, spec 35–47 retain separate metadata/disclosure/rotation/security requirements. Endpoint passed is neither service health, token issuance nor sandbox dialogue readiness. No readiness-driven task closure/change is supported.

The reviewed active artifacts do not own complete persisted-check UI coverage. An approved follow-up owner remains necessary. This review does not independently claim an exhaustive inventory of all active changes; it verifies the two assigned active owners and six baseline targets only.

## Architecture / Start Here

Server writes calculate persisted results; detail GET observes them. Peer recalculation can change checks without record-version movement. Blocked promotion is a special persistence boundary. Transient single-phrase preflight is separate from both persisted checks and token/security contracts.

Start with `openspec/specs/skill-checks-training/spec.md:9–11,63–70`, D and T; then apply the narrowly scoped MOS-1018 factual wording correction. Product approval remains required for follow-up ownership/scope, agreed send, disclosure, zones and configuration alignment. None is silently resolved here.

## Validation and limits

Local read-only JSON extraction and numbered artifact reads only; no network, MCP, browser, tests, generation, source/spec edits or nested agents. Historical checks/descriptions absence and preflight operation presence were directly checked. Jira is “Ready for test”, not test evidence; attachment body/comments are unavailable in the saved set. No runtime, migration, implementation completeness or deployment readiness was verified. Only this bound report was written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Primary API/Jira evidence independently checked against six baselines and both active changes; per-finding accept/revise/reject dispositions and minimal planning edits recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SKILL-CHECKS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read-only Python JSON extraction of scoped API operations, historical/local preflight and MOS-1245 only","result":"passed","summary":"Confirmed persisted check semantics, response limits and historical preflight existence."},
    {"command":"Numbered local baseline and MOS-1018/MOS-1023 artifact reads","result":"passed","summary":"Verified command, recovery, preflight and token/security gates."},
    {"command":"Tests, generation, network, browser, MCP","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Core reconciliation accepted; publication chronology and post-save read-recovery targeting require precision edits."],
  "residualRisks": ["Saved publication is not runtime, migration or backend-readiness evidence.","Zones, threshold configuration, whole-input preflight binding, agreed-send and disclosure remain owner decisions.","409 typed envelope/examples and Jira attachment body are not established by inspected evidence; no exhaustive active-change inventory performed."],
  "diffSummary":"Only the authoritative review report written; no source/spec edits or staging operations.",
  "reviewFindings": ["revise: preflight method predates new descriptions.","revise: distinguish post-PUT checks read failure from pre-PUT registration recovery.","accept: narrow persisted-check planning reconciliation with existing command/token/sandbox gates intact."],
  "manualNotes":"Independent primary-source review only. Index state was not inspected; no staging action was performed. Product decisions were preserved rather than selected."
}
```
