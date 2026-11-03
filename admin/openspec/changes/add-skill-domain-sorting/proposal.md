## Why

MOS-1052 independently requests domain sorting, but the registry exposes only name and modification-date sorting. The accepted registry join and review establish saved documentary support for `domain_name` and `-domain_name`, not deployed backend behavior.

## What Changes

- Add a domain-specific header sort action and both directions to the URL allowlist, preserving page reset, filters, history and server requests.
- Require authoritative semantic/backend confirmation before implementation and acceptance; unrestricted schema strings alone are not proof of support.
- Preserve server ordering; do not add local-page, status, dialog-count or creation-date sorting. Count-label correction remains a separate change.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `skill-catalog-experience`: extend the existing contract-backed registry requirement with gated server-backed domain sorting.

## Impact

Registry table/handler, registry sort types and URL allowlist, and focused URL/component/client assertions. Reuse the existing list endpoint and query transport without new dependencies or schema generation. No auth, lifecycle, warning, archive or main-spec edits in this planning package. Preserve accessibility, validation, error handling and security; browser/E2E requires separate permission.
