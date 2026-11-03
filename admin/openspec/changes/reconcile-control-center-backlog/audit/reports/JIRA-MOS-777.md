# MOS-777 — bounded hierarchy inventory

## Sources and provenance

All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`; JSON locators use zero-based array indices.

- Instructions: `work-items/JIRA-MOS-777.md` and `work-items/JIRA-INVENTORY-HANDOFF.md`. The supplemental handoff supersedes the pending-detail dependency: missing full descriptions are coverage gaps, not blockers.
- `sources/jira-hierarchy/r1/content.json` — `$.retrievedAt = 2026-10-16T11:08:08.629Z`; assigned entry `$.results[12]`, key `MOS-777`, type `Q key result`, five children. This is a hierarchy entry, not a collected full parent issue. Its status/update/details are absent.
- `sources/jira-member-index/r1/content.json` and `metadata.json` — both `$.retrievedAt = 2026-10-16T11:20:38.570Z`. Metadata selects summary, issuetype, status, subtasks, parent and updated, but actual member records must determine field presence. Metadata's pending-subtask note is older than the available subtask packet.
- `sources/jira-subtasks/r1/content.json` and `metadata.json` — both `$.retrievedAt = 2026-10-16T11:23:01.951Z`. Checked saved item keys and parent links against this module's assigned members; no matching nested records.
- `sources/jira-api-delta-scenarios/r1/content.json` — `$.retrievedAt = 2026-10-16T11:23:51.742Z`. Key-only applicability check found no assigned member; no supplementary bodies assessed.

## Member reconciliation

Every row has exactly one hierarchy occurrence and exactly one member-index record. Hierarchy locators below are within `sources/jira-hierarchy/r1/content.json`; index locators are within `sources/jira-member-index/r1/content.json`. The type, status, update and summary values come from the corresponding record's `.type`, `.status`, `.updated` and `.summary` fields.

| Member | Saved summary | Hierarchy locator | Index locator | Type | Status | Updated (verbatim) |
|---|---|---|---|---|---|---|
| MOS-885 | [B] Реализовать модуль "Отчеты" | `$.results[12].children[0]` | `$.items[78]` | Development task | Backlog | 2026-10-16T19:20:12.520+0800 |
| MOS-916 | [FE][Отчёты] Показать шаблоны отчётов и запуск в конструкторе | `$.results[12].children[1]` | `$.items[79]` | Development task | Backlog | 2026-10-15T14:16:19.727+0800 |
| MOS-919 | [FE][Отчёты] Подключить CSV-выгрузку из конструктора отчётов | `$.results[12].children[2]` | `$.items[80]` | Development task | Backlog | 2026-10-15T14:16:14.331+0800 |
| MOS-1015 | [FE][Отчёты] Создать конструктор отчёта с расширенным отбором | `$.results[12].children[3]` | `$.items[81]` | Development task | Hold | 2026-10-09T15:04:04.263+0800 |
| MOS-1016 | [FE][Отчёты] Сохранить отчёт как шаблон с расписанием | `$.results[12].children[4]` | `$.items[82]` | Development task | Backlog | 2026-10-09T15:04:07.048+0800 |

Identity-only comparison across `jira-hierarchy/r1/content.json:$.results[*].children[*]` found each assigned key exclusively at the locator above, with no duplicate or conflicting module membership. Within the assigned scope: five observed members, five unique keys, five index matches, zero missing index records, zero duplicate index matches and zero observed extra assigned-key records. Other modules' bodies and semantics were not assessed.

## Nested links and field coverage

For **each** of MOS-885, MOS-916, MOS-919, MOS-1015 and MOS-1016:

- Index record contains exactly `key`, `summary`, `type`, `status`, `updated`, `subtasks`.
- `.subtasks` is explicitly `[]` at the individual index locator above. Thus there are zero observed nested references to resolve, not proof that no hidden subtasks exist.
- `.parent` is **absent**, not an empty object or null. The direct module link is supported by the hierarchy children array, not independently confirmed by an index parent object.
- Full description, attachments, comments and custom acceptance fields are **absent**, not empty arrays, blank descriptions or evidence of no such content. Index presence supplies selected-field coverage only.

The saved subtask packet's `$.items[*].key` and `$.items[*].parent` checks found no record keyed by an assigned member and no nested record with an assigned member as parent. Consequently there is no observed nested parent mismatch, missing referenced subtask or extra parent-linked subtask to report for this module; no nested issue bodies were needed. The supplementary scenario packet supplies no additional coverage for these five keys.

## Limits and next collection

Inventory reconciliation is complete only for the observed saved hierarchy. No blocker or membership conflict was found. Status values do not establish implementation completion. Neither the explicit empty subtask arrays nor the hierarchy packet's lack of more/next controls establishes full visibility: `jira-hierarchy/r1/content.json:$.pagination` explicitly warns about hidden permission-filtered issues.

Retain each packet's separate retrieval timestamp and each member's verbatim update timestamp; later packet retrievals do not replace earlier provenance. For subsequent collection, the exact member keys needing full description, attachment metadata, comments, custom acceptance coverage and explicit parent confirmation are **MOS-885, MOS-916, MOS-919, MOS-1015, MOS-1016**. If parent detail/visibility confirmation is required, collect **MOS-777** itself; this report does not claim its full object exists. Recheck each member's subtask list under known visibility and collect only newly observed nested keys and parent links. No arbitrary linked issues, business semantics or implementation were assessed.

## Validation

Local read-only JSON inspection verified counts, actual field presence, assigned-key multiplicity and saved nested parent links. No network, browser, tests, generation, source edits or status edits were performed; only this bound report was written.
