# Code Context

## Result

**Baseline row5 ownership resolved: 9 requirements / 31 scenarios, four exact archived change owners. Recommend keep/no-op for current specification.** Historical text defects are qualified below; current implementation remains unverified. This is a concrete requirement/scenario/task join, not feature closure or G2 acceptance. Parent and independent reviewer retain acceptance.

Literal path aliases:
- C = `openspec/changes/reconcile-control-center-backlog`
- A = `openspec/changes/reconcile-control-center-backlog/audit`
- M = `openspec/specs/code-quality-gates/spec.md`
- Q = `openspec/changes/archive/2026-09-23-improve-code-quality`
- F = `openspec/changes/archive/2026-09-25-enforce-fsd-code-decomposition`
- K = `openspec/changes/archive/2026-10-14-add-optional-knowledge-base`
- B = `openspec/changes/archive/2026-10-15-add-optional-ab-testing`

No Jira identity is invented: LOCAL-001 retains this technical capability without a Jira match. Its active-proposal inventory does not identify a current product change owning these gate requirements. C owns reconciliation, not gate implementation.

## Files Retrieved

Complete reads, inclusive line ranges:

| Exact file using aliases above | Lines | Relevance |
|---|---:|---|
| A/work-items/G2-OWNERSHIP-WAVE.md | 1–19 | Complete common contract and assigned section; other lanes not executed |
| C/proposal.md; C/design.md; C/tasks.md | 1–30; 1–133; 1–45 | Authority, independent acceptance and open downstream gates |
| C/specs/control-center-backlog-reconciliation/spec.md | 1–108 | Evidence, unknown/missing and publication constraints |
| A/reports/LOCAL-001.md | 1–194 | Baseline identity and exact archive inventory |
| A/reports/G2-MAIN-CAPABILITY-JOINS.md | 1–204 | Row5, N5 and P/U definitions |
| M | 1–200 | All requirements/scenarios |
| Q/proposal.md; Q/design.md; Q/tasks.md; Q/specs/code-quality-gates/spec.md | 1–28; 1–88; 1–31; 1–56 | Original gate/guidance contract |
| F/proposal.md; F/design.md; F/tasks.md; F/specs/code-quality-gates/spec.md | 1–31; 1–123; 1–42; 1–156 | Structural migration and revised verification |
| K/proposal.md; K/design.md; K/tasks.md; K/specs/code-quality-gates/spec.md; K/verification.md | 1–35; 1–139; 1–75; 1–37; 1–104 | First optional exception and historical receipt |
| B/proposal.md; B/design.md; B/tasks.md; B/specs/code-quality-gates/spec.md; B/verification.md | 1–34; 1–123; 1–53; 1–42; 1–264 | Second exception, cross-optional prohibition and historical receipt |

Selective reads: `A/decisions.md:1–12` (complete D-062); `A/reviews/R-G2-MAIN-CAPABILITY-JOINS.md:1–220` (verdict, row5 and limitations; trailing acceptance JSON not fully read). Optional business specs were not read: relevant delta specs are code-quality, with full proposals/designs/tasks for context. No application/config/test files, external source bodies or temporary receipt logs opened. Scoped path discovery followed LOCAL-001 archive names; initial change-directory find truncated at 300 and was not absence evidence. Content reads used read; read-only Python calculated hashes/line locators. A final targeted grep verified Q/design.md:35,67.

## Key Code — requirement/scenario/task map

No runtime code inspected. Task numbers and exact scenario titles are stable locators. Checked tasks below are **historical declarations**, not fresh executed evidence.

