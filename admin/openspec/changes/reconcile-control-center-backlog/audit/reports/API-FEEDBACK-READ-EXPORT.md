# Code Context

## Integrity/review attribution

Independent reviewer verified local operations/prose and implementation joins but could not retrieve the single-line saved-r2 body through its reader. Parent subsequently parsed all three JSON files and independently verified both export operation objects equal after removing only security, and all ten transitively referenced schemas equal. This is parent-computed comparison, not reviewer certification or current-live evidence. Original reviewer limitation remains in R-FEEDBACK-REMAINING-EVIDENCE.md; no further model run needed.

## Result
API-FEEDBACK-READ-EXPORT only. **Contract/owning-plan no-op:** both survey CSV operations are published identically in saved r2 and current local contracts except approved security normalization. CRUD prose resolves several formerly unknown search/CSV semantics. Formal 422 versus business-envelope mismatch and export/read permission ambiguity remain real, already-planned integration checks—not new backlog or permission-policy decisions. Current plans already contain the previously accepted condition-pointer and metadata-label corrections.

## Files Retrieved — actual scope
Aliases: `A=openspec/changes/reconcile-control-center-backlog/audit`, `D=docs/api/contracts`, `P=openspec/changes` (expand literally).
- `A/work-items/G2-FEEDBACK-REMAINING-EVIDENCE.md` complete; only API lane executed.
- `A/reports/API-G2-MOS-1250-READS.md` lines 1–160: reused accepted search/lookup/metadata identity and closure; did not repeat its 24-schema census. Final attestation tail not read.
- `A/reports/REQ-G2-MOS-1258.md` lines 1–74; `A/reports/REQ-G2-MOS-1260.md` lines 1–117; `A/reports/SPEC-G2-MOS-1258.md` lines 1–72; `A/reports/SPEC-G2-MOS-1260.md` lines 1–90: accepted IDs and qualified plan dispositions. Combined numbered output truncated its beginning; needed 1258 opening and API report were separately retrieved. No original Jira/wiki re-extraction.
- `A/decisions.md` lines 1–19: D074–076, including integrated C9 correction.
- `A/sources/api-live/r2/metadata.json` lines 1–22, complete; `content.json` line 1 parsed selectively at operation/schema pointers below. Snapshot retrieved 2026-10-19T08:11:44.238Z; hash metadata-attributed, not recomputed. Not current-live/deployment evidence.
- `D/openapi.json`, `D/managed-resources.openapi.json`: JSON parsed only for two export operations, their ten transitive schemas, and three metadata/error schemas below; unrelated operations not inspected.
- `D/crud-api.md` lines 290–399, 530–649, 850–1021 (last range incidentally returned beginning of detail example; not audited). Scoped grep discovered relevant headings; no dialog/report export analysis.
- `D/README.md` lines 1–33; `D/managed-resources.md` lines 1–55: provenance, local normalization and limits.
- `P/mos-1258-feedback-conditions/specs/feedback-conditions/spec.md` lines 7–16 and `design.md` 45–59; `P/mos-1260-feedback-export/specs/feedback-export/spec.md` 7–14 and `design.md` 39–54; targeted export-owner grep additionally returned design 29/31 and tasks 4. Narrow current correction/risk checks, not another full plan audit.

