# MOS-776 — bounded hierarchy inventory

## Scope and sources

Inventory only; supplemental `work-items/JIRA-INVENTORY-HANDOFF.md` supersedes the pending-detail dependency in `work-items/JIRA-MOS-776.md`. Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit`; locators use zero-based JSON array indices.

- `sources/jira-hierarchy/r1/content.json`: `$.retrievedAt` = `2026-10-16T11:08:08.629Z`; assigned entry `$.results[11]`.
- `sources/jira-member-index/r1/content.json`: `$.retrievedAt` = `2026-10-16T11:20:38.570Z`; corresponding `metadata.json` confirms selected identity/status/update/subtask fields, not descriptions/comments/attachments/custom acceptance fields.
- `sources/jira-subtasks/r1/content.json`: `$.retrievedAt` = `2026-10-16T11:23:01.951Z`; corresponding `metadata.json` documents selected-field extraction, attachments enumerated rather than downloaded, and no comments/custom acceptance fields.
- Supplementary delta descriptions are not applicable: none of the handoff's four eligible keys belongs to this module. No other module bodies or business semantics were inspected.

## Observed membership and multiplicity

`$.results[11]` is `{ "key": "MOS-776", "type": "Q key result", "children": ["MOS-1145"] }` in the hierarchy packet. MOS-776 appears once as a module entry. Its one child is unique within that entry and occurs once across saved hierarchy child lists, at `$.results[11].children[0]`; no conflicting membership was observed. Cross-module checking was limited to key membership.

| Member | Exact selected record | Type | Status | Jira updated timestamp | Coverage |
| --- | --- | --- | --- | --- | --- |
| MOS-1145 | `sources/jira-member-index/r1/content.json: $.items[77]` | Development task | Ready for test | `2026-10-09T17:28:57.640+0800` | One matching record; `subtasks: []` explicitly present |

Selected summary at `$.items[77].summary`: `[B] Реализовать отключение и повторное включение навыка`.

Expected direct members: 1; matching index records: 1; missing direct-member keys: 0; duplicate matching index records: 0. MOS-1145 has no detail record in the subtask packet, as expected for a direct member with no observed subtasks. No extra records carrying parent `MOS-776` or `MOS-1145` were found in either packet. Unrelated packet records are not extras in this module inventory.

## Nested links and field coverage

- `sources/jira-member-index/r1/content.json: $.items[77].subtasks` is an explicit empty array, not an absent field. There are no listed nested keys requiring reconciliation.
- Across `sources/jira-subtasks/r1/content.json: $.items[*].parent` (stored string keys), zero records point to MOS-1145 or MOS-776. Therefore no observed nested parent links remain unmatched; this does not establish that hidden subtasks do not exist.
- At `$.items[77]`, `parent`, `description`, `attachments`, `comments`, and custom acceptance fields are absent, not empty arrays or empty descriptions. The member-to-module relationship is evidenced by the hierarchy child list, not by a collected member `parent` field.
- MOS-776 itself is present only as the selected hierarchy entry: no MOS-776 issue record exists in either member-index or subtask items. Its status/update timestamp and full parent issue fields were not collected in these packets.
- Full description, attachment metadata/content, comments, and custom acceptance coverage for MOS-1145 remain unavailable. Index presence and `Ready for test` do not establish completion or full visibility.

## Limitations and next collection

Hierarchy `$.method` documents saved parent-browser DOM extraction of child links. `$.pagination` states no more/next controls were found but explicitly warns that loaded HTML does not prove absence of permission-filtered issues. Snapshot retrieval times above remain separate from the issue update timestamp; the subtask metadata's later snapshot does not enrich MOS-1145. The index metadata's historical statement that nested details were pending is superseded by the available subtask packet, without implying additional visibility here.

Next collection key for missing full member fields: **MOS-1145**. Collect **MOS-776** separately only if full module-parent details or renewed child-panel evidence is required; no full parent object is claimed here. No observed nested keys are pending. Missing full descriptions are expected coverage gaps, not blockers. No membership conflicts or required-input blockers were found.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "Reconciled the single MOS-776 child against one index record; checked hierarchy multiplicity and both packets for nested parent links; documented exact locators, timestamps, absent fields and explicit empty subtasks."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-776.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command": "Read-only local Python JSON inspection of hierarchy, member-index and subtask packets and metadata", "result": "passed", "summary": "One unique assigned member, one index match, zero observed nested links or membership conflicts."}],
  "validationOutput": ["MOS-776: results[11]; MOS-1145: items[77]; subtasks explicitly []."],
  "residualRisks": ["Saved snapshots cannot exclude hidden or permission-filtered issues.", "Full MOS-1145 fields and full MOS-776 parent issue record are absent."],
  "noStagedFiles": true,
  "diffSummary": "Wrote only the bound inventory report; no source or status edits.",
  "reviewFindings": ["No inventory blockers observed."],
  "manualNotes": "Inventory-only inspection; no network, browser, tests, generation or business-semantic analysis. No staging operations performed."
}
```
