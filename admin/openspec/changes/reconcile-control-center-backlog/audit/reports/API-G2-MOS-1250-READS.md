# Code Context

## API-G2-MOS-1250-READS — independent analytical evidence

**Result:** All three requested read operations resolve in saved live r2 and both local contracts. Lookup is the instantiated `/catalogs/lookups/{section}` operation with `section=feedback`, not a missing literal operation or a substitute. The three operations differ live/local only in the already approved security normalization; all 24 transitively reachable schemas are structurally equal. Recommend contract no-op and narrow planning traceability clarification, not acceptance, publication, feature completion or runtime readiness.

Scope: POST search, GET feedback lookup, GET feedback metadata only. Reachable nested DTOs are described as wire dependencies, not expanded feature scope. No mutation operations, export workflows, conditions editor, new filters, code inspection, external collection, tests or nested delegation. HEAD verified `bc0d9800f25a90989b9c73c76f91996f8300f1d3`.

## Files Retrieved

Repository-relative aliases: `C=openspec/changes/reconcile-control-center-backlog`, `A=C/audit`, `D=docs/api/contracts`. These aliases expand exact paths below; JSON pointers are authoritative where JSON was selectively parsed rather than read as lines.

| Input | Retrieved range / purpose | SHA-256 of complete input bytes |
|---|---|---|
| `C/proposal.md` | 1–30; authority | `1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879` |
| `C/design.md` | 1–133; evidence and independent review gates | `632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828` |
| `C/tasks.md` | 1–45; G2 distinct from acceptance/publication | `a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83` |
| `C/specs/control-center-backlog-reconciliation/spec.md` | 1–108; bounded-source contract | `a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36` |
| `A/work-items/API-G2-MOS-1250-READS.md` | 1–11; assignment | `d38262f7c5db6c9123167237eda8fb0e8393c1cdd7d445472291689e07c146ed` |
| `A/decisions.md` | 3–13, 427–436; D-060/D-002 | `25bf2e9f347f65096f6337d59ca4300d2c48215261f386749d7297c99055acca` |
| `A/reviews/R-MOS-1250.md` | 1–97; reviewer corrections | `8270a6c6e150312051a148ed588e96e178b4e7c6cf613eaa7e018d80d7643aa8` |
| `A/reports/REQ-MOS-1250.md` | 1–122; stable requirement IDs | `32059c6375ded180a58e71fc02af44f541bd455f241f41924826d702bd6ed020` |
| `A/sources/jira-feedback/r1/content.json` | 35–39, `/items/3/description`; MOS-1250 only | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| `A/sources/jira-feedback/r1/metadata.json` | 1–11; provenance | `5c8df75fde70960ff15b33d6e6d3cc6c57b9d06daeee383076c753101f94fa70` |
| `A/sources/api-live/r2/content.json` | line 1; three operation subtrees and 24-schema closure below | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `A/sources/api-live/r2/metadata.json` | 1–22; dated snapshot provenance | `444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba` |
| `D/openapi.json` | selectively parsed pointers below; 22,075-line file | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `D/managed-resources.openapi.json` | same pointers; 10,447-line file | `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf` |
| `D/managed-resources.md` | 1–55; explanatory source, security and deployment boundaries | `529780f69c4451793d8a2af3cfb89cda9cc9c908d9a48c207de5ff21fb33435d` |
| `D/README.md` | 1–33; approved normalization and snapshot identity | `cb452cf8caf22245c7a62af5f16880e7b5c1b5aa6d591c5aa3e88261632929b3` |

All three launch-pinned contract hashes matched. Jira content hash also matches its metadata. Live metadata attributes capture to parent documentation GET on 2026-10-19T08:11:44.238Z, OpenAPI 3.1.0/service 0.1.0, 96 paths/130 operations/388 schemas. Local README describes the 2026-10-15 snapshot, 94/128/380; these whole-document counts do not imply any change in this lane. No external freshness check performed. D-060's incomplete source accounting remains qualified; no material missing explanation needed to establish the bounded wire comparison was identified.

## Key Code — operation identity and exact pointers

All pointers below apply independently to live r2, local aggregate and local split. `S(name)` means JSON pointer `/components/schemas/name`; `S(name)/properties/field` identifies each field described below. This is schema evidence, not executable application code.

