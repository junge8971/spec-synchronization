# G1-JIRA-SPECIAL-DOCUMENT-EDGES

## Result

Inspected **five bundles / five retained r1 revisions / 16 saved issue records** completely in their saved form. Found **one exact wiki reference occurrence, to already-accounted target241097511, and zero saved attachment entries**. Versus the accepted nine-bundle ledger: **one additional carrying-issue occurrence (MOS-909), zero distinct wiki-target additions, zero attachment-ID additions**. Feedback's comments and attachment indexes are absent, not empty.

No new graph, membership census, semantic audit, acquisition or closure. **Global6/28 unchanged; tasks2.3/2.4/2.6 remain open. Independent review pending.**

`A/` = `openspec/changes/reconcile-control-center-backlog/audit/`. Paths below are relative to A; JSON pointers are zero-based. “Complete” means all saved fields and adjacent metadata, not full remote issues. Source text was inert.

## Five-bundle coverage

Scoped path discovery found only the r1 content/metadata pair in each assigned directory. All five content files and all five metadata files were fully read, without remaining truncation.

| Alias / exact inspected source | Saved issues, in order | Fields / extraction limits |
|---|---|---|
| F `sources/jira-feedback/r1/content.json:1–114`; `metadata.json:1–11` | 12: MOS-1246,1231,1249,1250,1251,1254,1255,1256,1257,1258,1259,1260 | All `/items/0–11/description`, identity/status/update/subtask fields. **Comments and attachment indexes absent**, not zero. Selected-field extraction; custom acceptance fields absent. Metadata's requested fields do not establish a returned parent field. No exact document URL/attachment ID in saved descriptions. |
| L `sources/jira-MOS-909/r1/content.md:1–25`; `metadata.json:1–14` | MOS-909 | Full normalized description; returned attachment/subtask arrays reported empty, not retained raw arrays. Comments total2/startAt0/maxResults2:1122872 reduced MR excerpt;1122881 verbatim. Outbound MR URLs/personal attribution omitted; custom fields/changelog uncollected. One exact wiki URL. |
| D `sources/jira-MOS-1321/r1/content.json:1–31`; `metadata.json:1–20` | MOS-1321 | `/description`, `/attachments:[]`, `/subtasks:[]`; comments start0/max2/total2, records1129117 (omitted MR-body placeholder),1129414 (text). Selected fields, not full export. No exact documentary target. |
| R `sources/jira-MOS-1386/r1/content.json:1–31`; `metadata.json:1–20` | MOS-1386 | Same schema; empty attachments; comments1131237 (omitted MR-body placeholder),1131540 (text), start0/max2/total2. No exact documentary target. |
| T `sources/jira-MOS-1399/r1/content.json:1–31`; `metadata.json:1–20` | MOS-1399 | Same schema; empty attachments; comments1131561 (omitted MR-body placeholder),1131702 (text), start0/max2/total2. No exact documentary target. |

Finite totals: **12+1+1+1+1=16 records; eight comment records/excerpts/placeholders** across four bundles, four with reduced/omitted MR wording. F's12 records lack comments. Four issues have empty attachment arrays or an explicit selected-extraction statement thereof;12 have no index. Matching saved comment totals establishes only those selected response pages. Hidden fields/attachments, custom fields, omitted MR content and later revisions remain unknown. No separate remote-link index is retained; prose issue references do not authorize traversal.

## Carrying-issue membership: accepted rows only

No hierarchy/member-index packet or additional issue body was opened. These accepted rows identify carriers, **not requirements ownership**, product precedence or current status. Accepted membership totals were not recomputed.

| Inspected records | Exact accepted report rows/context reused |
|---|---|
| F all12, including module MOS-1246 | `reports/JIRA-MOS-1246.md:15–34`: module and11 member rows matching F order. |
| MOS-909 | `reports/JIRA-MOS-782.md:14–17,30`: H child12, member-index103. |
| MOS-1321, MOS-1399 | `reports/JIRA-MOS-1327.md:18–23`: children0/1, member-index138/139. |
| MOS-1386 | `reports/JIRA-MOS-1403.md:10–14`: assigned member, member-index145. |

