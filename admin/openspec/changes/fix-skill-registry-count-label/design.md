## Context

See proposal.md for motivation. `skills-registry.tsx:101` displays `registry.data.total` with a fixed suffix and passes the same total to pagination. Nearby component assertions expect incorrect singular/few labels. The accepted registry join and independent remaining-seven review establish the defect; bounded source inspection confirms this presentation seam. A search of `app` for `PluralRules`, `pluralize`, and `plural` found no existing helper.

## Goals / Non-Goals

**Goals:** isolate Russian word-form selection from data retrieval and preserve the existing count location and accessible text.

**Non-Goals:** changing numeric formatting, DTO validation, query normalization, filters, pagination, sorting, permissions, or unavailable features. No new dependency or cross-registry redesign.

## Decisions

- Use the platform `Intl.PluralRules('ru')` cardinal selection, mapping `one` to `навык`, `few` to `навыка`, and `many`/`other` to `навыков` for the existing integer server total. A small pure formatter in the registry area can keep this independently testable. A new dependency or hand-coded modulo rules adds unnecessary maintenance; an existing equivalent project facility can be reused if found during implementation.
- Keep `registry.data.total` as the sole numeric input, not `items.length`. Do not change request construction or pagination. Formatting the loaded page length would misrepresent filtered server results.
- Replace the erroneous 1/2 expectations and plan table-driven cases for 0, 1, 2, 3, 4, 5, 11, 12, 13, 14, 21, 22, 23, 24. Add a component regression selecting `status=training`, checking the server request and label, including a server total larger than the loaded page. Retain URL/history, reset and offset assertions rather than substituting local filtering.

## Risks / Trade-offs

- Platform locale support → verify Russian plural selection with focused unit checks during separately authorized implementation; do not add a dependency speculatively.
- Existing incorrect expectations can mask the defect → explicitly replace them and cover teen exceptions and 21–24.
- Count and sort packages may modify the same full requirement → parent must reconcile deltas without dropping preserved scenarios; sorting remains outside this package.
- Static/component evidence does not prove backend behavior or visual geometry → make no runtime or visual acceptance claim; browser/E2E remains separately permission-gated.

## Migration Plan

No data or API migration. After review and separate apply authorization, ship the label and focused assertions together; rollback only the presentation change if necessary. Preserve security, validation, error states, and accessibility. This writer executes no implementation or runtime checks.
