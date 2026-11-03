## Why

The accepted domain audit and seven-lane review identify a conditional read incompatibility: string zone codes outside the two assignment choices fail the shared response adapter, and simply widening it would mislabel those codes as «Открытая». Truthful reads can be corrected now without deciding dynamic selection or inactive-update policy.

## What Changes

- Preserve returned string zone codes in list, detail and PUT responses, including linked inactive values, server order and counts.
- Keep known labels and display unknown codes verbatim rather than normalizing them to anonymous.
- Separate the read representation from the fixed assignment choices; add focused read/display and no-loss rejection regression coverage.
- Retain PUT, version and idempotency behavior. No silent removal and no promise of successful unchanged-inactive writes.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `skill-domain-management`: clarify truthful zone reads and preservation on zone-related rejection within existing registry and editing requirements.

## Impact

Bounded changes to the skill-domain response type/adapter, registry labels, editor snapshot compatibility and connected unit/component tests. No new endpoint, lookup prerequisite, selector option, auth behavior or backend validation policy. Existing creation selection remains `authenticated`/`anonymous`; uniqueness/address deferrals and historical archives stay unchanged. Dynamic selector/lookup and concrete rejection payload/update policy remain separate owner decisions. This is planning only, not runtime or deployment evidence.