| Main requirement / range | All scenarios in source order | Exact originating delta and task owner |
|---|---|---|
| M:9–27 — Project agent guidance defines readable decomposition | Function mixes responsibilities; Existing code is already cohesive; Cohesive code violates mandatory placement | Q/specs/code-quality-gates/spec.md:7–20 originates first two; Q/tasks.md §1.2 and §§2–4 apply guidance. F/specs/code-quality-gates/spec.md:3–21 explicitly revises cohesive-code boundary/adds mandatory placement; F/tasks.md §2.1 and §§3–6 migrate owners. |
| M:28–41 — Lint warnings block acceptance | Warning without errors; Clean code | Q delta:21–34; Q/tasks.md §§1.3–1.4, 5.1 define full/staged configuration and clean/warning smoke checks. F/tasks.md §2.5 reinforces staged full-tree architecture/exit tests; §7.1 final verification. |
| M:42–50 — Quality rules cannot be bypassed to accept a refactor | Refactored code still exceeds complexity limit | Q delta:35–43; Q/tasks.md §§1.2–1.3, 5.3. F/tasks.md §§1.2, 3.2, 7.2 retain narrow justified exceptions rather than ignore/baseline. |
| M:51–69 — Verification reports distinguish executed and missing checks | Environment prevents verification; Logic is refactored; Browser tests are not authorized | Q delta:44–56 originates first two; Q/tasks.md §§1.1, 5.1–5.3. F delta:22–40 expressly replaces wording/adds authorization scenario; F/tasks.md §§1.1, 7.1–7.2 and behavior tests in §§3–6. |
| M:70–110 — Application code respects FSD ownership and public APIs | Dependency points to a higher layer or sibling slice; External consumer bypasses a slice public API; Internal implementation uses a local module; New slice is introduced; Optional module consumes stable dependencies; Business code depends on optional implementation; Optional modules depend on each other | F delta:43–66 originates first four; F/tasks.md §§2.3–2.5, 3–6. K delta:3–37 revises boundary/adds fifth and sixth; K/tasks.md §§1.1–1.3, 10.2. B delta:3–42 explicitly extends to A/B/adds seventh; B/tasks.md §§1.1–1.2, 7.2. Explicit MODIFIED lineage, not precedence guessed from dates. |
| M:111–139 — Declarations are located by purpose within their owner | Component declares named props inline; Fixed configuration shares a file with event logic; Handler depends on form and navigation state; Local computation uses const; Type is inferred from a validation schema | F delta:67–95; F/tasks.md §§2.1–2.2, 3.1–3.4, 4.1–4.3, 6.3. Mechanical type placement does not replace semantic review of constants/handlers/closures. |
| M:140–158 — Components are separated and nested by ownership | Multiple components share a file; Child belongs to one component; Child gains another consumer | F delta:96–114; F/tasks.md §§2.1–2.2, 3.2, 5.1–5.3, 6.2–6.3. Nearest lawful common owner, not automatic promotion to shared. |
| M:159–177 — Structural checks cover the whole handwritten application | Old file violates a new rule; Import target changes ownership; Rule configuration changes | F delta:115–133; F/tasks.md §§2.2–2.5, 6.3, 7.1–7.2. K/B tasks §1.1 extend executable architecture examples without blanket optional ignore. |
| M:178–200 — Migration preserves generated and framework contracts with explicit exceptions | Generated API schema is checked; Framework module is decomposed; Shadcn compound component conflicts with a rule; Migration is declared complete | F delta:134–156; F/tasks.md §§1.2, 3.1–3.2, 6.1–6.3, 7.1–7.2. Generator/output unchanged, framework exports/URLs retained, behavior/user edits preserved. |

Here “Q/F/K/B delta” means that owner's `specs/code-quality-gates/spec.md`. Count: 3+2+1+3+7+5+3+3+4 = **31**; all nine main clauses mapped. No duplicate capability or active remediation is invented.

## Architecture and lane applicability

Policy (`AGENTS.md`) + full/staged ESLint tooling + executable positive/negative examples + behavior-preservation checks constitute this capability. Q owns original lint/guidance, F application structure, K/B only named optional exceptions. Business HTTP/mock requirements remain their own capabilities even where Q historically refactored their code.

| Lane | Supported disposition |
|---|---|
| Requirements | All local normative requirements enumerated. No need to invent Jira/Confluence business scope for a technical gate. No independent external requirements-lane acceptance claimed. |
| OpenSpec | Exact full main→delta→task ownership for 31 scenarios; parent review pending. Stronger than inventory-only U, not implementation acceptance. |
| API | **No standalone business endpoint/DTO/error contract** belongs to lint/structure rules; Q/F proposals explicitly preserve API. However API-preservation is applicable to M:178–186 and Q transport refactor: generator/output and consumer compatibility must survive. Historical api:check is not current proof. Public slice API in M:70 means a module boundary, not REST. No fresh live API lane is needed merely for lint assessment, but blanket API irrelevance would erase preservation obligations. |
| Implementation/runtime | **Applicable technical execution**: clean/warning full/staged exit codes; whole-tree dependency checks; fixture acceptance/rejection; generated/framework compatibility; behavior preservation and optional isolation. Not inspected/run here. Historical receipts only; current gate correctness unknown, not absent. Semantic naming/ownership cannot be declared fully enforced by lint. |
| Deployment | Deployed business service not required to prove lint exits. Browser/E2E/backend credentials neither necessary nor permitted here. Optional build/module isolation has historical evidence, no current deployment proof. |
| Reconciliation | Keep current normative contract; qualify historical defects below. Independent acceptance outstanding. Do not mark original matrix lanes complete. |

## Inherited constraints and textual findings

