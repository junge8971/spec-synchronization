# AB-EXPORT — bounded implementation audit

## Result / authority

**Recommendation: keep / planning no-op.** No source-backed export discrepancy requiring a new change was identified in the inspected path. Existing `ab-testing-export` requirements and archived `2026-10-15-add-optional-ab-testing` tasks 3.6 and 6.1–6.3 already own the work. Do not duplicate them, rewrite the archive/main specs, or change any checklist based on this audit.

HEAD verified locally: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches work-item). OpenSpec inputs were read from current local files and hashed below; no historical equality asserted and no `git show` used. Accepted documentary authority is `audit/reports/DELTA-AB-TESTING-ROOT-DOC.md`, ABROOT-07 (root readable lines 44,57,126–144,159–162; HTML chunks [2]–[3],[7]–[9]), accepted by `audit/reviews/R-DELTA-AB-TESTING-ROOT-DOC.md`, ABROOT-07. Those source bodies/attachments were **not re-extracted**. Their picker/toast description is not proof of file delivery. Main export/module specs and complete relevant archive proposal/design/tasks/export+module deltas were read; archived verification execution claims were not relied upon.

## Scenario → code / transport / mock / written tests → owner

Paths beginning `A/` below mean `app/optional/ab-testing/`; `O/` means `openspec/changes/archive/2026-10-15-add-optional-ab-testing/`.

| Scenario and requirement | Mounted implementation and transport | Mock and written, unexecuted tests | Existing owner / disposition |
|---|---|---|---|
| Whole applied selection, second page, ordered metadata fields; empty selection blocked (`openspec/specs/ab-testing-export/spec.md:9–21`) | `A/routes/registry.tsx:1–4` mounts registry. `A/ui/ab-testing-registry.tsx:54–63` supplies actual `search`, not table rows; `A/model/use-ab-testing-registry.ts:14–17` derives applied selection from URL. `A/ui/export/ab-testing-export-form.tsx:19–35,38–58,67–75` intersects metadata with supported fields and retains selection order; `A/handlers/export.handlers.ts:5–22` appends reselected fields and prevents empty/pending submit. `A/api/ab-testing-export-client.ts:49–60` POSTs `{fields,search}` to `/managed-resources/ab-testing/experiments/export`; pagination stays in complete search, not used to slice locally. | `mocks/ab-testing/handlers.mjs:44–52,114–118` searches all live experiments without `page()`; shared `mocks/managed-search.mjs:75–85` filters/sorts only. `A/ui/export/ab-testing-export.test.tsx:66–101` asserts exact second-page search including OR numeric condition and field order; `:128–142` empty blocker. `A/ui/export/ab-testing-export-integration.test.tsx:40–56` checks default registry dialog wiring (does **not itself submit/assert request**). Mock `search-export.test.mjs:178–213` asserts full matching records with limit=1/offset=1. | O/design.md §7, O/tasks.md 6.1,3.6. Keep. |
| Limit error without truncated success (same spec:17–21) | `A/ui/export/ab-testing-export-heading.tsx:14–16` displays metadata maximum/fallback 10000; `A/ui/ab-testing-export.tsx:55–63` reports failure, suggests narrowing selection, only shows success from mutation success. It does not truncate. | `mocks/managed-search.mjs:94–102` rejects >10000 before CSV; `mocks/ab-testing/handlers.mjs:71` selects `EXPORT_LIMIT_EXCEEDED`. `mocks/ab-testing/search-export.test.mjs:229–239` checks 10000 accepted /10001 rejected, no attachment; component test `:143–165` covers HTTP 413/500, selected fields retained, no file/success. | O/tasks.md 6.1,3.6. Keep; enforcement is server-owned. |
| Saved detail only, dirty warning, five flat groups; new record disabled (spec:23–35) | `A/routes/{creation,details}.tsx:1–4` → `A/ui/ab-testing-editor.tsx:9–21` default export → `A/ui/editor/editor-header.tsx:73–77` saved `snapshot?.id`, dirty/pending → `A/ui/export/ab-testing-editor-export.tsx:7–23`. `A/model/export-availability.ts:8–10` blocks new/missing metadata. `A/constants/export.constants.ts:34–69` defines five groups; form `:62–65` explicitly disclaims nested rows. Heading `:18–22` warns dirty. Client `:63–75` validates UUID, sends only `{fields}` to detail export. No draft/groups/surfaces/sections payload. | Component `A/ui/export/ab-testing-export.test.tsx:102–142` checks five groups, summary disclaimer, saved ID/fields and new blocker; mounted integration `:57–72` checks new-editor disabled accessible explanation. Mock detail handler `mocks/ab-testing/handlers.mjs:75–85`; mock test `search-export.test.mjs:214–228` checks only selected detail, rejects nested fields/sections and extra search. | O/design.md:83–87; O/tasks.md 6.2,3.6. Keep flat saved configuration export, not nested group-table export or analytics. |
| Genuine file, safe name, errors, duplicate requests, owner change, cleanup (spec:37–44) | `A/api/ab-testing-export-client.ts:25–47` checks CSV UTF-8 headers, attachment filename, BOM and nonempty/non-JSON prefix; attaches response session. `app/shared/api/http-client.ts:132–183` retains protected binary transport/session/error path. `app/shared/api/file-response.ts:3–14` decodes RFC5987 filename and replaces controls/path separators. `A/model/use-ab-testing-export.ts:14–57` owner guards, abort signal, no retries, pending ref, blob URL allocation and timed/unmount cleanup. `app/shared/lib/handlers/download-attachment.ts:1–11` removes anchor in finally. UI `A/ui/ab-testing-export.tsx:23–25,43–66` blocks pending closure/submission; success says handed to browser, not persisted to disk. | `A/api/ab-testing-export-client.test.ts:7–31` checks empty/duplicate fields, invalid UUID, MIME/disposition/extension/BOM/JSON failures. Component export tests `:166–224` cover download exception/cleanup, double click, former-owner suppression before URL allocation and unmount abort. Mock CSV assertions `mocks/ab-testing/search-export.test.mjs:178–220` cover BOM, headers, quoting, formula safety, display names and flat summaries; actual serialization `mocks/managed-search.mjs:88–115`. | O/tasks.md 6.3,3.6; module spec session/access boundaries remain. Keep. |

