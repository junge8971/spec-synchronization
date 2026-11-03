# Code Context

## Result
SPEC-G2-MOS-1258 only: C1–C10 mapped. Existing owner plan substantially covers the accepted requirements; one narrow candidate is explicit 422 JSON Pointer-to-condition targeting, not generic error handling. No implementation acceptance or project edits.

## Files Retrieved
Complete reads (aliases below are exact paths):
- **P** `openspec/changes/mos-1258-feedback-conditions/proposal.md`, lines 1–34 — scope.
- **D** `openspec/changes/mos-1258-feedback-conditions/design.md`, lines 1–59 — integration and validation decisions.
- **T** `openspec/changes/mos-1258-feedback-conditions/tasks.md`, lines 1–10 — delivery and verification.
- **S** `openspec/changes/mos-1258-feedback-conditions/specs/feedback-conditions/spec.md`, lines 1–42 — normative requirements/scenarios.
- **R** `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1258.md`, lines 1–74 — accepted C1–C10, boundaries and unknowns.
- **V** `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-G2-FEEDBACK-EDITOR-CONDITIONS.md`, lines 1–29 — conditions acceptance at 9–18.
- **A** `openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-EDITOR-CONDITIONS-SPEC.md`, lines 1–21 — full assignment; only 1258 executed.

Additional scoped inspection: searched `openspec/changes/mos-1250-feedback-registry/{proposal,design,tasks}.md` and `openspec/changes/mos-1250-feedback-registry/specs/feedback-registry/spec.md` for pointer/inactive/draft/error clauses to check whether registry supplies the narrow missing targeting obligation. Returned generic error/preservation clauses (proposal:10, design:47–48, tasks:9, spec:46–51), not pointer targeting. These artifacts were not fully read; no saved-filter read was needed. No source extraction, code or API-schema audit.

## Key Code — requirement-to-plan mapping (no code audit)
Each R line below is the accepted requirement anchor; P/D/T/S resolve to the exact paths above.

| ID | Owner clause/scenario and task evidence | Assessment |
|---|---|---|
| C1 (R:23) | S:9; D:31; T:3 (1.1): seven fields, metadata-supported operators, one flat and/or group, maximum 50; rejects unsupported tags/nesting. | Covered; no-op. |
| C2 (R:24) | S:9,13,30–33; D:37,49; T:3: 1–100 unique codes, each 1–1000 characters, last removal deletes condition rather than sending []; inactive lookup checks and preserved source codes. | Covered collectively; do not demand another inactive-code scenario merely because preservation/check wording is distributed. |
| C3 (R:25) | S:9,13; D:37; T:3 value/no-value checks. | Covered: is_empty/is_not_empty absent or null, no required value. |
| C4 (R:26) | S:13,25–28; D:37; P:12; T:3. | Covered: six string operators, 1–1000, literal whitespace/no trim, 1001 blocks apply without draft loss. |
| C5 (R:27) | S:9,15–23; D:31–33; T:4 (1.2). | Covered: query/status/type AND group; audience only explicit group row, no hidden logic change. |
| C6 (R:28) | P:9; T:3–4 editor plus draft/applied, badge/bar/reset; S:11,30–37 (draft removal then application; applied panel); D:27–29 shared applied-search model. | Covered collectively: editing/apply/reset and applied-only search/export/save. No duplicate list of every button required. |
| C7 (R:29) | D:27,37; S:13,15–18; T:4,8,10: same search/counts/export, offset reset, server AND/OR gate; pagination/URL remain registry-owned. | Covered: server evaluation, not local page filtering; no extra pagination owner. |
| C8 (R:30) | D:29; S:11,15–18; T:4: complete URL/history/copy, including conditions/sort/pagination, single validated conversion, invalid-state explanation, clipboard Promise. | Covered; URL encoding unknown already answered by plan. |
| C9 (R:31) | P:10 input preservation; S:28,37,41–42 accessible errors/focus; D:50 real 422-envelope verification; T:8,10 general UI/error and integration checks. | Generic errors/input retention covered. Exact 422 JSON Pointer routing to the affected condition is not stated in these owner clauses or the scoped registry error matches. Narrow candidate below. |
| C10 (R:32) | T:3–4 explicit boundary/value/unknown-operator/inactive/AND/URL checks; T:8 unit/component umbrella; S:9,13,25–33 supplies limits, invalid/empty/no-local semantics; T:10 server gate. | Covered as a combined verification obligation; no task-per-case or cosmetic repetition demand. Tests have NOT been run. |

