# A/B integration verification

## Shared selection-chip pass (current)

User-approved shared presentational `SelectionChips` group + `SelectionChip` item
now serve KB skills and A/B surfaces. Domain fetching, RHF, limits and pagination
remain owner-local. A/B search and split selected badges/checkboxes are removed;
20-item catalog pagination and removable off-page selected IDs with name retry
remain. Retry buttons are siblings, never nested inside chips. Both removal
guides retain shared UI for the surviving consumer. The older presentation pass
below is historical, including its former surface search/checkbox description.

Gates passed (exit 0):

- Focused shared + KB/A/B editor component tests: 3 files, 75 tests;
  `/tmp/chips-focused-3.log`.
- `yarn typecheck`: `/tmp/chips-typecheck-final.log`.
- `yarn lint`: zero warnings; `/tmp/chips-lint-final.log`.
- `yarn format:check`: `/tmp/chips-format-check.log`.
- `yarn test`: 160 Vitest files / 1523 tests plus 154 Node tests;
  `/tmp/chips-full-test.log`, actual exit 0, 900-second allowance.
- `node scripts/ab-testing-verify.mjs`: `/tmp/chips-ab-production.log`.
- Then `node scripts/knowledge-base-verify.mjs`: `/tmp/chips-kb-production.log`.
  Both run ordinary production builds and verify isolation; sequential builds.
- `git diff --check` passed; `git diff --cached --name-only` empty.

Initial focused failure (`/tmp/chips-focused-1.log`) was a test assumption that
Base UI Tooltip exposes role=tooltip. It renders visible tooltip content without
that role; changed the assertion to visible ID text, consistent with existing KB
tests. Reruns pass without weakening keyboard/pressed/ID assertions.

No browser/E2E, real backend or API/schema checks run. No contract changed. Builds
emit the existing large-chunk warning; lint has no warnings. Independent review is
still required; this is implementation evidence, not final acceptance.

## Image-reference alignment verification (current presentation pass)

All five supplied PNGs were read directly. The approved composition mapping is in
`design.md`, under “Approved image-reference presentation alignment”. This pass
changes only A/B presentation/components, two component test files and these local
documents; prior saved-filter/null-default and accessibility fixes remain intact.

- Registry export/create now share the compact header; search/filter controls share
  one primary toolbar. Existing bordered table and pagination remain. Saved filters,
  reset and copy move below results into a native disclosure.
- Editor actions align right at desktop widths; metadata and four line tabs retain
  wrapping. Server comparison/recovery is collapsed by default; mutation feedback
  remains outside the disclosure.
- Group editor and preview are equal desktop columns, stacked on smaller widths.
  Compact cards have shared color cues, name/reorder/delete, percent/unit/tag and
  total feedback. Preview uses an inset contrasting semantic primary panel,
  chart-token segments, percent labels and complete wrapping legend/codes.
- Surfaces retain real pagination/search, ID resolution/retry and limits, with
  selected chips and keyboard-focusable compact checkbox pills. No static catalog.
- Rules retain all fields/toggles, with an ordered configuration explanation at
  right. No execution claims, status remapping, DTO/auth/mock/API or theme changes.

Current gates (exit 0):

- Focused `yarn vitest run app/optional/ab-testing/ui`: 8 files / 78 tests;
  `/tmp/ab-alignment-focused.log`. Added header/disclosure recovery assertions;
  updated percent-label tests without dropping width, zero-group, threshold or
  overflow coverage; added equal-column/inset/tabs/ordered-summary assertions.
- `yarn typecheck`: `/tmp/ab-alignment-typecheck.log`.
- `yarn lint`: zero warnings, `/tmp/ab-alignment-lint.log`.
- `yarn format:check`: all matched files formatted, `/tmp/ab-alignment-format.log`.
- `git diff --check` and `git diff --cached --name-only`: clean whitespace and
  empty index. Pre-existing tracked/untracked work preserved; no staging/commit.
- `yarn test`: 159 Vitest files / 1516 tests and 154 Node tests, all passed;
  `/tmp/ab-alignment-test.log`. 900-second allowance; exit status preserved.
- `env -u CONTROL_API_MOCKS node scripts/ab-testing-verify.mjs`: invokes normal
  production `yarn build`, verifies routes/manifest/output graph and no fixtures;
  `/tmp/ab-alignment-build.log`.

