# Dictionaries: API, implementation seams and OpenSpec ownership

Read-only planning analysis for **one `add-reference-dictionaries` change**, not an MVP selection or implementation. HEAD verified: `d2af6c5b61146306f0795b6a272c5a74bdfa08f7`. Repository status and staged diff were empty. No network, browser, prototype execution, test execution, application/contract/spec/config edits or Git mutations. Only this requested report is written.

## 1. Evidence and reproducibility

Paths below are repository-relative. `S` = `openspec/changes/reconcile-control-center-backlog/audit/sources/`.

| Source | SHA-256 |
|---|---|
| `S/wiki-247751846/r2/content.json` | `6f4a85bf911634a724e3411138c517fe3ce295d2036e09d573444dc9d6d04588` |
| `S/wiki-247751846/r2/readable.txt` | `002d6b34375939d9f8847350ef0cdf9ff6db8f151028f297da6750ba0d1c0957` |
| `S/local-dictionaries-prototype/r1/content.html` | `385f230467db6b8b2fdf26dbc08f9154ca7fd1651db037c6227eccc9fc8fa310` |
| `S/api-live/r2/content.json` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `docs/api/contracts/openapi.json` | `c19ff30e53a8705629bc11d51a25b3a2019ef641340348a7f2e985088127fe3d` |
| `docs/api/contracts/managed-resources.openapi.json` | `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf` |
| `docs/api/contracts/crud-api.md` | `4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058` |
| `docs/api/contracts/crud-api-2026-10-15.raw` | `91c8dc68fc1b602a64428d1d6f1d9c44a0e6a89eced226e4773853badf13954a` |

Wiki authority is the exact user URL `https://wiki.mos-team.ru/spaces/KR/pages/247751846/`, saved version 10. API r2 metadata identifies `https://nchat-a-tech.mos.ru/api/control/openapi.json`, retrieved 2026-10-19T08:11:44.238Z. This lane did not refresh either source. Wiki headings/anchor IDs in readable.txt are stable locators; prototype function names are static-code locators, not executed evidence.

Offline JSON comparison traversed **all 19 relevant operations and their 48-schema transitive closure**: local aggregate and managed split agree exactly; r2 schemas agree exactly; the only relevant operation differences are the accepted security normalization, live OR `[{AdminToken:[]},{AccessToken:[]}]` versus local AND `[{AdminToken:[],AccessToken:[]}]`. No dictionary-specific contract import is indicated. This is not a whole-API drift claim.

## 2. API report

### Published transport (not merely skill/dialog lookups)

Base `B = /api/control/api/v1/managed-resources`; generic dictionary base `C = B/catalogs`. Existing shared transport uses relative `/v1/managed-resources`, not the UI basename.

| Methods / path | Exact payload or output seam |
|---|---|
| GET `C/metadata` | `data.catalogs`: condition fields/operators, catalog bindings, export fields/max rows (`ManagedResourceMetadata`) |
| POST `C/search` | `ref_dictionaryListQuery`; envelope with items/pagination of `CatalogResponse` |
| POST `C` | `CatalogCreate`, required code/name; 201 `data.id` UUID |
| GET / PUT / DELETE `C/{entity_id}` | UUID; PUT `CatalogPatch`; GET/PUT 200 full `CatalogResponse`; DELETE 200 `data.id` |
| GET `C/lookups/{section}` | `CatalogLookupSectionName`; keyed arrays of `ManagedResourceCatalogItem` |
| GET / POST `C/{entity_id}/values` | GET array in data; POST union `ManagedCatalogCreate` / `AttachmentRuleCreate`, 201 `data.code` |
| PUT / DELETE `C/{entity_id}/values/{value_code}` | PUT union `ManagedCatalogPatch` / `AttachmentRulePatch`, 200 value; DELETE 200 `data.code`; address by current code, not value UUID |
| POST `C/export` | `ref_dictionaryExportRequest`: required ordered `fields`, optional `search` |
| POST `C/{entity_id}/export` | `ref_dictionaryDetailExportRequest`: required `fields`, no search |
| POST `C/{entity_id}/values/export` | **No request body**; ordinary/rules CSV schema selected by dictionary kind |
| POST / GET `B/saved-filters` | POST required resource=`catalogs`, name, search; 201 ID. GET resource query + limit 1–100 (default 20), offset >=0 (default 0) |
| GET / PUT / DELETE `B/saved-filters/{filter_id}` | UUID; PUT optional name/search; full search replacement; GET/PUT full saved record, DELETE ID |

