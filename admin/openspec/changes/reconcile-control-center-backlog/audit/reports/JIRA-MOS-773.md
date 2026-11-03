# MOS-773 — saved-packet inventory

## Scope and provenance

Inventory only, under `work-items/JIRA-MOS-773.md` and superseding `work-items/JIRA-INVENTORY-HANDOFF.md`. All locators below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`; JSON indices are zero-based.

- **H** = `sources/jira-hierarchy/r1/content.json`; `$.results[8]` is MOS-773, type `Q key result`, with 11 observed children. Retrieved `2026-10-16T11:08:08.629Z`. Saved parent-browser same-origin browse HTML extraction (`#type-val`, child-panel links); declared parent evidence `../../jira-MOS-623/r1/content.md`. No pagination controls observed; hidden/permission-filtered issues remain possible.
- **M** = `sources/jira-member-index/r1/content.json`; retrieved `2026-10-16T11:20:38.570Z`. Provenance: `sources/jira-member-index/r1/metadata.json`, revision 1, parent-browser read-only same-origin Jira REST exact member allowlist, extracted from parent transcript. Selected identity/status/update/subtask fields only.
- **S** = `sources/jira-subtasks/r1/content.json`; retrieved `2026-10-16T11:23:01.951Z`. Provenance: `sources/jira-subtasks/r1/metadata.json`, revision 1, selected-field-redacted extraction of parent-browser same-origin issue GETs for observed subtasks. Attachments enumerated, not downloaded; comments/custom acceptance fields absent. Packet metadata records redaction of a credential example.

These are distinct snapshots; issue update timestamps below are preserved verbatim, not replaced by retrieval times. No scenario reports, requirements, external links or implementation were assessed. Supplementary API-delta keys do not intersect this module, so that packet is not applicable.

## Direct members

All rows have observed type **Development task**. Each is present exactly once in M. **Index-only** means description, attachments, comments and custom acceptance fields are all uncollected in the selected record—not confirmed absent in Jira.

| Member | Status | Updated | Exact membership / record locator | Nested keys | Coverage |
|---|---|---|---|---|---|
| MOS-703 | Review | 2026-10-09T15:04:01.076+0800 | H `$.results[8].children[0]`; M `$.items[45]` | `[]` | Index-only |
| MOS-889 | Ready for test | 2026-10-09T15:08:46.969+0800 | H `$.results[8].children[1]`; M `$.items[46]` | `[]` | Index-only |
| MOS-1037 | Testing | 2026-10-16T18:15:19.254+0800 | H `$.results[8].children[2]`; M `$.items[47]` | MOS-1411, MOS-1412, MOS-1414, MOS-1419, MOS-1422 | Index-only |
| MOS-1038 | Ready for test | 2026-10-09T15:06:43.227+0800 | H `$.results[8].children[3]`; M `$.items[48]` | `[]` | Index-only |
| MOS-1040 | Ready for test | 2026-10-09T15:06:48.818+0800 | H `$.results[8].children[4]`; M `$.items[49]` | `[]` | Index-only |
| MOS-1041 | Ready for test | 2026-10-09T15:06:14.020+0800 | H `$.results[8].children[5]`; M `$.items[50]` | `[]` | Index-only |
| MOS-1042 | Ready for test | 2026-10-09T15:06:21.500+0800 | H `$.results[8].children[6]`; M `$.items[51]` | `[]` | Index-only |
| MOS-1043 | Ready for test | 2026-10-09T15:06:23.498+0800 | H `$.results[8].children[7]`; M `$.items[52]` | `[]` | Index-only |
| MOS-1044 | Ready for test | 2026-10-09T15:07:03.053+0800 | H `$.results[8].children[8]`; M `$.items[53]` | `[]` | Index-only |
| MOS-1045 | Ready for test | 2026-10-09T15:07:08.524+0800 | H `$.results[8].children[9]`; M `$.items[54]` | `[]` | Index-only |
| MOS-1211 | Ready for test | 2026-10-15T15:49:54.949+0800 | H `$.results[8].children[10]`; M `$.items[55]` | `[]` | Index-only |

