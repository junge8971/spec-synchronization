# WRITE-MOS-1260-LABELS — candidate only

Target: `openspec/changes/mos-1260-feedback-export/specs/feedback-export/spec.md`, line 9, existing Server CSV export requirement.

Baseline SHA-256: `a490622da85bbfd7dc20bc4f1714896427541bfeadb639c6de4b5af01994ea2b` — parent-verified per assignment; not independently recomputed. No hashing prerequisite imposed.

## Evidence inspected

Read the complete assignment `openspec/changes/reconcile-control-center-backlog/audit/work-items/WRITE-LIFECYCLE-EXPORT-MINIMAL.md`; complete owning `openspec/changes/mos-1260-feedback-export/{proposal.md,design.md,tasks.md,specs/feedback-export/spec.md}`; complete accepted `audit/reports/REQ-G2-MOS-1260.md`, parent-corrected `audit/reports/SPEC-G2-MOS-1260.md` and unchanged `audit/reviews/R-G2-LIFECYCLE-EXPORT-SPEC.md` under `openspec/changes/reconcile-control-center-backlog/`; and `audit/decisions.md` lines 3–9 (complete D-072).

Accepted R02 requires columns and labels from metadata export_fields. The corrected mapping and unchanged review identify labels as the sole material export omission. D-072 authorizes precisely this clarification. No design conflict found.

## Exact minimal unified diff

```diff
--- a/openspec/changes/mos-1260-feedback-export/specs/feedback-export/spec.md
+++ b/openspec/changes/mos-1260-feedback-export/specs/feedback-export/spec.md
@@ -9 +9 @@
-Список SHALL экспортироваться POST /feedback/surveys/export с fields и текущим применённым search целиком, независимо от страницы. Карточка SHALL экспортироваться POST /feedback/surveys/{id}/export только с fields и только из сохранённых данных. Колонки/порядок SHALL выбираться по metadata export_fields, сейчас name/code/type_code/audience_type/status; минимум одно уникальное поле обязательно. Вложенные данные и пользовательские ответы MUST NOT обещаться в файле. Для новой несохранённой карточки export SHALL быть недоступен; для dirty существующей SHALL поясняться источник сохранённых данных.
+Список SHALL экспортироваться POST /feedback/surveys/export с fields и текущим применённым search целиком, независимо от страницы. Карточка SHALL экспортироваться POST /feedback/surveys/{id}/export только с fields и только из сохранённых данных. Колонки/порядок SHALL выбираться по metadata export_fields, сейчас name/code/type_code/audience_type/status; минимум одно уникальное поле обязательно. Подписи колонок SHALL браться из metadata export_fields. Вложенные данные и пользовательские ответы MUST NOT обещаться в файле. Для новой несохранённой карточки export SHALL быть недоступен; для dirty существующей SHALL поясняться источник сохранённых данных.
```

## Exact old/new text (replacement span within line 9)

Old:
```text
минимум одно уникальное поле обязательно. Вложенные данные
```

New:
```text
минимум одно уникальное поле обязательно. Подписи колонок SHALL браться из metadata export_fields. Вложенные данные
```

Only the sentence `Подписи колонок SHALL браться из metadata export_fields.` is added. The full old/new line is reproduced in the diff. Existing column/order wording, current-inventory qualification, and selected-order scenario (lines 13–16) remain unchanged. No CSV reconstruction or value-label transformation is introduced. Filename, 422, defaults, presentation, tasks and every other requirement remain unchanged; all other files are unchanged in the candidate. No project files were edited.

## Review boundary

Candidate only, not self-accepted publication. Fresh independent review and parent integration/byte validation remain required, together with the separate source-version publication gate. No commands, code/API inspection, network, tests, build or delegation were run; unchanged originals were not represented as candidate validation.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Provided exact one-line unified diff and old/new replacement text adding only metadata-derived column labels, linked to accepted R02 and D-072."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/bc33e9b4-cac8-4cce-ba64-2f2be98dfeb3/labels-candidate.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [],
  "validationOutput": ["Manually compared candidate wording against the complete owning plan and accepted narrow evidence/review; no project validation executed."],
  "residualRisks": ["Baseline hash is parent-attributed; independent freshness and integrated-byte validation remain pending.","Candidate requires fresh reviewer and parent disposition; source-version publication gate remains open."],
  "noStagedFiles": true,
  "diffSummary": "External candidate report only; proposed spec change adds one sentence, with no project edits.",
  "reviewFindings": ["No scope or design conflict found; filename/422/default/presentation changes excluded."],
  "manualNotes": "Read full assignment and all four owning artifacts plus accepted requirement report, corrected mapping, unchanged review and D-072. No staging actions or staging inspection; candidate attestation is not publication acceptance."
}
```
