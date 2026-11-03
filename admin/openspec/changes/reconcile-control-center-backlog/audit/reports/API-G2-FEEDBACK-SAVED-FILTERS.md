# Code Context

## Result

**API-G2-FEEDBACK-SAVED-FILTERS only.** The inspected saved r2 and both local contracts publish **PUT, not PATCH**, for updating a managed saved filter. CRUD §9 expressly specifies **partial top-level update but complete replacement of a supplied `search`**: omitted name/search survive; omitted values inside supplied search receive defaults, not previous values. This is not whole-resource replacement. MOS-1249 already records published PUT; this audit supplies documentary verification, not new approval or runtime evidence. Jira PATCH remains a source discrepancy for parent disposition after independent review. No method-bearing edits, external reconciliation or additional product gate are authorized.

Parent was consulted on this material boundary and confirmed the above disposition: preserve Jira discrepancy, do not obscure the known published method, and do not invent an approval gate merely to retain already-planned PUT.

## Files Retrieved

Literal bases: `C = openspec/changes/reconcile-control-center-backlog`; `A = openspec/changes/reconcile-control-center-backlog/audit`; `D = docs/api/contracts`; `F = openspec/changes/mos-1249-feedback-api`. These expand all abbreviated paths below.

1. `A/work-items/G2-FEEDBACK-MUTATION-CONTRACTS.md` (lines 1–21), complete common contract and assigned unit; other unit visible, not executed.
2. `C/proposal.md` (1–30), `C/design.md` (1–133), `C/tasks.md` (1–45), `C/specs/control-center-backlog-reconciliation/spec.md` (1–108), complete governing documents. Truncated combined output was supplemented with the omitted proposal/design beginning.
3. `A/decisions.md` (1–17), D065 and adjacent D064 only.
4. `A/reports/REQ-G2-MOS-1259.md` (1–113), `A/reports/SPEC-G2-MOS-1259.md` (1–121), `A/reviews/R-REQ-G2-MOS-1259.md` (1–68), `A/reviews/R-SPEC-G2-MOS-1259.md` (1–82), complete including corrected F1. Initial combined output omitted the REQ beginning, subsequently read separately. Requirements are joined to accepted extraction, not newly re-extracted Jira/wiki.
5. `F/proposal.md` (1–32), `F/design.md` (1–81), `F/specs/feedback-api/spec.md` (1–38), complete API-owner documents; `openspec/changes/mos-1259-feedback-saved-filters/specs/feedback-saved-filters/spec.md` (1–28), complete narrowly relevant owner spec.
6. `D/README.md` (1–33), `D/managed-resources.md` (1–55), complete. Explicitly linked `D/crud-api.md` only lines 58–94, 415–428, 729–863, 1199–1220, 1282–1296; heading/keyword locator scan elsewhere was discovery, not a whole-document audit.
7. `A/sources/api-live/r2/metadata.json` (1–22), complete. JSON content semantic read set: **both complete assigned path items, all 15 transitive schema objects listed below, and both security scheme objects** in r2. Parsed corresponding local objects and compared each structurally against the fully read r2 objects; only operation security differs. No registry-read census or schema reuse from API-G2-MOS-1250-READS needed: no typed resource-search schema is reachable from these saved-filter objects.
8. `D/crud-api-2026-10-15.raw` was hashed only to verify the linked raw identity, not semantically read; evidence below cites the actual local Markdown at its own hash, not raw contents.

## Provenance and hashes

SHA-256 recomputed over complete file bytes (hashing is not semantic reading):

