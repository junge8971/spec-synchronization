# MOS-1327 — saved-packet inventory

## Scope and sources

Inventory only; no business-semantic, scenario or implementation assessment. The supplemental `work-items/JIRA-INVENTORY-HANDOFF.md` supersedes the pending-detail dependency in `work-items/JIRA-MOS-1327.md`. All paths below are relative to the audit root; JSON locators use zero-based array indices.

| Saved source | Retrieval timestamp | Exact relevant locator |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `2026-10-16T11:08:08.629Z` | `$.results[21]`; collection caveats at `$.method`, `$.classification`, `$.pagination` |
| `sources/jira-member-index/r1/content.json` | `2026-10-16T11:20:38.570Z` | `$.items[138]`, `$.items[139]` |
| `sources/jira-subtasks/r1/content.json` | `2026-10-16T11:23:01.951Z` | `$.items[*].key`, `$.items[*].parent` checked for assigned keys |
| `sources/jira-api-delta-scenarios/r1/content.json` | `2026-10-16T11:23:51.742Z` | `$.items[*].key` checked; no assigned member matches |

The three detail-packet `r1/metadata.json` files were also inspected (`$.retrievedAt`, `$.limitations`; member index additionally `$.fields`). Newer packets do not replace earlier snapshot provenance.

## Assigned members and multiplicities

Hierarchy `$.results[21]` identifies MOS-1327 as **Q key result**, with exactly two observed child occurrences, both unique. Each key occurs only once across the hierarchy's saved child lists, under MOS-1327, and exactly once in the member index. No missing assigned index record, duplicate assigned key, or conflicting saved module membership was found.

| Member | Hierarchy locator | Member-index locator | Observed type | Observed status | Issue updated timestamp | Nested references |
| --- | --- | --- | --- | --- | --- | --- |
| MOS-1321 — [B] Реализовать раздел "Справочники" | `$.results[21].children[0]` | `$.items[138]` | Development task | Hold | `2026-10-14T14:03:49.652+0800` | `$.items[138].subtasks = []` |
| MOS-1399 — [B] Актуализировать справочники для справочников | `$.results[21].children[1]` | `$.items[139]` | Development task | Hold | `2026-10-15T19:28:04.537+0800` | `$.items[139].subtasks = []` |

Neither selected member record contains a `parent` field; the saved hierarchy, not an issue-detail parent object, supplies its module membership evidence. MOS-1327 itself has no issue record in the member-index, subtask or supplementary packet; only the hierarchy entry is evidenced here.

## Nested parent-link reconciliation

The assigned index records contain zero observed nested references. Checking the subtask packet's saved keys and parent values found no record whose key is an assigned member and no record whose parent is MOS-1321 or MOS-1399. Thus there are no observed nested links to reconcile, missing referenced subtask details, duplicate nested references or extra subtask records attached to these members in these packets. This is an empty observed nested inventory, not proof that no subtasks exist or are visible elsewhere.

## Field coverage and remaining collection

| Member | Index presence | Full description | Attachments | Comments | Custom acceptance fields |
| --- | --- | --- | --- | --- | --- |
| MOS-1321 | Present once | Not collected | Not collected | Not collected | Not collected |
| MOS-1399 | Present once | Not collected | Not collected | Not collected | Not collected |

The actual selected records contain only `key`, `summary`, `type`, `status`, `updated`, and `subtasks`. The supplementary description packet has neither assigned key, so it adds no coverage. Missing fields are coverage gaps, not assertions of empty issue content and not blockers. Member-index metadata's historical “nested subtask details pending” note does not negate the available subtask packet checked above.

Next collection keys, if fuller evidence is required: **MOS-1321, MOS-1399** for descriptions, attachment metadata, comments, custom acceptance fields and refreshed parent/subtask fields; **MOS-1327** only if its own issue-detail object is required. No additional nested key is observed for collection.

## Limitations and result

All two observed assigned members are accounted for; no saved membership conflict was found. Hierarchy collection used loaded HTML, with no more/next controls found; that does not establish completeness against hidden or permission-filtered issues. Empty arrays and statuses establish neither completion nor visibility. This inventory preserves the distinct retrieval and issue-update timestamps above. Only the bound report was written; no source/status edits, tests, network, browser or generation were performed.