## Key Code — exact JSON pointers (schema evidence, not application code)
Pointers apply to each of the three JSON documents above. Define `S(N)=/components/schemas/N`.
- **L** = `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys~1export/post`; `/operationId` = `export_fb_survey_api_control_api_v1_managed_resources_feedback_surveys_export_post`.
- **E** = `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys~1{entity_id}~1export/post`; `/operationId` = `export_detail_fb_survey_api_control_api_v1_managed_resources_feedback_surveys__entity_id__export_post`. `E/parameters/0`: required UUID path `entity_id`; prose `{id}` is the same route, not a missing operation.
- `L/requestBody/content/application~1json/schema` → `S(fb_surveyExportRequest)`; `E/requestBody/content/application~1json/schema` → `S(fb_surveyDetailExportRequest)`; both `/requestBody/required=true`.
- Both request schemas: `/required=["fields"]`, `/additionalProperties=false`; `/properties/fields` array minItems 1/maxItems 100, `/items/enum=[name,code,type_code,audience_type,status]`. **No uniqueItems**. Business uniqueness/order is prose, not this array schema.
- `S(fb_surveyExportRequest)/properties/search` → `S(fb_surveyListQuery)`; optional, non-null, no explicit default. Detail has no search property and rejects extras. Reuse API1250 query/sort/filter/condition bounds; formal pagination remains validated even in export.
- `L/responses/200/content/text~1csv/schema` and `E/responses/200/content/text~1csv/schema`: `{type:string,format:binary}`; description CSV file. Neither 200 declares headers. CSV is formally published—do not claim JSON-only success from generic managed-resources caution.
- Both `/responses/422/content/application~1json/schema` → `S(HTTPValidationError)`; `/properties/detail/items` → `S(ValidationError)` requiring `loc,msg,type`. `loc` is array of string/integer, **not a JSON Pointer string**. No declared 400/403/404 response or business-code variant here.
- `S(ManagedResourceMetadata)/properties/export_fields`: string-valued map; `/properties/export_max_rows`: integer default 10000, no bounds; neither is required. `/properties/condition_fields/additionalProperties` → `S(ManagedResourceConditionField)`, whose `/properties/operators/items/enum` is generic, including numeric operators; this does not override feedback-specific operator enum at `S(fb_surveyCondition)/properties/operator/enum`.
- `S(fb_surveyCondition)/properties/value/anyOf` permits broader values than operator-dependent business rules; no uniqueItems or field/operator cross-validation. `S(fb_surveyConditions)/properties/items` maxItems 50; empty allowed. Do not infer numeric feedback conditions.
- `S(ErrorItem)/properties/field` nullable string supports an envelope field structurally, but does not specify pointer grammar and is **not referenced by these declared export 422 responses**.

Comparison: both operation objects equal across all three after removing only `/security`; all ten export-reachable schemas equal, as are separately checked ManagedResourceMetadata, ManagedResourceConditionField, ErrorItem. Ten-schema closure comprises the two export requests, ListQuery, Conditions, Condition, FeedbackSurveySort, both ManagedResourceFilter schemas already named in API1250, HTTPValidationError, ValidationError. No search response/lookup DTO census repeated.
Local `L/security` and `E/security` are `[{"AdminToken":[],"AccessToken":[]}]` (AND); saved r2 has two separate alternatives (OR). Keep approved normalization (`D/README.md:7–9`, `D/managed-resources.md:55`), not new auth work.

