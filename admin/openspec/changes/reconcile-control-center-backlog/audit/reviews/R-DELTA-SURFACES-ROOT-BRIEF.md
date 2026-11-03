# R-DELTA-SURFACES-ROOT-BRIEF — independent documentary review

## Review

**REVISE — one narrow wording correction.** All nine candidate dispositions otherwise preserve the scoped approved boundaries.

- **Correct:** Source identity, documentary qualifications, deferred configurator ownership, no-sandbox MVP and partial-save/read-recovery gates are preserved.
- **Fixed:** None; read-only review.
- **Finding: P2:** DSRB-02 reverses the domain-uniqueness constraint into a domain-count constraint.
- **Merge verdict:** **OK with notes** for the documentary analysis; apply the correction below before accepting the report unchanged.

## Mandatory minimal correction

Location: `audit/reports/DELTA-SURFACES-ROOT-BRIEF.md`, **DSRB-02**, “Actual wording and locator” column.

Replace:

> one domain per surface

with:

> each domain belongs to only one surface

Evidence: `audit/sources/wiki-241080065-readable/r1/content.txt:51,70` says «один домен — одна поверхность»; lines 8 and 21 explicitly describe conflicts when a domain is already used. This is uniqueness across surfaces, not a limit of one domain on each surface. `openspec/specs/surface-overview-connection/spec.md:9–19` explicitly preserves **all domains** returned for a surface. No other wording or owner change is necessary.

## Candidate verification

`A` = `openspec/changes/reconcile-control-center-backlog/audit`; `B` = `A/sources/wiki-241080065-readable/r1/content.txt`, page v1 / capture r1.

| Candidate | Result |
|---|---|
| **DSRB-01** | **Accept.** B44 supports columns, filters and search. Saved overview metrics are correctly separated from list behavior (`surface-overview-connection:56–78`). The uninspected list owner is not declared implemented, deficient or fully audited. |
| **DSRB-02** | **Revise wording only**, as above. B17–23/51/70 supports registration and conflict intent. Registration defaults, optional atomic creation, confirmed-ID read recovery, unknown-outcome replay prohibition and minimum production selection remain intact (`surface-registration:23–78`). |
| **DSRB-03** | **Accept.** B24–30/46 supports appearance, content and action labels without transport enums, exact placeholders or a save contract. Accepted r2/review/D-002 resolves earlier publication gaps without activating the deferred editor. |
| **DSRB-04** | **Accept.** B27/29/46 supports production selection and composition toggles, not global skill disable or web-domain availability. Existing empty-composition editing remains distinct from registration/publication minimums (`surface-skill-selection:85–145`). |
| **DSRB-05** | **Accept.** B9–11/47–50/83–84 supports preview, connection, overview and history intent. Server-owned code, nullable data and deferred preview/history are preserved; insertion instructions do not establish deployment or availability. |
| **DSRB-06** | **Accept.** B31–38/52–53/82–83 genuinely contains sandbox and greeting-gate contradictions. The report correctly retains them as historical evidence, not reopened blockers, status aliases or MVP prerequisites. |
| **DSRB-07** | **Accept.** B39–41 explicitly states hidden assistant/placeholder effects. These remain unverified source claims, distinct from skill status, global disable, link reachability and token/code revocation. |
| **DSRB-08** | **Accept.** B43–63/72–75 supports the MUST/phase tension and optional availability/copy/import detail. No schedule fulfillment, activation or missing-feature conclusion is inferred. |
| **DSRB-09** | **Accept.** B17/64–71/77 supports historical access, audit and latency targets. No measurement, enforcement verification, permission mapping or new admin-session policy follows. |

## Preserved critical gates

Verified against `surface-lifecycle-publication/spec.md:70–123,138–158,179–196`, the accepted journal chain and D-024:

**confirm → validate current skills/parameters → save enabled skills → fresh read begun after successful save → recheck eligibility → publish → fresh read confirming prod → success.**

The report preserves:

- Cancellation performs no writes.
- Preparation/save/read failure stops publication.
- Confirmed partial saves remain saved; publication failure does not imply rollback.
- Failed reads after successful writes permit read recovery, not blind mutation replay.
- Conflict recovery retains manual refresh and explicit new-action gates.
- No hidden configuration write, whole-card atomicity, synthesized configured status, sandbox activation or greeting prerequisite.
- Dates, journal closure and source wording do not establish precedence over approved boundaries.

## Actual inspected evidence

Read completely:

- Both assigned work-items and `A/reports/DELTA-SURFACES-ROOT-BRIEF.md`.
- Original `wiki-241080065/r1/metadata.json` and `content.json`, including canonical `bodyView` and separate attachment index.
- Derived metadata, all 84 readable lines and all five exact markup chunks.
- All four current scoped surface specifications.
- `SCENARIO-SURFACE-CONFIG-r2.md`, `R-SURFACE-CONFIG.md` and D-002 (`decisions.md:279–288`).
- `JOURNAL-SURFACE-MVP.md` and `R-JOURNAL-SUPPLEMENTS.md`, using only surface dispositions, plus D-024 (`decisions.md:97–104`).

The returned attachment index is empty; this does not establish complete linked-resource coverage. Distinct wiki-245673187 was neither substituted nor reopened.

## Verification limits

Local documentary inspection only. Parent-recorded hashes and chunk concatenation equality were **not independently recomputed**. Prior accepted API/journal investigations were consulted as attributed evidence, not independently recertified against their underlying sources.

No application code, API scan, tests/build, browser/network, source execution, examples, archive audit, nested delegation or repository mutation. Git/index uninspected; no staging or clean-tree attestation. No product approval, implementation acceptance, owner-plan change or global closure follows. **Global6/28 unchanged.**