# IMPL-SKILL-ENVIRONMENT-TOKENS

## Disposition

Read-only implementation evidence; no feature/runtime acceptance. Existing MOS-1023 tasks stay open. Token-specific card controls, operations and sandbox receiver are not present in the inspected connected implementation. Connection configuration exists, but is not token management. One necessary precision candidate strengthens the already accepted API-R2-TOKEN-04 cache warning with an actual current-code ingress path; no duplicate backlog is needed.

HEAD verified before and after inspection: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Full owning change and all four assigned accepted reports/reviews read; their hashes matched at both checks. Accepted requirements were reused, not re-extracted. No network, credentials, browser, test/build execution, project edits or delegation.

## Scenario → implementation → assertions → existing gate

Paths below are repository-relative. `O` = `openspec/changes/mos-1023-skill-environment-tokens`; `A` = `openspec/changes/reconcile-control-center-backlog/audit`.

| Scenario | Mounted UI and transport/mock evidence | Written assertions inspected (not executed) | Existing task/gate |
|---|---|---|---|
| Server metadata / explicit unissued / metadata failure | Route registry `app/shared/config/constants/application-routes.constants.ts:40–44` → `app/routes/skill-details.tsx:1–5` → `app/pages/skill-details/ui/skill-details-page.tsx:1–5` → `app/widgets/skill-details/ui/skill-details.tsx:13–16,55` → `ui/skill-details-tabs.tsx:37–38` → `ui/tabs/connection-tab.tsx:9–44`. Card renders endpoint, contract, auth-required/type and parameters, not environment cards or token state. Null connection says “Подключение не настроено” (:38), not token-unissued. Detail GET uses `app/entities/skill/api/skill-details-client.ts:89–94`; mock GET returns the stored skill in `mocks/domains-skills.mjs:264–268`. No token-specific unavailable/error/retry presentation in this subtree. | `app/widgets/skill-details/ui/skill-details.test.tsx:185–203` asserts null-connection text and only one detail GET across tabs; :228–264 asserts parameters and documentation link. These do not establish token metadata/error/unissued behavior. | O/tasks.md 1.1–1.2 (:5–6), 2.1 (:10). O/specs/skill-environment-tokens/spec.md:7–19. Generic detail request handling is not token-state acceptance. |
| Controlled disclosure / copy / rotation cancellation or lost response | `app/features/skill-connection-settings/ui/skill-connection-settings.tsx:17–54` mounts a connection form, explicitly excludes secret entry (:40–42), and uses existing session UI permissions (:29), not a business-token permission model. `app/entities/skill/api/skill-connection-schema.ts:5–22` permits connection fields and `transport_token` type, not lifecycle secret operations. No reveal/copy/reissue/revoke controls or clients found in assigned feature/entity/widget scope. | Feature `ui/skill-connection-settings.test.tsx:32–57` asserts keyboard opening, no secret-value field, Escape focus restoration, reset and cancel without fetch. Entity `api/skill-details-client.test.ts:72–104` asserts connection PUT payload/key and 409/422/invalid-response rejection. These are connection-edit tests, not cancellation or recovery of token rotation. | O/tasks.md 1.1, 2.2, 3.1 (:5,11,17); O/spec:21–33. Retain accepted RECON copy recommendations as recommendations, not implemented behavior. |
| Secret-free sandbox navigation and common token model | Connection card and its `connection-tab/connection-parameters.tsx:45–54` link only to parameter documentation; no skill-ID sandbox link. Global `/sandbox` is registered at `app/shared/config/constants/application-routes.constants.ts:69–76`, but `app/routes/sandbox.tsx:1–5` renders only `PlaceholderPage`, no token reader or skill binding. `app/entities/skill/model/types/skill.types.ts:8` aliases local generated detail DTO, not a separate environment-token model. | Connection widget test :260–263 asserts `/tsam-panel/docs?article=skill-params`, not sandbox navigation. No matching token URL/shared-metadata assertions found in inspected colocated tests. Global navigation existence must not be counted as MOS-1023 integration. | O/tasks.md 2.3 (:12), spec:35–42. Preserve MOS-1019 readiness ownership and accepted surface sandbox exclusion; no activation implied. |
| Close disclosed token / skill switch / safe cache and diagnostics | No disclosed-token state exists in inspected token-owner UI; therefore there is no implemented cleanup flow to accept. More importantly, ordinary detail ingress uses `z.looseObject` in `app/entities/skill/api/skill-details-client.ts:15–51`, with no declared token sanitizer. `app/shared/api/http-client.ts:230–239` returns parsed data. `app/entities/skill/model/use-skill-details-query.ts:8–10` caches that result; `model/use-update-skill-mutation.ts:12–16` also puts returned skill into the detail cache. Unknown top-level `tokens` from a compatible newer response would be retained by loose parsing, even though the local TypeScript DTO lacks it. | Widget test :266–289 explicitly checks the saved entire detail response is in `['skills','detail',skillId]` cache (:285). It contains no r2 secret-bearing extension assertion. No token cleanup/storage/log spy assertions found within inspected feature/entity/widget test files. | O/tasks.md 1.2, 2.4 (:6,13), design:13. Extend existing API-R2-TOKEN-04 integration warning with this concrete ingress path; do not claim observed leakage or persistent storage. |

