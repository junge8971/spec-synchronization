# MOS-782 — saved-packet inventory

## Scope and provenance

Inventory only; no scenario, requirement or implementation assessment. The supplemental `work-items/JIRA-INVENTORY-HANDOFF.md` supersedes the pending-detail dependency in `work-items/JIRA-MOS-782.md`. All locators below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`; fragments are zero-based JSON Pointers.

- **H**: `sources/jira-hierarchy/r1/content.json#/results/16` — MOS-782, type **Q key result**, 25 observed children. Retrieved **2026-10-16T11:08:08.629Z** through parent-browser same-origin browse GET/DOM child-panel extraction. Packet cites `../../jira-MOS-623/r1/content.md` as parent evidence (not independently inspected here). No more/next controls observed; hidden permission-filtered issues remain possible.
- **I**: `sources/jira-member-index/r1/content.json` — retrieved **2026-10-16T11:20:38.570Z**; provenance and selected-field limitations at `sources/jira-member-index/r1/metadata.json`. Parent-browser read-only Jira REST GET, exact hierarchy-member allowlist, extracted from parent transcript. Fields: summary, type, status, updated, subtasks; no descriptions/comments/attachments/custom acceptance fields.
- **S**: `sources/jira-subtasks/r1/content.json` — retrieved **2026-10-16T11:23:01.951Z**; provenance at `sources/jira-subtasks/r1/metadata.json`. Parent-browser same-origin GET for 16 observed subtasks; selected-field redacted extraction. Attachment metadata only; no comments/custom acceptance fields. Example credential redacted before persistence; no examples executed.
- **D**: `sources/jira-api-delta-scenarios/r1/content.json` — retrieved **2026-10-16T11:23:51.742Z**; provenance at `sources/jira-api-delta-scenarios/r1/metadata.json`. Parent-browser same-origin GET for four previously inventoried keys; only MOS-1245 and MOS-1306 belong here. Descriptions and attachment metadata, no attachment bodies/comments/custom fields.

## Per-member inventory

Every row is present exactly once in I and has type **Development task**, `subtasks: []`, and no saved parent field. H child position gives the exact membership locator `H/children/<position>`. Membership therefore comes from H, not a claimed member-side parent object. `Index only` means full description, attachments, comments and custom acceptance coverage are all uncollected. `D detail` means description and attachment metadata additionally present; comments/custom acceptance fields and attachment bodies still uncollected.

| Key | H child position | I locator | Observed status (I) | Updated (I; verbatim) | Detail coverage |
|---|---:|---|---|---|---|
| MOS-802 | 0 | I#/items/91 | CLOSED | 2026-09-16T18:08:11.814+0800 | Index only |
| MOS-803 | 1 | I#/items/92 | CLOSED | 2026-09-16T18:08:14.028+0800 | Index only |
| MOS-804 | 2 | I#/items/93 | CLOSED | 2026-09-16T18:08:20.184+0800 | Index only |
| MOS-805 | 3 | I#/items/94 | CLOSED | 2026-09-16T18:08:26.665+0800 | Index only |
| MOS-806 | 4 | I#/items/95 | CLOSED | 2026-09-16T18:08:31.129+0800 | Index only |
| MOS-811 | 5 | I#/items/96 | Backlog | 2026-10-09T15:08:19.171+0800 | Index only |
| MOS-809 | 6 | I#/items/97 | Ready for test | 2026-10-09T15:08:35.352+0800 | Index only |
| MOS-808 | 7 | I#/items/98 | CLOSED | 2026-10-16T14:16:08.544+0800 | Index only |
| MOS-807 | 8 | I#/items/99 | Backlog | 2026-10-15T14:38:33.569+0800 | Index only |
| MOS-810 | 9 | I#/items/100 | Hold | 2026-10-09T15:08:24.131+0800 | Index only |
| MOS-859 | 10 | I#/items/101 | CLOSED | 2026-10-13T21:35:28.306+0800 | Index only |
| MOS-907 | 11 | I#/items/102 | Ready for test | 2026-10-09T15:03:47.700+0800 | Index only |
| MOS-909 | 12 | I#/items/103 | Ready for test | 2026-10-09T15:03:58.003+0800 | Index only |
| MOS-935 | 13 | I#/items/104 | Ready for test | 2026-10-09T15:05:45.382+0800 | Index only |
| MOS-942 | 14 | I#/items/105 | Ready for test | 2026-10-09T15:05:48.352+0800 | Index only |
| MOS-929 | 15 | I#/items/106 | Ready for test | 2026-10-09T15:05:22.114+0800 | Index only |
| MOS-933 | 16 | I#/items/107 | Ready for test | 2026-10-09T15:05:40.689+0800 | Index only |
| MOS-1119 | 17 | I#/items/108 | Ready for test | 2026-10-09T15:04:31.809+0800 | Index only |
| MOS-1120 | 18 | I#/items/109 | CLOSED | 2026-10-09T15:04:35.341+0800 | Index only |
| MOS-1141 | 19 | I#/items/110 | Ready for test | 2026-10-12T20:10:06.627+0800 | Index only |
| MOS-1153 | 20 | I#/items/111 | Review | 2026-10-12T16:03:02.851+0800 | Index only |
| MOS-1157 | 21 | I#/items/112 | Ready for test | 2026-10-13T18:05:35.223+0800 | Index only |
| MOS-1245 | 22 | I#/items/113 | Ready for test | 2026-10-16T15:32:20.848+0800 | D detail: D#/items/0 |
| MOS-1306 | 23 | I#/items/114 | Ready for test | 2026-10-16T17:06:48.457+0800 | D detail: D#/items/1 |
| MOS-1381 | 24 | I#/items/115 | Development | 2026-10-16T19:20:14.172+0800 | Index only |

