## 1. Authorization and integration prerequisites

- [x] 1.1 Obtain parent acceptance of this package: the user explicitly instructed implementation against the published contract, with 19 default columns, no selector and no export-limit gate. Additional backend clarifications and independent review are not prerequisites; this acceptance does not claim a completed independent review.
- [x] 1.2 Record the published operation/schema/file/error/security contract and R01–R19 reconciliation, marking R15 excluded and unverified backend properties separately. Implement the available contract without awaiting backend clarifications or inventing fields, filenames or errors. Backend acceptance evidence remains task 4.2, not an implementation prerequisite (spec: Contract-gated skill export actions).
- [x] 1.3 After 1.1–1.2, align reproducible aggregate/split/generated contracts and provenance under existing API ownership; verify offline `yarn api:check` and review preserved security normalization. This task and all tasks below are blocked by 1.1–1.2 (REQ R19; design decision 1).

## 2. Typed requests and safe file lifecycle

- [x] 2.1 Add skill export access through the entity public API and focused feature ownership using agreed operations and existing transport; verify unit tests for current normalized filter/sort mapping, omitted pagination/selected IDs/fields, `{}` defaults and saved-card identity, including unsupported URL values (spec: Whole-selection registry export; Saved-card export and default columns; REQ R03–R10).
- [x] 2.2 Implement complete server-file validation and safe filename/download handoff using compatible existing shared utilities, without reserialization; verify byte-preserving success, malformed metadata/error-body rejection, transfer failure and no partial download tests (spec: Server CSV integrity and atomic failure; REQ R12–R14; generic failure safety independent of limit policy).
- [x] 2.3 Implement pending deduplication, explicit retry, abort/stale-context suppression and Blob URL/link disposal; verify cleanup on success, failed trigger, unmount and context replacement even when abort is ignored, with no automatic replay or retained file cache; verify export remains enabled without a published numeric limit and no client cap is added (spec: Accessible and context-safe download lifecycle; design decision 5).

## 3. Registry and card composition

- [x] 3.1 Compose registry CSV outside rollout selection; verify component cases for filtered/sorted later pages with checked rows, confirmed empty selection, loading/error/placeholder state and filter changes while pending, preserving URL navigation, pagination and rollout behavior (spec: Whole-selection registry export; REQ R04/R08/R09/R17).
- [x] 3.2 Compose saved-card CSV with clear saved-data scope and default columns; verify a dirty questionnaire is neither sent nor cleared, and missing/inaccessible-card failures yield no download (spec: Saved-card export and default columns; REQ R03/R05–R07/R10/R16/R18).
- [x] 3.3 Reuse existing skill-view UI permission/session APIs without new policy; reread the approved session/mock change artifacts before integration work, and verify component tests for view-only access, denied access, pending/retry labels, keyboard operation, unavailable explanation and usable focus without hover-only messages (spec: Contract-gated skill export actions; Accessible and context-safe download lifecycle; REQ R11).

## 4. Mock and integration acceptance

- [x] 4.1 Add explicit agreed export responses to existing Express mocks without credentials/role enforcement or client fallback; verify HTTP tests for server files, header-only empty results, saved card, optional-field parity/validation and published error behavior, without inventing a mock export limit; verify production exclusion remains intact (spec: Separate frontend and backend acceptance; REQ R03/R05–R07/R16–R19).
- [ ] 4.2 Collect separate backend acceptance evidence for BOM/semicolon/header, quoting and injection safety, date/card-ID filenames, one row per skill, deleted/team/skill access restrictions, view permission and no error-body download; verify the R01–R19 matrix explicitly distinguishes backend proof, mock fixtures, unresolved deployment evidence and R15 excluded from current scope (spec: Server CSV integrity and atomic failure; Separate frontend and backend acceptance).
- [x] 4.3 After implementation, run `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`, `yarn api:check` and `yarn build`; review diff/scope and record passed/failed/not-run results, regressions and residual risks. Do not create/edit/run browser or E2E tests without separate explicit authorization, and do not mark real integration accepted from mocks (spec: Separate frontend and backend acceptance; existing project/API verification rules).

## Implementation verification — 26.10.2026

- Published contract and R01–R19 reconciliation: `docs/api/contracts/skill-export.md`. Import limited to two export operations, three new schemas and the shared SkillStatus dependency; unrelated business contracts remain pinned by regression fingerprints. Existing security AND preserved.
- Passed: `yarn typecheck`, `yarn lint` (zero warnings), `yarn api:check`, `yarn build`, `git diff --check`.
- Passed: `yarn test` — 209 Vitest files / 2250 tests and 274 Node/mock tests. Initial failures from the added contract statuses/operation counts were corrected with explicit updated expectations, without weakening unknown-status or provenance assertions. The first full run timed out at 120 seconds; the final run completed with a longer timeout.
- `yarn format:check` failed on 531 pre-existing files outside this change, predominantly `reconcile-control-center-backlog/audit`. Targeted Prettier checks for all changed/new source files and this change's artifacts pass. No unrelated reformat or ignore-rule change was made.
- Production build inspection found no `skillExportHandlers`, mock CSV convention or `createMockApp` in client JS. Existing mock-isolation tests pass.
- Task 4.2 remains open: real export files, CORS/header exposure, backend CSV safety and access enforcement were not exercised. No browser/E2E tests or business requests on A/C/T were run. Per user instruction these are separate integration evidence, not blockers for implementing the published frontend contract.
- Large-file memory use remains a risk of buffering a complete server attachment; no client limit was introduced. Diff reviewed for preserved registry pagination/selection, editor drafts, session boundaries and resource cleanup.

## Same-tick export deduplication fix — 26.10.2026

- User-authorized local Playwright MCP checks reproduced two POST requests and two download handoffs from a zero-delay double click with a 1500 ms mock response delay. React's rendered `isPending` state alone did not prevent the second activation.
- Added a synchronous hook-owned activation lock before `mutate`, released by `onSettled` on success or failure. Both registry and card share this hook; transport, session checks and abort/Blob cleanup remain unchanged.
- Added a component regression with two native clicks in one `act`: failed before the fix (two requests), passed afterward (one request/download), including a subsequent successful export. Existing error-retry and unmount-abort tests pass.
- Local Playwright MCP verification after the fix: zero-delay double click with delayed response produces one POST and one download handoff; pending button is disabled. HTTP 500 followed by an explicit double-click retry also produces one POST and one successful handoff. Mock scenarios reset afterward. This does not prove disk persistence or real backend acceptance; task 4.2 remains open.
- Passed: `yarn typecheck`, `yarn lint`, focused CSV component tests (7), separately rerun documentation-session and CSV tests (9 total), all 274 Node/mock tests, targeted Prettier and `git diff --check`.
- Full `yarn test`: 2250 passed, one unrelated failure in `app/routes/documentation-session.test.tsx` (invalid article remained `missing`); that file passed on focused rerun. Node/mock tests were then run separately because the full script stopped at Vitest.
- `yarn format:check` remains failing (532 files); both source files touched by this fix pass targeted checks. API generation/build checks were not rerun for this hook-only fix.
