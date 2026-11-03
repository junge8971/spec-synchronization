# MOS-913 — additive review correction

Parent accepts JOIN-MOS-913 only together with R-D095-TEN C1–C3 and this overlay. Original report and REVISE verdict remain unchanged.

- `app/widgets/surface-details/ui/surface-details.test.tsx:710–718` already asserts disabled copying and absence feedback for null, empty and whitespace-only code (`it.each([null, '', '   '])`). Remove this item from proposed missing-regression work. Assertions were read, not executed.
- Two distinct static discrepancies remain: help navigation versus placeholder toast, and missing draft-membership explanation for equal-count replacement. The opening claim of only one discrepancy is not the accepted summary.
- Main `surface-overview-connection` requires `/docs` with basename. Reviewer found no superseding approval in inspected later archives; that is bounded repository evidence, not proof against approval elsewhere. Queue a narrow reconciliation, no automatic implementation.
- Saved `[A]` versus draft `[B]` is not detected by count-only comparison. Any correction must preserve saved checklist facts and existing selection/publication policy.
- Reverse metric combinations/integer validation remain separate optional questions, not established runtime failures.

Review: `../reviews/R-D095-TEN.md`. No application/spec/archive edits or test execution. Parent publication queue only.