Earlier failures, resolved: focused test expected the former name+percent segment
text (updated to percent-only label plus accessible segment name); lint and the
Node lint gate flagged RulesSummary complexity 12 (resolved using a typed watched
surface collection without redundant optional fallbacks, no rule changes). Full
suite rerun after the fix passed.

Limits: no browser/E2E operation, measured screenshot comparison, real backend or
filesystem-download verification. Neutral chart/primary tokens intentionally differ
from prototype red/green. Exact pixel spacing, font metrics and breakpoint rendering
remain unmeasured. API check is not rerun because no contract files changed; prior
API evidence below is historical. Independent review is required; not archived.

## Historical revalidation after review fixes

The contracts review blocked acceptance on P1 saved-filter interoperability; the
design review identified four P2 presentation/accessibility findings. Both reports
under `outputs/317f3763-0d2c-43c8-8140-15477a778396/reviews/` were read alongside the
fix owners' `saved-filter-complete.md` and `editor-complete.md` handoffs. The fixes
were inspected, not rewritten by this validation stage. Independent reviewer
confirmation of their resolution remains separate from these executed gates.

### Findings and regression evidence

- **P1 saved-filter round trip:** `validatePersistedRegistrySearch` drops only the
  three documented scalar defaults `metric_code`, `audience_code`, `launch_mode`
  when exactly null, then calls the unchanged strict validator. Saved-filter Apply
  uses that boundary. Unknown keys (including null) and unsupported non-null values
  still reject atomically; ordinary URL/request validation is unchanged. Seven new
  saved-filter component cases cover Apply/rejection. The new
  `mocks/ab-testing/saved-filter-interoperability.test.mjs` executes actual Express
  POST → list/detail → real frontend codec → URL roundtrip → search, including
  default and AND/OR selections, response immutability and non-null rejection.
  It is discovered by the existing nested test glob without new dependencies or
  configuration, and passed in the full suite below.
- **P2 distribution widths:** group and remainder segments share nonshrinking,
  min-width-zero/clipping classes; small remainder text is outside the bar and
  internal labels start at 12%. Regression covers 49/50/1 and the 12% boundary.
- **P2 toggle errors:** nearby alert, stable error ID, aria-invalid and
  aria-describedby expose a rejected log_group PUT; regression verifies Rules tab,
  focus, preserved false draft and no replay.
- **P2 long metadata:** code/owner/date spans wrap arbitrary long values; regression
  covers valid unbroken 100-character values. This is class-level component proof,
  not browser layout measurement.
- **P2 date display:** Russian date-only formatting explicitly uses UTC, with ISO
  datetime/input values preserved. The current full suite covers the regression;
  the fix owner's separate America/Los_Angeles focused run is historical additional
  evidence and was not rerun here.

### Current commands (all exit code 0)

- `yarn typecheck` — `/tmp/ab-final-typecheck.log`.
- `yarn lint` — zero warnings; `/tmp/ab-final-lint.log`.
- `yarn test` — **159 Vitest files / 1514 tests; 154 Node tests**, zero failures;
  `/tmp/ab-final-tests.log`. Both phases completed, including the new HTTP/frontend
  test. The command had a 900-second allowance and its exit status was saved before
  printing log excerpts. This supersedes the earlier 1504/153 totals below.
- `yarn format:check` — `/tmp/ab-final-format.log`.
- `yarn api:check` — `/tmp/ab-final-api.log`; generated DTO remains unchanged.
- `env -u CONTROL_API_MOCKS node scripts/ab-testing-verify.mjs` — normal production
  `yarn build`, exact three routes, basename/manifest and graph;
  `/tmp/ab-final-build.log`.
- `CONTROL_API_MOCKS=true node scripts/ab-testing-verify.mjs` — same production
  isolation checks; `/tmp/ab-final-build-mocks.log`.
- `node scripts/knowledge-base-verify.mjs` — existing KB build gate retained;
  `/tmp/ab-final-kb.log`.
- Explicit assertions over both saved emitted graphs confirm the new
  `saved-filter-interoperability.test.mjs` and all mock/test modules are absent;
  graphs retained as `/tmp/ab-final-{normal,mocks}-graph.json`.
- `openspec validate add-optional-ab-testing --strict` — valid;
  `/tmp/ab-final-openspec.log`.
- `git diff --check`, `git diff --cached --quiet` — clean whitespace, empty index.
  Actual tracked diff and complete untracked inventory inspected, including fixes
  and the new server test. No component fixes, wiring, dependency/auth/API scope or
  generated DTO changes were made by this stage. No current-run failed gate.

### Removal evidence reuse and task status

