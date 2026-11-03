# Code Context

## LOCAL-001 — read-only local inventory

Completed local enumeration only. No tests, network, MCP, code/spec edits, git commands, mutations, or nested agents. This report is the sole output artifact.

### Counts

| Inventory | Count |
|---|---:|
| Main capability directories, each containing `spec.md` | 40 |
| Active change directories, each containing `proposal.md` | 21 |
| Product active changes | 20 |
| Managing/process active change | 1 |
| Archive directories | 41 |
| Files under archive directories | 498 |
| Archive files including root `.gitkeep` | 499 |
| Distinct literal Jira MOS keys in active proposals | 25 |
| Initial baseline entries | 647 |
| Missing baseline paths | 0 |

Snapshot contained 690 OpenSpec files: 43 beyond baseline, all under managing change `audit/`. This snapshot precedes report creation and can change as other audit artifacts arrive. Baseline categories: main specs 41 files (40 specs + `.gitkeep`), archive 499, product active changes 101, managing change 5, root `openspec/config.yaml` 1. No baseline hashes were recomputed; presence is not integrity verification.

## Files Retrieved

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/LOCAL-001.md` (lines 1–9): inventory authority, inputs, acceptance and stop conditions.
- `openspec/changes/reconcile-control-center-backlog/audit/README.md` (lines 1–25): audit ownership, initial 647-file baseline and read-only scope.
- `openspec/changes/reconcile-control-center-backlog/audit/baseline-files.json` (entire JSON parsed by read-only Python; first 30 lines viewed): path-presence and category-count comparison.
- `openspec/changes/reconcile-control-center-backlog/proposal.md` (lines 1–30): process/product distinction, particularly lines 7–12 and 18–22.
- All 21 active `proposal.md` files: read by local Python for literal key extraction; line ranges supporting results are listed below. Main spec and archive contents were not semantically reviewed.

## Main capability IDs

Each ID below resolves to exact path `openspec/specs/<ID>/spec.md`; all 40 exist. Main root also contains `.gitkeep`, not a capability.

```text
ab-testing-editor
ab-testing-export
ab-testing-module
ab-testing-registry
code-quality-gates
control-center-api-integration
control-center-http
control-center-mock-server
control-center-permissions
control-center-shell
dialog-answer-insights
dialog-category-addition
dialog-details
dialog-export
dialog-registry
dialog-route
dialog-saved-filters
dialog-selection-builder
documentation-search
knowledge-base-editor
knowledge-base-export
knowledge-base-module
knowledge-base-registry
local-session-demo
mpmm-session
skill-bulk-rollout
skill-card-editing
skill-catalog-experience
skill-checks-training
skill-connection-settings
skill-domain-management
skill-global-toggle
skill-lifecycle
skill-registration
skill-review
skill-training-phrases
surface-lifecycle-publication
surface-overview-connection
surface-registration
surface-skill-selection
```

## Active changes and routing evidence

Every row resolves to `openspec/changes/<change>/proposal.md`. Line numbers identify literal Jira references, not proof of implementation, acceptance, dependency satisfaction or Jira membership. The primary product key is the directory's `mos-N` prefix; other references may denote dependencies, parents or exclusions.

| Change | All literal Jira keys in proposal | Evidence lines |
|---|---|---|
| mos-1015-report-constructor | MOS-1015, MOS-1016, MOS-916, MOS-919 | 3, 12, 16 |
| mos-1016-report-template-scheduling | MOS-1015, MOS-1016, MOS-916, MOS-919 | 3, 11, 30 |
| mos-1018-skill-phrase-conflicts | MOS-1018, MOS-1019, MOS-942, MOS-945 | 3, 10, 24, 27 |
| mos-1023-skill-environment-tokens | MOS-1019, MOS-1023 | 3, 26–27 |
| mos-1025-skill-monitoring | MOS-1025, MOS-1026, MOS-1030 | 3, 10, 26–27 |
| mos-1026-skill-operations-info | MOS-1025, MOS-1026 | 3, 24, 27 |
| mos-1030-skill-result-analytics | MOS-1025, MOS-1030 | 3, 11, 28 |
| mos-1031-skill-audit-history | MOS-1031 | 3, 27 |
| mos-1249-feedback-api | MOS-1246, MOS-1249, MOS-1259, MOS-1260 | 3, 5, 9, 20 |
| mos-1250-feedback-registry | MOS-1246, MOS-1249, MOS-1250, MOS-1258 | 3, 5, 9, 14, 16, 22, 32 |
| mos-1251-feedback-editor | MOS-1246, MOS-1249, MOS-1251, MOS-1254, MOS-1257 | 3, 5, 9, 22, 32, 34 |
| mos-1254-feedback-questions | MOS-1246, MOS-1249, MOS-1251, MOS-1254, MOS-1255 | 3, 5, 9, 14, 20, 30, 32 |
| mos-1255-feedback-preview | MOS-1246, MOS-1251, MOS-1254, MOS-1255 | 3, 5, 30, 32 |
| mos-1256-feedback-lifecycle | MOS-1246, MOS-1250, MOS-1251, MOS-1256 | 3, 5, 32 |
| mos-1257-feedback-labels | MOS-1246, MOS-1251, MOS-1257 | 3, 5, 30, 32 |
| mos-1258-feedback-conditions | MOS-1246, MOS-1249, MOS-1250, MOS-1258 | 3, 5, 9, 22, 32 |
| mos-1259-feedback-saved-filters | MOS-1246, MOS-1250, MOS-1258, MOS-1259 | 3, 5, 30 |
| mos-1260-feedback-export | MOS-1246, MOS-1249, MOS-1250, MOS-1251, MOS-1258, MOS-1260 | 3, 5, 16, 32 |
| mos-916-report-templates | MOS-916, MOS-919 | 3, 11, 29 |
| mos-919-report-csv-export | MOS-1015, MOS-1016, MOS-916, MOS-919 | 3, 10, 14, 28 |
| reconcile-control-center-backlog — managing, not product | MOS-623 | 7, 27 |

Routing buckets by local naming: reports 4 product changes, skills 6, feedback 10; managing process 1. `mos-916-report-templates/proposal.md:29` also references lowercase change ID `mos-1015-report-constructor`; that is a routing link, not an additional literal uppercase Jira key in that proposal. Broad identifier extraction produced `UTF-8` in CSV proposal line 14: explicitly excluded as an encoding, not Jira.

### Unmatched references and exclusions

Five referenced Jira keys have no matching primary active-change directory; none is silently dropped:

- MOS-1019: referenced by skill conflicts/tokens; archive name `2026-10-02-mos-1019-skill-checks-training` offers historical routing.
- MOS-945: referenced by skill conflicts; archive name `2026-09-30-mos-945-skill-training-phrases` offers historical routing.
- MOS-942: referenced by `mos-1018-skill-phrase-conflicts/proposal.md:10`; no active or archive directory explicitly names this key. Keep as unresolved local routing, not proof of missing implementation.
- MOS-1246: feedback proposals line 5 identify a wider task group; retain as group-level reference, not a fabricated active product change.
- MOS-623: managing proposal lines 7 and 27 identify audit scope root; retain in process routing, exclude from product-change total.

All main capability IDs and all archive directories are retained, including technical/support capabilities and names without Jira keys. No main-capability-to-Jira completeness claim is made. No active directory lacks a proposal. Managing capability `control-center-backlog-reconciliation` is declared at `openspec/changes/reconcile-control-center-backlog/proposal.md:18`; it is not among the 40 main specs and is not counted as product behavior.

## Archive directory inventory

Each row is an exact directory under `openspec/changes/archive/`; counts include all recursively enumerated files, including dotfiles. Root `.gitkeep` is additional to these directories.

| Directory | Files |
|---|---:|
| 2026-09-23-connect-control-center-http-client | 7 |
| 2026-09-23-improve-code-quality | 5 |
| 2026-09-24-update-control-center-shell | 5 |
| 2026-09-25-defer-auth-and-role-access | 8 |
| 2026-09-25-enforce-fsd-code-decomposition | 5 |
| 2026-09-28-surface-registry | 5 |
| 2026-09-28-update-assistant-modules-contract | 5 |
| 2026-09-28-update-control-center-routing | 5 |
| 2026-09-29-mos-944-skill-card-editing | 5 |
| 2026-09-30-merge-assistant-modules-contract-preserve-intents | 5 |
| 2026-09-30-mos-1022-skill-connection-settings | 5 |
| 2026-09-30-mos-911-surface-skill-selection | 5 |
| 2026-09-30-mos-945-skill-training-phrases | 5 |
| 2026-10-01-skills-prototype-alignment | 252 |
| 2026-10-01-skills-status-and-registration-recovery | 8 |
| 2026-10-02-mos-1019-skill-checks-training | 5 |
| 2026-10-02-mos-1020-skill-review | 6 |
| 2026-10-02-mos-909-skill-current-status | 5 |
| 2026-10-02-mos-909-skill-lifecycle-rollout | 8 |
| 2026-10-02-mos-911-prod-skill-selection | 5 |
| 2026-10-05-mos-1021-skill-bulk-rollout | 5 |
| 2026-10-05-mos-1037-dialog-registry | 5 |
| 2026-10-05-mos-1038-dialog-selection-builder | 5 |
| 2026-10-06-mos-1040-dialog-saved-filters | 5 |
| 2026-10-06-mos-1041-dialog-details | 6 |
| 2026-10-06-mos-1042-dialog-answer-insights | 5 |
| 2026-10-07-mos-1044-dialog-category-addition | 5 |
| 2026-10-07-mos-913-surface-lifecycle-publication | 5 |
| 2026-10-07-mos-913-surface-overview-connection | 5 |
| 2026-10-09-add-local-session-demo | 7 |
| 2026-10-09-integrate-mpmm-auth-permissions | 10 |
| 2026-10-12-mos-914-surface-lifecycle-mvp | 6 |
| 2026-10-13-mos-1027-skill-global-toggle | 5 |
| 2026-10-13-mos-1043-dialog-route | 5 |
| 2026-10-13-mos-1045-dialog-export | 5 |
| 2026-10-13-mos-906-documentation-search-url | 6 |
| 2026-10-13-update-control-center-contracts-put | 9 |
| 2026-10-14-add-optional-knowledge-base | 11 |
| 2026-10-15-add-optional-ab-testing | 11 |
| 2026-10-15-update-control-center-api-contracts | 11 |
| 2026-10-16-fix-existing-scenarios-test-contour | 7 |

## Key Code / Architecture

No application code retrieved: this is planning inventory. Main `openspec/specs/` supplies capability IDs; non-archive `openspec/changes/` supplies current proposal routing; `openspec/changes/archive/` supplies historical directories. The managing change explicitly separates reconciliation from business behavior and owns the audit packet. Directory presence and archive placement do not establish implementation completeness.

## Start Here

Use the active-proposal table for product routing and `openspec/changes/reconcile-control-center-backlog/proposal.md:18–22` to preserve managing/product separation. Carry MOS-942 into unresolved routing rather than dropping it.

## Limitations

No infrastructure failures. Work-item HEAD was not independently verified; git inspection was outside this run. No hash integrity check, external hierarchy verification, implementation review, spec semantic comparison or tests performed. Counts are a local snapshot; concurrent audit files may change total-file counts. Orphan classification is limited to explicit local directory names and proposal references.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Enumerated 40 main capabilities, 21 active changes (20 product plus 1 managing), 41 archive directories and all 25 literal Jira keys; retained five references without matching active directories."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only python3 pathlib/json/re inventory and baseline-path comparison (two invocations)","result":"passed","summary":"All 647 baseline paths present; 40 main specs, 21 active proposals, 41 archive directories and 499 archive files."}],
  "validationOutput": ["No active directory missing proposal.md; no main directory missing spec.md; 43 snapshot additions confined to managing audit packet."],
  "residualRisks": ["MOS-942 remains unmatched by explicit active/archive directory name.","External Jira scope, implementation status, baseline hashes and HEAD were not verified.","Audit artifact counts can change concurrently."],
  "noStagedFiles": true,
  "diffSummary": "Only the requested report artifact written; no source/spec changes or git operations.",
  "reviewFindings": ["No inventory blocker; unmatched references explicitly retained."],
  "manualNotes": "Read-only inventory completed without tests or external access. noStagedFiles denotes no staging performed by this worker, not inspection of pre-existing index state."
}
```
