# MOS-771 — saved-packet inventory

Scope: assigned module only; inventory, not semantic or implementation assessment. Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`. Supplemental `work-items/JIRA-INVENTORY-HANDOFF.md` supersedes the original pending-detail dependency: missing full member details are coverage gaps, not blockers.

## Sources and provenance

- `sources/jira-hierarchy/r1/content.json`, `/results/6` (line 14): MOS-771, type `Q key result`, children `["MOS-816"]`. Retrieved `2026-10-16T11:08:08.629Z`; parent-browser same-origin GET `/browse/<key>`, DOMParser selectors `#type-val` and `#jpo-child-issues-web-panel a[href*="/browse/MOS-"]`. Saved `parentEvidence` is `../../jira-MOS-623/r1/content.md` (provenance reference, not independently inspected). No more/next controls observed; loaded HTML does not prove absence of permission-filtered issues.
- `sources/jira-member-index/r1/content.json`, `/items/44` (lines 364–374 onward), with `metadata.json`: retrieved `2026-10-16T11:20:38.570Z`; parent-browser read-only same-origin Jira REST GET for exact hierarchy member allowlist, extracted from parent transcript. SHA-256 recorded in metadata: `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043`. Selected identity/status/update/subtask fields only.
- `sources/jira-subtasks/r1/content.json`, `/items/1` (lines 25–50), with `metadata.json`: retrieved `2026-10-16T11:23:01.951Z`; parent-browser same-origin Jira issue GET for 16 observed subtasks, selected-field redacted extraction from parent session. Metadata SHA-256: `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e`. Attachment metadata only; no comments/custom acceptance fields. Example bearer value redacted before persistence; no example executed.
- `sources/jira-api-delta-scenarios/r1/content.json`, `/items`: no assigned member match. Retrieved `2026-10-16T11:23:51.742Z`; supplementary four-key packet is inapplicable here and does not replace older snapshots.

## Per-member inventory

| Key / saved relationship | Observed summary | Type | Status (not completion evidence) | Exact issue updated timestamp | Coverage / locator |
|---|---|---|---|---|---|
| MOS-816 — direct member of MOS-771 | [B] Реализовать модуль управления состоянием модулей платформы | Development task | Ready for retest | `2026-10-14T15:09:34.720+0800` | Index present once: member-index `/items/44`; hierarchy `/results/6/children/0`. Description, attachments, comments and custom acceptance fields not collected. Index has no `parent` field; module relationship comes from hierarchy. |
| MOS-1150 — nested subtask of MOS-816 | data.items возвращает данные только по одному модулю при запросе реестра модулей | Dev-bug (sub-task) | Ready for test | `2026-10-09T15:06:03.028+0800` | Reference once at member-index `/items/44/subtasks/0`; detail once at subtasks `/items/1`, explicit `/parent` = `MOS-816`. Description present with saved redaction; two attachment metadata records; comments/custom acceptance fields absent. |

## Multiplicities and parent reconciliation

- Assigned direct member array: 1 occurrence, 1 unique key (MOS-816); index matches: 1. No missing direct index keys or duplicate assigned member records.
- Observed nested array: 1 occurrence, 1 unique key (MOS-1150). Across saved index references MOS-1150 occurs only at `/items/44/subtasks/0`; detail key occurs once in subtask packet. Reference and detail status agree. Explicit detail parent matches MOS-816.
- Reverse scan of saved subtask records finds exactly MOS-1150 with parent MOS-816; no extra detail records under this assigned member, and no detail records with parent MOS-771. No missing observed subtask detail keys or conflicting parent links.
- MOS-1150 `/subtasks` is saved as `[]`: zero further observed descendants, not proof against hidden/uncollected issues.
- MOS-771 has a hierarchy entry, not a full collected issue object in the selected detail packets. Parent status/update/description coverage must not be inferred.

## Attachments and next collection keys

MOS-1150 attachment metadata at `sources/jira-subtasks/r1/content.json`:

- `/items/1/attachments/0` (lines 35–41): ID `831194`, `response_1790844958023 (1).json`, `application/json`, 1038 bytes; saved locator `https://task.mos-team.ru/secure/attachment/831194/response_1790844958023+%281%29.json`.
- `/items/1/attachments/1` (lines 42–48): ID `831195`, `Screenshot_4.png`, `image/png`, 40788 bytes; saved locator `https://task.mos-team.ru/secure/attachment/831195/Screenshot_4.png`.

Missing collection keys:

1. **MOS-816:** full description, attachment enumeration/bodies, comments and custom acceptance fields; refresh nested enumeration only through authorized future collection.
2. **MOS-1150:** attachment bodies `831194`, `831195`, comments and custom acceptance fields. Description already available as redacted saved content, not an unredacted original.
3. **MOS-771:** parent issue details if parent-level coverage is required; currently hierarchy identity/type/membership only.

No required packet missing; no membership conflict observed. Missing full details are expected coverage gaps. No business semantics, external links, wiki bodies or implementation analyzed; no network/browser/tests performed. Snapshot retrieval times and issue update times remain distinct; statuses and empty arrays do not establish completion or exhaustive Jira coverage.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Reconciled one direct member and one nested subtask, exact locators, multiplicities, parent link, timestamps and missing collection keys."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-771.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read-only Python JSON inspection of saved packets","result":"passed","summary":"MOS-816 index count 1; MOS-1150 reference/detail counts 1 each; parent MOS-816 matches."}],
  "validationOutput": ["No missing observed member/subtask keys, duplicate assigned records or conflicting parent links."],
  "residualRisks": ["MOS-816 full detail coverage absent; MOS-1150 attachment bodies/comments/custom acceptance fields absent; hidden or permission-filtered issues cannot be excluded."],
  "noStagedFiles": true,
  "diffSummary": "Only the bound inventory report was written; no source or status edits.",
  "reviewFindings": ["No inventory blockers observed."],
  "manualNotes": "Inventory only from saved snapshots; no tests, browser, network or example commands executed. No staging operations performed."
}
```
