# Code Context

## Independent review — MOS-919

**Verdict: ACCEPT (bounded documentary reconciliation only).** No mandatory corrections to the original report identified. This is not acceptance of implementation, runtime availability, API activation, Jira completion or a new product plan. Original report and planning/source artifacts were not edited.

## Files Retrieved

All paths are repository-relative. Serialized evidence is located by JSON pointer and wiki section rather than misleading long-line excerpts.

- `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-919.md` (lines 1–130, complete): original report, including its acceptance attestation.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MOS-919.md` (1–8), `R-REPORTS-WAVE.md` (complete), and `REPORTS-PUBLICATION-HANDOFF.md` (complete), in the same work-items directory: assignment and absence-not-blocker clarification.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-reports-details/r1/content.json`, `/items/1` and `/items/3`, and complete `metadata.json`: MOS-885 requested backend scope and MOS-919 requirements.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241085838/r1/content.json`, `/version` and `/bodyView` (complete inert text, especially §§1.1–1.2, 1.5–1.6, 2.4–2.8), and complete `metadata.json`: positive published report contract.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (serialized line 1, path/schema discovery and exact report-symbol checks), complete `metadata.json`: bounded absence verification.
- `openspec/changes/mos-919-report-csv-export/proposal.md` (1–30), `design.md` (1–65), `tasks.md` (1–13), `specs/report-export-availability/spec.md` (1–28), all complete.
- `openspec/specs/dialog-export/spec.md` (1–115), complete: distinct export ownership and existing safeguards.
- `docs/api/contracts/README.md` (1–33), `docs/api/contracts/reports.md` (1–5), complete: historical provenance/absence, not a report contract.
- Complete `proposal.md` (1–38), `design.md` (1–171), and all six specs under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/specs/`: `control-center-api-integration/spec.md` (1–64), `control-center-http/spec.md` (1–71), `control-center-mock-server/spec.md` (1–27), `control-center-permissions/spec.md` (1–89), `control-center-shell/spec.md` (1–101), `mpmm-session/spec.md` (1–138). Also complete archived `tasks.md` (1–52).
- Complete `proposal.md` (1–28), `design.md` (1–70), and all three specs under `openspec/changes/archive/2026-10-09-add-local-session-demo/specs/`: `control-center-mock-server/spec.md` (1–106), `control-center-shell/spec.md` (1–55), `local-session-demo/spec.md` (1–123).
- `docs/mpmm-auth-rollout.md` (1–58), complete: final approval evidence, distinguished from older open-gate language.

## Key Code / Evidence

No application code was inspected. Independent SHA-256 recomputation matched saved metadata:

| Capture | SHA-256 |
|---|---|
| jira-reports-details/r1 | `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c` |
| wiki-241085838/r1 | `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74` |
| api-live/r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |

Wiki content and metadata agree on version 3, dated 2026-09-09T17:12:02.625+08:00; body identifies contract v1.0 dated 08.09.2026. The saved live capture has no report path/schema name; exact `report-preview`, `report-export`, `field_codes`, and `ReportParameters` strings are absent. No newer revision was assumed or fetched.

### Seven-candidate independent check

1. **C919-01 preserved:** wiki §§1.1, 2.4–2.5 define identical preview/export input: inclusive dates, nullable channel, ordered nonempty field_codes. §1.5 limits the displayed preview to five selected columns and 12 rows and separately defines total. Full-selection export is an existing explicit acceptance obligation in `design.md:47–48,60`, not proof of a working backend. Report correctly rejects CSV reconstruction from the preview sample.
2. **C919-02 preserved:** wiki §§1.2, 1.6 explicitly require selected order and one row per dialog; `design.md:49–50,60–62` preserves multiline cells without extra records.
3. **C919-03 preserved:** wiki §§1.6, 2.5 specify UTF-8 BOM, semicolon, doubling embedded quotes, quoting quote/semicolon/newline-bearing cells, empty missing values, constructor name `отчёт_YYYY-MM-DD_YYYY-MM-DD.csv`, HTTP 200 and `text/csv; charset=utf-8`, without JSON wrapping. Byte preservation is explicitly required by `design.md:61–62`; report does not invent client re-encoding.
4. **C919-04 preserved:** wiki §2.8 supplies the six listed error statuses/codes and envelope. `design.md:63` independently supplies rejection of malformed successful/non-2xx/JSON/HTML responses, pending protection, parameter retention and cleanup. These are not all claimed as wiki wire-protocol fields.
5. **C919-05 preserved:** MOS-919 `/items/3/description` excludes message-row and IDs export; `design.md:65` and `dialog-export/spec.md:33–35,61–63` establish separate ownership. Report correctly rejects importing dialog selection/chat_ids, 24-column defaults and parameters trailer.
6. **C919-06 preserved:** the same Jira description explicitly requires agreed report DTO extension for new conditions. Wiki §1.1 has no AND/OR, phrase scope, ranges, relative/all-time period or surface DTO. `design.md:38,58–60` preserves those future acceptance expectations separately, without silently translating surface to channel or dropping conditions.
7. **C919-07 preserved:** wiki §2.6 publishes template export separately; `design.md:36,54,65` and `tasks.md:13` assign template UI/selection to MOS-916 and do not make it a prerequisite for the unavailable action. This review does not expand into template/scheduler implementation.

