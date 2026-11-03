## 1. Action-specific success feedback

- [x] 1.1 Replace the generic status success title at the existing confirmed-success point in `use-dictionary-editor-handlers.ts`, distinguishing draft activation, pause and resumption from the captured pre-request state; verify component tests render the three specified titles through the real notification provider, without a new dialog or duplicate inline success.
- [x] 1.2 Extend lifecycle component coverage for pending, rejected, unknown and mismatched UUID/status responses; verify no lifecycle-success toast precedes confirmation or appears on failure, and repeat clicks retain the existing single-request lock.
- [x] 1.3 Extend existing dirty-edit and stale-context regression coverage: verify Save/Discard continuation, Stay and failed Save, old session/card completions, and rerender/refetch do not produce premature or replayed lifecycle success; retain deletion confirmation and system/unknown-status restrictions.

## 2. Verification and delivery

- [x] 2.1 Run `yarn typecheck`, `yarn lint`, `yarn test` and `yarn format:check`; record results and any unrelated failures, and review the final diff for changes outside dictionary feedback and its tests.
  - Passed: `yarn typecheck`, `yarn lint`, `yarn test` (2482 Vitest and 334 Node tests), and Prettier check for the changed files. The initial test attempt failed due to a worktree dependency symlink and a parallel-run timeout; after installing an independent copy of dependencies and rerunning, the full suite passed.
  - `yarn format:check` failed on 529 pre-existing files in `openspec/changes/reconcile-control-center-backlog/audit/`; no changed application files or MOS-1709 artifacts were reported.
- [x] 2.2 Obtain separate explicit permission for local browser checks under AGENTS.md, then use Playwright MCP with local mocks to check all three visible success titles, a failed transition, dirty cancellation and keyboard operation/dismissal without focus theft; record results or authorization/tool/app blockers, leaving verification incomplete if blocked. Do not create/edit/run automated E2E suites or use external UI environments; mocked checks do not establish deployed integration acceptance.
  - With explicit permission, checked the isolated local worktree using UI port 5189 and mock API port 30219: activation, pause and resume each displayed the expected success toast and status; keyboard Enter triggered pause/resume, F6/Tab/Enter dismissed the resume toast without the toast stealing focus or closing the card.
  - Dirty status action showed Save/Discard/Stay; Stay retained the draft and sent no PUT. A selected mock HTTP 403 on status PUT displayed the error, retained active status and showed no success toast.
  - Closed only the test tab and stopped only the isolated server; no external UI or automated E2E suite was used. This mock verification does not prove deployed integration.