| File | SHA-256 |
|---|---|
| `A/sources/api-live/r2/content.json` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `A/sources/api-live/r2/metadata.json` | `444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba` |
| `D/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `D/managed-resources.openapi.json` | `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf` |
| `D/crud-api.md` | `4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058` |
| `D/crud-api-2026-10-15.raw` | `91c8dc68fc1b602a64428d1d6f1d9c44a0e6a89eced226e4773853badf13954a` |
| `A/reports/REQ-G2-MOS-1259.md` | `b928122009f79f48b4789fadcd476bbd1a8bdf669fc438b4cceacd7b3197bd25` |
| `A/reports/SPEC-G2-MOS-1259.md` | `cdbde326a62a7996ed5adc07faaab46a7587ea81dde685425eec0955f594e62a` |
| `A/reviews/R-REQ-G2-MOS-1259.md` | `b0287c540b7222d1860f90a72e396960f645d184a12a3f82e8b6cc76d01bbbc2` |
| `A/reviews/R-SPEC-G2-MOS-1259.md` | `c5abce85f35cc51b2c75c60c70b37fc10f8d1749f4aedd573de1d10cc5eb1538` |
| `F/design.md` | `0b15bcebfea15e35aca35a90c835a00efd892bb9a962fc16401892ca6017d91d` |

All three expected contract hashes match. r2 metadata records retrieval `2026-10-19T08:11:44.238Z`, URL `https://nchat-a-tech.mos.ru/api/control/openapi.json`, discovered from saved Swagger documentation, full-decoded-response-text, 420099 bytes. This is retained documentation, **not current live freshness or deployment confirmation**. Metadata-wide counts were not independently recensused. Corrected SPEC hash differs from the original author hash quoted in its retained REVISE review; D065 explicitly records parent correction without fresh independent ACCEPT.

## Key Code — exact operation pointers

Pointer aliases (literal JSON Pointer prefix substitution, identical in all three JSON files):

- `P = /paths/~1api~1control~1api~1v1~1managed-resources~1saved-filters`
- `I = /paths/~1api~1control~1api~1v1~1managed-resources~1saved-filters~1{filter_id}`
- `S = /components/schemas/`
- Media schema suffix `J = /content/application~1json/schema`.

| Exact operation pointer | Request/parameters | Declared responses |
|---|---|---|
| `P/post` | `/requestBody/required=true`; `/requestBody` + J → `ManagedResourceSavedFilterCreate` | `/responses/201` + J → `TsamResponseSchema_EntityCreatedResponse_`; 422 → `HTTPValidationError` |
| `P/get` | `/parameters/0` limit integer 1–100 default20; `/parameters/1` offset integer >=0 default0; `/parameters/2` resource optional string length1–200 or null (`schema/anyOf`) | 200 → `TsamResponseSchema_PaginatedResponseSchema_list_SavedFilterResponse___`; 422 → `HTTPValidationError` |
| `I/get` | `/parameters/0` required path filter_id string UUID | 200 → `tsam__assistant_management__shared__endpoints__schemas__TsamResponseSchema_SavedFilterResponse___2`; 422 → `HTTPValidationError` |
| `I/put` | same path parameter; required JSON body → `SavedFilterPatch` | 200 → same detail envelope; 422 → `HTTPValidationError` |
| `I/delete` | same path parameter; no request body | 200 → `TsamResponseSchema_ManagedResourceDeletedResponse_`; 422 → `HTTPValidationError` |

Complete path-item key inspection yields only post/get at P and get/put/delete at I. **No `I/patch` exists.** `I/put/summary` is `Patch Saved Filter`; `/operationId` is `patch_saved_filter_api_control_api_v1_managed_resources_saved_filters__filter_id__put`. These names do not define the HTTP method. No alias, idempotency header, optimistic lock, expected_version or alternate update operation is declared in the inspected paths.

## Complete reachable schema constraints

Each row below is the full object at exact pointer `S` + the schema name. Child fields are `/properties/<field>`; required lists are `/required`; unions are `/anyOf`. No allOf/oneOf or external refs occur in this closure. Except where explicitly marked false, object `additionalProperties` is **unspecified**, not implicitly forbidden. No unlisted range/count/uniqueness/default restriction is inferred.

