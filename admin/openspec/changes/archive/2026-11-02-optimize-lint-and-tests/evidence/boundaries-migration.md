# Dependency-cruiser replacement probe

`@boundaries/eslint-plugin@7.4.0` runs through Oxlint with `eslint-import-resolver-enhanced-resolve@1.0.5` and the existing TypeScript resolver. The enhanced resolver was necessary because the node-first resolver accepted a package subpath omitted from its `exports`; TypeScript-only resolution changed existing import-rule diagnostics. The final configuration rejects that subpath.

Temporary CLI fixtures outside the worktree checked allowed and denied layer/public API imports, new and dot-prefixed sibling slices, optional boundaries, relative and alias imports, type-only imports, re-exports and dynamic imports. Separate checks covered missing value/type imports, `import()` type expressions, nested dot-directories and unresolved generated React Router type versus runtime imports. The actual PDF worker URL was accepted when its target existed and rejected when it did not (`boundaries-worker-missing.txt`). These were manual, temporary checks, not maintained regression tests or proof of complete resolver/rule equivalence.

An isolated `lint-staged` fixture passed with a valid public target and failed when the unchanged consumer referenced a moved/missing target (`boundaries-staged-{negative,positive}.txt`). The full `lint:fix` script also passed on an isolated valid fixture. No files were staged in the worktree.

The published packages are absent from corporate registry metadata (404). They were installed using the previously authorized temporary public-registry fallback; a subsequent immutable install passed from the populated local cache with the existing `ajv-formats` peer warning. A cold corporate install remains unverified and blocked by the missing metadata and previously observed Oxlint/Oxfmt binding failures.
