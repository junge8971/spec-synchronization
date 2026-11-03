# R-G1-ROOT-REGISTRY-FINAL-INCREMENT

## Review

**Decision: ACCEPT — bounded incremental accounting, with verification limits stated below.**

No issues found.

- **Correct:** The 42-row ledger, preserved D033 baseline, nine increments, attachment accounting, correction lineage and remaining permission gates agree with the inspected evidence.
- **Fixed:** None; read-only review.
- **Mandatory corrections:** None.
- **Merge verdict:** OK with notes. Three baseline packet projections and four byte measurements are parent-attributed, not independently recomputed by this reviewer. Acceptance does not close semantic, owner, implementation or global gates.

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

## Accounting verified

Read the complete target report and both work-items, the historical delta report/review, root r2 hrefs/metadata, decisions D027–D042 and coverage r13–r24. Compared all 42 ordered ledger IDs against `sources/wiki-238324523/r2/links.txt:1–42`, and their versions against actual canonical metadata fields.

| Check | Result |
|---|---|
| Ordered membership | All 42 ledger IDs match the existing root href ordering; no substitution by similar title. |
| Canonical packets | 42 present, zero absent; local r1 distinguished from external wiki version. |
| Historical D033 snapshot | Preserved: 18 captured, 24 absent, 17 indexes, 25 entries = four saved + 21 unread. |
| Subsequent increments | 24 packets and 24 indexes across nine increments. |
| Current indexes | 41; feedback 247734813 remains without an index. |
| Indexed entries | 34 across twelve nonempty parents. |
| Saved versus unread | Four saved inert prototype texts; 30 indexed bodies without matching canonical attachment content files in the inspected namespace. |
| Body formats | 40 `bodyView` packets, including three accepted containers; one selected image-only extraction and one flattened feedback extraction. |
| Readable derivatives | 37 exact root-member derivative metadata references; zero additional pages. |

For body/index totals, direct canonical field inspection covers 37 `bodyView` packets and their applicable indexes. Three older single-line packets use the separately supplied parent projection, as disclosed below.

### Nine increments

Each increment’s IDs, versions and index counts agree with its canonical records and coverage receipt.

| Receipt | Added IDs | Packets/indexes added | Entries added |
|---|---|---:|---:|
| r14 | 238347066, 238352321, 241074633 | 3/3 | 0 |
| r16 | 245670575, 241080643, 241083649, 241080071 | 4/4 | 0 |
| r17 | 238350232, 241080082 | 2/2 | 0 |
| r18 | 247747489, 241080088 | 2/2 | 2 |
| r19 | 247744768, 241080097 | 2/2 | 2 |
| r20 | 247728705, 241080065 | 2/2 | 0 |
| r21 | 250794931, 241080068, 241080080 | 3/3 | 0 |
| r22 | 247737907, 247742436 | 2/2 | 5 |
| r23 | 241102892, 238329164, 238333356, 241080100 | 4/4 | 0 |

Thus **18+24=42 packets; 17+24=41 indexes; 25+9=34 entries; 21+9=30 unread**. r15 and r24 supply dispositions, not additional packets. No historical count needs correction.

## Index and attachment checks

Directly inspected the ten nonempty ordinary JSON indexes at their cited `content.json:13–69` or shorter ranges, the overview Markdown index, and the parent-projected legacy skills index.

| Parent | Verified indexed IDs |
|---|---|
| 241092173 | 241105744, 241105743, 243764790, 243764789, 243764775, 243764773, 243764772, 243764759 |
| 241076726 | 241078199, 241078198 |
| 245678373 | 245678191 |
| 241077052 | 241080074, 241080073 |
| 241080062 | 245672060 — parent-projected legacy index |
| 243765248 | 245678564, 245678561, 245678560, 245678554, 245678553, 245678547, 245678536 |
| 247747489 | 250803776, 247747482 |
| 247744768 | 250800324, 247744753 |
| 247737907 | 250792853, 247746706, 247737899 |
| 247742436 | 250800308, 247742415 |
| 247751846 | 250805153, 247751845 |
| 247747363 | 250800526, 247747361 |

Enumerated results agree with saved sizes; all 41 saved indexes indicate `next: null`. This establishes no indicated continuation in those responses, not present external completeness.

`sources/wiki-241077052/r1/content.md:8–25` explicitly records selected image-only structure and a two-entry index, not original HTML/JSON. Journal’s separate empty index is in `sources/wiki-250781168/r1/metadata.json:14–22`; its canonical body has both `bodyView` and `bodyStorage`.

Feedback’s canonical top-level fields contain flattened text and links, not an attachment index or structural body. `sources/wiki-247734813/r1/content.json:12` is a prototype discovery edge, correctly excluded from the 34-entry population.

