# MOS-784 — saved inventory

## Sources and provenance

All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit`; locators use zero-based JSON array indices.

- Assignment: `work-items/JIRA-MOS-784.md`; input-availability revision: `work-items/JIRA-INVENTORY-HANDOFF.md`. Missing full member descriptions are coverage gaps, not blockers.
- **H**: `sources/jira-hierarchy/r1/content.json`, `$.results[18]`; retrieved `2026-10-16T11:08:08.629Z`. Parent-browser same-origin GET `/browse/<key>` with DOMParser, `#type-val` and `#jpo-child-issues-web-panel a[href*="/browse/MOS-"]`. Packet references `../../jira-MOS-623/r1/content.md` as parent evidence; that reference was not independently inspected. MOS-784 occurs once and has type `Q key result`, not literal Epic.
- **I**: `sources/jira-member-index/r1/content.json`, `$.items`; retrieved `2026-10-16T11:20:38.570Z`. Companion `metadata.json`: revision 1, parent-browser read-only same-origin REST GET for exact hierarchy member allowlist, selected JSON extracted from parent transcript; recorded SHA-256 `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` (not independently recomputed). Only summary/type/status/subtasks/parent/updated were requested; actual member records below have no parent field.
- **S**: `sources/jira-subtasks/r1/content.json`, `$.items`; retrieved `2026-10-16T11:23:01.951Z`. Companion `metadata.json`: revision 1, selected-field-redacted extraction from parent-browser same-origin GETs for 16 observed subtasks; recorded SHA-256 `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` (not independently recomputed). Packet-level bearer-example redaction noted. Attachment bodies were not downloaded; comments/custom acceptance fields were not collected.
- Supplementary API-delta descriptions are inapplicable: none of MOS-1245/MOS-1306/MOS-1237/MOS-959 belongs to this assigned member set. No delta bodies inspected.

## Per-member reconciliation

Observed assigned set: **MOS-704, MOS-705, MOS-706, MOS-906** (four entries, four unique keys). Each occurs once in the hierarchy child arrays and once in the member index. No missing indexed member, duplicate member record, or conflicting hierarchy assignment observed. Unrelated index records are outside scope, not extra module members.

| Member | Exact hierarchy / index locator | Observed type | Observed status | Exact updated timestamp | Saved nested references | Detail coverage |
|---|---|---|---|---|---|---|
| MOS-704 | H `$.results[18].children[0]`; I `$.items[134]` | Development task | CLOSED | `2026-10-14T13:51:02.451+0800` | `subtasks: []` | Index present; description, attachments, comments, custom acceptance fields uncollected |
| MOS-705 | H `$.results[18].children[1]`; I `$.items[135]` | Development task | CLOSED | `2026-10-14T14:31:18.164+0800` | One: `$.items[135].subtasks[0].key = MOS-1054` | Index present; description, attachments, comments, custom acceptance fields uncollected |
| MOS-706 | H `$.results[18].children[2]`; I `$.items[136]` | Development task | CLOSED | `2026-09-24T14:50:23.637+0800` | `subtasks: []` | Index present; description, attachments, comments, custom acceptance fields uncollected |
| MOS-906 | H `$.results[18].children[3]`; I `$.items[137]` | Development task | Ready for test | `2026-10-13T21:33:56.235+0800` | `subtasks: []` | Index present; description, attachments, comments, custom acceptance fields uncollected |

Module-parent links are evidenced by H, not by member REST parent fields. MOS-784 has no issue-detail object in I or S; its status, update time and full detail coverage are unavailable in these packets.

## Nested subtask and attachments

- **MOS-1054**: one reference in I `$.items[135].subtasks[0]`, status `CLOSED`; one detail record in S `$.items[15]`, type `Dev-bug (sub-task)`, status `CLOSED`, updated `2026-10-09T21:44:15.111+0800`. S `$.items[15].parent = "MOS-705"` agrees with its referencing member. No duplicate reference, missing nested detail, extra record linked to these four members, or parent mismatch observed. S `$.items[15].subtasks = []`; no further observed nested keys.
- S `$.items[15].description` is present (saved text only, no semantic assessment); `$.items[15].attachments` contains two metadata records, not downloaded content:
  - `[0]`: id `835960`, filename `EditTools_TrimVideo1791551349542.MOV`, MIME `video/quicktime`, size `35879862`, saved content locator `https://task.mos-team.ru/secure/attachment/835960/EditTools_TrimVideo1791551349542.MOV`.
  - `[1]`: id `835961`, filename `XRecorder_20261009_01.mp4`, MIME `video/mp4`, size `13280707`, saved content locator `https://task.mos-team.ru/secure/attachment/835961/XRecorder_20261009_01.mp4`.
- MOS-1054 comments and custom acceptance fields are uncollected. No external URL was followed.

## Missing collection keys and limitations

- **MOS-704, MOS-705, MOS-706, MOS-906**: collect full descriptions, attachment metadata/content as required, comments and custom acceptance fields; member index presence does not supply these fields.
- **MOS-1054**: comments/custom acceptance fields and attachment bodies remain uncollected; saved description and attachment metadata already exist.
- **MOS-784**: parent issue detail object remains uncollected in the inspected packets; collect separately if parent detail coverage is required.
- No missing detail key among the explicitly observed nested subtasks. Empty arrays only describe saved observations; they do not exclude hidden or permission-filtered issues. H reports no more/next controls in loaded child panels, not guaranteed completeness.
- Preserve distinct retrieval and issue-update timestamps above; statuses do not establish completion. No scenario, business-requirement, wiki-body or implementation assessment performed. Only local read-only packet inspection and this report write; no tests or network actions.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Four assigned members reconciled at exact JSON locators; one nested subtask parent verified; collection gaps and provenance recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-784.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read-only Python JSON inspection of hierarchy, member-index and subtask packets","result":"passed","summary":"4 unique assigned/indexed members, 1 nested reference and matching detail; no observed duplicates or mismatches."}],
  "validationOutput": ["MOS-784 occurs at hierarchy results[18]; members match index items[134..137]; MOS-1054 at subtask items[15] links to MOS-705."],
  "residualRisks": ["Selected-field snapshots omit member full details, comments and custom acceptance fields; attachment bodies uncollected.","Saved empty arrays and loaded hierarchy panels cannot exclude hidden issues; statuses are not completion evidence."],
  "noStagedFiles": true,
  "diffSummary": "Only assigned inventory report written; source and status files unchanged.",
  "reviewFindings": ["No blocking membership conflict observed."],
  "manualNotes": "Inspection was inventory-only. No staging commands, tests, external reads, business analysis or source edits performed. Metadata hashes recorded, not recomputed."
}
```
