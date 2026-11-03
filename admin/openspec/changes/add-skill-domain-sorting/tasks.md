## 1. Required confirmation before implementation

- [ ] 1.1 Record authoritative semantic/backend confirmation for `domain_name` and `-domain_name` over the full filtered list, explicitly reconciling saved wiki support with unrestricted-string r1/r2/local schemas; verify the evidence covers both directions before any implementation or acceptance. Stop and escalate contradictory semantics or new product-policy choices; do not infer runtime support from schemas or mocks.

## 2. Bounded frontend extension after confirmation and authorization

- [ ] 2.1 Extend the registry sort type, header handler field union and URL allowlist for both domain tokens; verify focused search-param assertions cover parsing, normalization, page reset, filter preservation, default `-updated_at` and continued rejection of status/dialog sorts.
- [ ] 2.2 Add a keyboard-accessible domain-specific header action using the existing sort path, without implying team sorting; verify component assertions cover ascending/descending toggles, offset 0 after changes, filters and back/forward page/sort restoration.
- [ ] 2.3 Verify the existing client transports both domain tokens with limit/offset and preserves server total and row order; extend client/component assertions with deliberately non-alphabetic server fixtures to reject local-page sorting and retain existing name/date behavior.

## 3. Bounded acceptance

- [ ] 3.1 Run the authorized focused unit/component checks for the changed URL, header and client seams and record exact results alongside the authoritative confirmation from 1.1; distinguish mocked transport/UI evidence from backend acceptance. Preserve security, error/retry and accessibility, and do not create or run browser/E2E without separate permission.
- [ ] 3.2 Review the final delta for domain-sort-only scope and full preservation of the original requirement/scenarios; verify no status/dialog sort, local comparator, count correction, schema widening, lifecycle/auth changes or historical rewrites entered the package. Parent reconciles any shared-requirement conflict with the separate count change before integration.
