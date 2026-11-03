# Code Context

## Decision: REVISE — bounded correction to F1

Independent review of **R-SPEC-G2-MOS-1259 only**. Accept the compatibility, saved-search identity, permission and URL conclusions independently. No new inventory, API audit or publication authorization.

Literal bases: `C = openspec/changes/reconcile-control-center-backlog`; `A = C/audit`; `O = openspec/changes/mos-1259-feedback-saved-filters`; `S = O/specs/feedback-saved-filters/spec.md`; `F = openspec/changes/mos-1249-feedback-api`; `N = openspec/changes/mos-1250-feedback-registry`.

## Key Code / minimum required corrections

### 1. F1: preserve the discrepancy; make method replacement conditional

`A/reports/SPEC-G2-MOS-1259.md:45–49` correctly identifies Jira PATCH versus owner PUT, but incorrectly recommends replacing PUT now. Its “no automatic precedence” disclaimer does not neutralize that instruction. Propagate the correction to Result, matrix method dispositions, Start Here and acceptance summary so they do not independently authorize replacement.

Evidence boundary:
- `A/sources/jira-feedback/r1/content.json:102`, `/items/10/description`, description paragraph2 and AC3/5/6 explicitly require PATCH. Accepted extraction `A/reports/REQ-G2-MOS-1259.md:39–66` explicitly does **not** verify published transport.
- `S:9,14`, `O/tasks.md:3–4`, `O/design.md:27` explicitly use PUT.
- `O/design.md:5–7` delegates source precedence to `F/design.md:5–10`: wire paths/DTOs come from OpenAPI and operation business semantics from CRUD documentation. Moreover `F/design.md:21–23` already instructs use of published **PUT** operations following the contract update. This is directly relevant existing planning evidence, not a newly verified API fact.
- `C/design.md:85–87` distinguishes requirement authority from published wire authority; conflict is a finding, not permission to rewrite it.

**Minimal replacement recommendation:** “Retain Jira PATCH versus owning-plan PUT as an unresolved method discrepancy. Before changing method-bearing planning clauses, join authoritative saved-filter API evidence and any accepted reconciliation ruling through the API owner. If that join establishes PATCH, update all affected references consistently; otherwise retain the discrepancy and resolve it without silent precedence. Preserve selected-ID targeting, complete search input and immutable resource regardless.”

Do not authorize removal of the existing `S:9` whole-object replacement semantics merely because wire semantics were not audited. Any semantic change likewise needs the authoritative join. No new API audit is required within this review, and this finding does not block independent non-method clarifications or reopen product scope.

### 2. Explicitly classify fixture additions as optional precision

The report's imperative “make/explicitly include/refine” wording can be read as new mandatory omissions. Label expanded query/multivalue/nondefault-limit fixtures, repeated pagination wording, and per-error input/no-success examples as **optional acceptance precision**, not missing requirements or prerequisites to accepting the existing coverage. `S:9,18–19,23`, `O/tasks.md:3–4` and `O/design.md:27` already cover full search, stored offset40 versus apply0, independent pagination, form preservation and honest errors.

The proposed title wording alignment is supported as a narrow documentary correction: `O/design.md:27` says “1–150 непробельных символов,” whereas `S:9` and Jira AC1 say 1–150 characters, not whitespace-only. Align wording without inventing trimming, character-counting or internal-space restrictions. Its extra boundary fixtures remain optional precision, not a newly absent requirement.

## Architecture / accepted findings

- **Identity and restoration (F2): ACCEPT.** Full owner consistently distinguishes new record creation from explicit update of the selected ID; duplicate title is not identity (`O/proposal.md:9,14,20`; `S:9–19`; tasks1.1/1.2). Stored search includes offset while apply resets result offset0. List pagination is independent (`O/design.md:27`). No additional naming policy, identity URL encoding or widget is justified.
- **Compatibility (F3): ACCEPT.** `O/tasks.md:4` explicitly disallows partial obsolete-schema application; `N/design.md:33` disallows partial application/automatic rewriting of damaged saved filters; `S:9` supplies error behavior. This is an existing no-partial-apply plan policy compatible with Jira AC4, not evidence of separate user approval and not a new reject-versus-recover gate. Keep original unknown/inactive data (`O/design.md:39`), no invented migration/version fields. Existing form/error/fallback safeguards remain.
- **Permissions (F4): ACCEPT.** `O/design.md:31–33` delegates to `F/specs/feedback-api/spec.md:26–38`: read and action rights, backend ownership, existing exact matching and isolation. Foreign/missing404 in `O/design.md:27` is not replaced by the separate server403 scenario. No new auth model or role-enforced mock requirement.
- **URL seam (F5): ACCEPT.** `N/design.md:31–33` names q/repeated status/repeated type/sort/limit/offset/conditions JSON and the common validated conversion for history/copy/saving/export. Accepted adjacent requirements/review retain MOS-1250 ownership. Saved-filter ID/history mechanics remain unspecified, not new gates.
- **Scope/completeness:** both requirements, all three scenarios and all five numbered unchecked tasks are accounted for in the author's joins. Full proposal/design introduce no overlooked saved-filter requirement that reverses these conclusions. Keep release evidence task2.3 open. Jira description paragraph3 explicitly excludes automatic name overwrite in stage one; wiki §3.5 prototype overwrite does not override that exclusion. No closure/runtime claim follows from any task text.

