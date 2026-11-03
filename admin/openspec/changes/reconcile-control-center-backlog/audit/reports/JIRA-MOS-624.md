# MOS-624 — saved-packet inventory

## Scope and provenance

Inventory only; no scenario, requirement, implementation or linked-content analysis. Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`; locators are zero-based JSON paths.

- Assignment: `work-items/JIRA-MOS-624.md`; revised availability: `work-items/JIRA-INVENTORY-HANDOFF.md`.
- **H** = `sources/jira-hierarchy/r1/content.json`, `$.results[0]`: key `MOS-624`, type `Q key result` (not literal Epic). Retrieved `2026-10-16T11:08:08.629Z` by parent-browser same-origin GET `/browse/<key>`, DOMParser selectors `#type-val` and `#jpo-child-issues-web-panel a[href*="/browse/MOS-"]`. Packet declares parent evidence `../../jira-MOS-623/r1/content.md` (reference only, not inspected).
- **I** = `sources/jira-member-index/r1/content.json`; metadata `sources/jira-member-index/r1/metadata.json`. Retrieved `2026-10-16T11:20:38.570Z`; parent-browser read-only same-origin Jira REST GET for exact hierarchy member allowlist, JSON extracted from parent transcript. SHA256 recorded in metadata: `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` (not independently rehashed). Selected fields only: summary, issuetype, status, subtasks, parent, updated.
- **S** = `sources/jira-subtasks/r1/content.json`; metadata `sources/jira-subtasks/r1/metadata.json`. Retrieved `2026-10-16T11:23:01.951Z`; parent-browser same-origin GET for 16 explicitly observed subtasks, selected-field-redacted extraction from parent session. SHA256 recorded: `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` (not independently rehashed). Packet-level bearer-example redaction noted; no commands executed. Attachments enumerated, not downloaded; comments/custom acceptance fields absent.

## Membership and multiplicities

H contains 29 child occurrences, 29 distinct member keys. Each appears exactly once in I, at indices 0–28. No assigned member missing or duplicated in I; no additional records claiming these members were observed. Other modules' index records are outside this inventory. H establishes module membership; I does not provide a module-parent link for these records. No full MOS-624 parent issue object occurs in I; H is a hierarchy entry, not a full parent detail collection.

For every row below, hierarchy locator is `H:$.results[0].children[n]`, and index locator is `I:$.items[n]`, where n is the first column. Multiplicity is **1 hierarchy / 1 index** for every row. `D` means exact observed type `Development task`; `SA` means `System Analytics`. **All rows have selected index coverage only: full description, attachments, comments and custom acceptance coverage are absent.** This is an expected collection gap, not a blocker.

