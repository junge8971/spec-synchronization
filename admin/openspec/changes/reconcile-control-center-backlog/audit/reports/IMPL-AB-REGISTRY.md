# AB-REGISTRY — bounded implementation audit

HEAD verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches assignment). Read complete current registry/module specs and accepted documentary report/review; no source re-extraction. Read complete proposal/design/tasks for archives `2026-10-15-add-optional-ab-testing` (A) and `2026-10-15-update-control-center-api-contracts` (C). No project files changed.

## Result / necessary planning correction

**No new registry implementation task justified by this inspection.** The documentary ABROOT-02 discrepancy is already accounted for by C proposal §What Changes (typed groups_count), design §4 and §7, and checked tasks 4.1–4.4. A design §3 and tasks 4.1/4.3 describe the historical unavailable group-count state; C explicitly says not to rewrite archives. Record that existing delta ownership in reconciliation, rather than reopening group-count implementation or silently changing A. This is not a claim of full conformance, executed tests or deployment.

## Scenario → mounted code → transport/mock → written tests → owner

Paths below are relative to repository root; `AB` means `app/optional/ab-testing/`.

- **Registry entry/navigation/access:** application composition `app/application/constants/application-routes.constants.ts:2–6` imports public A/B API unconditionally; `AB/constants/descriptor.constants.ts:12–31` registers registry/new/detail, content navigation and parent; `AB/routes/registry.tsx:1–5` mounts `AbTestingRegistry`. Registry query hooks `AB/model/ab-testing-queries.ts:12–28,46–78` gate reads on existing `usePermissions('*')`, guard session ownership before/after reads and pass abort signals. Module spec “Default removable section”/“Shell routes and access”; A tasks 1.1–1.3. No new permission policy or backend authorization inferred. Production graph/removal not verified here.
- **Columns and server-owned selection, later-page filter, short query:** `AB/ui/registry/registry-table.tsx:11–96` renders name/code, per-ID surfaces, groups_count and lookup status with code fallback; `registry-filters.tsx:15–77` retains query draft, sends query only through `registrySearchQuery`, resets offset for query/status/surfaces. `AB/model/registry-search.ts:92–95` trims and requires two characters. `registry-results.tsx:10–82` distinguishes pending/error/empty/no-matches, uses server total and offset/limit. `AB/handlers/registry-handlers.ts:33–40` provides three-click sort back to `-updated_at`. Client `AB/api/ab-testing-client.ts:33–44` POSTs parsed search through shared transport. `mocks/ab-testing/handlers.mjs:44–53,105–112` runs validated search before page(), explicitly enables case-sensitive equality and searches name/code/description/tags/group_tags/surface_names. `mocks/ab-testing/model.mjs:81–99` derives summaries from groups and nondeleted surface names. Written component assertions inspected at `registry.test.tsx:185–265` cover offset reset, short query, sort cycle and history; named tests at :126/:165 cover combination/columns. Mock test declarations `mocks/ab-testing/search-export.test.mjs:6,242` cover server selection/sorts. Owner: registry spec Server-owned selection; A tasks 3.4,4.2.
- **Conditions / numeric ranges / explicit unsupported fields:** `AB/api/ab-testing-search-schema.ts:9–99` enforces finite numeric values, exactly two ordered between bounds, numeric operators only on groups_count, nonempty text/set values and max 50 conditions. `AB/model/registry-search.ts:26–54` checks published metadata operator/type and rejects archived. `mocks/ab-testing/model.mjs:42–61` publishes groups_count integer and numeric operators. Full written component test `AB/ui/registry/registry-conditions.test.tsx:26–155` asserts Cancel does not apply; groups_count available while priority/surfaces disabled; incomplete/empty-in blocked; 51st row disabled; blank is not zero; OR [0,1.5] remains numeric. Owner: registry spec Supported condition builder/Unsupported conditions remain explicit; C tasks 4.1,4.2,4.4 (not a missing A task). Mock numeric test is indexed at `search-export.test.mjs:297–371`; evaluator NULL semantics were not independently audited in this lane.
- **Full URL / malformed selection / clipboard:** `AB/model/registry-search.ts:76–90` rejects unknown/duplicate query parameters and malformed/oversized JSON as a whole; JSON codec retains types. `AB/model/use-ab-testing-registry.ts:10–16` enables search only for valid decoded selection. `AB/ui/ab-testing-registry.tsx:38–45` provides explicit reset; :102–105 copies current complete href. `AB/handlers/registry-handlers.ts:20–31` reports clipboard failure, not success. Written assertions `registry.test.tsx:241–265` preserve numeric OR via Back/Forward; test declarations :266/:295/:327 cover copy/basename, invalid URL and OR pagination. Owner: registry spec URL round trip; A tasks 4.1/4.4, C task 4.3.
- **Managed saved filters:** `AB/api/ab-testing-saved-filter-client.ts:10–74` retains unvalidated stored search while listing (so invalid records remain deletable), resource-scopes paginated GET, POSTs complete parsed search with nonblank 1–150 name, deletes UUID ID without name-upsert. `AB/model/use-ab-testing-registry-saved-filters.ts:15–76` uses server offset, permissions/session guards, no mutation retry and only invalidates after confirmed success. `AB/model/registry-search.ts:57–73` normalizes only inert null DTO filters before strict application. Written test declarations `AB/ui/registry/registry-saved-filters.test.tsx:82,103,124,174,195,221` cover persistence, pagination, null defaults, failed delete/create, whole-search rejection and numeric range; client tests :13/:34 cover resource/pagination and duplicate-name POST/ID-delete. Mock test declaration `mocks/ab-testing/search-export.test.mjs:104` covers atomic validation/persistence by ID. Owner: registry spec Persistent saved filters/Typed group conditions survive saved filters; A tasks 3.5/4.4 and C task 4.3. These indexed tests were not all read end-to-end or executed.

