# Code Context

## Files Retrieved

Read the complete assignment and all four owning-plan files; no implementation inspected. Locator aliases below expand to these exact paths:

- **P** `openspec/changes/mos-1256-feedback-lifecycle/proposal.md` (1–34): scope and preserved PUT.
- **D** `openspec/changes/mos-1256-feedback-lifecycle/design.md` (1–53): ownership, lifecycle decisions, confirmation integration and uncertainty.
- **S** `openspec/changes/mos-1256-feedback-lifecycle/specs/feedback-lifecycle/spec.md` (1–40): requirements and scenarios.
- **T** `openspec/changes/mos-1256-feedback-lifecycle/tasks.md` (1–10): implementation/verification tasks, all open.
- **R** `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1256.md` (1–97): accepted 36 rows (23–58), source-only unknowns (71–80).
- **V** `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-G2-FEEDBACK-REQUIREMENTS-RESUME.md`: read complete; used lifecycle acceptance/integrity (1–51). Export text incidental, not compared.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-LIFECYCLE-EXPORT-SPEC.md`: complete assignment, only SPEC-G2-MOS-1256 executed.
- **F** `openspec/changes/mos-1249-feedback-api/specs/feedback-api/spec.md` (1–38): sole related-plan follow-up, explicitly linked by D:37, to resolve permission-key and mutation-error/retry ambiguities. This is agreed-plan reading, not API/source-contract inspection; no shared policy/history reread.

Hashes are parent-attributed from assignment/review, not recomputed. R's historical “pending” heading does not override the assignment's accepted status and V:31–51 ACCEPT. No new source extraction or freshness certification.

## Key Code — requirement-to-plan mapping

No code analysis: this table maps accepted rows, using exact owner clauses/scenario names rather than creating new requirements. **Covered** includes design and existing umbrella verification T:8 (task 2.1), not just repeated spec wording. All R01–R36 below mean 1256-Rxx.

| Accepted rows | Exact owner scenario/task mapping | Assessment |
|---|---|---|
| R01 | S:9 lookup codes; D:27; T:3 task 1.1 | Covered. Dictionary is not an allowed-transition matrix. |
| R02–R03 | D:27 saved-card pause/resume; T:3 task 1.1 names both; S:9 PUT status | Covered action semantics; no separate pause/resume scenario required. Accepted source supplies active↔paused, not arbitrary transitions. |
| R04–R06 | S:9 and “Disable versus delete” S:13–16; D:13,27; T:3–4 tasks 1.1–1.2 | Covered: disabled, not archived; CRUD retention; soft-delete/no restore. |
| R07–R08 | S:9,11,13–16,23–26; D:27,31; T:3–4 | Covered separate confirmations. |
| R09–R11 | S:9 and “Dirty card lifecycle action” S:18–21; D:27,31; T:3 save/cancel and retained input | Covered, including save/operation failure. S:9 applies dirty protection before separate operation, not only status-form submission. |
| R12 | T:4 task 1.2 “раздельные pending”/“отсутствие … двойного удаления”; T:3 one confirmed PUT | **Partial wording gap:** DELETE duplicate prevention explicit; repeated status submission while pending is not explicitly prohibited. One PUT per confirmation does not alone state pending re-entry prevention. |
| R13 | D:35 existing transport, D:42 no blind retry; F:9 mutations MUST NOT auto-repeat, “Unknown mutation outcome” F:21–24 | Covered by retained common transport policy. Local repetition optional. |
| R14–R16 | S:9 detail/registry/counters on server result; D:27 confirmed outcome; T:4 list/detail/counts | Covered for lifecycle success; task placement under DELETE does not negate broader S:9. |
| R17 | S:9 repeated DELETE 404 not success; “Disable versus delete” S:13–16 detail/export 404; D:27; T:4 no false success, T:10 task 2.3 | Covered collectively. Repeating all three 404 contexts in one sentence is optional, not new export scope. |
| R18 | S:9; D:27; T:4 and T:10 | Covered occupied code after deletion. |
| R19–R22 | S:11 both paths/cancel/one combined PUT; “Disable through ordinary form save” S:23–26; D:31; T:3 | Covered; button path explicit in requirement/task although named scenario illustrates form path. |
| R23 | D:31 expressly skips second PUT if preliminary save already reached target; P:12; T:3 one PUT, S:11 no repeated status PUT | Covered. A separate scenario/test-task restatement is optional. |
| R24 | S:11 and “Edit an already disabled survey” S:28–31; D:31; T:3 | Covered. |
| R25–R26 | D:35–37 preserves linked UI-only permissions; F:26–33 specifies `TSAM.ManagedResource:update/delete`, status uses update, each UI owner checks policy; T:8 umbrella component verification | Covered by explicit incorporation. No new authorization model or request ACL. |
| R27–R30 | T:3–4 checks disabled/delete, confirmations, dirty draft, 404; T:8 component umbrella; S:13–26 | Covered component obligations, not executed tests. |
| R31 | T:3 errors retain input + T:8 component umbrella; linked F:16–19 “Validation and inactive references” identifies 409 and preserved error payload | Covered error behavior/umbrella verification, less locally explicit than 404. Naming 409 in an existing check is useful traceability, not a mandatory separate test task or missing recovery design. |
| R32 | T:4 unknown outcome + T:8; D:42 baseline retained/no blind retry; linked F:21–24 | Covered unknown-outcome component obligation and existing reread boundary. |
| R33–R36 | T:3 explicitly both paths, cancellation, one PUT, unchanged disabled + T:8 component umbrella; S:11,23–31 | Covered; no duplicate per-assertion test tasks needed. |

## Architecture

D:21,31: entity owns API/query keys; editor/draft owner hosts the single disable-confirmation mechanism. MOS-1251 wires ordinary submit, MOS-1256 wires the separate action, without sibling-feature imports. Dirty separate actions save explicitly or cancel; confirmed form save combines changes in one PUT; preliminary save reaching target suppresses redundant PUT. Confirmed results refresh server-backed detail/list/counts; disabled retains CRUD while confirmed DELETE soft-deletes. Shared transport/session and UI-only permission policies remain unchanged (D:35–37, F:9,21–38).

### Existing answers to accepted source-only unknowns

- **Method:** D:27, S:9, T:3 preserve published PUT under D-066; no PATCH correction or renewed API inquiry.
- **Unknown outcome:** D:42 retains baseline/explains uncertainty/no blind retry; F:21–24 forbids guaranteed success/cancellation and permits explicit current-state reread. This resolves part of R boundary 3 without inventing reconciliation/retry machinery.
- **409:** F:16–19 already preserves status/code/message/JSON Pointers; local errors preserve input (T:3/S:21). Detailed copy and specialized recovery remain unspecified, not automatic blockers.
- **Unknown/inactive status values:** D:43 says preserve source data, do not replace with defaults or invent renderers. No inferred transition permission follows.
- **Permission shorthand:** F:28 resolves delete to `TSAM.ManagedResource:delete`, status to update; F:33 assigns UI policy verification to each owner. Backend remains authorizer.
- **Confirmation integration:** D:31 answers mechanism/owner and both entry paths. Cancellation preserves draft without requests; exact wording, field rollback and delete-dialog details remain unspecified. Do not reset draft by inference.
- **Still unspecified, no invented choices:** complete transition matrix, pending lifetime/error copy, post-delete navigation and exact counter identities. S:11's “from any other status” is a confirmation condition, not permission for every transition. None requires choosing Q1 or expanding scope. Actual endpoint/error/permission/CORS confirmation remains release evidence D:53/T:10, not this S-lane's job.

### Minimal correction / no-op candidates

1. **Narrow supported correction candidate (R12):** extend existing T:3 task 1.1 check to explicitly prevent repeated status submission while pending. Optionally express the same general lifecycle pending rule in S:9; do not add a state machine or separate test task. DELETE is already covered by T:4. This is a plan-specificity omission, not proof of an implementation bug.
2. **Optional only:** name 409 alongside existing error/component checks in T:3–4/8 for direct R31 traceability. Existing common 409 contract plus local error preservation/component umbrella already covers the obligation; no new recovery rule.
3. **No-op:** dirty draft, both confirmation paths, cancellation, combined PUT, save-already-reached-target suppression, unchanged disabled, disabled/delete distinction, occupied code, 404 false-success avoidance, no automatic retries, unknown outcomes and permissions. Repeating these across proposal/design/spec/tasks or adding one task per assertion adds no required behavior.
4. **No-op on historical prototype details:** no archived, browser `confirm()` mandate, toast placement/duration, restoration, client transition matrix, responses/export expansion, or question-options/Q1 choice. Only existing MOS-1250/1251 integration dependencies retained.

No material missing assigned input or unapproved product choice was needed; no affected conclusion required escalation. Publication/review and any edits remain parent's responsibility. This is plan coverage, not implementation acceptance or task closure.

## Start Here

Open `openspec/changes/mos-1256-feedback-lifecycle/tasks.md` line 3 for the sole narrow pending-status clarification candidate, then compare design line 31 to avoid duplicating already-complete confirmation/deduplication behavior.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"All 36 accepted MOS-1256 rows mapped to exact owning clauses and existing shared-plan references; narrow pending-status wording gap separated from covered behavior and optional 409 repetition."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/035012ee-f634-45c5-99f3-cbbf11cf9574/spec-1256.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"nl -ba on owning plan, accepted report/review and explicitly linked feedback-api spec; sed for selected numbered ranges","result":"passed","summary":"Read-only exact-line inspection; no source execution or validation commands."}],
  "validationOutput": ["36/36 rows mapped; only configured external report written.","Tests/build/network/API/code audit intentionally not performed."],
  "residualRisks": ["Parent-attributed hashes; no independent freshness certification.","Transition matrix and detailed UI copy/navigation remain unspecified; no choices inferred.","Plan coverage does not establish implementation or release-gate correctness."],
  "noStagedFiles": true,
  "diffSummary": "External artifact only; no repository edits or staging performed.",
  "reviewFindings": ["R12: status pending duplicate-submission prevention lacks explicit local wording; DELETE already covers it.","Other accepted behaviors covered; 409 local restatement optional."],
  "manualNotes": "Full owner plan and accepted requirements read. Only essential explicitly linked foundation spec followed to resolve source unknowns. PUT, Q1 and scope boundaries preserved; no extraction, implementation audit or task closure."
}
```
