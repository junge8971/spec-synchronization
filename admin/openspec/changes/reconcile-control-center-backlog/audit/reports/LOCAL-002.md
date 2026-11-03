# Code Context

LOCAL-002 — local source-routing inventory only. Paths are repository-relative. No scenario completeness assessment or backend verification was performed.

## Files Retrieved

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/LOCAL-002.md` (lines 1–8) and `audit/README.md` under the same change (lines 1–25): authority, scope and evidence constraints. Work-item records HEAD `bc0d9800f25a90989b9c73c76f91996f8300f1d3`; checkout identity was not independently checked.
2. `docs/api/contracts/README.md` (lines 1–35): current provenance, normalization and section routing.
3. `package.json` (lines 1–21), `scripts/test.sh` (lines 1–8), `vitest.config.ts` (lines 1–21), `playwright.config.ts` (lines 1–24): commands and test selection, inspected only.
4. `app/routes.ts` (lines 1–15), `app/application/constants/application-routes.constants.ts` (lines 1–6), `app/shared/config/application-routes.ts` (lines 1–94), `app/shared/config/constants/application-routes.constants.ts` (lines 1–144): route composition and business entry modules.
5. `app/optional/knowledge-base/index.ts` and `app/optional/ab-testing/index.ts` (lines 1–2 each): descriptor-only public entry points.
6. `mocks/README.md` (lines 1–100; remainder not read), `mocks/app.mjs` (lines 1–127): mock documentation and actual assembly entry.
7. `app/routes/dashboard.tsx`, `app/routes/reports.tsx`, `app/routes/sandbox.tsx` (lines 1–5 each), `app/pages/operations/ui/operations-page.tsx` (lines 1–29): direct routing caveats.

Directory/path inventories were obtained with scoped `find`/`ls`; one read-only Python traversal counted files/directories. Listed paths below are discovery evidence, not a claim that every file's content was read.

## API document inventory and provenance

`docs/api/contracts/` has **33 files: 18 Markdown, 13 JSON, 2 raw snapshots**.

- Markdown: `README.md`, `access-session.md`, `analytics-dashboard.md`, `assistant-modules.md`, `assistant-operations.md`, `audit.md`, `contract-audit.md`, `crud-api.md`, `delta-2026-10-13.md`, `delta-2026-10-15.md`, `dialog-export.md`, `dialogs.md`, `managed-resources.md`, `reports.md`, `skills-domains.md`, `surface-error-provenance.md`, `surfaces.md`, `teams.md`, `users.md`.

**Correction to the list/count interpretation:** `audit.md` is linked by README but was **not present in the directory inventory**. Excluding that linked-only name yields the measured 18 Markdown files. Treat the audit link as an unresolved source path, not evidence of an audit API document.

- JSON: `openapi.json`, `access-session.openapi.json`, `analytics-dashboard.openapi.json`, `assistant-modules.openapi.json`, `assistant-operations.openapi.json`, `dialogs.openapi.json`, `managed-resources.openapi.json`, `mpmm-auth.openapi.json`, `skill-incidents-internal.openapi.json`, `skills-domains.openapi.json`, `surfaces.openapi.json`, `teams.openapi.json`, `users.openapi.json`.
- Raw: `openapi-2026-10-15.raw`, `crud-api-2026-10-15.raw`.

README attributes aggregate OpenAPI 3.1.0, service version 0.1.0, to `https://nchat-a-tech.mos.ru/api/control/docs`, retrieved **15.10.2026**, source-byte SHA-256 `2f3c48d3542e4486f7c1a501c4a1a4a0b813c662af26079a1e98c9f09d6ea26d`. It states **94 paths / 128 operations / 380 schemas**, with security normalized from live OR to agreed AND (`X-Access-Token` + `X-Admin-Token`). Split contracts are described as aggregate operations with closed schema sets; gateway refresh is separate in `mpmm-auth.openapi.json`. `contract-audit.md` is explicitly historical; `crud-api.md` supplements DTOs. These are README assertions, not newly calculated counts/hash or live validation. README explicitly separates publication from backend availability and PUT deployment gates.

## Key Code and analyst entry paths

Route assembly is `applicationRoutes = [...baseRoutes, ...knowledgeBaseRoutes, ...abTestingRoutes]`; `app/routes.ts` maps descriptors to React Router entrypoints and appends compatible routes. Start with the descriptor registry, not navigation labels alone.

