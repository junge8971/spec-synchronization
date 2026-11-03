# WRITE-MOS-1256-PENDING — candidate only

## Code Context

### Files Retrieved

Read the full assignment, all four owning-plan files, and all three assigned accepted evidence/review reports; read only D-072 from the decision register. Key locators:

- `openspec/changes/mos-1256-feedback-lifecycle/proposal.md` (lines 1–34): complete scope, PUT and deduplication semantics.
- `openspec/changes/mos-1256-feedback-lifecycle/design.md` (lines 1–53): complete owner design; confirmation and preliminary-save deduplication at line 31.
- `openspec/changes/mos-1256-feedback-lifecycle/specs/feedback-lifecycle/spec.md` (lines 1–40): complete existing requirements.
- `openspec/changes/mos-1256-feedback-lifecycle/tasks.md` (lines 1–10): complete target; five unchecked tasks.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1256.md` (lines 23–58): accepted atomic requirements, including R12.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/SPEC-G2-MOS-1256.md`: read fully; requirement mapping R12 and “Minimal correction / no-op candidates” authorize the narrow clarification.
- `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-G2-LIFECYCLE-EXPORT-SPEC.md`: read fully; “Correction disposition: status pending re-entry — APPROVE” specifies task 1.1 only as the smallest fix.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/WRITE-LIFECYCLE-EXPORT-MINIMAL.md`: full assignment read; only WRITE-MOS-1256-PENDING executed.
- `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (lines 3–9): D-072 authorization and publication boundaries.

### Key text / exact candidate

Target: `openspec/changes/mos-1256-feedback-lifecycle/tasks.md`, task 1.1, line 3 only.

Baseline SHA-256: `b5c7255ec9131d9326dba7b9d5e58d7b15f72f4bce953469d53a7ee3be2bdd5e` — **parent-verified per assignment**, not independently computed. No hashing prerequisite introduced.

Minimal unified diff:

```diff
--- a/openspec/changes/mos-1256-feedback-lifecycle/tasks.md
+++ b/openspec/changes/mos-1256-feedback-lifecycle/tasks.md
@@ -3 +3 @@
-- [ ] 1.1 Добавить PUT статуса draft/active/paused/disabled, действия приостановки/возобновления/выключения и единое подтверждение выключения через кнопку и поле статуса + «Сохранить». Проверка: отмена без запроса/потери draft, подтверждение даёт один PUT, уже disabled не запрашивает подтверждение повторно; disabled остаётся в CRUD, archived не отправляется, dirty draft требует сохранения либо отмены, ошибки сохраняют ввод.
+- [ ] 1.1 Добавить PUT статуса draft/active/paused/disabled, действия приостановки/возобновления/выключения и единое подтверждение выключения через кнопку и поле статуса + «Сохранить». Проверка: отмена без запроса/потери draft, подтверждение даёт один PUT, уже disabled не запрашивает подтверждение повторно; disabled остаётся в CRUD, archived не отправляется, dirty draft требует сохранения либо отмены, ошибки сохраняют ввод; pending запроса смены статуса исключает повторную отправку.
```

Exact old text (whole line):

```text
- [ ] 1.1 Добавить PUT статуса draft/active/paused/disabled, действия приостановки/возобновления/выключения и единое подтверждение выключения через кнопку и поле статуса + «Сохранить». Проверка: отмена без запроса/потери draft, подтверждение даёт один PUT, уже disabled не запрашивает подтверждение повторно; disabled остаётся в CRUD, archived не отправляется, dirty draft требует сохранения либо отмены, ошибки сохраняют ввод.
```

Exact new text (whole line):

```text
- [ ] 1.1 Добавить PUT статуса draft/active/paused/disabled, действия приостановки/возобновления/выключения и единое подтверждение выключения через кнопку и поле статуса + «Сохранить». Проверка: отмена без запроса/потери draft, подтверждение даёт один PUT, уже disabled не запрашивает подтверждение повторно; disabled остаётся в CRUD, archived не отправляется, dirty draft требует сохранения либо отмены, ошибки сохраняют ввод; pending запроса смены статуса исключает повторную отправку.
```

### Architecture / rationale

Accepted R12 says “Pending исключает двойную отправку”. Existing task 1.2 already covers DELETE pending/double deletion. The single-PUT confirmation and preliminary-save deduplication rules do not explicitly prohibit repeated status submissions while pending. This addition expresses only that missing verification obligation, as approved in the independent review and D-072.

Every existing check and PUT remains intact. Tasks 1.1, 1.2, 2.1, 2.2 and 2.3 remain unchecked. No new task, scenario, state machine, retry policy, API change, 409 restatement or scope expansion is proposed. All other lines and all other project files remain unchanged. No project edits were performed.

### Start Here

Review the exact candidate against `openspec/changes/mos-1256-feedback-lifecycle/tasks.md:3`. Fresh independent review, source-version publication gate and parent integration remain required; this artifact does not self-accept or publish the change. No tests or validation of unchanged originals were run or represented as candidate validation.

```acceptance-report
{
  "criteriaSatisfied": [
    {"id":"criterion-1","status":"satisfied","evidence":"Provided exact one-line unified diff and matching full old/new task 1.1 text, preserving all five unchecked tasks and existing semantics; publication risks stated."}
  ],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/bc33e9b4-cac8-4cce-ba64-2f2be98dfeb3/pending-candidate.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [],
  "validationOutput": ["Manual comparison: only a pending-status repeat-submission verification clause is appended to task 1.1; no project files edited.","No hashing, code/API inspection, network, tests, builds or nested delegation performed."],
  "residualRisks": ["Baseline hash is parent-attributed, not independently recomputed.","Fresh independent exact-diff review, source-version publication gate and parent integration remain pending; no implementation or release acceptance implied."],
  "noStagedFiles": true,
  "diffSummary": "External candidate artifact only; proposed project diff changes one line in tasks.md and no other file.",
  "reviewFindings": ["No design conflict or scope expansion identified in the assigned retained evidence; candidate is not self-accepted."],
  "manualNotes": "Full assignment, full owning plan and assigned accepted narrow evidence/review read. No staging performed; no repository staging-state inspection claimed. Parent owns publication and integrated-byte validation."
}
```
