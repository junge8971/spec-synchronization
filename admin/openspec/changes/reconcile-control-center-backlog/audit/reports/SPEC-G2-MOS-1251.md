# Code Context

SPEC-G2-MOS-1251 only: owner-plan comparison, not requirements extraction or implementation/API audit. **Result: E01–E10 covered; no material owner-plan correction identified.** No project edits, execution, network, tests or delegation. Hashes and HEAD are parent-attributed from the assignment, not independently verified.

## Files Retrieved

All read completely. Exact path aliases used below:
1. P = `openspec/changes/mos-1251-feedback-editor/proposal.md` (1–36): scope and staged delivery.
2. D = `openspec/changes/mos-1251-feedback-editor/design.md` (1–77): data preservation, defaults, ownership and safety.
3. T = `openspec/changes/mos-1251-feedback-editor/tasks.md` (1–13): implementation and acceptance clauses.
4. S = `openspec/changes/mos-1251-feedback-editor/specs/feedback-editor/spec.md` (1–89): normative requirements and scenarios.
5. R = `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1251.md` (1–78): accepted E01–E10, especially 22–31; unknowns 54–59.
6. `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-G2-FEEDBACK-EDITOR-CONDITIONS.md` (1–35): editor ACCEPT at 3–7; no revisions/escalations at 15–20; artifact-only verdict at 30–32.
7. `openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-EDITOR-CONDITIONS-SPEC.md` (1–25): complete assignment, preserved PUT/Q1, parent-attributed hashes and comparison constraints.

## Key Code — requirement/scenario/task mapping

Aliases resolve to the exact paths above; no application code inspected. Each row maps the corresponding accepted R:22–31 row in sequence.

| ID | Exact owner evidence | Assessment / acceptance hook |
|---|---|---|
| E01 | S:9; D:29–31; T:3,7; P:34 | Three tabs, single draft/save, listed root fields, required name/code/type, draft/all, empty questions covered. T:3 explicitly requires independent GET loading and reopening; T:7 final shared payload. No need to duplicate independent loading into another scenario. |
| E02 | S:9; D:31; T:3,6,11 | Name 1–255, code ≤100/regex, owner ≤200, date format; server code uniqueness/no name uniqueness. D:31 explicitly places 409 NOT_UNIQUE at code. Validation and general error/component clauses cover this without a separate test task for every limit. |
| E03 | S:32–47 (Shared surfaces, Missing surface lookup access, Surface selection limit); D:37; T:4 | Segment labels/surface requiredness, paginated 1–100 UUID, rejected 101st with retained set, both-tab synchronization, hidden relations preserved. No Surface:view means no lookup request, UUID fallback and explanation, not invented names. |
| E04 | S:11,20–23,32; D:29,37; T:4,11 | Read-only external responsible UUID/«Не назначен», unchanged value retained without fabricated users; active-only new lookup selection, inactive saved codes retained. T:4 specifically tests responsible preservation; T:11 general targeted verification covers lookup policy. No cosmetic inactive-only task needed. |
| E05 | S:51; D:39,47; T:5 | All 17 display_rules fields covered, including separate dialog_type/dialog_result, priority and exclusive_show. T:5 explicitly implements all rules; no missing field candidate. |
| E06 | S:51–55,67–70 (Quiet hours validation); D:39–41,47; T:5 | Integer ≥0 delays/minima/cooldown, ≥1 frequency limits, integer/null priority; two timezone-free quiet-hour bounds and cross-midnight allowed. Zero differs from absent. Explanation is configuration only, not execution/delivery. Boundary verification explicitly distinguishes zero limit/delay. |
| E07 | S:51,57–65 (One rule changes; Unchanged rules during top-level edit); D:33–35,51; T:5–7,13 | Top-level-partial **PUT**, full questions/surface replacement and full changed rules; existing UUIDs preserved, backend assigns new IDs, baseline refreshed after POST→GET/PUT. T:7 checks subsequent GET without lost IDs/relations/rules; T:13 keeps real integration evidence gate. Label composition remains MOS-1257-owned; no new relation serializer inferred. |
| E08 | S:11,15–18,84–89; D:35; T:3–7,11 | Input survives tabs/errors; dirty navigation guarded; pending prevents duplicate submit; marked hidden tab and focused field. Success/boundary/failure/whole-card component coverage is distributed across T:3–7 plus T:11, not absent because no single task repeats the complete list. |
| E09 | S:55,62–80 (Unchanged rules, Preserve explicit nullable rule values, Clear a nullable rule explicitly); D:45–51; T:5 | Explicit null stays distinct from false/0/any; empty unselected controls; nullable clear sends null, never empty wire strings; trigger nonnullable; defaults only new/schema-absent fields. Exact GET-null→delay 0→full PUT→GET regression and top-level-only omission are covered. Literal «Не задано» duplication is not required by owner clarification. |
| E10 | S:13,25–28 (Confirm disabled selected in form); D:55; T:6 | Button and form paths share confirmation: cancel retains draft/no request; confirm one PUT of all edits; unchanged disabled no reconfirmation. D:55 allocates submit to MOS-1251, action to MOS-1256 and prevents a second PUT when prior explicit dirty-draft save already reached target. |

