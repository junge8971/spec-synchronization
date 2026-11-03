# MOS-1388 — observed inventory

Scope: inventory only. Paths below are relative to the audit root. The supplemental `work-items/JIRA-INVENTORY-HANDOFF.md` supersedes the work item's pending-detail dependency; missing descriptions are coverage gaps, not blockers.

## Membership and multiplicity

- `sources/jira-hierarchy/r1/content.json` `$.results[24]`: `{ "key": "MOS-1388", "type": "Q key result", "children": ["MOS-1387"] }`. The children array is **not empty**: one entry, one unique member.
- MOS-1388 occurs as a hierarchy entry exactly once. MOS-1387 occurs in hierarchy child arrays exactly once, at `$.results[24].children[0]`; no duplicate or competing module assignment was observed across the 26 entries.
- `sources/jira-member-index/r1/content.json` `$.items[144]` contains MOS-1387 exactly once across 146 items. Assigned/index reconciliation: 1/1 present, no missing or duplicate assigned records. Other module records are outside this inventory, not extra assigned members.

| Member and exact locator | Observed summary | Type | Status | Issue updated | Nested references |
| --- | --- | --- | --- | --- | --- |
| MOS-1387 — `sources/jira-member-index/r1/content.json` `$.items[144]` | [B] Реализовать раздел "Шаблоны ответов" | Development task | Hold | `2026-10-16T19:20:12.207+0800` | `$.items[144].subtasks = []` |

## Parent links and field coverage

- MOS-1387's index object has exactly `key`, `summary`, `type`, `status`, `updated`, and `subtasks`. Its `parent` field is absent: the module relationship is evidenced by the hierarchy children array, not a collected issue parent field.
- All 16 records in `sources/jira-subtasks/r1/content.json` `$.items[*].parent` were checked: none points to MOS-1387 or MOS-1388. Neither key occurs as a subtask record. Thus no observed nested keys require reconciliation; this is not proof that no hidden/uncollected subtasks exist.
- MOS-1387 has index coverage only. Description, attachments, comments, and custom acceptance fields are absent, not evidenced as empty. No MOS-1387 record appears in `sources/jira-api-delta-scenarios/r1/content.json` `$.items[*]`; no supplementary descriptions apply to this module.
- MOS-1388 is a collected **hierarchy entry**, not a collected full parent issue: no record with that key occurs in member-index, subtasks, or supplemental scenario items. Its summary, status, issue-update time, description, attachments, comments, and custom acceptance coverage are unavailable in these packets. Only hierarchy key/type/children are observed.

## Snapshot provenance and limits

Exact collection-time locators: each packet's `content.json` `$.retrievedAt`, corroborated by its sibling `metadata.json` `$.retrievedAt`:

| Source directory | Retrieved at |
| --- | --- |
| `sources/jira-hierarchy/r1/` | `2026-10-16T11:08:08.629Z` |
| `sources/jira-member-index/r1/` | `2026-10-16T11:20:38.570Z` |
| `sources/jira-subtasks/r1/` | `2026-10-16T11:23:01.951Z` |
| `sources/jira-api-delta-scenarios/r1/` | `2026-10-16T11:23:51.742Z` |

Hierarchy `$.method` records saved same-origin browser DOM extraction; `$.pagination` says no more/next controls were found, but loaded HTML does not establish completeness against permission-filtered issues. `$.classification` identifies module parents as Q key result, not literal Epic. Packet timestamps remain separate from the member issue's update time; no newer packet overwrites older provenance. Member-index metadata's pending-subtask note is historical: the available subtask packet was checked directly.

Next collection keys, if fuller coverage is required: MOS-1388 (full parent issue) and MOS-1387 (omitted full fields and refreshed nested references). No additional nested keys are observed. No blockers or membership conflicts found; statuses imply no completion conclusion. No business, scenario, or implementation assessment performed.