## Saved API vs local implementation

Saved `docs/api/contracts/managed-resources.openapi.json:1682–1781` declares both POST CSV operations with existing security schemes; schemas `:7478–7567` allow only supported flat fields (1–100), list search, and no extra detail payload. `docs/api/contracts/crud-api.md:1951–1963` explicitly says full search ignores limit/offset, maximum 10000, lookup display names, flat distribution and filenames. These are **saved contract evidence**, not a live deployment/API conformance result.

Mock registration is connected at `mocks/managed-resources.mjs:5,182`; local HTTP tests are written evidence only. Export business code remains in optional A/B; inspected imports use its own modules, shared technical helpers, and public session API. No cross-optional dependency or replacement auth policy was introduced by this path. This narrow inspection does not independently establish global removal/build isolation or all shell access behavior. Backend still authorizes requests; mock delivery is not approved real-server deployment or experiment execution.

## Planning / bounded gaps and limits

- **No new export task needed.** Existing archived tasks already describe selection, flat detail, transport/session and mock coverage. Record this mapping under active reconciliation task 3.5/3.6, subject to parent review; leave all task states untouched.
- Main spec and archive export delta agree on the inspected scenarios. The accepted root's demo feedback is deliberately superseded by approved genuine API-file behavior, not a reason to weaken it or claim live support.
- Mounted integration tests only open registry dialog / verify new-editor blocker; exact payload and dirty detail are tested at export-component level. This is a coverage boundary, not demonstrated failure or a basis to manufacture new work.
- No tests/build/typecheck/lint/typegen/API generation/browser/network/business requests/credentials/nested agents. No current execution results. No claim of final filesystem download, real backend availability, production mock exclusion, feature completion, or deployment.
- Only export connections were inspected; no editor lifecycle/registry feature re-audit, other export modules, source attachments or global architecture census. Shared file helpers were followed only for this seam. One bounded grep included guessed nonexistent `mocks/managed-resource-handlers.mjs` and exited 2; actual registration was located in `mocks/managed-resources.mjs` without blocker.

