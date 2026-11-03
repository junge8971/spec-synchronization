# Code Context

## Result

**Bounded historical-documentation supplement; no MVP change or sandbox activation.** The MOS-914 journal response supplies explicit documentary support for the already-approved no-sandbox MVP and save-before-command intent. It also records proposed future checking, entry and conversation semantics, but explicitly leaves audience unresolved and acknowledges contradictory prototype/role wording. CLOSED means an answer was accepted, not that the workflow exists or its contracts were reconciled.

Only the third data row dated 08.10.2026 (Лиза / MOS-914, Андрей response) and status legend are assessed. Other rows are not findings. No source precedence, role grants, whole-card atomic API, implementation compliance or task closure follows.

## Files Retrieved

Paths are repository-relative; `A` below expands exactly to `openspec/changes/reconcile-control-center-backlog/audit` and `M` to `openspec/changes/archive/2026-10-12-mos-914-surface-lifecycle-mvp`.

1. `A/work-items/JOURNAL-SURFACE-MVP.md` (1–9): scope.
2. `A/sources/wiki-250781168/r1/content.json` (1–13), `metadata.json` (1–24): primary journal; semantic scope `/bodyView` and matching `/bodyStorage`, third data row and legend only. Page revision 8, updated 2026-10-08T18:31:40.254+08:00, captured 2026-10-19T08:24:54.988Z. Locally recomputed SHA-256 matches metadata and assignment: `cd74e398e690d48e3da571a6c2adf02d8c755856948d98747b8d447ad628244d`.
3. `openspec/specs/surface-lifecycle-publication/spec.md` (1–196), fully read: current approved business boundary.
4. Complete archive: `M/.openspec.yaml` (1–2), `M/proposal.md` (1–38), `M/design.md` (1–85), `M/tasks.md` (1–28), `M/specs/surface-lifecycle-publication/spec.md` (1–152), `M/specs/surface-overview-connection/spec.md` (1–43). Checked tasks are historical delivery records, not newly executed tests.
5. `A/decisions.md` (101–113, 159–172): D-012, D-005 and D-004 accepted dispositions.
6. `A/reports/SCENARIO-MOS-960.md` (1–119), `A/reviews/R-SCENARIO-MOS-960.md` (1–117): context/session/version and corrected status/schema evidence.
7. `A/reports/SCENARIO-MOS-961.md` (70–115), `A/reviews/R-SCENARIO-MOS-961.md` (1–108): conversation/history, isolation and mandatory qualifications.
8. `A/reports/SCENARIO-MOS-962.md` (70–108), `A/reviews/R-SCENARIO-MOS-962.md` (1–107): retained sync/recipient/access owner questions and corrections.
9. `A/reviews/RECON-MOS-959.md` (1–107), `A/reviews/RECON-MOS-959-CONTRACT.md` (1–103), `A/reports/SCENARIO-SURFACE-CONFIG-r2.md` (70–115): accepted configurator ownership, split persistence and versioned contradictions.
10. `A/sources/api-live/r2/metadata.json` (complete): newer publication exists, captured 2026-10-19, SHA-256 recorded there `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993`. **No r2 operation/schema scan performed.** API facts below are attributed to accepted historical r1 reports/reviews, not freshly verified current API assertions.

No linked wiki reread was necessary to determine this journal delta; existing accepted comparisons are explicitly secondary evidence here. No image-only admin overview was used. Truncated archive/review output was continued from its inspection spool.

## Key Code / exact primary locators

No application code inspected. For embedded HTML, structural locators are more precise than its long physical JSON lines:

- **J** = `A/sources/wiki-250781168/r1/content.json#/bodyView`, first table, `tbody/tr[4]` (header counted; third data row), second physical `td` (`colspan=2`). This row is independently identified by date 08.10.2026 and Jira macro key MOS-914. Matching content exists under `/bodyStorage`.
- **J-Q1–Q4** = J, first ordered list, items 1–4. UUIDs respectively `c99160ac-6edd-4d1c-9347-1c53292a83a7`, `6ef5a0bd-322f-4c98-ad42-4604746128c7`, `10318adc-ef5a-40c1-8ede-7ac5bde7a9c9`, `014fc1ea-1858-4a49-81ba-8179bf3fa7aa`.
- **J-MVP** = J, paragraph after “Андрей:” and before second ordered list: “Для начала наверное надо сказать что песочница не входит в MVP”.
- **J-A1–A4** = J, second ordered list, items 1–4. UUIDs respectively `9fac1e10-855a-4ef3-bf03-701909c9a0c6`, `f512aa5f-8dd8-4e26-a140-c43341028d5d`, `d24755e2-3be8-40bc-9f39-980daf52b177`, `39e31fd7-9719-46ec-83d2-2c3c29a4feb4`.
- **J-CLOSED** = same row's third physical `td`, status macro `5479af4b-21b9-4391-8313-091671d458e4`: ЗАКРЫТЫЙ. **J-LEGEND** = paragraph with macro `ab39723d-3117-478f-bf10-5a2e2229b5b6`: “вопрос закрытый, ответ принят”. It is distinct from legend РЕШЕНИЕ (decision waiting for action) and ОТВЕТИЛИ (answer still requires a close/clarify decision).

