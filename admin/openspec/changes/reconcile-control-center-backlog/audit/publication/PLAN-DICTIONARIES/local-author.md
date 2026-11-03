# Offline Dictionaries planning — author result

Created **one** `openspec/changes/add-reference-dictionaries/` change through native OpenSpec scaffold. All four required workflow artifacts exist; an additional evidence document preserves complete source-section mapping. **Planning complete for review, not implementation-ready.** No application implementation, contract/main-spec/archive/auth changes, audit edits, network/browser/E2E/application tests, prototype execution, nested delegation or Git mutations occurred.

## Manifest and SHA-256

All paths below are relative to `openspec/changes/add-reference-dictionaries/`:

| Artifact | SHA-256 |
| --- | --- |
| `.openspec.yaml` | `30cfdee007123f96b2ab27ca107e406084602caf445d6b7cd2130ab329668ed3` |
| `proposal.md` | `14c73e5253e202bf9635774e5b9089a339523ede7654c40db856b7ee8cc764a9` |
| `design.md` | `7332651660a07eec6de670da0a2ef588a3de29b99c731833990690935887e58c` |
| `evidence.md` | `471fe1ac3c8cb997c7a0ec403846a520b1727ba562f9217a4d1c572038132a11` |
| `tasks.md` | `1d555d76dc9beb2aba6cdd70f6b1998ba0815ccee15892747b976efb5d5f5394` |
| `specs/reference-dictionaries/spec.md` | `38f2a37272f7267fb78719bda46d3e78e2a78cb1479348f2bff9667699ea0a0e` |

15 requirements, 22 scenarios, 34 unchecked tasks, zero checked feature tasks. Native status's four checked **artifact** entries indicate file completeness only, not feature delivery or gate closure. OpenSpec files are ignored by Git; clean status is not proof of no planning writes. Explicit file manifest/hashes provide evidence instead.

## Coverage and evidence

Reread updated PLAN-DICTIONARIES, config and all retained reports, with continuation after output truncation. Verified authoritative root and unchanged HEAD `d2af6c5b61146306f0795b6a272c5a74bdfa08f7`. Recomputed all primary/local-contract hashes; they match the retained handoffs:

- Wiki readable: `002d6b34375939d9f8847350ef0cdf9ff6db8f151028f297da6750ba0d1c0957`.
- Wiki content JSON: `6f4a85bf911634a724e3411138c517fe3ce295d2036e09d573444dc9d6d04588`.
- Exact prototype: `385f230467db6b8b2fdf26dbc08f9154ca7fd1651db037c6227eccc9fc8fa310`.
- Local aggregate: `c19ff30e53a8705629bc11d51a25b3a2019ef641340348a7f2e985088127fe3d`.
- Managed split: `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf`.
- CRUD Markdown: `4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058`.
- CRUD raw: `91c8dc68fc1b602a64428d1d6f1d9c44a0e6a89eced226e4773853badf13954a`.

`evidence.md` includes full retained Описание/Таблицы subsection matrices with Wiki line/prototype function locators, all named consumer fields, fourteen checks and current Q-to-G disposition. Attribution distinguishes primary requirements, prototype-only examples, historical Jira/journal comparisons and current offline facts. Exact Wiki URL remains https://wiki.mos-team.ru/spaces/KR/pages/247751846/ (supplied v10). Parent's fresh Swagger 403 is recorded as parent-reported access evidence, not author verification or proof of missing APIs.

No scope reduction: registry/search/multiselects/conditions/sorting/saved selections/links; card/settings/checks; ordinary and attachment values; creation/lifecycle/dirty navigation; all three CSV exports; model/ownership and documented consumers remain in one change. Historical complex-condition exclusion is explicitly retained for reconciliation rather than applied as a scope cut.

Independently rechecked local operation paths (14 catalogs plus five shared filters), CRUD mutation/consumer seams, actual route configuration, file-response and editor snapshot helpers and KB export reference pattern. Native existing-capability inspection read HTTP/API-integration/permissions requirements and scenarios. Reuse is grounded in ordinary FSD/public interfaces and native routing; optional internals are reference patterns only. No new permission mapping is proposed.

## Exact outstanding gates

- **G1 — save:** atomic aggregate prerequisite versus explicitly approved staged per-row persistence/reconciliation; settings/rows/reorder/default/rename/delete, partial failures and unknown outcomes. Neither chosen.
- **G2 — source contradictions:** computed versus writable flags; protected informational codes/deletion; soft versus physical deletion and reference/code-reuse semantics; disputed attachment and other roster classifications/ownership. No seed/migration/physical-delete permission inferred.
- **G3 — missing API and validation:** server checks/recheck/results, all fourteen identities, severity and create/save/activate stages, values_required meaning, comment journal persistence. Local validation cannot close this gate.
- **G4 — lifecycle/consumers:** draft activation, informational pause mapping, immediate propagation versus cache/publication/required settings and named owner-table consumer integration. Stored status is not enforcement.
- **G5 — missing registry powers:** group/type sorting and numeric value-count conditions plus explicit historical-scope reconciliation. No page-local filtering or kind-sort substitution.
- **G6 — external attachment policy:** exact MIME/masks, extension fallback, overlap/order priority, valid zones/extensions, inactive rules and unmatched denial with enforcement owner evidence. No uploader implementation authorization.
- **G7 — material UX:** actual discard/committed subsets, route/card/modal/lifecycle sequencing; full URL/sort/reset/blank/invalid conditions; duplicate saved-filter names/application offset; source creation-case/normalization/default-owner reconciliation.
- **D1 — unverified deployment:** actual operations/classifications/registrations/errors, CSV/CORS filenames, backend authorization and consumer/evaluator effects. Distinct from missing publication; later separately authorized verification only.