## Architecture

D:23,59–61: entity owns transport/DTO/query keys; editor owns shared draft and private editors, with public APIs/FSD boundaries. No sibling-feature imports or replacement auth model. P:34, D:21 and T:3–7 preserve **foundation 1.1–1.4 → MOS-1254/MOS-1257 → composition 1.5**. Foundation alone does not close final editor acceptance. S:84 limits unrelated UI scope without cancelling explicit integration dependencies. T:13 requires real agreed HTTP evidence or environment-owner confirmation; mocks are not release evidence (D:73).

## Already-answered unknowns / minimal candidates

- **No-op: defaults.** R:57 lacked exact rule defaults in assigned AC, but D:39 supplies manual, skip_if_rated=true, quiet_hours_enabled=false, any/any, priority=0, exclusive_show=false. D:51/S:55 constrain application to new or schema-absent fields; never fill persisted null. Do not invent other defaults.
- **No-op: null presentation.** R:30 preserves Jira wording «Не задано»; P:12, D:45–51 and S:55 explicitly settle empty/unselected presentation while preserving the semantic distinction. No literal-label correction or new precedence decision proposed.
- **No-op: HTTP method.** D:33, S:51 and T:5–7 implement PUT, preserving D-066 despite historical quoted PATCH. Do not reopen method choice.
- **No-op: verification granularity.** General errors and targeted unit/component acceptance (T:6,11), plus explicit boundary/success/integration clauses (T:3–7,13), count. No demand for duplicate scenario/task wording per row.
- **Residual nondecision:** Q1 unknown-type options remains unselected. D:37/67 code-preservation/fallback language does not choose an unknown question-type options policy. Equal quiet-hour-boundary meaning remains unspecified; do not infer it or make it an automatic blocker.
- **Real gap candidates:** none supported by this comparison. Actual endpoint/errors/permissions/CORS remain the existing release confirmation boundary (D:77, T:13), not a newly discovered plan defect. No checkbox, implementation or deployment completion claims.

## Start Here

Open `openspec/changes/mos-1251-feedback-editor/tasks.md` lines 3–13 first: it makes the foundation/final-integration distinction and existing verification coverage explicit; use S/D locators above for each requirement.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Complete E01–E10 comparison with exact owner file/line aliases, existing answers, no-op candidates and residual nondecisions; all required artifacts read completely."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/29d40e22-b791-457b-a578-bf632024a780/spec-1251.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [],
  "validationOutput": ["Manual owner-plan comparison: all ten accepted requirements covered; no material correction identified."],
  "residualRisks": ["Q1 remains unselected; equal quiet-hour-boundary semantics unspecified.","Runtime/API correctness and release evidence not assessed; existing integration gate remains open absent evidence."],
  "noStagedFiles": true,
  "diffSummary": "Configured external report only; no project edits or staging.",
  "reviewFindings": ["No material owner-plan gap found; retain PUT, nullable semantics and staged integration acceptance."],
  "manualNotes": "Read/search only plus authorized report write. No tests, execution, network, code/API audit or nested agents. Hashes parent-attributed, not independently computed. No extra linked-owner reads needed."
}
```
