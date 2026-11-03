## Context

See proposal.md for motivation. Reuse source audit `reports/JOIN-SKILL-REGISTRY.md` and `reviews/R-SKILL-REMAINING-SEVEN.md` under `openspec/changes/reconcile-control-center-backlog/audit/`. Saved wiki §2.5 explicitly lists ±domain_name. The review reconciles saved r1, r2 and local `docs/api/contracts/openapi.json`: sort is an unrestricted string, default `-updated_at`, with no enum or conflicting allowed-values list. There is no schema contradiction, but neither schemas nor this plan certify runtime support.

Read-only code inspection confirms a plain “Домен и команда” header, a handler restricted to name/updated_at, and the same four-value URL allowlist. The existing search-param updater resets page on sort changes and preserves other parameters; the client forwards sort and computes offset, returning server order/total unchanged.

## Goals / Non-Goals

**Goals:** Extend that existing URL-to-request path for domain-name sorting without duplicating state or altering pagination semantics. Make the action clearly sort domain, not team.

**Non-Goals:** Status/dialog sorts, local sorting, count inflection, registry redesign, created-date UI sort, new backend policies, auth/lifecycle changes or generated API/schema changes.

## Decisions

1. **Explicit prerequisite:** Before implementation and acceptance, obtain and record authoritative semantic/backend confirmation of both sort tokens and domain-name ordering on the full filtered result set. The saved wiki is positive documentary evidence; permissive schema typing is not an executable guarantee. If confirmation contradicts this plan or requires new product ordering policy, stop and escalate rather than guessing collation, tie-breaking or fallback. No runtime investigation is authorized by this planning task.
2. **Extend existing plumbing:** After the gate, extend the registry sort type, handler field union and allowlist together; reuse the header button pattern with a domain-specific accessible name. First activation selects `domain_name`; repeat selects `-domain_name`. Reuse the current updater for page reset and query preservation. Reject a separate local sort state or unrestricted-string allowlist because either breaks URL/server consistency.
3. **Server remains authoritative:** Continue passing the selected token to the list endpoint and render returned order unchanged. Preserve default `-updated_at`, existing supported sorts, invalid-sort normalization, filter reset behavior, history and error/retry handling. Do not invent a client comparator, team sort or secondary tie-break.
4. **Focused future verification:** Extend existing search-param, registry component and client tests for both tokens, header toggling, page reset, back/forward restoration, filters and request offsets. Use intentionally non-alphabetic fixture order to prove the UI does not reorder server rows. Mock assertions establish transport/UI behavior only, not deployed backend semantics. Browser/E2E remains separately permissioned.

## Risks / Trade-offs

- [Backend semantics remain unconfirmed] → Keep prerequisite unchecked; no implementation or acceptance from schema permissiveness alone.
- [Combined domain/team header suggests team sorting] → Explicit domain-specific accessible action; team data stays unchanged.
- [Count lane touches the same requirement] → Preserve the complete original block here; parent reconciles future integration without dropping either delta or existing scenarios.

## Migration Plan

No data migration or new dependency. After separate authorization and confirmation, implement the bounded frontend extension; rollback removes only the added domain-sort exposure/type/allowlist entries and retains existing normalization/default behavior. Parent reviews and integrates this isolated planning directory; no runtime apply in this run.
