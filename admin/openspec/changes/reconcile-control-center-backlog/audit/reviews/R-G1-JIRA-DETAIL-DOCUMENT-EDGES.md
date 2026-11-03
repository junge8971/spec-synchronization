# R-G1-JIRA-DETAIL-DOCUMENT-EDGES

## Review

**Decision: ACCEPT — bounded saved-reference accounting only.**

No issues found.

- **Correct:** Independently checked the nine bundles’ saved reference-bearing fields, metadata, carrying-issue memberships, exact wiki references and attachment indexes.
- **Fixed:** None; read-only review.
- **Mandatory corrections:** None.
- **Merge verdict:** OK with notes. This accepts finite documentary accounting, not explanatory sufficiency, acquisition authority or task closure.

`A/` = `openspec/changes/reconcile-control-center-backlog/audit/`. Source aliases below match the reviewed report. JSON pointers are zero-based.

## Independently inspected coverage

Read the complete target report and both assignments. Read all nine content packets below without remaining output truncation, including the single-line SK packet. Read every adjacent metadata file and lifecycle r1’s complete failure receipt.

| Alias / source under `A/sources/` | Content inspected | Saved issues | Comments/excerpts | Indexed attachments |
|---|---|---:|---:|---:|
| AD `jira-api-delta-scenarios/r1` | `content.json:1–71` | 4 | Fields absent | 3 |
| SK `jira-details-MOS-774/r1` | Complete `content.json:1` | 19 | Fields absent | 9 |
| LC `jira-lifecycle-details` | `r1/access-result.json`; `r2/content.md:1–67` | 1 | 2 selected excerpts | 1 |
| MN `jira-monitoring-details/r1` | `content.json:1–195` | 4 | 1 | 0 |
| OP `jira-operations-details/r1` | `content.json:1–121` | 5 | 2 | 0 |
| RP `jira-reports-details/r1` | `content.json:1–134` | 6 | 1 | 0 |
| SB `jira-sandbox-details/r1` | `content.json:1–70` | 3 | 0 | 0 |
| SH `jira-shell-details/r1` | `content.json:1–240` | 6 | 7 | 9 |
| SW `jira-skill-switch-details/r1` | `content.json:1–183` | 2 | 2 | 1 |
| **Total** | **Nine bundles, ten revisions** | **50** | **15 retained records/excerpts** | **23** |

Verified qualifications:

- AD/SK’s **23 issues have absent comment fields**, not demonstrated zero comments.
- LC r1 saved no payload. Requested MOS-782/909/1120 are not counted as inspected issue records. Timeout establishes neither HTTP status nor remote absence.
- LC r2 contains only MOS-1119’s selected/normalized description and two non-personal comment excerpts. Omitted MR URLs and original complete wording remain unavailable.
- Saved comment pagination starts at zero and captured counts equal reported totals. This establishes saved-page accounting, not hidden/current/full-Jira completeness.
- Custom fields, separate remote-link indexes, hidden attachments and later revisions remain outside coverage.

### Carrying-issue membership

Checked only authorized accepted membership rows and necessary context:

- `reports/JIRA-MOS-624.md:7–46`: module identity and SH/OP/SB member indices.
- `reports/JIRA-MOS-774.md:7–38`: module identity and all eighteen members, indices56–73.
- `reports/JIRA-MOS-775.md:9–25`: module and indices74–76.
- `reports/JIRA-MOS-776.md:14–18`: module and index77.
- `reports/JIRA-MOS-777.md:8–23`: module and indices78–82.
- `reports/JIRA-MOS-782.md:14–41`: MOS-1119/1245/1306 at indices108/113/114.
- `reports/JIRA-MOS-783.md:27–43`: MOS-959/1237 at indices126/130.

These support all **50 carrying-issue identities**. No hierarchy/member-index source was opened, no new graph was constructed, and membership was not interpreted as requirements ownership. MOS-773 rows were unnecessary for this independent mapping.

## Wiki references: 13 IDs / 40 occurrences

`D(n)` means `/items/n/description` in the indicated source alias. Each listed index represents an individually checked occurrence.

| Exact wiki ID | Verified locators | Occurrences | Canonical disposition |
|---|---|---:|---|
| 241082009 | AD D(3); SK D(17); SB D(0); SH D(5) | 4 | Retained r2, v5 |
| 241097511 | SK D(5–17); SB D(0); SH D(5) | 15 | Retained r2, v6 |
| 241085439 | SK D(16); RP D(4) | 2 | Retained r1, v15 |
| 241085838 | RP D(1–5) | 5 | Retained r1, v3 |
| 241088180 | OP `/items/0/comments/items/0/body`, comment1131251 | 1 | Retained r1, v4 |
| 241092242 | SK D(15); OP D(3,4) | 3 | Retained r1, v4 |
| 238347672 | SK D(5), MOS-944 | 1 | Scoped canonical gap |
| 241080659 | SK D(5,17), MOS-944/1031; SH D(5), MOS-905 | 3 | Scoped canonical gap |
| 241095761 | SK D(13,16), MOS-1025/1030 | 2 | Scoped canonical gap |
| 241077434 | SK D(17), MOS-1031 | 1 | Scoped canonical gap |
| 241079770 | SH D(4), MOS-904 | 1 | Scoped canonical gap |
| 223087110 | SH D(0), MOS-624 Documentation cell | 1 | Scoped canonical gap; relevance unknown |
| 222659162 | SH D(0), same cell | 1 | Scoped canonical gap; relevance unknown |
| **Total** | | **40** | **Six retained / seven gaps** |

