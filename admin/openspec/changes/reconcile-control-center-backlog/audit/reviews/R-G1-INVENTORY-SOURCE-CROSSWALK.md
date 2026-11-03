# R-G1-INVENTORY-SOURCE-CROSSWALK

## Review

**Decision: REVISE — one narrow locator qualification.**

- **Correct:** All26 accepted module reports were read completely. All157 direct keys and16 nested keys are represented once, with matching membership, baseline records and nested parents. Later issue-detail joins and field limitations match the accepted detail/special ledgers.
- **Fixed:** None; read-only review.
- **Finding: P2 — feedback hierarchy order is asserted beyond the inspected accepted evidence.** `reports/G1-INVENTORY-SOURCE-CROSSWALK.md:51,86` derives every exact H child position from member-table order, including feedback. However, `reports/JIRA-MOS-1246.md:15–34` establishes membership equality and lists **feedback packet** records/line ranges; it does not explicitly establish hierarchy child-array order. The special ledger/review establishes F order, not H child order. This is an unsupported exact-pointer inference, **not a demonstrated membership mismatch**.
- **Smallest fix:** Exempt feedback from the order-derived H child-position claim. Preserve its accepted hierarchy membership evidence at `JIRA-MOS-1246.md:10–19` and exact F(1–11) detail pointers; state that individual feedback H child positions were not independently established from the consulted accepted reports. Alternatively cite an already-accepted receipt explicitly establishing those positions. No primary graph census or new collection is necessary.
- **Merge verdict:** **OK with notes for bounded accounting after that qualification; REVISE the current exact-locator claim.** No replacement crosswalk is needed.

