# D-087 — parent publication acceptance

Three new corrective changes installed byte-for-byte after fresh independent ACCEPT review; no mandatory patches. Writer receipts and review.md preserved unchanged. installed-hashes.json records all 15 installed artifacts. Four source main-spec hashes reverified against review.md immediately before copying. Original requirements preserved; 5 KB + 3 AB + 6 domain tasks remain unchecked.

- fix-knowledge-base-export-limit-feedback: actual 422 EXPORT_LIMIT_EXCEEDED advice, unrelated-code negative regression, unchanged selection/file semantics.
- clarify-ab-testing-sample-size: accessible per-group meaning without scalar/default/bounds/DTO/execution changes.
- fix-skill-domain-zone-read-compatibility: truthful returned string codes and labels, fixed assignment boundary, preservation/error regressions; unresolved selector/directory/inactive-update policies excluded.

Writer workflow f08b434b-4e1b-4ab2-98e6-24455dc2ceba; fresh review 4e940772-c914-48b5-a110-22fe8d3a4e27. Seven underlying reports independently accepted by c7f90fbc-3fb2-4d62-b954-88a8a89b758e (reviews/R-OPTIONAL-DOMAINS-SEVEN.md). No rerun of completed analysis, runtime acceptance or hidden failure recovery.

Post-install `openspec validate --all --strict`, `openspec doctor` and explicit three-change Prettier check passed (logs alongside). Prior full `yarn format:check` failure on 413 files remains unresolved, not rerun or waived. Typecheck/lint/test/api:check/build/typegen/browser/E2E not run: this packet changes planning/audit only; runtime and browser work prohibited. No main-spec sync, archive edits or external refresh. Local hash freshness is not source-server currency or deployment evidence.

Active-change event count 26; Jira 59P/4B/110U and global 11/28 unchanged. No feature or global task closure. Planning package complete; remaining audit gaps remain open.
