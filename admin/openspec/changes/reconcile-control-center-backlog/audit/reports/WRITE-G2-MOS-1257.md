# WRITE-G2-MOS-1257 — minimal documentary candidate

Candidate only; not applied or independently accepted. Three existing lines of substance plus task1.1 are corrected; proposal, existing scenarios and all five unchecked tasks retain their status. No repository file was written.

# Code Context

## Files Retrieved

Full semantic reads unless a range is explicitly bounded:

1. `openspec/changes/mos-1257-feedback-labels/proposal.md` (1–34), `openspec/changes/mos-1257-feedback-labels/design.md` (1–53), `openspec/changes/mos-1257-feedback-labels/tasks.md` (1–10), `openspec/changes/mos-1257-feedback-labels/specs/feedback-labels/spec.md` (1–25): complete owner; sole delta found by path discovery.
2. `openspec/changes/reconcile-control-center-backlog/proposal.md` (1–30), `openspec/changes/reconcile-control-center-backlog/design.md` (1–133), `openspec/changes/reconcile-control-center-backlog/tasks.md` (1–45), `openspec/changes/reconcile-control-center-backlog/specs/control-center-backlog-reconciliation/spec.md` (1–108): governing process.
3. `openspec/changes/reconcile-control-center-backlog/audit/work-items/WRITE-G2-FEEDBACK-MINIMAL-PLANS.md` (1–25): common contract and assigned owner; neighboring assignments read incidentally, not executed.
4. `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (1–27 only): D-065–D-067.
5. `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1257.md` (1–135) and `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-REQ-G2-MOS-1257.md` (1–61): accepted extraction and ACCEPT.
6. `openspec/changes/reconcile-control-center-backlog/audit/reports/SPEC-G2-MOS-1257.md` (1–144) and `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SPEC-G2-MOS-1257.md` (1–82): parent-corrected report and original REVISE. D-065 accepts bounded corrected findings; no fresh independent ACCEPT is claimed.
7. `openspec/changes/reconcile-control-center-backlog/audit/reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md` (1–162) and `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-API-G2-FEEDBACK-SURVEY-MUTATIONS.md` (1–72): accepted API evidence and ACCEPT; D-066 records subsequent citation-only cleanup.
8. `docs/api/contracts/crud-api.md` (483–517 only): exact §7.1 source for field scope, omission, edge trim and parsed segments.
9. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-feedback/r1/content.json` (77–85 only), `/items/8/description` at line84: assigned issue and all six AC.

No implementation inspection or new API-schema audit was performed. Accepted IMPL findings do not drive any added scope or mock tasks here. Wiki statements are inherited through accepted reports, not independently re-read.

## Key Code / source and decision mappings

No application code changes. Baseline target clauses are design:29, delta:9/11 and task1.1 at tasks:3.

| Changed clause | Exact support | Decision / bounds |
|---|---|---|
| Omitted field on update preserves previous associations, unlike empty-string clearing: design:29, delta:9, task1.1 | Jira line84 AC3; REQ-G2-MOS-1257-07/08; CRUD:509–513; corrected SPEC and original review omission finding | D-065/067 authorize omission correction; D-066 confirms partial-top-level PUT. No requirement to omit every unchanged field; creation defaults are not changed. |
| Per-field 100 distinct / 150 after edge trim / 16000 input: design:29, delta:9, task1.1 | Jira AC4; REQ-11/12/13; CRUD:499–502,515–517; API report label joins and API review findings | D-066 resolves earlier source-only per-field uncertainty. D-067/common contract permits precise wording. No client algorithm, internal-whitespace collapse, Unicode count convention or new numeric limit. |
| Segment audience requires nonempty parsed `segments`, not merely any label: delta:11 and task1.1 verification | Jira AC4; REQ-14; CRUD:512–513; corrected SPEC and API report | D-065/067 precision correction; no nonempty constraint added to tags/operator_groups. |
| Bounded omission-versus-empty and 150/151-after-trim checks in existing task1.1 | Jira AC3/4/6; REQ-08/12/19; original SPEC review substantive corrections | D-067: prospective verification only. Existing test-family lists, no-null/quoted-comma scenarios and task2.1 are not duplicated. |

The reviewed API report's current hash differs from the original review's target hash because D-066 records locator cleanup. This report uses the current corrected artifact, not a claim that its new hash received a fresh independent review.

## Architecture

Private chips feed MOS-1251-owned draft/single save; name strings pass through the entity/API boundary; backend remains normalization authority; canonical response updates saved UI. Changes affect survey associations only. PUT, no global CRUD, no catalogs/suggestions, no role-enforced mocks and existing safety/accessibility/release gates remain untouched. Q1 unknown-type/options policy is outside this patch and remains unselected; preview remains local-only with no answer API changes.

## Start Here

Review `openspec/changes/mos-1257-feedback-labels/specs/feedback-labels/spec.md:9–11` against `docs/api/contracts/crud-api.md:509–517`, then check task1.1's bounded verification. These isolate the smallest substantive correction.

