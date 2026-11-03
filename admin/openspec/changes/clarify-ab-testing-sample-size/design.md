## Context

See proposal.md — Why. Read-only source inspection confirms `editor-main.tsx` renders the generic sample label beside `executionBoundary`. `editor-text-field.tsx` already binds labels with `htmlFor` and hints with `aria-describedby`, and converts an empty numeric input to null. Existing `editor.test.tsx` cases cover the empty new default and clearing 42 to null using the old label. The accepted report/review establishes the per-group clarification, not a numerical defect.

This short design resolves the label-versus-hint choice before implementation and keeps regression work bounded.

## Goals / Non-Goals

**Goals:** Make the meaning discoverable in the field's accessible name while preserving current scalar handling and nearby execution disclaimer.

**Non-Goals:** No data migration, model/DTO or transport change, statistics calculation, per-group array, traffic enforcement, auth changes or editor redesign. Existing validation and error/draft behavior remain authoritative.

## Decisions

- Prefer the label “Минимальный размер выборки в каждой группе” on the existing field. A linked hint would satisfy the specification, but the direct label makes the qualifier available immediately and needs no new association mechanism. Avoid unassociated explanatory text.
- Keep `min_sample_size`, numeric conversion, defaults and validators untouched. A per-group label describes the existing scalar, not separate group values or an aggregate total. Do not multiply by group count.
- Extend focused component coverage in `ui/editor/editor.test.tsx`: locate the field by its clarified accessible name in new/detail views, preserve null/default and null-clearing assertions, check unchanged scalar payloads at both inclusive bounds, and rejection/no mutation for 0, negative, fractional and over-max input. Reuse existing form-model boundary coverage where appropriate rather than expanding unrelated editor tests.
- Assert the existing `executionBoundary` remains visible beside these controls. No new execution behavior or alternative disclaimer is introduced.

## Risks / Trade-offs

- Longer label may wrap → use the existing responsive field layout, without redesigning surrounding cards.
- Existing label-based tests will need updates → change only relevant queries and add semantic assertions rather than weakening selectors.
- Wording could be mistaken for runtime enforcement → retain the current disclaimer and avoid statistical or traffic promises.
- Component mocks cannot establish deployed API behavior → claim only bounded regression coverage, not integration acceptance.

## Migration Plan

No persisted-data or API migration. After separate implementation authorization, ship the local wording and focused tests together; rollback only those edits if necessary. Leave archived tasks and main specs untouched during planning. No browser/E2E activity is authorized.
