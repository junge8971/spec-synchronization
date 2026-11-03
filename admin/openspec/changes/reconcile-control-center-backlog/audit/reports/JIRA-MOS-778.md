# MOS-778 — saved-packet inventory

## Scope and evidence

Inventory only, governed by `work-items/JIRA-MOS-778.md` and supplemental `work-items/JIRA-INVENTORY-HANDOFF.md`; the latter supersedes the pending-detail dependency. All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit`; JSON locators use zero-based array indices.

- `sources/jira-hierarchy/r1/content.json`, `$.results[13]`: MOS-778, type `Q key result`, six observed children. Snapshot `$.retrievedAt` = `2026-10-16T11:08:08.629Z`. Collection used saved parent-browser child-panel evidence; `$.pagination` explicitly warns that loaded HTML does not establish visibility of permission-filtered issues.
- `sources/jira-member-index/r1/content.json`, `$.items[83:89]` (indices 83–88 inclusive): all six selected member records. Snapshot `$.retrievedAt` = `2026-10-16T11:20:38.570Z`, also recorded in `sources/jira-member-index/r1/metadata.json`, `$.retrievedAt`. Metadata `$.fields` lists the selected request fields; actual records determine field presence.
- `sources/jira-subtasks/r1/content.json`, `$.items[0:16]` (indices 0–15 inclusive): checked key/parent identities only for association with this module. Snapshot `$.retrievedAt` = `2026-10-16T11:23:01.951Z`, corroborated by `sources/jira-subtasks/r1/metadata.json`, `$.retrievedAt`. No matching parent links or assigned keys; unrelated bodies were not analyzed. Metadata `$.limitations` describes attachments as enumerated, not downloaded, and excludes comments/custom acceptance fields.

The supplementary description allowlist (MOS-1245/MOS-1306/MOS-1237/MOS-959) has no intersection with this module; its bodies were not inspected.

## Observed members

Each hierarchy locator below is within `sources/jira-hierarchy/r1/content.json`; each index locator is within `sources/jira-member-index/r1/content.json`. Type/status/update values are the `.type`, `.status`, and `.updated` fields of the cited index object, not assertions of completion.

| Key | Hierarchy locator | Index locator | Type | Status | Updated (verbatim) |
|---|---|---|---|---|---|
| MOS-734 | `$.results[13].children[0]` | `$.items[83]` | Development task | Review | 2026-10-09T15:04:35.974+0800 |
| MOS-818 | `$.results[13].children[1]` | `$.items[84]` | Development task | Testing | 2026-10-09T15:03:46.554+0800 |
| MOS-915 | `$.results[13].children[2]` | `$.items[85]` | Development task | Backlog | 2026-10-15T14:47:06.054+0800 |
| MOS-1011 | `$.results[13].children[3]` | `$.items[86]` | Development task | Backlog | 2026-10-09T15:03:37.175+0800 |
| MOS-1012 | `$.results[13].children[4]` | `$.items[87]` | Development task | Backlog | 2026-10-09T15:03:41.168+0800 |
| MOS-1013 | `$.results[13].children[5]` | `$.items[88]` | Development task | Backlog | 2026-10-09T15:03:44.322+0800 |

## Reconciliation and field coverage

- Six child occurrences, six distinct keys. Each assigned key occurs exactly once across saved hierarchy child-key arrays and exactly once in the member index. Identity-only cross-check found no alternate module placement, duplicate, or missing assigned member. No extra record is attributable to MOS-778 by saved parent links.
- Each of the six cited index objects has exactly `key`, `summary`, `type`, `status`, `updated`, and `subtasks`. Each `.subtasks` is explicitly `[]`; `.parent` is absent, not an empty object or array. Module membership is supported by the hierarchy, not an independently collected member parent field.
- For **each** of MOS-734, MOS-818, MOS-915, MOS-1011, MOS-1012, MOS-1013: selected index coverage is present; full description, attachments, comments, and custom acceptance fields are absent, not observed empty collections. A summary is not a full description.
- The union of observed member subtask references is empty. Checking `sources/jira-subtasks/r1/content.json`, `$.items[0]` through `$.items[15]`, specifically each `.key` and `.parent`, found no parent equal to any assigned member (or MOS-778) and no key equal to an assigned member. Thus there is no observed nested subtask to reconcile or collect for this module in these packets; no dangling reference, duplicate nested key, or conflicting nested parent was found within assigned scope. This does not establish that Jira has no hidden/unloaded subtasks.
- MOS-778 is present as a hierarchy object only. No MOS-778 issue-detail object occurs in either selected-member or subtask packet. Its status/update/full description and other detail fields are not established by the hierarchy entry.
- The member metadata's “nested subtask details pending” wording is older than the available subtask packet; the actual later packet was checked without overwriting the earlier snapshot's provenance.

## Residual coverage and next collection

No required-file or membership blocker found. The six-member observed inventory is reconciled, not a claim of full Jira visibility or implementation completion. Status labels and empty subtask arrays provide neither assurance.

Next detail-collection keys: MOS-734, MOS-818, MOS-915, MOS-1011, MOS-1012, MOS-1013 for missing full descriptions, attachment metadata/content coverage, comments, and custom acceptance coverage. Collect MOS-778 separately if parent issue details are needed. No nested child keys are currently observed to queue; any later collection must recheck subtask visibility and retain snapshot provenance. No business semantics, external links, implementation, or other module bodies were assessed. No network, browser, tests, generation, source edits, or status edits were performed.