These are 14 catalogs + 5 saved-filter operations, no PATCH. Locate each under `/paths` and named DTO under `/components/schemas` in r2/local JSON. `docs/api/contracts/crud-api.md` §§4, 9–10, 14, 18 supplies semantics not fully expressed by JSON Schema; `managed-resources.md` documents precedence/conflicts and release gates.

**Search:** query nullable, 2–200 characters; sort defaults `name`, enum ±name/code/kind/status/owner/values_count/created_at/updated_at. **No group/type sort**. limit 1–100; offset >=0. kind/status/group accept scalar or arrays; group enum system/informational/user. Conditions max 50, logic and/or; fields code/name/description/owner/kind/status/group. Operators contains/not_contains/eq/ne/starts_with/ends_with/is_empty/is_not_empty/in/not_in. Numeric branches in the generic value union **do not** authorize numeric conditions or `values_count` conditions. No local filtering of a single loaded page can satisfy those missing server capabilities.

**Dictionary settings:** wire `group` corresponds to Wiki type, `kind` distinguishes list/rules-attachments. Response includes UUID, timestamps, code/name/description/owner/kind/status/group/storage_table/public_api/values_required/cache_seconds/values_count/value_code_editable/allow_add/allow_delete/allow_rename. No checks, comment history or `is_disabled` field. Create code `^[a-z][a-z0-9_]*$`, max 100; name 1–255; owner <=200; cache_seconds integer 0–2147483647. Default group user, kind list, **status active**, public_api false, values_required false, cache_seconds 0. Draft can be requested as status; whether that is the agreed UI behavior must be explicit, not an accidental reliance on defaults.

PUT is partial. Documentation permits null clearing description/owner; JSON nullable patch branches are broader than documented business acceptance. group/kind/storage_table immutable; user dictionary code is editable by API, unlike Wiki's always-disabled code field. allow_* and value_code_editable are **computed response fields**, not writable preferences. POST creates only user; DELETE physically removes user dictionary/values and frees its code; non-user delete documented 405.

**Ordinary values:** code/display_name required; code pattern lowercase Latin first, then lowercase/digits/underscore; max 50 for connected section catalogs, 64 for user values (generic schemas permit 64). display_name 1–150; nullable description; sort_order 0–32767; is_active defaults true, is_default false; timestamps may be null. No separate value ID. Read includes inactive values, sorted sort_order then code. Default selection atomically clears previous default **within one value request**; default must be active; disabling default requires both is_active=false and is_default=false. At most one, not necessarily exactly one. Each row request is separately committed: **no batch/atomic entire-card save or reorder endpoint**. System values read-only; informational can add/edit except code but cannot delete; user can add/edit/rename/delete. These constraints differ materially from Wiki's informational delete and configurable allow_*.

**Attachment rules:** same value endpoints plus extensions (nonblank <=1000), mime (<=255, defaults empty), max_size_mb/max_count (integers 1–2147483647), zones (nonblank string <=255). Creation additionally requires extensions/max_size_mb/max_count/zones; only description clears with null. note maps conceptually to description; enabled to is_active, not Wiki table is_enabled. Do not silently translate auth/anon to skill-domain authenticated/anonymous: independent vocabularies. CRUD document §18.7 seeds attachment_rules as **user**, whereas Wiki registry lists **system**. APIs store policy settings, **do not enforce file uploads/MIME priority/security**.

**CSV:** r2 explicitly publishes `text/csv` binary success for all three exports. Documentation: UTF-8 BOM, semicolon, escaped/quoted cells, formula neutralization, filename from exposed Content-Disposition; limit 10,000 gives 422 EXPORT_LIMIT_EXCEEDED, never truncated success. List exports entire search irrespective of pagination. Fields: name/code/group/kind/values_count/owner/status/description/created_at/updated_at, unique/nonempty ordered selection. kind/status use labels; group is code. Values ordinary columns code/display_name/description/is_default/is_active; attachment columns code/category/extensions/MIME/max size/max count/zones/enabled/note. Exports read **saved** server data, not unsaved editor draft. Detail export is separate from values export.