1. **Historical E2E contradiction explicitly resolved:** Q/design.md:79–88 migration and Q/tasks.md:29 request `yarn test:e2e`; Q delta:44–46 mentions E2E without approval qualification. F/design.md:1–17 explicitly identifies this mismatch with AGENTS and says its delta corrects it. F delta:22–40 and M:51–69 prohibit creating/editing/running browser tests without separate approval. No new product decision or archive edit required; Q is not present permission.
2. **Historical missing flag token:** Q/tasks.md:5 has empty inline code for the lint flag; Q/design.md:67 repeats an empty token in warning smoke instructions. Q/design.md:35 names `eslint .` without zero-warning flag despite Q delta:21–34 requiring warning failure. This is a real historical textual omission, not a current implementation defect. F/design.md:85–107 explicitly supplies `--max-warnings 0`, full-tree staged checks, examples and implementation choices. M specifies the required exit behavior. Preserve the omission as provenance; no archive repair or inference that old gates actually ran.
3. **Different scopes, not contradiction:** Q full lint includes app/mocks/scripts/tests/config (M:30); F/proposal.md:25–31 excludes server mocks/infrastructure/E2E from *structural migration*. That does not exclude them from warning gates.
4. **No optional loophole:** K's sole exception is explicitly modified by B, not generalized to arbitrary optional folders. File/type/component rules persist; application composes public APIs; optional modules depend only on their own code/shared/public entities. KB↔A/B imports are prohibited in both directions. Framework route entrypoints are allowed, not arbitrary external deep imports.
5. **Exceptions and semantics:** F/design.md:85–107 records narrow shadcn agreement (15 then-listed compound files and two context types), not all shared/ui. Semantic constants/handlers/component ownership remain review obligations. This run does not verify today's exception list. Generated schema/generator must not be manually decomposed; no whole-tree compliance claim.
6. **Receipt status is historical:** B/verification.md:75–85 says independent review required / not archived despite now residing in archive. This is historical stage wording, not current acceptance metadata. Archive placement and checked tasks do not independently accept implementation.

## Historical validation reused, never rerun

- `K/verification.md:1–104` records successive successful typecheck/lint/format/API/test/build-graph checks, historical separately authorized browser work, and explicit later non-reruns of build/API/browser. Real backend/session/authorization remain unchecked. Its browser approval is specific historical KB scope, not permission for this audit.
- `B/verification.md:1–34` records the shared-chip pass: zero-warning lint, 160 Vitest files / 1523 tests plus 154 Node tests, both optional production verifiers; explicitly no API/schema/browser check that pass. `B/verification.md:124–170` records earlier API/build gates and reused rather than rerun removal evidence; `B/verification.md:179–193` maps architecture fixtures including optional directions; `B/verification.md:235–264` records temporary-removal checks and limitations. Referenced `/tmp` logs/graphs were not opened or verified.
- Q/F checked tasks are documentary completion assertions only; no standalone Q/F execution receipt was supplied/read. They do not establish current clean/warning/staged behavior.
- D-062 (`A/decisions.md:3–11`) accepts bounded baseline40 joins, not full capability coverage, and records a later global formatting failure (337 files). This is attributed audit history, not a fresh failure measured here; older success cannot be represented as today's green project state.

## Remaining gaps and concrete disposition

No material input is missing for this **spec ownership** result; no product precedence question is needed. Unverified: current AGENTS/config alignment; full/staged exit behavior and unstaged-consumer detection; architecture fixtures for new slices/aliases/relative/type-only/re-export; current whole-tree placement and semantic review; present approved exception list; behavior/API/framework preservation on current HEAD; current optional graph/removal evidence; integrity/availability and independent acceptance of old temporary logs. These are evidence gaps, not findings of absent implementation or a request for blanket re-audit.

**No technical/product artifact change justified.** Parent can add the exact mapping to row5 while retaining technical runtime unknown and historical-only validation. No shared registry, feature checkbox or archive changed. HEAD/index/external freshness not inspected.

## Input fingerprints

Current local SHA-256, not historical HEAD identity or source freshness. Hashes cover exact entire files; semantic read ranges remain those above (notably partial decisions/review).

