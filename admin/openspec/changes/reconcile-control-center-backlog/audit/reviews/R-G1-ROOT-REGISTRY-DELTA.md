# R-G1-ROOT-REGISTRY-DELTA

## Review

**Decision: ACCEPT — incremental accounting and provenance only.**

No issues found.

- **Correct:** The established 42-ID ledger, fourteen additions, attachment accounting, historical acceptance distinctions and nine remaining batches are supported by the inspected local evidence.
- **Fixed:** None; read-only review.
- **Required corrections:** None.
- **Merge verdict:** OK for this ledger artifact only. No semantic, implementation or global-task acceptance follows.

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

## Independently verified accounting

Compared the complete target report and original work-item with the accepted baseline, root r1 ID records and r2 hrefs. This reused established membership rather than conducting a new census.

| Check | Result |
|---|---|
| Ledger identity | All 42 ordered IDs and baseline labels match `sources/wiki-238324523/r1/content.json:8–49`; href locators match `r2/links.txt:1–42`. |
| Baseline captures | Four: 243776365, 241080062, 245673187, 247734813. |
| Additions | Ten D031 pages plus 241077052, 250781168, 247751846 and 247747363: **14**. |
| Current canonical coverage | **4 + 14 = 18** captured; **42 − 18 = 24** absent. Canonical files were present for the captured IDs; all 24 missing IDs were absent from the inspected source-directory listing. |
| Returned indexes | **18 − feedback = 17**. Fourteen additions have exhausted returned indexes; three unchanged baseline indexes are reused from accepted baseline evidence. |
| Known indexed entries | **8 + 2 + 1 + 7 + 2 + 1 + 2 + 2 = 25**. |
| Saved attachment bodies | Four inert prototype texts, with matching parent IDs and versions **1/1/2/1**. |
| Unread indexed bodies | **18 D031 + 2 overview + 1 skills SVG = 21**; **4 + 21 = 25**. |

All fourteen changed metadata files were read directly. Their IDs, retrieval timestamps, external versions and content filenames match the report’s provenance table. All ten D031 records also match `collection-D031-held-pages.json`.

Direct index-field inspection covered the twelve new ordinary page packets: `sources/wiki-ID/r1/content.json:13–18`, plus their attachment IDs where nonempty. Overview evidence is in `sources/wiki-241077052/r1/content.md:8–25`; journal’s zero-entry index is in `sources/wiki-250781168/r1/metadata.json:14–22`.

The report correctly separates:

- Full saved `bodyView` fields from full semantic inspection.
- Journal `bodyView`/`bodyStorage` from its separately acquired index.
- Overview’s selected image-only extraction from original HTML and unread image content.
- Three containers from substantive or mixed relevance classifications.
- Flattened feedback extraction from structural body evidence and an attachment index.
- Readable derivatives, attachment packets and off-root pages from direct-root page coverage.

The feedback prototype at `sources/wiki-247734813/r1/content.json:12` remains a discovery edge, not an enumerated attachment population. Four prototype `content.txt` files exist; their metadata establishes inert decoded text, not independently verified wire bytes.

## Nine remaining batches

Independently compared each batch with the missing ledger rows and saved root href positions.

| Batch | Exact IDs | Root r2 href lines |
|---|---|---|
| Skills | 238347066, 238352321, 241074633 | 5, 6, 7 |
| Dialogs | 245670575, 241080643, 241083649, 241080071 | 2, 8, 9, 31 |
| Auth/access | 241102892, 238329164, 238333356, 241080100 | 11, 37, 38, 34 |
| Optional | 247737907, 247742436 | 20, 25 |
| Reports | 238350232, 241080082 | 10, 33 |
| System state | 247747489, 241080088 | 21, 28 |
| Templates/stubs | 247744768, 241080097 | 22, 35 |
| Teams/surfaces | 247728705, 241080065 | 29, 30 |
| Admin tools | 250794931, 241080068, 241080080 | 26, 32, 36 |

**3 + 4 + 4 + 2 + 2 + 2 + 2 + 2 + 3 = 24**, with no duplicate or already captured ID. Each batch contains at most four pages.

Feedback repair, **247734813 / line 19**, is correctly separate. No duplicate root, journal, overview, dictionary/API or D031 capture is proposed. Rechecking packet presence before collection remains necessary.

## Historical versus accepted state

Read `decisions.md:3–95`, coverage revisions r7–r13, the D031 receipt, both D031 reviews, corrected PLANNING report and selected prototype coverage declarations.

- **Root:** r1 metadata remains absent. `sources/wiki-238324523/r2/metadata.json:5–15` establishes a separately timestamped v3 link extraction and empty index, not retroactive r1 provenance or fresh full-root-body coverage.
- **D031/D032:** All ten former holds are resolved for bounded documentary collection/classification. Receipt and metadata “pending” wording is historical.
- **PLANNING:** The original reviewer **REVISE** remains intact. Corrected `reports/REL-D031-PLANNING-API.md` explicitly distinguishes analyst-unread from globally uncaptured and routes the three known captured children. D032 records parent acceptance after correction, not a new reviewer ACCEPT.
- **DATA/MPMM:** Accepted relevance classifications remain distinct from complete requirements, diagram or contract reconciliation.
- **Journal:** D024/D025 and r7/r8 establish five documentary row dispositions without downstream closure.
- **Dictionary/prototypes:** D027/D028 retain correction history; D029/r11 supersede wholly-unread prototype statements only for selected findings. Prototype coverage declarations preserve unread/unassessed regions and do not establish rendered behavior.
- **Transport:** r13 records discovery timeout before any skill-page request. It supports neither HTTP403/404 nor an inaccessible-page classification.
- **Authority:** D031’s attachment-download prohibition is retained. Direct-root documentary authority does not activate auth models, optional features, recursive traversal or implementation.

Tasks **2.3, 2.4 and 2.6** remain explicitly open; accepted recorded progress remains **6/28**. This ledger does not close Jira-linked, attachment, explanatory-document, owner-decision or implementation-mapping gaps.

## Snapshot and verification limits

**Cutoff:** the local evidence returned during this review, ending with a repeated `sources/` directory listing. Both listings agreed for the established root IDs; no later root capture was observed. The latest capture timestamp in the fourteen-addition table is **2026-10-19T09:37:21.481Z**. That is a source timestamp, not an invented reviewer wall-clock timestamp or filesystem freeze.

Counts are accepted for this inspected snapshot. A subsequent collector addition would require a dated ledger update, not retroactively make this arithmetic wrong. Concurrent file mutation and external freshness were not independently excluded.

Verification used local reads, listings and targeted searches, with manual ID comparison and arithmetic. No parser script, digest recomputation or derivative roundtrip check was executed. Long `bodyView` search results were truncated and used only to establish field presence, never full-body inspection. Baseline body/index facts and prior semantic classifications were explicitly reused from accepted evidence.

One brace-glob metadata search returned no matches; all fourteen metadata files were subsequently read individually. No conclusion relies on that search result.

Repository staging state was **not inspected**. The target correctly omits an empty-index attestation; “staged nothing” describes activity, not repository state. This reviewer makes no `noStagedFiles` assertion.

No edits, network/browser/MCP access, credentials, source execution/rendering, application-code inspection, tests/build/E2E, nested delegation, semantic reaudit, global inventory or task closure occurred. Hash, acquisition and original-byte claims remain attributed to saved metadata and prior accepted reports.