**Saved filters:** keep resource catalogs, not dialog filters. Name nonblank 1–150; backend-owned user_id/IDs/timestamps. Search stored with defaults; PUT search replaces entire object, omitted fields default rather than merge with old search. Docs reject explicit null and empty PUT despite wider nullable schema; foreign/missing filter both 404. Pagination of saved-filter list differs from saved search pagination. User choice about applying stored offset vs resetting first page must be recorded.

**Errors:** formal OpenAPI generally enumerates success and 422 HTTPValidationError only (metadata only 200); that is not an exhaustive runtime status list. Preserve common code/data/message/errors envelope plus loc/msg validation details. Documentation includes 400 INVALID_ARGUMENT (UUID/query/section), 401/403 authorization/scope, 404, 405 non-user delete, 409 CONFLICT with IMMUTABLE_FIELD/SYSTEM_VALUES_READ_ONLY/DELETE_NOT_ALLOWED/IMMUTABLE_CODE/VALUE_IN_USE/NOT_UNIQUE, 422 invalid body/EMPTY_PATCH/EXPORT_LIMIT_EXCEEDED. JSON Pointer field errors can be nested under /search/conditions/items. Do not equate mock DUPLICATE_CODE with a guaranteed backend NOT_UNIQUE payload. No optimistic version or idempotency contract is published for these managed mutations. Preserve dirty input and unknown outcomes; no automatic replay or invented rollback guarantee.

### Lookup and consumer boundary

`C/lookups/catalogs` supplies kinds/statuses, not arbitrary table names or user-created dictionaries. Published section enum additionally contains skills/feedback/knowledge-base/ab-testing/api/response-templates. The CRUD text's smaller enum and assertion that `/skills/v1/catalogs` was removed are superseded by live and documented local normalization. That skill endpoint remains published and used by `app/entities/skill/api/skill-catalogs-client.ts`; it provides skill types/training/autotest states, not generic dictionary administration. `/dialogs/v1/dictionaries` and `/dialogs/v1/saved-filters` are likewise separate domain APIs; do not replace them.

Lookup includes inactive values for historical display; new choices normally use is_active. Existing consumers must preserve historical/unknown codes rather than replacing them with defaults. Registration and linking to owner tables belong to backend; user creation does not wire a new dropdown into every screen. No generic zone lookup contract was established by this inspection. Wiki's consumer catalogue is requirements evidence, not proof those consumers/registrations currently exist.

## 3. Implementation report (inspection, not delivery)

### Actual shell and reusable seams

- `app/routes.ts` builds native React Router entries from `app/application/constants/application-routes.constants.ts`, base `app/shared/config/constants/application-routes.constants.ts` and compatible routes. **No Dictionaries/catalogs/reference route or menu entry is registered** in these lists. `app/pages/placeholder/ui/placeholder-page.tsx` is a generic administrative-console placeholder, not an existing Dictionaries screen. Do not describe this as merely replacing a live dictionary page.
- Register the eventual section through the existing route/menu/breadcrumb configuration and `app/application/model/route-access.ts`, not prototype manual routing. Exact new URL/menu grouping requires a planning decision; do not inherit MOS959 URLs or optional-module policy.
- Reuse installed React Router search parameters/blocking facilities, TanStack Query/Table, React Hook Form/Zod; shared UI input/select/dialog/sheet/tabs/switch/selection-chips and `shared/lib/hooks/use-editor-input-snapshot.ts`. There is **no general shared dictionary filter/form engine** in inspected shared code. KB/A/B/feedback registry search, conditions, saved-filter and editor implementations are reference patterns, not legal imports of optional internals.
- `shared/api/http-client.ts`: apiRequest/apiBinaryRequest, error preservation, cancellation, session generation; `shared/api/file-response.ts`: readResponseFilename (filename* required, sanitized); `shared/lib/handlers/download-attachment.ts`: anchor download, caller owns object URL lifecycle. `optional/knowledge-base/api/knowledge-base-export-client.ts` demonstrates CSV MIME/BOM/non-JSON validation plus assertResponseSession/withResponseSession, but is **not** a shared export service. New client must preserve those protections without importing KB internals or doing a broad extraction.
- Ordinary FSD applies: proposed public `entities/reference-dictionary` for transport/DTO/query/domain state; feature slices for independent editor/filter/export actions, widgets/pages composition, framework route adapters. Names are a proposal, not edits. Do not create `app/optional/reference-dictionaries` merely by analogy: approved KB/A/B exceptions do not transfer. Types/constants/handlers stay with nearest owner; no feature-to-feature or optional cross-imports.