| Schema name (exact) | Constraints and refs |
|---|---|
| `ManagedResourceSavedFilterCreate` | object, additionalProperties=false, required resource/name/search. resource nonnull string enum feedback-surveys/catalogs/knowledge-base-entries/ab-experiments/api-endpoints/response-templates. name nonnull string minLength1 maxLength150 pattern `\\S` (JSON string encoding; regex means a non-whitespace character). search nonnull object additionalProperties=true, no nested properties/ref/required/minProperties. |
| `SavedFilterPatch` | object, additionalProperties=false, no required or minProperties. name anyOf constrained string (1–150, non-whitespace pattern) or null; search anyOf object additionalProperties=true or null. resource/user_id/id/date fields absent and thus forbidden as extra input. `{}`, null name and null search are formally admitted; null whole body is not. |
| `tsam__assistant_management__managed_resources__endpoints__http__schemas__SavedFilterResponse` | object additionalProperties=false; all seven fields required, nonnull: id UUID string; created_at/updated_at date-time strings; resource/user_id/name plain strings without input enum/name constraints; search object additionalProperties=true. No schema version or migration field. |
| `EntityCreatedResponse` | object, required id string UUID. |
| `ManagedResourceDeletedResponse` | object, required id string UUID. |
| `PaginatedResponseSchema_list_SavedFilterResponse__` | object, required items array of qualified SavedFilterResponse and pagination ref PaginationDto; no min/max item count. |
| `PaginationDto` | object, required limit,offset,current_page,total_items,total_pages; all integers with no declared bounds. Do not project request bounds onto response schema. |
| `TsamResponseSchema_EntityCreatedResponse_` | object required code/data/message; code ref ResponseCode; data ref EntityCreatedResponse; message string; optional nonnull errors array ref ErrorItem. |
| `TsamResponseSchema_ManagedResourceDeletedResponse_` | same envelope, data ref ManagedResourceDeletedResponse. |
| `TsamResponseSchema_PaginatedResponseSchema_list_SavedFilterResponse___` | same envelope, data ref PaginatedResponseSchema_list_SavedFilterResponse__. |
| `tsam__assistant_management__shared__endpoints__schemas__TsamResponseSchema_SavedFilterResponse___2` | same envelope, data ref qualified SavedFilterResponse. |
| `ResponseCode` | string only; no SUCCESS/error enum. |
| `ErrorItem` | object, required message string; optional field and code each string-or-null; optional details anyOf object additionalProperties=true or null. JSON-Pointer syntax is not schema-enforced. |
| `HTTPValidationError` | object; optional detail nonnull array ref ValidationError; no required list. |
| `ValidationError` | object, required loc array of string-or-integer union, msg string, type string; optional input unconstrained schema, ctx object. No numeric bound, array-count or loc syntax restriction. |

**Full-search limitation:** saved search is deliberately opaque at `S/ManagedResourceSavedFilterCreate/properties/search`, `S/SavedFilterPatch/properties/search/anyOf/0`, and qualified response `/properties/search`. No reference to Feedback search DTO exists here. Thus this unit cannot claim query/filter/conditions/sort/limit/offset validation is enforced by these JSON schemas, or reuse unrelated registry-read constraints as if reachable. CRUD supplies the resource validation semantics; typed resource-search recensus is outside this unit.

## Local versus r2 comparison and security boundary

All 15 schema objects are structurally equal between r2, aggregate and split, including every union, required member and additionalProperties clause. All five operation objects differ from r2 **only at `/security`**; path methods, parameters, bodies, responses, extensions and operationIds otherwise match. Aggregate and split have identical assigned paths and reachable schemas.