## Baseline SHA-256

Computed over current complete file bytes, not copied from historical reports. Parent must recheck before integration.

| Candidate target | SHA-256 |
|---|---|
| `openspec/changes/mos-1257-feedback-labels/design.md` | `696819963b5df1695641c2fdf0ee6849591ca103b97eeb23e0375aaae062a585` |
| `openspec/changes/mos-1257-feedback-labels/specs/feedback-labels/spec.md` | `7b3704e24f3f64ac9d5d08e20a152bfd245c3b02585c87a5a91e5b641060e24c` |
| `openspec/changes/mos-1257-feedback-labels/tasks.md` | `173a3d33a3242cd2a4cf1540f3fd6f89c027182359f46045f909966955925899` |

Unchanged proposal: `00fef67d22a0c465537f081c16948042d0980641198736d52f3e855780a60846`.

Current evidence SHA-256 (paths under `openspec/changes/reconcile-control-center-backlog/audit/`):

| Evidence | SHA-256 |
|---|---|
| `reports/REQ-G2-MOS-1257.md` | `bab215846ec9451dfe979865097509f2b5adce9cfd683d454bf63047e8d9979d` |
| `reviews/R-REQ-G2-MOS-1257.md` | `229921653804c9db48f6dd8b67a034252402adaf2546fe07df6789b2187a05fe` |
| `reports/SPEC-G2-MOS-1257.md` | `2fc5d7be701420778b67cbff6e65df7731b22fc6c38da6e13c6f53b06a8d0e85` |
| `reviews/R-SPEC-G2-MOS-1257.md` | `8d963bc8fc071e9a12f7f2bed8ac8685d80239184c92959d503d33da3b2527b9` |
| `reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md` | `7ad3581a30759824b88905c5ba6a04f969784b2a04661af4a04d964821de95be` |
| `reviews/R-API-G2-FEEDBACK-SURVEY-MUTATIONS.md` | `522ab17db6d94ace1c484dd5bdb566328822c43b388d94aa3a53d0ab1af0fee0` |

## Minimal unified diff

```diff
--- a/openspec/changes/mos-1257-feedback-labels/design.md
+++ b/openspec/changes/mos-1257-feedback-labels/design.md
@@ -26,7 +26,7 @@
 
 ### Implementation decisions
 
-MOS-1257 владеет chip-вводом tags/segments/operator_groups внутри редактора. Wire — строка имён через запятую, не массив codes/UUID. Удаление chip меняет только связи при сохранении опросника. Пустая строка очищает набор, null недопустим; backend выполняет trim, регистронезависимое устранение повторов и возвращает канонические имена. Лимиты: 100 меток, 150 символов в имени, 16000 во входной строке; запятая всегда разделитель.
+MOS-1257 владеет chip-вводом tags/segments/operator_groups внутри редактора. Wire — строка имён через запятую, не массив codes/UUID. Удаление chip меняет только связи при сохранении опросника. При обновлении пропущенное поле сохраняет прежние связи, пустая строка очищает набор, null недопустим; backend выполняет trim, регистронезависимое устранение повторов и возвращает канонические имена. Лимиты каждого поля: 100 различных меток, 150 символов в имени после обрезки пробелов по краям, 16000 во входной строке; запятая всегда разделитель.
 
 Общий реестр справочников не входит в MOS-1257. Его правила не смешиваются с метками: feedback_statuses системный, остальные семь справочников информационные. Расширение справочника типами с новой семантикой не реализует соответствующий renderer автоматически.
 
--- a/openspec/changes/mos-1257-feedback-labels/specs/feedback-labels/spec.md
+++ b/openspec/changes/mos-1257-feedback-labels/specs/feedback-labels/spec.md
@@ -6,9 +6,9 @@
 
 ### Requirement: Free survey labels
 
-Теги, сегменты и группы операторов SHALL редактироваться chips внутри карточки, передаваться как tags/segments/operator_groups со строками имён через запятую. UI MUST NOT создавать отдельные CRUD-ресурсы меток, генерировать их API-коды или обещать глобальное удаление. Лимиты SHALL быть 100 различных меток, 150 символов в имени, 16000 во входной строке; запятая всегда разделитель. Пустая строка SHALL очищать связи, null MUST NOT отправляться. Канонический результат backend SHALL заменять сохранённое представление после успеха.
+Теги, сегменты и группы операторов SHALL редактироваться chips внутри карточки, передаваться как tags/segments/operator_groups со строками имён через запятую. UI MUST NOT создавать отдельные CRUD-ресурсы меток, генерировать их API-коды или обещать глобальное удаление. Лимиты каждого поля SHALL быть 100 различных меток, 150 символов в имени после обрезки пробелов по краям, 16000 во входной строке; запятая всегда разделитель. При обновлении пропущенное поле SHALL сохранять прежние связи; пустая строка SHALL очищать связи, null MUST NOT отправляться. Канонический результат backend SHALL заменять сохранённое представление после успеха.
 
-При audience_type=segment SHALL требоваться хотя бы одна непустая метка; переключение аудитории MUST NOT само очищать сохранённые метки.
+При audience_type=segment поле segments после разбора SHALL содержать хотя бы одну метку; переключение аудитории MUST NOT само очищать сохранённые метки.
 
 #### Scenario: Canonical labels and clearing
 
--- a/openspec/changes/mos-1257-feedback-labels/tasks.md
+++ b/openspec/changes/mos-1257-feedback-labels/tasks.md
@@ -1,6 +1,6 @@
 ## 1. MOS-1257 — Реализовать ввод тегов, сегментов и групп операторов
 
-- [ ] 1.1 На foundation MOS-1251 (task 1.1) добавить три доступных chip-ввода; сериализация в строки имён без кодов/UUID, пустая строка для очистки. Проверка: добавление/удаление с клавиатуры, запятая как разделитель, 100 меток/150 символов/16000 входных символов и ошибки без потери ввода.
+- [ ] 1.1 На foundation MOS-1251 (task 1.1) добавить три доступных chip-ввода; сериализация в строки имён без кодов/UUID, пустая строка для очистки, пропущенное при обновлении поле сохраняет прежние связи. Проверка: добавление/удаление с клавиатуры, запятая как разделитель, в каждом поле 100 различных меток/150 символов в имени после обрезки пробелов по краям/16000 входных символов и ошибки без потери ввода; пропуск поля сохраняет связи в отличие от пустой строки; имя из 150 символов с пробелами по краям укладывается в лимит, из 151 после обрезки — нет; при audience_type=segment требуется непустой набор segments после разбора.
 - [ ] 1.2 Принять канонические метки backend после сохранения, сохранять исходные связи при переключении аудитории, исключить отдельные CRUD вызовы меток. Проверка: нормализация дублей/регистра из ответа, очистка только связей и отсутствие запросов глобального удаления.
 
 ## 2. Приёмка подзадачи
```