| n | Member | Type | Observed status | Exact updated timestamp | Saved subtasks |
|---|---|---|---|---|---|
| 0 | MOS-668 | D | Ready for review | 2026-10-09T15:03:44.887+0800 | [] |
| 1 | MOS-659 | D | CLOSED | 2026-09-17T15:04:02.420+0800 | [] |
| 2 | MOS-660 | D | CLOSED | 2026-09-17T15:17:20.428+0800 | [] |
| 3 | MOS-661 | D | CLOSED | 2026-10-09T15:03:30.348+0800 | [] |
| 4 | MOS-664 | D | CLOSED | 2026-09-17T23:08:13.111+0800 | [] |
| 5 | MOS-666 | D | CLOSED | 2026-10-09T15:06:51.629+0800 | MOS-1053 |
| 6 | MOS-665 | D | CLOSED | 2026-09-10T13:55:20.628+0800 | [] |
| 7 | MOS-663 | D | CLOSED | 2026-09-10T13:55:32.794+0800 | [] |
| 8 | MOS-646 | D | CLOSED | 2026-09-03T20:20:07.101+0800 | [] |
| 9 | MOS-669 | D | CLOSED | 2026-10-09T15:05:39.908+0800 | [] |
| 10 | MOS-672 | D | CLOSED | 2026-09-22T21:33:47.993+0800 | [] |
| 11 | MOS-673 | D | CLOSED | 2026-09-23T17:21:47.836+0800 | [] |
| 12 | MOS-674 | D | CLOSED | 2026-09-22T21:44:47.949+0800 | [] |
| 13 | MOS-685 | D | Review | 2026-10-09T15:05:05.177+0800 | [] |
| 14 | MOS-699 | D | CLOSED | 2026-10-09T15:04:23.208+0800 | [] |
| 15 | MOS-717 | D | CLOSED | 2026-10-15T15:13:58.701+0800 | [] |
| 16 | MOS-754 | D | Review | 2026-10-09T15:06:44.968+0800 | [] |
| 17 | MOS-755 | D | CLOSED | 2026-10-13T14:16:29.221+0800 | [] |
| 18 | MOS-767 | SA | Draft is Ready | 2026-10-09T15:03:48.868+0800 | [] |
| 19 | MOS-904 | D | Ready for test | 2026-10-09T15:04:05.422+0800 | [] |
| 20 | MOS-905 | D | Ready for test | 2026-10-09T15:04:08.569+0800 | [] |
| 21 | MOS-923 | D | Backlog | 2026-10-15T14:46:40.107+0800 | [] |
| 22 | MOS-961 | D | Backlog | 2026-10-15T14:47:13.597+0800 | [] |
| 23 | MOS-922 | D | Backlog | 2026-10-15T14:46:44.693+0800 | [] |
| 24 | MOS-962 | D | Backlog | 2026-10-15T14:46:47.097+0800 | [] |
| 25 | MOS-960 | D | Backlog | 2026-10-15T14:46:55.374+0800 | [] |
| 26 | MOS-920 | D | Backlog | 2026-10-15T14:46:59.601+0800 | [] |
| 27 | MOS-1049 | D | CLOSED | 2026-10-09T15:03:56.427+0800 | [] |
| 28 | MOS-1142 | D | Hold | 2026-10-13T14:28:14.573+0800 | [] |

## Nested subtask reconciliation

Exactly one nested reference is observed for this module: `I:$.items[5].subtasks[0]` → `MOS-1053`, status `CLOSED`. Exactly one matching detail record exists at `S:$.items[0]`:

- Key `MOS-1053`; type `Dev-bug (sub-task)`; status `CLOSED`; updated `2026-10-09T15:05:26.189+0800`.
- `S:$.items[0].parent` = `MOS-666`, matching the referring member. Summary and status match the index stub. This subtask is nested, not an extra direct MOS-624 member.
- `S:$.items[0].subtasks` = `[]`; no deeper descendants explicitly observed.
- Description present at `S:$.items[0].description`; attachment metadata present at `S:$.items[0].attachments[0]`: id `826713`, filename `404.png`, MIME `image/png`, size `9096`, saved content locator `https://task.mos-team.ru/secure/attachment/826713/404.png`. Attachment body not collected; URL not accessed.
- Comments and custom acceptance fields not collected. No missing or duplicate observed subtask detail, parent mismatch, or extra S record parented to these 29 members was found.

The member-index metadata's “nested subtask details pending” note is historical; the later S packet supplies this one observed detail without replacing I's timestamp or provenance.

## Missing collection keys and limitations

- Full member descriptions, attachment metadata/bodies, comments and custom acceptance fields: **MOS-668, MOS-659, MOS-660, MOS-661, MOS-664, MOS-666, MOS-665, MOS-663, MOS-646, MOS-669, MOS-672, MOS-673, MOS-674, MOS-685, MOS-699, MOS-717, MOS-754, MOS-755, MOS-767, MOS-904, MOS-905, MOS-923, MOS-961, MOS-922, MOS-962, MOS-960, MOS-920, MOS-1049, MOS-1142**. Field absence does not establish that source issues have no such content.
- **MOS-1053**: comments, custom acceptance fields, attachment body `826713` remain uncollected; saved description and attachment metadata are available.
- **MOS-624**: full parent detail object, including status/update and content fields, is not established by inspected packets; collect separately if required. Only its hierarchy key/type/children are established here.
- No missing observed membership keys or nested-subtask detail keys. Supplemental delta keys MOS-1245/MOS-1306/MOS-1237/MOS-959 are not assigned members, so that packet was not inspected.
- H reports no more/next controls, but loaded HTML is not proof against permission-filtered/hidden issues. Empty saved subtask arrays likewise do not prove absence of hidden subtasks. Statuses are recorded metadata, not completion evidence. Separate snapshot times are preserved above.
- No network, browser, tests, source/status edits, external content retrieval or semantic assessment performed; only the bound report was written.
