# IMPL-SKILL-PHRASE-CONFLICTS

## Result

**Justified planning no-op.** Current mounted UI explicitly leaves conflicts unverified; a generated contract and an independently callable local mock exist, but no application conflict-check client/invocation/result pipeline was found within the inspected boundary. Existing MOS-1018 tasks already cover the missing integration and remain open behind 1.1. Do not republish the accepted four corrections, reopen excluded count/highlighting proposals, or infer feature/runtime acceptance.

HEAD verified before and after inspection: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Full owning change and all accepted inputs/reviews listed below were read. Their hashes were recorded before code analysis and rechecked unchanged afterward (batch instruction hash recorded at final check). Publication acceptance is documentation-only. No external source re-extraction was performed.

## Scenario → mounted code → transport/mock → written assertions → existing tasks

Paths are repository-relative. Task references are to `openspec/changes/mos-1018-skill-phrase-conflicts/tasks.md`.

| Scenario/boundary | Current code and written evidence | Existing task/gate |
|---|---|---|
| Global check / conflict outside current registry page | `app/routes/skill-details.tsx:1–4` → `app/pages/skill-details/ui/skill-details-page.tsx:1–5` → `app/widgets/skill-details/ui/skill-details.tsx:13–55`. Tabs mount editor and checks (`ui/skill-details-tabs.tsx:31–35`); `ui/tabs/checks-tab.tsx:12–19` shows server status and explicit unverified/unavailable notices, not a clear result. `ui/skill-details.test.tsx:148–203` asserts notice, absence of fabricated passed/progress state, and only one GET detail request across tabs. No frontend global-check invocation found. | 1.1/1.2, 2.3, 3.1; unavailable is not completion. |
| Editor save is not preflight | `app/features/skill-training-phrases/ui/skill-training-phrases.tsx:12–62` and `model/use-skill-training-phrases.ts:21–48` manage form/snapshot and PUT mutation, not conflict state. `handlers/training-phrases-handlers.ts:14–32` submits the full draft and accepts saved response. `app/entities/skill/api/skill-intents-client.ts:19–30` sends versioned PUT intents with idempotency header through existing `apiRequest`. `model/use-update-skill-intents-mutation.ts:15–38` disables automatic retry, merges confirmed intents/version, invalidates detail/registry. `app/widgets/skill-details/ui/skill-details.test.tsx:696–758` asserts PUT body, pending controls, saved response and subsequent GET; `760–789` preserves confirmed save when that GET fails. `app/entities/skill/api/skill-intents-client.test.ts:15–54` asserts PUT contract, malformed/mismatched responses, and no retry after API error. These are save tests, not conflict-client tests. | 1.2, 2.2, 2.4; preserve existing save/recovery protocol. |
| Wizard invocation/recovery | `app/routes/skill-creation.tsx:1` → `app/pages/skill-creation/ui/skill-creation-page.tsx:3–21` mounts existing registration. `app/features/skill-registration/ui/registration-wizard.tsx:100–115` composes step/navigation; `ui/registration-step.tsx:16–30` selects review/phrases. `ui/steps/registration-phrases.tsx:30–33` explicitly says conflicts unchecked and save does not mean training. `model/use-registration-save.ts:65–100,117–142` implements POST → GET actual version → PUT intents, recovery phases, no preflight. `ui/skill-registration.test.tsx:28–89` asserts unavailable notice, Create enabled, no draft-save/send-for-check buttons, and no writes from generic form submit. `298–344` asserts exactly POST/GET/PUT and distinct keys; `346–383` asserts repeated clicks/refetch failure do not repeat creation. | 2.4; do not rebuild wizard or add guessed send. |
| Exact/semantic rendering and restricted disclosure | `app/shared/api/schema.d.ts:4615–4645` contains single phrase request and conflict array with type/severity/similarity and required skill/domain id/name objects. Generated DTO presence is not a runtime decoder or safe restricted-detail policy. No application conflict table, semantic warning, neutral hidden-detail renderer, or disclosure fetch pipeline found. Mock `mocks/skill-operations.mjs:43–61,92–99` scans other saved skills, trim/lowercases Russian text, emits exact/blocking/100 with skill/domain. It does not simulate semantic matching or redact details. | 1.1 must settle disclosure/normalization; 1.2 decoder; 2.1 presentation/no-extra-fetch assertions remain missing. |
| Single-phrase clear result must not certify whole input; stale/pending/error/retry | No conflict-result state exists in the editor/wizard/hooks inspected. Their dirty snapshots and version handling protect edits, not checked-input identity. No written preflight race, error/retry, whole-set certification, or restricted-detail assertions were found in the named slices/tests. The mock handler returns conflicts without a persistence write, but its focused test does not assert persisted readiness is unchanged. | 2.2 and 3.1 already explicitly require these cases; no duplicate tasks. |
| Agreed send gating | `app/widgets/skill-details/ui/skill-details.tsx:48–55` mounts lifecycle separately from phrase editor. `app/features/skill-lifecycle/model/use-skill-lifecycle.ts:28–35` guards read/fetch/mutation/refresh state and confirmation skill ID/version/status, not phrase conflict/current draft. `ui/skill-lifecycle.tsx:66–76` binds permission button to that guard. `app/entities/skill/api/skill-details-client.ts:68–87` sends status POST with expected_version/idempotency. Detail test `ui/skill-details.test.tsx:164,170–174` explicitly combines enabled draft send with unchecked conflicts. This is current baseline behavior, not evidence MOS-1018's future agreed-send gate is satisfied or permission to block saving. | 1.1 retains concrete send/server revalidation decision and draft→checking tension; 2.3 then integrates exact/pending/stale/error and semantic warning. |

