# Code Context

## Result

**Already-covered shared surface binding, plus an unanswered historical UI-duplication question; no established contradictory decision.** The first journal row does not approve removing a control, retaining synchronization, or creating another relation. Current MOS-1251 explicitly plans one `surface_ids` set across two tabs. Preserve that agreed planning baseline without treating this audit as renewed policy approval. MOS-1258 concerns registry search conditions, not these card controls.

Only the first data row dated 08.10.2026 and the journal legend are evidence for this supplement. No implementation inspection, feature closure, new auth scope, or planning edits were performed.

## Files Retrieved

Paths are repository-relative; ranges are physical file lines. Embedded JSON locators below identify paragraphs without inventing internal line numbers.

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/JOURNAL-FEEDBACK-AUDIENCE.md` (1–9): assignment.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-250781168/r1/metadata.json` (1–24), `content.json` (1–13): provenance, legend and first data row. Other rows returned in the same strings are excluded.
- `openspec/changes/mos-1251-feedback-editor/.openspec.yaml` (1–2), `proposal.md` (1–36), `design.md` (1–77), `tasks.md` (1–13), `specs/feedback-editor/spec.md` (1–89): full active editor artifacts.
- `openspec/changes/mos-1258-feedback-conditions/.openspec.yaml` (1–2), `proposal.md` (1–34), `design.md` (1–59), `tasks.md` (1–10), `specs/feedback-conditions/spec.md` (1–42): full active conditions artifacts.
- `openspec/changes/mos-1249-feedback-api/design.md` (1–81), `tasks.md` (1–14), `specs/feedback-api/spec.md` (1–38): relevant precedence, CRUD and policy dependencies; not a fresh whole-API audit.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/SPEC-MOS-1250.md`, “Architecture / Key planning contract”, and `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-MOS-1250.md`, sections 1, 3, 4 and “Key Code and Architecture”: ownership context only. The review narrows the earlier SPEC concerns; its rejected new policy-decision blocker is not revived. Their implementation claims were not independently audited or used as evidence.

## Source identity and exact locators

Source: **«Журнал вопросов - для админки ЦАМ»**, page `250781168`, URL `https://wiki.mos-team.ru/spaces/KR/pages/250781168/`, revision r1, page version 8, updated `2026-10-08T18:31:40.254+08:00`, captured `2026-10-19T08:24:54.988Z`. Local SHA-256 independently matched metadata: `cd74e398e690d48e3da571a6c2adf02d8c755856948d98747b8d447ad628244d`.

Locators apply to both decoded `$.bodyView` (content.json:10) and `$.bodyStorage` (:11):

- **J-L**: pre-table legend, fifth top-level paragraph, macro ID `14a1345a-5b10-4152-be8d-2c34a0130ba7`: «РЕШЕНИЕ — по нему приняли решение, и он пока ждёт от нас действий». Seventh paragraph distinguishes «ЗАКРЫТЫЙ — вопрос закрытый, ответ принят».
- **J-R**: first table, `tbody/tr[2]` (header is row 1), first data row, date `08.10.2026`. Later rows share the date; date alone is insufficient. Middle cell is second physical `td`, spanning two columns.
- **J-R/P1–P2**: middle-cell `div.content-wrapper`, paragraph 1 «Глеб:»; paragraph 2 asserts one `survey -> surface` table `fb_survey_surface`, versus two prototype locations: «Основное -> Аудитория -> Поверхности» and «Правила показа -> Триггеры показа -> Поверхности».
- **J-R/PRE1**: first `pre`, quoted model §2.3 `fb_survey_surface`, purpose «поверхности показа опросника», uses registry «Аудитория», main-card «Поверхности», rules «На каких поверхностях». This is a source-attributed model excerpt, not verified backend storage.
- **J-R/P4**: fourth middle-cell paragraph «Правильно понимаю, что это один и тот же набор…»: asks whether changes reflect in the other field, whether a field can be removed, or another relation is needed. Alternatives are questions, not approved requirements.
- **J-R/P5 + OL1**: fifth paragraph «Решение: уточнить на встрече с ГК, с Русланом,»; list item UUID `5589b816-1bab-4179-a7a3-edc007048fd9` asks the effect on ГК of removing surfaces from rules; item UUID `debb3a98-0508-4908-b2a8-b2dc304222e1` asks removal versus retaining synchronization and attributes “тяжело и долго” to developers. No meeting outcome or independent effort assessment appears.
- **J-R/STATUS**: last physical `td`, macro `23e504b4-1547-4275-8469-0c78d920d4b5`, «РЕШЕНИЕ». Read with J-L and action text: the recorded action is meeting clarification, not final removal approval.

## Key Code / planning contract

No application code inspected. Existing planning anchors:

- `openspec/changes/mos-1251-feedback-editor/design.md:29–41`: one draft; `surface_ids` replaces the full set on PUT; separate full `display_rules`; one surface set for both tabs; configuration does not prove real presentation.
- `openspec/changes/mos-1251-feedback-editor/specs/feedback-editor/spec.md:30–47`: **Linked audience and surfaces / Shared surfaces** requires the shared set and reflected edits. `audience_type=surface` requires at least one UUID; maximum 100, pagination and preservation of hidden bindings remain required. Missing lookup access preserves UUIDs without fabricated names.
- Same spec `:49–55`: `trigger_type` and timing/limit fields belong to `display_rules`; no second trigger-specific surface relation is specified. Trigger execution and sending surveys remain excluded.
- `openspec/changes/mos-1258-feedback-conditions/design.md:27–37`, `specs/feedback-conditions/spec.md:7–24`: `audience_type` is a registry condition inside a flat and/or group, not independent `audience AND (A OR B)`. Local page filtering, nested groups and tags conditions remain excluded.
- `openspec/changes/mos-1249-feedback-api/specs/feedback-api/spec.md:7–23`: shared CRUD/search/lookup/metadata and full-card baseline. Existing policy at `:26–38` is unchanged. `design.md:5–23` records explicit user-approved scope and source precedence; journal labels and chronology alone cannot override it.

