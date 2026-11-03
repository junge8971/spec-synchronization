# Code Context

## Result — IMPL-G2-FEEDBACK-SURVEY-MOCK

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches assignment). Read-only static inspection: **connected generic survey CRUD scaffold, not faithful nested-question/label scenario support**. It provides in-memory nested ID generation, replacement/order and omitted-field preservation, but lacks the business validation/canonical label behavior described by accepted API evidence. Existing tests exercise generic CRUD; they do not assert the assigned nested/label scenarios. No tests or requests executed. No UI, real integration or deployment conclusion. Q1 remains unresolved; no preserve/omit/block policy selected. Parent owns acceptance.

Aliases below expand literally: `C=openspec/changes/reconcile-control-center-backlog`, `A=openspec/changes/reconcile-control-center-backlog/audit`. Qnn = REQ-G2-MOS-1254-nn; Lnn = REQ-G2-MOS-1257-nn.

## Key Code — bounded evidence joins

| Join | Actual connected implementation | Existing assertion / bounded finding |
|---|---|---|
| Parent POST/GET/PUT; Q02,Q21; L04 | `mocks/app.mjs:35–104` registers operations from actual loaded OpenAPI; `mocks/managed-resources.mjs:169–193` maps operation IDs to `create_fb_survey`, `get_fb_survey`, `patch_fb_survey`. `patch` is an internal handler name, not HTTP PATCH. `saveResource:21–40` responds 201 with ID or 200 with record; GET `43–55` returns stored record. | `mocks/managed-contract-test-helpers.mjs:69–95` calls POST→GET→PUT (description null), asserting code/description and generic search/export/deletion. `mocks/contract-documents.test.mjs:190–222` asserts schema/method presence, not scenario persistence. No inferred feature completion. |
| Nested IDs/order/full replacement; Q09,Q21–24,Q30–31 | `mocks/managed-resources.mjs:28–34` shallow-merges existing root and request. `mocks/managed-model.mjs:27–59,72–76` recursively populates Create then Response schemas: absent IDs receive randomUUID, supplied IDs survive, arrays map in request order. Supplied questions replace the whole array; supplied options are not merged by ID; omitted options inside a supplied question become `[]`. Omitted root questions retain existing composition; `[]` clears it. | Static implementation supports normal full-final-list round trip if callers resend existing IDs. No identity/ownership reconciliation: schema-valid supplied UUIDs are accepted without checking membership/duplicates; omitted existing nested IDs generate new ones. This is not a newly invented error policy. Helper fixture `:17–24` contains one question/one option, but no nested ID, text, membership or order assertion exists in `:69–95`. No edit/reorder/add/delete nested fixture in the fully read managed suite. |
| Nested limits/forbidden fields; Q10–15,Q24 | Request middleware `mocks/contract.mjs:139–177` validates against actual request schemas before handler. Read schemas enforce max100 questions/options, title1–500, option text1–255, UUID shape, no extra request fields. `managed-model:31–59` fills optional required=false/options=[]. | **Business-validation gap:** the connected save path has no tags-nonempty or known-non-tags-options rule. Thus schema-valid `tags` with empty options and known `text` with nonempty options pass these guards by static analysis. Existing fixture actually uses question type `rating` plus options (`managed-contract-test-helpers:23`), so it is a generic permissiveness fixture, not proof of seven-type fidelity. Q1 is not decided by this observation. No nested limit/boundary assertions were found in the bounded suite. |
| Active/inactive/unknown references; Q25–28 | Generic handler validates response shape and duplicate survey code (`managed-resources:35–37`); it does not consult question-type lookup data or existing question membership. Type_code is merely a bounded string in the runtime schema. | Static permissiveness can retain an unknown code/options, but does not establish approved Q1 semantics or faithful active-only new-reference behavior. No survey nested REFERENCE_INACTIVE/REFERENCE_NOT_FOUND handling is present on this connected path. Do not propose credentials or role enforcement for these local mocks. |
| Labels omission/clear/null; L05–10,L17 | Root merge preserves omitted `tags`, `segments`, `operator_groups`; supplied strings replace them; Create defaults absent labels to empty. Empty string persists unchanged. Arrays fail request validation. PUT null is admitted by Patch but remains null through population and fails nonnull Response validation (`managed-validation:6–16`), yielding 422 before mutation. | Partial scaffold support: omission and literal-empty clear are represented, but there is no global label store/association model proving global-lifetime behavior. Switching audience alone leaves omitted stored labels unchanged by merge. Tests assert nullable owner/description, **not label** omission/empty/null/audience preservation. No canonical chip adoption or UI no-CRUD conclusion. |
| Label canonicalization/limits; L06,L11–16 | `managed-model:44–59` copies primitive strings unchanged. `managed-resources:21–40` has no label parsing/canonicalization; runtime schemas only bound each string to16000. | **Business fidelity gap:** no comma parsing, edge trim, skipped empty tokens, case-insensitive dedupe, saved-spelling reuse, sorting or comma-space output; no per-field100-distinct/150-after-trim limits; no parsed-nonempty-segments validation. Whitespace/comma-only strings remain raw rather than canonical empty. Static examples: a 151-character single tag or 101 distinct short tags fit the schema and reach storage; `audience_type='segment', segments=''` fits it too. These are reasoned code paths, not executed requests. Accepted API report `:91–93` and review `:15` explicitly settle these requirements; this is not reopening the earlier count-scope uncertainty. |
| Error/no false success; Q32–34,L18–19 | Request schema errors yield422 `{detail:[{loc,msg,type}]}` with decoded path components (`contract:34–50,139–177`). Invalid final response yields generic loc `['body']` (`managed-validation:6–16`). Missing entity gives404, duplicate root code409 `DUPLICATE_CODE` with message-only errors (`managed-resources:23–37`, `contract:200–202`). Candidate validation precedes push/Object.assign. | Schema-invalid nested values can produce nested422 loc paths, but no faithful nested business409 JSON-Pointer errors are constructed. This agrees with the accepted API lane's distinction between formal422 and business prose; do not claim mock422 violates formal OpenAPI. `managed-resources.test.mjs:42–69` snapshots state around generic invalid requests/missing entities and asserts unchanged state. It does not assert nested409/422 targets, label errors or failed draft retention. Client input retention is out of this mock seam. Empty PUT `{}` is accepted by the path and updates timestamp, unlike accepted CRUD EMPTY_PATCH prose; no survey empty-PUT rejection assertion. |