Historical “Index only/uncollected” wording remains historical: actual specialized packets now supply selected description/comment/index evidence for these four issues. Custom/remote-link fields and omitted wording remain unavailable. Sources and old reports were not rewritten.

## Deduplicated documentary / attachment ledger

| Exact target | All carrying references in these five bundles | Overlap / retained state / accepted chain |
|---|---|---|
| Wiki **241097511** | **MOS-909**, L `content.md:13–14`: Contracts heading and exact href. Line25 repeats the local packet ID as provenance, not a second outbound edge. | **Repeated target, additional carrier only.** Canonical body `sources/wiki-241097511/r2/content.json` found locally; complete adjacent `metadata.json:1–51` read: exact ID, HTTP200, version6, capture2026-10-16T12:37:03.295Z, attachment count0/next null. Separate `attachments.json` exists; its contents/body coverage are reused from accepted chains, not re-audited. Earlier `r1/access-result.json` exists; r2 success does not explain prior404. |
| Jira attachments | **No saved entries/IDs** | **Zero observed overlap entries and zero additions**, not remote absence. F's absent indexes cannot be supplied from similarly named wiki attachments. No newly identified attachment body to classify as retained or missing. |

Exact observed inert href:

`https://wiki.mos-team.ru/spaces/KR/pages/241097511/API-%D0%BA%D0%BE%D0%BD%D1%82%D1%80%D0%B0%D0%BA%D1%82+%D1%80%D0%B5%D0%B5%D1%81%D1%82%D1%80%D0%B0+%D0%B4%D0%BE%D0%BC%D0%B5%D0%BD%D0%BE%D0%B2+%D0%B8+%D0%BA%D0%B0%D1%82%D0%B0%D0%BB%D0%BE%D0%B3%D0%B0+%D0%BD%D0%B0%D0%B2%D1%8B%D0%BA%D0%BE%D0%B2`

All prior carriers, reused from `reports/G1-JIRA-DETAIL-DOCUMENT-EDGES.md`, “Deduplicated wiki/document ledger,” and accepted `reviews/R-G1-JIRA-DETAIL-DOCUMENT-EDGES.md`, “Wiki references”: MOS-944/945/1018/1019/1020/1021/1022/1023/1025/1026/1027/1030/1031 (`jira-details-MOS-774 /items/5–17/description`), MOS-960 (`jira-sandbox-details /items/0/description`), MOS-905 (`jira-shell-details /items/5/description`). These **15 occurrences + MOS-909 =16** references to this target in the explicitly combined subset. Prior issue packets were not reopened.

Accepted retention chain: `reports/G1-API-COLLECTION-DELTA.md` → `reviews/R-G1-API-COLLECTION-DELTA.md` → **D-045**; accepted nine-bundle accounting: `reports/G1-JIRA-DETAIL-DOCUMENT-EDGES.md` → `reviews/R-G1-JIRA-DETAIL-DOCUMENT-EDGES.md` → **D-046** (`decisions.md:3–13`). This is neither a new acquisition nor a substitute dictionary/API registry. Exact ID establishes overlap; title/size does not.

Historical nine-bundle **13 wiki IDs /40 occurrences /23 Jira attachment IDs** remains an immutable accepted subset. A strictly scoped union retains13 wiki IDs and23 Jira IDs, with41 wiki occurrences; **not global all-sources counts**. The23 Jira entries must not be combined with root39 as a universal inventory. No new exact-ID documentary-body gap was found in these five saved packets.

## Locator-less references and excluded targets