| Scenario family | UI/source entry paths | API/mock entry paths |
|---|---|---|
| Skills/domains | `app/routes/skills.tsx`, `skill-creation.tsx`, `skill-details.tsx`; `app/pages/{skills,skill-creation,skill-details}/index.ts`; `app/widgets/{skills-registry,skill-domains-registry,skill-details,skill-review}/index.ts` | `app/entities/skill/api/`, `app/entities/skill-domain/api/skill-domain-client.ts`; `mocks/domains-skills.mjs`, `skill-operations.mjs`, `skill-catalogs.mjs` |
| Surfaces | `app/routes/{surfaces,surface-registration,surface-details}.tsx`; `app/pages/{surfaces,surface-registration,surface-details}/index.ts`; matching `app/widgets/` roots | `app/entities/surface/api/surface-registry-client.ts`; `mocks/surfaces.mjs` |
| Dialogs | `app/routes/{dialogs,dialog-details}.tsx`; `app/pages/{dialogs,dialog-details}/index.ts`; `app/features/{dialog-category-addition,dialog-export,dialog-saved-filters,dialog-selection}/index.ts` | `app/entities/dialog/api/{dialog-client,dialog-detail-client,dialog-category-client,dialog-export-client}.ts`; `mocks/{dialogs,dialog-details,dialog-categories,dialog-fixtures}.mjs`, `dialog-export-files.json` |
| Teams/users | `app/routes/teams.tsx`, `app/pages/teams/index.ts` | `app/entities/team/api/team-client.ts`, `app/entities/business-user/api/business-users-client.ts`; `mocks/{teams,users}.mjs` |
| Session/local demo | `app/entities/session/index.ts`, `app/entities/session/api/current-principal.ts`; `app/application/{model,ui}/`, `app/shared/auth/`, `app/shared/lib/local-demo/index.ts` | `app/shared/api/{http-client,session-transport}.ts`; `mocks/{session-demo,response-scenarios}.mjs`; read agreed auth/demo change specs before semantic analysis |
| Knowledge base (optional) | `app/optional/knowledge-base/index.ts`, `constants/descriptor.constants.ts`, `routes/{registry,creation,details}.tsx` within that root | `app/optional/knowledge-base/api/{knowledge-base-client,knowledge-base-directory-client,knowledge-base-export-client}.ts`; `mocks/knowledge-base/{handlers,model,seed,validation}.mjs` |
| A/B testing (optional) | `app/optional/ab-testing/index.ts`, `constants/descriptor.constants.ts`, `routes/{registry,creation,details}.tsx` within that root | `app/optional/ab-testing/api/{ab-testing-client,ab-testing-export-client,ab-testing-saved-filter-client,ab-testing-users-client}.ts`; `mocks/ab-testing/{handlers,model,seed,validation}.mjs` |
| Analytics/reports/sandbox | `app/routes/{dashboard,reports,sandbox}.tsx` currently directly render `PlaceholderPage` | `mocks/analytics.mjs`; route presence or mock presence must not be read as UI implementation |
| Operations/assistant management | `app/routes/operations.tsx`, `app/pages/operations/ui/operations-page.tsx` (tabs render “Раздел в разработке”) | `mocks/{assistant-modules,maintenance,stubs}.mjs`; route from `assistant-modules.md`, `assistant-operations.md` before assigning finer scenarios |
| Other managed resources | Start with `docs/api/contracts/managed-resources.md`, rather than assume dedicated UI slices | `mocks/{managed-resources,managed-registry-handlers,managed-catalogs,api-endpoints,response-templates}.mjs` |
| Home/documentation | `app/routes/{home,documentation}.tsx`; `app/pages/{home,documentation}/index.ts`; `app/entities/documentation/index.ts` | Local documentation ownership should not be conflated with a backend article API |

## Architecture and root inventory

- `app/entities/`: **8** roots — `business-user`, `dialog`, `documentation`, `session`, `skill`, `skill-domain`, `surface`, `team`.
- `app/pages/`: **13** roots — `dialog-details`, `dialogs`, `documentation`, `home`, `operations`, `placeholder`, `skill-creation`, `skill-details`, `skills`, `surface-details`, `surface-registration`, `surfaces`, `teams`.
- `app/features/`: **19** roots — `dialog-category-addition`, `dialog-export`, `dialog-saved-filters`, `dialog-selection`, `skill-bulk-rollout`, `skill-connection-settings`, `skill-domain-editing`, `skill-editing`, `skill-global-toggle`, `skill-lifecycle`, `skill-registration`, `skill-registry-filter`, `skill-registry-pagination`, `skill-review`, `skill-training-phrases`, `surface-registration`, `surface-registry-filter`, `surface-registry-pagination`, `surface-skill-selection`.
- `app/widgets/`: **11** roots — `breadcrumbs`, `documentation`, `header`, `navigation`, `skill-details`, `skill-domains-registry`, `skill-review`, `skills-registry`, `surface-details`, `surface-registration`, `surfaces-registry`.
- `app/optional/`: **2** isolated modules — `knowledge-base`, `ab-testing`; app composition resides in `app/application/`, including `knowledge-base-integration.md` and `ab-testing-integration.md`.
- Shared transport/generated contract: `app/shared/api/http-client.ts`, `session-transport.ts`, `schema.d.ts`; generator `scripts/generate-api-types.mjs`. No generation was run.
- `mocks/app.mjs:createMockApp` assembles handlers, iterates OpenAPI operations by `operationId`, attaches validation/scenario/idempotency middleware and mounts `/api`. `mocks/contract.mjs`, `state.mjs`, `seed.json`, `vite-plugin.mjs` are supporting inspection entrypoints. README distinguishes demo session from credential-free business mocks; documented mock counts were not runtime-verified.
- Respect FSD public `index.ts` boundaries and optional-module isolation when later planning changes. This inventory proposes no changes.