| Input | SHA-256 |
|---|---|
| A/work-items/G2-OWNERSHIP-WAVE.md | 9dd958ad5d13a2bca16b60a66c02d73431b1aad5edae3a8e368bea689e1987e3 |
| C/proposal.md | 1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879 |
| C/design.md | 632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828 |
| C/tasks.md | a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83 |
| C/specs/control-center-backlog-reconciliation/spec.md | a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36 |
| A/reports/LOCAL-001.md | 0ab83e87351849500a625c2d7efea2b3142d5b1b473924dc2160e03f511e010d |
| A/reports/G2-MAIN-CAPABILITY-JOINS.md | 58912cbe79aeaa7b72273215dc84f26c9a1fcd86366de04b189893ec87f036b0 |
| A/reviews/R-G2-MAIN-CAPABILITY-JOINS.md | 2f11435ee6da92bab528ae413704e6fd2a7c6481405c86c3373ad760b58cdb95 |
| A/decisions.md | 0b875b2a5504480e29a0c99671614d1e65bbfc7d4173e3e3496a5dea89999798 |
| M | 1e55e2fe646805cbe206f6a8ae6de00e38354657fc541bf3b39a2415a4797494 |
| Q/proposal.md | a89e2d4a2a90a7d486908d274823644b826f01155869a1565da3c55caf49fe6b |
| Q/design.md | c2e9109fb507e78b105fc84da7cd87f7d1fb35ce34956ec2cbd306daf78b1014 |
| Q/tasks.md | 854b2745fe2f95f517e9bf0f704037f246beca60d0bfe4d4089daf25e44859de |
| Q/specs/code-quality-gates/spec.md | 6c1f5fc338f7ab0f58af883b4d79d71ec2438b03fa8be2fd76426333436cba51 |
| F/proposal.md | 553787bc78f5764c71f9f8492dd201e7266e9546cc1c5d362cdd66a0f314572f |
| F/design.md | d52414c9ea79a5464cecc10fdd9081238028a04d9d26ec1d0234dfe100d5d42c |
| F/tasks.md | 33fd168dea596ca3260ab94485a9c27d1fc18d28e3cb070bc95b819626f9b7c9 |
| F/specs/code-quality-gates/spec.md | 8ee49bd2677fe3ef706dd5ce07b53f478af0b075d91da9ee7182a2cb280e90f4 |
| K/proposal.md | 2ad551556756d7a32617702fba28b14302f5212546d96e66291f7d993b63e095 |
| K/design.md | 76110bb2afca215e8404fcd00c81c1ddc9f0c29caddef3af07a0a833beff2667 |
| K/tasks.md | 8da528d3d8cc27463bfea88b49dcb002aa07f2969bb0721531c5178045097e6d |
| K/specs/code-quality-gates/spec.md | f14b53e8e4e32c375bc54de6443599f2bf003dabbf5ab2d5ab06f22045b9f570 |
| K/verification.md | a4c4fe89b50689e5de9b045997bb86c5606292035a15df813affa4e9aa0faddd |
| B/proposal.md | 93d219f6c749cda697f3b1dcc231e3d4dbf2ea71b99267f7d610b19ba390edfd |
| B/design.md | fba208c2d27c670ff0e981d5fa17d2121df16ff67ca66d8df0adf255fff2cee6 |
| B/tasks.md | e005921905e56e00cead68fd3c58d7ae30b9ffb79d6313de3162734ec30f1073 |
| B/specs/code-quality-gates/spec.md | 027c401a133d32780ca5aeee9d3c40b1ca1624494d570e1c10306e4757dabb0e |
| B/verification.md | c3669c8b4e13b0ab739b96413a97587cd68b3d4670d1de8ff72ffcf6b144d557 |

## Start Here

Open `openspec/specs/code-quality-gates/spec.md:9–200` with the ownership table. All clauses have documentary owners; retain execution gaps rather than replacing inventory U with feature-complete status.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped baseline row5's nine requirements and 31 scenarios to four archived deltas and numbered tasks; classified API preservation and technical execution applicability; documented no-op, historical defects, actual input hashes and remaining gaps."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SPEC-G2-CODE-QUALITY.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python pathlib/hashlib line-count, fingerprint and clause-locator inspection","result":"passed","summary":"28 local input hashes and exact clause starts recorded."},{"command":"typecheck/lint/test/format/API/build/OpenSpec/browser/E2E gates","result":"not-run","summary":"Prohibited by read-only assignment; historical receipts attributed only."}],
  "validationOutput": ["Manual count: 3+2+1+3+7+5+3+3+4=31 scenarios, nine requirements.","Only configured report written; no implementation/product-plan/shared-registry edits."],
  "residualRisks": ["Current implementation/gate execution unverified; historical receipts do not establish present compliance.","Temporary logs, HEAD/index and external freshness not verified.","Parent and fresh independent reviewer retain acceptance."],
  "diffSummary":"Sole configured report created; no project implementation edits.",
  "reviewFindings":["Current specification no-op supported; historical E2E and blank lint-flag text qualified by explicit later clarification.","No new product decision required for bounded ownership result."],
  "manualNotes":"Complete governing/common and relevant planning artifacts read; selective decision/review boundaries disclosed. No network, browser, tests, nested delegation or staging performed; no assertion about pre-existing index state."
}
```