## Transport, mock and contract distinction

- Current local `docs/api/contracts/openapi.json` was inspected by schema/path names and shared skill property names only: no token-named paths or schemas, and no `tokens` property in `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/properties`. Matching search of generated `app/shared/api/schema.d.ts` found no `SkillToken`, `token_value`, token paths or `tokens:` declaration. Thus proposal's **local-file** claim remains supported; this is not a denial of r2 publication.
- Accepted `A/reports/API-R2-TOKEN-DELTA.md` and `A/reviews/R-API-R2-TOKEN-DELTA.md` remain authority for separately dated r2: reissue/revoke commands, environment enum, expected_version/idempotency inputs, nullable issuance and potentially secret-bearing ordinary `tokens[].token_value`. Publication is not agreed disclosure, replay, invalidation or deployment behavior. No remote source was reopened or requirement extraction repeated.
- Existing connection transport is ordinary skill PUT (`skill-details-client.ts:53–66`) with version/body/key; status POST (:69–86) is not token rotation. `mocks/domains-skills.mjs:324–349` updates skill fields/version and returns the skill, with PUT aliased to existing handler. Searches in this handler, `mocks/skill-operations.mjs`, `mocks/skill-catalogs.mjs`, `mocks/skill-contract-delta.test.mjs` found no token lifecycle implementation. No inference about backend availability follows.
- Business integration tokens are distinct from employee sessions. Existing `PermissionButton` and `assertResponseSession` are observed integration mechanisms only; no auth-policy or credential-transport decision is made here.

## Bounded absences and plan disposition

Absence boundary: enumerated files in `app/pages/skill-details`, `app/features/skill-connection-settings`, `app/entities/skill`; connected `app/widgets/skill-details` connection card/tabs/widget and colocated test search; route registry and sandbox entrypoint; the named skill mock handlers/tests; local generated contract and OpenAPI path/schema/property inventory. This is not a repository-wide proof that no token-related code exists, nor a live API inventory. Unread unrelated session/surface/dialog logic is outside scope. Generic errors, form cancellation and navigation do not substitute for token-specific assertions.

Necessary candidate **IMPL-1023-01**, existing owner only: attach the concrete loose-parser → whole-detail-query-cache path to API-R2-TOKEN-04 / tasks 1.2 and 2.4. Before authorized r2 integration, explicitly cover sanitization/separation of ordinary `tokens[].token_value` on detail GET and other shared-detail response ingress, not just `issued_token`; add a written synthetic-response boundary test alongside `skill-details-client.test.ts` and cache consumer tests. This is a scoped refinement of an existing accepted warning, not permission to implement operations, change session behavior or assert runtime exposure. Current implementation can retain additional fields in ordinary in-memory cache; persistence, telemetry leakage and actual secret delivery were not established.

