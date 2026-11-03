## 1. Read boundary and truthful display

- [ ] 1.1 Separate string-code response typing/validation from fixed assignment types in the skill-domain entity; verify client regressions preserve wider codes in list, detail and PUT responses while rejecting non-string zones and invalid counts, with PUT/version/idempotency assertions unchanged.
- [ ] 1.2 Replace registry binary labels with explicit known labels and raw-code fallback; verify component fixtures retain domain/zone ordering, linked inactive history, total, skills_count and navigation, without a zone lookup request.

## 2. Editor preservation and negative coverage

- [ ] 2.1 Adapt only the editor read-snapshot boundary needed for wider codes; verify returned codes remain visible/preserved, fixed assignment options remain exactly authenticated/anonymous, and no code is silently stripped, converted, or promoted to a new option.
- [ ] 2.2 Add focused empty/duplicate/unknown/inactive zone rejection regressions using existing error-handler/component boundaries and generic published error shapes; verify values and linked codes survive, known field locations and general fallback remain accessible, and no false success or automatic modified-body retry occurs. Do not assert an invented exact backend rejection payload or successful unchanged-inactive save.

## 3. Bounded verification

- [ ] 3.1 After separate implementation authorization, run the affected client, registry, editor and error-handler unit/component checks; verify existing conflict, retry-key, dirty-refetch and keyboard cancellation coverage remains passing and record results without claiming real integration. No browser/E2E tests without explicit permission.
- [ ] 3.2 Review the final implementation diff against this delta; verify no selector/lookup expansion, PUT reversal, omission/null policy, mock business-policy invention, auth changes or uniqueness/address scope creep, and record the separately unresolved owner decisions.
