## Context

See proposal.md for motivation and D-020 authority. This design makes the generic/shared ownership boundary explicit before coding; the fix does not require a new architecture.

Observed chain: `app/features/skill-lifecycle/constants/skill-lifecycle.constants.ts` defines seven actions; `model/use-skill-lifecycle.ts` indexes that map by server status; `ui/skill-lifecycle.tsx` renders a permission-wrapped trigger only when an action exists; `handlers/skill-lifecycle-handlers.ts` snapshots the action and submits it after confirmation. All these paths are within the same feature. `app/widgets/skill-details/ui/skill-lifecycle.test.tsx:48–136` currently requires and submits all seven actions. These are connected behaviors, not unused entries (IMPL909-03 and R-IMPL-MOS-909).

`app/entities/skill/api/skill-details-client.ts` validates the broader published status enum, skill ID, expected_version, key and returned detail. `app/entities/skill/model/use-change-skill-status-mutation.ts` disables retry, cancels older detail reads, checks session ownership, commits the actual response and invalidates non-detail skills queries. `app/features/skill-review/model/use-skill-review.ts` also uses this mutation, with its own checklist/confirmation guards. Its archived design explicitly forbids expanding generic lifecycle. `app/widgets/skill-details/ui/skill-details.tsx` composes lifecycle and dedicated toggle as siblings and owns observed detail reads.

## Goals / Non-Goals

**Goals:** Fix availability at its existing feature-owned source; make regression assertions independent of the production action map; preserve all existing safe execution and read paths.

**Non-Goals:** Shared enum/API narrowing, permission/session changes, transport/error-classification refactoring, new models/dependencies, mocks, generated DTOs, checks UI, unrelated explanatory copy, other capability edits, main-spec sync or archive. Backend acceptance of additional transitions is not a reason to expose them here.

## Decisions

1. **Remove exactly four entries from the feature map.** Keep draft/checking, sandbox/review and whitelist/prod source/target pairs and their labels. Leave the map's existing partial status-record type and the hook/UI/handler unchanged. Removing entries naturally removes triggers and prevents opening a new confirmation; a previously opened confirmation still fails existing ID/version/status freshness checks after a server status change. Reject hiding buttons with a second UI allowlist or adding handler-only prohibitions: those duplicate policy or leave misleading triggers. No generic next-stage algorithm.

2. **Do not change shared command validation.** Preserve `skillStatuses`, the entity client and mutation, review's checklist-controlled review → whitelist, bulk ownership and toggle's dedicated disable/enable paths. Restricting shared targets to checking/review/prod would break other owners. Do not move review into lifecycle or reuse review internals across feature slices.

3. **Use the existing mounted component suite as the regression seam.** In `app/widgets/skill-details/ui/skill-lifecycle.test.tsx`, retain the all-nine-status table and eight-step/disabled/current-marker assertions. Replace its seven-action positive expectations with an explicit three-action matrix, plus explicit absence of all four removed labels in every recognized state. In checking/training/autotest/review/prod/disabled assert no generic action trigger or newly opened lifecycle dialog and GET-only observation; do not assert that the whole card lacks buttons, because refresh and prod/disabled toggle remain valid. Assertions must not import the production action map to compute their expected policy.

   Restrict the successful command table to the three approved edges, retaining exact POST path/body/version/key, double-click single-send, prod warning, actual saved DTO and registry invalidation assertions. Add a server-refresh boundary case moving an actionable card to a no-generic-command state, verifying the former trigger disappears without a POST. Add a stale open-confirmation case with a status-only change (unchanged version) to review, verifying confirmation is disabled, no POST occurs, and closing it cannot expose a review transition. Preserve cancellation/focus, stale-version, older-read cancellation, unknown-outcome/new-key, HTTP 409/422, failed-refresh and mismatched-response tests.

4. **Keep observation and safety behavior unchanged.** The neutral eight-stage scale excludes recognized disabled without losing its truthful header. Processing-state polling remains in `useSkillDetailsQuery`; do not replace polling with local advancement. Preserve permission wrappers, snapshot checks, synchronous pending lock, strict unknown-state validation, accessibility, no optimistic status, no automatic POST retry, GET recovery and server-derived cache updates. Corrected IMPL909-07 establishes that published 409 SKILL_CHECKS_BLOCKED already enters conflict reread; this plan contains no missing-reread fix.

5. **Modify only Contract-gated lifecycle in the delta.** Copy its full existing block and preserve its safety scenarios while clarifying generic-only scope and adding allowed/forbidden/owner scenarios. Leave Safe single-skill transitions unchanged. Existing obsolete disabled/eight-status and API-results wording elsewhere is known documentary debt from SCENARIO-MOS-909 C03/C05, not authority to reject disabled or expand this plan.

## Risks / Trade-offs

- [Tests merely delete the four positive cases and miss reintroduction] → explicit negative assertions across all recognized statuses, independently authored expectations and a refresh/stale-confirmation boundary case.
- [An absence assertion accidentally bans separate toggle/review actions] → target generic lifecycle labels/confirmation; leave neighboring owners and shared API unchanged.
- [Broader main-spec wording remains inconsistent about disabled] → preserve recognized disabled and current toggle ownership per D-018/D-020; defer unrelated documentary corrections rather than reproduce obsolete validation.
- [Passing local tests is mistaken for backend transition approval] → report unit/component evidence separately; no integration or runtime propagation claim.

## Migration Plan

After independent planning review and a later explicit implementation request, change the feature map and its mounted component tests together. No data migration, API regeneration or build configuration change is needed. Run `yarn typecheck`, `yarn lint` with no warnings, `yarn test` and `yarn format:check`; do not run browser/E2E tests. API/build checks are unnecessary for this bounded change because neither API types nor build configuration changes. Review the final diff for untouched shared client/review/toggle/polling and preserved safety assertions. A deployment rollback would restore the unwanted four triggers, so it requires explicit disposition; no reverse server transition or data rollback is part of this change. Planning alone performs none of these implementation steps.
