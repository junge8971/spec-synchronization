# R-G1-JIRA-SPECIAL-DOCUMENT-EDGES

## Review

**Decision: ACCEPT — bounded saved-reference accounting only.**

No issues found.

- **Correct:** Five complete saved source pairs support16 issue records, eight comment records/excerpts/placeholders, one overlapping wiki occurrence and zero saved attachment entries.
- **Fixed:** None; read-only review.
- **Mandatory corrections:** None.
- **Merge verdict:** OK with notes. Acceptance does not establish full remote-issue coverage, explanatory sufficiency, acquisition authority or task closure.

`A/` = `openspec/changes/reconcile-control-center-backlog/audit/`. Paths below are relative to A; JSON pointers are zero-based.

## Actual independent coverage

Read the complete target report and both assignments. Scoped file discovery returned only one retained r1 content/metadata pair for each assigned bundle. Read all ten files completely, without remaining truncation.

| Source under `sources/` | Complete content / metadata | Issue records | Comments | Attachment evidence |
|---|---|---:|---|---|
| `jira-feedback/r1` | `content.json:1–114`; `metadata.json:1–11` | 12 | Fields absent | Index fields absent |
| `jira-MOS-909/r1` | `content.md:1–25`; `metadata.json:1–14` | 1 | Two selected records | Explicit extraction statement: returned array empty |
| `jira-MOS-1321/r1` | `content.json:1–31`; `metadata.json:1–20` | 1 | Two records, including omitted-body placeholder | `/attachments: []`, line10 |
| `jira-MOS-1386/r1` | Same ranges | 1 | Two records, including omitted-body placeholder | `/attachments: []`, line10 |
| `jira-MOS-1399/r1` | Same ranges | 1 | Two records, including omitted-body placeholder | `/attachments: []`, line10 |

Verified **12+1+1+1+1=16 records**. Feedback contains MOS-1246,1231,1249,1250,1251,1254,1255,1256,1257,1258,1259,1260, in that order.

The eight saved comment records/excerpts/placeholders are:

| Issue | IDs and exact content locators |
|---|---|
| MOS-909 | 1122872 at `content.md:20`;1122881 at line21 |
| MOS-1321 | 1129117 and1129414; `/comments/items/0/body` at line21 and `/comments/items/1/body` at line27 |
| MOS-1386 | 1131237 and1131540; same pointers/lines |
| MOS-1399 | 1131561 and1131702; same pointers/lines |

Each of these four issues records startAt0/maxResults2/total2. MOS-909 retains one reduced MR excerpt and one verbatim comment; the other three retain one omitted automated-MR-body placeholder each. Thus four records have reduced/omitted MR wording.

These are selected or normalized extractions, not full remote issues. Matching comment totals establishes only the retained selected response pages. Feedback’s12 issues have **absent comments and attachment indexes—not zero comments or demonstrated empty indexes**. Requested `parent` in feedback metadata is not a returned parent field. Custom fields, remote-link indexes, omitted MR URLs/content, hidden material and later revisions remain outside coverage.

## Sole exact documentary edge

Verified the report’s exact percent-encoded href against `sources/jira-MOS-909/r1/content.md:14`, following the Contracts heading at line13. Its target is **241097511**.

Line25 mentions the local historical packet `wiki-241097511/r2` as provenance; it is **not a second outbound edge**. No other exact documentary URL or attachment ID occurs in the five bundles’ retained reference-bearing fields. This negative conclusion does not extend to omitted content.

Scoped path discovery confirmed:

- `sources/wiki-241097511/r2/content.json`
- `sources/wiki-241097511/r2/attachments.json`
- `sources/wiki-241097511/r2/metadata.json`
- Earlier `sources/wiki-241097511/r1/access-result.json`

Read the complete r2 metadata, lines1–51. It identifies exact source241097511, recorded HTTP200, version6, capture **2026-10-16T12:37:03.295Z**, and attachment count0/next null. Its `priorAttempt` explicitly preserves the unexplained earlier404. Successful r2 retention does not explain or erase that failure.

The wiki body, separate attachment index and earlier failure receipt were not reopened; their accepted dispositions were reused. HTTP observation, capture time, hash, bytes and acquisition safeguards remain metadata/prior-chain attribution.

## Accepted comparison ledger reused—not re-audited

Read complete:

