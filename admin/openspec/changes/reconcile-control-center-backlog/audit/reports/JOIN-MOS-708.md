# JOIN-MOS-708 — historical filters, pagination and URL semantics

## Result and ownership

**Bounded analytical join; parent review and acceptance required.** Current code supports server-backed conditions, URL restoration, page reset and compact pagination. Two historical expectations require explicit distinction:

1. Historical **two-character search threshold** is absent from the inspected current frontend.
2. Historical **automatic upper-page correction** has become an **explicit last-page action**, consistent with the archived MOS-910 owner’s design and tests.

Neither difference authorizes a correction or product-policy choice. MOS-708 retains ownership of its exact historical search/filter/pagination assertions. MOS-910 independently owns later server integration, envelope mapping, labels and statistics; this report does not claim its coverage or completion.

No files were written. This Markdown is supplied for runtime persistence at the assigned output path.

## Sources and prior evidence

Here, `A` means `openspec/changes/reconcile-control-center-backlog/audit`.

### Exact source

`A/sources/jira-surface-details-d095/r1/content.json#/items/1`:

- `/key`: `MOS-708`.
- `/description`: implement search, filters and pagination according to an attached example.
- `/status`: `CLOSED`; `/updated`: `2026-10-09T15:05:07.714+0800`.
- `/retrievedAt`: `2026-10-20T16:56:26.245Z`, distinct from packet cutoff `2026-10-20T16:56:26.589Z`.
- `/comments/items/1`: comment **1112691**, updated `2026-09-18T20:46:59.546+0800`. Claims URL persistence, search after two characters, reset on filtering/sorting, compact pagination and automatic nearest-page correction. Its ten checks include case/edge-space handling, combined conditions, reload persistence and automatic correction of `page=999`.
- `/comments/items/2`: comment **1118144**, updated `2026-09-28T21:30:46.776+0800`, attributes successful testing to the named contour **on mocks**.
- `/comments/items/0`: estimate only.
- `/attachments/0`: attachment **818853**, `image-2026-09-07-17-25-54-024.png`, 101972 bytes. Metadata only; image body unavailable.
- Three comments returned, matching `/comments/total`.

The adjacent `/items/5/description` identifies MOS-910’s later server-filter ownership; it is used only to distinguish seams, not to complete that member.

### Prior reports, review and decisions consulted before implementation inspection

- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md` and `A/reviews/R-SURFACE-CONFIG.md`: publication is not deployment or configurator activation.
- `A/decisions.md`, D-090–D-094: exact-member ownership, pending-only candidates, historical/mock evidence limitations and no checkbox closure.
- `A/publication/DRAFT-SURFACE-D091.md`, inspected through its proposed implementation tasks: existing catalog-text/domain-reflection candidates are unrelated and are not repeated here.

Registration geometry, catalog presentation, domain reflection, configurator and sandbox/lifecycle findings remain with their existing owners.

## Specification availability and interruption

The attempted read of `openspec/specs/surface-registry/spec.md` returned **ENOENT**. Listing `openspec/specs/` confirmed that capability directory is absent.

Inspection paused for supervisor direction. The supervisor independently confirmed the absence and authorized continued bounded discovery: the guessed main-spec path is not a mandatory existing input; archived artifacts may be read as **historical decisions, not substituted as current normative authority**.

Read completely:

`openspec/changes/archive/2026-09-28-surface-registry/`:

- `proposal.md`: describes MOS-910 following baseline MOS-707/708, preserving server conditions and URL.
- `design.md`, Decisions 1 and 5: preserve explicit out-of-range recovery; do not restore local prototype filtering.
- `specs/surface-registry/spec.md`: **Persistent query state**, **Server-backed registry**, and **Loading empty and error states / Out of range page**.
- `tasks.md`: historical checked/unchecked tasks, not execution evidence for this audit.

Existing current main-spec locator:

`openspec/specs/control-center-api-integration/spec.md`, scenarios **Surface filter and sorting** and **Legacy URL parameters**: canonical server values and normalization without hidden local filtering.

**Unknown:** why the archived registry capability lacks a current main counterpart; no sync, deletion history or normative completeness is inferred.

## Expected / observed / unknown matrix

All observations below are static inspection; tests were read, not executed.

| Seam | Historical expectation | Observed current implementation and test locators | Qualification |
|---|---|---|---|
| Search threshold | One character does not filter; two or more starts search | `app/features/surface-registry-filter/ui/surface-registry-filters.tsx`, `SurfaceRegistryFilters`: 300 ms debounce, no minimum length. `model/registry-search-params.ts`, `parseSurfaceRegistrySearchParams`: any nonempty query retained. `app/entities/surface/api/surface-registry-client.ts`, `getSurfaceRegistry`: forwards query. | Frontend threshold is absent. Whether real backend ignores one character is unknown. Inspected component tests do not assert the historical one-character case. |
| Search text semantics | Name/domain/owner matching, case-insensitivity, edge spaces | `app/widgets/surfaces-registry/ui/surfaces-registry.test.tsx`, **searches through the server-backed query** checks `zakupki`. Its `createRegistryResponse` trims and lowercases query and searchable fields. Frontend parser does not trim/lowercase. | Test helper demonstrates mock semantics, not production matching. No claim of real case/space parity. |
| Status/type combinations | Filter individually and combine with search | Filter handlers call `withSurfaceRegistrySearchParams`; selects use canonical entity values. Widget tests **uses canonical status and surface type values**, **offers the contract statuses in the filter**. | Current choices and serialization are inspectable; exhaustive real combinations are unverified. |
| Reset pagination | Changing search, filter or sort returns to page one | `withSurfaceRegistrySearchParams` clears `page` when query/status/type/sort changes unless caller explicitly supplies a page. Filter and sort handlers use it without a page override. Model test **resets page for a changed filter unless an explicit page is supplied**; widget test **resets pagination after changing a filter**. | Code covers all four update keys; inspected component assertions directly exercise filter reset, not every permutation. |
| URL persistence | Search/filter/sort/page survive reload | Widget uses React Router `useSearchParams`; model parses all five fields. Tests **restores all registry conditions from a direct URL and browser history**, **syncs the search field when the URL changes externally**. | Direct URL/history are asserted in a memory router. Actual browser reload was not performed. |
| Invalid lower/noninteger page | Invalid page corrected | `getPositiveInteger` defaults invalid/nonpositive values to 1; normalization deletes page resolving to 1, and widget replaces normalized URL. Model tests cover `0`, `-1`, `text`, `1.5`. | This is syntactic/default normalization, not upper-bound correction. |
| Upper out-of-range page | `page=999` automatically becomes last available page, no empty state | Widget displays out-of-range empty state and invokes `handleSurfacesRegistryLastPage` only on user action. Test **leaves an out-of-range offset empty and offers an explicit jump to the last page** expects `?page=999` until click, then `?page=2`. | Explicit historical divergence, supported by archived design and delta. Not automatically a regression. |
| Compact pagination | Ellipses for large registries | `app/features/surface-registry-pagination/model/get-pagination-items.ts` implements small/start/middle/end windows. UI computes pages from server total and limit. Component test **renders a limited page window for a large registry** checks page 20 of 42, adjacent pages, endpoints and two ellipses. | Helper clamps its display window; it does not correct registry URL/request. |
| Twenty mock rows/two pages | Historical fixture expectation | Widget test **navigates between API pages** uses 20 seed-derived records and checks different ten-row pages. | Fixture cardinality is not a production requirement or deployment observation. |

## API boundary

Current local contract:

`docs/api/contracts/surfaces.openapi.json#/paths/~1api~1control~1api~1surfaces~1v1~1surfaces/get`

Exact parameter pointers:

- `/parameters/0`: optional nullable string `query`; no `minLength` or matching/normalization description.
- `/parameters/1` and `/parameters/2`: `status` and `type`.
- `/parameters/3`: `sort`, default `name`.
- `/parameters/4`: `limit`, minimum 1, maximum 100, default 20.
- `/parameters/5`: `offset`, minimum 0, default 0.

`getSurfaceRegistry` explicitly sends UI page size 10 and `(page - 1) * pageSize`. `useSurfacesRegistryQuery` keys the request by its conditions and passes cancellation signal.

These locators explain why current frontend conditions become server requests. Full envelope, response compatibility and statistics analysis remains MOS-910’s exact ownership. The contract inspected here does not resolve historical search matching or two-character policy.

