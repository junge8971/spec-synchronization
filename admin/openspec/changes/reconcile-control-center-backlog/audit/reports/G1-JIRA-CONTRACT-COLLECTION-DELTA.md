# Code Context

## Result — bounded collection-disposition delta

**Current scoped ledger: 13 exact wiki IDs = 9 retained canonical packets + 4 canonical gaps.** The accepted historical D-046 snapshot remains **6 retained/7 gaps, 40 occurrences**; D-047 adds MOS-909's occurrence of the already-retained domains/skills contract, yielding **41 combined occurrences**, not a new target. Three subsequent exact-ID captures resolve team/dashboard/audit document-availability gaps only. They add **0 members to root42**. Global **6/28 unchanged**; tasks2.3/2.4/2.6 are not closed.

This report reuses accepted membership and reference edges, not primary Jira fields, a new graph, a census or renewed semantic audits. Independent review follows. `A` below expands literally to `openspec/changes/reconcile-control-center-backlog/audit`; all abbreviated paths are under A.

## Files Retrieved

1. `A/work-items/G1-JIRA-CONTRACT-COLLECTION-DELTA.md:1–17` — bounded assignment.
2. `A/reports/G1-JIRA-DETAIL-DOCUMENT-EDGES.md:1–220` and `A/reviews/R-G1-JIRA-DETAIL-DOCUMENT-EDGES.md:1–160`; `A/reports/G1-JIRA-SPECIAL-DOCUMENT-EDGES.md:1–130` and `A/reviews/R-G1-JIRA-SPECIAL-DOCUMENT-EDGES.md:1–130` (reads ended at EOF where shorter) — accepted target/carrier ledger, membership attribution and finite-coverage limits. No underlying Jira packet reopened.
3. `A/decisions.md:1–85`, particularly D-050 through D-044 — current acceptance, historical snapshot and original REVISE lineage.
4. Complete `A/sources/wiki-241080659/r1/metadata.json:1–24`, `wiki-241095761/r1/metadata.json:1–26`, `wiki-241077434/r1/metadata.json:1–26`; their three `-readable/r1/metadata.json:1–13` files — exact identities, dates, formats, indexes and derivative limits.
5. `A/sources/wiki-241077434-readable/r1/envelope-index-projection.json:1–23` — parent-parsed identity and complete attachment object, not independently parsed canonical JSON.
6. `A/sources/api-teams-review-projection/r2/metadata.json:1–100` and `api-dashboard-review-projection/r2/metadata.json:1–100` — source identity and operation/schema/edge counts at lines2–7. Remaining per-file hash listings unnecessary; no complete metadata-file or hash verification claimed.
7. Complete baseline metadata: `A/sources/wiki-241082009/r2/metadata.json:1–50`, `wiki-241097511/r2/metadata.json:1–51`, and `wiki-{241085439,241085838,241088180,241092242}/r1/metadata.json:1–56` (each brace member is a separate path). Baseline bodies/index dispositions reused, not re-audited.
8. `A/reports/DELTA-TEAMS-API-CONTRACT.md:1–44`; complete `A/reviews/R-DELTA-TEAMS-API-CONTRACT.md:1–145` — source/index attribution and ACCEPT chain.
9. `A/reports/DELTA-DASHBOARD-BOARD-CONTRACT.md:1–44`; complete `A/reviews/R-DELTA-DASHBOARD-BOARD-CONTRACT.md` (read1–130 to EOF); `A/reports/DELTA-DASHBOARD-METRICS-CONTRACT.md:70–151`; complete `A/reviews/R-DELTA-DASHBOARD-METRICS-CONTRACT.md` (read1–140 to EOF) — two selected semantic lanes and eight corrected metrics locators, not a new review.
10. `A/reports/DELTA-AUDIT-SERVICE-CONTRACT.md:1–78`, especially **line48**; complete `A/reviews/R-DELTA-AUDIT-SERVICE-CONTRACT.md:1–105` — original sole finding compared with actual row and D-050, without reopening source semantics.

Scoped `find` confirmed all nine canonical content paths below and the three new canonical directories' contents (each has `r1/content.json` and `r1/metadata.json`). Scoped `find` under `A/sources` for names containing the four remaining IDs returned none; corroborating `grep` restricted to `A/sources/**/metadata.json` for those four exact IDs returned no matches. This is canonical-store absence only, not global absence of unbound copies, inaccessible remote pages or missing backend capability.