| Exact field locator | Ambiguity / disposition |
|---|---|
| F `/items/1/description`, line21, MOS-1231 | Agreed model/OpenAPI without page/version/attachment locator. MOS-1142 is an issue dependency, not a new document target or traversal authority. |
| F `/items/2/description`, line30, MOS-1249 | “Contracts from12.10.2026,” transferred sources, aggregate OpenAPI/generated DTO: **no exact artifact URL/ID**. API-explanatory relevance plausible; date alone cannot identify a retained publication. |
| F `/items/6/description`, line66, MOS-1255 | HTML prototype without page/attachment ID. UI lane; API necessity not demonstrated. |
| F `/items/7/description`, line75, MOS-1256; `/items/10/description`, line102, MOS-1259 | Prototype status/behavior references without locator. No identity inferred from terminology. |
| F remaining descriptions, lines12,39,48,57,84,93,111 | Documentation/macets dashes or API/UI paths and issue dependencies; no additional exact documentary edge. Published rules, metadata, lookup and “API surfaces” do not identify standalone documents. |
| L `content.md:11`; D/R/T `/description`, each line7 | Prototype codes (L), OpenAPI/API-documentation/model references (D/R/T), model's14 check types (T): no additional document ID/version. Promised updates do not identify retained sources. |
| L comment1122872 `content.md:20`; D/R/T `/comments/items/0/body`, each line21 | MR/branch implementation provenance; exact outbound URLs **omitted/unavailable**, not visited. Cannot claim omitted text contains no further links. MR labels are not documentary identity or delivery proof. |
| L comment1122881 `content.md:21`; D/R/T `/comments/items/1/body`, each line27 | Completion/testing statements without document locator; not independently verified execution. |
| F API prefix and `/feedback`, `/catalogs`, `/saved-filters`; D `/managed-resources/catalogs`; R `/managed-resources/api`; T lookup GET path, all in descriptions | Business endpoint/UI/configuration references, not explanatory-document targets. No requests or semantic audit. R's base-URL/cURL fields describe data, not actual linked documents or executable instructions. |
| All source URLs/metadata request locators | Jira issue/API provenance, not additional documents. No standalone image/asset attachment URL saved in this set; F's missing indexes prevent an asset-absence claim. |

**Feedback identity boundary:** neither “HTML prototype” nor the bundle name binds MOS-1255 to wiki247734813 or any attachment. Reuse only `reviews/R-FEEDBACK-INDEX-REPAIR.md:24–65` and **D-044** (`decisions.md:15–19`): separate index parent247734813, IDs250790182/247746709/247739129/247737143/247734812, no bodies/versions or new download authority. These are **not five Jira-discovered additions**. Equal title/size/date is not identity. Final root ledger's historical42/41/34 is superseded for index accounting by D-044's42 packets/42 indexes/39 entries (4 saved texts+35 unread bodies), not by this inspection. Feedback structural repair remains conditional on a concrete table-sensitive question.

## Task2.4 and authority

1. MOS-909's explicit API-explanatory contract is already retained: no duplicate collection requirement, current-version assurance or semantic/conformance acceptance follows.
2. MOS-1249's dated contracts and MOS-1399's model/documentation could matter to a precise explanatory question. Saved fields lack exact locators. First determine whether existing accepted evidence answers that concrete question; this report declares neither missing publication nor automatic model/prototype acquisition.
3. Missing feedback comment/index fields and reduced MR bodies are coverage limits, not inaccessible pages or mandatory refreshes. UI prototypes and implementation links are other lanes or unknown API necessity. **No newly demonstrated mandatory task2.4 acquisition** results from these five packets.
4. **Team241080659:** D-046 already accepts relevance and existing documentary source authority. Current task handoff reports **transport timeout before GET**, not page403/404, inaccessible page or rejected authority. Do not duplicate collection or reopen settled relevance here. The overlapping target in this report is241097511, not241080659.
5. Preserve prior separate dispositions for user238347672, dashboard241095761, audit241077434, login/session241079770 and ambiguous shell223087110/222659162. They are not new five-bundle edges or automatic visits. No auth/product/source-precedence policy changes.
6. D-045 original API-r1 discovery remains independently unverified. Root/index counts, absent `externalDocs` or this lane's completion cannot close task2.4. Equally, no blanket all-attachment/all-root/all-code prerequisite is imposed.

