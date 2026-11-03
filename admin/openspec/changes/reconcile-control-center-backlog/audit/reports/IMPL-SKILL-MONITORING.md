# IMPL-SKILL-MONITORING — MOS-1025

## Result
Mounted implementation provides an explicit monitoring-unavailable explanation, not per-skill health, probes, measurements or monitoring configuration. Existing MOS-1025 tasks remain open; no new backlog item or checkbox completion is warranted. Necessary implementation-plan correction: **no-op**. Retain the already accepted documentary enrichment from MOS1397-C01/C05–C08/C10–C14 and SME-01–03/06 without adopting their proposed/example endpoints. These findings do not activate writes, establish current API publication absence or attest deployment.

HEAD verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches assignment). Full owner proposal/design/spec/tasks read. Accepted scenario/review evidence reused, not re-extracted from primary publications. MOS-1146 and MOS-1398 establish excluded incident/responsible ownership in MOS-1026; their review corrections remain applicable, without importing those scenarios into MOS-1025.

## Mounted evidence → task/gate

Paths below are repository-relative.

| Scenario | Mounted UI | API/mock | Written assertions (not executed) | MOS-1025 disposition |
|---|---|---|---|---|
| Direct skill read and unavailable monitoring | `app/routes/skill-details.tsx:1–5` → `app/pages/skill-details/ui/skill-details-page.tsx:1–5` → `app/widgets/skill-details/ui/skill-details.tsx:12–55`; `ui/tabs/overview-tab.tsx:19–26` displays “Мониторинг недоступен: API ещё не подключён” alongside questionnaire | `app/entities/skill/model/use-skill-details-query.ts:7–22` reads detail; `api/skill-details-client.ts:getSkillDetails` calls `/skills/v1/skills/{id}` with detail schema. `mocks/domains-skills.mjs:264–268` returns stored skill or 404 | `app/widgets/skill-details/ui/skill-details.test.tsx:148–203` asserts visible unavailable text and questionnaire, tab navigation and exactly one GET to detail | Preserves truthful baseline. Does not satisfy 1.1/1.2/2.1 or close MOS-1025 |
| Status versus health/checks | `ui/skill-details-header.tsx:19–20` renders lifecycle status/version; `ui/tabs/checks-tab.tsx:13–20` explicitly says server stage is not check results, current phrase processing or sandbox readiness. `ui/skill-details-tabs.tsx:13–41` mounts overview, phrases, checks, connection, history—not monitoring metrics | Detail schema validates status/training/autotest metadata, not a monitoring response. Query polling is conditional lifecycle-status polling, not a health probe | `skill-details.test.tsx:80–125` checks status refetch, absence of progress/success claims and invalid detail status; `skill-details-client.test.ts:176–210` preserves training/autotest metadata and rejects invalid status | 2.1/3.1 open. Lifecycle/status labels are not availability, quality or threshold evaluation |
| Freshness | Header `:31` formats `skill.updated_at` under “Обновлён”; overview supplies no external-data timestamp or invocation date | Detail schema has created_at/updated_at, not a dedicated monitoring freshness model | `skill-details-client.test.ts:223–239` accepts offset updated_at and rejects invalid timestamps; these are questionnaire DTO assertions, not stale-data monitoring assertions | 2.2 open. No evidence of substitution into a monitoring timestamp because no such display is mounted |
| Thresholds, insufficient sample, null/zero, independent failure/retry | Overview is static unavailable copy, not server not-connected/no-data/maintenance/evaluated. No metric values, threshold comparison, monitoring loading/error/retry or period labels in mounted monitoring surface | No dedicated monitoring query/schema found in bounded skill owners; detail error/refetch is not an independent monitoring request | Existing unsupported-section test covers baseline only. No matching monitoring threshold/sample/freshness assertions found in bounded owners | 1.2, 2.1–2.3, 3.1 remain planned, gated by 1.1; missing planned work is not a new defect/backlog item |
| Configuration boundary | `ui/tabs/connection-tab.tsx:10–49` mounts skill service connection settings and parameters. `app/entities/skill/api/skill-connection-schema.ts:5–27` declares endpoint, contract version, auth fields and parameters—not thresholds/windows/monitoring refresh | Existing detail update endpoint is not evidence of a monitoring writer | `skill-details.test.tsx:187–190` checks “Подключение не настроено” and connection setup action, not monitoring configuration | No mounted MOS-1025 monitoring settings found. Preserve explicit read-only scope and conditional PUT/refresh gates; operational settings audit excluded |