The full saved hrefs and carrying issues agree with the target ledger. The last two IDs use `pages/viewpage.action?pageId=…`; the other eleven use the saved `/spaces/KR/pages/<ID>/…` form.

Independently read all six canonical `metadata.json` files. Exact identities, revisions and recorded versions match. Their attachment metadata records count0/next null. Also read both separate r2 `attachments.json` files: empty results, size0 and no continuation link.

Canonical content-path discovery under `A/sources/` found the six reported wiki packets and no exact-ID packet for the seven gaps. A scoped search of `**/metadata.json` found no matches for those seven IDs. This supports only the stated canonical-store gap—not global absence, inaccessibility, replacement identity or authorization.

The five explicit contract gaps remain distinct from the two unknown-relevance shell references. Similar titles do not substitute retained teams, dashboard, monitoring, auth or other documents.

## Jira attachments: 23 distinct IDs

Checked every indexed ID, filename, content URL, carrying issue and array position against the report.

| Source / pointer | Owner | Verified attachment IDs |
|---|---|---|
| AD `/items/0/attachments/0` | MOS-1245 | 839666 |
| AD `/items/1/attachments/0` | MOS-1306 | 839773 |
| AD `/items/2/attachments/0` | MOS-1237 | 839665 |
| LC `r2/content.md:59–63` | MOS-1119 | 833803 |
| SW `/items/1/attachment/0` | MOS-1145 | 835759 |
| SK `/items/1/attachments/0–2` | MOS-675 | 817149,825983,817148 |
| SK `/items/2/attachments/0–3` | MOS-676 | 817153,817152,826603,817151 |
| SK `/items/3/attachments/0–1` | MOS-677 | 817155,817154 |
| SH `/items/1/attachments/0–2` | MOS-672 | 817138,825952,817137 |
| SH `/items/2/attachments/0–2` | MOS-673 | 817141,826497,817140 |
| SH `/items/3/attachments/0–2` | MOS-674 | 817144,825968,817143 |

Confirmed **5 Markdown + 6 HTML + 12 PNG = 23**. Repeated image markup and test-plan comment references do not add attachment IDs.

Canonical path discovery found only these two corresponding saved Jira attachment bodies:

- `sources/jira-attachment-833803/r1/content.md`
- `sources/jira-attachment-835759/r1/content.md`

Read both adjacent metadata files completely. Their exact indexed URLs, identities and recorded capture times match the report. The other **21 IDs** have no corresponding canonical body path in the checked namespace; the scoped metadata search likewise returned no matches for them.

All six HTML indexes record the same filename and size1158654. Neither establishes content equivalence or identity with D-029’s separately identified wiki attachments250805153/247751845/250800526/247747361.

Read complete accepted reviews `R-DELTA-MOS-1119-TESTPLAN.md` and `R-DELTA-MOS-1145-TESTPLAN.md`, together with D-017 and D-030. These support the retained TP01–08 and TP01–10 chains. Historical unread835759 wording remains historical, superseded for present body accounting—not rewritten.

## Exclusions and authority boundaries

The saved fields support the report’s collection-lane distinctions:

- GitLab MR/repository/branch/author links are implementation/provenance references, not newly authorized explanatory-document acquisition.
- Service/API paths, auth endpoints, UI routes, Jira REST/self/avatar/icon URLs and test-environment URLs are not additional documentary targets.
- Twelve screenshots remain indexed assets, not queued documentary downloads.
- Locator-less section7.2, prototype, documentation-button and contract-deliverable mentions remain unresolved identities; no IDs were manufactured.
- LC’s omitted outbound MR URL remains explicitly unavailable.
- OP’s adjacent “Неактуально” comment does not silently erase the recorded contract reference or establish source precedence.

These exclusions are specific to this lane, not universal irrelevance findings.

Exact **241080659**, carried by MOS-944/1031/905, is a defensible first **sufficiency/authority question**. Its presence grants no acquisition permission and establishes no mandatory task2.4 dependency. No auth model, grant, reader approval or source-precedence decision follows.

## Accepted accounting boundaries and actual limits

Read complete `G1-API-COLLECTION-DELTA.md` and its accepted review, complete `G1-ROOT-REGISTRY-FINAL-INCREMENT.md`, and relevant D-045/D-044/D-030/D-029/D-017 entries.

- D-045’s original API-r1 discovery uncertainty remains independently unverified; no repeat Swagger/API/container/child/registry/835759 acquisition is introduced.
- D-044’s **42 packets /42 indexes /39 entries =4 saved texts +35 unread bodies** is reused accepted root accounting. The **23 Jira attachments are not added to39 as a global total**.
- No all-attachment, all-root or all-code prerequisite is imposed.
- Wiki/prototype/test-plan bodies were not semantically re-audited. Prior accepted semantics remain attributed to their report/review/decision chains.
- Hashes, byte measurements, acquisition safeguards, HTTP results and external timestamps remain metadata/prior-review claims; none was recomputed or remotely verified.
- Filesystem discovery establishes canonical path presence/absence, not absence of unbound copies or content equivalence elsewhere.
- No single-line tooling limitation remained for the nine-bundle inspection. Search output truncation in decision discovery was resolved by exact `read` ranges before relying on those decisions.
- Only local `read`, `find` and scoped `grep` were used. No repository edits, browser/network/storage/credential access, requests, downloads, rendering, source execution, code/tests/build/E2E, nested delegation or staging attestation occurred.

**Global progress remains6/28. Tasks2.3/2.4/2.6 remain open.**