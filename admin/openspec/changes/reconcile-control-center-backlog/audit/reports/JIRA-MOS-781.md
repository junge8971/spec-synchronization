# MOS-781 — saved-packet membership inventory

## Scope and provenance

Inventory only; no business-semantic, scenario or implementation assessment. Applied `work-items/JIRA-MOS-781.md` and supplemental `work-items/JIRA-INVENTORY-HANDOFF.md`; the latter supersedes the pending detail-packet dependency. Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`. JSON array indices are zero-based.

| Saved source | Retrieval timestamp | Exact locator / use |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `2026-10-16T11:08:08.629Z` | `$.results[15]`: MOS-781, type `Q key result`; `$.results[15].children[0]`: MOS-890. Collection method and limitations: `$.method`, `$.classification`, `$.pagination`. |
| `sources/jira-member-index/r1/content.json` | `2026-10-16T11:20:38.570Z` | `$.items[90]` (lines 781–788): sole assigned member record. |
| `sources/jira-member-index/r1/metadata.json` | `2026-10-16T11:20:38.570Z` | `$.fields`, `$.limitations`: selected-field coverage, not full issue details. |
| `sources/jira-subtasks/r1/content.json` | `2026-10-16T11:23:01.951Z` | Checked `$.items[*].key` and `$.items[*].parent` against assigned keys; no MOS-890 child record. |
| `sources/jira-subtasks/r1/metadata.json` | `2026-10-16T11:23:01.951Z` | `$.scope` is in content; metadata `$.limitations` establishes attachment metadata only, no comments/custom acceptance fields. |

## Assigned member

| Key | Observed summary | Type | Status (snapshot only) | Issue update timestamp | Evidence |
| --- | --- | --- | --- | --- | --- |
| MOS-890 | [B] Реализовать модуль "Технические работы" | Development task | Ready for test | `2026-10-13T14:18:08.905+0800` | Hierarchy `$.results[15].children[0]`; member index `$.items[90]` |

MOS-890 is present once in the assigned hierarchy children and once in the member index. Its index record contains `key`, `summary`, `type`, `status`, `updated`, `subtasks`; it does **not** contain `parent`, description, attachments, comments or custom acceptance fields. Membership is therefore supported by the hierarchy, not by an independently collected issue parent field. Full description, attachment enumeration/content, comments and custom acceptance coverage are unavailable for this member, not established empty. None of the supplemental description allowlist keys belongs to this module; that packet is not applicable.

MOS-781 is observed as a hierarchy entry only: no member-index or subtask detail object for MOS-781 was found. Its issue status/update/full detail coverage is unavailable.

## Multiplicity and nested-link reconciliation

- MOS-781 occurs once as a hierarchy module entry. Its observed children list has 1 occurrence and 1 unique key: MOS-890; no duplicates.
- Scanning hierarchy child lists for MOS-890 found only the assigned occurrence at `$.results[15].children[0]`; no conflicting module assignment was observed.
- Assigned-member index reconciliation: 1 expected key, 1 matching record; 0 missing keys and 0 duplicate matching records. No extra module-associated record was found through index `parent` fields. Unrelated index entries are outside this inventory, not extras.
- Member index `$.items[90].subtasks` is explicitly `[]`: zero named nested keys in this snapshot. Checking the saved subtask packet found zero records with `parent == "MOS-890"`, zero with `parent == "MOS-781"`, and no record keyed MOS-890 or MOS-781. Thus no observed nested parent links require reconciliation; no missing, duplicate or extra assigned nested keys were found. This is not proof that no hidden or subsequently created subtasks exist.

## Coverage limits and next collection keys

The observed inventory reconciles without a required-file or membership blocker. The hierarchy states that no more/next controls were found, but loaded HTML does not prove completeness against permission-filtered issues. Snapshot timestamps remain distinct; later subtask retrieval does not refresh hierarchy or member metadata. Status is recorded only and establishes neither completion nor visibility.

Next detail collection key: **MOS-890**, for full description, attachment enumeration/content as needed, comments, custom acceptance fields and explicit parent/subtask recheck. **MOS-781** remains a parent-detail coverage gap if parent details are required. There are no named nested keys awaiting collection in these saved packets. No external links or attachment bodies were fetched, and no tests or business requests were run.
