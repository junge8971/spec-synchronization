## Why

[MOS-1709](https://task.mos-team.ru/browse/MOS-1709) requests popup feedback for dictionary activation, pause and resume. The user-provided screenshot of the issue discussion clarifies that this means a success notification, not a confirmation before the request; the current handler already emits the generic «Статус сохранён.» but does not identify the completed action.

## What Changes

- Show one existing nonblocking success toast with action-specific wording: «Справочник активирован», «Справочник приостановлен» or «Работа справочника возобновлена».
- Emit this feedback only after a matching dictionary/status response is confirmed; preserve errors, unknown-outcome handling and stale-context suppression.
- Keep dirty Save/Discard/Stay behavior and existing deletion confirmation; add no status-confirmation modal.
- Preserve the distinction between stored status and downstream effects. No consumer propagation guarantees are added.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `reference-dictionaries`: Explicit action-specific, confirmed-success feedback for card lifecycle transitions, using the existing `operation-feedback` conventions.

## Impact

- Narrow changes in `app/optional/reference-dictionaries/handlers/use-dictionary-editor-handlers.ts` and related lifecycle message logic/tests, principally `ui/detail/dictionary-editor.test.tsx`.
- Reuse `shared/ui/notifications`; no new dependency, transport, API, permission or data-model change.
- Unit/component verification covers all transitions, pending/error/unknown outcomes, dirty edits and stale completions. Plan local mock Playwright MCP checks for visible feedback and keyboard interaction; obtain separate explicit browser authorization under AGENTS.md before execution. No automated browser suites or external UI actions are authorized by this proposal.
- Source context: [MOS-1327](https://task.mos-team.ru/browse/MOS-1327), [Wiki section 10](https://wiki.mos-team.ru/spaces/KR/pages/247751846/Раздел+Справочники), and the user-supplied screenshot (discussion dated 2026-10-28). Wiki downstream-effect claims remain outside the agreed stored-status scope. No deployed visibility defect has been reproduced.
