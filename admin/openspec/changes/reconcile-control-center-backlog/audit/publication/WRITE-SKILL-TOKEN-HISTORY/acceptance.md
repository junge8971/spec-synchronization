# D-081 — token/cache and audit-reader planning corrections

Parent accepts seven replacements in five planning files, exactly matching `candidates.json` independently accepted by run `35631d26-cc8e-4b6f-a47d-386d38ec21e1` (`review.md`). Parent alone performed project writes. All target before hashes and candidate hash matched review immediately before applying; installed bytes verified against original files plus exact replacements. See `installed-hashes.json`, `accepted.diff` and `before/`. All 15 token/history feature tasks remain unchecked.

## Evidence and scope

D-080 accepts the three bounded implementation reports and independent batch review. MOS-1018 requires no new planning correction. MOS-1023 now explicitly separates secrets before ordinary Query cache, including compatible ordinary skill-detail responses, with synthetic response/cache tests and metadata preservation. This is a conditional risk, not observed secret delivery/leakage. Existing API/security gate remains; no operation is activated.

MOS-1031 removes nonexistent local audit.md as evidence and distinguishes a separately documented audit service from unaccepted browser-reader integration. Routing, credential destination, authorization, identity, redaction and consistency remain gates; no new auth model or endpoint is invented.

Freshness: parent read-only documentation check at `2026-10-20T12:29:58.622Z`, `https://wiki.mos-team.ru/rest/api/content/241077434?expand=version`, HTTP 200, page version 2, timestamp `2026-09-07T19:22:13.762+08:00`; matches accepted evidence. Token claims concern the already accepted saved r2 and current local parsing/cache paths, explicitly conditional on agreed integration, not a claim about today's live schema or response. No new Jira behavior inferred; no external write, business endpoint or browser/E2E test.

## Validation

- `openspec validate mos-1023-skill-environment-tokens --strict`: pass.
- `openspec validate mos-1031-skill-audit-history --strict`: pass.
- `openspec validate --all --strict`: pass.
- `openspec doctor`: pass.
- Targeted Prettier check of all five changed planning files: pass.
- Full `yarn format:check`: not rerun in this package; last failure 413 files retained in `../WRITE-REPORTS-PLANS/reports-format.log`. User explicitly authorized continuing independent work with this separate failed gate; no waiver or full-format success claimed.
- Runtime typecheck/lint/test/api:check/build/typegen: not run, no runtime/API/build changes. Browser/E2E: not run.

## Disposition

Package published; no pending candidate remains. Global 11/28 and 57P/5B/111U unchanged: these are deeper partial joins, not feature completion or global gate acceptance. Formatting and untouched scenarios remain. Original empty-final child failures remain recorded despite independently accepted recovered report artifacts.
