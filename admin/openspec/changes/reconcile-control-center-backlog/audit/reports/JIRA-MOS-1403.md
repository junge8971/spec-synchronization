# MOS-1403 — observed Jira inventory

## Sources and membership
Paths below are relative to the audit root; JSON locators use zero-based indices. Applied `work-items/JIRA-INVENTORY-HANDOFF.md`, which supersedes the original pending-detail dependency.

- `sources/jira-hierarchy/r1/content.json`, `$.results[25]`: MOS-1403, type **Q key result**, children exactly `["MOS-1386"]`. Snapshot `$.retrievedAt`: **2026-10-16T11:08:08.629Z**. One module entry; one child occurrence, one distinct assigned member, no duplicates. MOS-1386 occurs in no other hierarchy child array.
- `sources/jira-member-index/r1/content.json`, `$.items[145]`: exactly one matching member record among 146 items. Snapshot `$.retrievedAt`: **2026-10-16T11:20:38.570Z**, corroborated by sibling `metadata.json`, `$.retrievedAt`.
- `sources/jira-subtasks/r1/content.json`, `$.items`: all 16 saved records checked for matching keys and parent links. Snapshot `$.retrievedAt`: **2026-10-16T11:23:01.951Z**, corroborated by sibling `metadata.json`, `$.retrievedAt`.

## Assigned member and field coverage

| Member | Summary | Type | Status | Issue updated | Exact locator |
|---|---|---|---|---|---|
| MOS-1386 | [B] Реализовать раздел "API" | Development task | Hold | 2026-10-15T18:08:32.599+0800 | `sources/jira-member-index/r1/content.json#/items/145` |

The record contains exactly `key`, `summary`, `type`, `status`, `updated`, and `subtasks`. `subtasks` is explicitly `[]`. No `parent`, full description, attachments, comments, or custom acceptance fields are present. The member-index metadata's requested `parent` field is not evidence that this individual record contains it. Membership under MOS-1403 is evidenced by hierarchy `#/results/25/children/0`, not an independently collected member parent field.

## Reconciliation and nested links

- Assigned set and matching index set are both `{MOS-1386}`: no missing assigned record, duplicate record, or observed extra assigned key.
- Neither the member-index nor subtask packet has a record with `parent` referencing MOS-1403 or MOS-1386. No subtask record has either key. Thus there are zero observed nested children for this member, consistent with its explicit empty `subtasks` array; no nested parent-link conflict is observed.
- MOS-1403 has a hierarchy entry, **not a full parent issue object** in these packets: it is absent as an item key from both detail collections. Its status, issue update time, description, attachments, comments, and custom acceptance coverage are not available here.
- Supplementary scenario descriptions are restricted by handoff to four other keys; none is assigned to this module, so that packet is not applicable.

## Limits and next collection

This is an inventory of saved observations, not a completeness claim against hidden or permission-filtered issues. Hierarchy `$.pagination` reports no more/next controls but explicitly disclaims such completeness. Snapshot retrieval times above remain distinct from the member's issue update time. Status does not establish completion.

Expected coverage gaps are not blockers. Next collection keys: **MOS-1403** for the full parent record and **MOS-1386** for missing description/attachments/comments/custom acceptance fields and an independently saved parent link. No additional nested key is supported by current evidence. No business, scenario, or implementation assessment performed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Verified one assigned member, exact multiplicity and locators, snapshot timestamps, explicit empty subtasks, available parent links, and field gaps."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-1403.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python JSON inspection of hierarchy, member-index, subtasks and metadata","result":"passed","summary":"MOS-1403 results[25]; MOS-1386 items[145]; no matching parent-linked records or duplicate membership."}],
  "validationOutput": ["Assigned members: 1; matching index records: 1; observed nested subtasks: 0."],
  "residualRisks": ["Saved hierarchy cannot exclude hidden issues; full parent issue and member detail fields are absent."],
  "noStagedFiles": true,
  "diffSummary": "Wrote only the bound inventory report; no source or status edits.",
  "reviewFindings": ["No inventory blockers observed."],
  "manualNotes": "Inspected both mandatory work items and available relevant packets locally. No network, browser, tests, generation, or nested agents used."
}
```