### Permission/session integration without grants

Current `entities/session/constants/permissions.constants.ts` contains no ManagedResource entries; `permissions.unmapped='*'`. `control-center-permissions` explicitly requires wildcard for unmapped business UI. `route-access.ts` defaults unmapped routes accordingly; `hasPermission` supports exact action/resource/*, not arbitrary prefixes. Backend CRUD docs publish ManagedResource read/create/update/delete/export and require global scope, but this **does not approve a new Dictionaries UI mapping**. Preserve current fallback unless separately approved. MOS-1249's proposed feedback mapping is not authority for this new section. No role grants, request ACL, auth redirect, transport token logic or mock credential changes are needed. Existing real/mock mode and session-owner checks govern JSON and CSV.

### Mocks and tests are useful but incomplete

Read `mocks/managed-resources.mjs`, `managed-catalogs.mjs`, `managed-model.mjs`, registry handlers/validation and relevant tests (`managed-resources.test.mjs`, `managed-registry.test.mjs`), plus README. The generic dictionary handlers already exist; this is not a missing-handler/501 feature. But they are not a faithful substitute for full §18 semantics:

- Generic catalog save spreads request fields; special protected registry IDs drive some read-only checks, not a complete group/allow_* domain model.
- Generic value writes validate a record and detect duplicate codes, but do not implement the documented cross-row default transaction, complete informational restrictions, all timestamp/order effects or owner-table linkage guarantees.
- Generic values export currently selects only code/display_name/description, not the documented five ordinary or nine attachment columns; generic metadata uses ref_dictionary resource key rather than required catalogs key. Lookup fallback is broader than the documented per-section dataset.
- Existing tests cover schema/union validation, local mutation no-loss, counts and saved filters. They do not prove server publication, all lifecycle semantics, upload enforcement or real permissions/CORS. Dedicated scoped mock/test work would be required in the future implementation change, not a rewrite of other managed owners.

Future unit/component/server acceptance should cover exact methods/DTOs, malformed responses, errors vs empty/unavailable, full-search export, limits/filename safety, URL/saved-filter roundtrip, unknown/inactive preservation, type/allow_* matrix, default and reorder partial failures, dirty navigation, session replacement, keyboard/focus, and no false checks/save success. No tests were added/run in this analysis.

## 4. OpenSpec report and boundaries

Read entry contract PLAN-DICTIONARIES.md and openspec/config.yaml. Existing capability guidance inspected: `control-center-http`, `control-center-api-integration`, `control-center-permissions`, `knowledge-base-module`, `ab-testing-module`. They provide transport/security/no-fabrication and isolation constraints, **not** a full Dictionaries product specification.

Direct owners inspected in full (proposal/design/tasks and the directly owned delta where applicable):

- `fix-skill-domain-zone-read-compatibility`: proposal/design/tasks + `specs/skill-domain-management/spec.md`. Owns only widened string-code reads across list/detail/PUT, known labels/raw fallback and editor no-loss; fixed assignment choices remain authenticated/anonymous. Explicitly excludes dynamic selectors/lookups and inactive-write policy. New Dictionaries work must not absorb, delete or silently complete it; attachment zones are unrelated. Future consumption changes need separate owner coordination.
- `mos-1249-feedback-api`: proposal/design/tasks + `specs/feedback-api/spec.md`. Explicitly excludes general dictionary CRUD; owns feedback lookup/metadata/client and its proposed permission mapping. Existing `app/optional/feedback` implementation makes historical design statements about absent code unsafe as current-code evidence. Do not mark its unchecked tasks complete or transplant its approved scope reductions.
- Archived `2026-10-13-update-control-center-contracts-put` and `2026-10-15-update-control-center-api-contracts`: full proposal/design/tasks inspected. They own contract synchronization, accepted security AND, PUT aliases, local managed handler coverage and preservation of distinct skill lookup. Their implementation checklists **do not certify a Dictionaries UI or production integration**. Historical 501 statements are superseded by later handler coverage. No archive edits requested.

KB/A/B remain independently removable consumers with their own module specs and integration documents. This lane does not claim full archived optional-feature acceptance coverage. Main specs `knowledge-base-registry`/`ab-testing-registry` and active feedback feature owners remain consumer boundaries, not permission to refactor those slices. No current dedicated dictionary product capability was found in the capability/change-name and relevant content searches.

Recommended single change composition: registry/filter/saved-filter/export; detail/settings/ordinary values/attachment values; creation/lifecycle/checks/dirty protection; explicit API and cross-consumer gates. These may be capabilities/tasks **inside one change**, never separate replacement feature changes. All new implementation checkboxes stay unchecked. No main specs, archives, contracts or config are edited by this analysis.

## 5. Material questions and gates (keep full Wiki scope)

**Product/source conflicts requiring explicit disposition, not silent normalization:**

1. **Whole-card Save versus per-row API commits:** approve a staged multi-request flow with visible partial-success/reconciliation semantics, or require a backend atomic save contract? Include reorder, default switching, deletion, rename identity and dirty-close behavior. A fake atomic save is unacceptable.
2. **Checks:** Wiki Tables §7 says 14 checks are computed server-side; no checks/recheck/result endpoint exists. Prototype `buildDictChecks` (~2017) computes locally and uses warning severities for description/MIME/enabled-rule. Is server readiness a backend prerequisite, with explicitly differentiated local validation only, or is a separately approved local-only product intended? Cannot claim “all checks passed” from DTO validity.
3. **Type/settings/deletion policy:** Wiki §§2,5,6 allows configurable flags/informational deletion, always immutable dictionary code and system settings read-only; API flags are computed, informational deletion denied and user code mutable. Wiki model says soft deletion, API documents physical deletion. Wiki/API disagree on attachment_rules group and registry ownership/classification. Which requirement needs backend change versus stricter UI-only restriction? Do not guess or auto-migrate data.
4. **Lifecycle/consumption promises:** draft creation can use explicit status, but status transition/save activation rules need confirmation. API expressly does not apply paused/public_api/cache_seconds/values_required to external consumers or enforce upload rules. Wiki promises immediate application and paused exclusion. Keep those promises as unmet integration requirements, not locally simulated success or scope removed from the encompassing change.
5. **Missing registry powers:** Wiki §3 asks type sorting and numeric values_count conditions; published enums lack both. Require backend extension or an explicit user-approved unavailable presentation. Never substitute kind sorting for group sorting or filter a loaded page. Comment-to-journal field has no API. Code uniqueness can be advisory search by code but has no dedicated availability/check endpoint and remains race-prone until POST/PUT conflict.
6. **Permissions and shell decisions:** retain wildcard-only existing policy, or separately approve the already-published ManagedResource mapping for this section? Choose route/menu placement and detailed URL/back/forward semantics; MOS959-specific decisions do not transfer.

**Unknown runtime/deployment gates, distinct from absent publication:** verify approved real operations, owner-table registrations/classifications, status/lookup effects, error payloads, CSV/CORS headers and authorization/global scope before release. Saved API evidence and local HTTP mocks prove none of these. Do not perform network/mutating verification in this planning run.

**Missing published contracts:** server checks/results, atomic aggregate save, writable allow_* / change-comment audit, type sorting, values_count numeric conditions, external publication/cache/paused-consumer behavior and upload-policy execution. These are not ordinary fetch failures. Preserve them explicitly in the one change, with no invented endpoints.

## Validation record

Read-only commands: `git rev-parse HEAD`, `git status --porcelain`, `git diff --cached --name-only`, targeted read/rg/find/sed/cat, `sha256sum`, and Python JSON/ref-closure comparison. Comparison passed: 19 operations, 48 schemas; no schema or split mismatches, accepted security-only operation difference. Source hashes above reproduced. Exploratory search errors included nonexistent `app/pages/compatible*` (and another guessed permissions glob); a separate grep/xargs no-match pipeline exited 123. These were inspection failures, not project mutations or runtime setup failures. Actual compatibility routing was inspected in `app/shared/config/constants/compatible-routes.constants.ts` and `app/routes/compatible.tsx`; permission code was located under `app/entities/session`. No guessed-path searches were repeated after the supervisor guidance. A follow-up report read requested an offset beyond its 126 lines, then correctly read the validation section; no evidence was lost. No yarn checks (analysis-only, no implementation), no browser/E2E, no staging. Independent review should check the material questions before authoring normative behavior.
