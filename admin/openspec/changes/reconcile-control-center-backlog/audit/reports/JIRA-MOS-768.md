# MOS-768 — observed hierarchy inventory

## Scope and evidence

Inventory only, governed by `work-items/JIRA-MOS-768.md` and mandatory `work-items/JIRA-INVENTORY-HANDOFF.md`; the latter supersedes the pending-detail dependency. All paths below are relative to the audit root. Locators use zero-based JSON Pointers.

| Saved packet | Collection timestamp (`/retrievedAt`) | Relevant locators |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `2026-10-16T11:08:08.629Z` | `/results/3`, `/method`, `/classification`, `/pagination`, `/parentEvidence` |
| `sources/jira-member-index/r1/content.json` | `2026-10-16T11:20:38.570Z` | `/items/38`–`/items/41`, `/scope` |
| `sources/jira-member-index/r1/metadata.json` | `2026-10-16T11:20:38.570Z` | `/fields`, `/limitations`, `/method` |
| `sources/jira-subtasks/r1/content.json` | `2026-10-16T11:23:01.951Z` | `/items` (checked keys and string-valued `parent` fields for assigned-key matches), `/scope` |
| `sources/jira-subtasks/r1/metadata.json` | `2026-10-16T11:23:01.951Z` | `/limitations`, `/method`, `/redactions` |

MOS-768 appears once as a module entry, at hierarchy `/results/3`; observed type is **Q key result**, not literal Epic. Its four observed children are enumerated below. No MOS-768 issue object appears in either selected issue packet; its status, updated time and full issue fields are not established by this inventory. The hierarchy's `/parentEvidence` is a reference, not an independently inspected parent issue object here.

## Member reconciliation

`H` = hierarchy content; `I` = member-index content, at the paths above. Each row has one hierarchy occurrence and one index record; exact identity/status/update fields are under the listed index pointer (`/key`, `/summary`, `/type`, `/status`, `/updated`).

| Member | Observed summary | Type | Status | Issue updated time | Exact membership / index locators |
| --- | --- | --- | --- | --- | --- |
| MOS-836 | [B] Реализовать модуль "Команды" | Development task | Ready for test | `2026-10-09T15:07:10.322+0800` | H `/results/3/children/0`; I `/items/38` |
| MOS-931 | [B] Реализовать получение списка пользователей ЦАМ | Development task | Ready for test | `2026-10-09T15:05:35.272+0800` | H `/results/3/children/1`; I `/items/39` |
| MOS-1032 | [FE][Команды] Создать список и обзор команд | Development task | Backlog | `2026-10-09T15:05:45.747+0800` | H `/results/3/children/2`; I `/items/40` |
| MOS-1033 | [FE][Команды] Создать команду и управлять её составом | Development task | Backlog | `2026-10-09T15:05:23.793+0800` | H `/results/3/children/3`; I `/items/41` |

MOS-931's saved summary has a trailing space, omitted only in the display above.

- Observed membership: **4 occurrences, 4 distinct keys**. Selected index reconciliation: **4 records, 4 distinct assigned keys**, no missing or duplicate assigned records.
- Exact assigned-key occurrence checks across hierarchy child arrays found each only at its listed MOS-768 locator: no conflicting module membership observed.
- None of the four index objects contains a `parent` field. Module membership is supported by hierarchy child locators, not an independently collected issue-parent relationship.
- No additional assigned-linked keys were found in the subtask packet. Unrelated index/subtask records are outside this module inventory and are not treated as extras.

## Nested links and per-member field coverage

| Member | Saved nested observation | Subtask-packet reconciliation | Full-field coverage |
| --- | --- | --- | --- |
| MOS-836 | I `/items/38/subtasks` = `[]` | No record with `parent = "MOS-836"`; no self-key record | Index present; description, attachments, comments and custom acceptance fields absent |
| MOS-931 | I `/items/39/subtasks` = `[]` | No record with `parent = "MOS-931"`; no self-key record | Index present; description, attachments, comments and custom acceptance fields absent |
| MOS-1032 | I `/items/40/subtasks` = `[]` | No record with `parent = "MOS-1032"`; no self-key record | Index present; description, attachments, comments and custom acceptance fields absent |
| MOS-1033 | I `/items/41/subtasks` = `[]` | No record with `parent = "MOS-1033"`; no self-key record | Index present; description, attachments, comments and custom acceptance fields absent |

The saved subtask `/items` array also contains no `parent = "MOS-768"` link. Observed nested count for this module is **0**; there are no observed nested keys awaiting record matching and no observed nested parent conflicts. Empty arrays and absent matching records do **not** establish that Jira has no further subtasks or permission-hidden issues.

The supplemental-description allowlist (MOS-1245/MOS-1306/MOS-1237/MOS-959) has no intersection with these members; the delta/scenario packet was not inspected. No unrelated wiki/task packets, scenario reports, business semantics or implementation were examined.

## Limitations and next collection

- Hierarchy evidence is saved parent-browser HTML extraction. Its `/pagination` states that no more/next controls were found, but loaded HTML is not proof against hidden permission-filtered issues.
- The member-index metadata explicitly limits collection to selected identity/status/update/subtask/parent fields; actual assigned records omit `parent`. Missing full descriptions are expected coverage gaps, not blockers.
- Subtask metadata reports enumerated rather than downloaded attachments and excludes comments/custom acceptance fields; there are no matching subtask records here to extend member coverage.
- Preserve the three snapshot timestamps separately. Issue update times are not collection times; statuses do not prove completion or full visibility.
- Next collection keys, if separately authorized: **MOS-836, MOS-931, MOS-1032, MOS-1033** for descriptions, attachment metadata/content as required, comments, custom acceptance fields and refreshed nested visibility; **MOS-768** for its own issue object and authoritative membership/visibility confirmation. Collect any newly observed nested keys only after explicit discovery. No such collection was performed.

## Validation

Read-only local JSON inspection reconciled every assigned key and its occurrence count, selected-field coverage and nested parent matches. No missing required packets, membership conflicts or infrastructure failures were encountered. Only this bound report was written; no source/status edits, network, browser, tests, generation or agents were used.

```acceptance-report
{
  "criteriaSatisfied": [
    {
      "id": "criterion-1",
      "status": "satisfied",
      "evidence": "Four distinct observed MOS-768 members reconciled one-to-one with saved index records; exact pointers, collection/update timestamps, nested-link checks and coverage limitations recorded."
    }
  ],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-768.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {
      "command": "Read-only local Python JSON inspection of hierarchy, member-index and subtasks packets and metadata",
      "result": "passed",
      "summary": "4 hierarchy occurrences / 4 unique members / 4 index records; no duplicate or conflicting assigned membership; 0 matching nested parent links."
    }
  ],
  "validationOutput": ["All assigned observed members accounted for; no required packet missing."],
  "residualRisks": ["Saved visibility is not proven exhaustive; full descriptions, attachments, comments and custom acceptance fields are not collected for the four members; module parent issue object is absent from inspected selected issue packets."],
  "noStagedFiles": true,
  "diffSummary": "Bound MOS-768 inventory report only; no source or status edits.",
  "reviewFindings": ["No inventory blockers observed."],
  "manualNotes": "Inspection only; no tests or external collection performed. No staging operations performed; repository staging state was not inspected."
}
```