The removal guide remains accurate: both fixed frontend code and the new HTTP test
live inside the two deleted A/B directories. No import/registration/script/glob or
lint exception was added by the fixes. Current registry, Vite, mock registrations,
package test glob, lint-gate assertion and architectural module list were transformed
according to the guide and compared byte-for-byte with the earlier validated
`/tmp/ab-removal-vJfzJk` copy; they match. The retained KB route test and generated
schema also match. Therefore removal typegen/build/architecture/core-KB gates were
**not rerun**; their successful execution below is reused, not presented as a new
run. No main-checkout removal occurred and no backend/server data was touched.

Task 7.4 was left unchecked by the fix owners and is checked again only after all
current gates above passed. Other 32 task marks were preserved; no unchecked
omissions remain. This stage changes only tasks.md and this report. Browser/E2E,
real backend and actual filesystem delivery remain untested/prohibited as stated
below. Recommended next step: independent review of resolved findings and final
acceptance, not additional feature scope.

## Historical initial integration evidence

The initial integration stage completed tasks 1.2–1.3 and 7.1–7.4 only. Earlier owners' checked
1.1, 2.1–2.4, 3.1–3.7, 4.1–4.4, 5.1–5.8 and 6.1–6.3 remain intact. Their handoffs
were checked against source test names and the final full-suite execution; no
unchecked implementation item is being silently deferred. Independent review is
still required; this report is not reviewer acceptance.

## Spec / task evidence

