# Code Context

## Result

**IMPL-G2-FEEDBACK-SAVED-FILTER-MOCK only; read-only static audit.** HEAD `bc0d9800f25a90989b9c73c76f91996f8300f1d3` matches assignment. The connected mock implements all five saved-filter operations, ID-based storage, replacement of supplied search, and independent list paging. For `resource=feedback-surveys`, it is nevertheless a generic scaffold rather than faithful business-contract support: empty PUT succeeds, search defaults/full validation are missing, and validation errors use the formal 422 grammar rather than the documented business errors. Existing assertions partly encode these differences. No test was run; no UI, deployment, ownership enforcement or feature acceptance is claimed. Q1 remains unresolved and no preserve/omit/block choice is made. Parent owns acceptance.

Literal path bases used below: `C = openspec/changes/reconcile-control-center-backlog`; `A = openspec/changes/reconcile-control-center-backlog/audit`; `D = docs/api/contracts`. These are exact repository-relative prefix substitutions.

## Key Code — bounded evidence joins

### F1 — Feedback empty PUT incorrectly reports success (high confidence, static)

Accepted API report/review and `D/crud-api.md:827–830` require `422 EMPTY_PATCH`; MOS-1259 R19/R24 require honest failure handling. Actual path: `mocks/app.mjs:62–80` → schema request validator → `mocks/managed-resources.mjs:115–133`. `SavedFilterPatch` permits `{}`; `saveFilter` copies the existing record, updates `updated_at`, and returns SUCCESS. Its validation chain (`:106–112`) has no Feedback empty-body check: `validSavedManagedStringConditions` checks only conditions (`mocks/managed-validation.mjs:87–91`); all three other saved-search helpers return immediately for this resource. The registry helper's EMPTY_PATCH branch applies only to api-endpoints/response-templates, not Feedback.

Thus an existing valid Feedback filter plus PUT `{}` reaches success, not the required error. Missing-ID PUT `{}` still returns404 first. This is a concrete false-success **mock** path, not evidence about UI toast behavior. Tests `mocks/managed-resources.test.mjs:162–188` check missing-ID `{}` but never existing Feedback `{}`. `mocks/managed-registry.test.mjs:253–285` checks empty PUT rejection for other resources only (its examples `:10–42`). Do not transfer those assertions to Feedback.

### F2 — supplied search replaces, but Feedback defaults/current-resource validation are absent (high confidence, static)

R03–R07/R16 join `D/crud-api.md:749–780,827–850`: save complete resource search with defaults; omitted top-level fields survive, supplied search replaces and omitted nested parameters default rather than inherit. `saveFilter` uses `{ ...existing, ...req.body }` (`mocks/managed-resources.mjs:120–128`), so top-level preservation and whole-search replacement exist; it does not deep-merge the old search. However no Feedback normalizer runs. `validManagedRecord` validates the response's **open object** search, not `fb_surveyListQuery`; `validManagedStringConditions` explicitly treats Feedback search as opaque except for conditions (`mocks/managed-validation.mjs:42–84`). `mocks/contract.mjs:26–32` does not enable AJV useDefaults.

Consequences supported by actual flow, not executed requests: Feedback `search:{}` stays `{}`; malformed non-condition fields such as `{limit:0}`, unsupported sort or extra properties are not checked against the current resource search DTO. Inspected `fb_surveyListQuery` instead declares limit1–100/default20, offset>=0/default0, default sort and additionalProperties=false. No survey execution audit is needed for this finding.

Existing static assertions actively demonstrate the seam: `mocks/managed-contract-test-helpers.mjs:97–112` creates a Feedback filter then asserts PUT `{search:{}}` returns exactly `{}`. `mocks/managed-resources.test.mjs:195–277` saves opaque `future` alongside valid conditions for Feedback/catalogs and asserts it survives; it does not establish general current-resource validation. This finding does **not** decide Q1 unknown-question options: saved-search fields and question options are different boundaries.

### F3 — invalid-query/error grammar differs from the business contract (high confidence, static)

