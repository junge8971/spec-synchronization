# MOS-780 — bounded hierarchy inventory

## Scope and sources

Inventory only, under `work-items/JIRA-MOS-780.md` and the superseding `work-items/JIRA-INVENTORY-HANDOFF.md`. Paths below are relative to the audit root; JSON locators are zero-based. No business-semantic or implementation assessment performed.

| Saved source | Retrieval timestamp | Exact locator / use |
| --- | --- | --- |
| `sources/jira-hierarchy/r1/content.json` | `2026-10-16T11:08:08.629Z` | `$.results[14]`: assigned module; `$.retrievedAt`, `$.method`, `$.classification`, `$.pagination`: provenance and caveats |
| `sources/jira-member-index/r1/content.json` | `2026-10-16T11:20:38.570Z` | `$.items[89]`: sole assigned member; `$.retrievedAt` |
| `sources/jira-member-index/r1/metadata.json` | `2026-10-16T11:20:38.570Z` | `$.fields`, `$.limitations`, `$.method`: selected-field collection, not full issue detail |
| `sources/jira-subtasks/r1/content.json` | `2026-10-16T11:23:01.951Z` | `$.items[*].parent` and `$.items[*].key`: structural reconciliation against assigned keys; `$.retrievedAt` |
| `sources/jira-subtasks/r1/metadata.json` | `2026-10-16T11:23:01.951Z` | `$.limitations`: attachments enumerated only, comments/custom acceptance fields not collected |

## Observed module and member

`jira-hierarchy/r1/content.json:$.results[14]` has `key: "MOS-780"`, `type: "Q key result"`, and `children: ["MOS-713"]`. This is not a literal Epic. The saved module entry contains no summary, status, updated timestamp, description, attachments, comments, custom acceptance fields, or `subtasks` field. Its `children` array is present and nonempty.

| Member | Summary | Type | Status | Issue updated | Exact identity and membership locators |
| --- | --- | --- | --- | --- | --- |
| MOS-713 | [B] Подготовить контракты шаблонов отчётов, конструктора, выгрузок и расписания | Development task | Review | `2026-10-09T15:06:30.638+0800` | `sources/jira-hierarchy/r1/content.json:$.results[14].children[0]`; `sources/jira-member-index/r1/content.json:$.items[89]` (`.key`, `.summary`, `.type`, `.status`, `.updated`) |

### Coverage and nesting

At `sources/jira-member-index/r1/content.json:$.items[89]`:
- `subtasks` is explicitly present as `[]`; zero nested keys are advertised in this snapshot.
- `parent` is absent, not an empty object or array. The MOS-780 → MOS-713 link is established by the hierarchy packet, not a member-index parent field.
- `description`, `attachments`, `comments`, and custom acceptance fields are absent. Full-description, attachment, comment, and custom acceptance coverage is unavailable, not empty or proven unnecessary.

Structural reconciliation of actual saved packets:
- MOS-780 occurs once as a hierarchy module, at `$.results[14]`.
- Its one child occurrence is one distinct key: MOS-713. Checking only membership keys across hierarchy entries found MOS-713 only at `$.results[14].children[0]`; no duplicate/cross-module assignment observed.
- MOS-713 occurs exactly once in member-index `$.items[*].key`, at index 89. Missing assigned index keys: none. Duplicate assigned index keys: none.
- MOS-780 has no member-index issue record. The module hierarchy entry is collected; a detailed parent issue object is not evidenced by these packets.
- In subtask `$.items[*]`, parent values are strings. No record has `.parent` equal to MOS-713 or MOS-780, and neither key occurs as a subtask `.key`. Thus no nested records require parent-link validation for this module and no unexpected module-linked nested record is observed. This agrees with the member's explicit empty `subtasks` array, without proving hidden subtasks cannot exist.
- No supplementary-description allowlisted key (MOS-1245/MOS-1306/MOS-1237/MOS-959) belongs to this module. Supplementary descriptions were not inspected. No unrelated module bodies or scenarios were assessed.

## Limitations and next collection

All observed assigned members are accounted for: **1 member, 1 matching index record, 0 advertised nested subtasks, 0 matching saved nested records**. This is a bounded observed inventory, not a completeness or completion claim. `Review` does not establish completion. The hierarchy packet explicitly warns that no more/next controls in loaded HTML does not exclude permission-filtered issues.

The member-index metadata's historical “nested subtask details pending” note does not negate the later saved subtask packet; both retain their own timestamps. Full descriptions remain expected coverage gaps, not blockers.

Next collection keys, if authorized: **MOS-713** for full description, attachments, comments, custom acceptance coverage and refreshed parent/subtask fields; **MOS-780** for a detailed parent issue object and visibility-aware child-list confirmation. No other issue keys are requested by this inventory. No infrastructure or membership-conflict blocker encountered.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "Reconciled the sole assigned member MOS-713 at hierarchy results[14].children[0] and member-index items[89]; checked multiplicity and saved nested parent links."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-780.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command": "Read-only local JSON inspection with Python", "result": "passed", "summary": "Verified packet timestamps, assigned-key occurrences, actual fields and module-linked subtask parent matches."}],
  "validationOutput": ["One distinct assigned child; one index record; explicit subtasks []; no matching nested parent links."],
  "residualRisks": ["Permission-filtered or otherwise hidden issues are not excluded.", "Full member description, attachments, comments and custom acceptance fields are absent; detailed parent issue object is not collected in these packets."],
  "noStagedFiles": true,
  "diffSummary": "Only the bound inventory report was written; no source or status edits performed.",
  "reviewFindings": ["No blockers observed."],
  "manualNotes": "Inventory-only structural inspection; no tests, network, browser, generation, or unrelated business-body analysis. No staging operations performed."
}
```
