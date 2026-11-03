# MOS-1329 — saved-packet inventory

## Scope and provenance

Inventory only, applying `work-items/JIRA-MOS-1329.md` and the superseding `work-items/JIRA-INVENTORY-HANDOFF.md`. Paths below are relative to the audit root; JSON array locators are zero-based.

| Saved source | Retrieval timestamp | Exact relevant locator |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `2026-10-16T11:08:08.629Z` | `$.results[23]`; caveats at `$.method`, `$.classification`, `$.pagination` |
| `sources/jira-member-index/r1/content.json` | `2026-10-16T11:20:38.570Z` | `$.items[142]`, `$.items[143]` |
| `sources/jira-member-index/r1/metadata.json` | `2026-10-16T11:20:38.570Z` | `$.fields`, `$.limitations` |
| `sources/jira-subtasks/r1/content.json` | `2026-10-16T11:23:01.951Z` | `$.items[*].parent` (all 16 records checked for assigned-parent matches) |
| `sources/jira-subtasks/r1/metadata.json` | `2026-10-16T11:23:01.951Z` | `$.limitations` |

## Observed membership and multiplicities

`$.results[23]` records MOS-1329 as `Q key result`, with children `["MOS-1323", "MOS-1384"]`. The module entry occurs once. Both members occur once in its children, once across the saved hierarchy children, and once in the member index. No duplicate, missing assigned member, conflicting hierarchy membership, or additional module-associated record was observed. Other modules' index records are outside this inventory, not extras.

| Member | Hierarchy locator | Index locator | Observed type | Observed status | Issue update timestamp |
| --- | --- | --- | --- | --- | --- |
| MOS-1323 | `$.results[23].children[0]` | `$.items[142]` | Development task | Hold | `2026-10-14T14:03:53.543+0800` |
| MOS-1384 | `$.results[23].children[1]` | `$.items[143]` | Development task | Review | `2026-10-15T18:18:14.860+0800` |

Both index records contain `key`, `summary`, `type`, `status`, `updated`, and `subtasks`; neither contains a `parent` field. Their module membership is evidenced by the hierarchy, not an index parent link. MOS-1329 itself has no issue object in the inspected member-index or subtask packets; its hierarchy entry is not a full parent issue collection.

## Nested links and detail coverage

- `sources/jira-member-index/r1/content.json:$.items[142].subtasks` and `$.items[143].subtasks` are both `[]`: zero explicitly listed nested keys, so no listed nested key requires a detail-record reconciliation.
- Inspection of all 16 `sources/jira-subtasks/r1/content.json:$.items[*].parent` values found no parent equal to MOS-1323, MOS-1384, or MOS-1329. Neither assigned member appears as a subtask record. Thus no observed nested parent link, duplicate nested key, missing listed nested record, or extra nested record is attributable to this module.
- For **each** of MOS-1323 and MOS-1384: selected index record present; full description, attachment enumeration/content, comments, and custom acceptance fields **not collected in these records**. This is unavailable coverage, not evidence of empty issue fields.
- Supplemental description keys MOS-1245/MOS-1306/MOS-1237/MOS-959 are not assigned members; the supplementary packet is therefore inapplicable and was not inspected.

## Limitations and next collection keys

The hierarchy was extracted from saved parent-browser HTML. Its `$.pagination` explicitly warns that no more/next controls does not prove completeness against hidden permission-filtered issues. Empty subtask arrays and observed statuses establish neither completion nor visibility completeness. Snapshot retrieval times and issue update times above remain separate provenance; no newer snapshot substitutes for the hierarchy.

Next collection keys for missing full issue detail coverage: **MOS-1323, MOS-1384**. Collect descriptions, attachment metadata, comments, custom acceptance fields, and refreshed explicit subtask/parent fields as needed. **MOS-1329** is an additional key only if a full module-parent issue object is required. No nested issue keys were observed to queue. Missing descriptions are expected coverage gaps, not blockers.

Manual verification: local JSON inspection and occurrence/parent-link counts only; no network, tests, business-semantic analysis, implementation analysis, or source/status edits.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "Both assigned members reconciled exactly once with precise JSON locators and timestamps; all 16 saved nested parent links checked, with no module matches."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-1329.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command": "Read-only Python JSON inspection of hierarchy, member-index, subtask packets and metadata", "result": "passed", "summary": "2 unique assigned members, 2 selected index records, 0 explicitly listed or matching nested records."}],
  "validationOutput": ["No observed missing, duplicate, conflicting or extra module-associated keys."],
  "residualRisks": ["Full member descriptions, attachments, comments and custom acceptance coverage unavailable.", "Saved HTML and empty subtask arrays do not establish hidden-issue or current-state completeness."],
  "diffSummary": "Bound inventory report only.",
  "reviewFindings": ["No blockers in the inspected inventory evidence."],
  "manualNotes": "Inventory-only local inspection; no tests or external requests executed. Parent full issue object not present in inspected issue packets."
}
```