R19 joins `D/crud-api.md:776–778,824–830`: nested `/search/...` business errors, invalid list query `400 INVALID_ARGUMENT`, empty update422. `mocks/contract.mjs:49–51,152–179` emits `{detail:[{loc,msg,type}]}` with422 for non-Dialogs validation; Feedback condition errors use the same function (`mocks/managed-validation.mjs:48–80`). `mocks/managed-resources.test.mjs:182` explicitly expects422 for saved-filter `?limit=0`, contrary to CRUD400. This aligns with the formal OpenAPI422 representation, whose disagreement with business prose is already retained by accepted API review; it is not a newly discovered authority decision. Missing IDs do use business `404 NOT_FOUND` (`managed-validation.mjs:18–20`). Null name/search are rejected by response-record validation before persistence, but only at generic `body` location (`:6–15`), not a targeted business pointer. Existing null/immutable-resource/state-preservation assertions at test `:178–186` are for catalogs; Feedback rejection follows the same record/request schemas but is not independently asserted there.

### Supported scaffold behavior and exact assertion limits

| Requirement join | Actual implementation | Existing assertions read / limitation |
|---|---|---|
| R01/R08/R09/R14/R15/R23: create, ID identity, detail, update/delete | `managed-resources.mjs:115–165`: random UUID, push on every create, find/update/splice by ID; no name lookup or uniqueness rejection. Fixed `user_id:'local-demo'`. POST201, GET/PUT200, DELETE200. Published PUT is registered despite `patch_saved_filter` function key. | helper `:97–112` asserts create→detail name, PUT search, count and DELETE returned ID for Feedback. No duplicate-name pair or selected-ID isolation assertion in the read saved-filter tests; no post-delete Feedback GET assertion. Runtime persistence is in-memory only, reset by createManagedState; not real server persistence. |
| R02/R16: title, immutable resource, omitted top-level fields | Request schemas enforce name1–150/non-whitespace and forbid extra top-level fields/resource changes. Object spread preserves omitted name/search; nulls rejected before mutation. | test `:162–188` checks blank catalog name and immutable-resource/null failures; no Feedback title boundary suite, name-only/search-only preservation assertions. |
| R10/R11: resource isolation and separate paging | handler `:140–154` filters resource before sorting created_at DESC/id DESC and `page`; `list.mjs:3–16` slices with independent query limit20/offset0 defaults. Empty total_pages overridden to0. Saved search pagination is not touched. Omitted resource lists all mock resources. | test `:175–177` verifies Feedback list count0 when only a catalog filter exists; helper checks total1 unfiltered. No multiple-Feedback-page/order/tie-break or persisted-search-offset independence assertion in inspected tests. |
| R19: no mutation on invalid conditions | Conditions schema/value checks execute before push/Object.assign. | test `:195–277` loops explicitly over Feedback/catalogs, rejects numeric/mixed/invalid condition values, unknown field and invalid operator, deep-compares state snapshots and verifies final search. Nested detail-loc assertion there targets **export**, not saved-filter error pointer. No injected Feedback storage-failure assertion in this read set. |
| R12/R13/R22 | Local mocks deliberately have no credentials/role/owner enforcement; missing-ID GET/PUT/DELETE404 exists. | test `:183–186` covers missing IDs on shared endpoint. No real foreign-owner behavior can be inferred; lack of mock enforcement is not a defect. |
| R17/R18/R20/R21/R24 consumer application | Full apply/offset0, stale-search UI rejection, input preservation, no localStorage fallback and permission-visible controls belong to consumer/UI evidence. | Not assessed by this mock seam. No UI composition files read; no assertion that UI is present or absent. Static mock tests cannot satisfy these consumer scenarios or deployment acceptance. |

## Architecture

`createMockState` (`mocks/state.mjs:13–34`) creates `managed.savedFilters=[]` (`managed-model.mjs:95–101`). `createMockApp` mounts an Express `/api` router and registers operations from the local OpenAPI, mapping published `/api/control/api/...` to mock `/api/...` via `toRoutePath`. Registered `managedResourceHandlers` builds saved-handler operationId mappings (`managed-resources.mjs:169–194`); `createRequestValidator` validates request schemas before invoking them. `saveFilter` merges top-level inputs into a new record, validates conditions/resource-specific helpers and the response record, then mutates memory and sends a response checked against its response envelope. GET/list/delete use the same state. This is actual connected **mock application** code, not a generated DTO as implementation proof, and not the production transport/UI route.

The optional/registry saved helpers were followed only to establish their early-return boundary for Feedback. No optional feature or dialog consumer audit was performed. Shared transport/application deployment configuration was not audited; no production inclusion/exclusion claim is made.

## Files Retrieved — exact semantic coverage

