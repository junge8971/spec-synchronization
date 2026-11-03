## Why

The mounted generic skill lifecycle exposes seven transitions and its component tests affirm all seven, whereas the approved MOS-909 scope permits only three (audit IMPL909-03 and independent R-IMPL-MOS-909). Decision D-020 explicitly selects restoring the three-command scope through a separate corrective plan, not implementing it during this planning run.

## What Changes

- Restore the generic card actions to draft → checking, sandbox → review and whitelist → prod only.
- Remove generic checking → training, training → autotest, autotest → sandbox and review → whitelist triggers; explicitly require their absence, alongside no generic command in prod/disabled.
- Strengthen positive and negative mounted component regression coverage without weakening confirmation, recovery, accessibility or server-derived cache assertions.
- Clarify that the generic feature boundary does not restrict the separately owned review → whitelist capability, dedicated prod/disabled toggle or shared status API.
- Preserve the neutral eight-stage scale, recognized disabled state, polling, permission wrappers, strict validation and existing error handling.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `skill-lifecycle`: make the existing Contract-gated lifecycle requirement's generic-only boundary explicit and add allowed/forbidden action scenarios; retain the other safety requirements unchanged.

## Impact

Future implementation is limited to `app/features/skill-lifecycle/constants/skill-lifecycle.constants.ts` and `app/widgets/skill-details/ui/skill-lifecycle.test.tsx`. The existing hook/UI/handler already derive command availability from that map. No shared enum/client/mutation, transport, generated DTO, auth, mock policy, review/toggle implementation or dependency changes are needed. No checks UI, unrelated copy correction, main-spec synchronization or archive edits belong to this planning assignment.

Authority and evidence: `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (D-018–D-020), `reports/IMPL-MOS-909.md` (IMPL909-03; corrected IMPL909-07), `reviews/R-IMPL-MOS-909.md`, and accepted `reports/SCENARIO-MOS-909.md` / `reviews/R-SCENARIO-MOS-909.md` under that audit directory. Backend admissibility is not frontend command authorization. Independent artifact review remains pending; implementation requires a later explicit apply request.