`C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `C/audit`. Paths below are relative to A unless stated otherwise.

## Actual row coverage

Compared every direct and nested row with its complete accepted inventory report, not primary hierarchy/member-index/subtask bodies.

| Module | Accepted report read completely | Direct / nested | Verified baseline records |
|---|---|---:|---|
|624|`reports/JIRA-MOS-624.md:1–69`|29/1|I0–28; S0|
|651|`reports/JIRA-MOS-651.md:1–45`|5/0|I29–33|
|652|`reports/JIRA-MOS-652.md:1–68`|4/0|I34–37|
|768|`reports/JIRA-MOS-768.md:1–85`|4/0|I38–41|
|769|`reports/JIRA-MOS-769.md:1–38`|2/0|I42–43|
|770|`reports/JIRA-MOS-770.md:1–38`|0/0|Explicit observed empty children|
|771|`reports/JIRA-MOS-771.md:1–55`|1/1|I44; S1|
|772|`reports/JIRA-MOS-772.md:1–35`|0/0|Explicit observed empty children|
|773|`reports/JIRA-MOS-773.md:1–69`|11/5|I45–55; S2–6|
|774|`reports/JIRA-MOS-774.md:1–55`|18/3|I56–73; S7–9|
|775|`reports/JIRA-MOS-775.md:1–49`|3/0|I74–76|
|776|`reports/JIRA-MOS-776.md:1–51`|1/0|I77|
|777|`reports/JIRA-MOS-777.md:1–46`|5/0|I78–82|
|778|`reports/JIRA-MOS-778.md:1–39`|6/0|I83–88|
|780|`reports/JIRA-MOS-780.md:1–59`|1/0|I89|
|781|`reports/JIRA-MOS-781.md:1–36`|1/0|I90|
|782|`reports/JIRA-MOS-782.md:1–67`|25/0|I91–115; AD0/1 supplemental|
|783|`reports/JIRA-MOS-783.md:1–72`|18/5|I116–133; S10–14; AD2/3 supplemental|
|784|`reports/JIRA-MOS-784.md:1–55`|4/1|I134–137; S15|
|788|`reports/JIRA-MOS-788.md:1–55`|0/0|Explicit observed empty children|
|1246|`reports/JIRA-MOS-1246.md:1–52`|11/0|F1–11; F0 separate parent|
|1327|`reports/JIRA-MOS-1327.md:1–44`|2/0|I138–139|
|1328|`reports/JIRA-MOS-1328.md:1–57`|2/0|I140–141|
|1329|`reports/JIRA-MOS-1329.md:1–53`|2/0|I142–143|
|1388|`reports/JIRA-MOS-1388.md:1–35`|1/0|I144|
|1403|`reports/JIRA-MOS-1403.md:1–44`|1/0|I145|

The table covers **146 I records +11 F members =157 direct rows**, and **S0–15 =16 nested rows**. All module counts match `inventory-acceptance.json`; complete `inventory-reconciliation.json` supplies accepted aggregate membership verification. These are report comparisons, not independently recomputed primary-source sets or hashes.

For non-feedback modules, the inventory reports explicitly provide H positions or state that their table follows H child order. The feedback qualification above is the only exact-H-order support gap identified.

### Nested links

Verified each stub position, detail position and saved parent:

- I5/subtasks/0 → S0 MOS1053 → MOS666.
- I44/subtasks/0 → S1 MOS1150 → MOS816.
- I47/subtasks/0–4 → S2–6 MOS1411/1412/1414/1419/1422 → MOS1037.
- I57/subtasks/0–1 → S7–8 MOS1050/1051 → MOS676.
- I58/subtasks/0 → S9 MOS1052 → MOS677.
- I118/subtasks/0–4 → S10–14 MOS1110/1164/1165/1166/1167 → MOS709.
- I135/subtasks/0 → S15 MOS1054 → MOS705.

Saved selected descriptions, parent links, attachment indexes and empty further-subtask arrays do not establish hidden-subtask completeness or enrich the direct parents’ omitted descriptions.

## Later joins and field coverage

Read complete detail/special reports and their complete accepted reviews. Compared joins against their explicit issue-to-array-position coverage tables—not key sorting or metadata request-field order.

Verified:

- **SK0–18:** parent774 and all18 members; descriptions retained, comments omitted. Nine indexed attachments belong only to SK1–3.
- **SH0–5:** parent624 and members672/673/674/904/905; saved comment counts0/1/1/1/2/2 and nine indexed attachments agree.
- **AD0–3:** MOS1245/1306/1237/959 respectively; comments omitted; three plan indexes and MOS959’s explicit empty attachment array.
- **LC:** MOS1119 only, normalized description and two selected comment excerpts; exact833803 body accepted. Failed r1 does not fill MOS782/1120. J909 separately supersedes only MOS909’s failed-request gap.
- **MN0–3:** MOS775/1146/1397/1398; singular attachment arrays empty; saved comment counts0/1/0/0.
- **OP0–4:** MOS717/754/920/922/923, including the noncontiguous inventory ordering; empty attachments, two comments only for717.
- **RP0–5:** MOS777/885/916/919/1015/1016; empty attachments, one comment only for1015.
- **SB0–2:** MOS960/961/962, correctly joined to I25/I22/I24; empty saved comments and attachments.
- **SW0–1:** MOS776/1145; exact835759 accepted body remains distinct from historical unread wording.
- **F0–11:** correct module/member order and retained descriptions; comments/attachment fields omitted. P is later review of the same capture, not a new capture.
- **J909/J1321/J1386/J1399:** exact singleton paths, normalized/selected descriptions, empty attachment evidence and reduced/omitted MR wording match P.

Evidence: `reports/G1-JIRA-DETAIL-DOCUMENT-EDGES.md:15–31,72–103`, complete corresponding review; `reports/G1-JIRA-SPECIAL-DOCUMENT-EDGES.md:11–24`, complete corresponding review.

**U/N are appropriately bounded.** No later join was identified within these inspected ledgers/checkpoints/decisions. That does not establish global absence, irrelevance, remote denial or a requirement to fetch. Omitted fields remain unknown rather than zero. Parent detail remains separate from children; retained wiki contracts do not fill omitted issue fields. No overlapping population was subtracted from157.

## E12a — all20 attachment IDs

Compared every row with the six complete accepted inventories and the accepted disposition review’s exact-ID table.

**Independent path check:** two scoped `find` searches under `A/sources` used the explicit20-ID set plus833803:

1. Canonical `jira-attachment-<ID>/**`, all revisions.
2. Names containing any of those exact IDs.

Both returned only the833803 control. The canonical search returned its `r1/`, `content.md` and `metadata.json`; the name search returned its directory. No body was read.

In the following table:

- **Q:** no result for that ID in either scoped search.
- **J:** no later accepted exact-ID body join identified in the inspected records.
- **NB:** historical selected metadata-only capture; bodies not acquired there; this assignment provides no body-reading/download authority. Current necessity and semantics remain unknown.

| Owner | S attachment pointer | ID | Accepted identity/type limit | Path / later join / reason |
|---|---|---|---|---|
|1053|`/items/0/attachments/0`|826713|404.png; image/png|Q / J / NB|
|1150|`/items/1/attachments/0`|831194|JSON response; application/json|Q / J / NB|
|1150|`/items/1/attachments/1`|831195|Screenshot_4.png; image/png|Q / J / NB|
|1411|`/items/2/attachments/0`|839653|Type not reproduced in accepted report|Q / J / NB|
|1412|`/items/3/attachments/0`|839662|Same type limit|Q / J / NB|
|1414|`/items/4/attachments/0`|839675|Same type limit|Q / J / NB|
|1419|`/items/5/attachments/0`|839862|Same type limit|Q / J / NB|
|1422|`/items/6/attachments/0`|839906|Same type limit|Q / J / NB|
|1422|`/items/6/attachments/1`|839905|Same type limit|Q / J / NB|
|1050|`/items/7/attachments/0`|826531|Type not reproduced in accepted report|Q / J / NB|
|1050|`/items/7/attachments/1`|826530|Same type limit|Q / J / NB|
|1051|`/items/8/attachments/0`|826544|Same type limit|Q / J / NB|
|1110|`/items/10/attachments/0`|829292|2909.png; filename evidence only|Q / J / NB|
|1164|`/items/11/attachments/0`|832277|1.png; filename evidence only|Q / J / NB|
|1165|`/items/12/attachments/0`|832288|2.png; filename evidence only|Q / J / NB|
|1166|`/items/13/attachments/0`|832305|3.png; filename evidence only|Q / J / NB|
|1167|`/items/14/attachments/0`|832324|4.png; filename evidence only|Q / J / NB|
|1167|`/items/14/attachments/1`|832323|5.png; filename evidence only|Q / J / NB|
|1054|`/items/15/attachments/0`|835960|MOV; video/quicktime|Q / J / NB|
|1054|`/items/15/attachments/1`|835961|MP4; video/mp4|Q / J / NB|

**MOS1052:** `/items/9/attachments` is explicitly empty; it is not an omitted field or a twenty-first attachment.

JSON831194 is not screenshot-only. No MIME was inferred from filenames where the accepted report did not reproduce it. Videos remain index-only; no playback or semantic claim.

Read repository `.gitignore` and `.git/info/exclude`; the latter includes `/openspec/`. The discovery tool nevertheless returned the retained positive control. Tool visibility and ignore behavior therefore remain explicit limitations: these results support only scoped non-discovery, not global absence or absence of unbound/hidden copies.

No sum with root39, finite Jira23 or off-root session4 was made.

## Supersession and gate boundaries

Verified the named thirteen-target retention progression against the complete contract-collection report/review, D043–058 and collection checkpoint:

- Team241080659: D048.
- Dashboard241095761: D049, preserving metrics original REVISE and parent locator corrections.
- Audit241077434: **D050 accepted without report edit**, original REVISE retained.
- Shell223087110/222659162: D052/053, relevance/context without adopted shell requirements.
- User238347672/session241079770: D055/056, original REVISE and two parent corrections retained.

The six earlier retained targets and MOS909’s additional241097511 occurrence remain consistent with the accepted **finite13-target/41-occurrence** ledger. This is named documentary supersession, not global completeness or renewed semantic acceptance. No18-finding auth analysis was repeated.

**E12:** row-complete bounded accounting is supported, subject to the single feedback H-order qualification.

**E12a:** ready for acceptance as exact-ID index/no-body accounting with explicit visibility and uncertainty limits. No further generic crosswalk or automatic acquisition is warranted.

**E13 remains separate/open.** `source-checkpoint-r1.json:364–366` excludes saved-body links from its root-only enumeration. This review does not close that boundary.

**G1/source sufficiency and task checkboxes remain parent decisions. Tasks2.3/2.4/2.6 remain open; global6/28 unchanged.**

## Inspection record and limitations

Read completely:

- Target363-line crosswalk and both crosswalk assignments.
- Inventory acceptance/reconciliation.
- All26 inventory reports listed above.
- G1 disposition report/review.
- Detail, special and contract-collection ledgers and their corresponding reviews.
- `C/design.md`, `C/tasks.md`, governing reconciliation spec.
- `coverage-partial-r41.json`, `source-checkpoint-r2.json`, `collection-checkpoint.md`.
- Repository `.gitignore` and `.git/info/exclude`.

Read targeted ranges:

- `decisions.md:1–110`.
- `source-checkpoint-r1.json:1–110,350–366`.

Later source-specific semantic reports and their original reviews were not independently re-audited; acceptance lineage was checked through the accepted ledgers/reviews and decisions. Other uninspected receipts cannot be excluded globally.

Only local reads, scoped discovery and manual comparison were performed. No primary Jira graph census, source/attachment body reading, metadata-field inference from key order, external requests, credentials, downloads, execution, code/tests/build/E2E, nested delegation or repository edits. No hashes, historical acquisition safeguards, external freshness or staging state were independently certified.