## Candidate dispositions

### JOURNAL-FEEDBACK-AUDIENCE-01 — shared binding already covered

**Evidence:** J-R/P2, PRE1, P4 versus MOS-1251 design:29–37 and spec:30–47. No proven disagreement.

**Owner/tasks:** MOS-1251 **1.2** (`tasks.md:4`), persistence **1.4–1.5** (:6–7), release check **2.3** (:13). MOS-1249 **1.2** (`tasks.md:4`) remains the DTO/client dependency.

**Recommendation: no-op on requirements/implementation.** Optional provenance cross-reference to the existing shared-binding rationale only. Do not add duplicate work, another table/API field or a second draft. Existing task 1.2 already checks cross-tab synchronization; persistence checks already exist.

### JOURNAL-FEEDBACK-AUDIENCE-02 — historical duplicate-control question

**Evidence:** J-L and J-R/P5 + OL1 + STATUS. The source records a clarification action, not approved removal; source-attributed effort concern is not technical proof.

**Owner/tasks:** MOS-1251 design **Implementation decisions / Open Questions**, spec **Linked audience and surfaces / Shared surfaces** (:30–37), task **1.2** (:4). Only if later explicitly approved, reconcile these artifacts together.

**Recommendation: question/provenance supplement only.** Bounded question: “Is there an explicitly approved outcome of the cited ГК/Руслан clarification that changes the two-control presentation already planned in MOS-1251? If supplied, record its exact source and affected acceptance.” No answer selected here. Missing meeting outcome does not itself invalidate or block the agreed baseline. No mandatory spec update is evidenced; no removal, synchronization policy or new relation is newly authorized by this audit.

### JOURNAL-FEEDBACK-AUDIENCE-03 — keep audience/search/trigger boundaries

**Evidence:** J-R/PRE1 mentions registry audience display; P2 mentions card display triggers. Neither defines registry search-condition semantics.

**Owner/tasks:** MOS-1258 **1.1–1.2** (`tasks.md:3–4`), **Advanced conditions and reproducible selection** (`specs/feedback-conditions/spec.md:7–24`); MOS-1251 **1.3** (`tasks.md:5`) owns display-rule configuration.

**Recommendation: no-op; ownership guard.** Do not introduce registry surface filters or independent audience filters, reinterpret trigger execution, or transfer this question to conditions. Preserve all existing deferred scope and API boundaries.

## Architecture

Planned card flow: two UI locations → one editor-owned draft `surface_ids` → existing feedback CRUD DTO/client → single saved binding as described by the source. Number of controls is presentation; number of persisted relations is contract. Neither defines when a survey triggers. `display_rules` configures that separate domain without frontend execution. Registry `conditions.audience_type` instead selects survey records through server search.

MOS-1249 owns public entity contract/transport; MOS-1251 owns draft/card/rules; MOS-1250 owns registry applied search/URL; MOS-1258 adds conditions. Shared vocabulary does not merge responsibilities. Registry review is ownership context, not grounds to reopen permissions or inspect implementation.

## Start Here

Open `openspec/changes/mos-1251-feedback-editor/specs/feedback-editor/spec.md:30–47` alongside `tasks.md:4`. Both already answer the shared-set concern. Any later approved control-presentation change must explicitly reconcile these clauses, not silently remove a field based on journal status.

## Constraints and residual risks

- Local saved evidence only. No approved meeting outcome appears in the scoped row; no external follow-up attempted.
- Source reports backend model and implementation difficulty; neither verified against code/database/runtime. Planning coverage is not implementation completion.
- No tests/build/network/browser/code audit, staging, spec sync/archive, implementation or policy selection. Only this authorized report written. Read-only Git diff/index inspection returned no tracked or staged differences before report creation; repeated index inspection was empty.
- Full owner artifacts read; unrelated feedback findings deliberately not pursued. Independent review remains separate.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Compared first journal row/legend with full editor/conditions plans and relevant API requirements; supplied stable candidates, exact source locators, targeted tasks and bounded no-op/question recommendations."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOURNAL-FEEDBACK-AUDIENCE.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find/ls; sha256sum; wc -l; nl/sed; git diff --name-only; git diff --cached --name-only","result":"passed","summary":"Scoped evidence inspected; journal hash matched; line ranges checked; tracked/index diffs empty before writing, repeated index check empty."}],
  "validationOutput": ["Shared binding already covered by MOS-1251 task 1.2 and Shared surfaces scenario.","Journal action is meeting clarification, not approved removal or a new relation.","MOS-1258 conditions remain separate; no policy change justified."],
  "residualRisks": ["No approved meeting outcome in scoped evidence.","Backend model, effort claim and implementation behavior not independently verified; tests intentionally not run."],
  "noStagedFiles": true,
  "diffSummary": "Authorized report only; no code/spec/task/source changes.",
  "reviewFindings": ["No established contradictory decision; retain historical UI-duplication question without replacing agreed planning."],
  "manualNotes": "Manually compared full active MOS-1251/MOS-1258 artifacts and relevant MOS-1249 requirements. Registry report/review used only for ownership. No implementation or product-policy decision made."
}
```
