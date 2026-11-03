# MOS-769 — saved hierarchy inventory

## Scope and provenance

Inventory only; supplemental `work-items/JIRA-INVENTORY-HANDOFF.md` supersedes the original pending-detail dependency. Paths below are relative to the audit root; JSON locators use zero-based array indexes.

- `sources/jira-hierarchy/r1/content.json`, `$.retrievedAt`: `2026-10-16T11:08:08.629Z`. Assigned module is `$.results[4]`, key `MOS-769`, type `Q key result`, with two observed children. This is a hierarchy entry, not a collected full parent issue object.
- `sources/jira-member-index/r1/content.json`, `$.retrievedAt`: `2026-10-16T11:20:38.570Z`; corroborated by `sources/jira-member-index/r1/metadata.json`, `$.retrievedAt`. Selected-field index, not full issue details.
- `sources/jira-subtasks/r1/content.json`, `$.retrievedAt`: `2026-10-16T11:23:01.951Z`; corroborated by `sources/jira-subtasks/r1/metadata.json`, `$.retrievedAt`. Saved explicit nested-subtask packet.

## Assigned members

| Member | Saved summary | Type | Status (observation only) | Issue updated | Exact membership / index locators |
| --- | --- | --- | --- | --- | --- |
| MOS-903 | [B] Реализовать API приема событий в МПММ | Development task | Ready for test | 2026-10-09T15:04:02.033+0800 | hierarchy `$.results[4].children[0]`; member-index `$.items[42]` |
| MOS-908 | [B] Реализовать отправку событий аудита из ЦАМ в МПММ | Development task | Ready for test | 2026-10-09T15:03:52.967+0800 | hierarchy `$.results[4].children[1]`; member-index `$.items[43]` |

All field values in the table come from the corresponding index object's `.summary`, `.type`, `.status`, and `.updated`; packet paths and collection times are given above.

## Multiplicity and nested-parent reconciliation

- One hierarchy entry for MOS-769; two child occurrences and two distinct child keys.
- MOS-903 occurs once in the saved hierarchy child arrays, at `$.results[4].children[0]`, and once in the index, at `$.items[42]`.
- MOS-908 occurs once in the saved hierarchy child arrays, at `$.results[4].children[1]`, and once in the index, at `$.items[43]`.
- Assigned-member index coverage: 2/2. Missing assigned keys: none. Duplicate assigned records or conflicting hierarchy assignments: none observed. No extra assigned keys observed; other modules' index records are outside scope.
- `member-index $.items[42].subtasks` and `$.items[43].subtasks` are both `[]`. Both records lack a `.parent` field: their MOS-769 membership is established by the hierarchy, not an independent index parent assertion.
- Checked `sources/jira-subtasks/r1/content.json`, `$.items[*].parent`: no saved record has parent MOS-903, MOS-908, or MOS-769. Thus zero explicit nested keys, zero relevant nested detail records, zero observed parent-link conflicts, and no expected nested keys missing from this packet. There are no relevant nested record locators to enumerate. Empty observations do not establish that hidden or uncollected subtasks do not exist.
- MOS-769 itself has no record in `member-index $.items`; no full parent issue collection is asserted.

## Coverage gaps and next collection

For **each** of MOS-903 and MOS-908: index presence confirmed; full description, attachments, comments, and custom acceptance fields are **not collected in these inputs**, not proven empty. The index metadata explicitly excludes these fields (`$.limitations`); its note that nested details were pending is supplemented by the later saved subtask packet, without replacing the older snapshot provenance.

Neither assigned member is among the four allowed supplementary description keys, so no API-delta scenario packet was inspected. No business semantics, implementation, unrelated task/wiki packets, or scenario reports were analyzed.

Next collection keys: MOS-903 and MOS-908 for full descriptions, attachment metadata, comments, custom acceptance fields, and a refreshed explicit subtask listing. If new nested keys appear, collect their parent links and detail records. Collect MOS-769 separately only if full parent detail coverage is required.

The hierarchy's `$.pagination` says no more/next controls were found but explicitly disclaims completeness against permission-filtered issues. Statuses and empty arrays do not prove completion or full visibility. Snapshot inventory is reconciled; broader Jira completeness and business completion remain unassessed.
