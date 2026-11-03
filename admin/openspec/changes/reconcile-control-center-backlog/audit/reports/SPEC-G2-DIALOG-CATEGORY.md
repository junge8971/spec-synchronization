# Code Context

## Result

**Baseline row12 ownership and normative semantics resolved: MOS-1044 → archived `2026-10-07-mos-1044-dialog-category-addition` → main `dialog-category-addition`. Existing local approval is explicit. No product-plan correction is justified by this analysis.** DBP-08's contrary manual-tagging exclusion remains a bounded source-applicability/precedence question, not an absent capability or an approval gate to reopen. DLC-04 remains read metadata, not mutation authority.

Parent retains acceptance. This report adds an exact OpenSpec/ownership join to D-062's historical all-U row; it does not rewrite that historically accurate index, close API/implementation lanes, or establish deployment.

## Files Retrieved

Repository-relative aliases: `C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `openspec/changes/reconcile-control-center-backlog/audit`; `O` = `openspec/changes/archive/2026-10-07-mos-1044-dialog-category-addition`; `M` = `openspec/specs/dialog-category-addition/spec.md`. Suffixes below expand literally. All reads used the read tool; fingerprints are separately computed whole-file hashes, not claims of whole-file semantic reading where ranges are partial.

| Exact path | Actual lines read | Purpose |
|---|---:|---|
| `A/work-items/G2-OWNERSHIP-WAVE.md` | 1–19, complete | Common contract and assigned section |
| `C/proposal.md` | 1–30, complete | Authority |
| `C/design.md` | 1–133, complete | Evidence precedence, publication and gates |
| `C/tasks.md` | 1–45, complete | No automatic closure |
| `C/specs/control-center-backlog-reconciliation/spec.md` | 1–108, complete | Governing process |
| `A/decisions.md` | 1–13,189–195 | D-062 and D-035 complete decisions |
| `A/reports/LOCAL-001.md` | 1–194, complete | Exact main ID/archive inventory |
| `A/reports/G2-MAIN-CAPABILITY-JOINS.md` | 1–204, complete | Row12, DB/DL chains, N11 |
| `A/reviews/R-G2-MAIN-CAPABILITY-JOINS.md` | 1–250, complete | Qualified acceptance and row12 limits |
| `A/reports/DELTA-DIALOG-BUSINESS-PLAN.md` | 1–60, complete | DBP-08 and scope limits |
| `A/reports/DELTA-DIALOG-LIST-CARD-EXAMPLES.md` | 1–128, complete | DLC-04 and read/mutation distinction |
| `A/reviews/R-DELTA-DIALOG-SUPPLEMENTS.md` | 1–84, complete | Accepted documentary comparisons only |
| `A/reports/JIRA-MOS-773.md` | 1–35 | Accepted membership reference, MOS1044 row27 |
| `M` | 1–58, complete | All four requirements/seven scenarios |
| `O/proposal.md` | 1–28, complete | Explicit MOS1044 identity, scope, approval |
| `O/design.md` | 1–28, complete | Gate closure, architecture and exclusions |
| `O/tasks.md` | 1–15, complete | Exact historical task mapping |
| `O/specs/dialog-category-addition/spec.md` | 1–56, complete | Originating full delta |
| `openspec/specs/dialog-details/spec.md` | 1–40 | Read snapshot/category display owner |
| `A/sources/wiki-241080071-readable/r1/content.txt` | 1–81, complete | Actual brief exclusion and phases |
| `A/sources/wiki-241083649-readable/r1/content.txt` | 159–178 | Actual category read table |
| `A/sources/wiki-245670575-readable/r1/content.txt` | 79–88 | Documentary MOS1044 listing |
| `A/sources/wiki-241080071/r1/metadata.json` | 1–21, complete | Wiki v2, retrieved 2026-10-19T10:35:02.088Z |
| `A/sources/wiki-241083649/r1/metadata.json` | 1–21, complete | Wiki v2, retrieved 2026-10-19T10:35:01.839Z |

No original PDF/HTML, remote pages, raw wiki envelopes, exact markup chunks, API schema or application code were inspected. Prior supplement reviewers read exact markup; that verification is attributed to their accepted reports, not repeated here. No new source discovery was performed: archive and saved sources were reached through supplied inventory/report references.

## Key Code — normative contract, not implementation

### Exact identity and approval

- `O/proposal.md:3,16,24–28` explicitly identifies MOS-1044, this capability, MOS1041 card composition, MOS1037 dictionary reuse and the accepted write contract. `O/design.md:13` explicitly records user acceptance of PDF §3.6 and §8.16/8.24/8.30, ESK write, idempotency, concurrent preservation and backend audit. It explicitly distinguishes approval from deployed ESK availability.
- `A/reports/JIRA-MOS-773.md:27` supplies existing accepted membership pointers: hierarchy `$.results[8].children[8]`, member index `$.items[53]`. Its Ready-for-test status is historical index-only evidence, not acceptance of requirements or implementation. The decomposition's line87 names MOS1044 but adds no mutation semantics.
- Main and originating delta have the same four requirement bodies and seven scenarios (main line numbers are delta +2). Archive tasks are checked historical records; this run neither validates those receipts nor changes their state.

| Requirement and all named scenarios | Main / originating delta | Exact owner tasks and decisions | Preserved contract |
|---|---|---|---|
| Category action requires an accepted write contract; Write API unavailable | `M:9–16`; `O/specs/dialog-category-addition/spec.md:7–14` | `O/tasks.md:3–4` tasks1.1/1.2; `O/design.md:13` | After accepted gate: POST `/api/control/api/dialogs/v1/dialogs/{chat_id}/categories`, only `{ name }`; dictionaries.categories. No guessed endpoint, category_id, expected_version, new permissions or client audit. Gate condition is satisfied in the local planning record, not proof of runtime availability. |
| Form selects one dictionary category; Dictionary no longer contains an existing category; Unknown category rejected | `M:18–30`; delta16–28 | `O/tasks.md:8–9,11` tasks2.1/2.2/2.4; design15,18 | One dictionary name, trim/case-insensitive membership; no free creation/removal/set replacement. Preserve historical categories; distinguish empty/error; keyboard accessibility; 422 /name retains selection and prior state. |
| Success replaces categories with the server result; Repeated addition; Concurrent additions; Stale detail response | `M:32–49`; delta30–47 | `O/tasks.md:8,10` tasks2.1/2.3; design16–17 | Success only HTTP200 full categories; no duplicate/double-submit, stale chat_id or old detail overwrite; no whole-card refetch. Replacing the displayed field with a server snapshot is not a replace-set write operation. |
| Write failures preserve state and allow explicit retry; Network or source failure | `M:51–58`; delta49–56 | `O/tasks.md:11` task2.4; design18 | Preserve categories/input; meaningful 503,404,401/403 business failures; explicit retry after uncertain network failure, no endless replay or feature-owned auth. |

`O/tasks.md:15` task3.1 historically calls for typecheck/lint/test/format/API checks and independent addition without MOS1042/1043/1045. These are historical acceptance instructions/checkboxes, not fresh successful executions. No further backend or employee-auth policy is inferred.

### SPEC-G2-DC-01 — positive mutation scope, not nonexistent capability

The new exact mapping corrects only the former knowledge gap: DBP-08 explicitly had not read this capability. Now its approved operation is known: an employee selects one existing dictionary category and confirms a persisted addition. The exclusions of free-form category creation, deletion and whole-set replacement do **not** turn that operation into read-only behavior. The original DBP report and D-035 remain correct about their own limited inspection; no retrospective report correction is needed.

### SPEC-G2-DC-02 — genuine opposing statements; no evidenced phase resolution

The actual saved brief `A/sources/wiki-241080071-readable/r1/content.txt:57–62` says COULD automatic ML topics/categories, then WON'T editing and “Ручная разметка диалогов (только просмотр и экспорт).” Its lines71–74 distinguish November MVP, December additions and 2027 automatic ML/Writer/XLSX; none explicitly allocates manual dictionary category addition to a later phase. `O/proposal.md:3–9,27` and `O/design.md:13–18` explicitly approve exactly such user-driven persisted category addition.

These are substantively opposing scope statements if applied to the same product stage. No inspected artifact explicitly relates or supersedes the brief's WON'T clause, defines “manual tagging” to exclude dictionary assignment, or provides a temporal/dependency reconciliation. The archive's “new PDF” reference and later date are not that missing linkage. The closed write-contract gate resolves integration approval, not the brief's applicability. Conversely the brief does not revoke recorded local approval.

**Disposition: bounded unresolved applicability/precedence question, no plan edit.** Question for parent/product disposition: *What is the applicability of the brief's manual-tagging WON'T clause to the explicitly approved MOS1044 dictionary-addition scope—does an accepted exception/supersession or distinct stage exist?* Do not reopen local approval or disable/revert the feature while that documentary linkage is unresolved.

Parent was contacted through the decision channel after this conflict was established. Parent replied that no separately verified reconciliation decision could be supplied; instructed retaining the bounded question, positively mapping all four requirements, preserving the archived user approval as existing approved local scope, and making no plan edits or source collection. Parent explicitly limited the blocker to a change relying on reconciliation, not ownership mapping or independent evidence lanes. This is an analytical disposition, not a newly invented product precedence decision.

### SPEC-G2-DC-03 — read metadata is compatible, not mutation authorization

DLC-04 is supported by actual `A/sources/wiki-241083649-readable/r1/content.txt:169–175`: categories expose id/dialogId/name/assignedBy operator|auto/assignedAt. That table says what is returned, not who may mutate through this UI or how. It neither proves a contradiction with view-only scope nor grants a write permission. `openspec/specs/dialog-details/spec.md:23–25` already requires category display from the snapshot. Existing historical categories remain visible even when unavailable in the dictionary (`M:20–25`). Do not adopt the historical read IDs as write category_id or infer a new audit API from assignedBy/assignedAt.

## Architecture

Normative dependency flow: MOS1037 shared dictionary client → MOS1044 feature via public entities/dialog API → MOS1041 card receives full returned category snapshot. `O/design.md:14–17` assigns feature mutation and card-result ownership while forbidding page imports, duplicate dictionary clients, local fabricated persistence and stale cache overwrite. Backend owns persistence, concurrent set semantics and audit; client owns truthful form/error/cache behavior. This is planned architecture, not inspected runtime.

Coverage disposition for row12 after parent acceptance: **R partial** (exact local approved requirement plus unreconciled contrary brief); **S exact four-requirement/seven-scenario ownership mapping** (not whole capability delivery); **A applicable but independently unexamined** (write/read dictionaries/result/error contract needs real evidence, not an N/A label); **I applicable but independently unexamined** (form, mutation/cache and errors); **X partial/question** (read-versus-write distinction resolved, source applicability unresolved). API contracts and runtime absence cannot be inferred from this report.

## Start Here

Open `openspec/changes/archive/2026-10-07-mos-1044-dialog-category-addition/design.md:13–18`, then `openspec/specs/dialog-category-addition/spec.md:9–58` and DC-02 above. Retain the current main spec/archive unchanged. The concrete deliverable is this positive ownership/requirement/task join and narrowly bounded question—not a request for a new audit wave.

## Actual input fingerprints

SHA-256 computed locally over current complete file bytes. These fingerprints do not establish historical integrity, wiki roundtrip, remote freshness or runtime acceptance. Paths expand using the exact aliases above. Partial read ranges remain partial despite whole-file hashing.

| Path | SHA-256 |
|---|---|
| `C/proposal.md` | `1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879` |
| `C/design.md` | `632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828` |
| `C/tasks.md` | `a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83` |
| `C/specs/control-center-backlog-reconciliation/spec.md` | `a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36` |
| `A/work-items/G2-OWNERSHIP-WAVE.md` | `9dd958ad5d13a2bca16b60a66c02d73431b1aad5edae3a8e368bea689e1987e3` |
| `A/decisions.md` | `0b875b2a5504480e29a0c99671614d1e65bbfc7d4173e3e3496a5dea89999798` |
| `A/reports/LOCAL-001.md` | `0ab83e87351849500a625c2d7efea2b3142d5b1b473924dc2160e03f511e010d` |
| `A/reports/G2-MAIN-CAPABILITY-JOINS.md` | `58912cbe79aeaa7b72273215dc84f26c9a1fcd86366de04b189893ec87f036b0` |
| `A/reviews/R-G2-MAIN-CAPABILITY-JOINS.md` | `2f11435ee6da92bab528ae413704e6fd2a7c6481405c86c3373ad760b58cdb95` |
| `A/reports/DELTA-DIALOG-BUSINESS-PLAN.md` | `4b198ead456ab37b65f99c08511f1f9bfe2f677c0b40189c91870ee6433b2bcd` |
| `A/reports/DELTA-DIALOG-LIST-CARD-EXAMPLES.md` | `8901ff894ee25d02ba11620fb30a03fc8078a25e51e0817ae5f7e11c79e6b442` |
| `A/reviews/R-DELTA-DIALOG-SUPPLEMENTS.md` | `492369378811af9aae798173419506eea0010bb9b27647b7967f3aad4bfa7fc6` |
| `A/reports/JIRA-MOS-773.md` | `26b57e113f042ad274fa051a8df20039d723cccd7827089aac4813804181c8b5` |
| `M` | `cba0585a946e649233f28d0e3775f32dfb36cbddc80277ab9ac2c56d04819e93` |
| `openspec/specs/dialog-details/spec.md` | `25fa6ea2bb92bbcd37ac24d6fb668b6756e7be04dd36d3e23b2abb399d666334` |
| `O/proposal.md` | `04a2d4b05690342b9e4155024f138ea86002a700ffb05ab050667df5508eb476` |
| `O/design.md` | `3ba354a2649c21c1cfdfcf138ac93730fe3c0bf000a5587e54500a4ea0db33b5` |
| `O/tasks.md` | `47af85325e78563f1426cc357079c51882cf5221aa5af1f1bc659ab26878472f` |
| `O/specs/dialog-category-addition/spec.md` | `60fc6e51a2679cee44aaee5df5d3136c972202d144c99b89e87f9d20df62964b` |
| `A/sources/wiki-241080071-readable/r1/content.txt` | `0a4f008f6884a7a1fa8725b374d5c0b945ecc6b8c393bdc6d85341d036eb6a3b` |
| `A/sources/wiki-241083649-readable/r1/content.txt` | `1146d1c063c9ac6a1b751ff2b71e15914443b388eb2fd819ac59aa44501244de` |
| `A/sources/wiki-245670575-readable/r1/content.txt` | `9db02038e89e03e19982b9c034e4aeeca3590f444bf4ae5c00ddb26159382468` |
| `A/sources/wiki-241080071/r1/metadata.json` | `5430c68e13444c739a1d48ebb89dbaae0f3cc7a1cd1c3817fbafe5488e82c570` |
| `A/sources/wiki-241083649/r1/metadata.json` | `85142a1a0631ae75643813f844533a2055b047f6e5853a08a06c0fd3e09c6847` |

## Validation and residual risks

Observed HEAD matches assignment: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`; `git diff --cached --name-only` returned empty. No staging or project edits were performed except this authorized report. No tests/build/typecheck/lint/format/API validation, network/browser, source example execution or nested delegation were run. Main/archive files are unchanged by this worker; other workers' concurrent output is not attested.

