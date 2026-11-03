# IMPL-SKILL-AUDIT-HISTORY

## Result

Current mounted skill history is deliberately unavailable, with written component assertions for its message, keyboard access and absence of an additional request. No frontend audit reader was found within the connected boundary below. Mock status/action storage is separate from a query reader. Existing MOS-1031 tasks remain open; no feature/runtime acceptance is claimed.

Read the common batch contract and assigned item, all five owning-change files, complete accepted DELTA report and independent review. Reused accepted documentary evidence rather than reopening wiki sources. The review remains **REVISE** historically; `audit/decisions.md:223–227` (D-050) accepts its substantive findings and explains why the sole locator complaint was not reproduced. This is not a new reviewer ACCEPT.

HEAD verified before and after inspection: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (expected). Owner/report hashes below were computed before analysis and recomputed unchanged afterward. Decisions hash likewise unchanged across its targeted inspection.

## Scenario → implementation → written assertions → existing tasks

Paths below are repository-relative. W = `app/widgets/skill-details/ui`; E = `app/entities/skill`; M = `openspec/changes/mos-1031-skill-audit-history`.

| Scenario / boundary | Current code and transport/mock evidence | Written assertions, not executed | Existing owner task/gate |
|---|---|---|---|
| Open skill history before accepted reader | Route config `app/shared/config/constants/application-routes.constants.ts:41–42` → `app/routes/skill-details.tsx:1–5` → `app/pages/skill-details/ui/skill-details-page.tsx:1–5` → `W/skill-details.tsx:13–16,55`. `W/skill-details-tabs.tsx:25,40–42` mounts `HistoryTab` without skill/ID props. `W/tabs/history-tab.tsx:1–14` renders only a static card/message, no fetch/hook or fabricated events. | `W/skill-details.test.tsx:149–203` opens History, asserts unavailable text, exactly one fetch and only detail GET; `:205–226` asserts tab keyboard navigation and visible unavailable text. | `M/tasks.md:1–6`: retain unavailable until 1.1; 1.2 reader remains unimplemented in this boundary. |
| Renamed or same-name skills; every-page type+ID filter | Detail hook `E/model/use-skill-details-query.ts:7–20` uses `['skills','detail',skillId]` and AbortSignal. `E/api/skill-details-client.ts:89–94` reads skill DTO, not records. History has neither identity input nor pagination. Existing detail isolation is not evidence of audit isolation. | Rename assertion `W/skill-details.test.tsx:414–440` checks updated heading/cache/list invalidation, **not history**. No history request/filter/page assertion found in connected tests. | 1.1–1.2, 2.1, 3.1 (`M/tasks.md:5–6,10,16`); no closure for renamed/same-name/next-page scenarios. |
| Server record table, historical author, safe details | Static history card has no row/details/author renderer. `E/index.ts:1–51` exposes skill operations/queries, no audit reader. Detail schema `E/api/skill-details-client.ts:15–51` is a loose skill schema, not audit DTO validation; lack of declared history is not a claim that unknown fields are rejected. | Only unavailable message assertions above; no history table, author, pagination, secret-redaction or malicious-detail assertion found in boundary. Existing skill material-link safety tests concern a different renderer. | 1.1–1.2, 2.1–2.2, 3.1 (`M/tasks.md:5–6,10–11,16`). |
| History loading/empty/error/retry and late prior-skill response | `W/skill-details.tsx:18–25,29–36` manages **card** request states; History itself has none. A keyed card Activity (`:30`) and detail AbortSignal do not demonstrate a reader race solution. | Component tests contain card-error/retry and edit-draft isolation checks, not failed-history/empty-history/late-history assertions. The unavailable test does not establish runtime behavior against a service. | 2.2 and 3.1 (`M/tasks.md:11,16`). |
| Mutation succeeded but event delayed; honest history refresh | Mutation search finds detail/list cache updates: `E/model/use-update-skill-mutation.ts:13–20`, `use-change-skill-status-mutation.ts:14–21`, `use-update-skill-intents-mutation.ts:13–38`, `use-toggle-skill-mutation.ts:16–23`. No history query exists to refresh. Some broad `['skills']` invalidations could affect future queries depending on their keys, but do not implement current history refresh. No local history row is rendered. | No delayed-audit-event/history-refetch assertion found. Detail save/refetch tests are not audit refresh coverage. | 2.3 (`M/tasks.md:12`); consistency remains part of 1.1. |
| Mock write/storage is not reader | `mocks/domains-skills.mjs:264–290` returns detail and writes status history only on change; `mocks/skill-operations.mjs:22–40` separately records toggle action/status history. `mocks/app.mjs:61–101` mounts saved-spec operations, with fallback404 at `:104–105`; `mocks/contract.mjs:1–9` loads saved OpenAPI. | `mocks/skills-status-analytics.test.mjs:82–135` asserts stored reason/actor snapshot, duplicate/error/no-change behavior, no `history` in response, GET equals returned detail, and fresh-state reset. These are storage/mock assertions, not frontend query tests. | Preserve 1.1 reader gate and independent 3.1 acceptance; no replacement with local storage. |

## Transport and bounded absences

