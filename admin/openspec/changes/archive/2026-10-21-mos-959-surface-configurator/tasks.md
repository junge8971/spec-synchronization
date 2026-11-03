## 1. Configuration contract and local transport

- [x] 1.1 Align configuration request bounds, add the published `link` member to `SurfaceCardActionType`, and align relevant descriptions in `docs/api/contracts/openapi.json` and its `surfaces.openapi.json` mirror, with exact-delta provenance tests preserving raw snapshots/hashes (approved during apply), using the saved r2 evidence in design.md; regenerate through `yarn api:generate` and verify `yarn api:check`, preserving operation/security normalization and creation omission/null behavior.
- [x] 1.2 Extend `app/entities/surface/api/surface-registry-client.test.ts` around the existing configuration client/mutation: verify seven-field full replacement, no enabled_skills/card IDs, parsed response and field errors; retain separate skills transport coverage.
- [x] 1.3 Align the configuration handler in `mocks/surfaces.mjs` and add `mocks/surfaces.test.mjs` save/readback tests for bounds, conditional fallback, action formats, unchanged timestamp/token/code, no synthetic status transition and preserved state on rejection; verify credential-free operation without role enforcement and retain existing creation tests.

## 2. Editor and local preview

- [x] 2.1 Add `app/features/surface-configurator/` with a public controller/editor API and owned types/constants/handlers; verify unit tests for GET initialization, dirty equality including equal-count edits/reversion, tab preservation, owner/surface separation and server normalization without overwriting another dirty draft.
- [x] 2.2 Implement labelled appearance/greeting/fallback/suggestion/card controls and validation with existing form/UI tools; component tests must cover arbitrary #RRGGBB versus invalid formats, token insertion, required whitespace, conditional fallback, five/four caps, empty lists, action bounds, saved accent preservation and exact empty-state/hint text.
- [x] 2.3 Implement Greeting/Dialog and separate fallback local previews using explicit demonstration substitutions; verify component tests for unsaved styling/content, text escaping and zero preview requests/navigation/message/skill execution, including malicious text and link values.

## 3. Explicit save and card integration

- [x] 3.1 Replace the configurator placeholder and default scenarios tab in `app/widgets/surface-details/ui/surface-details/surface-details-content.tsx`; reuse existing session presentation policy without new grants and verify default tab, read-only archived/viewer behavior, keyboard labels and unchanged history/sandbox placeholders in component tests.
- [x] 3.2 Integrate explicit configuration saving with the existing mutation controller and shared operation lock in `use-surface-details-operations.ts`; verify one PUT then fresh GET, rejection preserves input, prior reads cannot confirm writes, and configuration save never writes skills or resets a dirty skills draft.
- [x] 3.3 Add confirmed-write/readback-unconfirmed recovery for configuration and existing skill save/preparation paths; request-count tests must prove GET-only retry after successful PUT, no implicit publish, preserved last-known facts, conflict manual refresh and no stale-owner result adoption.
- [x] 3.4 Add both-draft dirty and pending-readback guards to shared publication policy, both buttons and post-confirmation handlers; update checklist copy. Verify `surface-details.test.tsx` and action-policy tests cover same-count dirty changes, both entry points, restored-clean values, no configuration PUT during publication, and retained clean skills PUT → fresh GET → POST preparation with existing confirmation/status/error rules.

## 4. Regression and acceptance

- [x] 4.1 Extend existing surface component/transport/mock tests to prove registration defaults stay server-owned, draft remains draft absent server confirmation, archived writes remain blocked, no sandbox/history API calls occur, and code/token are not fabricated; verify test assertions distinguish local mock evidence from deployment behavior.
- [x] 4.2 Run `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`, `yarn api:check` and `yarn build` after implementation, recording failures rather than weakening rules; do not create/edit/run browser or E2E tests without separate explicit permission.
- [x] 4.3 Review the implementation diff against the three approved policies and complete modified requirements; verify no combined save, hidden/default configuration PUT, new permissions, navigation policy, external preview calls or unrelated contract refresh, and report source freshness/deployment limitations before requesting acceptance.

## Implementation validation

- Passed: `yarn typecheck`, `yarn lint` (zero warnings), `yarn api:check`, `yarn build`, `yarn test` (177 frontend files / 1821 tests; 217 Node tests).
- `yarn format:check` failed on 521 files outside the implementation diff; targeted Prettier checking of all changed and new implementation files passed. Unrelated files were not reformatted and no rules were relaxed.
- Diff review: separate configuration/skills writes; no configuration PUT in publication; fresh GET confirmation and GET-only recovery; unchanged permission, navigation, history and sandbox scope. Raw API snapshots/hashes are intact; exact-delta provenance tests pass.
- Source freshness remains the saved API r2 referenced in design.md, not a new live/deployment verification. Local tests do not prove deployed backend validation or widget propagation timing. No browser/E2E tests were created, edited or run.
- OpenSpec artifacts reside in this project's ignored `openspec/` tree; task tracking was updated there without force-adding ignored files.
