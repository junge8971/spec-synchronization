# SPEC-MOS-1250 — current registry plan coverage

## Result

The plan substantially covers Jira registry requirements and preserves explicit deferrals. Remaining concerns are endpoint/metadata consumption traceability, main permission-policy integration, thin negative/boundary acceptance cases, and uncommitted wiki-only UI details. These are planning findings, not implementation defects or product decisions.

Independently decoded the saved MOS-1250 row and relevant wiki sections and compared them with the complete registry change. The REQ report supplied stable IDs, not proof of coverage. No source precedence selected; no implementation readiness asserted.

## Files Retrieved / locator key

All paths are repository-relative. Abbreviations below expand exactly here.

- **P** `openspec/changes/mos-1250-feedback-registry/proposal.md`, lines 1–34: purpose, dependency, deferrals.
- **D** `openspec/changes/mos-1250-feedback-registry/design.md`, lines 1–57: ownership, URL decisions, safety and release gates.
- **T** `openspec/changes/mos-1250-feedback-registry/tasks.md`, lines 1–11: all tasks, unchecked.
- **S** `openspec/changes/mos-1250-feedback-registry/specs/feedback-registry/spec.md`, lines 1–51: complete requirements/scenarios; only spec file discovered in this change.
- **A** `openspec/changes/mos-1249-feedback-api/specs/feedback-api/spec.md`, lines 1–38: linked operations and permission requirements/scenarios. Mutation clauses are not registry evidence.
- **M** `openspec/specs/control-center-permissions/spec.md`, lines 1–91: linked main requirements and scenarios for matching, feature policy, navigation and server scope.
- **R** `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-1250.md`, lines 1–122: stable extraction IDs.
- **J** `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-feedback/r1/content.json`, `$.items[3]`, independently verified `key = MOS-1250`; `description` under `h3. Описание` (**J-D**) and ordered acceptance bullets (**J-A1…7**). JSON/text locators are authoritative for this string-valued evidence.
- **W** `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247734813/r1/content.json`, `$.text`, sections `2. Общая структура` and `3. Экран «Список опросников»`, subsections 3.1–3.6. Exact heading/quote locators below; no invented line numbers inside the JSON string.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-feedback/r1/metadata.json` and `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247734813/r1/metadata.json`, lines 1–11 each: extraction limits.

## Coverage table

“Covered” means plan evidence, not implementation or successful tests. Grouped ranges are inclusive; all 56 IDs are represented. Task numbers are accompanied by physical lines.

| REQ-1250 IDs | Source locator | Exact requirement/scenario/task evidence | Assessment |
|---|---|---|---|
| 1–3 | J-D entry, creation/detail, three routes | S7–14 Survey navigation and registry / Direct card link; D29 named Feedback entry; T1.1 (line 3) | Covered navigation; no editor implementation implied. |
| 4 | J-D `POST /api/control/api/v1/managed-resources/feedback/surveys/search` | S21–33 server search; A7–9 Contract aligned feedback operations names POST/base; T1.3/2.3 (5,11) | Covered via dependency, exact endpoint absent locally. |
| 5 | J-D `GET /catalogs/lookups/feedback` | S9 labels; A9 lookup path; T1.2/2.3 (4,11) | Partial exact-method traceability: dependency names path, not GET; local consumption/gate present. |
| 6 | J-D `GET … /feedback/metadata` | A9 metadata path; A28 read permission; D19/41 dependency | Partial: registry consumption and metadata-specific scenario/task absent; GET likewise not explicit in A9. |
| 7–9 | J-A1 columns, lookup, unknown code | S9; T1.2 (4), including unknown code and lookup failure | Covered; task supplies negative check without separate scenario. |
| 10 | J-A1 keyboard opening | S9, S44–51 Accessible registry interactions / Keyboard and narrow layout within this task; T2.1 (9) | Covered. |
| 11–16 | J-A2 query bounds, multiselects, empty/short query | S23–33 Server search and base filters / Multi value search / Clearing and stale response; D31; T1.3 (5) | Covered requirements. One-character task exists; explicit 200/201 boundary scenario absent. |
| 17–19 | J-A3 sorts, descending/default, not page-local | S23 server sorts/default and unsupported page-local prohibition; D31/35; T1.3 (5) | Covered requirements; no explicit default/direction/server-order acceptance example. |
| 20–22 | J-A4 API pagination/counters/reset | S23, S27–28, S37; T1.2/1.3 (4–5) | Covered; total versus page size tested in task; limit bounds lack dedicated scenario. |
| 23 | J-A4 late responses | S30–33 Clearing and stale response; T1.3 (5) | Covered clear-query race; other selection races only implicit in task wording. |
| 24–25 | J-A5 full URL/history/copy; W3.5 narrower `q, status, type` | S35–42 Reproducible registry selection / Restore registry link; D33; T1.3 (5) | Covered Jira wording; source disagreement retained, not resolved here. |
| 26 | J-A5 conditions after MOS-1258 | S37 conditional integration; D31; T1.3 “местом для conditions MOS-1258” | Covered future boundary; D33's unqualified wording merits clarification. |
| 27 | J-A5 damaged URL explanation | S37; D33 normalization/explanation; T1.3 valid restoration | Requirement covered; malformed-link acceptance example absent. |
| 28 | J-A5 clipboard success after write | S37/42; D33 Promise; T1.3 refusal | Covered including failure. |
| 29–31 | J-A6 loading/empty/no matches/error-retry | S9, Empty filtered page S16–19; T1.2 (4) | Requirements covered; retry and empty-versus-filtered-zero transitions lack explicit task examples. |
| 32 | J-A6 independent direct detail | S9, Direct card link S11–14; T1.1 (3) | Explicit split: isolated route/UUID test; GET/404 delegated to MOS-1251. Full obligation remains integration-dependent. |
| 33 | J-A6 `new` not ID | S9; T1.1 static new (3) | Covered. |
| 34 | J-A7 unit/component coverage | T1.1–1.3 (3–5), T2.1–2.2 (9–10) | Planned multifilters, short/empty query, pagination, URL and error coverage; no execution claim. |
| 35 | J-A7 existing read UI-policy | D39–41; A26–38 Published feature permissions / Read only user / Server scope denial; T1.1 denied access without load | Partial local traceability; S lacks explicit read-policy clause. Main-policy reconciliation concern below. |
| 36–39 | J-D deferred tags/segments/surfaces/type-name; W3.2 those search fields | P12–16; D13/35; S23 excludes display-type/related-label promises | Deferrals retained; type_code filtering/search is not display-name search. |
| 40–41 | J-D audience sort/independent filter deferred; W3.1 audience checkmark and W3.3 third multiselect | P14; D13/35; S23 allowed sorts/status-type filters | Deferrals retained. Audience display S9 remains required. |
| 42 | J-D conditions MOS-1258; W3.4 builder | P9/14/22; D31; S37; T1.3 | Editor deferred; future common URL integration retained. |
| 43 | W2 list is starting screen | S9 `/feedback` registry; D29; T1.1 | Registry entry covered; no extra redirect inferred. |
| 44 | W2 `по клику на строку таблицы` | S9 keyboard navigation; T1.1 generic navigation | Partial: whole-row mouse target not explicit. |
| 45 | W2 breadcrumb return | Direct card link S14; T1.1 (3) | Covered. |
| 46 | W3.1 `Стрелка «›»` | S9/T1.2 name only business columns | Wiki-only arrow affordance unrepresented. |
| 47 | W3.1 green/yellow/light/gray statuses | S9/T1.2 lookup labels, not colors | Wiki-only visual mapping unrepresented; no status-code conflict inferred. |
| 48–50 | W3.2 name, service code, description | S23 name/code/description API search | Requirement covered; T1.3 has no per-field acceptance. Backend not verified. |
| 51 | W3.3 code beside label, monospace | S9 unknown-code fallback only | Wiki-only rendering requirement unrepresented. |
| 52 | W3.3 `Все ...` clears filter | T1.3 clearing; S19 no-match reset | Partial: does not establish each multiselect's All control. |
| 53 | W3.6 Reset visible only with active filters | S19 no-match reset | Partial: general conditional visibility unspecified. |
| 54 | W3.6 found-count at right | S23/S19 API counters; T1.2 total | Value covered, right alignment unrepresented. |
| 55 | W3.6 create opens empty card/defaults | S9 `/feedback/new`; T1.1 | Navigation covered; defaults not specified here. Follow up with card owner, not registry scope expansion. |
| 56 | W3.6 empty registry prompts first creation | S9 empty dataset; T1.2 empty | Partial: empty state present, creation prompt unspecified. |

## Findings and required follow-ups

1. **Endpoint/metadata traceability (IDs 4–6).** J-D names POST and both GET operations. A9 supplies shared paths, S23 server search, T2.3 search/counters/pagination/lookup but not metadata. A's operation scenarios concern mutations, not these registry reads. Follow-up: explicitly trace registry read consumers and method/path checks to MOS-1249 and identify where registry metadata consumption is verified. This does not establish an absent backend or authorize new APIs.

2. **Permission-policy integration (ID 35).** A28 requires `TSAM.ManagedResource:read`, with read-only/403 scenarios A30–38. D41 links it; T1.1 denies access without load. M's `Explicit feature policy` has no ManagedResource row and requires explicit `*` for other uncovered operations; its `Unmapped dialogs` scenario demonstrates the fallback, not a registry-specific decision. P24–26 says no modified capabilities and existing permissions remain. The feature mapping exists, but incorporation into the main-policy fallback is not traced here. Follow-up: reconcile/document the applicable policy extension and registry menu/direct-route/no-load/read-only acceptance. Do not choose wildcard versus ManagedResource in this audit; this is a planning integration tension, not a proven runtime bug.

3. **Conditional integration wording (IDs 26/32/42).** D33 says URL stores full conditions without S37/D31/T1.3's temporal qualifier. S9 lists 404 while Direct card link S14 assigns GET/404 to MOS-1251 and isolated registry checks to route parameters. Explicit ownership bounds these statements; S46/D25 reject adjacent-feature completion as registry acceptance. Follow-up: distinguish current isolated checks from future card loading/404 and conditions-restoration integration. Retain every P14 deferral.

4. **Acceptance precision, not missing requirements.** S23/S37/S9 require query/bounds/server sorting/damaged-URL explanation/retry. T1.3 and Restore registry link S39–42 emphasize valid restoration; T1.2 lacks retry examples. Follow-up: add focused planned unit/component cases for malformed URL with explanation/no misleading partial selection, query/limit boundaries, default/descending server order, retry, and empty registry versus filtered zero. Source anchors J-A2…6. No browser tests or live validation requested by this audit.

5. **Wiki-only UI gaps remain unadjudicated.** IDs 44/46/47/51–54/56 trace to W2/W3.1/W3.3/W3.6 in the table. These are not explicit Jira deferrals; neither does their absence authorize implementation. Follow-up: obtain scope disposition for each and add requirement/task evidence only if retained. ID55's defaults require card-owner follow-up. W3.5's narrower copied-link description remains a disagreement against J-A5/S37/D33, not an internal defect to fix by dropping full search.

## Architecture / Key planning contract

D21 assigns API/DTO validation/query keys/types/normalized selection to public `entities/feedback`; pages/widgets compose registry. React Router owns routes (D23/29). MOS-1250 owns applied search/URL; MOS-1258 later integrates conditions (D31). MOS-1249 supplies shared contract/policy, MOS-1251 actual detail GET/404. S37 requires full restoration of `query, status/type_code, sort, limit/offset` and conditions after MOS-1258, not just wiki `q/status/type` copying.

**Start here:** `openspec/changes/mos-1250-feedback-registry/specs/feedback-registry/spec.md`, lines 7–42; compare its requirements and scenarios with T1.1–1.3 before proposing edits.

## Limitations / excluded scope

- No implementation readiness inferred from tasks, Jira Development status or D3's historical implementation statement. No backend contract correctness or source precedence adjudicated.
- Jira excludes comments/attachments/custom acceptance fields. Wiki is flattened prose; prototype attachment not inspected/executed. Initial extraction accidentally stopped at `4.` inside `3.4`; a subsequent targeted read recovered 3.4–3.6. Incidental adjacent card text returned by that read is excluded.
- API schema/docs and adjacent card/conditions/saved-filter/export plans not audited. Saved filters/export and draft/tab/question-order language in D21–35 is shared context, not new MOS-1250 obligations. No unrelated feature scope added.
- No tests/build/lint/network/MCP/generation/status updates/staging. Only this authorized report written. Independent final decision review remains separate; evidence was recomputed, not accepted from author summaries.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped all 56 REQ IDs to planning requirements/scenarios/tasks and independently decoded Jira/wiki locators; retained deferrals and documented unresolved follow-ups."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SPEC-MOS-1250.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python JSON extraction and numbered document inspection; wc -l for referenced documents","result":"passed","summary":"Verified MOS-1250 source identity/text, wiki sections 2–3, planning line numbers and file lengths. No executable validation run."}],
  "validationOutput": ["All 56 IDs represented, including deferred/wiki-only cases; entire registry change spec read."],
  "residualRisks": ["Selected Jira fields/flattened wiki omit attachment and comment evidence.","Endpoint consumption, main-policy integration and conditional cross-change acceptance need follow-up.","No implementation/backend readiness or source precedence established; wiki-only scope undecided."],
  "noStagedFiles": true,
  "diffSummary": "Authorized planning report only; no source/spec edits.",
  "reviewFindings": ["Planning traceability gaps and acceptance refinements documented; no runtime defect asserted."],
  "manualNotes": "Manual independent source-versus-plan comparison. No staging performed; pre-existing index not inspected. Tests and remote operations prohibited and not run."
}
```
