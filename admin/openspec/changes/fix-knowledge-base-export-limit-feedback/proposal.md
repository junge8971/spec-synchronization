## Why

The existing Knowledge Base export limit scenario requires advice to narrow selection, but the connected HTTP 422 `EXPORT_LIMIT_EXCEEDED` message contains no advice and the UI renders it verbatim. The accepted bounded export audit and review identify a focused correction; existing tests inject advice themselves under different statuses.

## What Changes

- Make the existing limit scenario explicit for HTTP 422 `EXPORT_LIMIT_EXCEEDED` without server-supplied advice.
- Show narrowing advice while preserving selected fields, with no download or false success.
- Cover the real envelope at the export component boundary and distinguish unrelated 422 validation failures.
- Preserve the current row limit, API, transport, optional-module boundaries and historical archive task states.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `knowledge-base-export`: Clarify limit-error feedback in the existing full-selection CSV export requirement, including a non-limit 422 negative case.

## Impact

Focused changes are expected in `app/optional/knowledge-base/ui/knowledge-base-export.tsx` and `app/optional/knowledge-base/ui/export/knowledge-base-export.test.tsx`, with a KB-local presentation helper only if needed. Existing shared error types and file transport remain unchanged; no optional cross-imports, API changes, dependencies, authentication or permission work. The original `2026-10-14-add-optional-knowledge-base` archive remains historical; this active correction does not reopen its tasks 9.1–9.3. Planning evidence: `IMPL-KB-EXPORT.md` and the KB-limit-advice section of `R-OPTIONAL-DOMAINS-SEVEN.md` under the reconciliation audit.