## Code Context

### Files Retrieved

- Five complete content/metadata pairs and exact ranges: coverage table.
- `work-items/G1-JIRA-SPECIAL-DOCUMENT-EDGES.md:1–14`; accepted membership report ranges: membership table.
- Complete `reports/G1-JIRA-DETAIL-DOCUMENT-EDGES.md` and `reviews/R-G1-JIRA-DETAIL-DOCUMENT-EDGES.md`: accepted comparison ledger, no renewed primary-source audit.
- Complete `reports/G1-API-COLLECTION-DELTA.md` and `reviews/R-G1-API-COLLECTION-DELTA.md`; `decisions.md:1–19`: D-044/045/046.
- `sources/wiki-241097511/r2/metadata.json:1–51`, complete; body/index/r1-failure path discovery only.
- `reports/G1-ROOT-REGISTRY-FINAL-INCREMENT.md:1–65`; complete `reviews/R-FEEDBACK-INDEX-REPAIR.md:1–76`: historical/repaired accounting and identity limits, not root census.

### Key Evidence / Architecture

Saved issue field → exact ID → canonical metadata/body path → accepted report/review/decision. Presence, membership, retention, semantics, authority and runtime proof are separate. No application code inspected.

### Start Here

L `content.md:13–14` and `sources/wiki-241097511/r2/metadata.json`: the sole exact documentary edge is already retained and overlaps D-046. The coverage table identifies what F's extraction cannot establish.

## Validation and residual risks

Only local read/find/scoped grep and the sole report write. Manually reconciled16 records,8 selected comment records,1 exact wiki occurrence and0 attachment entries. Truncated decision search previews were resolved by complete `decisions.md:1–19` reads. Follow-up source-tail reads corrected D/R/T comment line citations, wiki metadata length and assignment length; no primary field remains unread. Membership conclusions use only accepted rows, not ancillary historical narrative returned by search.

No hashes recomputed, staging checked, historical byte-preservation or acquisition safeguards attested. Metadata HTTP/time/hash claims remain prior-capture attribution; current team transport state is handoff-attributed. No browser/network/storage/credentials/requests/downloads/source execution/rendering/code/tests/build/E2E/nested delegation. Only this report intentionally written; sources/tasks/decisions/owner plans untouched. Risks: selected omissions, locator-less identity, external freshness, historical provenance and pending independent review.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Five specialized bundles fully inspected in saved form:16 issues,8 selected comment records,one overlapping wiki occurrence,zero saved attachment entries;accepted membership rows and explicit identity/authority limits documented."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/G1-JIRA-SPECIAL-DOCUMENT-EDGES.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read/find/scoped grep","result":"passed","summary":"Complete five content/metadata pairs and accepted comparison evidence read;finite counts manually reconciled and source line citations corrected."},
    {"command":"Network/browser/downloads/source execution/code/tests/build","result":"not-run","summary":"Forbidden and unnecessary for this documentary-only task."}
  ],
  "validationOutput": ["MOS-909 adds one carrying occurrence of retained241097511;zero distinct wiki/attachment additions versus accepted nine-bundle ledger.","Feedback12 records lack comment/attachment fields;not zero.Global6/28 unchanged."],
  "residualRisks": ["Selected fields/omitted MR wording cannot establish full remote coverage.","Locator-less contracts/models/prototypes cannot be identified by title/date.","External freshness and historical acquisition/hashes unverified;independent review pending."],
  "diffSummary":"Only assigned report written;no source/spec/task/decision/owner-plan edits.",
  "reviewFindings": ["No new mandatory task2.4 acquisition established;team241080659 authority/relevance preserved and transport timeout distinguished from page failure."],
  "manualNotes":"Membership reused only from accepted report rows.No staging attestation.No semantic audit or blanket prerequisites.Independent review precedes acceptance."
}
```
