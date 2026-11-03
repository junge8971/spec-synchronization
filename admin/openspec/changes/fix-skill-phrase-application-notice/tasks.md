## 1. Phrase application disclosure

- [ ] 1.1 Add the persistent application-version/retraining-data-unavailable notice to the phrase section without changing save, permission, validation, or error flows; verify it is accessible in both viewing and editing states and contains no inferred training state or timeline.
- [ ] 1.2 Extend detail component assertions for a published skill's confirmed PUT: verify the confirmed saved version and groups coexist with the notice, and no active-version or training-start/completion claim appears.
- [ ] 1.3 Extend failed-follow-up-GET assertions: verify confirmed groups/version and notice remain visible alongside the separate refresh error, without reclassifying the PUT as failed or triggering another write.

## 2. Bounded regression verification

- [ ] 2.1 After separate implementation authorization, run the targeted phrase/detail component assertions and existing save/cancel/error/metadata regressions; record results and verify the diff adds no model indicator, readiness display, MOS1018 preflight, new API/dependency, or permission behavior. Do not run browser/E2E checks without separate permission; mock results do not establish deployed application or retraining behavior.