## Requirements → semantic evidence / action
| Accepted IDs | Evidence and distinction | Disposition |
|---|---|---|
| 1258 C1 | CRUD 292–299,398–399 defines `data.surveys.condition_fields` authority; 618–649 gives seven fields, flat group ≤50. Metadata example 329–375 is explicitly shortened, not exhaustive per-field matrix. | Keep metadata-driven plan; actual complete compatibility matrix remains runtime input. |
| C2–C4 | CRUD 634–644: first six operators require 1–1000 string; empty operators omit/null; in/not_in 1–100 unique strings ≤1000; remove cleared condition; no trim. Case-sensitive eq/ne/in/not_in, insensitive substring/prefix/suffix; NULL/empty satisfy ne/not_contains for nonempty input and not_in; `%`, `_`, backslash literal. Inactive lookup codes allowed by 563. | Answers prior semantic unknowns; schema alone is insufficient. No client page-filter implementation authorized. |
| C5,C7 | CRUD 541–564,584–585: query substring in name/code/description/type_code; ordinary scalar exact, array OR, filters/query/group AND; absent/null/[] clears ordinary filter, unknown codes no match. Selection applies to list/total_items/export. 611–614 gives page formulas and frontend offset reset. | Keep shared registry search ownership. Query case/trim is still unspecified (do not extrapolate condition rules). |
| C6,C8,C10 | CRUD 645–646 resolves empty items as no restriction for either logic, clear conditions by omission/null. URL/draft/apply UX and tests are client requirements, not API guarantees. | Keep accepted plans; empty wire meaning is answered, general clear/apply interaction remains unselected. No tests run. |
| C9 | CRUD 961–975: 422 VALIDATION_ERROR; `/conditions/items/0/field`, `/operator`, or whole `/conditions/items/0`; export adds `/search`. | Current 1258 spec:15 already targets condition without input loss. Formal 422/envelope mismatch remains design:50 integration gate; no repeat correction. |
| 1260 R01–R05 | Binary success and fields schemas above; CRUD 889–895 and 934–940 establishes unique fields, order, metadata labels. | Current 1260 spec:9 already includes metadata-derived labels. No duplicate candidate. |
| R06–R08 | CRUD 889–891: full selection with selected sort; limit/offset validated but ignored for file; search omitted/{} means unrestricted, null invalid. Applied-versus-draft is client responsibility. | Keep; not a formal pagination contradiction. |
| R09–R11 | Detail fields-only schema; CRUD 934–943 one saved row, no search, ignores unsaved edits. New-card gate/dirty disclosure are UI requirements. | Keep existing plan. |
| R12–R17,R19 | CRUD 901–915: text/csv charset utf-8, Content-Disposition filename*, CORS exposure; BOM, semicolon, quoted values, Russian headings, null empty, apostrophe before potential formula; empty selection header-only. Detail filename adds ID (945–947). | Header/BOM/escaping guarantees are business prose, not formal response headers. Preserve server bytes; actual CORS/bytes require release evidence. |
| R18,R20 | Metadata default 10000; CRUD 917–920,977–993: 422 EXPORT_LIMIT_EXCEEDED/no file; envelope errors[].details.max_rows; fresh query respects rights/soft-delete (post-list changes may appear). | Keep row-limit plan; no malformed-metadata fallback invented. |
| R21–R30,R38–R42 | CRUD supplies JSON errors, not browser cancellation/owner isolation/Blob lifecycle or full malformed-response policy. Formal 422 differs from business envelope. | Already client verification and integration obligations in accepted SPEC1260; not missing endpoints. No execution evidence. |
| R24–R26 specifically | CRUD 956–960: absent/deleted detail 404 NOT_FOUND, invalid UUID 400 INVALID_ARGUMENT, bad/duplicate/empty fields 422 VALIDATION_ERROR. Formal operations publish only 200/422, UUID format in parameter. | Documented formal/prose error mismatch and missing status descriptions; do not assert actual backend behavior or rewrite schemas. |
| R31–R32 | CRUD 959 says detail rights same as read, whereas separate export permission is recorded in accepted plan and README/prose context. | Existing 1260 design:45 explicitly retains read+export UI policy and server-permission release question. No new choice/enforcement in mocks. |
| R33–R37 | CRUD 921 and 941 excludes results/responses and nested questions/options/rules; detail/list share CSV format. | Keep stage-one boundary and no borrowed dialog headers. |

Additional previously unknown CSV facts: CRUD 897–899 specifies lookup display_name including inactive values, fallback code, audience label; 889 specifies requested row sorting. Formula-trigger detection set, tie-breaking, filename validation algorithm, actual metadata payload and backend behavior remain unspecified/unverified; frontend must not invent CSV reconstruction.

## Architecture / Start Here
Read `docs/api/contracts/crud-api.md:889–993` alongside L/E above and `openspec/changes/mos-1260-feedback-export/design.md:44–45,54`. Shared entity/search supplies applied selection; export sends it server-side without page truncation; condition editing and download/session UX remain separate owners. Formal schema, backend prose, and approved local security normalization are distinct evidence layers. No further owning-plan change justified; retain existing release checks for errors/permissions/CORS/server semantics. Missing formal headers/status variants are documentation gaps, not proof absent functionality. No material missing input prevented this bounded conclusion; no global G2/feature closure.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Compared both export operations and transitive dependencies in three saved/local contracts; mapped C1–C10 and R01–R42 to schema/prose/client boundaries and verified prior corrections are present."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/28516eb5-13bf-4fa0-bc54-6a760de63be1/api-read-export.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local Python JSON parsing/comparison of two export operations, referenced schemas and selected metadata/error schemas","result":"passed","summary":"Both operations equal excluding approved security; inspected schemas equal across r2/aggregate/split."}],
  "validationOutput": ["Manual requirement mapping and current pointer/label correction checks completed; no tests, network, source execution, code audit or project edits."],
  "residualRisks": ["Formal 422 shape differs from business envelope; headers and 400/403/404 are not formally declared.","Runtime semantics, metadata matrix, permission sufficiency and CORS remain existing release checks; snapshot freshness not verified."],
  "diffSummary": "External findings report only; repository untouched.",
  "reviewFindings": ["No new mandatory owning-plan correction; retain existing error/permission integration questions."],
  "manualNotes": "Accepted API1250 facts reused; only export dependency closure and missing semantics inspected. Hashes metadata-attributed. No staging actions or git-index inspection; no claim about index state. Parent review pending."
}
```