## Already-answered unknowns and retained limits
- R:56 URL serialization uncertainty is answered by D:29: `q`, repeated `status`/`type`, `sort`, `limit`, `offset`, and JSON `conditions` via URLSearchParams; shared URL ↔ validated search conversion. This does not invent a full conditions wire schema.
- R:56 metadata uncertainty is partly answered by D:31 / S:9: authority is `data.surveys.condition_fields`, supported operators per field. Exact field/operator matrix remains runtime metadata/contract input, not a reason to invent a matrix here.
- D:37 / S:13 answer case/literal semantics: eq/ne/in/not_in case-sensitive, contains/not_contains/starts_with/ends_with insensitive; preserve literal characters and whitespace. They do not explicitly settle uniqueness deduplication comparison rules.
- R:57 last-value behavior is answered specifically by S:30–33: remove from draft, then absent from search after applying. General clear/reset immediacy and empty-group representation remain unspecified; do not extrapolate a default or block coverage automatically (V:17–18).
- Error pointer syntax and actual backend envelope are not established by D:50; release confirmation remains open by D:55,59 / T:10. No API audit performed.

## Independent-review supplement (parent disposition)

Review R-G2-EDITOR-CONDITIONS-SPEC confirms the C9 omission after checking incorporated foundation clauses: mos-1249-feedback-api/specs/feedback-api/spec.md:9,18–19 preserves nested pointers; design.md:54 gives a condition-value pointer example; tasks.md:4 verifies shared409/422 pointers. These transport obligations do not specify condition-editor placement; the shared presentation scenario names1251/1254, not1258. Parent accepts the existing candidate with these supplemental citations. Original external report and review retained; no fresh reviewer verdict fabricated.

## Minimal candidates
1. **Narrow correction candidate — C9 only:** in S's existing advanced-conditions requirement/scenario, make explicit that a server 422 JSON Pointer is mapped to the affected condition without losing entered values. Existing T:8,10 already supplies error/component/integration verification; no separate test task or repeated generic error clauses needed. This restores accepted R:31 semantics, does not select pointer grammar or new API behavior. Parent should review candidate before publication; no edits performed.
2. **No-op — C1–C8/C10:** retain distributed coverage. In particular, do not manufacture gaps from absent repeated inactive-code wording, button lists, saved-filter tasks, or one dedicated test line for every boundary. C9's general error/input-preservation portion is also no-op.

## Architecture
D:21,27–33 assigns normalized selection/API to public `entities/feedback`, base registry/search/URL to MOS-1250, and this editor's contribution to MOS-1258. R:44–50 / V:12 retain saved-filter/export ownership separately. Registry search conditions are not MOS-1251 card display rules (`fb_display_rule`, R:42,49); this comparison authorizes neither display-rule changes nor trigger execution.

Explicit exclusions remain: independent audience AND (A OR B), tags, nesting and local page filtering (P:16; D:13,33); audience sorting and relation-label search deferred (D:33). No union with broader prototype scope, new precedence, checkbox changes or feature/deployment claims.

## Start Here
Open `openspec/changes/mos-1258-feedback-conditions/specs/feedback-conditions/spec.md:7–37` alongside accepted `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1258.md:31`; review only the narrow pointer-targeting candidate against existing generic error coverage.

## Provenance
A:16–17 supplies parent-verified SHA-256, **parent-attributed, not recomputed**: proposal `a38950f7a8478421fbe6932afa0c066823aba7c812683175dd7d762f57c0598f`; design `64e879ed2c1869a8173a35558feed6bb708ba35c2f1c112f811a4903beebb948`; tasks `c749150ccdfb4fc050b808e9a0b72f89f33ab1a15802eb745edf4d1b7ddaa757`; spec `875d5c7c0118d43033967eeca0caf716d1e029008f5034745a742411b720232e`; accepted report `709231d4e390c599842a30e567d2eb0cedbd2f3700ce03e9b4c84bb93fe8a7f8`.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Complete C1–C10 mapping with exact owner/report line anchors, answered unknowns, explicit deferrals and one narrow correction candidate."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/29d40e22-b791-457b-a578-bf632024a780/spec-1258.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"nl -ba on the seven assigned Markdown artifacts","result":"passed","summary":"Obtained exact line evidence; inspection only."}],
  "validationOutput": ["Read complete assignment, four owner artifacts, accepted requirement report and relevant review.","No repository edits, network, tests, source execution or nested agents."],
  "residualRisks": ["Pointer-targeting candidate requires parent review; no backend pointer grammar verified.","Empty-group/general clear timing and exact metadata matrix remain unselected; no implementation or deployment acceptance."],
  "diffSummary": "Configured external report only; repository and task checkboxes untouched.",
  "reviewFindings": ["Candidate: condition-specific JSON Pointer targeting is absent from inspected plan clauses; general errors and input preservation already covered."],
  "manualNotes": "Manual plan-to-accepted-requirement comparison, not repeated extraction or API/code audit. Hashes parent-attributed. No staging operations or git/index verification. General verification clauses counted; no cosmetic duplication requested."
}
```
