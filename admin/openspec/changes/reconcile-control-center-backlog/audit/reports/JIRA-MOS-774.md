# MOS-774 — saved hierarchy inventory

## Scope and provenance
Inventory only; no scenario, requirement, implementation or status-completion assessment. Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`; JSON array locators are zero-based.

- Instructions: `work-items/JIRA-MOS-774.md` and superseding availability note `work-items/JIRA-INVENTORY-HANDOFF.md`.
- **H** = `sources/jira-hierarchy/r1/content.json`, `$.results[9]`: MOS-774, type `Q key result`, 18 children. Retrieved **2026-10-16T11:08:08.629Z** via parent-browser same-origin browse HTML/DOM child-panel extraction. Recorded parent evidence reference: `../../jira-MOS-623/r1/content.md` (not inspected or treated as a collected parent issue object).
- **M** = `sources/jira-member-index/r1/content.json`, `$.items[56:74]` (indices 56–73 inclusive); retrieved **2026-10-16T11:20:38.570Z**. `sources/jira-member-index/r1/metadata.json` records revision 1, parent-browser same-origin REST exact hierarchy allowlist extraction, selected summary/type/status/subtasks/parent/updated fields; SHA-256 `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` (recorded, not independently recomputed).
- **S** = `sources/jira-subtasks/r1/content.json`, `$.items[7:10]` (indices 7–9 inclusive); retrieved **2026-10-16T11:23:01.951Z**. `sources/jira-subtasks/r1/metadata.json` records revision 1, selected-field-redacted parent-browser same-origin REST extraction; SHA-256 `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` (recorded, not independently recomputed). Attachments enumerated, not downloaded; packet-wide example credential redaction noted.

## Reconciliation
All 18 H children occur exactly once in M. No duplicate child keys, missing indexed members or cross-module duplicate assignment for these keys. Exactly three nested keys are referenced, each once and by the expected member; all three have exactly one S record and matching parent. S has no additional records parented to this member set. Unrelated packet records are outside scope, not extras. MOS-774 itself has no issue object in M or S: H supplies module identity/type and observed child-panel membership, not a full parent issue. M member records do not expose parent fields, so direct membership rests on H, not an independently collected REST parent relationship.

Supplementary API-delta descriptions are limited by the handoff to MOS-1245/MOS-1306/MOS-1237/MOS-959; none belongs to this module, so that packet is not applicable and was not inspected.

## Per-member inventory
Every row has index presence **yes**, observed type **Development task**, and coverage **I**: summary/type/status/updated/subtasks only; full description, attachments, comments and custom acceptance fields **not collected in M**. This is a collection gap, not evidence those fields are empty. `[]` means the saved subtasks array is empty, not proof against hidden issues. H child position follows row order (0–17).

| Member | Exact M locator | Observed status | Issue updated (verbatim) | Observed nested keys | Coverage |
|---|---|---|---|---|---|
| MOS-675 | `$.items[56]` | CLOSED | 2026-09-22T21:54:23.623+0800 | [] | I |
| MOS-676 | `$.items[57]` | Require improvement | 2026-10-09T15:04:19.424+0800 | MOS-1050, MOS-1051 | I |
| MOS-677 | `$.items[58]` | Require improvement | 2026-10-09T15:04:14.473+0800 | MOS-1052 | I |
| MOS-701 | `$.items[59]` | Review | 2026-10-09T15:07:29.990+0800 | [] | I |
| MOS-944 | `$.items[60]` | Ready for test | 2026-10-16T19:20:14.349+0800 | [] | I |
| MOS-945 | `$.items[61]` | Ready for test | 2026-10-09T15:05:32.196+0800 | [] | I |
| MOS-1018 | `$.items[62]` | Backlog | 2026-10-16T19:20:13.428+0800 | [] | I |
| MOS-1019 | `$.items[63]` | Ready for test | 2026-10-09T15:04:22.458+0800 | [] | I |
| MOS-1020 | `$.items[64]` | Ready for test | 2026-10-09T15:04:25.679+0800 | [] | I |
| MOS-1021 | `$.items[65]` | Ready for test | 2026-10-09T15:04:32.582+0800 | [] | I |
| MOS-1022 | `$.items[66]` | Ready for test | 2026-10-09T15:04:53.104+0800 | [] | I |
| MOS-1023 | `$.items[67]` | Backlog | 2026-10-16T19:20:12.745+0800 | [] | I |
| MOS-1025 | `$.items[68]` | Backlog | 2026-10-16T19:20:14.618+0800 | [] | I |
| MOS-1026 | `$.items[69]` | Backlog | 2026-10-16T19:20:13.648+0800 | [] | I |
| MOS-1027 | `$.items[70]` | Ready for test | 2026-10-13T19:04:55.072+0800 | [] | I |
| MOS-1030 | `$.items[71]` | Hold | 2026-10-09T15:05:17.041+0800 | [] | I |
| MOS-1031 | `$.items[72]` | Backlog | 2026-10-16T19:20:12.957+0800 | [] | I |
| MOS-1409 | `$.items[73]` | Development | 2026-10-16T17:33:09.886+0800 | [] | I |

## Nested subtask verification
All three have observed type **Dev-bug (sub-task)**, status **Backlog**, nonempty saved `description`, and `subtasks: []`. Comments/custom acceptance fields are absent from this packet. Index-reference statuses also match S.

| Subtask | Exact reference → detail locator | Saved parent | Issue updated (verbatim) | Attachment coverage |
|---|---|---|---|---|
| MOS-1050 | M `$.items[57].subtasks[0]` → S `$.items[7]` | MOS-676 (match) | 2026-10-09T15:08:56.135+0800 | `$.items[7].attachments[0:2]`: metadata IDs 826531, 826530; binaries not collected |
| MOS-1051 | M `$.items[57].subtasks[1]` → S `$.items[8]` | MOS-676 (match) | 2026-10-09T15:03:34.094+0800 | `$.items[8].attachments[0]`: metadata ID 826544; binary not collected |
| MOS-1052 | M `$.items[58].subtasks[0]` → S `$.items[9]` | MOS-677 (match) | 2026-10-09T15:04:29.040+0800 | `$.items[9].attachments`: explicitly [] |

## Collection gaps / next collection keys
- All 18 member keys listed above: collect full issue descriptions, attachment enumeration, comments/custom acceptance coverage if required by the next collection stage. Existing index presence is not full-detail coverage.
- MOS-1050/MOS-1051/MOS-1052: descriptions are saved; comments/custom acceptance coverage remains absent. MOS-1050 and MOS-1051 have three attachment metadata entries total, not downloaded evidence. No deeper nested keys are observed.
- MOS-774: module issue details/status/update time remain uncollected in the inspected packets; do not infer a full parent object from H.
- H reports no more/next controls but explicitly warns loaded HTML does not establish completeness against permission-filtered issues. Snapshot times remain separate; issue update times are not collection times. M metadata's older “nested subtask details pending” note is superseded for these three observed keys by S, without replacing M provenance.

No required input failure or membership conflict found. No network, browser, tests, generation, source/status edits or semantic analysis performed; only this bound report was written.
