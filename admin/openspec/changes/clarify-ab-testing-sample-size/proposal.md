## Why

The accepted ABROOT-05 clarification and optional-domain review identify a wording gap: the editor says “Минимальная выборка” without explaining that the minimum is per group. Make that meaning accessible without changing numeric behavior or implying experiment execution.

## What Changes

- Clarify the existing sample-size field through an accessible label or associated hint stating “в каждой группе”.
- Add focused label, null/default and numeric-boundary regression coverage; retain the execution disclaimer.
- Preserve the nullable integer 1–2147483647 scalar, defaults and API payloads. No statistics, calculator, traffic enforcement or broad editor rewrite.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `ab-testing-editor`: clarify the per-group meaning in “Complete editor and initial values”, preserving the complete existing requirement and scenario.

## Impact

Bounded to `app/optional/ab-testing/ui/editor/editor-main.tsx` and focused editor/model regression tests. Existing `EditorTextField` label/help association supports the clarification; no shared component, DTO, API, mock contract, dependency or module requirement change is needed. Archive task 5.1 remains historical. Security, validation, draft/error handling and existing access boundaries remain unchanged; browser/E2E work is not authorized.
