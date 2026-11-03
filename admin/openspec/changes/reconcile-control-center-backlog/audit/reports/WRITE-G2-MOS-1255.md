# Code Context

## WRITE-G2-MOS-1255 — documentary candidate only

One verification-sentence change in task2.1. No repository file changed or candidate materialized locally. Parent must independently review, recheck baseline/source versions, then integrate. No feature completion or global audit closure claimed.

Path aliases expand literally: `O = openspec/changes/mos-1255-feedback-preview`; `C = openspec/changes/reconcile-control-center-backlog`; `A = openspec/changes/reconcile-control-center-backlog/audit`.

## Files Retrieved

- `O/proposal.md:1–34`, `O/design.md:1–51`, `O/tasks.md:1–10`, `O/specs/feedback-preview/spec.md:1–28`, `O/.openspec.yaml:1–2`: full owner artifacts; task2.1 is the sole target.
- `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`: full governing process. Initial combined output truncated its prefix; proposal and design prefix recovered separately.
- `A/work-items/WRITE-G2-FEEDBACK-MINIMAL-PLANS.md:1–21`: complete common contract; only MOS-1255 executed.
- `A/decisions.md:1–90`: returned range read; only D-065–067 at3–33 used as authority.
- `A/reports/REQ-G2-MOS-1255.md:1–110`, `A/reviews/R-REQ-G2-MOS-1255.md:1–58`, `A/reports/SPEC-G2-MOS-1255.md:1–109`, `A/reviews/R-SPEC-G2-MOS-1255.md:1–70`: full accepted reports/reviews. MOS-1255 SPEC disposition is ACCEPT, not one of the other owners' corrected REVISE reports.
- `A/sources/jira-feedback/r1/content.json:59–67`, exact `/items/6` including `/description` at66: only this issue semantically read. `A/sources/wiki-247734813/r1/content.json:8`, decoded `/text[4893:6286]` (Unicode, zero-based, end-exclusive): only preview reference slice semantically read. Whole source files parsed/hashed, not a whole-source semantic review.

No API lane applies to this local-preview clarification (D-067 identifies API applicability to1254/1257/1259). No implementation report, neighboring owner, application code, tests, archive or main spec needed or inspected; static implementation acceptance is not used to expand this patch.

## Key Code — baseline and minimal unified diff

Target: `openspec/changes/mos-1255-feedback-preview/tasks.md`

Baseline SHA-256 (complete file bytes): `311d06349f6bf1781845fe300af6cbb6df900c77120899a673a194c77583b12b`.

Observed HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Hash, not Git visibility of ignored planning files, is the integration precondition.

```diff
--- a/openspec/changes/mos-1255-feedback-preview/tasks.md
+++ b/openspec/changes/mos-1255-feedback-preview/tasks.md
@@ -5,6 +5,6 @@
 
 ## 2. Приёмка подзадачи
 
-- [ ] 2.1 Проверить FSD/public APIs, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты, без browser/E2E.
+- [ ] 2.1 Проверить FSD/public APIs, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты; component-тесты покрывают все семь типов, required без ответа и с ответом (включая 0 для scale/NPS и false для boolean), живые изменения draft и отсутствие сетевых запросов отправки пробных ответов; без browser/E2E.
 - [ ] 2.2 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`; при изменении API-типов — `yarn api:check`, при изменении сборки — `yarn build`. Проверка: записать реальные результаты; environment failures не считать успехом.
 - [ ] 2.3 Перед выпуском проверить локальную проверку preview без сетевого сбора ответов; component-тестами подтвердить отсутствие requests. Проверка: конкретные результаты согласованных HTTP-проверок либо подтверждение владельца стенда без секретов; для локального preview — component evidence. При отсутствии evidence gate оставить открытым.
