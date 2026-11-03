## 1. Limit feedback correction

- [ ] 1.1 Update KB export error presentation to append narrowing advice for the structured HTTP 422 `EXPORT_LIMIT_EXCEEDED` error while preserving the server message and accessible alert; verify the limit-envelope component regression shows advice without receiving it from the server and unrelated errors keep their existing presentation.
- [ ] 1.2 Preserve form selection/order, mutation and download behavior without new transport or optional cross-imports; verify the scoped diff leaves server limit, API, session ownership, saved-detail behavior and historical archive tasks unchanged.

## 2. Focused component regression

- [ ] 2.1 Add a regression in `app/optional/knowledge-base/ui/export/knowledge-base-export.test.tsx` using the actual HTTP 422 `EXPORT_LIMIT_EXCEEDED` envelope with `Mock export exceeds 10000 rows`; verify limit plus narrowing advice, non-default selected fields/order retained through an explicit retry, no object URL/download/false success on failure and no automatic replay.
- [ ] 2.2 Add a negative case with HTTP 422 and a different validation code, without supplied narrowing advice; verify its own error remains visible, no limit advice is added, selected fields remain and no download or false success occurs.
- [ ] 2.3 After implementation authorization, run the focused KB export component suite and scoped formatting checks; verify existing successful/full-selection, generic-error, saved-detail and file-lifecycle regressions remain green, without E2E/browser checks or claims of live API/deployment acceptance.