- Connected skill client uses shared `apiRequest`, with URL construction from Control API base (`app/shared/api/http-client.ts:45–46,71`; `app/shared/config/control-api.ts:10`). Component assertion `W/skill-details.test.tsx:109–112` names `/api/control/api/skills/v1/skills/{id}` and GET. This is skill transport, not the separate audit service.
- Inventory/search boundary: `app/pages/skill-details`, all files under `app/widgets/skill-details` and `app/entities/skill`, connected route/config entries, `app/shared/api`, `mocks`, and local `docs/api/contracts/openapi.json`. Searches for history/History/audit and audit/records/history found the mounted placeholder and mock storage/tests, but no connected audit reader or saved audit endpoint. No claim of backend/global API absence or absence outside this boundary.
- The large `skill-details.test.tsx` read returned lines1–1019 before the tool's size limit; relevant history assertions at149–226 were fully read. Full-file search located all history references. Remaining lines were not claimed as fully read; no whole-suite review is claimed.
- Exact `docs/api/contracts/audit.md` path does not exist (`test -e` exit1). This confirms a stale local evidence pointer, not an absent service.
- Accepted `DELTA-AUDIT-SERVICE-CONTRACT.md` AUDIT-01/06/07/10/11 and its architecture/gates already distinguish documentary service query candidates from approved browser integration, storage projection and deployment. Preserve routing/credential destination, reader authorization, DTO/redaction, identity/event mapping, period/retention/pagination and consistency gates. No token values or credentials inspected; no proposed credential transport changes.

## Necessary existing-plan correction candidate

**IMPL-1031-C01 — evidence wording only, parent review required.** Reconcile `M/proposal.md:24–25` and `M/design.md:3,13` with accepted D-050 and DELTA evidence: replace reliance on nonexistent `docs/api/contracts/audit.md` and unqualified “no contract” interpretation with “saved Control API has no connected frontend audit reader; separate audit-service documentary candidate exists, adoption remains blocked by accepted integration/reader gates.” Link the already accepted DELTA/D-050 rather than introducing a new endpoint or requirement. This is the previously identified owner-reconciliation need, not a duplicate backlog item. Keep `M/tasks.md:3–6` unavailable/1.1 acceptance gate and all checkboxes open.

Otherwise **implementation-plan no-op**: tasks1.1–3.2 already cover the missing reader, states, isolation, mutation refresh and unit/component validation. No additional implementation task or feature activation is justified by this inspection.

## Input SHA256

M prefix as above; A = `openspec/changes/reconcile-control-center-backlog/audit`.

| Input | SHA256 |
|---|---|
| M/.openspec.yaml | `d707823457f58b4f938a99bc049bddd9b937affec2d09c976c9a16a9dcd03f77` |
| M/proposal.md | `59785c7c1d12d1619322c6e1af8451fa1b983193bd7ad1ff1ef9b92384fe3a8e` |
| M/design.md | `3e5b5e3f5130035ea501bbce273388fbd9ac3990cba5d82c2244b6088ffd53db` |
| M/tasks.md | `83c42abdbb9fc3a2f81aaa4a8826f0657df08f26cdc2b884b23aa29d103dada0` |
| M/specs/skill-audit-history/spec.md | `cdfaf7e2a954e49725fd577fc624c7d29d57b06fcddbf7c20ccb73c74feaf87f` |
| A/reports/DELTA-AUDIT-SERVICE-CONTRACT.md | `1b646251f755eff7e1a4df252b86e60f77676c396c64f04ffb16b29e0d587af0` |
| A/reviews/R-DELTA-AUDIT-SERVICE-CONTRACT.md | `3da7c8938207e2ec252be661bf087b61d98e88b86b6a76fb0658f09cd57f044c` |
| A/decisions.md (only D-050 passage relied upon) | `e3b3d5ec2547eed441e896cc556bc63b7e753e485ef5e6e6a057689f97fc1ef5` |

## Validation/limits

Local read/search/hash/Git inspection only; sole write is this configured external artifact. No project edits, network/browser, tests/build/typegen, source execution, credentials or delegation. One exploratory rg included nonexistent `mocks/routes*` and reported that unmatched path; subsequent explicit `mocks/app.mjs` read and mocks-wide search supplied the intended boundary (no infrastructure blocker). Test outcomes/runtime/deployment remain unverified. Independent batch review and parent publication remain pending.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped mounted unavailable history, detail transport, distinct mock storage, written assertions and open MOS-1031 tasks; recorded unchanged owner/evidence hashes and expected HEAD."}],
  "changedFiles": [],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD (before/after)","result":"passed","summary":"Expected bc0d9800f25a90989b9c73c76f91996f8300f1d3 both times."},
    {"command":"sha256sum owner files, DELTA report/review and decisions (before/after)","result":"passed","summary":"All recorded hashes unchanged."},
    {"command":"git diff --cached --name-only","result":"passed","summary":"No staged paths returned."},
    {"command":"tests/build/typecheck/browser","result":"not-run","summary":"Forbidden by read-only assignment."}
  ],
  "validationOutput": ["History placeholder and written no-additional-request/keyboard assertions inspected; no execution claimed."],
  "residualRisks": ["Runtime/service deployment, reader authorization/integration and event completeness unverified.","No full-suite or global API-absence claim; inspected boundary and partial large-test read documented.","Independent batch review pending."],
  "noStagedFiles": true,
  "diffSummary": "No project changes; external report only.",
  "reviewFindings": ["Evidence-wording reconciliation candidate C01 only; existing implementation tasks remain open."],
  "manualNotes": "Accepted documentary requirements reused, not re-extracted. Service/storage evidence does not activate frontend reading. Parent owns publication."
}
```
