## Context

See proposal.md for motivation. Accepted `JOIN-SKILL-PHRASES.md` and `R-SKILL-REMAINING-SEVEN.md` identify this narrow MOS945 correction. Direct inspection of the complete phrase editor confirms save/error/version-mismatch messages but no application-unavailable disclosure. Existing detail tests at lines 696–789 cover confirmed PUT and failed follow-up GET, not this disclosure. These are static observations, not executed tests.

## Goals / Non-Goals

**Goals:** Resolve notice placement and save/read-error interpretation without introducing new state semantics.

**Non-Goals:** Actual applied-model version, training progress/start/completion, timelines, new API fields or requests, MOS1018 preflight, persisted readiness display, wizard changes, authentication or permission changes. Full application indicator remains deferred until an agreed model and semantics are separately approved.

## Decisions

- Render a persistent explanatory paragraph within the existing phrase section, outside its view/edit branch. Use existing typography/accessibility patterns rather than a transient toast or a checks-tab-only disclaimer, so the information remains available while editing and after a save.
- Keep the existing API-confirmed saved-version source and save/recovery flow. The notice explains unavailable data; it does not derive state from skill status, version changes, readiness checks, or GET success/failure. Retain separate save confirmation and refresh-error messages. A read failure cannot turn a confirmed PUT into a failed save.
- Extend existing detail component assertions with an explicitly published-skill fixture, notice presence in both modes, confirmed version after save, and confirmed groups/version plus notice after follow-up GET failure. Assert no active-version or training-start/completion claim. Do not replace save-protocol, metadata, cancel, dirty-input, or failure regressions.

## Risks / Trade-offs

- Static text can be mistaken for a dynamic training indicator → explicitly name unavailable applied-version and retraining data; no status badge or inferred state.
- Refresh errors can obscure save confirmation → assert both the retained confirmed snapshot and independent refresh error alongside the notice.
- Mock assertions cannot certify deployed training behavior → retain the deferred contract gate and make no runtime acceptance claim.

## Migration Plan

No data/API migration. After review and separate implementation authorization, deliver the bounded UI/assertion change through the existing release process. Rollback is a UI-only revert; no data rollback or command replay. Preserve current security, validation, permissions, and accessibility. Browser/E2E testing requires separate permission.
