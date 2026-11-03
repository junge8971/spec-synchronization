# Code Context

## R-SPEC-G2-MOS-1249 — ACCEPT

Fresh independent review of SPEC only. **ACCEPT the bounded analytical report and F1/F2 minimal planning corrections; no mandatory report revision or escalation.** F3/F4/F6 are supported no-ops; F5 is optional acceptance precision, not newly missing functionality. This is a reviewer recommendation, not parent acceptance/publication or feature closure.

HEAD independently verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. All 37 hashes in the evaluated report's input table match actual local bytes, including the four assigned MOS-1249 artifacts and saved Jira content/metadata. No stale input found. Evaluated report SHA-256: `9f2ae005c83fe0d71c1d2fac32573bf4ec84efa0185a1928036724657adacebd`. Review work-item SHA-256: `b7caf65fc8f8ff414cafd61a366847ee72e62c295ad4a5dd1036cd8e85ec5d4c`.

## Files Retrieved

Exact repository-relative bases below expand every listed path:
- C = `openspec/changes/mos-1249-feedback-api`
- G = `openspec/changes/reconcile-control-center-backlog`
- A = `openspec/changes/reconcile-control-center-backlog/audit`
- H = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`
- D = `openspec/changes/archive/2026-10-09-add-local-session-demo`
- U = `openspec/changes/archive/2026-10-15-update-control-center-api-contracts`
- P = `openspec/changes/archive/2026-10-13-update-control-center-contracts-put`

All reads used the read tool, not sed/cat. Full reads except explicitly selected ranges:

| Files | Lines | Purpose |
|---|---|---|
| A/work-items/R-G2-SPEC1249-IMPL916.md; A/work-items/SPEC-G2-MOS-1249.md; A/reports/SPEC-G2-MOS-1249.md | 1–13; 1–11; 1–197 | Complete assignment and evaluated report; IMPL instructions read but not acted on |
| G/proposal.md; G/design.md; G/tasks.md; G/specs/control-center-backlog-reconciliation/spec.md | 1–30; 1–133; 1–45; 1–108 | Governing authority and evidence/publication limits |
| C/proposal.md; C/design.md; C/tasks.md; C/specs/feedback-api/spec.md | 1–32; 1–81; 1–14; 1–38 | Entire change, enumerated independently: one delta |
| openspec/specs/control-center-api-integration/spec.md; openspec/specs/control-center-http/spec.md; openspec/specs/control-center-permissions/spec.md | 1–149; 1–138; 1–91 | Inherited contract/error/policy requirements |
| H/proposal.md; H/design.md | 1–38; 1–171 | Full auth prerequisite |
| H/specs/control-center-api-integration/spec.md; H/specs/control-center-http/spec.md; H/specs/control-center-mock-server/spec.md | 1–64; 1–71; 1–27 | Full auth deltas |
| H/specs/control-center-permissions/spec.md; H/specs/control-center-shell/spec.md; H/specs/mpmm-session/spec.md | 1–89; 1–101; 1–138 | Full remaining auth deltas |
| D/proposal.md; D/design.md | 1–28; 1–70 | Full demo prerequisite |
| D/specs/control-center-mock-server/spec.md; D/specs/control-center-shell/spec.md; D/specs/local-session-demo/spec.md | 1–106; 1–55; 1–123 | All demo deltas, including fixed profiles |
| U/proposal.md; U/design.md; U/specs/control-center-api-integration/spec.md; U/specs/control-center-mock-server/spec.md | 1–39; 1–120; 1–27; 1–184 | Explicit successor decisions, not timestamp inference |
| P/proposal.md; P/design.md; P/tasks.md | 1–35; 1–75; 1–34 | Complete historical PUT/supplement/unavailable migration |
| A/sources/jira-feedback/r1/content.json | selected 23–32; semantic scope only $.items[2], MOS-1249 | Description and seven acceptance criteria |
| A/sources/jira-feedback/r1/metadata.json; A/reports/JIRA-MOS-1246.md; A/reviews/R-MOS-1250.md | 1–11; 1–53; 1–97 | Source limitations and existing dispositions, not repeated implementation audit |
| A/decisions.md | selected 1–11 and 427–431 | D-060 and D-002 feedback disposition |

Auth and demo proposal/design/all six and three delta specs respectively were fully read before policy interpretation. Their tasks were not read. Unrelated resource paragraphs in U were contextual only. No application, mocks, tests, raw contracts, HTML/PDF or external sources were inspected.

## Key Code / independently checked findings

This lane reviews normative planning interfaces, not runtime code.

### F1 — accept correction

`C/tasks.md:3` currently says to retain “экспортное дополнение”; `C/design.md:21` says the export is now published and the supplement removed. `P/design.md:26–30` proves the old supplement was deliberate, while `U/design.md:84–92`, `U/proposal.md:12,37`, and `U/specs/control-center-mock-server/spec.md:13–15` explicitly replace it without discarding safety. This is an actionable current task/design conflict, not a missing Feedback CSV client.

Supported minimal replacement in task 1.1: “Использовать актуальные aggregate и standalone managed-resources, сохранив опубликованные операции, включая экспорт диалогов, и нормализацию security AND двух заголовков; не восстанавливать заменённое опубликованным контрактом локальное экспортное дополнение.” Retain source/provenance preservation, reference resolution, regression preservation and api:generate/api:check instructions. No checkbox change.

The related residue in `openspec/specs/control-center-http/spec.md:102–109` is real. Route it separately to the parent; do not edit main specs or make broad reconciliation a prerequisite to this narrow correction.

### F2 — accept correction

`C/tasks.md:14` still instructs deleting operations from an unavailable list under the older migration. `C/design.md:21–23` names its successor and existing managed handlers. Crucially, `U/specs/control-center-mock-server/spec.md:1–7` explicitly removes that requirement and says to preserve handlers; `:113–144` retains coverage and missing-handler failure. `P/design.md:48–56` establishes why the obsolete instruction once made sense.

Minimal task 1.4 change: replace “Добавить контрактные … handlers и fixtures” with “Проверить и при необходимости дополнить существующие контрактные feedback/lookup/metadata handlers и fixtures”. Preserve credential-free Express, no role enforcement/production inclusion, successful create/read and conflict HTTP assertions, and existing session profiles/fixed errors.

Minimal trailing instruction: identify `update-control-center-api-contracts` as the migrated baseline, review/reuse existing handlers and add only necessary feedback-specific fixtures/validation/tests; do not recreate the former general unavailable list. Keep the prohibition on implementing unrelated CRUD sections. This does **not** certify generic handlers as sufficient, remove genuinely unsupported behavior elsewhere, or close task 1.4.

### F3 — accept no-op

Saved Jira AC2 (`A/sources/jira-feedback/r1/content.json:30`) says PATCH. Local design `C/design.md:48,54`, task 1.2 and delta `:9` consistently require PUT. `P/tasks.md:21` explicitly records feedback PATCH→PUT with scope/checklist preservation; `P/design.md:42,54–56` supports the migration and retention of *Patch/EMPTY_PATCH names. Keep PUT and record Jira discrepancy; no fallback or external edit.

### F4 — accept no-op

`C/specs/feedback-api/spec.md:26–38`, `C/design.md:56–58`, and `C/tasks.md:5` already define pending ManagedResource mapping. Main permissions `:35–38` concerns unmapped operations, not a prohibition on this explicit pending extension. D-002 at `A/decisions.md:431` confirms disposition. No fresh wildcard-versus-ManagedResource decision is warranted. Keep UI-only permission checks, backend scope authority, server 403, exact action/resource/* and session isolation.

Demo profiles are fixed by `D/specs/local-session-demo/spec.md:45–59`; viewer/editor do not acquire ManagedResource implicitly. Read-only test principals may be test doubles. Do not change profiles or introduce request ACL to satisfy task 1.3.

### F5 — accept optional precision only

Exact GET lookup/metadata, no obsolete /feedback/catalogs, forbidden request fields, malformed-success/HTTP-error separation and all nested pointers are supported by Jira AC1–3, `C/design.md:49,54`, delta `:9,16–19`, and main HTTP `:64–91`. Adding focused assertions to task 1.2 would clarify existing acceptance, not enlarge requirements. Repeating CORS in task 2.3 follows `C/design.md:81` and Jira AC7. None is a reason to reject the bounded report or add browser tests/new metadata UI.

### F6 — accept no-op

`C/design.md:3` dates the original implementation observation to 12.10; `:21–23` separately describes later contract/mock migration. Do not convert this into a present-day whole-repository absence claim. Historical source hashes at `:12–19` are expressly identified as historical at `:21`; they must not be overwritten. Source preservation and deployment verification remain open. Feedback lacks published locking/idempotency (`:54,69`); shared transport rules are not authority to invent these backend guarantees.

### Requirement/task mapping check

All seven Jira criteria, both delta requirements, five scenarios and seven unchecked tasks have traceable planning coverage:
- AC1/AC7 contract/client consistency → delta 7–14; tasks 1.1, 1.2, 2.2.
- AC2 POST→GET/full-card PUT/payload omission → delta 9–14; task 1.2; PATCH mismatch explicitly retained above.
- AC3 validation/errors/cancellation → delta 9,16–19; design 54; task 1.2 and shared HTTP behavior.
- AC4 no replay/unknown outcome/isolation → delta 21–24; tasks 1.2–1.3.
- AC5 permissions/backend scope → delta 26–38; task 1.3, with actual route/action verification delegated to UI owners.
- AC6 mocks → design 62, tasks 1.4, 2.1–2.2 and inherited demo requirements; no dedicated Feedback mock scenario is claimed.
- AC7 real API/CORS → task 2.3 and design 77–81; release evidence remains required.
- Deferred saved-filter/CSV clients and UI ownership → proposal 9–24, design 29–43; no neighboring scope absorbed.

The report's owners are responsibility slices, not assigned individuals or evidence of implementation. API/implementation lanes remain independent prerequisites for broader conclusions, not blockers to the textual findings.

## Architecture

Planned UI consumers → public entities/feedback DTO/client/query interfaces → existing shared HTTP and session owner/generation mechanisms. Express fixtures are a separate local path. UI permission visibility is not request authorization; mocks and generated DTO are neither mounted frontend behavior nor deployment evidence.

## Start Here

`openspec/changes/mos-1249-feedback-api/tasks.md:3–14`, beside `design.md:21–23`. The smallest supported planning diff is only task 1.1 wording, task 1.4's existing-handler premise, and the trailing migration paragraph. Keep all seven `[ ]` states. F5 may remain a separate optional refinement. No evaluated files were changed.

## Residual risks and actual validation

All reported input hashes matched; the saved Jira hash matches revision-1 metadata. This is local-byte freshness only, not fresh external Jira/API verification. Comments, attachments and custom fields are absent from the extraction. Runtime handler correctness, frontend completeness, real endpoints/null/errors/scope/CORS and deployment ownership remain unverified. Historical archive test results are not test results of this review. Prior R-MOS-1250 runtime observations were read only as attributed bounded evidence.

Used read/find plus non-interactive git, sha256sum and wc inspection. Git index path output was empty; worktree cleanliness is not asserted. No tests, source execution, build, typegen, network/browser/E2E inspection, nested agents, or project writes occurred. Only this configured output was written. Parent must recheck freshness before publication.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently read primary planning/archive sources and full auth/demo prerequisites; verified F1–F6 and seven-task mapping; all 37 reported input hashes and reference HEAD match."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/2c0ab53c-6d8b-4fef-ae97-035408969060/task-1.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"read/find primary planning and archived prerequisites","result":"passed","summary":"Complete required artifacts read; selected Jira item and decision paragraphs checked."},
    {"command":"git rev-parse HEAD; git diff --cached --name-only; sha256sum scoped inputs; wc -l","result":"passed","summary":"HEAD matched; index path output empty; every report-table input hash matched."},
    {"command":"Tests/build/typegen/network/browser/source execution","result":"not-run","summary":"Prohibited by read-only review scope."}
  ],
  "validationOutput": ["ACCEPT bounded SPEC report; no stale inputs or mandatory report corrections.","F1/F2 support a minimal tasks-only wording correction; all feature tasks remain unchecked."],
  "residualRisks": ["External freshness and omitted Jira fields remain unknown.","Runtime/API/deployment correctness is outside this lane; release gate remains open.","Main HTTP historical wording requires separate parent disposition; no main-spec edits authorized."],
  "noStagedFiles": true,
  "diffSummary": "Only configured independent review output written; no evaluated artifacts changed.",
  "reviewFindings": ["No blockers to accepting the bounded analytical report.","Accept F1/F2 corrections, F3/F4/F6 no-ops and F5 optional precision without scope or checkbox changes."],
  "manualNotes": "Fresh SPEC-only review. Reviewer acceptance is not parent publication or feature completion. All file contents were inspected through read; no sed/cat inspection, execution checks or runtime absence claims."
}
```