### Minimal critical snippets

`mocks/managed-resources.mjs:28–39`:
```js
const record = enrichManagedRecord(resource, {
  id: randomUUID(), created_at: timestamp, ...existing, ...req.body,
  updated_at: timestamp,
});
if (!validManagedRecord(resource.schema, record, res)) return;
// duplicate root code check precedes persistence
if (create) items.push(record);
else Object.assign(existing, record);
```

`mocks/managed-model.mjs:31–36,55–59`: missing arrays become `[]`; missing `id` becomes `randomUUID()`; arrays of objects are populated with `value.map(...)`, with no sort or merge by ID. This explains the normal-path identity/order capability and its limits better than generated DTO presence.

## Architecture

`createMockState` (`mocks/state.mjs:13–34`) initializes `createManagedState` (`managed-model:95–101`), whose survey collection starts empty. `createMockApp` loads the aggregate contract and registers the actual method routes under `/api`; `toRoutePath` strips `/api/control/api` (`contract:71–73`). Thus the local route is `/api/v1/managed-resources/feedback/surveys[/:entity_id]`. Request validation → generic survey handler → recursive schema-driven defaults/IDs → response-record validation → in-memory write → validated success envelope.

The later handler overlays were checked at their returned-key seams: knowledge-base overrides kb_entry, A/B overrides ab_experiment, registry overrides api_endpoint/tpl_template; none replaces fb_survey. These bounded overlay reads are composition verification, not adjacent business audits. Optional scenario middleware exists (`app:39,56–59,76–77`); its internals were not audited. Test start uses default sessionDemo=false (`managed-resources.test:12–15`). Observations concern the ordinary managed handler, not synthetic scenario responses.

No mounted frontend, shared real transport or deployment inspected. Persistence here means process-local state, not durable backend persistence. No business calls, test processes, network/browser activity, typegen or nested agents.

## Files Retrieved — actual semantic coverage

