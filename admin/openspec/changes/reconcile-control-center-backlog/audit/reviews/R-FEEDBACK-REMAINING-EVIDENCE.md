# Consolidated Feedback evidence review

## Review
- **Correct:** The candidates distinguish published schema, business prose, connected mock behavior, written assertions and deployed behavior. Their principal implementation findings are supported.
- **Fixed:** None; review-only.
- **Merge verdict:** **OK with notes for evidence consolidation**, subject to the small report corrections below. This is not feature acceptance or global G2 completion.

## Per-report disposition

| Candidate | ACCEPT | REVISE | ESCALATE |
|---|---|---|---|
| `api-read-export.md` | Local CSV operation identity, binary success, schema/prose distinctions, operator semantics, and existing-owner/no-new-plan disposition. | Attribute cross-document equality to the analyst’s comparison, not this independent review. | Independent certification of saved-r2 equality remains limited: its single 410KB line exceeds the reader’s 50KB limit. Metadata was read; snapshot operation/schema content was not independently retrieved. Parent notified. No new product decision needed. |
| `impl-read-export.md` | Actual Feedback options, permissive membership, CSV defaults, test limitations and bounded consumer absence. | Resolve the metadata join explicitly; remove stale suggestions that C9/R02 remain pending planning corrections. Exact replacements below. | None beyond existing real-API release checks. |
| `impl-editor-lifecycle.md` | Replacement/null behavior, missing quiet-hour dependency, released codes after deletion, and carefully bounded assertions. | No material correction required. Treat candidate source/hash checks as candidate-attributed, not independently reproduced here. | None. Q1 remains untouched. |

## Independently verified joins

### 1. Feedback uses generic—not stronger registry—options

`mocks/managed-resources.mjs:81–100` calls `searchManaged` and `sendManagedCsv` without options; detail export does likewise at line 47. Thus:

- Equality/membership lowercases values: `mocks/managed-search.mjs:41–54`.
- CSV defaults to comma, no BOM, generic filename and `EXPORT_LIMIT`: lines 94–113.
- Stronger options in `mocks/managed-registry-handlers.mjs:56–84` belong to `api_endpoint`/`tpl_template`, identified in `managed-registry-model.mjs:3–27`, not Feedback.
- Registration is connected through `managed-resources.mjs:169–193` and `mocks/app.mjs:41–81`.

These are concrete mock fidelity gaps, not evidence that the real backend behaves likewise.

### 2. Schema allowance does not establish operator-dependent validity

`docs/api/contracts/openapi.json:19197–19338` allows scalar strings and arrays without uniqueness constraints. The connected validator explicitly passes `allowScalarMembership:true, uniqueMembership:false` (`mocks/managed-validation.mjs:69–72`).

Business prose instead requires unique arrays for membership and case-sensitive equality/membership (`docs/api/contracts/crud-api.md:618–646`). Current MOS-1258 spec lines 9–15 agrees.

The tests **positively accept** scalar and duplicate membership (`mocks/managed-resources.test.mjs:249–267`); these are not merely missing assertions.

### 3. CSV findings and test discrimination are accurate

- Duplicate export fields pass the inspected schema and handler; requested order, including duplicates, reaches CSV (`managed-search.mjs:102–105`).
- Business CSV requires BOM, semicolon, metadata labels, unique fields and `EXPORT_LIMIT_EXCEEDED` (`crud-api.md:893–918`).
- `managed-search.test.mjs:15–53` asserts comma/no-BOM bytes and `EXPORT_LIMIT`, including the 10000/10001 boundary.
- Filtering precedes pagination; export bypasses pagination (`managed-resources.mjs:81–97`).
- The export assertion uses only one matching record (`managed-resources.test.mjs:113–118`): it does **not** discriminate larger-than-page export or ignored offset.
- All composition fixtures are draft (`:73–107`): the test does **not** discriminate an incorrect status-AND implementation against a wrong-status OR match.
- The helper only matches CSV content, and its delete assertion checks DELETE then GET404—not repeated DELETE (`managed-contract-test-helpers.mjs:86–94`).

### 4. Metadata envelope is now resolved

**Finding P2 — evidence wording should finish this join.**

`resourceMetadata` produces `{fb_survey: ...}` (`managed-resources.mjs:58–74`), and `sendSuccess` wraps that object as `data` (`mocks/contract.mjs:180–197`). The actual statically inferred success envelope is therefore **`data.fb_survey`**.