At each of the five exact operation pointers + `/security`, r2 has `[{"AdminToken":[]},{"AccessToken":[]}]` (OR), locals have `[{"AdminToken":[],"AccessToken":[]}]` (AND). `/components/securitySchemes/AdminToken` and `/components/securitySchemes/AccessToken` are identical across files: apiKey, header, names X-Admin-Token/X-Access-Token; descriptions explicitly request both raw tokens. README lines7–9 and F/design:21 identify the approved normalization separately. This is not a method/schema discrepancy and is not permission to weaken local security. Operation OpenAPI declares no TSAM permission extension; action permissions and global/owner scopes come from CRUD/plan.

## Architecture — semantic and requirement joins

R01–R24 are the accepted IDs in `A/reports/REQ-G2-MOS-1259.md:43–66`.

| Requirements | Contract evidence and bounded conclusion |
|---|---|
| R01/R10–R13 | CRUD:731–750,810–830,849–863: personal persistence, own list, resource filter, backend owner, indistinguishable foreign/missing `404 NOT_FOUND`. P/get supplies separate pagination; response `user_id` is already present, not a proposed owner field. CRUD says external-admin string identifier, not necessarily UUID. No client owner authority. |
| R02/R14 | Create/Patch name constraints above; CRUD:744–750 explicitly permits duplicate names. Neither uniqueness nor automatic overwrite is declared. Trimming/Unicode counting/case normalization unspecified; internal spaces are not prohibited. |
| R03–R07/R16 | CRUD:749–750,776–781,827–848: full search including query/ordinary filters/conditions/sort/limit/offset, validated against current resource and stored whole with defaults. Saving does not execute search or save results. `search:{}` saves defaults. Resource immutable; top-level omitted fields retained; supplied search entirely replaces prior search and missing nested values use defaults. Formal open search object alone does not encode these rules. |
| R08/R09/R23 | P/post 201 UUID data.id; I/get 200 full detail; I/delete 200 UUID data.id. CRUD:830 explicitly physical deletion. Create-then-GET is owner plan F/design:54, not an automatic server follow-up. No name-as-ID or soft-delete inference. |
| R11 | P/get parameter defaults/bounds above; CRUD:810–825 says fixed created_at DESC then id DESC, empty list on no matches, no resource returns own filters across resources. List paging does not mutate persisted search paging. Query resource is not enum-constrained in OpenAPI. |
| R15/R16/R19/R24 | **Method discrepancy:** accepted Jira explicitly PATCH; P/I enumerate published PUT only; CRUD:741,827–848 specifies PUT; F/design:8 delegates wire/semantics to these sources, :21–23 records contract-update PUT ruling, :51–54 explicitly names saved-filter PUT. D065:5–9 preserves semantic/method boundaries. This is a join to an existing recorded ruling, not precedence guessed from recency or similarity. Keep known PUT contract distinct from unresolved external requirement wording. |
| R17/R18 | CRUD:854–863 allows submission of saved search and offset0 when first page desired; stale objects remain readable, application validates current contract. Mandatory apply offset0/full restoration and no-partial policy belong to accepted owning plan/spec:9,18–19 and corrected SPEC F3. Contract does not itself mandate URL/history encoding or prohibit every explained recovery. No new migration/version field/policy. |
| R19–R21 | CRUD:778–781 gives 422 VALIDATION_ERROR with `/search/...` pointers; :825 invalid query →400 INVALID_ARGUMENT; :827–830 rejects null and empty PUT→422 EMPTY_PATCH. Formal OpenAPI instead admits null fields/empty object, and declares only autogenerated 422 detail grammar. Input preservation, honest UI success and no localStorage fallback remain consumer requirements, not server schema effects. |
| R22 | CRUD:72–92 requires authorization, global scope, TSAM.ManagedResource read/create/update/delete by action and owner restriction. F/spec:26–38 preserves UI-only mapping and backend scope. No frontend ACL, role-derived grants or credential-bearing mock requirement. |
| R24 | Scenario verification obligation only. This documentary audit runs no tests, demonstrates no implementation or deployment, and closes no feature task. |

### Error/status grammar and remaining mismatches