Full reads (line ranges inclusive):
- `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`; `A/README.md:1–25`; `A/work-items/G2-FEEDBACK-IMPLEMENTATION-SEAMS.md:1–17` (common contract and assigned unit; neighboring assignments incidental).
- `A/reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md:1–162`, `A/reviews/R-API-G2-FEEDBACK-SURVEY-MUTATIONS.md:1–72`; `A/reports/REQ-G2-MOS-1254.md:1–133`, `REQ-G2-MOS-1257.md:1–135`; `A/reports/SPEC-G2-MOS-1254.md:1–160`, `SPEC-G2-MOS-1257.md:1–144`; `A/reviews/R-SPEC-G2-MOS-1257.md:1–82`. Accepted joins reused, primary Jira/wiki/CRUD not freshly audited. Large combined read was truncated; omitted portions recovered through `/tmp/pi-bash-9a7dbc98158cea68.log` reads. No conclusion depends on unseen output.
- `mocks/managed-model.mjs:1–101`, `managed-validation.mjs:1–91`, `managed-resources.mjs:1–194`, `managed-resources.test.mjs:1–277`, `managed-contract-test-helpers.mjs:1–112`, `app.mjs:1–127`, `contract.mjs:1–202`, `state.mjs:1–34`. Neighbor saved-filter/deletion/display-rule code incidental; not separately audited.

Bounded reads:
- `A/decisions.md:1–25` (D-066/D-065 and start D-064).
- `mocks/managed-registry-handlers.mjs:100–146`; `mocks/managed-registry-model.mjs:1–42`; `mocks/knowledge-base/handlers.mjs:96–123`; `mocks/ab-testing/handlers.mjs:93–120`; `mocks/contract-documents.test.mjs:190–245`. Additional targeted navigation excerpts in state/three overlay handlers are search-only, not full module reads.
- `docs/api/contracts/openapi.json`: parsed whole bytes; semantic read only full JSON operation pointers `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys/post`, `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys~1{entity_id}/get` and `/put`; complete `/components/schemas/{FeedbackSurveyCreate,FeedbackSurveyPatch,FeedbackSurveyResponse,FeedbackQuestion,FeedbackQuestionResponse,FeedbackOption,FeedbackOptionResponse}`. These are the actual runtime-loaded validation/population inputs, not generated declarations used as implementation proof. No complete schema-closure/API re-audit claimed.

Discovery limits: `find **/*` in A (500-result truncation; navigation only); `find *.mjs` in mocks (nested paths returned); scoped `rg -n 'managed|feedback|fb_survey'` in state and three overlay handlers; scoped `rg -n 'questions|operator_groups|segments|feedback/surveys|fb_survey' mocks/*.test.mjs` found survey references in managed-resources and contract-documents tests. Actual full managed test/helper reads establish their assertion gaps. This is not an exhaustive repository test absence claim; application tests/other source roots were not searched. No UI absence claim.

## Start Here

Open `mocks/managed-resources.mjs:21–40`, then `mocks/managed-model.mjs:27–59` beside `mocks/managed-contract-test-helpers.mjs:17–24,69–95`. They isolate both the useful scaffold and why generic CRUD coverage cannot stand in for Q21–34/L07–19 scenario fidelity. Any future authorized correction would likely touch these helpers/validation and the managed test suite; no changes proposed for unresolved Q1, no new product gate.

## Input SHA-256

Complete-byte hashes, not claims of full semantic reads. Paths use the exact aliases above.

