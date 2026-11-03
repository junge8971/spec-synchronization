## Context

See proposal.md for motivation. Read-only inspection confirms that `ui/knowledge-base-export.tsx` renders `mutation.error.message` in an alert, while `mocks/knowledge-base/handlers.mjs` supplies `EXPORT_LIMIT_EXCEEDED` to `sendManagedCsv`, which emits HTTP 422 with `Mock export exceeds 10000 rows`. The component test currently injects narrowing advice into generic 413/500 envelopes. Shared `ApiError` in `app/shared/api/http-client.ts` already exposes status and code. This design resolves error-classification and test-boundary choices before implementation.

## Goals / Non-Goals

**Goals:** Keep the correction inside KB error presentation and verify it through the mounted export component using the existing fetch/transport seam. Preserve the alert's accessibility and form state.

**Non-Goals:** No new transport, server limit, endpoint, DTO, dependency, auth/session/permission behavior, optional cross-import, broad export refactor or archive rewrite. Saved-detail, pending, session-owner and file-resource behavior remain intact.

## Decisions

- Recognize the existing structured HTTP 422 `EXPORT_LIMIT_EXCEEDED` error using shared `ApiError` information at the KB presentation boundary. Retain the server error text and add explicit local advice such as «Сузьте отбор и повторите экспорт». Do not match English message substrings or infer a limit from 422 alone: both alternatives are brittle or misclassify validation failures.
- Keep generic failures on the existing alert path. Do not reset/remount the field form or change mutation/download flow to add advice. A KB-local helper is acceptable if needed for readability; importing A/B export behavior or moving domain-specific copy into shared transport is unnecessary coupling.
- Add focused component coverage using HTTP 422 with `{ code: 'EXPORT_LIMIT_EXCEEDED', data: null, message: 'Mock export exceeds 10000 rows', errors: [] }`. Exercise non-default selected fields/order, assert server limit plus local advice, no object URL/download/success, no automatic replay and selection retention for retry. A separate 422 with a different validation code and no advice must retain its own message without added limit advice. Keep existing generic-error and successful-export regressions; do not change the mock to supply the missing advice.

## Risks / Trade-offs

- [Mock envelope is not live-backend proof] → Keep claims bounded to the saved connected contract and component regression; no deployment or browser-delivery acceptance follows.
- [Server text may already contain advice] → Local advice remains reliable without language-dependent parsing; repeated server wording is preferable to omitting required guidance.
- [Error formatting accidentally resets state or broadens classification] → Assert non-default field selection/order on retry and an unrelated 422 negative case through the component boundary.

## Migration Plan

No data migration or backend rollout is required. After separate implementation authorization, ship the local presentation correction and focused regression together; rollback is limited to those code/test edits. Preserve the original archive and all unrelated requirements. This planning run performs no implementation, tests, builds or browser checks.