### Mock wiring and bounded test coverage

`mocks/app.mjs:35–44,62–106` registers `skillOperationHandlers` by saved operationId, validates requests, and routes them under `/api`; the conflict operation is not in its idempotent-write list. `mocks/api-update.test.mjs:119–161` writes another skill's phrase, asserts normalized exact match with exact DTO details, unmatched `[]`, self-exclusion, 422 for empty/overlong phrase and 404 for unknown skill. These are **written assertions only**, not executed results. They do not cover inactive-group exclusion (the helper iterates all intents), semantic scoring/order, hidden data, current-input races, server-on-send enforcement or full registry production behavior. `mocks/README.md:180` explicitly bounds this mock to exact trim/lowercase matching and says absence of exact matches does not prove production conflict freedom.

## Evidence distinctions and inspected absence boundary

- Accepted documentary inputs already establish published single-phrase preflight versus persisted full-set save/recalculation versus agreed-send validation; linked catalog delta is accepted no-material-delta. These facts were reused, not re-extracted from snapshots.
- Generated API shape at `app/shared/api/schema.d.ts:1399,4615–4645` and local mock implementation are positive presence evidence. They do **not** establish deployed availability, accepted normalization/disclosure, or frontend integration. Do not label the API absent.
- File discovery covered `app/pages/skill-details`, all `app/features/skill-training-phrases`, all `app/entities/skill`, connected detail widget, registration and lifecycle paths and their written tests. Targeted application search for `phrase.conflict|PhraseConflict|check_phrase` found generated schema references only; scoped searches in entity/editor/registration/detail widget found none. Direct reads of mounted forms, hooks, clients and mock confirmed the boundary. This is not an exhaustive whole-repository behavioral proof or a search for every possible synonym.
- Old accepted review statements limiting the UI command matrix are historical context, not a current-code description: `app/features/skill-lifecycle/constants/skill-lifecycle.constants.ts:9–17` currently maps seven forward actions. This assignment neither audits their separate authorization history nor recommends reverting/expanding them. MOS-1018 must still use the send agreed in task 1.1.
- No new necessary plan correction identified: tasks 1.1/1.2, 2.1–2.4, 3.1/3.2 already own the observed missing implementation/tests. Mock fidelity differences are limitations, not authority to implement production semantics before 1.1. Runtime/deployment, semantic algorithm, safe disclosure and server revalidation remain unknown/unverified.

## Input SHA-256 manifest

`P = openspec/changes/mos-1018-skill-phrase-conflicts/`; `A = openspec/changes/reconcile-control-center-backlog/audit/`.