`app/entities/skill/api/skill-details-client.test.ts:212–221,263–280` additionally asserts direct detail URL/cancellation and preserved 404. These do not verify per-skill monitoring transport. The route assertion is `app/routes.test.ts:44`.

## Bounded absence and limits

Enumerated files under `app/widgets/skill-details`, `app/pages/skill-details`, `app/entities/skill`; inspected the mounted route/page/widget/overview/checks/connection/header, detail query/schema/type and connected detail mock handler. Searches in those owners plus `mocks/{domains-skills,skill-operations,skill-catalogs}.mjs` and `mocks/{skills-status-analytics,skill-contract-delta}.test.mjs` for `monitor|health|probe|dataUpdatedAt|lastCallAt|observed_at|evaluation_status|threshold_` returned no matches (the English monitoring term is not used in the Russian static copy). Separate `monitor|health|probe|check|Монитор|монитор` scan of the three app owners located the unavailable copy, its assertion and lifecycle/check references. File enumeration and complete mounted tab/overview reads support absence of a mounted metric/configuration block in this seam—not universal repository/backend absence.

No current OpenAPI recensus performed. Prior accepted API-r1 absence findings are historical; the documentary example explicitly leaves current API-r2 unverified. Dashboard contracts, fixtures or aggregates were not substituted. No monitoring DTO, endpoint, credential behavior, new health policy or client calculator adopted. Documentary fractions versus backend-requested percentages, separate timestamp meanings, sample/null semantics and conditional writes remain unresolved under existing task 1.1.

No tests, build, typecheck, lint, formatting, API generation, network/browser, credentials, nested agents or project writes. Task 3.2 checks were intentionally not run. Deployment and runtime behavior remain unverified. `git diff --cached --name-only` returned empty; this attests observed index state only, not a clean working tree. Only this external report was written.

## Input SHA-256 (full files)

Owner prefix `openspec/changes/mos-1025-skill-monitoring/`:

| File | SHA-256 |
|---|---|
| proposal.md | `1056c3c2d4d63e86828856b43113d8d121e42275c77ee2c6fbb10daf8de5ef37` |
| design.md | `705131c4ba33d553c2dbae6edb90afea8da28208bb50398a09e602175ce24c81` |
| tasks.md | `069e9a4f274aa0355b063502338bdf90a04e6d10639d012feaa97f2b4745c9c1` |
| specs/skill-monitoring/spec.md | `07d874d8fe439797c8a0b7d0efe6db455f970a73f4fd574929ba0426b631cdee` |

Accepted input prefix `openspec/changes/reconcile-control-center-backlog/audit/`:

| File | SHA-256 |
|---|---|
| reports/SCENARIO-MOS-1146.md | `f963a783787bd3394da10ba6ee96a7e07f024279873fb150140264fd5743c3f4` |
| reports/SCENARIO-MOS-1397.md | `ac69f23cba0bd2a2bf906a529342d2b756ae7fa5e4d80aaf7a7896b1c914a2c1` |
| reports/SCENARIO-MOS-1398.md | `8065fad2f964bbf4edc6dc86cbf397a8d038bbfc697be687a18e1e1310236175` |
| reports/DELTA-SKILL-MONITORING-EXAMPLE.md | `6e5b97a8fdf7708116894db60d64e4c78cdc83b9b33e44f8b2b014443de86fcb` |
| reviews/R-SCENARIO-MOS-1146.md | `551b481b45c3986388c5f8bcbbc9fcca0932326a2d9083b9ab348c932ee776d5` |
| reviews/R-SCENARIO-MOS-1397.md | `54831f61478ee162f591a2e5977ff5f04cf92f11297312b9a0459cd1d00f346c` |
| reviews/R-SCENARIO-MOS-1398.md | `aef769ed5e5e958fc6971f0aba8ab9d75dacbf012048f1427a7cfedca7591112` |
| reviews/R-DELTA-SKILL-EXAMPLES.md | `fb377325d346a290b2b86e5f05957b38feb4499f739cadc2b36e826f710b2d44` |

Hashes verify local input identity, not external freshness. Independent package review and parent acceptance remain required.
