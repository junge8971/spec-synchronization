# R-FEEDBACK-INDEX-REPAIR

## Review

**Decision: ACCEPT — narrow additive index accounting and provenance only.**

No issues found.

- **Correct:** The separate five-entry selected projection and r25 accounting agree with the accepted prior snapshot and D-043 repair boundary.
- **Fixed:** None; read-only review.
- **Mandatory corrections:** None.
- **Merge verdict:** OK with notes. Acquisition and hash remain parent-attributed; historical packet preservation is not a reviewer-certified byte comparison.

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

## Evidence checked

Read completely:
- `sources/wiki-247734813-attachment-index/r1/content.json`
- Its `metadata.json`
- `coverage-partial-r25.json`
- The accepted final-increment report and review.

Also inspected D-043 (`decisions.md:3–9`), existing root href (`sources/wiki-238324523/r2/links.txt:19`), original feedback metadata, and the scoped canonical attachment-file listing.

### Selected index

`content.json:2–24` records parent **247734813**, HTTP **200**, capture **2026-10-19T12:13:31.104Z**, start **0**, limit **100**, size **5**, and `next: null`. Its five distinct IDs are:

| ID | Recorded title |
|---|---|
| 250790182 | ПротоОбратнаяСвязь.html |
| 247746709 | Прототипчик.html |
| 247739129 | База знаний.html |
| 247737143 | Прототип обратной связи.html |
| 247734812 | новый 5.html |

All five entries have `text/html` media types and ID-consistent self links. The parent’s root href matches saved root line19.

The artifact explicitly identifies itself as a **selected projection, not raw HTTP response** (`content.json:9–10`; `metadata.json:11`). Download/webui links are omitted. No version objects are recorded; metadata’s `version: null` does not establish attachment versions. URL version parameters would not independently establish them either.

`next: null` means no continuation indicated in this saved projection, not current external completeness. Names, media types and links establish neither relevance nor runtime behavior or source precedence.

### Additive counts

D-043 and the accepted report/review establish the historical **42 packets / 41 indexes / 34 entries = four saved + 30 unread** snapshot.

`coverage-partial-r25.json:8–25` adds only the separate index:

| Measure | Accepted prior | Addition | After repair |
|---|---:|---:|---:|
| Root body/extraction packets | 42 | 0 | **42** |
| Root pages with returned indexes | 41 | 1 | **42** |
| Known indexed entries | 34 | 5 | **39** |
| Saved prototype texts | 4 | 0 | **4** |
| Unread indexed bodies | 30 | 5 | **35** |

Thus **39 = 4 + 35**. The five IDs are distinct from the prior report’s enumerated attachment population.

The untruncated `sources/wiki-attachment-*/**/*` listing returned only the four previously saved attachment packets. None of the five new IDs has a canonical `wiki-attachment-ID/*/content.*` file in that inspected namespace. This is scoped local evidence, not whole-repository absence or an asset census.

### Preservation and authority

Original feedback metadata (`sources/wiki-247734813/r1/metadata.json:2–10`) retains its **2026-10-16** capture, external page version **11**, and flattened text/links limitation. The new index has a distinct source ID, directory and later timestamp. Neither it nor r25 claims a new page-body capture or backdates index coverage.

D-043 (`decisions.md:9`) permits the separate index/provenance repair, not attachment bytes. Structural body repair remains conditional on a concrete table-sensitive owner question. r25 preserves that boundary and leaves the accepted historical snapshot intact.

## Actual limits

- The **42 unchanged page packets** are carried forward from accepted accounting; no new packet is added by this repair. I did not reopen or hash all 42 packets or compare a historical committed range.
- The audit-scoped working-tree check showed no changes against reviewer-launch HEAD. This does **not** verify pre-launch committed changes or historical byte identity.
- Browser acquisition, origin/DOM guards, HTTP observation and capture time are parent-recorded provenance, not independently observed here. The selected-projection SHA-256 in metadata remains parent-attributed and was not recomputed.
- No attachment bodies, raw response, full-page structure, attachment versions, external freshness, exhaustive linked assets, semantic acceptance or runtime behavior were verified.
- Only local reads, a targeted search, listing and working-tree inspection were used. No shell, browser/network/storage/credentials access, requests, downloads, source execution, code inspection, tests/build/E2E, nested delegation or repository edits occurred.

Acceptance resolves only this five-entry index repair’s accounting review. It grants no new acquisition or product authority. **Global progress remains 6/28; tasks 2.3, 2.4 and 2.6 remain open.**