| Method and concrete request | Operation JSON pointer | operationId | Contract |
|---|---|---|---|
| POST `/api/control/api/v1/managed-resources/feedback/surveys/search` | `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys~1search/post` | `list_fb_survey_api_control_api_v1_managed_resources_feedback_surveys_search_post` | Required JSON body `S(fb_surveyListQuery)`; 200 JSON search envelope; 422 JSON validation error |
| GET `/api/control/api/v1/managed-resources/catalogs/lookups/feedback` | `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get` | `get_section_catalog_lookups_api_control_api_v1_managed_resources_catalogs_lookups__section__get` | Required path parameter `section`, includes `feedback`; 200 JSON lookup envelope; 422 JSON validation error |
| GET `/api/control/api/v1/managed-resources/feedback/metadata` | `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1metadata/get` | `metadata_feedback_api_control_api_v1_managed_resources_feedback_metadata_get` | 200 JSON metadata envelope only; no body or parameters declared |

For each operation the success schema locator is `<operation>/responses/200/content/application~1json/schema`; request schema is `<search>/requestBody/content/application~1json/schema`; lookup parameter is `<lookup>/parameters/0`. The concrete lookup path has no literal entry, correctly resolved by the templated route. `S(CatalogLookupSectionName)` is string enum `catalogs, skills, feedback, knowledge-base, ab-testing, api, response-templates`.

### Search request

`S(fb_surveyListQuery)` is an object, `additionalProperties:false`, with **no required property list** (required body does not make fields mandatory). All seven fields:

| Field | Wire shape / constraints / default |
|---|---|
| query | Optional string length 2–200 or null; no explicit default. Empty/one-character strings fail the string bounds; omitted and null are distinct allowed representations. No trimming, debounce or matching-field semantics specified. |
| sort | Optional non-null `S(FeedbackSurveySort)` string enum `name,-name,type_code,-type_code,status,-status,updated_at,-updated_at`; default `-updated_at`. |
| limit | Optional non-null integer 1–100 inclusive; default 20. |
| offset | Optional non-null integer ≥0; default 0; no maximum. |
| status | Optional null or string length 1–32 or array of 0–100 strings each length 1–32. No status enum or default. |
| type_code | Optional null or string length 1–50 or array of 0–100 strings each length 1–50. No type enum or default. |
| conditions | Optional null or `S(fb_surveyConditions)`; presence is not approval to implement MOS-1258 now. |

Exact filter schema names (each is an `S(...)` pointer):
- `ManagedResourceFilter_Annotated_str__FieldInfo_annotation_NoneType__required_True__metadata__MinLen_min_length_1___MaxLen_max_length_32_____`
- `ManagedResourceFilter_Annotated_str__FieldInfo_annotation_NoneType__required_True__metadata__MinLen_min_length_1___MaxLen_max_length_50_____`

Arrays have no `uniqueItems`; empty arrays are permitted, but their business meaning and OR-within/AND-between behavior are not defined by the schema. Do not infer related-label search or audience sorting from these shapes.

Closure-only conditions: `S(fb_surveyConditions)` forbids extra fields; optional non-null `logic` enum and/or defaults and; optional non-null `items` array ≤50, no explicit default/minimum. Items reference `S(fb_surveyCondition)`, which forbids extra fields, requires `field,operator`, and has optional nullable `value`. Field length 1–100, enum code/name/description/type_code/status/audience_type/owner; operator enum contains/not_contains/eq/ne/starts_with/ends_with/is_empty/is_not_empty/in/not_in. Value permits string length 1–1000, array 1–100 such strings, integer, number, two-element numeric array, or null. Schema unions do not establish operator/value compatibility or grant numeric operators to these string fields. No editor/expanded-filter recommendation follows.

### Search response and nested reachable DTOs

`S(TsamResponseSchema_PaginatedResponseSchema_list_FeedbackSurveyResponse___)` requires non-null `code,data,message`; optional non-null `errors` array. `code` references `S(ResponseCode)` (unrestricted string, no success enum); message is string. Data references `S(PaginatedResponseSchema_list_FeedbackSurveyResponse__)`, requiring `items` (non-null array of `FeedbackSurveyResponse`) and `pagination` (`PaginationDto`). No item-array minimum/maximum is declared.

`S(PaginationDto)` requires five non-null integers `limit,offset,current_page,total_items,total_pages`; no bounds/defaults appear in the **response** schema. It supplies counters but does not promise page numbering convention or separate unfiltered-registry totals.