### Supplementary snapshots (not replacements for I)

- **MOS-1245**, D#/items/0: Development task; Ready for test; updated **2026-10-16T19:22:44.467+0800**; description at `/description`; `subtasks: []`. Attachment metadata at `/attachments/0`: ID **839666**, `mos-1245-test-plan.md`, `text/markdown`, **20881 bytes**. Body not collected.
- **MOS-1306**, D#/items/1: Development task; Ready for test; updated **2026-10-16T19:22:45.212+0800**; description at `/description`; `subtasks: []`. Attachment metadata at `/attachments/0`: ID **839773**, `TEST_PLAN_MOS_1306.md`, `text/markdown`, **17306 bytes**. Body not collected.

Description text presence is recorded without assessing its requirements or treating embedded prose as a collected custom acceptance field.

## Reconciliation and nested links

- H contains **25 keys, 25 unique**; each appears exactly once in I. Missing assigned index keys: **0**; duplicate assigned keys: **0**. D contributes two matching snapshots, not new members; no module-associated extra keys observed. Other packet records are outside this module, not extras to add.
- All 25 I `/subtasks` arrays are empty; both scoped D arrays are also empty. Checked S#/items/0 through S#/items/15 `/parent` against all assigned members and MOS-782: **zero matching parent links**. Thus there are no observed nested references requiring a detail record, no observed nested duplicates, and no conflicting parent links in this module. This is a snapshot result, not proof that no hidden/new subtasks exist.
- MOS-782 itself is present as H's hierarchy entry, **not** as a full issue object in I, S or D; parent status, updated time and details are not established.
- MOS-1119 and MOS-1120 have identical saved summaries but different keys; retained as two members, not deduplicated by title.

## Collection gaps and next keys

1. Full descriptions and attachment inventories remain uncollected for **MOS-802, MOS-803, MOS-804, MOS-805, MOS-806, MOS-811, MOS-809, MOS-808, MOS-807, MOS-810, MOS-859, MOS-907, MOS-909, MOS-935, MOS-942, MOS-929, MOS-933, MOS-1119, MOS-1120, MOS-1141, MOS-1153, MOS-1157, MOS-1381** (the 23 `Index only` rows above). Expected coverage gaps, not blockers.
2. Comments and custom acceptance fields remain uncollected for **all 25 table keys**. Collect attachment bodies only under separately authorized collection; the two observed IDs are listed above. Missing fields do not establish empty values.
3. If parent issue details are needed, next key **MOS-782**; do not infer that its full object was collected. No currently observed nested-subtask keys are pending for this module.
4. Preserve separate retrieval and update timestamps when collecting newer revisions. Statuses do not establish business completion; loaded hierarchy HTML does not prove completeness against inaccessible issues.

## Validation / execution notes

Local JSON inspection reconciled membership, counts, field presence and nested parent references. One inspection command initially constructed an incorrect absolute path (`/r1/content.json`); corrected immediately, and the intended required packets were successfully read. This was a local command typo, not a missing required packet or infrastructure failure. No network, tests, browser, generation, source/status edits or external-link traversal performed. Only this report was written.
