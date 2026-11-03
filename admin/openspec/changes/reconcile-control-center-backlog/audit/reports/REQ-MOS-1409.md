# REQ-MOS-1409 — saved requirement lane

## Result and authority
MOS-1409 explicitly requests backend list/card CSV POST exports. It does **not** explicitly assign frontend entrypoints or UI delivery. Implementation, API presence, specification coverage and deployment are unknown in this lane, not missing or accepted. No new change is proposed.

HEAD verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches contract).
Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.
Primary evidence: `sources/jira-details-MOS-774/r1/content.json#/items/18`, key MOS-1409, summary `[B] CSV-экспорт списка навыков`, type Development task, status Development, updated `2026-10-16T19:23:49.394+0800`. This is saved status, not delivery evidence. Saved subtasks and attachments arrays are empty.

Metadata: `sources/jira-details-MOS-774/r1/metadata.json`, retrieved `2026-10-16T11:49:06.782Z`; selected description/identity/status/update/parent/subtask/attachment fields. Comments, custom fields and attachment bodies were not collected. Redacted examples were not executed.
Membership corroboration: `reports/JIRA-MOS-774.md:7–12,17–19,38` attributes MOS-1409 to the 18-member MOS-774 hierarchy and member-index `#/items/73`; hierarchy membership, not an independently captured REST parent relationship. Its earlier updated timestamp `2026-10-16T17:33:09.886+0800` is separate from the later details snapshot. `reports/G2-JIRA-MEMBER-JOINS.md:25–43,104,203` records MOS-774 membership and MOS-1409 as `U / UD: SK(18) detail only`; unresolved analysis is not absent implementation.

## Atomic requirement register
Locator convention: Dn means line n of the decoded string at `sources/jira-details-MOS-774/r1/content.json#/items/18/description`, counted with `splitlines()` (not physical JSON lines). D5 is “Что сделать”; D20 is “Критерии приёмки”.

| ID | Explicit obligation | Exact locator |
|---|---|---|
| R01 | Add list `POST /api/control/api/skills/v1/skills/export`. | D7 |
| R02 | Add card `POST /api/control/api/skills/v1/skills/{skill_id}/export`. | D8 |
| R03 | Both receive export parameters in JSON request bodies; `{}` selects default settings. | D9,D22 |
| R04 | List reuses `SkillListRequest` search/filter/sort and validation for `query`, `domain_id`, `team_id`, `status`, `type_code`, `sort`; behavior matches the list. | D10,D23 |
| R05 | Both support optional nonempty `fields` column-code list; omission exports all prescribed columns. | D11,D26 |
| R06 | Equal `fields` produces the same columns for list and card. | D26 |
| R07 | Empty `fields` and unknown column codes produce validation errors. | D27 |
| R08 | Export the entire accessible selection independently of current page; do not use `limit` or `offset`. | D12,D24 |
| R09 | Reuse list selection logic, excluding deleted skills and preserving team access restrictions. | D13,D31 |
| R10 | Card reads saved data by `skill_id` with skill-access check, not unsaved edits. | D14,D25 |
| R11 | Both require `TSAM.Skill:view`; team restrictions persist. | D28 |
| R12 | CSV uses UTF-8 with BOM, semicolon delimiter and header row. | D15 |
| R13 | CSV-injection protection is required. | D15 |
| R14 | Return attachment via `Content-Disposition: attachment`; filename contains generation date, plus `skill_id` for card. | D16 |
| R15 | Apply common list-export limit; exceeding it returns an error without a partial file. | D17,D32 |
| R16 | Card CSV has headers and one saved-data row; each skill corresponds to one CSV row. | D25,D29 |
| R17 | Empty selection yields headers only for selected columns. | D30 |
| R18 | Missing/inaccessible card errors follow existing skills API behavior. | D33 |
| R19 | Update OpenAPI with POST methods, JSON body schemas, permitted `fields` values, file response and errors. | D18 |

