# MOS-783 — saved-packet inventory

Inventory only; no scenario, requirements or implementation assessment. All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`. JSON locators use zero-based array indices.

## Files retrieved / provenance

- `work-items/JIRA-MOS-783.md` (lines 1–9) and `work-items/JIRA-INVENTORY-HANDOFF.md` (lines 1–21): assignment and superseding input availability; absent descriptions are coverage gaps, not blockers.
- `sources/jira-hierarchy/r1/content.json` (lines 2–6, 25; `$.results[17]`): MOS-783 is a **Q key result**, with 18 observed children. Retrieved `2026-10-16T11:08:08.629Z` by parent-browser same-origin browse GET and DOM child-panel extraction. `sources/jira-hierarchy/r1/metadata.json` records revision 1 and SHA-256 `4d1881959ecbe13e4c2d4c27903b63a4ba71e1cba38e349dc33855a7e605fb77`. Saved parentEvidence reference: `../../jira-MOS-623/r1/content.md` (not independently assessed).
- `sources/jira-member-index/r1/content.json` (`$.items[116:134]`, lines 989–1158), and `sources/jira-member-index/r1/metadata.json`: retrieved `2026-10-16T11:20:38.570Z`, revision 1; parent-browser exact-allowlist same-origin REST GET, selected fields extracted from parent transcript. SHA-256 `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043`.
- `sources/jira-subtasks/r1/content.json` (`$.items[10:15]`, lines 209–310), and `sources/jira-subtasks/r1/metadata.json`: retrieved `2026-10-16T11:23:01.951Z`, revision 1; parent-browser same-origin issue GET, selected-field redacted extraction. SHA-256 `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e`. Packet-level example credential redacted before persistence; no examples executed.
- `sources/jira-api-delta-scenarios/r1/content.json` (`$.items[2]`, lines 42–59; `$.items[3]`, lines 60–69), and `sources/jira-api-delta-scenarios/r1/metadata.json`: retrieved `2026-10-16T11:23:51.742Z`; parent-browser same-origin issue GET, selected-field extraction. SHA-256 `b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed`. Only assigned MOS-1237/MOS-959 records inventoried.

Hashes above are recorded metadata, not independently recomputed.

## Reconciliation

18 distinct hierarchy children; all 18 appear exactly once in the member index. No assigned-member duplicate, missing record, or cross-module membership overlap found in saved hierarchy. MOS-783 itself has a hierarchy entry, **not a collected member-index issue object**. Direct module membership comes from the hierarchy child panel, not a member `parent` field.

Only MOS-709 lists subtasks: five unique references, each present exactly once in the subtask packet and each explicitly pointing back to MOS-709. No extra subtask records with a parent among these 18 members and no alternative member-index parent references for these five keys. All five saved detail records have `subtasks: []`; other 17 member records also have `subtasks: []`. These are observed empty arrays, not proof against hidden issues.

## Per-member inventory

Every row has index presence = yes and type = `Development task`. Locator `I[n]` means `sources/jira-member-index/r1/content.json#$.items[n]`; every key is also in `sources/jira-hierarchy/r1/content.json#$.results[17].children` in the order shown.

Coverage **G**: description, attachments, comments and custom acceptance fields absent from index and no assigned supplementary description record. **D2/D3**: description and attachment metadata collected in delta `$.items[2]/[3]`, respectively; comments/custom acceptance fields still absent. No attachment bodies collected.