| Capability / tasks       | Executed evidence and limits                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Module: 1.1–1.3, 7.1–7.2 | scripts/eslint-fsd-config.test.mjs covers public API/layers, both optional directions and structural rules. application/model/ab-testing-config.test.ts covers default registration in both modes, base preservation, three unique paths, static new, basename, navigation and descriptor-only imports. application/ui/ab-testing-host.test.tsx covers real shell/session/access with an isolated business probe: no mounting before session/wildcard access, active menu, breadcrumbs, all tab links/unknown fallback, new without ID and draft continuity during session checking. Actual editor deep-link/unknown fallback tests remain in editor.test.tsx. No host auth changes. Build verifiers and temporary removal below cover default production and independent deletion. |
| Registry: 4.1–4.4        | model/registry-search.test.ts, ui/registry/*.test.tsx and api/ab-testing-saved-filter-client.test.ts cover AND/OR URL roundtrip, invalid atomic rejection, short query, server total/sort/pagination, metadata operators, 50/51 limits, unsupported conditions, applied/draft separation, paginated surface and saved-filter selection, duplicate names, clipboard/delete failures.                                                                                                                                                                                                                                                                                                                                                                                                 |
| Editor: 2.1–2.4, 5.1–5.8 | api/ab-testing-client.test.ts, api/ab-testing-users-client.test.ts, model/ab-testing-{form,errors,queries,mutations}.test.ts and ui/editor/editor.test.tsx cover runtime contract, nullable defaults/reference handling, IDs/reorder/100 limits, integer sums/preview/legend, paginated external references, hidden-tab focus, POST→GET recovery, PUT diff, pending/409/422/invalid/uncertain outcomes, saved-snapshot tags, status-only commands, leave/stay/beforeunload and owner safety. Pathname blockers are editor-owned; shell tests isolate access and navigation, not a browser end-to-end flow.                                                                                                                                                                          |
| Export: 6.1–6.3          | api/ab-testing-export-client.test.ts, ui/export/ab-testing-export.test.tsx and ab-testing-export-integration.test.tsx cover default registry/editor export seams, complete applied search, ordered metadata columns, limit failures, saved ID only, dirty/new states, flat summaries, pending/download failure and old-owner suppression. Delivery means passing an attachment to the browser API, not confirming a filesystem save.                                                                                                                                                                                                                                                                                                                                                |
| Mocks: 3.1–3.7           | mocks/ab-testing/{aggregate,search-export}.test.mjs plus existing contract, managed and KB HTTP tests cover all eight published operations, chained catalogs, full-aggregate validation and rejection without mutation, IDs/replacement, search-before-pagination, CSV/full selection, saved searches, no-credentials behavior and seed reset. Local Express is not evidence of real backend fidelity.                                                                                                                                                                                                                                                                                                                                                                              |

All these tests ran as part of final `yarn test`: **159 Vitest files / 1504 tests;
153 Node tests; zero failures/cancellations/skips in the Node phase**. Command exit
status was captured directly, with a 900-second allowance, not hidden by `tail`.

## Prototype/API matrix reconciliation

- archived remains visibly unavailable; disabled retains its API meaning, no DELETE UI.
- `return_to_control`, `surface_ids`, array order and saved group IDs follow DTO;
  no prototype-only sort_order/sections/nested payloads.
- Numeric/group-count/priority/surface conditions remain unsupported rather than
  locally filtering a page or changing OR semantics.
- Percentages are integers and total 100 for persistence; 20/20 previews retain
  60 remainder, invalid totals are not normalized; 0% is named in the legend.
- min_sample_size is null or positive int32, not prototype zero. Prototype defaults
  are explicit only when lookup codes are available. Unknown/inactive saved values
  and nullable controls are not silently replaced.
- scheduled uses started_on, not an invented scheduled timestamp; responsible ID
  is external business data, not session principal.
- CSV groups are flat text summaries with saved state; no nested table/export draft.
- Success follows confirmed API response/delivery. Settings and status commands do
  not claim execution, traffic allocation, scheduling, metrics, control assignment
  or auto-stop. No execution engine, timers or new auth/API/dependencies were added.

## Commands and actual results

PASS final:

- `yarn typecheck` — typegen and tsc; `/tmp/ab-integration-typecheck.log`.
- `yarn lint` — zero warnings; `/tmp/ab-integration-lint.log`.
- `yarn test` — full results above; `/tmp/ab-integration-tests.log`.
- `yarn format:check` — all matched files; `/tmp/ab-integration-format.log`.
- `yarn api:check` — generated DTO unchanged; `/tmp/ab-integration-api.log`.
- `node scripts/ab-testing-verify.mjs` — invokes `yarn build`, exact three routes,
  basename/browser manifest, emitted chunk graph, no mock/test/fixtures;
  `/tmp/ab-integration-build.log`.
- `CONTROL_API_MOCKS=true node scripts/ab-testing-verify.mjs` — same production
  checks with dev mock setting true; `/tmp/ab-integration-build-mocks.log`.
- `node scripts/knowledge-base-verify.mjs` — unchanged KB gate passes;
  `/tmp/ab-integration-kb.log`.
- `openspec validate add-optional-ab-testing --strict` — valid;
  `/tmp/ab-integration-openspec.log`.
- `git diff --check`, `git diff --cached --name-only` — clean whitespace, empty index.
  Tracked diff and untracked source inventory inspected; AGENTS/OpenSpec are locally
  ignored. No commits/staging, generated DTO edits or browser/E2E operations.

Earlier failed attempts (fixed, not concealed): the new descriptor-source test used
import.meta.url under jsdom and resolved to `/app`; replaced with project-relative
file reading, then full suite passed. First temporary-copy typecheck lacked the
local Yarn release because .yarn was excluded; copied .yarn and reran successfully.

## Temporary removal

Copy: `/tmp/ab-removal-vJfzJk` (path also saved in `/tmp/ab-removal-path`). Copied the
working tree including untracked additions, with node_modules symlinked; no source
removal in the main checkout. Applied the exact integration guide disconnects:
registry, Vite plugin, dedicated tests/scripts, mock registrations/glob, A/B-only
architecture fixtures/exception. AGENTS is policy documentation, not build input;
its owner-managed exception update is documented rather than deleting shared policy.

PASS in copy:

- `yarn typecheck` — `/tmp/ab-removal-typecheck.log`.
- `yarn build` — `/tmp/ab-removal-build.log`.
- `node --test scripts/eslint-fsd-config.test.mjs` — KB architecture retained;
  `/tmp/ab-removal-architecture.log`.
- `yarn vitest run app/routes.test.ts app/application/model/knowledge-base-config.test.ts app/application/ui/knowledge-base-host.test.tsx` — 3 files / 20 tests;
  `/tmp/ab-removal-tests.log`.
- `node scripts/knowledge-base-verify.mjs` — KB production retained;
  `/tmp/ab-removal-kb.log`.
- `yarn exec react-router routes --json` plus assertions — A/B absent, three KB
  routes present; `/tmp/ab-removal-routes.json`.
- Directory comparisons: KB business code, core pages/entities unchanged; generated
  schema byte-identical. Generic managed model/contracts/data were retained.

NOT RUN: browser/E2E (prohibited), real backend, real browser filesystem delivery,
full project suite in the removal copy (targeted removal gates above were run).
No outstanding implementation blocker identified. Server authorization and runtime
backend behavior remain deployment validation, not claims made from mocks.