- `reports/G1-JIRA-DETAIL-DOCUMENT-EDGES.md`
- `reviews/R-G1-JIRA-DETAIL-DOCUMENT-EDGES.md`
- `reports/G1-API-COLLECTION-DELTA.md`
- `reviews/R-G1-API-COLLECTION-DELTA.md`
- `reviews/R-FEEDBACK-INDEX-REPAIR.md`
- `decisions.md:1–19`, covering D-046/D-045/D-044.

D-046 accepts the earlier finite nine-bundle ledger. Its241097511 row supplies15 prior occurrences:

- MOS-944/945/1018/1019/1020/1021/1022/1023/1025/1026/1027/1030/1031: `jira-details-MOS-774 /items/5–17/description`.
- MOS-960: `jira-sandbox-details /items/0/description`.
- MOS-905: `jira-shell-details /items/5/description`.

Adding MOS-909 produces **16 occurrences of this target** in the explicitly combined subset. The accepted historical **13 wiki IDs /40 occurrences /23 Jira attachment IDs** remains unchanged as its own subset; the scoped union is **13 wiki IDs /41 occurrences /23 Jira attachment IDs**.

Therefore this lane adds **one carrying occurrence, zero distinct wiki targets and zero attachment entries/IDs**. These are not global totals. None of the nine primary bundles was reopened or re-audited.

## Membership verification

Used only the specified accepted rows and necessary table context:

| Inspected carriers | Accepted report evidence |
|---|---|
| Feedback module and11 members | `reports/JIRA-MOS-1246.md:15–34` |
| MOS-909 | `reports/JIRA-MOS-782.md:14–17,30`: child12/member-index103 |
| MOS-1321 and MOS-1399 | `reports/JIRA-MOS-1327.md:18–23`: children0/1, indices138/139 |
| MOS-1386 | `reports/JIRA-MOS-1403.md:10–14`: index145 |

All16 identities match. No hierarchy/member-index source or additional issue body was opened, and no membership census or graph was constructed. Carrying-issue membership does not determine requirements ownership. Historical “Index only/uncollected” wording remains historical; the specialized packets now supply only their explicitly retained fields.

## Locator-less references and boundaries

Verified the report’s locators and conservative treatment:

- Feedback MOS-1231 `/items/1/description`, line21: agreed model/OpenAPI without an exact publication locator.
- MOS-1249 `/items/2/description`, line30: contracts dated12.10.2026, transferred sources, aggregate OpenAPI/generated DTO; no exact artifact URL/ID.
- MOS-1255 `/items/6/description`, line66: HTML prototype without an ID.
- MOS-1256 and MOS-1259 `/items/7/description`, line75, and `/items/10/description`, line102: prototype references without locators.
- MOS-909 `content.md:11`: prototype codes, not another document identity.
- MOS-1321/1386/1399 `/description`, line7: model/OpenAPI/documentation references without additional document locators. MOS-1399 explicitly names14 model check types without identifying their publication.
- MR excerpts/placeholders do not expose the omitted outbound URLs. Completion/testing statements are documentary assertions, not verified execution.
- API/UI paths, issue dependencies and metadata request locators are not new explanatory-document edges or traversal authority.

No date, filename or prototype wording binds these mentions to feedback wiki attachments. D-044’s separate parent247734813 and five indexed IDs250790182/247746709/247739129/247737143/247734812 remain accepted index evidence—not five Jira-discovered additions or attachment-body authority.

D-044’s **42 packets /42 indexes /39 entries =4 saved texts+35 unread bodies** remains separate accepted root accounting, not recomputed or combined with23 Jira IDs. Feedback structural repair remains conditional on a concrete table-sensitive question.

## Authority, task status and inspection limits

- D-046 already dispositions team241080659 relevance and existing documentary authority. The reported transport timeout **before GET** is handoff-attributed, not independently observed here and not a page403/404, authority rejection or new edge from these five bundles.
- User238347672, dashboard241095761, audit241077434, login/session241079770 and shell223087110/222659162 retain their separate prior dispositions; no automatic visits follow.
- D-045’s original API-r1 discovery remains independently unverified. No API/schema, root or application semantic audit was repeated.
- **No newly demonstrated mandatory task2.4 acquisition** follows from these five saved packets. This is not task2.4 closure or a completeness certificate. No blanket all-document/all-attachment/all-root/all-code prerequisite is introduced.
- Used only local read and file-discovery tools. No network/browser/storage/credentials access, requests, downloads, rendering, source execution, code inspection, tests/build/E2E, nested delegation or repository edits occurred.
- No hashes or byte measurements were recomputed; no staging, historical byte-preservation or another agent’s tool-use history was certified.

**Global progress remains6/28. Tasks2.3/2.4/2.6 remain open.**