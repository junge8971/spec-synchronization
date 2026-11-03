## Why

Published persisted readiness results are not yet typed or displayed in the checks tab. This change assigns the single accepted display follow-up from SCENARIO-SKILL-CHECKS, R-SKILL-CHECKS and JOIN-SKILL-CHECKS; it does not reopen historical MOS-1019 delivery or MOS-909 lifecycle work.

## What Changes

- Read and render persisted check type, status, blocking, corrective message and checked_at, including empty/uncomputed and failed/nonblocking results.
- Reconcile fresh results even when record version is unchanged; preserve stale-read labeling, GET-only recovery and unsaved input.
- Preserve current conditional polling, identity isolation, security and process/sandbox deferrals. No check execution, new lifecycle command, review-MVP expansion or preflight ownership transfer.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `skill-checks-training`: extend status observation with truthful persisted-check display and read reconciliation.

## Impact

Future implementation touches skill detail types/decoder, checks-tab props/rendering and existing detail-query/component assertions. Reuse the published detail API and existing UI facilities; no new dependency, backend calculation or permission policy. Saved contract evidence is not deployed runtime acceptance. Run identifiers, processed-input binding, technical process errors, rerun permissions and sandbox availability remain unresolved and outside this change.