| Input | SHA-256 |
|---|---|
| P `.openspec.yaml` | `d707823457f58b4f938a99bc049bddd9b937affec2d09c976c9a16a9dcd03f77` |
| P `proposal.md` | `8a5437a6850b21aa0d1b6343527b22f2c002cb87e14b5b2416a7b43daffd01df` |
| P `design.md` | `624af037030f75831ab0dc3068808b0659f007088a1441b2aac88c07d1624a0a` |
| P `tasks.md` | `fd18b43481483c2c42aeb08aeaf73b9f339d1d7b317eb725b954daf0ef1fb66a` |
| P `specs/skill-phrase-conflicts/spec.md` | `479fc93a9e4133d32af81e763c686730395114641386a36d72ef510d8d355808` |
| A `work-items/G2-SKILL-IMPLEMENTATION-BATCH.md` | `e8237f43cfd87e1a39b1e717deb2dfaa6ccb0fdc05e459ffbcfda3891fd4581a` |
| A `reports/REQ-MOS-1018.md` | `a68c56b72f18baee6ec2e7051efd28c3069f50dd97fb304381ac9f1339f81157` |
| A `reports/SCENARIO-SKILL-CHECKS.md` | `6f7d55e19d37b668de2df544ae6cfd371cb90500c39b125dced1713742459c5b` |
| A `reports/DELTA-MOS-1018-LINKED-CONTRACT.md` | `87ad0b778d76fd151ee87eb5d0a18f4c1945b04a6390f309e984b1ce5c774b01` |
| A `reviews/RECON-MOS-1018.md` | `51a41f8839bd35b628b24b0d0a792777e36096959fcc3b882f2cf01cafa1d474` |
| A `reviews/R-SKILL-CHECKS.md` | `64c8e4caab3d46614cbb63b0ce6d691bd354ed124fae7150deb31651116df909` |
| A `reviews/R-DELTA-MOS-1018-LINKED-CONTRACT.md` | `2c3ded1f6399b03bfa72eadf4bd58acaea8aa9930edb55ff4d71cecc333250ce` |
| A `reviews/R-WRITE-MOS-1018.md` | `adef3368c2df142df3964e2484cb5c18bb5f0afd6896807a2506721919395c57` |
| A `publication/WRITE-MOS-1018/acceptance.json` | `a5d58cc0c11e7ef6ebebf95e7ff9ccd0b9139ab9285e01593bf11e5e6a4839bc` |

## Validation / disposition

Read-only listing, search, file reads, SHA-256 and HEAD/index inspection only. Some exploratory searches named nonexistent guessed paths; actual owners were located and read afterward (not infrastructure failure). No project files edited, credentials accessed, tests/build/typegen/browser/network run or nested delegation. Only configured output written. Parent owns publication and independent batch review; no task checkbox closure.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped mounted editor/wizard/checks and send guards to clients, generated DTO, mock and written assertions; bounded missing conflict pipeline and preserved existing gated plan."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/d10d3bb3-05f1-4405-859e-1a42d0ade96a/impl-skill-phrase-conflicts.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD; input SHA-256 before/after","result":"passed","summary":"Expected HEAD and unchanged owning/accepted input hashes verified."},
    {"command":"Read-only find/rg/read inspection","result":"passed","summary":"Connected UI, transport, mock and written assertions inspected; guessed missing paths resolved."},
    {"command":"git diff --cached --name-only","result":"passed","summary":"No staged paths."},
    {"command":"Tests/build/typecheck/typegen/browser/network","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["No-op planning recommendation; all existing MOS-1018 implementation gates remain open."],
  "residualRisks": ["Normalization, disclosure, whole-input binding and concrete send/server validation remain gated.","No runtime or deployment verification; local mock exact matching is intentionally incomplete.","Absence findings are bounded to named connected paths and searches, not exhaustive behavioral proof."],
  "noStagedFiles": true,
  "diffSummary": "Configured report only; no project edits.",
  "reviewFindings": ["No necessary new plan correction; generated/mock presence must not be confused with frontend conflict integration."],
  "manualNotes": "Written tests were inspected, not executed. Historical review command limits were not represented as current code. Independent batch review and publication remain parent-owned."
}
```