`S(FeedbackSurveyResponse)` fields:
- Required non-null: `id` UUID string; `created_at,updated_at` date-time strings; `name` string 1–255; `code` string ≤100, pattern `^[a-z][a-z0-9_]*$`; `type_code` string 1–50; `questions` array of `FeedbackQuestionResponse`; `display_rules` object `FeedbackDisplayRulesResponse`.
- Optional nullable: `description` string; `owner` string ≤200; `responsible_user_id` string (no UUID format declared); `active_since` date string. No explicit defaults.
- Optional non-null: `status` string 1–32 default draft; `audience_type` string 1–32 default all; `tags,segments,operator_groups` strings ≤16000 default empty string; `surface_ids` array ≤100 UUID strings, no explicit default. No status/audience enum or expansion of these strings into arrays is justified.

Full nested closure, not a card/editing assignment:
- `S(FeedbackQuestionResponse)` requires non-null id UUID, title string 1–500, type_code string 1–50, options array of `FeedbackOptionResponse`; optional non-null boolean `required` defaults false. No response questions/options array cap.
- `S(FeedbackOptionResponse)` requires non-null id UUID and text string 1–255.
- `S(FeedbackDisplayRulesResponse)` has no required fields. Optional non-null `trigger_type` string 1–50 defaults manual. Other fields explicitly allow null: integer ≥0 `min_messages,min_duration_sec,delay_show_sec,pause_after_last_sec,cooldown_sec`; integer ≥1 `max_per_session,max_per_day,max_per_user`; booleans `skip_if_rated` default true, `quiet_hours_enabled` default false, `exclusive_show` default false; time strings `quiet_from,quiet_to`; strings 1–32 `dialog_type,dialog_result` default any; integer `priority` default 0 without bounds. Unlisted defaults are absent. Null is not equivalent to default.

Response objects above do not declare `additionalProperties:false`; do not copy request strictness onto responses. Likewise required questions/display_rules on the list response do not require a registry to render or edit them.

### Lookup response

`S(TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___)` requires non-null code/data/message and optionally errors as above. Data is an arbitrary-key object whose values are arrays of `S(ManagedResourceCatalogItem)`; no required dictionary keys, minimum size or actual values are supplied.

Catalog item requires non-null `code` string 1–64 and `display_name` string 1–150. Optional nullable description string and created_at/updated_at date-time strings; optional non-null sort_order integer 0–32767 default 0, is_active boolean default true, is_default boolean default false. No extra-field prohibition. There is no promise that inactive values are absent, that every survey code resolves, or that a fixed number of survey types exists. Lookup supports labels, but fallback presentation and keyboard behavior remain UI requirements.

### Metadata response

`S(TsamResponseSchema_dict_str__ManagedResourceMetadata__)` requires non-null code/data/message, optional errors. Data is an arbitrary-key object of `S(ManagedResourceMetadata)`; the schema does not mandate a particular feedback resource key or actual binding contents.

`ManagedResourceMetadata` requires non-null `catalog_bindings` (arbitrary-key map to `ManagedResourceCatalogBindingMetadata`). Optional non-null `condition_fields` map to `ManagedResourceConditionField`, `export_fields` string-valued map, `export_max_rows` integer default 10000 with no bounds. No explicit defaults for maps. Their existence is wire evidence only, not required registry consumption or authority to implement conditions/export.

`S(ManagedResourceCatalogBindingMetadata)` requires non-null catalog string, value_field enum code/id, multiple boolean. `S(ManagedResourceConditionField)` requires non-null label string; optional non-null type enum string/integer/number default string; optional non-null operators array enum contains/not_contains/eq/ne/starts_with/ends_with/is_empty/is_not_empty/in/not_in/gt/gte/lt/lte/between, no size bounds/default. These metadata objects have no explicit extra-field prohibition. Generic metadata operator possibilities do not override feedback condition-specific enums.

Endpoint presence and schema inspection satisfy only API traceability for REQ-1250-6. Jira names GET metadata, but neither that sentence nor schema existence defines which metadata fields the basic registry must consume. Preserve the read dependency; identify registry-relevant verification/use ownership in planning without inventing a metadata-driven UI.

### Errors and security