| Member | Index locator | Observed status | Index updated (verbatim) | Subtasks | Coverage |
|---|---|---|---|---|---|
| MOS-707 | I[116] | CLOSED | 2026-09-24T17:18:32.529+0800 | 0 | G |
| MOS-708 | I[117] | CLOSED | 2026-10-09T15:05:07.714+0800 | 0 | G |
| MOS-709 | I[118] | Require improvement | 2026-10-09T15:05:22.838+0800 | 5 | G |
| MOS-712 | I[119] | Review | 2026-10-09T15:06:54.796+0800 | 0 | G |
| MOS-901 | I[120] | Require improvement | 2026-10-16T19:20:13.190+0800 | 0 | G |
| MOS-910 | I[121] | Testing | 2026-10-09T15:04:29.281+0800 | 0 | G |
| MOS-911 | I[122] | Ready for test | 2026-10-09T15:04:32.758+0800 | 0 | G |
| MOS-913 | I[123] | Ready for test | 2026-10-09T15:04:13.786+0800 | 0 | G |
| MOS-914 | I[124] | Ready for test | 2026-10-14T20:38:47.150+0800 | 0 | G |
| MOS-958 | I[125] | Hold | 2026-10-14T20:44:01.006+0800 | 0 | G |
| MOS-959 | I[126] | Backlog | 2026-10-16T19:20:11.528+0800 | 0 | D3 |
| MOS-976 | I[127] | Ready for test | 2026-10-09T15:08:10.713+0800 | 0 | G |
| MOS-1130 | I[128] | Backlog | 2026-10-16T19:20:15.049+0800 | 0 | G |
| MOS-1178 | I[129] | Review | 2026-10-16T15:00:48.479+0800 | 0 | G |
| MOS-1237 | I[130] | Ready for test | 2026-10-16T15:31:51.977+0800 | 0 | D2 |
| MOS-1308 | I[131] | Review | 2026-10-16T17:28:19.004+0800 | 0 | G |
| MOS-1336 | I[132] | Ready for test | 2026-10-15T20:50:28.715+0800 | 0 | G |
| MOS-1407 | I[133] | Development | 2026-10-16T17:33:09.299+0800 | 0 | G |

Delta supplement: `sources/jira-api-delta-scenarios/r1/content.json#$.items[2]` retains MOS-1237 type/status, but updated = `2026-10-16T19:22:44.086+0800` (does not replace index timestamp). Nonempty description and one attachment metadata entry (`attachments[0]`: ID 839665, `mos-1237-test-plan.md`, text/markdown, 19543 bytes); `subtasks: []`. `$.items[3]` retains MOS-959 type/status and updated = `2026-10-16T19:20:11.528+0800`; nonempty description, `attachments: []`, `subtasks: []`. Empty attachments here is an observed array, unlike absent attachment coverage in G rows.

## Nested subtasks

Each has type `Dev-bug (sub-task)`, status `Backlog` (also matches its member-index reference), parent `MOS-709`, nonempty saved description, attachment metadata, and no comments/custom acceptance fields. `S[n]` means `sources/jira-subtasks/r1/content.json#$.items[n]`. Reference locators below are within `sources/jira-member-index/r1/content.json#$.items[118]`.

| Key | Reference → detail locator | Detail updated (verbatim) | Attachment metadata IDs / filenames |
|---|---|---|---|
| MOS-1110 | `.subtasks[0]` → S[10] | 2026-10-09T15:06:06.973+0800 | 829292 / 2909.png |
| MOS-1164 | `.subtasks[1]` → S[11] | 2026-10-09T15:06:35.325+0800 | 832277 / 1.png |
| MOS-1165 | `.subtasks[2]` → S[12] | 2026-10-09T15:06:55.903+0800 | 832288 / 2.png |
| MOS-1166 | `.subtasks[3]` → S[13] | 2026-10-09T15:07:28.233+0800 | 832305 / 3.png |
| MOS-1167 | `.subtasks[4]` → S[14] | 2026-10-09T15:08:08.485+0800 | 832324 / 4.png; 832323 / 5.png |

Parent proof is each S record's `.parent`; attachment locators are `.attachments[0]`, plus S[14]`.attachments[1]`. Six attachment metadata entries, no downloaded bodies.

## Collection gaps / next keys

- Description and attachment-field collection remains for the 16 G keys: MOS-707, MOS-708, MOS-709, MOS-712, MOS-901, MOS-910, MOS-911, MOS-913, MOS-914, MOS-958, MOS-976, MOS-1130, MOS-1178, MOS-1308, MOS-1336, MOS-1407. Index presence does not establish full issue-detail coverage.
- Comments/custom acceptance coverage remains absent for all 18 members and five nested keys. Description prose is not treated as custom acceptance-field collection.
- Attachment bodies remain uncollected for MOS-1237 and MOS-1110/MOS-1164/MOS-1165/MOS-1166/MOS-1167; identifiers above support any separately authorized collection. MOS-959 has an observed empty attachment list at its delta snapshot.
- MOS-783 parent issue details are not represented by an index record; hierarchy identity/type alone must not be described as a collected full parent object.
- No missing required packets or conflicting observed membership found. Hierarchy metadata reports no more/next controls, but loaded HTML cannot establish completeness against permission-filtered/hidden issues. Snapshot times differ; statuses imply neither implementation completion nor acceptance.

Manual validation: read-only local JSON inspection checked exact key multiplicity, hierarchy overlap, forward subtask references and reverse parent links. No network, browser, tests, generation, source/status edits or business-content analysis performed. Only this bound report was written.