| Input | SHA-256 |
|---|---|
| C/proposal.md | 1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879 |
| C/design.md | 632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828 |
| C/tasks.md | a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83 |
| C/specs/control-center-backlog-reconciliation/spec.md | a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36 |
| A/README.md | e1fc6e1f8f4063a9c75a59dbad75e4a6b0dc98b505a2f5a50db43c6167edb9d6 |
| A/decisions.md | 0c6ab613cd2f9d7a6ba9c79609cafd1dc3fc73d0c1645cbcee355b06e0b3d857 |
| A/work-items/G2-FEEDBACK-IMPLEMENTATION-SEAMS.md | 34e936ab5ed856502b7ef90636c6ef6257d8b0cba6b1cf40e571f372ab565f66 |
| A/reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md | 7ad3581a30759824b88905c5ba6a04f969784b2a04661af4a04d964821de95be |
| A/reviews/R-API-G2-FEEDBACK-SURVEY-MUTATIONS.md | 522ab17db6d94ace1c484dd5bdb566328822c43b388d94aa3a53d0ab1af0fee0 |
| A/reports/REQ-G2-MOS-1254.md | 764084c9fed0d395911e5ee57198d5a1dc125d667f9f54d98ed9491a11032f92 |
| A/reports/REQ-G2-MOS-1257.md | bab215846ec9451dfe979865097509f2b5adce9cfd683d454bf63047e8d9979d |
| A/reports/SPEC-G2-MOS-1254.md | d63bd8618ea0f4ac2aaff2f18676cdb80a51c8f47c1b7b0d06f346361ba262ac |
| A/reports/SPEC-G2-MOS-1257.md | 2fc5d7be701420778b67cbff6e65df7731b22fc6c38da6e13c6f53b06a8d0e85 |
| A/reviews/R-SPEC-G2-MOS-1257.md | 8d963bc8fc071e9a12f7f2bed8ac8685d80239184c92959d503d33da3b2527b9 |
| mocks/managed-model.mjs | 472534b1746b60145a8e45d35cd98c141afd3ab59bd1c6ee5194061ea6a95a61 |
| mocks/managed-validation.mjs | fce2b2f8bbd2d7820a9885e3a8a1358ef042d5c3225bef02c6a151231382b44c |
| mocks/managed-resources.mjs | 491ea71f90c4ef4c6b7876450b3f763286ff856e5c9c076eb92cf74570ef6483 |
| mocks/managed-resources.test.mjs | f84fb6d35b7b88d35cb86fd38d5d7666b5aa0c661ce43cae551cdec920b43245 |
| mocks/managed-contract-test-helpers.mjs | d1e753fbe2de85f72287672b82728defb34cb1b8c1e7218377b4e6df92cfaf62 |
| mocks/app.mjs | b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0 |
| mocks/contract.mjs | ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371 |
| mocks/state.mjs | d80532dc6318021afe15c65bb095ebac55876d34e61195e0731604d6af59a93e |
| mocks/managed-registry-handlers.mjs | 20cc8eeb909ab7c525fbe002f55d59425c031da17dfd66c975a159bfd19611de |
| mocks/managed-registry-model.mjs | bfaef2dcf35735476af29a2840a1e18e714ccbc50cf3318778b087a39117eab6 |
| mocks/knowledge-base/handlers.mjs | e7fa15ce533690bea5d5a0c506012fa4cf06ca3b3da62e5b09c10b770b2fc497 |
| mocks/ab-testing/handlers.mjs | 93f4ab0853c27c2084cb8b6a655665db324074488e04ce86fc5822572c5d25cf |
| mocks/contract-documents.test.mjs | 9db62cc6418b5fe713a78ee3b927e7d8a8bbe7cebe239fe8edf180a717c9582c |
| docs/api/contracts/openapi.json | c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7 |

Current API report hash differs from its original review's listed target hash; D-066 explicitly records parent locator-only cleanup and preserved originals. This unit uses current saved bytes, does not claim a fresh independent acceptance of revised artifacts.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Connected POST/PUT/GET path and actual managed assertions inspected; bounded nested/label evidence joins, exact read coverage and hashes recorded."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/75dfce2b-1e10-4111-9fea-8a150a50fdfc/IMPL-G2-FEEDBACK-SURVEY-MOCK.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"find/read/scoped rg; nl/sed; Python read-only JSON extraction and SHA-256","result":"passed","summary":"Actual mock composition, schemas, test assertions and documentary joins inspected."},
    {"command":"git rev-parse HEAD; git diff --cached --name-only","result":"passed","summary":"Expected HEAD; staged-file list empty."},
    {"command":"tests/build/typegen/network/browser/business calls","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Generic nested replacement/ID generation and root omission preservation present.","Label canonicalization/business limits and nested business validation absent on inspected connected save path.","Existing managed tests do not assert nested identity/order or label persistence scenarios; no tests executed."],
  "residualRisks": ["Q1 remains unapproved; observed mock permissiveness is not policy.","Static analysis only; no runtime or deployment evidence and no UI audit.","Test search bounded to mocks root test files and connected helper; no repository-wide absence claim.","Precise backend Unicode and nested-ID error policy remain unspecified by accepted evidence."],
  "noStagedFiles": true,
  "diffSummary": "Configured external report only; no project writes or staging.",
  "reviewFindings": ["Scenario fidelity gaps: label parsing/canonicalization/limits, question type-option/reference validation, targeted assertions.","Parent and independent review own acceptance; no feature checkbox closure."],
  "manualNotes": "Full common contract read. Neighbor saved-filter/delete/display-rule code incidental only. No policy choice, credentials/role-enforcement proposal, nested agents or prohibited execution. Hashing is not whole-file semantic coverage."
}
```