## Key Evidence — current exact-ID ledger

Reference notation, inherited unchanged from D-046/D-047: **AD**=`sources/jira-api-delta-scenarios/r1/content.json`; **SK**=`sources/jira-details-MOS-774/r1/content.json`; **SB**=`sources/jira-sandbox-details/r1/content.json`; **SH**=`sources/jira-shell-details/r1/content.json`; **RP**=`sources/jira-reports-details/r1/content.json`; **OP**=`sources/jira-operations-details/r1/content.json`. `D(n)` is `/items/n/description`; every listed index denotes an occurrence, not an inferred edge. `W(ID,r)` means exact canonical `A/sources/wiki-ID/r/content.json`, with adjacent `metadata.json`. All retained rows record HTTP200; timestamps below are **retrievedAt**, not precedence or freshness guarantees.

Baseline JSON body/view formats and returned-index meanings are reused from accepted D-045/D-046/D-047, not independently reparsed. Baseline metadata has no explicit `format` field: do not relabel it as a newly verified raw response. New three metadata files explicitly say **selected JSON envelope with full decoded bodyView, not raw HTTP response**.

| Exact ID / current disposition | Canonical packet, page version, capture timestamp, body/index | Source-carrying references (accepted ledger) | Accepted chain / separate limitation |
|---|---|---|---|
| **241082009 — baseline retained** | W(241082009,r2), v5, `2026-10-16T12:28:15.837Z`; JSON body/view; separate `attachments.json`, metadata count0/next null | AD D(3) MOS-959; SK D(17) MOS-1031; SB D(0) MOS-960; SH D(5) MOS-905: **4** | D-045 collection disposition → D-046; preserve failed r1. Not a refresh or new semantic acceptance. |
| **241097511 — baseline retained** | W(241097511,r2), v6, `2026-10-16T12:37:03.295Z`; JSON body/view; separate `attachments.json`, count0/next null | SK D(5–17) MOS-944/945/1018/1019/1020/1021/1022/1023/1025/1026/1027/1030/1031; SB D(0) MOS-960; SH D(5) MOS-905; `sources/jira-MOS-909/r1/content.md:13–14` MOS-909: **16** | D-045 → D-046/D-047. Earlier r1 404 remains unexplained; successful retention does not rewrite it. |
| **241085439 — baseline retained** | W(241085439,r1), v15, `2026-10-16T13:31:52.139Z`; JSON body/view; metadata attachment status200/count0/next null | SK D(16) MOS-1030; RP D(4) MOS-1015: **2** | D-045 → D-046. Eight recorded bearer-example redactions preserved, not reproduced; not later dialogue-list/card IDs. |
| **241085838 — baseline retained** | W(241085838,r1), v3, `2026-10-16T13:31:51.607Z`; JSON body/view; metadata attachment status200/count0/next null | RP D(1–5) MOS-885/916/919/1015/1016: **5** | D-045 → D-046; D-036 catalog versus later root examples remains separate. |
| **241088180 — baseline retained** | W(241088180,r1), v4, `2026-10-16T13:03:14.658Z`; JSON body/view; metadata attachment status200/count0/next null | OP `/items/0/comments/items/0/body`, MOS-717 comment1131251: **1** | D-045 → D-046. Adjacent “Неактуально” does not silently erase the edge or establish precedence; not root system-state pages. |
| **241092242 — baseline retained** | W(241092242,r1), v4, `2026-10-16T13:03:14.883Z`; JSON body/view; metadata attachment status200/count0/next null | SK D(15) MOS-1027; OP D(3,4) MOS-922/923: **3** | D-045 → D-046. Exact stubs/banner/maintenance contract, not root template/admin-stub identity. |
| **241080659 — newly retained** | W(241080659,r1), v5, `2026-10-19T13:03:50.342Z`; selected full decoded bodyView envelope; metadata attachments status200/size0/next null | SK D(5,17) MOS-944/1031; SH D(5) MOS-905: **3** | TEAMAPI-01–08 report → original reviewer **ACCEPT** → D-048. Full index fields additionally attributed to accepted report/review below. Exact team availability gap resolved; no detailed team-owner/runtime acceptance. |
| **241095761 — newly retained** | W(241095761,r1), v8, `2026-10-19T13:42:47.528Z`; selected full decoded bodyView envelope; metadata attachments status200/start0/limit100/size0/next null | SK D(13,16) MOS-1025/1030: **2** | BOARD-01–08 ACCEPT and corrected DMC-01–12 accepted by D-049; metrics original **REVISE** retained. Not dashboard brief241080080 or monitoring example241074633. |
| **241077434 — newly retained** | W(241077434,r1), v2, `2026-10-19T14:00:29.066Z`; selected full decoded bodyView envelope; metadata attachments status200/start0/limit100/size0/next null; parent projection additionally results[] | SK D(17) MOS-1031: **1** | AUDIT-01–12 accepted D-050 **WITHOUT report edit**; original **REVISE** remains. Sole locator finding not reproduced. No reader activation or MOS1031 closure. |
| **238347672 — canonical gap** | No exact-ID canonical packet/metadata found in checked namespace; version/capture/body/index **unavailable**, not empty | SK D(5), MOS-944: **1** | D-046/D-047: explicit user-management API documentary candidate; necessity/applicable authority unresolved. No exact-ID accepted body chain. |
| **241079770 — canonical gap** | Same scoped absence; version/capture/body/index unavailable | SH D(4), MOS-904: **1** | D-046/D-047: explicit login/session API documentary candidate; approved auth scope remains governing. Historical238329164 is not identity replacement or new-policy authority. |
| **223087110 — canonical gap, ambiguous** | Same scoped absence; version/capture/body/index unavailable | SH D(0), MOS-624 Documentation cell, `pages/viewpage.action?pageId=223087110`: **1** | D-046/D-047: unnamed reference; identity/relevance/authority clarification remains before collection proposal. Not presumed API explanation or obsolete. |
| **222659162 — canonical gap, ambiguous** | Same scoped absence; version/capture/body/index unavailable | SH D(0), MOS-624 same cell, `pages/viewpage.action?pageId=222659162`: **1** | Separate unnamed ID and separate unresolved disposition; proximity does not merge it with223087110 or a retained shell source. |