Directly read all four attachment metadata objects and checked content-file existence:

| Attachment | Parent | Version | Saved decoded-text bytes |
|---|---|---:|---:|
| 250805153 | 247751846 | 1 | 121187 |
| 247751845 | 247751846 | 1 | 77132 |
| 250800526 | 247747363 | 2 | 106202 |
| 247747361 | 247747363 | 1 | 249285 |

**Byte measurements are parent-attributed.** They match the supplied measurement artifact, not a reviewer recomputation or wire-byte certification.

The untruncated `sources/wiki-attachment-*/**/*` listing returned these four packets only. None of the other 30 enumerated IDs had canonical attachment content files in that inspected namespace. This is not a whole-repository asset census or a claim that another analyst has never encountered related material.

D029 and the accepted historical ledger support selected ADP01–10/AAP01–11 review only. Four saved texts are not four wholly reviewed attachments; search-only, styling, unrelated-module and initialization exclusions remain intact. No prototype body was reopened or executed here.

## Derivatives and provenance

Checked 36 modern derivative `source` references and declared filenames against canonical IDs and local file listings. Added the legacy skills derivative, whose `metadata.json:5–13` uses `originalPath`, `originalMetadataPath` and `exactBodyChunks`, rather than `source`. Its complete metadata and listed chunk/readable-text paths were inspected. Total: **24 later + ten D031 + two dictionary/API + one legacy skills = 37**.

No derivative digest, concatenation equality or HTML structure was recomputed. Off-root derivatives observed in listings were excluded from the 42-member accounting.

Root r1 contains `content.json` but no metadata in the inspected listing. Root r2 metadata records a separately timestamped v3 link extraction and expressly disclaims DOM/version alignment and retroactive provenance. The report preserves this limitation correctly.

## Accepted chains and authority

`reports/G1-ROOT-REGISTRY-FINAL-INCREMENT.md:95–120` agrees with decisions and coverage records:

- D032 preserves PLANNING’s original REVISE and corrected parent acceptance; analyst-local unread is not globally uncaptured. DATA/MPMM classifications remain bounded.
- D027–D029 retain dictionary correction provenance and selected prototype acceptance.
- D034–D037 retain accepted skill, dialogue, reports and system-state documentary findings.
- D038–D040 retain original REVISE verdicts and subsequent parent-verified citation/domain corrections. Admin-tools structural coverage belongs to the prior reviewer, not this review.
- D041 retains bounded KB/A-B acceptance and attachment/runtime exclusions.
- D042/r24 preserve the session qualifier correction and original REVISE, alongside access/roles ACCEPT. No fresh independent session ACCEPT is invented.

These are reused approved dispositions, not repeated semantic audits.

The feedback repair proposal at report lines146–148 matches the accepted historical ledger’s separate repair row: obtain index/provenance; preserve r1; collect structural body only for a table-sensitive owner need. It does **not** authorize attachment-body acquisition.

D031’s ten-page permission holds remain resolved. Attachment-body gates, no recursive traversal, no chronology precedence, and no new auth/grant/product/owner scope remain intact. The remaining overview, diagram and prototype candidates are explicitly conditional or permission-gated.

## Actual inspection limits

The reviewer used local reads, targeted searches, listings and manual comparisons/arithmetic. No parser/stat execution capability was available.

After identifying that limitation, the supervisor supplied `root-ledger-review-parent-projection.json`. Its complete contents were read:

- Parent-parsed packets 243776365, 241080062 and 245673187 report `bodyView` present, indexes **0/1/0**, `next: null`, and sole attachment **245672060**.
- Parent-measured lengths for the four saved texts match the table above.

The reviewer independently compared this projection with the report and accepted historical evidence, but **did not independently parse those three complete original JSON objects or measure the four files**. Their canonical file existence and metadata versions were checked directly. This narrow attribution is part of the acceptance boundary.

An initial brace-glob search returned no matches; exact-ID metadata searches superseded it. An initial derivative selector assumed the wrong reference prefix; inspecting the actual relative-path shape resolved it. One envelope search hit the output limit; a narrower follow-up covered the remaining selected records. Truncated HTML excerpts established field presence only, never complete-body review.

No hashes, roundtrips, original wire bytes, acquisition integrity, external freshness, concurrent-mutation exclusion or staging state were certified. No network/browser/storage/credentials access, requests, downloads, source execution, application-code inspection, tests/build/E2E, nested delegation or repository edits were performed by this reviewer.

**Global progress remains 6/28. Tasks 2.3, 2.4 and 2.6 remain open.** Acceptance covers this accounting artifact only; feedback/index, unread attachments, broader sources, semantic reconciliation, owners and implementation gates remain unresolved.