Otherwise **no new plan correction**: keep existing tasks open, carry forward prior RECON/API-R2 candidates without republishing them as new requirements. Current token absence is evidence to fill the audit, not reason to add parallel tasks. Record that unavailable token UI itself is not explicitly rendered here; task 2.1 already owns that gap. Do not close any checkbox from generic connection tests. Tests/build and independent package review remain unperformed by this analyst.

## Input SHA256

Owner files and four accepted documents were hashed before analysis and rechecked unchanged afterward. Additional inspected contract/code hashes are end-of-inspection provenance, not a claim of before/after content verification for every code file.

| Input | SHA256 |
|---|---|
| O/.openspec.yaml | d707823457f58b4f938a99bc049bddd9b937affec2d09c976c9a16a9dcd03f77 |
| O/proposal.md | 40c764c37f0017c01cdd91d0283c5c0cc031d460dcb1d2f254833e84b648bc3a |
| O/design.md | d2944e6cf270a88f90ddfb57d0d69669e28620942ee86fceff681bda0e9c04c8 |
| O/tasks.md | 8da3635da6e0aa46ea45b20f321b44ecce816c6dcaeec568856b011df1492c75 |
| O/specs/skill-environment-tokens/spec.md | 130aa7f19daa88428808af5ccd717482308318029a30764ecedc7985ac760ace |
| A/reports/REQ-MOS-1023.md | c525a9b6d131140b0a6cfbe491a887943b4cd82ea2cabc935e05f9f2aa8d4ae6 |
| A/reviews/RECON-MOS-1023.md | 6aefdd171f01fae161f7f265bb78025267d935d810dbf8fac11b7aed08d3a291 |
| A/reports/API-R2-TOKEN-DELTA.md | 3172e52910a665cd02fbf03a72fb1f224a9dfe99530fc67351552d394295e932 |
| A/reviews/R-API-R2-TOKEN-DELTA.md | 06f6c2decd547f691edb22565b1ef314f94f0e8ccaf6693223bae2f0a39c70da |
| A/work-items/G2-SKILL-IMPLEMENTATION-BATCH.md | e8237f43cfd87e1a39b1e717deb2dfaa6ccb0fdc05e459ffbcfda3891fd4581a |
| docs/api/contracts/openapi.json | c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7 |
| app/entities/skill/api/skill-details-client.ts | de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6 |
| app/entities/skill/model/use-skill-details-query.ts | 88db0ee56655ee10d1dbd6df477679ecaedb838181d8339478214d39a16e1bbe |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped mounted connection UI, detail transport/mock, sandbox placeholder and written assertions to existing MOS-1023 tasks; bounded absence and concrete cache-ingress refinement recorded."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/d10d3bb3-05f1-4405-859e-1a42d0ade96a/impl-skill-environment-tokens.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD; sha256sum assigned owner and accepted evidence","result":"passed","summary":"Expected HEAD verified twice; owner and accepted evidence hashes unchanged."},
    {"command":"Local find/rg/read and Python OpenAPI path/schema/property-name inventory","result":"passed","summary":"Inspected connected implementation and written tests without executing project code or disclosing values."},
    {"command":"Tests/build/typegen/browser/network","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["No token-specific UI/client/mock or sandbox receiver found within stated boundary; ordinary loose detail parsing can retain additional token fields in query cache."],
  "residualRisks": ["Actual r2 response delivery, deployment, persistence and secret leakage are unverified.","Existing disclosure, state mapping, invalidation, recovery and sandbox gates remain unresolved; independent batch review pending."],
  "diffSummary": "Only configured external report written; no project edits.",
  "reviewFindings": ["Refine existing API-R2-TOKEN-04/tasks 1.2 and 2.4 with actual loose-parser/cache ingress and synthetic boundary-test coverage; no new backlog or task closure."],
  "manualNotes": "Read-only code and written-assertion analysis, not runtime or feature acceptance. No git index-state attestation; no credentials or actual token values inspected. Parent owns publication and independent review."
}
```