```

### Changed-clause/source/decision mapping

All clauses modify only `O/tasks.md:8`; none add runtime behavior or named scenarios. Authority for each is D-065's supported suite clarification, D-067's explicit AC6-suite-only authorization and the MOS-1255 common-contract unit.

| Candidate clause | Exact accepted evidence / existing owner |
|---|---|
| Explicit **component** coverage of all seven types | Jira `/items/6/description` AC6; `A/reports/REQ-G2-MOS-1255.md:48–54,70` (R09–15,R31); `O/specs/feedback-preview/spec.md:9` already lists the types. Scale and NPS are distinct types. |
| required without/with answer, including scale/NPS0 and boolean false | Jira AC4/AC6; REQ report60–62,70 (R21–23,R31); owner delta9,11–14. `A/reviews/R-SPEC-G2-MOS-1255.md:11` explicitly supports unanswered-versus-answered coverage, not a new validation policy. |
| Live draft changes | Jira AC1/AC6; REQ report41–47,70 (R02–08,R31); owner delta9 and task1.1. No placement/layout change. |
| Absence of network requests sending **trial answers** | Jira description D2 and AC3/AC6; REQ report58–59,70 (R19–20,R31); owner tasks1.2/2.3 and delta9. No prohibition of unrelated editor transport or real-answer API/staging requirement. |

`A/reports/SPEC-G2-MOS-1255.md:44–46,62–64` and independent `A/reviews/R-SPEC-G2-MOS-1255.md:11–15` establish why generic unit/component wording under-specifies AC6 while optional scenario repetition, exact toast copy and staging expansion are unnecessary. D-067 excludes those optional additions from candidate scope.

### Evidence integrity

Freshly recomputed full-byte hashes; accepted report/source hashes match recorded review evidence:

| File under A | SHA-256 |
|---|---|
| `reports/REQ-G2-MOS-1255.md` | `61207d52e321907edca1799a165a3e26ead9ea9b372395cb7100ffe12e65a065` |
| `reports/SPEC-G2-MOS-1255.md` | `0487438ca9dfae7b512c996439095254bcbf9e3a1d9ec5ba83e5d3f5f70d36a6` |
| `reviews/R-REQ-G2-MOS-1255.md` | `c76592a768b0a70167499572b97e638e803beca1583866748554e1c441b9a554` |
| `reviews/R-SPEC-G2-MOS-1255.md` | `9dc06d6372a5f8f72d3efd58468418b3e4102167d6d74e510800686f9b430b1e` |
| `sources/jira-feedback/r1/content.json` | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| `sources/wiki-247734813/r1/content.json` | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |

## Architecture

MOS-1251 owns the foundation draft; MOS-1254 supplies question/options editing; MOS-1255 immediately projects that draft and owns separate local trial answers. This patch only clarifies future evidence for existing behavior. All five tasks remain unchecked, task2.3's local component-evidence exception is unchanged, and browser/E2E remains prohibited. No Q1 preserve/omit/block choice, PUT edit, mock task, role enforcement, new capability, copy mandate or answer API introduced.

## Start Here

Review `openspec/changes/mos-1255-feedback-preview/tasks.md:8–10` against the diff and retained Jira AC6. Recheck target SHA-256 before integration.

## Validation and limits

- Passed: read-only local JSON extraction and SHA-256 computation; generated unified diff in memory directly from baseline. Exact old/context hunk lines originate from current file bytes, not reconstructed wording. Replacement occurs once; five unchecked tasks and unchanged task2.3 asserted in memory. Manual diff inspection: one line replaced, only task2.1 verification expanded. Final scoped numbered inspection confirmed report locators and file lengths.
- Passed: `git rev-parse HEAD; git diff --cached --name-only`; staged paths empty. No staging performed.
- **Not run:** `git apply --check` or patch application. Parent may perform independent apply check; in-memory generation is not claimed as apply-check success.
- **Not run:** OpenSpec strict validation/doctor, format checks, tests, typecheck, lint, API check/typegen, build, network/browser/business calls. Candidate not installed; commands/test obligations in task text are future obligations, not executed evidence. No repository writes or nested agents.
- Residual risks: retained-source freshness not checked live; wiki flattening, unread attachment and omitted Jira fields remain inherited limits. No runtime, test-suite or deployment correctness established. Parent review/version check/integration pending. Q1 unselected and unaffected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Produced tasks-only one-line unified diff, target baseline hash, source/decision mappings and explicit validation limits for MOS-1255."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/a764f7bc-1d09-48a2-950a-3cd1247e5cd5/WRITE-G2-MOS-1255.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python JSON extraction, hashlib SHA-256 and difflib generation","result":"passed","summary":"Baseline-derived hunk generated in memory; hashes computed; five unchecked tasks and unchanged local-preview gate verified."},
    {"command":"git rev-parse HEAD; git diff --cached --name-only","result":"passed","summary":"HEAD recorded; staged paths empty."},
    {"command":"git apply --check; OpenSpec validation; format/application checks","result":"not-run","summary":"External candidate only; no installation or application checks performed."}
  ],
  "validationOutput": ["Single task2.1 verification sentence replacement; all checkbox states and task2.3 preserved."],
  "residualRisks": ["Independent review, apply check, freshness/baseline recheck and integration pending.","Saved-source limitations persist; no runtime/test/deployment evidence assessed; Q1 remains unselected."],
  "noStagedFiles": true,
  "diffSummary": "External report only; proposed one-line tasks.md clarification, not applied.",
  "reviewFindings": ["No blocker identified within authorized MOS-1255 documentary scope."],
  "manualNotes": "Read full owner and accepted REQ/SPEC evidence; no added scenarios, layout/copy/staging requirements, API or code edits. Parent retains independent acceptance authority."
}
```
