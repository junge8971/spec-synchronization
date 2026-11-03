# MOS-652 — bounded saved-packet inventory

## Scope and provenance

Inventory only, following `work-items/JIRA-MOS-652.md` and the superseding `work-items/JIRA-INVENTORY-HANDOFF.md`. Paths below are relative to the audit root; JSON locators use zero-based array indexes. No business semantics, scenario reports, implementation, external links or unrelated issue details were assessed.

| Saved source | Retrieval timestamp | Exact evidence locator |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `2026-10-16T11:08:08.629Z` | `$.results[2]` (MOS-652), `$.retrievedAt`, `$.method`, `$.classification`, `$.pagination` |
| `sources/jira-member-index/r1/content.json` | `2026-10-16T11:20:38.570Z` | `$.items[34:38]` (end exclusive), `$.retrievedAt`, `$.scope` |
| `sources/jira-member-index/r1/metadata.json` | `2026-10-16T11:20:38.570Z` | `$.retrievedAt`, `$.fields`, `$.limitations` |
| `sources/jira-subtasks/r1/content.json` | `2026-10-16T11:23:01.951Z` | `$.items[*].key`, `$.items[*].parent` checked against assigned member keys; `$.retrievedAt`, `$.scope` |
| `sources/jira-subtasks/r1/metadata.json` | `2026-10-16T11:23:01.951Z` | `$.retrievedAt`, `$.format`, `$.limitations` |

MOS-652 is recorded as `Q key result` at `$.results[2].type`, not a literal Epic. This is a hierarchy entry, not a collected full parent issue object. No parent update timestamp or full parent detail is established by that entry. Snapshot timestamps above remain independent. The member-index metadata's pending-subtask note is superseded by the available subtask packet; its missing-full-fields limitation remains applicable.

## Assigned members and multiplicity

All four observed children are accounted for. Hierarchy occurrences and selected-index record multiplicities are each exactly one per key. An exact-key membership cross-check found each assigned key only under MOS-652 in the saved hierarchy. There are no duplicate assigned keys, missing assigned index records, or conflicting saved memberships.

| Member / saved summary | Hierarchy locator | Index locator (and file lines) | Type | Status | Issue updated | Hierarchy / index multiplicity |
| --- | --- | --- | --- | --- | --- | --- |
| MOS-756 — Тестовая задача | `$.results[2].children[0]` | `$.items[34]`, lines 284–291 | System Analytics | Cancel | `2026-10-01T21:22:05.784+0800` | 1 / 1 |
| MOS-670 — [B] Описать модель ролей и каталог разрешений | `$.results[2].children[1]` | `$.items[35]`, lines 292–299 | Development task | Ready for review | `2026-10-09T15:03:51.653+0800` | 1 / 1 |
| MOS-671 — [B] Описать внутренний контракт проверки доступа | `$.results[2].children[2]` | `$.items[36]`, lines 300–307 | Development task | CLOSED | `2026-10-13T14:20:07.145+0800` | 1 / 1 |
| MOS-912 — [B] Расширить ролевую модель в МПММ | `$.results[2].children[3]` | `$.items[37]`, lines 308–315 | Development task | Ready for test | `2026-10-09T15:04:11.205+0800` | 1 / 1 |

Index locators refer to `sources/jira-member-index/r1/content.json`; hierarchy locators refer to `sources/jira-hierarchy/r1/content.json`. Each index record contains `key`, `summary`, `type`, `status`, `updated`, and `subtasks`; none contains a `parent` field. Module membership therefore comes from the hierarchy, not an independently confirmed index parent field. The shared index is not module-labelled: unrelated records are not classified as module extras.

## Nested-parent reconciliation

`$.items[34].subtasks`, `$.items[35].subtasks`, `$.items[36].subtasks`, and `$.items[37].subtasks` in the member index are each explicitly `[]`. The observed nested-key multiset is empty. Exact-key/parent filtering across the saved subtask packet found zero records with a key among these four members or a parent among these four members. Thus there are zero saved nested links to validate, zero missing referenced nested keys, zero relevant duplicate subtask records, and zero additional nested records pointing to an assigned member. No nested parent object is claimed collected.

These are saved-packet observations only, not proof that subtasks do not exist or that all issues were visible.

## Per-member detail coverage

| Member | Selected index | Full description | Attachments | Comments | Custom acceptance fields | Nested evidence |
| --- | --- | --- | --- | --- | --- | --- |
| MOS-756 | Present once | Not collected | Not collected | Not collected | Not collected | Saved `subtasks: []`; no matching subtask record |
| MOS-670 | Present once | Not collected | Not collected | Not collected | Not collected | Saved `subtasks: []`; no matching subtask record |
| MOS-671 | Present once | Not collected | Not collected | Not collected | Not collected | Saved `subtasks: []`; no matching subtask record |
| MOS-912 | Present once | Not collected | Not collected | Not collected | Not collected | Saved `subtasks: []`; no matching subtask record |

Missing fields are expected collection gaps, not evidence of empty Jira content and not blockers. None of MOS-1245/MOS-1306/MOS-1237/MOS-959 belongs to this observed module, so the supplementary API-delta packet was not inspected. The subtask packet's attachment metadata capability does not establish attachment coverage for these members.

## Limitations and next collection

The hierarchy reports no more/next controls in child panels, but explicitly disclaims completeness against hidden permission-filtered issues. Status values (including Cancel and CLOSED), empty arrays, and later packet timestamps do not establish completion or full visibility. The selected fields cannot establish full descriptions, attachment presence/content, comments or custom acceptance coverage.

Next collection keys for those missing fields and a fresh nested-list check: **MOS-756, MOS-670, MOS-671, MOS-912**. Collect **MOS-652** separately if a full module-parent issue object is required. Any newly observed subtasks require explicit saved key/parent reconciliation; none is presently identified for this module.

Manual validation: read local required instructions and packets; parsed JSON to reconcile exact assigned keys, record counts, selected fields, hierarchy occurrences and relevant nested parents. No network, tests, browser, generation, source edits or status edits were performed. Only this bound report was written.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "Four observed members reconciled once each with exact snapshot locators and timestamps; nested-link and per-member coverage gaps recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-652.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command": "Read-only local Python JSON inspection and exact-key/parent reconciliation", "result": "passed", "summary": "4/4 index matches; multiplicity one each; zero relevant nested records."}],
  "validationOutput": ["No assigned membership conflict or missing required packet found."],
  "residualRisks": ["Descriptions, attachments, comments and custom acceptance fields are not collected for all four members.", "Saved empty subtask arrays and hierarchy visibility cannot prove completeness or completion."],
  "noStagedFiles": true,
  "diffSummary": "Bound inventory report only; no source or status edits.",
  "reviewFindings": ["No inventory blockers found."],
  "manualNotes": "Inventory-only local inspection; no tests or external collection performed. No staging operations performed."
}
```