Approved sequence, not a proposed implementation:

```text
confirm → validate current skills/parameters → PUT enabled-skills
        → fresh GET → recheck eligibility → bodyless POST publish
        → fresh GET confirming prod → success
```

Main spec lines 72–78, 181–196 and archive design 40–64 require stopping on preparation/save/read failure, truthful partial success, no fabricated configuration PUT or locally synthesized configured status. These are more precise than “save everything in one action”.

## Stable candidate dispositions

IDs below are supplemental evidence IDs, not new delivery tasks. Existing issue/candidate ownership is preserved.

| ID / classification | Exact journal basis and narrow delta | Existing owner / disposition |
|---|---|---|
| **JOURNAL-SURFACE-MVP-01 — no-op** | J-MVP + J-CLOSED/J-LEGEND explicitly document that sandbox is outside MVP. This answers whether the journal itself intended immediate sandbox delivery: no. CLOSED does not certify execution. | `surface-lifecycle-publication` main spec 37–68; M proposal 5–18, tasks 6/28. Preserve no visible or hidden sandbox launch, readable review/sandbox statuses, history/configurator deferral. No source edit or renewed scope decision needed. |
| **JOURNAL-SURFACE-MVP-02 — bounded documentation candidate** | J-Q1 / J-A1 distinguishes send (save/status/history event) from a successful test: system-recorded pass/fail with author/date/response trace, formed from stand response, no separate user confirmation. It claims a skill record exists but no equivalent surface record, and says edits require rechecking; additional training blocks sandbox. This supplies historical intended semantics, not an operation, test run, revision binding or implemented event. | Existing MOS-960-C08/C09 and MOS961-C05/C07; MOS-962 readiness dependency. Append this provenance to their evidence handoff if separately authorized. Accepted R960 61–80 already distinguishes saved skill checks/history model from session/tested-version proof. Do not revert to “no check metadata exists”, or infer tested revision from status/time/version. Surface result model, binding, invalidation confirmation and completed training evidence remain owner questions. |
| **JOURNAL-SURFACE-MVP-03 — no-op with bounded wording candidate** | J-A1 says sandbox checklist criterion has no effect and publication is blocked “only” by no scenarios/draft. Historical support exists for no sandbox prerequisite, but “only” is not the complete approved MVP policy. | Main spec 39–78, 100–103 and M overview delta 24–43 govern: allowed configured/review/sandbox, current AND saved nonempty composition, valid parameters, successful save/fresh read; disabled/archived/prod do not directly publish. Saved greeting/domain facts and unconfirmed global validation are not readiness proof; no new greeting blocker. Sandbox checklist item is removed, not retained as a failed optional check. Preserve SANDBOX_CHECK_REQUIRED handling without hidden sandbox (main 138). Existing MOS961-A04 remains a versioned contradiction with linked contract §2.7; journal does not erase it. |
| **JOURNAL-SURFACE-MVP-04 — bounded documentation candidate; genuine future owner question retained** | J-Q2 / J-A2 explicitly favors Russian entry labels «Настроена», «Проверка», «Песочница» for the future send transition, distinguishes prototype visibility “any except Prod”, and acknowledges contradiction with absent action buttons in Draft/Checking/Sandbox. Draft must save first; Disabled must return to work first; Archive cannot send. This narrows historical analyst intent, not current transport truth. | MOS-960 surface/product/backend owner; existing R960 51 and MOS961-A03. Retain Russian «Проверка» versus wiki `checking` versus historical OpenAPI `review`, and historical API permissiveness including prod/archived. No aliases or precedence chosen. Approved MVP still never sends sandbox; enable/restore show actual server status, including accepted prod response, rather than forcing configured (main 43–63; M design 64). Future entry/visibility and contract reconciliation remain open only if activated. |
| **JOURNAL-SURFACE-MVP-05 — genuine owner question, supplemented not closed** | J-Q3 / J-A3 expressly says recipients remain undefined: all surface users, sender only, or status only. The same answer attributes to prototype a separate test session/contour without replacing production configuration and a Sandbox screen with live dialogue/trace/timings/errors/history. Those assertions do not resolve its own stated unknown. | MOS-960-C02/C04/C08/C09, MOS961-C01/C03/C05/C07 and MOS-962 context/configuration owner question 3. Preserve audience, server session identity/lifecycle, effective loaded snapshot, isolation, synchronization and conversation/history protocol questions. Do not substitute ordinary-dialog APIs or claim either proven production isolation or backend absence. New evidence is historical UI intent, not a session contract. |
| **JOURNAL-SURFACE-MVP-06 — no-op for policy; genuine existing owner question** | J-A3 attributes dialogue access to control-center administrator, reviewer, skill owner and skill analyst; history to everyone except dialogue analyst/observer. It explicitly contrasts surface owner's matrix view/warning-only access with prototype dialogue access. | Existing access/backend/product owners in accepted MOS-961 and MOS-962 reviews, not a new role model. Record the contradiction as documentary attribution only. No grants, permission-string mapping, auth reinterpretation or role enforcement inferred; no role assigned to a person. D-012 historical auth approval remains preserved, neither reopened nor extended to sandbox. No fresh auth/mock-policy analysis performed. |
| **JOURNAL-SURFACE-MVP-07 — bounded documentation candidate; existing integration question retained** | J-Q4 / J-A4 explicitly includes greeting, suggestions, cards, color/shape/font AND scenario composition/skill parameters; saving precedes send/publication, failure stops next command and status change. This narrows a blanket “save orchestration intent unknown”: historical business ordering and desired scope are documented. “Whole card, one action” does not establish one request, server atomicity, rollback or a combined PUT contract. | Existing lifecycle owner main 72–78/179–196 and MOS-959/configuration contract owners under D-004/005. Current MVP saves only editable skills/parameters; absent configuration editor is not simulated. M design 44/54/58/78 explicitly preserves partial success and excludes whole-card transaction. Future integration still needs separately approved editor orchestration/recovery and reconciliation of wiki combined persistence versus historically published separate operations. No new configurator change is created; no hidden PUT, default write or automatic publish added. |