**Manual arithmetic:** baseline6 + newly retained3 = **9**; historical7 gaps − exact successful3 = **4**; 9+4 = **13**. Combined occurrence counts are **4+16+2+5+1+3+3+2+1+1+1+1+1 = 41**. No new edge or carrier was discovered in this task; acquisition changes retention, not target membership or occurrence count.

D-044 root accounting stays **42 page packets/42 returned indexes/39 entries = 4 saved texts +35 unread bodies**. New canonical metadata explicitly labels all three captures off-root; derivatives/projections add no pages. **23 Jira attachment IDs** remain the separate D-046/D-047 subset (2 accepted plan bodies +21 index-only); do not add23 to39 as a universal total. Root counters were reused, not recounted.

## Actual metadata/index fields and projection boundaries

| New canonical | Publication timestamp (`versionWhen`) | Direct metadata/index versus attributed evidence |
|---|---|---|
| team241080659 | `2026-09-16T18:26:00.056+08:00` | Metadata `/attachments` has **status,size,next only**. It does not itself contain start/limit/results. The accepted team report/review explicitly inspected canonical `/attachments` and report status200/start0/limit100/size0/next null/results[]. That fuller shape is **reused accepted evidence**, not this scout's canonical parse. |
| dashboard241095761 | `2026-09-22T20:47:12.900+08:00` | Metadata directly supplies status200/start0/limit100/size0/next null, **no results field**. Accepted board/metrics chains attribute empty returned index to collection/parent. No direct canonical results-array inspection or invented separate file. |
| audit241077434 | `2026-09-07T19:22:13.762+08:00` | Metadata has same five fields as dashboard. Existing parent `envelope-index-projection.json` `/fields/attachments` additionally contains **results:[]** and states that this is the complete original attachment object. Parent parsing/equality attribution remains explicit. |

All three record zero redactions and HTTP200; these are retained metadata claims, not this run's remote observations. “Separate index” means separately returned attachment data included in the selected envelope; **no standalone `attachments.json` exists in these three canonical directories**. It must not be confused with baseline r2 standalone index files. Saved empty returned indexes do not prove global asset absence, no hidden attachments or future completeness. Source dates, collection dates and claims of synchronization do not settle precedence or deployed behavior.

Readable derivatives are `sources/wiki-ID-readable/r1/{content.txt,body-view-chunks.json}`: team **328 lines/8 chunks**, dashboard **854/34**, audit **480/15**, per their metadata. They derive from the respective canonical r1, lose markup in plain text, and are **not new captures or independent documents**. Roundtrip and hashes are parent-attributed; no derivative body was re-read here.

