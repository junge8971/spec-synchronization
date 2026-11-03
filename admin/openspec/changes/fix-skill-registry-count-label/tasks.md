## 1. Correct count presentation after separate implementation authorization

- [ ] 1.1 Add Russian count-word selection using platform plural facilities (or an existing equivalent helper), without dependencies; verify focused unit cases for 0, 1, 2, 3, 4, 5, 11, 12, 13, 14, 21, 22, 23 and 24 match the delta scenario.
- [ ] 1.2 Apply the formatter to `registry.data.total` in the existing registry count label; verify by diff review and a component assertion that a server total larger than the loaded page remains the displayed number and pagination input, with no request/URL/permission changes.

## 2. Regression verification

- [ ] 2.1 Replace `1 навыков` and `2 навыков` expectations in `skills-registry.test.tsx` with correct forms; verify the focused registry component suite passes while retaining existing 0/11 and unknown-status coverage.
- [ ] 2.2 Add a training-status component regression covering the filtered server-total label, server `status=training` request, first-page reset, URL/history and page offsets; verify it preserves server filtering and pagination rather than counting or filtering the loaded page.
- [ ] 2.3 Record focused unit/component results and review the final diff for preserved error handling, validation, accessible count text and unchanged API/security boundaries; explicitly record that mocks do not certify backend integration and that browser/E2E and visual acceptance remain unauthorized and unperformed.
