## 1. Accessible sample-size wording

- [ ] 1.1 Update only the sample-size label in `app/optional/ab-testing/ui/editor/editor-main.tsx` to state “в каждой группе”; verify the existing label association exposes that accessible name and the nearby execution disclaimer remains unchanged, with no DTO/default/validator/transport changes.

## 2. Focused regression coverage

- [ ] 2.1 Update relevant label queries and add new/detail component assertions in `app/optional/ab-testing/ui/editor/editor.test.tsx`; verify the per-group accessible name, visible execution disclaimer, empty/null new default and clearing a saved number to a null payload.
- [ ] 2.2 Add or reuse focused component/form-model boundary cases for null, 1 and 2147483647 acceptance and 0, negative, fractional and 2147483648 rejection; verify accepted payloads retain the one scalar without group-count multiplication and rejected saves retain draft, expose a field error and send no mutation. After separate implementation authorization, run only the relevant unit/component cases and record results; no browser/E2E or real-API claim.
