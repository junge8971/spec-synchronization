## 1. Correct count presentation after separate implementation authorization

- [x] 1.1 Add Russian count-word selection using platform plural facilities (or an existing equivalent helper), without dependencies; verify focused unit cases for 0, 1, 2, 3, 4, 5, 11, 12, 13, 14, 21, 22, 23 and 24 match the delta scenario.
- [x] 1.2 Apply the formatter to `registry.data.total` in the existing registry count label; verify by diff review and a component assertion that a server total larger than the loaded page remains the displayed number and pagination input, with no request/URL/permission changes.

## 2. Regression verification

- [x] 2.1 Replace `1 навыков` and `2 навыков` expectations in `skills-registry.test.tsx` with correct forms; verify the focused registry component suite passes while retaining existing 0/11 and unknown-status coverage.
  - The named suite was absent on this branch. Created it with the intended `0 навыков`, `1 навык`, `2 навыка`, `11 навыков`, and unknown-status assertions; existing tests were not removed. The 1/2 cases failed against the fixed suffix and passed with the formatter.
- [x] 2.2 Add a training-status component regression covering the filtered server-total label, server `status=training` request, first-page reset, URL/history and page offsets; verify it preserves server filtering and pagination rather than counting or filtering the loaded page.
- [x] 2.3 Record focused unit/component results and review the final diff for preserved error handling, validation, accessible count text and unchanged API/security boundaries; explicitly record that mocks do not certify backend integration and that browser/E2E and visual acceptance remain unauthorized and unperformed.
  - Passed 14 formatter cases and 5 registry component tests, including `status=training`, offsets 0/10 and back/forward. The count remains plain text and reads the same server total as pagination. The count diff leaves request, validation, error and permission paths untouched. Mocks do not certify backend integration; browser/E2E and visual acceptance were not authorized or performed for MOS-1051.
