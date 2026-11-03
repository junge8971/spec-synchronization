# MOS-651 — saved Jira inventory

## Scope and provenance

Inventory only; governed by `work-items/JIRA-MOS-651.md` and the supplemental `work-items/JIRA-INVENTORY-HANDOFF.md`. Paths below are relative to the audit root; JSON locators use zero-based indices.

- `sources/jira-hierarchy/r1/content.json#/results/1`: one MOS-651 module entry, type `Q key result`, five observed children. Retrieved `2026-10-16T11:08:08.629Z` using parent-browser same-origin GET `/browse/<key>`, DOMParser, `#type-val` and `#jpo-child-issues-web-panel a[href*="/browse/MOS-"]`. Saved parent-evidence reference: `../../jira-MOS-623/r1/content.md` (not independently inspected).
- `sources/jira-member-index/r1/content.json#/items` and `sources/jira-member-index/r1/metadata.json`: retrieved `2026-10-16T11:20:38.570Z`; parent-browser read-only same-origin Jira REST GET for exact hierarchy member allowlist, JSON extracted from parent transcript. Selected fields only. Metadata SHA-256: `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043`.
- `sources/jira-subtasks/r1/content.json#/items` and `sources/jira-subtasks/r1/metadata.json`: retrieved `2026-10-16T11:23:01.951Z`; selected-field, redacted parent-session extraction of same-origin Jira GET results for 16 explicitly observed subtasks. Metadata SHA-256: `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e`. Attachment metadata only, not downloaded; no comments/custom acceptance fields.

## Per-member inventory

`H` = `sources/jira-hierarchy/r1/content.json`; `I` = `sources/jira-member-index/r1/content.json`. All five records have type `Development task`. Multiplicity is hierarchy occurrences / index records. For **each** row, index presence is confirmed but full description, attachments, comments and custom acceptance fields are **not collected**, not confirmed empty. Each index record has `subtasks: []` and no `parent` field; membership comes from H, not an independently collected child-parent field.

| Member | Saved summary | Status | Updated (verbatim) | Exact locators | Multiplicity | Nested evidence |
|---|---|---|---|---|---|---|
| MOS-927 | [FE][Авторизация и моки] Подключить MPMM-сессию и доступность UI по permissions | Ready for test | 2026-10-12T20:34:21.131+0800 | H#/results/1/children/0; I#/items/29 | 1 / 1 | Empty index subtasks; 0 saved subtask parent matches |
| MOS-1009 | [B] Реализовать API проверки разрешения в МПММ | Ready for test | 2026-10-09T15:03:27.160+0800 | H#/results/1/children/1; I#/items/30 | 1 / 1 | Empty index subtasks; 0 saved subtask parent matches |
| MOS-1024 | [B] Использование API проверки разрешений и профиля МПММ в ЦАМ | Testing | 2026-10-16T14:17:13.637+0800 | H#/results/1/children/2; I#/items/31 | 1 / 1 | Empty index subtasks; 0 saved subtask parent matches |
| MOS-1029 | [B] Реализовать API получения профиля в МПММ | CLOSED | 2026-10-15T15:11:14.790+0800 | H#/results/1/children/3; I#/items/32 | 1 / 1 | Empty index subtasks; 0 saved subtask parent matches |
| MOS-1034 | [B] Реализовать API получения информации о текущем пользователе в ЦАМ | Ready for test | 2026-10-09T15:05:31.528+0800 | H#/results/1/children/4; I#/items/33 | 1 / 1 | Empty index subtasks; 0 saved subtask parent matches |

## Reconciliation and collection gaps

- Observed assigned set: **5 occurrences, 5 unique members, 5 matching index records**. Missing index keys: none. Duplicate assigned hierarchy/index keys: none. No extra in-scope records or conflicting membership observed.
- Checked `sources/jira-subtasks/r1/content.json#/items/0` through `#/items/15` by `parent`: no record names any assigned member as parent. Expected nested keys from the five index arrays: none; matched nested records: zero; missing, extra or conflicting observed nested links: none. This does not establish that hidden subtasks do not exist.
- The supplemental description allowlist (MOS-1245, MOS-1306, MOS-1237, MOS-959) has no overlap with this module; no supplementary description coverage applies.
- **Next collection keys:** MOS-927, MOS-1009, MOS-1024, MOS-1029, MOS-1034 — full descriptions, attachment metadata/content coverage, comments and custom acceptance fields, plus refreshed nested-subtask visibility if completeness is required. No specific missing nested key is known.
- **Module parent gap:** MOS-651 is represented only by the hierarchy entry in inspected evidence, with zero member-index records. Its full issue object, status, update time and detail fields are not established; collect MOS-651 separately if parent details are required.
- The hierarchy reports no more/next controls in loaded child panels, but loaded HTML and saved empty arrays do not rule out hidden or permission-filtered issues. Snapshot timestamps remain separate; statuses (including CLOSED) are not completion evidence. Missing details are expected coverage gaps, not blockers. No scenario, business-requirement or implementation assessment was performed.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "All five assigned members reconciled one-to-one; nested parent references checked; collection gaps and exact snapshot locators recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-651.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command": "Read-only local Python JSON inspection and multiplicity/parent-match counts", "result": "passed", "summary": "One module entry, five unique members, one index record each, zero nested parent matches."}],
  "validationOutput": ["Missing assigned index keys: none; duplicate assigned records: none; observed missing nested keys: none."],
  "residualRisks": ["Full member details and module parent issue object are not collected in inspected packets.", "Saved empty arrays and loaded hierarchy cannot exclude hidden issues; statuses do not prove completion."],
  "noStagedFiles": true,
  "diffSummary": "Only the assigned inventory report was written; no source or status edits.",
  "reviewFindings": ["No inventory blockers observed."],
  "manualNotes": "Local saved-packet inventory only; no network, browser, tests, generation, implementation analysis or external-link traversal. Hashes are preserved metadata values, not recomputed checksums. No staging operations performed."
}
```