## Architecture / what changes in the evidence, not the product

The journal sits between business intent and an already narrower approved delivery. Entity status is not a check result; a check/history record is not a server test session; a prototype session is not an agreed audience/isolation contract. The existing lifecycle coordinator owns saves and publication for the editable skill draft. A future configurator would introduce additional draft ownership and persistence, but this report neither designs nor activates it.

**Historically answered/narrowed:** explicit no-sandbox MVP; send alone is insufficient testing; desired automated result capture and no manual result confirmation; intended recheck after edits/training prerequisite; analyst's preferred entry labels versus prototype visibility; full-card business save intent and stop-before-command ordering. These are documentary answers only.

**Still open:** surface check/result contract, tested revision/session binding and invalidation confirmation; audience/effective stand state/isolation; conversation/events/history transport and version; sync confirmation; contradictory role claims and approved operation mapping; future configuration-save composition/recovery and contract alignment. Some journal assertions reinforce already-known intent rather than supplying any new contract.

D-005 contradictions remain intact: shape/font vocabulary, nullable fallback versus required-string PUT, initialization defaults/payload, combined configuration/skills persistence versus separate operations, and weaker timestamp/example tensions. Journal contains no resolving schema. Already-published bounds, HEX/UUID/normalization facts are not reopened as missing documentation. No chronology-based authority is selected. Earlier r1 API findings are historical accepted evidence; newer r2 exists and has not been re-audited here.

## Start Here

Open `openspec/specs/surface-lifecycle-publication/spec.md` lines 179–196, then M proposal lines 9–18 and J-A4. Together they explain why “save the whole card” adds historical intent without authorizing a configurator or atomic endpoint. For sandbox claims, read main lines 37–78 alongside J-MVP/J-A1 before using future workflow prose.

## Validation and residual risks

Manual bounded comparison completed; primary journal hash verified. No input blocker. Only this report intentionally written; no application/source/spec/task edits, network/browser/MCP, tests/builds, nested delegation, credential access or executed source examples. No implementation or fresh API scan claimed. Git/index was not inspected; no clean-tree or no-staged-files attestation. Independent review and any subsequent bounded documentation publication remain separate approvals.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Seven stable journal candidates with exact third-row/list-item UUID locators, complete main/MVP comparison, existing accepted owners and explicit no-op/documentation/question dispositions."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOURNAL-SURFACE-MVP.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local find/read/grep and read-only nl/sed/wc inspection","result":"passed","summary":"Read complete lifecycle main and all MOS-914 MVP archived artifacts; consulted scoped accepted reports/reviews and decisions; recovered truncated inspection output."},
    {"command":"sha256sum openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-250781168/r1/content.json","result":"passed","summary":"Matches cd74e398e690d48e3da571a6c2adf02d8c755856948d98747b8d447ad628244d."},
    {"command":"Tests/build/network/browser/runtime/API scan","result":"not-run","summary":"Outside this local documentary assignment; API conclusions attributed to accepted historical evidence only."}
  ],
  "validationOutput": ["No sandbox activation, role grants, whole-card atomic API inference or source precedence.","Historical answer acceptance distinguished from deployed behavior and current approved MVP."],
  "residualRisks": ["Journal retains explicit audience and role contradictions; session/tested-version and runtime isolation remain unproven.","Historical accepted API comparisons use r1; r2 publication exists but was not semantically scanned here.","No code/tests/runtime verification or index inspection; independent review pending."],
  "diffSummary": "Sole mandated findings artifact; no product/source/spec/archive/task mutation.",
  "reviewFindings": ["No missing-input blocker; retain existing owner questions and D-004/005/012 boundaries."],
  "manualNotes": "Manual primary-journal versus approved MVP and accepted-evidence comparison only. Source CLOSED means answer accepted, not runtime proof. Index state uninspected. No implementation or writer authorization implied."
}
```