## Files Retrieved / actual read limits

- Complete governing artifacts: `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`.
- Complete assignments: `A/work-items/R-G2-FEEDBACK-SPEC-WAVE.md:1–25`, `A/work-items/G2-FEEDBACK-SPEC-WAVE.md:1–25`; other assignment descriptions visible, not executed.
- Complete target report `A/reports/SPEC-G2-MOS-1259.md:1–121`; complete accepted input `A/reports/REQ-G2-MOS-1259.md:1–113`, `A/reviews/R-REQ-G2-MOS-1259.md:1–68`.
- Complete owner: `O/proposal.md:1–32`, `O/design.md:1–49`, `O/tasks.md:1–10`, `S:1–28`. Scoped find confirmed one delta spec. Scoped main-capability path search returned none; no implementation inference.
- Primary Jira: `A/sources/jira-feedback/r1/content.json:95–103`, complete assigned record and all six AC only. Wiki `A/sources/wiki-247734813/r1/content.json:8`, decoded `/text` Unicode half-open slices `[1366:3145]`, `[8496:8707]`, `[10514:11134]` (§§3.2–3.6,6.1,8); remainder parsed/hashed, not substantively read. No attachment or metadata reread.
- Explicit seams only: `F/design.md:1–48` (authority clauses used at5–23; remaining visible context not an API audit), `F/specs/feedback-api/spec.md:26–38`; `N/design.md:29–33`; `A/reports/REQ-MOS-1250.md:40–75`; `A/reviews/R-MOS-1250.md:20–64` (findings1/6 used, others incidental historical claims). No fresh adjacent source extraction or adjacent whole-plan audit.

## SHA-256 — recomputed complete file bytes

| Input | SHA-256 |
|---|---|
| `A/reports/SPEC-G2-MOS-1259.md` | `6fb75adc59f208118bc4394edaf83b988312dfd1398ea3a00e8d5707afacff50` |
| `A/reports/REQ-G2-MOS-1259.md` | `b928122009f79f48b4789fadcd476bbd1a8bdf669fc438b4cceacd7b3197bd25` |
| `A/reviews/R-REQ-G2-MOS-1259.md` | `b0287c540b7222d1860f90a72e396960f645d184a12a3f82e8b6cc76d01bbbc2` |
| `O/proposal.md` | `c955adf218151450f06e1260040fd65dff6cf8905ca49eb2720b8d5908da983b` |
| `O/design.md` | `ffd8b183f81be81aee20d199b76cc7ad73ad196b604a41ead9d56019778b8e08` |
| `O/tasks.md` | `029e84d2fb5fad51da26bf567325709055405101a5c91cebddbf9159f04b3b5a` |
| `S` | `4e9aee0264a677b7dd13a6d4a3bb2eb2bd648b52be1b877a19e86bc33e36655f` |
| `F/design.md` | `0b15bcebfea15e35aca35a90c835a00efd892bb9a962fc16401892ca6017d91d` |
| `A/sources/jira-feedback/r1/content.json` | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| `A/sources/wiki-247734813/r1/content.json` | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |

Hashes match the author's recorded shared inputs. They prove retained-byte identity, not live freshness or complete original sources.

## Start Here

Revise `A/reports/SPEC-G2-MOS-1259.md:45–49` alongside `O/design.md:5–7` and `F/design.md:5–23`. Parent owns decisions/publication. No project edits performed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Full owner and precise primary clauses independently checked; REVISE limited to method authority and optional-precision classification, with remaining findings accepted separately."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/4c8350f6-00b1-4897-abcc-c15158018af4/R-SPEC-G2-MOS-1259.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find; Python JSON slices/hashlib; nl/sed","result":"passed","summary":"Read full owner and bounded evidence; recomputed report/input hashes."},{"command":"Network/browser/tests/build/typegen","result":"not-run","summary":"Prohibited documentary-review scope."}],
  "validationOutput": ["Existing delegated API plan expressly names published PUT; accepted Jira extraction cannot authorize PATCH replacement.","No-partial-apply policy, selected-ID identity, complete search and separate pagination already documented."],
  "residualRisks": ["Authoritative saved-filter method/semantics join remains outside this review; no live/API/runtime conclusion.","Jira omitted fields, flattened wiki and unread attachment limit completeness; live freshness unverified."],
  "noStagedFiles": false,
  "diffSummary": "Only configured external review artifact written; project untouched.",
  "reviewFindings": ["REVISE F1 to conditional reconciliation, not immediate PUT-to-PATCH publication.","Mark expanded fixtures/repeated wording as optional; retain supported title clarification.","Accept compatibility, identity, permission and URL ownership findings."],
  "manualNotes": "No tests, network, browser or nested agents. Index not inspected; noStagedFiles=false makes no assertion that staged changes exist. Parent retains acceptance and publication authority."
}
```
