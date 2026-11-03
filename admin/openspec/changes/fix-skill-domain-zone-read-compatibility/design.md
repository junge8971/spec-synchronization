## Context

See proposal.md for motivation. Accepted inputs are `reconcile-control-center-backlog/audit/reports/IMPL-SKILL-DOMAINS.md` and the domain portion of `audit/reviews/R-OPTIONAL-DOMAINS-SEVEN.md` (D-002 domain-zone / D-007 continuation).

Read-only source inspection confirms `app/entities/skill-domain/api/skill-domain-client.ts` shares a two-code enum response schema between list, detail and PUT. Its types alias generated schema types. `app/widgets/skill-domains-registry/ui/skill-domains-registry.tsx` labels every non-authenticated code as open. `app/features/skill-domain-editing/model/skill-domain-form-schema.ts` separately restricts assignment choices. Client tests cover seeded codes and invalid counts, not wider string responses. The accepted audit records existing editor snapshot, field-error and retry coverage; this plan extends rather than replaces it.

## Goals / Non-Goals

**Goals:** A truthful string-code read boundary and display, retained snapshots, focused negative coverage, no accidental widening of assignment options.

**Non-Goals:** Dynamic selector or directory integration, new error-envelope contract, frontend enforcement of backend assignment rules, successful unchanged-inactive writes, auth changes, uniqueness/address decisions, broad CRUD rewrite or archive updates.

## Decisions

1. Use string arrays for response validation consistently across all three read paths. Check the generated response aliases and introduce only a narrow local response projection if needed; do not widen create/update assignment types incidentally or regenerate unrelated contracts. Keep non-string zone values and malformed counts invalid. Reject the alternative of widening only list reads because detail and PUT would remain inconsistent.
2. Replace the binary label with explicit known-code mapping and raw-code fallback rendered as text. Do not normalize, sort, filter or infer activity from code. No activity metadata or lookup is required. Keep domain order, pagination and skill counts unchanged. Reject anonymous fallback because it misrepresents server data.
3. Keep response snapshots distinct from selectable assignment values. Adapt the editor initialization boundary only as needed to retain wider returned codes visibly without casts that pretend they are valid fixed choices. Existing two-code controls remain the only assignment choices. Do not silently filter initial values to satisfy the form schema or change serialization to omission/null. A wider read is not write eligibility; existing validation may prevent an unsupported assignment, but must preserve data and explain the failure rather than report success. Do not implement a new inactive-update policy.
4. Extend existing client, registry and editor tests. Model linked inactive history as fixture provenance, not invented DTO activity metadata. Cover empty/duplicate/unknown/inactive rejection and preservation with the published generic validation/error handling shapes, including unknown paths/general fallback. Fixtures demonstrate UI handling only, not exact backend payloads or successful inactive round trips. Do not modify mocks into an invented directory validator.

## Risks / Trade-offs

- Wider response types may leak into selector types → keep read snapshots and fixed choices separate; add explicit option regression assertions.
- No activity metadata exists in the inspected DTO → retain linked codes without claiming eligibility or attaching invented inactive labels.
- Backend rejection payloads and inactive resubmission policy remain unresolved → test generic no-loss behavior without asserting exact business envelopes or approving a new update strategy.
- Static fixtures cannot establish deployment → future authorized unit/component checks remain local evidence only; no browser/E2E work without explicit permission.

## Migration Plan

After separate implementation authorization, land the bounded adapter/display/editor-boundary correction together with focused regressions. No server migration or directory dependency. Roll back the frontend patch as a unit if needed; no persisted data rewrite. This planning run does not execute tests/builds or apply changes.

## Open Questions

Separate future owner work must establish dynamic selector approval, lookup endpoint/key/labels/order/inactive inclusion, concrete rejection payloads and unchanged-inactive update semantics. None is a prerequisite for this read/preservation correction; do not resolve these by implementation side effects.