Local approval remains archive-recorded; the cited external PDF and original approval conversation were not independently inspected. Contrary brief applicability remains unresolved as directed by parent. Current API/schema, code/tests and deployed ESK behavior are unknown, not missing. Source metadata/version and accepted membership are existing saved records; this run is not remote recollection or full source-integrity recertification. Independent report review and parent acceptance remain pending; G2–G5 and feature closure are unaffected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Resolved row12 exact MOS1044 ownership; mapped all four requirements, seven scenarios and historical tasks; verified actual brief exclusion/read-category evidence; parent consulted and bounded precedence question retained without reopening existing approval."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SPEC-G2-DIALOG-CATEGORY.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD; git diff --cached --name-only","result":"passed","summary":"Assignment HEAD matched; no staged paths at inspection."},
    {"command":"wc -l and nl -ba for originating planning files; read-only Python SHA-256/line counts of 24 listed inputs","result":"passed","summary":"Recorded actual read ranges, requirement/task locators and current input fingerprints."},
    {"command":"Tests/build/typecheck/lint/format/API checks/network/browser","result":"not-run","summary":"Prohibited or unnecessary for this explicitly read-only documentary analysis."}
  ],
  "validationOutput": ["Four requirements and seven named scenarios have exact main/archive/task joins.","Read metadata is not mutation authorization; archived gate closure is not deployment verification.","Parent confirmed unresolved brief applicability must not reopen approved local scope or block independent lanes."],
  "residualRisks": ["No verified explicit linkage reconciles the manual-tagging exclusion with approved MOS1044 scope; only changes relying on that reconciliation are blocked.","PDF/original approval conversation, API/runtime and remote freshness not independently verified; independent report review pending."],
  "noStagedFiles": true,
  "diffSummary": "Authorized report only; no shared register, product plan, main-spec, archive or application edits.",
  "reviewFindings": ["No evidence-backed product correction; positive ownership join plus bounded applicability question, not a missing feature or approval gap."],
  "manualNotes": "Read complete governing and originating planning artifacts and cited evidence at declared ranges. Parent retains acceptance; no chronological precedence or tagging policy invented."
}
```