1. `A/work-items/G2-FEEDBACK-IMPLEMENTATION-SEAMS.md:1–17` complete common contract/unit; other unit descriptions visible, not executed.
2. Governing `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108` complete. Truncated combined output was repaired by separate proposal/design1–36 reads. `A/decisions.md:1–30` only, D066/Q1 and acceptance boundaries.
3. `A/reports/API-G2-FEEDBACK-SAVED-FILTERS.md:1–140`, `A/reports/REQ-G2-MOS-1259.md:1–113`, `A/reports/SPEC-G2-MOS-1259.md:1–121`; `A/reviews/R-API-G2-FEEDBACK-SAVED-FILTERS.md:1–74`, `A/reviews/R-REQ-G2-MOS-1259.md:1–68`, `A/reviews/R-SPEC-G2-MOS-1259.md:1–82`, complete. API/REQ beginnings lost in an initial combined output were read separately. Accepted source extraction reused; no fresh Jira/wiki census. Initial command requested audit README but its output was truncated away: no README semantic read claimed or relied upon.
4. Complete: `mocks/managed-resources.mjs:1–194`, `mocks/managed-resources.test.mjs:1–277`, `mocks/managed-contract-test-helpers.mjs:1–112`, `mocks/managed-model.mjs:1–101`, `mocks/managed-validation.mjs:1–91`, `mocks/app.mjs:1–127`, `mocks/contract.mjs:1–202`, `mocks/list.mjs:1–30`, `mocks/state.mjs:1–34`. Unrelated survey/catalog code visible in these bounded starter files is context, not separately audited.
5. Boundary reads only: `mocks/managed-registry-validation.mjs:65–90`, `mocks/managed-registry-model.mjs:1–65`, `mocks/managed-registry.test.mjs:1–55,250–290`, `mocks/knowledge-base/validation.mjs:150–187`, `mocks/ab-testing/validation.mjs:150–185`.
6. `D/crud-api.md:729–863`. `D/openapi.json` semantic JSON reads: both complete `/paths/~1api~1control~1api~1v1~1managed-resources~1saved-filters` and `/paths/~1api~1control~1api~1v1~1managed-resources~1saved-filters~1{filter_id}` objects; complete `/components/schemas/{ManagedResourceSavedFilterCreate,SavedFilterPatch,tsam__assistant_management__managed_resources__endpoints__http__schemas__SavedFilterResponse,fb_surveyListQuery}`. No transitive schema-closure audit or generated declarations read.

Discovery bounded to `find('*managed*', path='mocks')`, then grep under mocks `*managed*.mjs` for `saved.filter|SavedFilter|savedFilter`, and `*.mjs` for exported saved helpers/managedResourceHandlers/createManagedState. Audit path find was filename discovery (1000-result truncation), not a complete audit inventory. Absence claims above are limited to the connected functions and read assertions, **not repository-wide test absence**. No project commands executed beyond non-interactive local inspection, JSON extraction, HEAD and hashing.

## SHA-256 provenance

Computed over full bytes; hashing is not semantic reading. Path prefixes expand as above. The API report hash differs from its original reviewer target because D066 records parent citation cleanup; no fresh independent acceptance inferred.