`D/crud-api.md:415–428,1199–1220` describes SUCCESS with empty errors on success; errors use data:null, code/message and all error items, with `field` JSON Pointer or absent for form errors and optional details. `:1282–1296` lists general 200/201/400/401/403/404/405/409/422/500 statuses; it does not prove each general example applies to saved filters. Saved-filter-specific 400/404/422 meanings are above; null rejection's precise code is not explicitly selected. No saved-filter-specific 409 uniqueness failure is established, and duplicate titles are explicitly allowed.

The inspected OpenAPI operation response maps contain only success and 422; 422 refers to HTTPValidationError (`detail[].loc/msg/type`, not TSAM envelope). ErrorItem is reachable through success envelope optional errors, but that does **not** formally document a business-error response status. No invented union or silent coercion reconciles these shapes. F/design:71 already records broad nullability/autogenerated-422 versus business-document differences and an integration check boundary. Actual deployed response grammar and permission enforcement remain unknown.

## Explicit unknowns / residual risks

- Deployment, current live freshness, CORS, real ownership/permissions, and actual error envelopes are unverified. No source acquisition or business calls occurred.
- Jira PATCH wording requires parent reconciliation disposition; this is not uncertainty about inspected PUT publication. No method edit or API substitution is proposed.
- OpenAPI admits null/empty updates where CRUD rejects them; resource search fields are untyped at this boundary. Runtime validation/default normalization cannot be claimed from schemas alone.
- Exact whitespace trimming/character counting, concurrent update guarantees, stale-schema migration, selected-filter URL encoding/history, active-filter deletion aftermath, retries/undo are not established by assigned operations. No policy invented from absence.
- Readability of stale search is documented; successful application is not guaranteed. Existing UI no-partial policy remains separate from server current-schema validation.
- Accepted requirement evidence inherits omitted Jira comments/custom fields and flattened wiki limitations; those primaries were not freshly audited here. Independent acceptance/publication belongs to parent and reviewer.

## Start Here

Open `docs/api/contracts/crud-api.md:827–850` with `docs/api/contracts/managed-resources.openapi.json` at `I/put` and `S/SavedFilterPatch`, then `openspec/changes/mos-1249-feedback-api/design.md:8,21–23,51–54`. These distinguish the published method, two-level replacement semantics, schema/business mismatch and existing authority without changing scope.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Read all five saved-filter operations and 15 reachable schemas, compared r2/aggregate/split, verified expected hashes, joined R01–R24 and explicit API-owner PUT ruling while preserving source discrepancy."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/c4b6be31-55d1-4433-871d-e24706064a72/API-G2-FEEDBACK-SAVED-FILTERS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read/find/scoped grep; local Python JSON reference traversal, structural equality and hashlib; sed/nl/head","result":"passed","summary":"All expected contract hashes matched; 15 reachable schemas equal and all five operation differences limited to approved security normalization."},{"command":"Tests/typegen/build/network/browser/business calls","result":"not-run","summary":"Prohibited by assigned read-only documentary scope."}],
  "validationOutput": ["Published PUT only; DTO/operationId Patch naming does not declare PATCH.","CRUD preserves omitted top-level fields and replaces supplied search with defaults for omitted nested values.","OpenAPI null/empty update and autogenerated 422 differ from explanatory business constraints."],
  "residualRisks": ["Runtime/deployment/live freshness unverified.","Jira method wording awaits parent disposition; independent review pending.","Business versus formal validation/error grammar differences remain explicit."],
  "noStagedFiles": false,
  "diffSummary": "Only configured external report written; repository not edited.",
  "reviewFindings": ["No authority to rewrite methods; existing PUT ruling joined, no new product gate.","Do not conflate whole-search replacement with whole-resource replacement."],
  "manualNotes": "Parent confirmed authority boundary via contact_supervisor. No nested agents or tests. Index state was not inspected; noStagedFiles=false does not assert staged changes. Hashing raw CRUD was identity verification only, not semantic reading."
}
```