## Architecture / Distinct seam challenge

The report properly keeps three layers separate: wiki publication, absence in the assigned saved OpenAPI, and the existing unavailable-action plan. `specs/report-export-availability/spec.md:9–28` still prohibits activation, hidden Enter submission, HTTP export, local CSV/Blob/download and false success. `tasks.md:3` additionally requires an implemented MOS-1015 base before apply; neither report nor review attests that base exists.

**Dialog-only protocol transfer was specifically challenged and rejected.** `openspec/specs/dialog-export/spec.md:86,98–115` mandates Content-Disposition attachment/filename*, Content-Length, nosniff, no-store, size checks, formula protection and actionable missing-header errors for dialog exports. Wiki report §§1.6/2.5 do not publish those header/formula rules. Original report lines 57 and 82 explicitly identify the gap and forbid inventing a report protocol by analogy. Its shared-transport preservation sentence must remain read with that qualification: preserve existing dialog safeguards and common session/error safety; do not declare undocumented report headers mandatory merely because a dialog downloader requires them. Future compatibility remains unresolved, not permission to weaken existing safeguards or patch server bytes.

MOS-885 `/items/1/description` requests an isolated fake-data provider and explicitly excludes real dialog integration. Requested DoD is not delivery evidence. Frontend Express fixtures are not that provider. Original report preserves all three distinctions.

Historical auth approval remains closed: archived auth `tasks.md:48–52` and `docs/mpmm-auth-rollout.md:5,24–34` record user confirmation on 09.10.2026, not agent-run real-environment checks or deployment. Older proposal/design/demo statements do not reopen it. This approval is not extended to report endpoints/file headers or fake-provider delivery. Shared real-session preparation, UI-only permissions, wildcard-only report visibility, backend authorization, no 401 replay, no 403 refresh, stale-owner isolation and credential-free local demo are correctly retained as agreed constraints, not newly verified runtime behavior.

## Mandatory corrections / Unsupported claims

**None.** No blocker or materially unsupported assertion identified within the assigned documentary scope. No product/source correction is authorized by this verdict.

Original report disclaims working-tree/index verification and does not assert `noStagedFiles:true`. That is appropriate. This review likewise leaves index state unverified; not staging files during a run is not evidence that the index is empty.

## Start Here / Bounded owner questions

Start with `openspec/changes/mos-919-report-csv-export/design.md:38–65` for any parent-owned reconciliation, retaining the current unavailable-action spec. Existing questions remain bounded: report-specific filename/header exposure and file-safety agreement; empty-export/size behavior; advanced DTO agreement with MOS-1015. These are future contract/ownership questions, not missing-input blockers and not a proposed new implementation plan.

## Remaining evidence limits

No network, MCP, browser, credentials, product code, tests, build, generation, runtime checks, git/index inspection, task closure or source-precedence decision. Local hashes establish saved-byte integrity, not remote origin/runtime state. The optional dialog wiki was unnecessary: the complete main dialog spec provides the preservation boundary. Only this designated review artifact was written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently checked all seven CSV candidates against primary captures and complete MOS-919 planning, challenged dialog-only protocol transfer, and preserved historical auth approval and evidence limits."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-919.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python JSON/hashlib inspection of the three assigned captures","result":"passed","summary":"Three digests matched metadata; wiki version confirmed; saved report paths/schema names and four exact report symbols absent."},
    {"command":"Read-only artifact inspection with read, find, cat and nl","result":"passed","summary":"Original report, work items, primary evidence, complete relevant plans/specs and historical approval inspected; handoff found in work-items after initial parent-directory lookup failed."},
    {"command":"Tests/build/network/browser/MCP/runtime validation","result":"not-run","summary":"Excluded by assignment."}
  ],
  "validationOutput": ["ACCEPT, bounded documentary review; no mandatory corrections."],
  "residualRisks": ["Report runtime and fake-provider delivery remain unknown.","Report file-safety/header protocol, advanced DTO and export limits remain unresolved.","Index and working-tree state unverified; no empty-index attestation."],
  "diffSummary": "Designated review artifact only; original report and product/source/planning artifacts preserved.",
  "reviewFindings": ["No blockers or mandatory corrections within scope."],
  "manualNotes": "Read complete prerequisites before auth/mock conclusions. Historical 09.10.2026 approval remains closed without extension to reports. No implementation validation claimed."
}
```