Published server filters/exports are recommended directly; no artificial persistence architecture question remains. Three distinct exports, saved-server values, CSV semantics/limits and active default validity are grounded in local contracts. Ordinary route naming is proposed, not a new product blocker. Missing capabilities remain prerequisites, not disabled-control acceptance of a reduced release.

## Validation

Passed:

- `openspec context --json`: nearest expected root.
- Native `new change`, per-artifact `instructions`, repeated `status`, dependency rereads; final status 4/4 artifacts complete.
- `openspec validate add-reference-dictionaries --strict` before and after formatting: **Change 'add-reference-dictionaries' is valid**.
- `yarn prettier --write 'openspec/changes/add-reference-dictionaries/**/*.md' openspec/changes/add-reference-dictionaries/.openspec.yaml`.
- Same scoped `yarn prettier --check`: **All matched files use Prettier code style!**
- Hash/manifest/checklist checks; no scaffold placeholders or TODOs detected.
- `git diff --check`, `git diff --cached --name-only`, `git status --porcelain`: clean; staging empty. `git check-ignore` confirms planning files are ignored.

One initial inspection command ended with status 2 because probing the not-yet-created target directory with `ls` found no directory; context/HEAD/status/config succeeded. No infrastructure failure or fallback occurred. Large retained/spec output was continued from its saved command output; no lost dependency reading.

Not run: application typecheck/lint/tests/API check/build or browser/E2E (planning-only authorization). Future verification tasks enumerate unit/component/HTTP tests, accessibility/error/draft/session/CSV boundaries and applicable project checks. No runtime/deployment integration is asserted.

## Review recommendation

Independent reviewer should inspect source-to-gate coverage, local transport details and whether any proposed interaction inadvertently selects a gated policy. The candidate is ready for **planning review only**. Parent should preserve this manifest and obtain gate dispositions before any apply request; no routine completion handoff or further project writes are needed from this author.

```acceptance-report
{
  "criteriaSatisfied": [
    {"id":"criterion-1","status":"satisfied","evidence":"One complete full-section planning change created only in the authorized new directory; unresolved choices explicitly gated and no implementation performed."},
    {"id":"criterion-2","status":"satisfied","evidence":"Manifest hashes, full section mapping, strict validation, scoped formatting and exact open gates supplied for independent review."}
  ],
  "changedFiles": [
    "openspec/changes/add-reference-dictionaries/.openspec.yaml",
    "openspec/changes/add-reference-dictionaries/proposal.md",
    "openspec/changes/add-reference-dictionaries/design.md",
    "openspec/changes/add-reference-dictionaries/evidence.md",
    "openspec/changes/add-reference-dictionaries/specs/reference-dictionaries/spec.md",
    "openspec/changes/add-reference-dictionaries/tasks.md"
  ],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"openspec context --json; openspec new change add-reference-dictionaries; per-artifact instructions/status","result":"passed","summary":"Native scaffold and dependency-order authoring completed."},
    {"command":"openspec validate add-reference-dictionaries --strict","result":"passed","summary":"Valid before and after formatting."},
    {"command":"yarn prettier --check 'openspec/changes/add-reference-dictionaries/**/*.md' openspec/changes/add-reference-dictionaries/.openspec.yaml","result":"passed","summary":"All scoped files formatted."},
    {"command":"sha256sum source and generated artifacts; git diff --check; git diff --cached --name-only; git status --porcelain","result":"passed","summary":"Hashes recorded; no staged files or tracked diff."},
    {"command":"Initial ls of absent target directory","result":"failed","summary":"Expected not-yet-scaffolded target; no effect on workflow."},
    {"command":"Application checks/tests/build and browser/E2E","result":"not-run","summary":"Planning only; no application changes or test execution authorized."}
  ],
  "validationOutput": ["Strict validation passed.","Scoped formatting passed.","15 requirements; 22 scenarios; 34 unchecked tasks; no checked feature tasks."],
  "residualRisks": ["G1–G7 and D1 remain open; not implementation-ready.","Independent review remains required.","Ignored planning files require explicit manifest-based persistence."],
  "noStagedFiles": true,
  "diffSummary": "Six new planning files in one change; no application/contracts/main-spec/archive/audit changes.",
  "reviewFindings": ["No self-review scope blocker found; independent reviewer must assess gated policy preservation."],
  "manualNotes": "Native complete status refers only to artifact existence, not approved product behavior or deployment readiness."
}
```