API projections are a different source lane: `sources/api-teams-review-projection/r2/metadata.json:2–7` points to saved `sources/api-live/r2/content.json`, **8 operations/29 schemas/54 edges**; dashboard counterpart points to the same API publication, **5/34/46**. They do not replace wiki acquisition or constitute new API fetches. Accepted team review independently inspected projected contents; original parsing, pointer equality and source hash were parent work. Dashboard metrics selected **2 operations/26 schemas**, board **3 operations/13 schemas/16 edges**; overlapping schemas are not additive. Projection totals are not a whole-API or runtime audit. No API schema bodies or closure graph were reopened here.

## Accepted semantic lineage — not renewed acceptance

- **Team:** `reports/DELTA-TEAMS-API-CONTRACT.md` → `reviews/R-DELTA-TEAMS-API-CONTRACT.md` (**ACCEPT**, no fixes) → **D-048**. Eight candidate families document selected contracts and remaining differences. Membership IDs versus principal, required fields/error representations, search/order, membership lifecycle and version/idempotency publication boundaries remain documentary. Detailed team-owner acceptance, runtime and MOS1031/MOS1023 gates do not follow from exact retention.
- **Dashboard board:** corresponding `DELTA-DASHBOARD-BOARD-CONTRACT` report → `R-DELTA-DASHBOARD-BOARD-CONTRACT` **ACCEPT**, no fixes → **D-049**. Catalog/board configuration is separate from measurements, skill analytics, monitoring and reports. Hidden-widget/full-replacement product questions remain open.
- **Dashboard metrics:** corresponding report → original `R-DELTA-DASHBOARD-METRICS-CONTRACT` **REVISE for locators only** → **D-049 parent acceptance after eight exact locator corrections** in DMC04/05/06/07/08/09/11 and Start Here. Current report70–151 contains the prescribed ranges (140–159;453–483 plus504;794–798;484–504 and505–532;505–532;484–532;526;453–532). No fresh reviewer ACCEPT is claimed. Formula/window/Other, unavailable-versus-zero, formal422 and auth/audit-stage uncertainties remain.
- **Audit:** `reports/DELTA-AUDIT-SERVICE-CONTRACT.md` → original `reviews/R-DELTA-AUDIT-SERVICE-CONTRACT.md` **REVISE solely for alleged missing chunk locator** → **D-050 parent acceptance without editing the report**. Actual report **line48** already says **`§3.1 T148–251, C6–8; §5.3 T449–455, C13–14`**. This matches D-050's explicit finding-not-reproduced explanation. Do not describe this as a corrected report, applied audit fix or new reviewer ACCEPT. All twelve candidates are documentarily accepted by the parent decision, not by relabeling the original review.

Original historical reports, snapshots and decisions remain intact. Their “gap,” “pending review” or discovery-timeout wording is historical in its own capture context. D-046/D-047's discovery transport timeouts occurred before GET; subsequent successful exact captures supersede current collection blockage **only for these acquired pages**, not another page's access or permission status. A timeout is not403/404 or denial of documentary authority.

## Architecture and remaining questions

**Accepted carrying edge → exact canonical acquisition/metadata/index → readable derivative or API projection → bounded semantic report/review/decision → separately gated owner/runtime acceptance.** None of these steps substitutes for the next. No application code was inspected, no source precedence selected, and no semantic owner assigned.

Smallest remaining questions, not an automatic collection queue:

1. **User contract238347672 (MOS-944):** does this exact document answer a still-unresolved user-management API explanatory question that accepted evidence does not answer? If yes, confirm applicability and existing documentary collection authority for this exact ID before proposing a bounded capture. A team member/contact DTO is not confirmed-session identity, nor an identity substitute for this publication.
2. **Login/session contract241079770 (MOS-904):** what concrete documentary question remains after the already-approved session/permissions integration, and is this exact source applicable and authorized for that question? If necessary, classify against approved auth scope before a future capture/interpretation. This is not authority for session requests, credentials, new authentication models, logout or role grants. No current page-access failure is established.
3. **Unnamed shell223087110 and222659162 (MOS-624):** identify each document and its relevance to a concrete explanatory question, then applicable documentary authority. Retain both ambiguous holds separately; no title-based substitution, automatic exclusion or traversal mandate.

