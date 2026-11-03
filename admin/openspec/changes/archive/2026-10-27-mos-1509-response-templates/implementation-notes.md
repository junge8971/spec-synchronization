# Implementation notes

## Worktree

Implementation checkout: `/home/user/my/work/codesrc/projects/CAM/worktrees/tsam-admin-front/mos-1509-response-templates`, branch `feat/mos-1509-response-templates`, base `2887ffe`.
OpenSpec and ignored AGENTS.md were copied from the original checkout. Task progress is maintained in this copy; the original checkout is unchanged.

## 1.1 Contract verification

Read-only comparison against https://nchat-t-tech.mos.ru/api/control/openapi.json through Playwright MCP on 2026-10-26. No business API calls.

The 13 schemas ExternalUser, FullName, ManagedResourceSavedFilterCreate, ResponseTemplateCreate/Patch/Response, SavedFilterPatch, UserSearchResult, tpl_templateCondition/Conditions/DetailExportRequest/ExportRequest/ListQuery match the current local aggregate exactly after recursive key sorting (`localeCompare` with en, array order retained). Both canonical SHA-256 values: `b5ab0fc208075dad9da27051d44fd95598239a4d04f9fbd503a45375176f0768`.

No contract regeneration needed on this base. Scope includes the existing system-state-toggles enum value in the comparison, but adds no system-state implementation. The old CRUD Markdown saved-filter prohibition remains superseded by the published enum, as documented in the design.

Added `mocks/response-templates/contract.test.mjs` and its normal test-runner glob. Three Node contract tests passed; `yarn api:check` passed. Dependency install completed with existing peer warnings (ajv-formats vs resolver peer range); no package or lockfile changes intended.

## 1.2–2.2 Boundaries and mock ownership

Added the targeted optional boundary and corresponding worktree AGENTS rule (AGENTS is ignored by Git). All 141 architecture tests pass. Moved template descriptor, labels, catalogs, seed and validator under `mocks/response-templates/`. Shared handlers now invoke each resource validator rather than selecting template behavior as the default branch. Template HTTP tests moved into the module; shared API registry tests retain their previous assertions. Added checks for failed atomic aggregate writes, empty initial links, clearing both sets, historical links, scope independence and cross-resource saved-filter isolation.

Verification: 24 targeted contract/HTTP tests passed (including other managed-resource regressions); `yarn lint`, `yarn typecheck`, `yarn api:check`, changed-code Prettier check, `git diff --check` and strict OpenSpec validation passed.

## Pause before task 3.1

`yarn format:check` failed on 529 files, principally pre-existing copied OpenSpec audit/archive artifacts. No broad exclusions or mass reformatting applied. Full `yarn test` was separately attempted but exceeded the 200-second command timeout after printing only the Vitest start banner; no full-suite success is claimed. No Vitest process remained after timeout. Build and browser checks not run at this checkpoint; no frontend module has been implemented yet.

Progress: 4/22 tasks complete (1.1, 1.2, 2.1, 2.2). Await guidance on continuing with these full-check blockers recorded, rather than changing unrelated artifacts or weakening verification. Original checkout remains unchanged; no commit or merge performed.

## Continuation checkpoint

User authorized continuing without reformatting unrelated historical artifacts. Implemented tasks 3.1–3.3, 4.1–4.3, 5.1–5.6 and 6.1–6.2, then verified the production build graph (7.2). Registry/editor routes are now composed by default with unchanged access fallback. No new dependencies, grants or authentication transport were introduced.

Final worktree checks: typecheck, lint (zero warnings), api:check, strict OpenSpec validation, changed-source Prettier and diff whitespace check passed. Full `yarn test` passed: 2353 Vitest tests across 228 files plus 328 Node tests. `node scripts/response-templates-verify.mjs` invoked the successful production `yarn build` and confirmed all three routes and absence of mock/test modules from the client graph. Global `yarn format:check` still reports 529 files; no unrelated mass formatting or exclusions applied.

Removal rehearsal in `/tmp/mos-1509-removal.91iY24` passed typecheck/build but mock startup failed with `Missing mock handler: metadata_response_templates_api_control_api_v1_managed_resources_response_templates_metadata_get`. Shared OpenAPI remains intact and the strict all-operations registration guard remains unchanged. Task 7.1 stays open pending agreement on an explicit composition policy for intentionally removed optional sections; no general missing-handler fallback was added. Task 7.3 initially stayed open without separate browser-test permission; this was superseded by the explicit permission and smoke results below.