Export seam only: registry passes the applied `search` to its local export component (`AB/ui/ab-testing-registry.tsx:59–67`); export behavior belongs to AB-EXPORT and was not audited.

## Evidence limits

Static local inspection only; no tests/build/typecheck, browser, network, credentials, mutations or nested agents. Test evidence distinguishes inspected assertions from test-title indexing; neither proves passing. Shared mock evaluator, full surface-resolution implementation, shell access component tests, saved API snapshot equivalence, production artifact graph and live backend remain outside this bounded inspection. Historical checked tasks are documentary state, not rerun evidence. No global/feature checkbox changes; no feature-completion or rollout inference. Accepted root report ABROOT-01/02 is the documentary source mapping; attachment/PDF coverage is not expanded.

## Current local SHA256 inputs

OpenSpec is ignored; these hashes are current filesystem bytes, not historical Git equivalence.

| Input | SHA256 |
|---|---|
| openspec/specs/ab-testing-registry/spec.md | f23569188a872ab976bbe1ae8be032a667c854ed4a544404f068e1d6e4a59bd5 |
| openspec/specs/ab-testing-module/spec.md | 0013ea05d4c913d321baae18dca1076029792bf58ffc06e6a1715d53eca60366 |
| audit/work-items/G2-OPTIONAL-DOMAINS-SEVEN.md | 9720c147622d55b007071126202799405226f607c8935d431761f980c476e89a |
| audit/reports/DELTA-AB-TESTING-ROOT-DOC.md | cd8cb41cc08c0f2400a03dc842f089eec3f1c393e8db8070ffc11f65f91fea69 |
| audit/reviews/R-DELTA-AB-TESTING-ROOT-DOC.md | 3db6568ae32989577ee8271a092d41c44abf9fd2c1bb6e3f705c10ceb2b9ce82 |
| A/proposal.md | 93d219f6c749cda697f3b1dcc231e3d4dbf2ea71b99267f7d610b19ba390edfd |
| A/design.md | fba208c2d27c670ff0e981d5fa17d2121df16ff67ca66d8df0adf255fff2cee6 |
| A/tasks.md | e005921905e56e00cead68fd3c58d7ae30b9ffb79d6313de3162734ec30f1073 |
| C/proposal.md | 6ece6e82490038d5ce491f19acf089c10a27dc845f74c2cf035ac37826c13bd8 |
| C/design.md | 58f8cdbd387508c10285387b3fcdbf208bfdb73559a8243997af676e38df6156 |
| C/tasks.md | 6002750f35319a52ce0c9fcd50731385ada811844c6edc3499943d87051dd478 |

`audit/` expands to `openspec/changes/reconcile-control-center-backlog/audit/`; A/C expand to the two archive paths identified above.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Bounded registry scenario/code/mock/written-test/owner mapping; current HEAD and eleven input hashes recorded; existing typed-condition delta prevents duplicate work."}],
  "changedFiles": [],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"git rev-parse HEAD","result":"passed","summary":"Matches assigned HEAD"},{"command":"sha256sum scoped OpenSpec specs, work item, accepted report/review and archive planning inputs","result":"passed","summary":"Eleven current-local hashes recorded"},{"command":"local find/rg/wc and read","result":"passed","summary":"Bounded ownership discovery and source inspection"},{"command":"tests/build/typecheck/browser/network","result":"not-run","summary":"Prohibited by assignment"}],
  "validationOutput": ["No new registry task justified; C tasks 4.1–4.4 already own numeric groups_count migration."],
  "residualRisks": ["Static partial code/test inspection is not full conformance; tests and deployment unverified; shared evaluator and production isolation not audited."],
  "diffSummary": "Only configured external report written; no project edits.",
  "reviewFindings": ["No demonstrated new registry blocker; reconcile documentary ABROOT-02 to existing contract migration without rewriting archives."],
  "manualNotes": "Accepted documentary extraction reused. Editor/export excluded except mounted export handoff. Git staging not inspected; no staging-state attestation."
}
```
