# MOS-1328 — saved-packet inventory

## Scope and provenance

Inventory only, governed by `work-items/JIRA-MOS-1328.md` and supplemental `work-items/JIRA-INVENTORY-HANDOFF.md`; the latter supersedes the pending detail-packet dependency. Paths below are relative to the audit root. Locators are zero-based JSON paths.

| Packet | Saved retrieval timestamp | Relevant locators |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `2026-10-16T11:08:08.629Z` | `$.retrievedAt`, `$.results[22]`, `$.pagination`, `$.method` |
| `sources/jira-member-index/r1/content.json` | `2026-10-16T11:20:38.570Z` | `$.items[140]`, `$.items[141]` |
| `sources/jira-member-index/r1/metadata.json` | `2026-10-16T11:20:38.570Z` | `$.retrievedAt`, `$.fields`, `$.limitations` |
| `sources/jira-subtasks/r1/content.json` | `2026-10-16T11:23:01.951Z` | `$.retrievedAt`, `$.items` (16 records checked for assigned keys and parent references) |
| `sources/jira-subtasks/r1/metadata.json` | `2026-10-16T11:23:01.951Z` | `$.retrievedAt`, `$.limitations` |

Hierarchy evidence is saved parent-browser DOM extraction. `$.results[22]` records MOS-1328 as **Q key result**, with exactly two observed child occurrences, both unique. It does not contain the parent's status, update time or full issue detail. MOS-1328 has no issue record in the member-index or subtask packets inspected.

## Assigned members

| Member / observed summary | Membership locator in hierarchy | Index locator | Observed type | Observed status | Issue update timestamp | Nested evidence |
| --- | --- | --- | --- | --- | --- | --- |
| MOS-1322 — [B] Реализовать раздел "База знаний" | `$.results[22].children[0]` | `$.items[140]` | Development task | Hold | `2026-10-14T14:03:51.688+0800` | `$.items[140].subtasks = []` |
| MOS-1362 — [FE][База знаний] Реализовать раздел управления материалами как отключаемый модуль | `$.results[22].children[1]` | `$.items[141]` | Development task | Ready for test | `2026-10-14T18:14:20.314+0800` | `$.items[141].subtasks = []` |

Each index record contains only `key`, `summary`, `type`, `status`, `updated`, and `subtasks`. For **each** member: index presence is verified; full description, attachment metadata/content, comments and custom acceptance fields are not collected in these records. Neither has a `parent` field; the module-to-member relationship is supported by the hierarchy child panel, not independently confirmed by an index parent field. No assigned member is among the four keys eligible for the supplemental API-delta description packet.

## Multiplicity and nested-parent reconciliation

- MOS-1328 occurs once as a hierarchy module object, at `$.results[22]`.
- Each assigned key occurs once in the entire hierarchy child lists, exclusively under MOS-1328, and once in the 146-record member index at the locators above. No duplicate, missing assigned index record or conflicting module membership was found.
- Neither assigned key occurs as a nested reference in any member-index `$.items[*].subtasks[*].key`.
- In `sources/jira-subtasks/r1/content.json`, no `$.items[*].key` equals either assigned key; no `$.items[*].parent` equals MOS-1328, MOS-1322 or MOS-1362. Thus no saved nested record needs a parent-link reconciliation for this module, and no unexpected module-associated nested record was found.
- Observed nested reference set and matching nested-detail set are both empty: zero missing, duplicate or extra nested keys relative to this saved evidence. This does not establish absence of hidden or uncollected subtasks.

## Coverage limits and next collection

The hierarchy notes no more/next controls in the loaded child panels, explicitly without guaranteeing completeness against permission-filtered issues (`$.pagination`). Empty subtask arrays and statuses are recorded observations, not proof of completion, visibility or exhaustive coverage. Retrieval timestamps and issue-update timestamps remain separate snapshot provenance; the later subtask packet does not refresh member records. Member-index metadata's generic “nested subtask details pending” note is older than the available subtask packet and is not treated as a blocker.

Next detail-collection keys: **MOS-1322, MOS-1362**, for descriptions, attachments, comments, custom acceptance coverage and explicit parent confirmation. **MOS-1328** would require its own detail collection if parent status/update/full detail is needed. Recheck child/subtask listings if exhaustive or current visibility is required. Missing descriptions are expected coverage gaps, not blockers. No required-file, conflicting-membership or infrastructure blocker was encountered.

## Validation

Read-only local JSON inspection verified exact object indices, assigned-key multiplicities across hierarchy/index packets and nested parent references across the saved subtask packet. No network, browser, tests, generation, semantic analysis, source edits or status edits were performed; only this bound report was written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Both observed MOS-1328 members reconciled at exact JSON locators with timestamps, multiplicities, field coverage and nested-parent checks."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-1328.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only local Python JSON inspection of hierarchy, member-index, subtasks and metadata","result":"passed","summary":"Two unique assigned members, one index record each, zero matching nested references or parent-linked subtask records."}],
  "validationOutput": ["No duplicate, missing assigned index record, conflicting membership or unexpected associated nested key observed."],
  "residualRisks": ["Saved HTML and empty arrays cannot establish hidden-issue visibility or exhaustive membership.","Member descriptions, attachments, comments, custom acceptance fields and explicit index parent fields are not collected; parent full issue detail is absent."],
  "noStagedFiles": true,
  "diffSummary": "Bound inventory report only; no source/status edits.",
  "reviewFindings": ["No blockers in inspected evidence."],
  "manualNotes": "Supplemental handoff applied; inventory only. No tests or external requests were run. No staging operations were performed."
}
```