## Open questions / missing detail, not implementation findings
- No explicit frontend owner, route, button, selection dialog, download interaction or UI error workflow is specified. Determine frontend ownership in reconciliation; do not derive it from the task title or endpoint obligations.
- Column codes, labels, ordering and detailed full-default column set are not enumerated here. Duplicate-field handling is unspecified.
- Numeric common export limit and its exact error status/body are not given; card error status/body references existing API without reproducing it.
- Existing `SkillListRequest` validation/default sort and exact semantics of nonempty bodies containing `limit`/`offset` are not reproduced. “Do not use” does not alone settle reject versus ignore.
- Injection mitigation algorithm, CSV quoting/newline/null conventions, content type, date format/timezone and exact filenames are not specified beyond R12–R14.
- Backend authorization remains explicit; nothing here authorizes adding credentials or role enforcement to local business mocks. No mock requirement is stated.
- Missing comments/custom fields/attachment bodies limit conclusions about additional requirements. No live freshness, delivery or deployment claim.

## Actual read boundary and fingerprints
Only the MOS-1409 object was selected and printed from the parsed details packet; neighboring issue objects were not extracted or analyzed. Metadata was read completely. Membership report reads: JIRA-MOS-774 lines 1–19 plus focused match/context lines 35–41; G2-JIRA-MEMBER-JOINS lines 1–65 plus focused hits 104,203,330,362 and a selected SK/MOS-1409 match. The latter read incidentally exposed unrelated report-chain rows; they were not used or followed. The batch contract was displayed completely (including other lane instructions), but only REQ was executed. No API/spec/code sources were inspected.

Fresh SHA-256 values (local bytes only):

| Input | SHA-256 |
|---|---|
| `work-items/G2-MOS-1409-EXPORT-BATCH.md` | `67b7f9ecf72665502af7379939536ae6f8467fc715def7860e137e72bf5024b0` |
| `sources/jira-details-MOS-774/r1/content.json` | `e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208` |
| `sources/jira-details-MOS-774/r1/metadata.json` | `a76eb6f93c564b94c6c627e4209a449361ef0da69415b49033c584e16fcca1ec` |
| `reports/JIRA-MOS-774.md` | `04f21e1039acdcf56460ba84a0e01101a4b0131a1e9f0d3f47f3191c4a22719c` |
| `reports/G2-JIRA-MEMBER-JOINS.md` | `dc9b199c2a9500b2ff1857de1feaec9282e8130fa1b78720f551913907618b44` |

Primary content hash matches both contract and metadata. Other hashes are fingerprints, not comparisons against an independently supplied expected hash. Historical source hashes quoted in membership reports were not recertified. No project edits, network/browser, tests/build/typegen, credential access, source-example execution or nested agents.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Extracted 19 bounded requirements with exact decoded-description locators, membership/provenance, verified HEAD and primary hash, and explicit unknowns."}],
  "changedFiles": [],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD","result":"passed","summary":"Matches required bc0d9800f25a90989b9c73c76f91996f8300f1d3."},
    {"command":"Python SHA-256 and selected MOS-1409 JSON extraction","result":"passed","summary":"Primary content hash matches contract and metadata; other read-input fingerprints recorded."},
    {"command":"Tests/build/network/browser","result":"not-run","summary":"Prohibited and unnecessary for requirement-only lane."}
  ],
  "validationOutput": ["Saved MOS-1409 requirement evidence only; no implementation/deployment acceptance."],
  "residualRisks": ["Frontend ownership and referenced common CSV/limit/API details require cross-lane reconciliation; omitted source fields remain unknown."],
  "noStagedFiles": true,
  "diffSummary": "No project changes; only configured external report written.",
  "reviewFindings": ["No requirement-lane blocker; missing frontend ownership is an open question, not authorization to implement."],
  "manualNotes": "No files staged by this run; existing staging state not inspected. Actual read boundary and all fresh input fingerprints documented above."
}
```