## Validation and limits

- Read-only Python generated the candidate in memory with `difflib.unified_diff` from actual file contents. Every replacement asserted exactly one old-text match; unchecked-marker counts stayed identical. Old/context hunk lines therefore originate directly from the recorded baseline. No candidate target file was materialized.
- `git diff --cached --name-only` returned empty. No staging operations performed. Git status alone would not certify ignored OpenSpec files; full-byte hashes are supplied instead.
- Apply-check: **not run**; no `git apply`, including `--check`, was executed. Parent should validate the extracted diff and fresh baseline independently before integration.
- OpenSpec strict/doctor, format checks, tests, lint/typecheck, build and typegen: **not run**. Candidate not installed; this is documentary preparation, not application or publication validation. Network/browser/business calls and nested agents were not used.
- Saved evidence does not establish current deployment/freshness. Exact Unicode counting/trim repertoire remains unspecified; no new interpretation selected. Formal nullable labels versus prose no-null and error-envelope discrepancies remain API evidence, not changed here. Q1 remains unresolved and unaffected.
- No global audit closure, feature acceptance, code/test changes, new mock queue, main-spec/archive edit or policy choice claimed. Independent candidate review and parent integration remain pending.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"External minimal three-file unified diff, fresh baseline hashes and exact AC/CRUD/decision mappings supplied; limitations and original REVISE lineage retained."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/a764f7bc-1d09-48a2-950a-3cd1247e5cd5/WRITE-G2-MOS-1257.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read/find/scoped grep; read-only Python SHA-256 and in-memory difflib generation","result":"passed","summary":"All old replacement strings matched once; baseline hashes recorded; unchecked-marker counts preserved."},
    {"command":"git diff --cached --name-only","result":"passed","summary":"Empty staged-file list."},
    {"command":"git apply --check; OpenSpec validation; format checks; application checks/typegen","result":"not-run","summary":"Candidate not installed; parent checks after independent review. No tests or typegen authorized."}
  ],
  "validationOutput": ["Three existing target files only; no local candidate writes or repository modifications.","All five task checkboxes remain unchecked in the proposed diff."],
  "residualRisks": ["Independent candidate review, fresh parent baseline check and apply/format/strict validation pending.","Saved documentation is not live/deployment evidence; Unicode precision and API schema/prose mismatches remain.","Q1 unknown-type/options policy remains unresolved and unselected."],
  "noStagedFiles": true,
  "diffSummary": "External report only; proposes omission preservation, per-field distinct/edge-trim precision, parsed-segment wording and bounded existing-task verification.",
  "reviewFindings": ["No blocker to this bounded candidate; original SPEC REVISE and parent corrections preserved, not relabeled fresh ACCEPT."],
  "manualNotes": "Inspected complete owner and accepted reports/reviews plus exact AC3/4 and CRUD7.1. Candidate generated in memory from baseline; no repository write, code change, checkbox closure or runtime acceptance. Parent independently reviews and integrates."
}
```