`S(ErrorItem)` requires non-null message string; optional nullable field/code strings and details object with arbitrary properties. All three 200 envelopes have optional non-null errors arrays; no business code enumeration or HTTP mapping is specified. Search and lookup 422 reference `S(HTTPValidationError)` with optional non-null detail array of `S(ValidationError)`. Each ValidationError requires loc array of string-or-integer, msg string, type string; optional input is unconstrained (can be null), ctx is object. No defaults or array bounds; no extra-field prohibition. Metadata has no declared 422. None of these three operations declares 401/403/404/5xx or retry policy: absence in these snapshots is **bounded documentation absence**, not proof those statuses cannot occur.

`/components/securitySchemes/AdminToken` and `/components/securitySchemes/AccessToken` are identical in the three documents: header apiKey `X-Admin-Token` and `X-Access-Token`, descriptions require both raw tokens. At each `<operation>/security`, live has `[{"AdminToken":[]},{"AccessToken":[]}]` (OpenAPI OR); both locals have `[{"AdminToken":[],"AccessToken":[]}]` (AND). Preserve the approved local AND normalization documented in `D/README.md:7–9` and `D/managed-resources.md:5,55`. This is not a new auth finding or authorization to revert local contracts.

REQ-1250-35 concerns UI policy, not API-key security schemes. D-002 and R-MOS-1250 explicitly retain the pending MOS-1249 extension mapping registry/lookup/metadata reads to `TSAM.ManagedResource:read` using existing exact action/resource/wildcard semantics. No new wildcard-versus-ManagedResource decision or main-spec-sync blocker is raised. Backend request authorization remains distinct from UI visibility; no permission enforcement was exercised.

## Architecture and requirement mapping

Wire flow: required POST JSON search → paginated survey records/counters; GET section lookup → code/display-name dictionaries; GET metadata → catalog bindings and resource descriptors. Registry basic query, sort and paging can use the published schema; label joining and safe unknown-code display are client responsibilities. Shared credential handling and pending UI mapping are separate from these response DTOs. No implementation was examined.

| REQ-1250 ID | API relationship / remaining boundary |
|---|---|
| 4 | Exact POST exists; required request body and 200/422 shapes above. |
| 5 | GET template with section=feedback resolves the named concrete lookup. |
| 6 | Exact metadata GET exists; consumption requirements are not inferred from generic fields. |
| 7 | Survey name/code/type_code/audience_type/status exist; segments/surface_ids also returned. Column composition and optional-field handling are UI decisions, not server guarantees of populated labels. |
| 8 | Lookup code/display_name and metadata bindings provide structural support; actual dictionary keys/content are not fixed here. |
| 9 | Unknown-code fallback is UI behavior; contract does not ensure every code has a lookup match. |
| 10 | Keyboard opening is UI-only; API id is UUID, no accessibility claim follows. |
| 11 | Query string bounds match 2–200. Matching fields/case/trim semantics unknown. |
| 12 | status scalar-or-array supports multiselect transport; 0–100 array and item bounds above. UI selection/combination semantics not certified. |
| 13 | type_code scalar-or-array supports multiselect transport with distinct 50-character bound. |
| 14 | query omission permitted; Jira explicitly requires omit on clear, although wire also permits null. |
| 15 | One-character string invalid by schema; suppressing the request is UI behavior, not established by 422 presence. |
| 16 | Applied-search presentation is UI-only. |
| 17 | All eight required sort variants exactly present. |
| 18 | Request default is -updated_at. |
| 19 | Server sort input exists; absence of page-local substitution requires implementation evidence, not schema inspection. |
| 20 | Request limit 1–100/default20, offset ≥0/default0; response includes limit/offset and page counters. |
| 21 | API pagination provides total_items/total_pages/current_page; no separate global unfiltered count asserted. |
| 22 | Reset offset on changed selection is UI logic, not automatic schema behavior. |
| 23 | Late-response protection is client concurrency behavior; no version/correlation guarantee declared by these operations. |
| 35 | Existing UI-policy plus pending MOS-1249 mapping retained per D-002; raw-header security is separate. |

REQ-1250-24 onward other than 35, deferred filter/editor/export work and adjacent write/card scenarios are not expanded by this report.

## Comparison, corrections and unknowns

Inspection traversed all `$ref` links from exactly three operation objects: **24 distinct schemas**, all present and structurally equal live/local aggregate/local split. Removing only operation `security` made all three operation objects structurally equal; security schemes themselves match. Thus there is no scoped DTO, requiredness, nullable/default/bounds/error/operationId drift to correct. This comparison does not certify unrelated paths or entire files as equal.