## Bounded publication candidates — queue only

| Disposition | Candidate | Boundary |
|---|---|---|
| **Keep** | Existing URL restoration, canonical filters, reset and compact pagination evidence. | No replacement pagination mechanism or duplicate MOS-910 plan. |
| **Update evidence** | Annotate MOS-708’s automatic upper-page correction as historical; current implementation intentionally exposes explicit recovery in archived owner artifacts. | Preserve original comment/status and archived history. No automatic policy reversal. |
| **Question** | Does the historical two-character threshold remain intended under server-backed search? What are authoritative case/space/matching semantics? | Frontend difference is established; desired product behavior and backend behavior are not. No implementation candidate until ownership resolves intent. |
| **Question** | Clarify ownership of the absent current `surface-registry` main capability. | No main-spec creation/sync, archive repair or assumed loss history. |
| **Conditional test candidate** | After policy clarification, add unit/component assertions for single-character versus two-character search and search/sort reset from later pages. | Test strengthening is not proof of a defect or an authorized task. No browser/E2E proposed as an implicit requirement. |

No independent new product change is recommended from this row alone. Parent alone decides acceptance, coverage transition and queue integration.

## Input fingerprints

SHA-256 computed locally over exact file bytes. Prefixes: `R = openspec/changes/archive/2026-09-28-surface-registry`; `F = app/features/surface-registry-filter`; `P = app/features/surface-registry-pagination`; `W = app/widgets/surfaces-registry/ui`.

| Input | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| Same directory `metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `R/proposal.md` | `9785022b4382ac10469754fc49799021684e5ff7956b23fe6a543540dd10a8de` |
| `R/design.md` | `2968bf34ebd61cc2d861b129e080512843f0718b08ba796ab3049dc714644681` |
| `R/tasks.md` | `a1ad5429920f771dc04d8a8ff218fed59f9ff7dbda244a242f22aa3a3a69d6b2` |
| `R/specs/surface-registry/spec.md` | `7895c5b5e6e66f066138b541eb16b3a1dde760c591f92e3c82f2d919dd1bccdf` |
| `openspec/specs/control-center-api-integration/spec.md` | `697c9c5fcb5e55e361662f93785ce5c2eb55ea8efd4992d18825c36b0107db09` |
| `docs/api/contracts/surfaces.openapi.json` | `9d8ef7ff68e187cebb051e6ee85a9ad333f0af903537a5e181425694c48d9758` |
| `F/model/registry-search-params.ts` | `265318604d7244312ff78c752f6eef4cc174c098deab34764d73142783ed9fce` |
| `F/model/registry-search-params.test.ts` | `7fa0e55072a08957bc628d080efc51b4b40f4aaa1399f85f2bd09da2aaa03671` |
| `F/ui/surface-registry-filters.tsx` | `14aac51821e13aa4b168d70c139585ecf02b24b9f47bc76b0d84dca61a50b267` |
| `P/ui/surface-registry-pagination.tsx` | `f8c3b5f809445fde6f94ea80781c270d89ad6dd32672005a5237db8fb4c40405` |
| `P/ui/surface-registry-pagination.test.tsx` | `a0fe944f6e79ce37d2ea443eff90c751059cb646874901371418a6e26e4a9d21` |
| `W/surfaces-registry.tsx` | `56f3348b48ee5e0cbaf85c6533389649935f4775642826d2abb065f4cf56b779` |
| `W/surfaces-registry.test.tsx` | `dc780c80f7f731076e667d57174313d1d1242222c655e8a36d4c3ba52865015e` |
| `app/entities/surface/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |

## Limitations

- Historical CLOSED and mock-test comments are attributed evidence, not present execution proof.
- Attachment body unavailable: screenshot fidelity and historical geometry unknown.
- No network, linked issue/MR traversal, browser, business API, tests, build, configuration changes or git mutations.
- Production matching, deployed version, persistence and browser reload behavior were not observed.
- Current main registry capability is absent; archived delta is not presented as synced current authority.
- Source packet hash matches its metadata. Other publication freshness gates are not cleared.
- No assertion about pre-existing staged files or independently verified HEAD.