## Current local input SHA256

These are current bytes, not Git history or fresh external-source integrity attestations. Prefixes: `S=openspec/specs/`; `R=openspec/changes/reconcile-control-center-backlog/`; `O=openspec/changes/archive/2026-10-15-add-optional-ab-testing/`.

```text
9720c147622d55b007071126202799405226f607c8935d431761f980c476e89a R/audit/work-items/G2-OPTIONAL-DOMAINS-SEVEN.md
d672a8a81e8847e28f91910e2b34510ff320ebf7a3a81df219923195ec5801ca S/ab-testing-export/spec.md
0013ea05d4c913d321baae18dca1076029792bf58ffc06e6a1715d53eca60366 S/ab-testing-module/spec.md
cd8cb41cc08c0f2400a03dc842f089eec3f1c393e8db8070ffc11f65f91fea69 R/audit/reports/DELTA-AB-TESTING-ROOT-DOC.md
3db6568ae32989577ee8271a092d41c44abf9fd2c1bb6e3f705c10ceb2b9ce82 R/audit/reviews/R-DELTA-AB-TESTING-ROOT-DOC.md
93d219f6c749cda697f3b1dcc231e3d4dbf2ea71b99267f7d610b19ba390edfd O/proposal.md
fba208c2d27c670ff0e981d5fa17d2121df16ff67ca66d8df0adf255fff2cee6 O/design.md
e005921905e56e00cead68fd3c58d7ae30b9ffb79d6313de3162734ec30f1073 O/tasks.md
1a8bec1cfb40b3759e54016c5007595a1e457c227a09a6e70e6bc6b92814607b O/specs/ab-testing-export/spec.md
f2f83ebaa1bc01e27fd5cf7aa988e18c57cabb01ff114a41602322afc71eed37 O/specs/ab-testing-module/spec.md
add5cee6ffa34551e8d3affef972d89fd0a62c607a3db9062f8ade6822353300 R/tasks.md
4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058 docs/api/contracts/crud-api.md
cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf docs/api/contracts/managed-resources.openapi.json
```

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"AB-EXPORT-only scenario/code/transport/mock/written-test/owner mapping, no-op recommendation, HEAD and current local SHA256 recorded."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/50982ca9-1cc4-42f9-b49b-912e0b738c81/impl-ab-export.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD; sha256sum scoped local inputs","result":"passed","summary":"Expected HEAD and 13 local input hashes recorded."},
    {"command":"bounded read/rg/find/wc inspections","result":"passed","summary":"Mapped export seam and existing owners; no execution tests."},
    {"command":"rg registration search including guessed mocks/managed-resource-handlers.mjs","result":"failed","summary":"Guessed filename absent; actual registration found in mocks/managed-resources.mjs:5,182."},
    {"command":"git diff --cached --name-only","result":"passed","summary":"No staged paths reported."},
    {"command":"tests/build/browser/network","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Read-only static audit; existing tests inspected, not executed."],
  "residualRisks": ["Live backend, deployment, production graph/removability and runtime test outcomes unverified; documentary attachment limits retained."],
  "noStagedFiles": true,
  "diffSummary": "Only configured external report written; no project edits or task changes.",
  "reviewFindings": ["No blockers established in bounded export seam; planning no-op, retain existing export owners."],
  "manualNotes": "Accepted documentary extraction reused without repetition. Optional module delivery distinguished from live API and deployment; no feature completion inferred."
}
```