**Task2.4 effect:** evidence now removes three specific documentary availability gaps and supplies accepted bounded explanatory comparisons, so repeating team/dashboard/audit collection is unjustified absent a new concrete question. It does **not** certify that all relevant explanations are sufficient or automatically close task2.4. The two named remaining contracts are documentary candidates, not proven mandatory dependencies; the two unnamed references require clarification first. Parent sufficiency judgment remains bounded to actual unresolved questions, not an all-documents/all-attachments/all-root/all-code prerequisite. Other attachment/locator-less/selected-field limits remain as D-046/D-047 dispositions, without a new mandate.

Preserve **D-045 original API-r1 discovery independently unverified**. Preserve **D-050 and audit-chain unavailable `docs/api/contracts/audit.md` pointer** as prior checked evidence, not a new local probe here, backend absence or permission to repair owner plans. MOS1031 still needs accepted routing/credential destination, reader authorization/object scope, wire/event projection, DTO/error handling, redaction, period/retention, pagination and consistency acceptance. Publication service identity/fail-open is not employee reader access/fail-closed; dashboard503 applicability remains unresolved. Approved auth/UI-permission/backend-scope, owner/session isolation, no automatic replay, MOS1023 token, source-conflict and other owner gates remain untouched. No plan/task/spec or policy changes.

## Start Here

Open **`A/decisions.md:3–31` (D-050/D-049/D-048)** beside this13-row ledger. For the critical lineage check, compare **`A/reports/DELTA-AUDIT-SERVICE-CONTRACT.md:48`** with **`A/reviews/R-DELTA-AUDIT-SERVICE-CONTRACT.md:12–20`** and D-050: acceptance required **no audit report edit**. Next ask only the four remaining exact-ID disposition questions above, not another full semantic audit.

## Validation and residual risks

Only local read/find/scoped grep and this sole report write were used. Manually reconciled accepted row counts against verified canonical paths and directly read metadata. No canonical body, primary Jira field, API operation/schema, derivative body or semantic graph was re-audited. One initial read mistakenly targeted the audit directory and returned EISDIR; scoped find then supplied paths. No conclusion relies on that failed read or the exploratory metadata glob that returned no matches; the successful exact-file reads and dedicated four-ID search are the evidence.

No browser/network/MCP/storage/credentials/requests/downloads/rendering/source execution/code/tests/build/E2E/nested delegation. No hashes, byte identity, acquisition safeguards, runtime or staging state independently checked or attested. Metadata and existing parent projections remain attributed; external freshness, full issue coverage and unbound-copy equivalence remain unknown. Independent review of this delta is pending. Only the assigned report was intentionally written; no source/spec/archive/task/owner-plan/decision edits.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Thirteen-row exact-ID ledger reconciles accepted membership/41 occurrences with nine verified canonical paths and four scoped gaps; actual metadata/index fields, derivatives and D048–D050 lineage remain distinct."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/G1-JIRA-CONTRACT-COLLECTION-DELTA.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read/find/scoped grep and manual arithmetic","result":"passed","summary":"Confirmed three new canonical metadata pairs, six baseline retained paths, four exact-ID scoped gaps;9+4=13 and41 accepted occurrences."},
    {"command":"Initial read of audit directory","result":"failed","summary":"EISDIR; recovered with scoped file discovery;no evidence conclusion based on this read."},
    {"command":"Network/browser/source execution/code/tests/build/hash/staging checks","result":"not-run","summary":"Excluded by documentary-only assignment;no runtime or staging attestation."}
  ],
  "validationOutput": ["Historical6/7 and40-occurrence snapshot preserved;current9/4 and combined41 verified without membership recensus.","Audit row48 already includes C13–14;D050 accepted without report edit;original REVISE remains.","Root42/42/39 and separate Jira23 unchanged;global6/28 unchanged."],
  "residualRisks": ["Two named contracts remain documentary candidates;two unnamed shell IDs remain ambiguous;none automatically mandatory.","Index/body parsing and projection equality reused with explicit attribution;hashes,external freshness andruntime unverified.","API-r1 discovery uncertainty,unavailable audit.md pointer and auth/token/reader/owner gates persist;independent review pending."],
  "diffSummary":"Sole assigned collection-disposition report written;no historical report/source/plan/task/decision edited.",
  "reviewFindings": ["No automatic task2.4 closure or blanket prerequisites;no corrected audit text or fresh reviewer ACCEPT invented."],
  "manualNotes":"Accepted membership/edge ledger reused,not rederived.Index metadata fields differ between the three new packets;complete audit index is parent-projected.Team full index is accepted-review attribution.No staging attestation."
}
```
