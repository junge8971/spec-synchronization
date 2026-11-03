# Code Context

## R-WRITE-G2-MOS-1255 — ACCEPT

**Mandatory corrections: none.** Accept the exact proposed task2.1-only diff, not implementation or publication. Parent retains integration/version-check authority.

## Files Retrieved

Paths below are repository-relative; aliases expand literally: `O = openspec/changes/mos-1255-feedback-preview`, `C = openspec/changes/reconcile-control-center-backlog`, `A = openspec/changes/reconcile-control-center-backlog/audit`.

- Full owner: `O/proposal.md:1–34`, `O/design.md:1–51`, `O/tasks.md:1–10`, `O/specs/feedback-preview/spec.md:1–28`, `O/.openspec.yaml:1–2`.
- Full candidate `A/reports/WRITE-G2-MOS-1255.md`; full accepted `A/reports/REQ-G2-MOS-1255.md:1–110`, `A/reports/SPEC-G2-MOS-1255.md:1–109`, `A/reviews/R-REQ-G2-MOS-1255.md:1–58`, `A/reviews/R-SPEC-G2-MOS-1255.md:1–70`.
- Governing `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`; `A/decisions.md:1–34` (D065–067); full assigned WRITE/review work-items. Truncated combined-read prefixes recovered separately.
- Primary `A/sources/jira-feedback/r1/content.json:59–67`, complete decoded `/items/6`; `A/sources/wiki-247734813/r1/content.json:8`, only decoded `/text[4893:6286]` semantically inspected (Unicode, zero-based, end-exclusive). Whole source bytes hashed, not whole-source semantic review.

## Key Code

The replacement at `O/tasks.md:8` explicitly requires component coverage of seven types, required unanswered/answered including scale/NPS **0** and boolean **false**, live draft changes, and absence of requests **sending trial answers**. Direct Jira AC6 plus AC1–4 support every addition; accepted SPEC review:11–15 and D067 authorize exactly this bounded clarification.

No unrelated editor-traffic prohibition, real-answer API/staging requirement, toast/layout mandate, optional scenario repetition, mock expansion, method substitution or Q1 policy appears. Existing behavior remains in owner delta:9–28 and tasks:3–4. In-memory reconstruction verified the old hunk matches once, only line8 changes, all five tasks remain unchecked, and task2.3—including its local component-evidence exception—is byte-preserved. No patch applied.

### Integrity (SHA-256, complete bytes)

- Reviewed candidate report `A/reports/WRITE-G2-MOS-1255.md`: `62a8529ac1032f0835f68b21368c5173769153dd0e0259655e8d78b29b5e3f3f`.
- Current target baseline `O/tasks.md`: `311d06349f6bf1781845fe300af6cbb6df900c77120899a673a194c77583b12b` — matches candidate.
- Resulting tasks bytes reconstructed solely in memory: `1a123c8a60456a7ee17635dc927a991f4af0bbe06c3ee87600fdc905a4117ee7`.
- All six report/review/source digests recorded in the candidate were independently recomputed and match. Proposal/design/delta digests also match accepted SPEC evidence.
- HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`; staged-path inspection empty.

## Architecture

Foundation draft MOS-1251 → question/options editor MOS-1254 → private MOS-1255 preview with separate local trial answers. This changes evidence specificity only; it neither changes ownership nor adds transport.

## Start Here

Integrate only the reviewed hunk into `openspec/changes/mos-1255-feedback-preview/tasks.md:8` after parent freshness/baseline checks. Installed-candidate validation remains the parent's responsibility. No independent apply-check repeated.

Residual limits: retained-source freshness was not checked live; flattened wiki, unread attachment and omitted Jira fields persist. No runtime/test/deployment correctness or global audit closure established. Repository remained read-only; prohibited execution was not performed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"ACCEPT exact task2.1 diff after full-owner comparison, direct primary-clause inspection, matching baseline/evidence hashes and in-memory preservation checks; no mandatory corrections."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/74bc6dd6-9269-4000-bf37-ff9f6935f926/R-WRITE-G2-MOS-1255.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python JSON extraction, SHA-256 and in-memory hunk reconstruction","result":"passed","summary":"Baseline and evidence hashes match; candidate digest recorded; only task2.1 changes; five unchecked tasks and local exception preserved."},
    {"command":"git rev-parse HEAD; git diff --cached --name-only","result":"passed","summary":"Expected HEAD; no staged paths."},
    {"command":"Patch application/apply-check, tests/build/typegen, browser/network and installed-candidate validation","result":"not-run","summary":"Read-only candidate review; no application; integration validation belongs to parent."}
  ],
  "validationOutput": ["ACCEPT; mandatory corrections: none."],
  "residualRisks": ["Live freshness and retained-source completeness remain limited.","Parent integration/version checks and installed-candidate validation remain; no runtime or delivery acceptance."],
  "noStagedFiles": true,
  "diffSummary": "External review only; repository unchanged.",
  "reviewFindings": ["No blockers within authorized MOS-1255 candidate scope."],
  "manualNotes": "Independently verified exact diff against complete owner, Jira AC1–6, selected wiki preview clause and D065–067; unrelated editor transport and existing local component-evidence exception remain intact."
}
```