## Nested-subtask reconciliation

All five have observed type **Dev-bug (sub-task)** and status **Backlog**, matching the corresponding M subtask stub status. Each occurs exactly once in S; each S `.parent` equals `MOS-1037`. Each S `.subtasks` is `[]`. Description text is present at each S record's `.description`; attachment metadata is present at `.attachments`; comments and custom acceptance fields are uncollected for every row.

| Subtask | Updated | Index stub → detail locator | Attachment metadata IDs |
|---|---|---|---|
| MOS-1411 | 2026-10-16T15:21:18.530+0800 | M `$.items[47].subtasks[0]` → S `$.items[2]` | `839653` |
| MOS-1412 | 2026-10-16T15:30:12.067+0800 | M `$.items[47].subtasks[1]` → S `$.items[3]` | `839662` |
| MOS-1414 | 2026-10-16T18:15:19.233+0800 | M `$.items[47].subtasks[2]` → S `$.items[4]` | `839675` |
| MOS-1419 | 2026-10-16T18:18:36.194+0800 | M `$.items[47].subtasks[3]` → S `$.items[5]` | `839862` |
| MOS-1422 | 2026-10-16T18:39:35.845+0800 | M `$.items[47].subtasks[4]` → S `$.items[6]` | `839906`, `839905` |

## Result and next collection gaps

- One assigned hierarchy entry; 11 unique direct members; 11/11 selected index records. No missing or duplicate assigned member keys.
- Five unique expected nested keys; five matching detail records. No missing, duplicate, extra module-parent subtask keys or conflicting nested parent links. Other packet records are outside this module's scope, not extras.
- Direct-member association is evidenced by H, not a collected `.parent` field in these M rows. MOS-773 itself has a hierarchy entry but no issue object in M; its detail/status/update coverage is not established.
- Next collection keys for full direct-member descriptions, attachment lists, comments and custom acceptance coverage: **MOS-703, MOS-889, MOS-1037, MOS-1038, MOS-1040, MOS-1041, MOS-1042, MOS-1043, MOS-1044, MOS-1045, MOS-1211**. MOS-773 parent details also remain uncollected in these inputs.
- Next collection keys for comments/custom acceptance fields and, if needed, attachment binaries: **MOS-1411, MOS-1412, MOS-1414, MOS-1419, MOS-1422**. Six attachment metadata entries are not six downloaded artifacts.
- Empty nested arrays mean only no further subtasks observed in these snapshots. Missing full descriptions are expected collection gaps, not blockers. Neither statuses nor saved hierarchy coverage establish completion or exhaustive visibility.

## Validation

Local JSON inspection reconciled the assigned child set, record counts, expected versus actual nested-key sets, and S parent links. No network, browser, tests, generation, source/status edits or semantic assessment performed; only this report written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"11/11 assigned members and 5/5 nested subtasks reconciled with exact JSON locators, timestamps and coverage gaps."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-773.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read-only Python JSON inspection of hierarchy/member-index/subtasks and metadata","result":"passed","summary":"11 unique members present once each; five nested records present once each; expected/actual nested sets equal and all parents MOS-1037."}],
  "validationOutput": ["Missing nested keys: []; extra module-parent nested keys: []; parent issue object absent from member index."],
  "residualRisks": ["Snapshot visibility is not exhaustive; direct-member full details and all comments/custom acceptance coverage remain uncollected; attachment binaries not downloaded."],
  "noStagedFiles": true,
  "diffSummary": "Assigned inventory report only; no source/status changes or staging operations.",
  "reviewFindings": ["No inventory blockers found."],
  "manualNotes": "Inventory-only inspection; no business interpretation, scenario analysis or tests. noStagedFiles denotes no staging performed by this run, not a repository-wide staging inspection."
}
```