| Input | SHA-256 |
|---|---|
| `C/proposal.md` | `1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879` |
| `C/design.md` | `632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828` |
| `C/tasks.md` | `a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83` |
| `C/specs/control-center-backlog-reconciliation/spec.md` | `a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36` |
| `A/work-items/G2-FEEDBACK-IMPLEMENTATION-SEAMS.md` | `34e936ab5ed856502b7ef90636c6ef6257d8b0cba6b1cf40e571f372ab565f66` |
| `A/decisions.md` | `0c6ab613cd2f9d7a6ba9c79609cafd1dc3fc73d0c1645cbcee355b06e0b3d857` |
| `A/reports/API-G2-FEEDBACK-SAVED-FILTERS.md` | `6b1f871690de1d73bb177b1f14f8698c27d9a6dbbaadc08f274a49d4ec42e7b2` |
| `A/reports/REQ-G2-MOS-1259.md` | `b928122009f79f48b4789fadcd476bbd1a8bdf669fc438b4cceacd7b3197bd25` |
| `A/reports/SPEC-G2-MOS-1259.md` | `cdbde326a62a7996ed5adc07faaab46a7587ea81dde685425eec0955f594e62a` |
| `A/reviews/R-API-G2-FEEDBACK-SAVED-FILTERS.md` | `424ab182b586431790e84f923090e75740d1de2319686371610b7f7a1a397d04` |
| `A/reviews/R-REQ-G2-MOS-1259.md` | `b0287c540b7222d1860f90a72e396960f645d184a12a3f82e8b6cc76d01bbbc2` |
| `A/reviews/R-SPEC-G2-MOS-1259.md` | `c5abce85f35cc51b2c75c60c70b37fc10f8d1749f4aedd573de1d10cc5eb1538` |
| `mocks/managed-resources.mjs` | `491ea71f90c4ef4c6b7876450b3f763286ff856e5c9c076eb92cf74570ef6483` |
| `mocks/managed-resources.test.mjs` | `f84fb6d35b7b88d35cb86fd38d5d7666b5aa0c661ce43cae551cdec920b43245` |
| `mocks/managed-contract-test-helpers.mjs` | `d1e753fbe2de85f72287672b82728defb34cb1b8c1e7218377b4e6df92cfaf62` |
| `mocks/managed-model.mjs` | `472534b1746b60145a8e45d35cd98c141afd3ab59bd1c6ee5194061ea6a95a61` |
| `mocks/managed-validation.mjs` | `fce2b2f8bbd2d7820a9885e3a8a1358ef042d5c3225bef02c6a151231382b44c` |
| `mocks/app.mjs` | `b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0` |
| `mocks/contract.mjs` | `ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371` |
| `mocks/list.mjs` | `e1af394687dd92e656f0e0def06e3206a9eb217a43a5f366e6d410d622a34b7c` |
| `mocks/state.mjs` | `d80532dc6318021afe15c65bb095ebac55876d34e61195e0731604d6af59a93e` |
| `mocks/managed-registry-validation.mjs` | `369552248f687c687eee908a6983a86090077b934d0f798a301bd1d01ab8d530` |
| `mocks/managed-registry-model.mjs` | `bfaef2dcf35735476af29a2840a1e18e714ccbc50cf3318778b087a39117eab6` |
| `mocks/managed-registry.test.mjs` | `6a72303dfd997d8730e8dfdfdf7e84d493658ea5155cb722925bb11c4e2e30c4` |
| `mocks/knowledge-base/validation.mjs` | `d9d2dbe94c6d0202bbbd79a514adf071733a91b241f9abdd2fec396f7631a39e` |
| `mocks/ab-testing/validation.mjs` | `28b92373bb78af2d2cbe4cf96e4b9a5728f288bbd72c0577850e2768c774ff67` |
| `D/crud-api.md` | `4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058` |
| `D/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |

## Start Here

Open `mocks/managed-resources.mjs:106–133` with `mocks/managed-contract-test-helpers.mjs:97–112` and CRUD827–850. Review the resource-specific validation dispatch before treating shared operation coverage as Feedback acceptance. Potential future remediation belongs to these handlers/validators and relevant test assertions; no changes are authorized or made here.

Residual risks: all findings are static, not observed request results; uninspected tests may add coverage but cannot negate the connected code paths. UI integration, real storage failures, deployed error grammar, current backend behavior and foreign-owner isolation remain unverified. Original Jira/wiki completeness limitations are inherited. Q1 is still pending; no task checkbox or publication disposition changed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Bounded connected mock/test audit joins MOS-1259 rows and accepted API evidence; three concrete static gaps and supported behavior recorded with exact coverage and hashes."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/75dfce2b-1e10-4111-9fea-8a150a50fdfc/IMPL-G2-FEEDBACK-SAVED-FILTER-MOCK.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find/scoped grep; git rev-parse HEAD; nl/head/sed; Python JSON extraction and SHA-256","result":"passed","summary":"Read connected handlers and existing assertions; recorded HEAD and full-byte input hashes."},{"command":"Tests/network/browser/business calls/build/typegen","result":"not-run","summary":"Explicitly prohibited; no nested agents or project writes."}],
  "validationOutput": ["Static: Feedback empty PUT reaches SUCCESS; supplied search lacks defaults/full validation; validation grammar/query status differ from CRUD business prose."],
  "residualRisks": ["No runtime/UI/deployment or real ownership proof; uninspected tests not inventoried.","Q1 remains unresolved; parent owns independent acceptance/publication."],
  "noStagedFiles": false,
  "diffSummary": "Only configured external report written; no project files changed.",
  "reviewFindings": ["F1: existing Feedback empty PUT false success.","F2: Feedback search defaults/current-resource validation absent beyond conditions.","F3: 422 detail grammar and invalid-query status differ from business contract."],
  "manualNotes": "Static manual inspection only. Index not inspected; noStagedFiles=false makes no assertion that staged files exist. This attests report completion, not parent acceptance or feature delivery."
}
```
