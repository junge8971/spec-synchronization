# MOS-775 — bounded saved-packet inventory

## Scope and sources

Inventory only, governed by `work-items/JIRA-MOS-775.md` and supplemental `work-items/JIRA-INVENTORY-HANDOFF.md`. Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit`; JSON locators use zero-based array indexes.

| Source | Exact locator / retrieval timestamp | Use |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `$.results[10]`, line 18; `$.retrievedAt` = `2026-10-16T11:08:08.629Z` | MOS-775 module membership; type `Q key result` |
| `sources/jira-member-index/r1/content.json` | `$.items[74:77]` (indexes 74–76), lines 653–676; `$.retrievedAt` = `2026-10-16T11:20:38.570Z` | Selected member records |
| `sources/jira-member-index/r1/metadata.json` | `$.retrievedAt`, `$.fields`, `$.limitations`; retrieval `2026-10-16T11:20:38.570Z` | Index field coverage |
| `sources/jira-subtasks/r1/content.json` | `$.items` scanned for assigned member keys and their parent links; `$.retrievedAt` = `2026-10-16T11:23:01.951Z` | Nested-record reconciliation |
| `sources/jira-subtasks/r1/metadata.json` | `$.retrievedAt`, `$.limitations`; retrieval `2026-10-16T11:23:01.951Z` | Subtask packet coverage |

Supplementary delta-description allowlist (MOS-1245/MOS-1306/MOS-1237/MOS-959) has no intersection with assigned membership; that packet was not inspected. No unrelated task/wiki packets or implementation were analyzed.

## Member inventory

Every row has hierarchy multiplicity **1**, index-record multiplicity **1**, and **0** corresponding records in the subtask packet. Hierarchy locators are under `sources/jira-hierarchy/r1/content.json`; index locators are under `sources/jira-member-index/r1/content.json`.

| Member | Saved summary | Observed type | Observed status | Issue updated (verbatim) | Exact membership / record locator |
| --- | --- | --- | --- | --- | --- |
| MOS-1146 | [B] Добавить хранение и отображение инцидентов навыка | Development task | Ready for test | `2026-10-12T14:56:06.450+0800` | `$.results[10].children[0]`; `$.items[74]`, lines 653–660 |
| MOS-1397 | [B] Мониторинг навыка | Development task | Development | `2026-10-16T19:20:13.916+0800` | `$.results[10].children[1]`; `$.items[75]`, lines 661–668 |
| MOS-1398 | [B] Ответственные по навыку | Development task | Backlog | `2026-10-15T17:04:57.918+0800` | `$.results[10].children[2]`; `$.items[76]`, lines 669–676 |

### Multiplicity and nested parent reconciliation

- Assigned hierarchy entry occurs once: 3 child occurrences, 3 unique keys. Each assigned key occurs under MOS-775 only in the saved hierarchy; no cross-module membership conflicts observed for these keys.
- All 3 assigned members have exactly one index record: no missing or duplicate assigned-key records. Their selected records contain no `parent` field; membership evidence is the hierarchy, not an independently collected member-to-module parent object.
- Each member's `$.items[74].subtasks`, `$.items[75].subtasks`, and `$.items[76].subtasks` is explicitly `[]`: 0 observed nested keys, 0 duplicate nested occurrences.
- Across `sources/jira-subtasks/r1/content.json#$.items`, no record has an assigned member key and no `parent` links to MOS-1146, MOS-1397, or MOS-1398. Thus no observed nested parent link needs reconciliation and no missing or extra nested records were detected for this module. Unrelated records are outside this inventory, not extras.
- MOS-775 itself has no issue record in either member-index or subtask packet. Its hierarchy entry is collected; a detailed module issue/parent object is not established by these inputs.

## Per-member coverage and collection gaps

| Member | Selected index fields | Full description | Attachments | Comments | Custom acceptance fields |
| --- | --- | --- | --- | --- | --- |
| MOS-1146 | Present; summary/type/status/updated/subtasks | Not collected | Not collected | Not collected | Not collected |
| MOS-1397 | Present; summary/type/status/updated/subtasks | Not collected | Not collected | Not collected | Not collected |
| MOS-1398 | Present; summary/type/status/updated/subtasks | Not collected | Not collected | Not collected | Not collected |

Missing detail fields are expected coverage gaps, not blockers or evidence of empty issue content. The index metadata's older “nested subtask details pending” note is superseded by the available subtask packet and supplemental handoff; none of that packet's observed nested records belongs to this module.

Next collection keys: **MOS-1146, MOS-1397, MOS-1398** for full descriptions, attachment metadata/content as authorized, comments, custom acceptance coverage, and refreshed subtask/parent evidence. Collect **MOS-775** separately if module issue details are required. No additional nested keys can be named from this snapshot.

## Limitations and result

All 3 observed members are accounted for; no membership conflict or missing required packet was encountered. Retrieval timestamps and issue update timestamps are distinct and preserved above; no newer snapshot overwrites older provenance. Hierarchy collection used loaded child-panel HTML: its `$.pagination` caveat explicitly says lack of more/next controls does not prove visibility of permission-filtered issues. Status values and empty subtask arrays do not prove completion or full visibility. No business-semantic or implementation assessment, network/browser activity, tests, or source/status edits were performed.
