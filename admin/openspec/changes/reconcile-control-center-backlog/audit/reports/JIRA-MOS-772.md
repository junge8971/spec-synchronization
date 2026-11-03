# MOS-772 — observed hierarchy inventory

## Evidence and membership
All source paths below are relative to the audit root. Both assigned work item and mandatory supplemental handoff were read; the latter supersedes the pending-detail dependency.

| Source / exact locator | Snapshot retrievedAt | Observation |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json`, `/results/7` (line 15) | `2026-10-16T11:08:08.629Z` | `key: MOS-772`, `type: Q key result`, `children: []`. Exactly one matching module entry; zero member occurrences, zero distinct members, zero duplicates. |
| `sources/jira-member-index/r1/content.json`, `/items` (146 records); accompanying `metadata.json`, `/fields`, `/limitations` | `2026-10-16T11:20:38.570Z` | No record with key MOS-772; no assigned children to reconcile. Actual records contain key, summary, type, status, updated, subtasks. None contains a parent field: this packet cannot independently establish parent-linked membership. |
| `sources/jira-subtasks/r1/content.json`, `/items` (16 records), each `/items/{i}/parent`, `i=0…15`; accompanying `metadata.json`, `/limitations` | `2026-10-16T11:23:01.951Z` | All 16 records have parent fields; none links to MOS-772 and none has key MOS-772. No observed assigned member exists to anchor a nested-subtask reconciliation. |

Observed assigned set is **empty**. Missing/extra indexed assigned keys and nested assigned keys: none observed; this is not a claim that uncollected issues do not exist. Supplementary API-delta descriptions are not applicable because no described key belongs to this empty observed set.

## Field coverage and boundaries
- MOS-772 is a **hierarchy entry**, not a collected full parent issue in the inspected packets. Its observed type is `Q key result`; summary, status, issue update timestamp, description, attachments, comments and custom acceptance fields are absent for this parent. Retrieval timestamps above are not issue update timestamps.
- There are no member rows for which type/status/update or full-detail coverage can be reported. Member-index presence must not be equated with full issue coverage: its metadata explicitly excludes descriptions, attachments, comments and custom acceptance fields.
- Subtask records provide descriptions and attachment metadata, but no comments/custom acceptance fields; attachments were not downloaded. Their presence elsewhere in the packet supplies no MOS-772 membership evidence. The older index metadata's pending-subtasks note is superseded by the available subtask snapshot, without merging snapshot timestamps.
- Hierarchy `/pagination` reports no more/next controls, while expressly warning that loaded HTML does not prove absence of hidden or permission-filtered issues. The finding is limited to observed membership.

## Next collection / residual risks
If additional completeness or parent-field evidence is required, next collection key is **MOS-772** (full parent issue and refreshed child panel). No child keys can legitimately be proposed from this snapshot. No membership conflict or required-packet blocker was found. No business/scenario/implementation assessment, network access, tests, source edits or status edits were performed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Verified explicit empty children at hierarchy /results/7, actual selected-field coverage, and absence of MOS-772 parent links across all 16 saved subtasks."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-772.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read-only Python JSON inspection of hierarchy, member-index and subtasks packets and metadata","result":"passed","summary":"Empty assigned set; 146 index records without parent fields; 16 subtask parent fields with no MOS-772 link."}],
  "validationOutput": ["One MOS-772 hierarchy entry; zero observed children or duplicate member occurrences."],
  "residualRisks": ["Hidden or permission-filtered children are not excluded; full MOS-772 parent issue fields are unavailable in inspected packets."],
  "diffSummary": "Created only the bound inventory report.",
  "reviewFindings": ["No blockers observed."],
  "manualNotes": "Supplemental handoff applied; missing full descriptions treated as coverage gaps, not blockers. No tests run for this inventory-only task."
}
```
