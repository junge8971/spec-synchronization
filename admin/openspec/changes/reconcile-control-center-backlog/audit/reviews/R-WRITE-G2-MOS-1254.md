# Code Context

## ACCEPT — R-WRITE-G2-MOS-1254

**Mandatory corrections: none.** Accept only the exact proposed documentary diff, not implementation or publication completion. Repository unchanged; parent integrates and validates.

## Files Retrieved

Literal roots: `C=openspec/changes/reconcile-control-center-backlog`, `A=openspec/changes/reconcile-control-center-backlog/audit`, `O=openspec/changes/mos-1254-feedback-questions`.

- Full owner: `O/proposal.md:1–34`, `O/design.md:1–53`, `O/tasks.md:1–10`, `O/specs/feedback-questions/spec.md:1–30`, `O/.openspec.yaml:1–2`.
- Full candidate `A/reports/WRITE-G2-MOS-1254.md`; full governing `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`; `A/decisions.md:1–31`; both minimal-plan WRITE/review briefs (only assigned unit executed).
- Full accepted evidence and dispositions: `A/reports/REQ-G2-MOS-1254.md:1–133`, `A/reviews/R-REQ-G2-MOS-1254.md:1–66`, `A/reports/SPEC-G2-MOS-1254.md:1–160`, `A/reviews/R-SPEC-G2-MOS-1254.md:1–73`, `A/reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md:1–162`, `A/reviews/R-API-G2-FEEDBACK-SURVEY-MUTATIONS.md:1–72`.
- Direct primary clauses: `A/sources/jira-feedback/r1/content.json:57`, complete `/items/5/description`; `docs/api/contracts/crud-api.md:223–239,1199–1280`. Dependency seams: `openspec/changes/mos-1251-feedback-editor/design.md:29–37`; `openspec/changes/mos-1249-feedback-api/design.md:21–24,45–54`. Truncated combined governing output was recovered by separate reads.

## Key Code

- Active-only wording precisely implements Jira AC5/REQ27 and CRUD223–239: **any new selection**, including existing-question type changes, while retaining saved-inactive edit/reorder. Unknown-type behavior is unchanged.
- New scenario explicitly conditions its obligation on parent save **returning a nested 409 or 422 for a question or option**. Placement at that item and retention of all entered draft implement AC6/REQ32–33; task2.1 retains that nested scope. It does not promise every backend error is item-addressed, require both statuses for every field, or prescribe mapping grammar. CRUD1216–1218 and1279–1280 retain form-level errors outside this condition.
- Only design29, spec11/new scenario after21, and existing tasks1.1/2.1 change. All five unchecked tasks, parent submission, PUT, UUID/full-array semantics, accessibility, safety, confirmation, preview ownership and existing release verification remain. No Q1 preserve/omit/block selection, cancel/undo policy, repeated identity exclusions, fixture mandate, new mock scope or duplicate acceptance list.

## Exact-byte verification

HEAD matches assignment: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`.

SHA-256 of reviewed `A/reports/WRITE-G2-MOS-1254.md`: `064d7d7ce43e61c2663356a0a7e77f6c98f995453b1f2c41a4b71f06c752e23c`.
Extracted fenced diff (including trailing newline): `7fe603dce2bef0991c466c747b21eb037a6041b367907b4468c0ee277d0ad9dd`.

| Target under O | Baseline SHA-256 (matches report) | In-memory candidate SHA-256 |
|---|---|---|
| design.md | 181f2800f8e8f359147ef9c9d3a6eb4f3d4daafa20324dd3b8e1cf0c23d54e10 | cb891fc3bdd717c065a93b3b853429079b77081778f3f4657e5f05d832baf101 |
| specs/feedback-questions/spec.md | eeb2d92c74667f09a97d933390176b2771d39a1596a4f0c21cf0e23e39c9d27c | 35e1558375dea280c906f547c7c1234d13bb1023c00f2e3427cd40fe7f06367a |
| tasks.md | 2920f54aba3994e856679db78d4706c553e7a97be0c17d420643b7f3d72fba65 | 8279fa1cd82bb872dae3e3c0a8048325cfa930a458838a8acbcf7056d811e8f6 |

Independently verified every old/context line and hunk count against current bytes, reconstructed candidates only in memory, and confirmed five unchecked tasks. `git apply --check -` exited0; no patch applied. Staged-file listing empty.

## Architecture / Start Here

Start with `O/specs/feedback-questions/spec.md:9–25` and the exact candidate. MOS-1254 remains a nested editor feeding MOS-1251's single draft/save; MOS-1249 retains transport and MOS-1255 preview. D-065–067 support only these bounded corrections.

Residual limits: Q1 remains unresolved/excluded; actual422 envelope/index behavior and live-source freshness are unverified. Existing ambiguous Q1 clauses are intentionally untouched. Strict installed-candidate validation belongs to parent integration; no runtime or feature acceptance.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"ACCEPT exact three-file candidate after full-owner comparison, direct authoritative clauses, baseline/report/diff/candidate hashes and successful read-only apply check; no mandatory corrections."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/74bc6dd6-9269-4000-bf37-ff9f6935f926/R-WRITE-G2-MOS-1254.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"read/find/nl/sed; Python source extraction, SHA-256 and in-memory hunk verification","result":"passed","summary":"Exact candidate and primary clauses verified; all three baselines match and five unchecked tasks preserved."},
    {"command":"git apply --check -","result":"passed","summary":"Exit0, stdin exact fenced diff; no application."},
    {"command":"git rev-parse HEAD; git diff --cached --name-only","result":"passed","summary":"Expected HEAD; empty staged list."},
    {"command":"tests/build/typegen/network/browser; installed-candidate validation","result":"not-run","summary":"Prohibited activities not performed; installation validation deferred to parent."}
  ],
  "validationOutput": ["ACCEPT; mandatory corrections none; repository read-only."],
  "residualRisks": ["Q1 unresolved and excluded.","Saved-source freshness and runtime error envelope/index behavior unverified.","Parent must recheck bytes and validate after integration."],
  "noStagedFiles": true,
  "diffSummary": "External review only; no repository changes or patch application.",
  "reviewFindings": ["No blockers within authorized candidate scope."],
  "manualNotes": "Original SPEC REVISE and corrected classifications were read together. Accepted API evidence reused without repeating its whole schema audit; changed clauses checked directly against Jira and CRUD. No nested agents or delivery claim."
}
```
