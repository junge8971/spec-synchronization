## 1. Typed persisted results

- [ ] 1.1 Extend skill detail types and decoder with published check fields and exact type/status enums; verify decoder assertions for all five types, four statuses, nullable message, checked_at, empty array and malformed/missing fields without synthetic success.
- [ ] 1.2 Pass typed checks through existing detail/checks-tab props and render ordered textual status, blocking, corrective message and timestamp; verify component cases for passed/null, blocked, failed/nonblocking, warning/nonblocking and empty/uncomputed results, with safe text rendering and no aggregate rank.

## 2. Observation and recovery

- [ ] 2.1 Reconcile successful detail reads even when version/updated_at are unchanged; verify changed checks/checked_at render while dirty input and editor expected_version remain intact and another skill ID cannot replace current results.
- [ ] 2.2 Extend last-loaded/read-error presentation to checks using existing GET recovery; verify retained stale results, polling pause, GET-only retry and no mutation replay or inferred process failure.
- [ ] 2.3 Preserve existing polling and identity behavior; verify bounded unit/component assertions for visible processing-only intervals, hidden/unmount cancellation, one observer, stop at sandbox, manual non-processing read and skill-ID isolation.

## 3. Boundary regression review

- [ ] 3.1 Update affected detail fixtures and status-only assertions to include persisted results and retain current-input/training/sandbox disclaimers; verify no new run/recheck controls, lifecycle transitions, review-MVP results, preflight ownership, security policy or dependencies are introduced. Run only separately authorized focused non-browser checks during implementation; document that mock assertions do not certify backend integration.