CRUD explicitly requires **`data.surveys`** (`crud-api.md:291–303`). The formal schema permits arbitrary resource keys (`managed-resources.openapi.json:7278–7304`), so this is a **mock-versus-prose mismatch, not a formal-schema violation**.

Smallest report correction: replace “retain this integration seam for API join” with that conclusion. Keep labels qualified: mock headers equal mock metadata labels; richer business labels/catalog bindings remain fidelity work, not proof that the current helper contradicts its own metadata.

### 5. Editor/lifecycle conclusions are supported

- Shallow replacement plus population preserves omitted top-level rules, replaces supplied nested rules and preserves explicit null/false/0 (`managed-resources.mjs:28–39`; `managed-model.mjs:31–59,72–76`). **Do not recommend deep merge.**
- Rules schema permits nullable quiet boundaries without a cross-field dependency (`managed-resources.openapi.json:4692–4901`); inspected save validation adds none. Enabled quiet hours with missing boundaries are therefore a supported static gap. Timezone/cross-midnight runtime behavior remains unverified.
- DELETE physically removes the record; uniqueness checks only remaining records (`managed-resources.mjs:36–37,48–53`). State has no reserved-code store (`managed-model.mjs:95–101`). Deleted codes can consequently escape recreate/update uniqueness checks.
- Null assertions cover two rules through an owner-only PUT, not the full edit/null/replacement regression (`managed-resources.test.mjs:108–111`).
- Never-existing-ID404 tests are not repeated-deletion tests (`:63–67`).

### 6. Formal API versus prose remains an existing release gate

Both local export operations were directly read in aggregate (`openapi.json:4315–4420`) and split (`managed-resources.openapi.json:230–335`): required request bodies, binary CSV200, formal HTTPValidationError422, no declared success headers or additional business status variants.

CRUD supplies the richer envelope/status/header behavior (`crud-api.md:901–993`). MOS-1260 `design.md:44–45,54` already retains error/permission integration checks. No schema rewrite or new permission policy is justified.

## Minimal report and owner disposition

**Finding P2 — stale planning language:** In `impl-read-export.md` “Keep plans” and its final `reviewFindings`, replace language “retaining … planning correction” with:

> C9 condition-targeted errors and R02 metadata-derived labels are already integrated; no further planning correction is proposed.

Their current clauses are present in MOS-1258 spec line 15 and MOS-1260 spec line 9. Lifecycle status-pending is also already present in MOS-1256 task 1.1.

| Existing owner/task | Consolidated remaining implementation/evidence work |
|---|---|
| MOS-1258 tasks 1.1–1.2, 2.3; MOS-1250 shared selection | Metadata fidelity, operator-specific validation/case semantics, discriminating composition tests and connected draft/applied UI. |
| MOS-1260 tasks 1.1–1.2, 2.3–2.4 | Feedback-specific CSV options/field validation, endpoint/header/beyond-page assertions, download/session behavior and real CSV gates. Do not change shared defaults indiscriminately. |
| MOS-1251 tasks 1.3–1.4, 2.3 | Quiet-hour dependency, full nullable/replacement regression and editor/error/unknown-outcome behavior. |
| MOS-1256 tasks 1.1–1.2, 2.3 | Preserve occupied codes after deletion; test recreate/update conflicts, repeated DELETE404 and disabled-record retention. |

**No genuinely missing planning change established.** No mock role enforcement, feature closure, Q1 choice or global G2 closure is proposed.

## Actual coverage and limits

Read both assignments and all three candidates completely; directly inspected the named generic handlers/model/validation, all three relevant test/helper files, request/response envelope and registration seams, local export operations, condition/export/rules/metadata schema slices, relevant CRUD clauses and current owner tasks/spec/design clauses.

Rechecked route composition, complete base/compatibility registries and both optional route descriptors; reused accepted UI-entry findings. This supports **no mounted Feedback consumer at that composition boundary**, not absence of every disconnected implementation or test.

Saved-r2 metadata was read; full snapshot equality and candidate dependency-closure comparisons were **not independently reproduced**. Candidate artifact hashes remain parent-attributed as supplied in the assignment; no hash or checkout certification is claimed here.

No edits, network, tests, build, browser/E2E, source execution or nested delegation occurred. All behavior conclusions are static; no passing tests or deployment acceptance is asserted.

Output: `/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/6b3228e6-2df8-4803-9f61-1dc5e71d8bb8/feedback-batch-review.md`