## Tests and package check scripts

Filename counts, not test-case or passing-coverage counts:

- **162** `*.test.ts(x)` files under `app/`, co-located across entities/features/widgets/pages/shared/application/providers/routes. Includes **15** in `app/optional/knowledge-base/` and **17** in `app/optional/ab-testing/`.
- **36** `*.test.mjs` under `mocks/`: **30** at root and **3** per optional module (`aggregate.test.mjs`, `saved-filter-interoperability.test.mjs`, `search-export.test.mjs`). Representative routing anchors: `mocks/contract.test.mjs`, `contract-documents.test.mjs`, `auth-contract.test.mjs`, `dialog-scenarios.test.mjs`, `managed-resources.test.mjs`.
- **2** script tests: `scripts/serve-spa.test.mjs`, `scripts/eslint-fsd-config.test.mjs`.
- **4** browser spec files inventoried only: `e2e/{control-center-shell,home,surface-registration,surface-registry}.spec.ts`; helper `e2e/support/mock-control-api.ts`. No browser test content was analyzed or executed.
- Vitest selects `app/**/*.test.{ts,tsx}`, jsdom, setup `app/test/setup.ts`; `scripts/test.sh` runs Vitest then serialized Node tests from mocks (including optional roots) and the two script tests.

| Package command | Definition / routing significance |
|---|---|
| `yarn typecheck` | `react-router typegen && tsc` — includes generation; prohibited in this run |
| `yarn lint` | `eslint . --max-warnings 0` |
| `yarn format:check` | `prettier --check .` |
| `yarn test` | `sh scripts/test.sh` |
| `yarn api:check` | `node scripts/generate-api-types.mjs --check` |
| `yarn api:generate` | `node scripts/generate-api-types.mjs` — mutating generator |
| `yarn build` | `react-router build` |
| `yarn test:e2e` | `playwright test` — forbidden here; config would build and start a web server |

Other script entrypoints discovered: `scripts/{knowledge-base,ab-testing}-{build-graph,verify}.mjs`; these are not named package scripts. No listed check, build, server, generator or test was run.

## Start Here

Open `app/shared/config/constants/application-routes.constants.ts` first for base scenario-to-route assignment, then `app/application/constants/application-routes.constants.ts` for optional composition. Pair each assigned scenario with its specific contract Markdown and the API/test paths above.

## Limitations

Local filenames and selected source excerpts only. No network/MCP, live API, browser, tests, typegen, dependency commands, git mutations or nested agents. No source/spec edits; only this authorized report artifact was written. Contract bodies, snapshots and hashes were not semantically audited. README operation totals and dates remain attributed claims. No claim of complete business coverage, backend availability, permissions correctness, test success or implementation completeness. Missing linked `docs/api/contracts/audit.md` is a routing limitation, not a missing required inventory input; all required inputs were available. No infrastructure failure occurred.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Inventoried contract filenames/provenance, business and optional entry roots, mocks, test locations/counts and package checks; exclusions and limitations recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-002.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"read-only Python pathlib inventory of docs/api/contracts and app/mocks/scripts/e2e","result":"passed","summary":"33 contract files; 162 app, 36 mock, 2 script and 4 browser test files counted."}],
  "validationOutput": ["Scoped read/find/ls retrievals succeeded; no validation or tests executed."],
  "residualRisks": ["README links audit.md, which was absent from the observed contract directory.","Source provenance/count claims not independently verified against live API or raw bytes.","Inventory does not establish business completeness or passing tests."],
  "noStagedFiles": false,
  "diffSummary": "Only the authorized report was written; git status/staging was not inspected (false is not a finding of staged changes).",
  "reviewFindings": ["Routing caveat: docs/api/contracts/README.md links absent audit.md; do not route an analyst to it as an available source."],
  "manualNotes": "Read-only discovery completed without infrastructure failure. No tests, generators, network calls, browser actions, source edits or git mutations were performed."
}
```