Proposed parent dispositions (not applied or accepted here):
1. **Keep/no-op contracts:** preserve current local aggregate/split and security normalization. No API absence blocker for these reads.
2. **Narrow planning clarification:** use the concrete lookup URL with its `{section}=feedback` identity; explicitly identify POST/GET methods and link MOS-1249 dependency, consistent with R-MOS-1250 finding 2. Explain registry-relevant metadata verification ownership without requiring all metadata fields to drive UI.
3. **Keep boundaries:** one-character suppression, omission on clear, server-sort use, offset reset, races, unknown-code fallback and keyboard access need UI evidence. Contract existence alone cannot close these tasks. Conditions/export data in reachable schemas remains future/out-of-scope consumption.
4. **Keep pending mapping:** no new security/policy blocker, no main-spec rewrite or auth-model choice. Historical API-OPS-001/API-SCHEMA-001/R-API-001/D022–023 are not reused as current acceptance.

Residual unknowns: exact query matching and filter combination semantics; actual lookup keys/values and metadata resource bindings; successful runtime availability, authorization, CORS, deployment, business error statuses, retry and counter behavior. These are not silently converted into unsupported substitute operations or current contract defects. No product precedence was selected; no material input/approval gap prevented this bounded analysis. Any later requirement to prescribe unprovided semantics must reopen a narrow source question through parent under D-060.

## Start Here

Start with the three operation pointers in `docs/api/contracts/managed-resources.openapi.json` and the `fb_surveyListQuery`/three response-envelope schemas, alongside `A/reviews/R-MOS-1250.md` finding 2 and D-002. The likely follow-up is only reviewed planning traceability, not code or contract edits. Source versions must be rechecked before any publication.

## Inspection evidence and limitations

Local read/find/grep plus non-interactive Python JSON parsing/SHA-256 and `git rev-parse HEAD` only. Parsed operation objects, traversed all referenced schemas, compared structural equality, and checked the three launch hashes. No app code or test source inspected. No network/browser/business calls, credentials, tests/build/lint/typecheck/typegen/format execution, staging or project edits. Only this authorized report written. Git index/dirty state not inspected; no empty-index claim is made. Jira is selected-field extraction (comments/attachments/custom acceptance fields absent); live is saved documentation, not observed backend behavior. Governing explanatory Markdown was read but linked documents were not fetched or implicitly treated as inspected.

```acceptance-report
{
  "criteriaSatisfied": [
    {"id":"criterion-1","status":"satisfied","evidence":"Resolved all three bounded reads, recorded exact operation/schema pointers and all 24 reachable schemas, mapped REQ-1250 IDs 4–23/35, verified pinned hashes and scoped live/local equality apart from approved security normalization; stated residual unknowns."}
  ],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/API-G2-MOS-1250-READS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read/find/grep and Python JSON reference traversal, structural comparison, SHA-256 inspection","result":"passed","summary":"Three launch hashes matched; all 24 reachable schemas equal across live/aggregate/split; all three operations equal after excluding security only."},
    {"command":"git rev-parse HEAD","result":"passed","summary":"bc0d9800f25a90989b9c73c76f91996f8300f1d3 matches assignment."},
    {"command":"Tests, build, typecheck, lint, format and API generation/check","result":"not-run","summary":"Prohibited/unnecessary for this local analytical lane; no runtime/API edits."}
  ],
  "validationOutput": ["Lookup resolves via required section=feedback path parameter, not a missing endpoint.","No scoped DTO drift; approved local AND security differs from live OR.","Contract presence does not establish runtime acceptance or UI requirement completion."],
  "residualRisks": ["Saved snapshots do not establish external freshness, deployment or backend semantics.","Actual lookup keys/values, metadata bindings, query matching/filter combination and business error behavior are not fixed by inspected schemas.","UI behavior and permissions integration were not inspected or executed; selected Jira fields omit comments/attachments/custom acceptance fields."],
  "noStagedFiles": false,
  "diffSummary": "Only designated analytical report written; no project/source/contract/planning changes applied.",
  "reviewFindings": ["No scoped contract blocker; preserve security normalization and pending ManagedResource mapping.","Recommend narrow method/lookup-template/metadata-ownership traceability clarification, subject to independent review."],
  "manualNotes": "Analytical lane completion only, not independent acceptance/publication. noStagedFiles=false records uninspected index state, not observed staged files. All cited hashes cover complete saved input bytes; JSON content inspection was scoped to named operations and transitive dependencies."
}
```