Acceptance and detailed registrations are tracked in `app/optional/response-templates/ACCEPTANCE.md` and `app/application/response-templates-integration.md`. Task 7.4 records performed checks and the known failures, not a claim that removal/browser acceptance passed. Work remains entirely in the requested worktree. The original checkout now contains unrelated concurrent changes; they were not edited or merged by this implementation.

## Authorized local browser smoke — 27 October 2026

User requested starting the server and checking the application in the browser. Started `yarn dev --host 127.0.0.1 --port 5173` in the worktree (log `/tmp/mos-1509-dev.log`) and exercised local Express mocks through Playwright MCP. No external business data was touched; no E2E suite or application code was added/edited during this pass.

Registry search/URL conditions, saved-filter reload/apply, access fallback, explicit creation, responsible/link selection, literal preview, archive confirmation, atomic clear, changed-only PUT, duplicate-code 409 with field focus, dirty breadcrumb navigation, native beforeunload and direct detail tabs were exercised. Full results and remaining cases are in `app/optional/response-templates/ACCEPTANCE.md`.

Both list and detail CSV return HTTP 200 but fail to download because the actual mock response lacks the mandatory `Cache-Control` header required by the shared file reader. Detail response uses saved text, not the dirty draft; list request correctly omits pagination. Also reproduced `A router only supports one blocker at a time` on tab/navigation transitions, including after a fresh direct detail load. Root cause is not established. Surface choices show repeated indistinguishable visible labels.

Task 7.3 remains incomplete for fixes/retesting and remaining scenarios, not for lack of permission. Previous passing automated checks do not certify this browser integration. Task 7.1 and its removal-policy blocker are unchanged. Screenshot evidence is in the browser tool's allowed original-checkout artifact directory `.playwright-mcp/mos-1509-browser-editor.png`; unrelated source changes there remain untouched. Server is left running for inspection.

## UI corrections and repeat verification — 27 October 2026

User requested fixing the browser findings and matching the supplied three screenshots/prototype
and neighboring sections, not inventing another visual language. Reworked the registry toolbar/table,
editor header/actions, line tabs, two-column Cards, literal Bubble preview, responsible popup and
shared selection chips. No cross-optional imports, new UI library or theme. Repeated names show
compact distinguishing ID suffixes, with full-ID fallback on collisions; full IDs remain accessible
in tooltips/accessible names. Unknown historical selections retain their full IDs.

The shared mock CSV helper now provides no-store, nosniff and UTF-8 filename headers, preserving
Express fallback/custom dispositions and avoiding duplicate filename*. Added actual HTTP-to-shared
file-reader coverage, including empty export. Both registry and detail files were downloaded by
Chrome and inspected on disk; dirty detail export contains the saved text, not the draft.

The blocker warning was reproduced in component tests and traced to React Router 8.3.1 useBlocker
registrations surviving Activity effect teardown/restoration. A reproducible Yarn patch adds a
cleanup effect keyed by router/blockerKey in development and production. Cleanup must not depend
on the changing blocker function, which would discard active blocked navigation. Existing session
boundaries and auth behavior are unchanged. Package resolutions/lockfile now install this patch;
there is no added library. Maintenance/removal notes are in the integration guide.

Repeat browser checks passed creation with validation focus, URL filters/explicit conditions,
saved-filter reload/apply, actual downloads, safe preview, atomic save from Links, archive cancellation,
Back/Stay/Leave/reverted forms, keyboard controls, 390px layout and local directory failure/retry.
No multiple-blocker warnings remain. The injected error route was removed in finally. Clipboard
readback could not obtain browser permission (extension lacks Browser.grantPermissions); later-page
association browser coverage needs more than the current 15 skills/20 surfaces. These and exhaustive
keyboard traversal remain explicit gaps in 7.3, rather than claims of complete acceptance.

Task 7.1's independent mock-removal policy remains unresolved and unchanged. Task 8 records the
requested fixes and UI correction; current check totals/logs and screenshots are in ACCEPTANCE.md.
Final rerun after compact-chip/CSV edge-case refinements passed typecheck, zero-warning lint,
2356 Vitest tests (228 files) plus 329 Node tests, build and production graph verification.
Immutable patched install, api:check, changed-source formatting, strict OpenSpec validation and
diff whitespace checks also passed. Global format:check still fails on 529 historical files.
OpenSpec apply instructions refreshed: 22/24 tasks complete, 7.1 and 7.3 remain open.
No automated E2E files, real backend writes, commit or merge. Server remains available locally.
