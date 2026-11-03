# Code Context

## SCENARIO-MOS-919 — bounded report-builder CSV reconciliation

**Result:** MOS-919 and the captured report wiki support a concrete, server-produced, row-per-dialog CSV candidate. The active MOS-919 plan still authorizes only an unavailable action. The saved live OpenAPI contains no report preview/export operations or report DTOs. This is a publication/plan difference, not evidence of delivery, permission to activate export, a source-precedence decision, or Jira closure.

Only this report was written. No application code audit, network/MCP/browser, tests, builds, generation, git mutation, credentials inspection, or product/spec edits were performed. HTML was treated as inert text. Supervisor confirmed that absent operations in the assigned live revision are a valid finding, not a reason to fetch another revision.

## Files Retrieved

Paths below are repository-relative. JSON pointers/section names qualify long serialized source lines.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MOS-919.md` (lines 1–8): bounded assignment.
2. `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (routing table and main capability inventory): used only to locate active MOS-919 and main dialog-export artifacts; inventory attestations were not adopted.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-reports-details/r1/content.json` (`/items/1`, MOS-885, key at line 32; `/items/3`, MOS-919, key at line 68) and `metadata.json` (complete): only those two issue records analyzed.
4. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241085838/r1/content.json` (lines 1–64; `/version`, `/bodyView`, §§1.1–1.2, 1.5–1.6, 2.4–2.5, 2.8; template/access text only for boundary context) and `metadata.json` (complete): report parameters, CSV semantics and errors. Unrelated template/scheduler text encountered during inert extraction was not analyzed.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1; path/schema-name discovery and exact report-symbol absence checks only) and `metadata.json` (complete): bounded published-operation absence.
6. `openspec/changes/mos-919-report-csv-export/proposal.md` (lines 1–30), `design.md` (1–65), `tasks.md` (1–13), `specs/report-export-availability/spec.md` (1–28): matching active artifacts fully read.
7. `openspec/specs/dialog-export/spec.md` (lines 1–115): fully read; distinct owner and existing file/error/security safeguards, not a report DTO substitute.
8. `docs/api/contracts/README.md` (lines 1–33), `docs/api/contracts/reports.md` (1–5): independently read local historical provenance notes, not a report API contract. Existing contract filenames enumerated; no assumed newer OpenAPI sought.
9. Mandatory auth prerequisites, fully read under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: `proposal.md` (1–38), `design.md` (1–171), `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138). Additionally `tasks.md` (44–52), for release evidence.
10. Mandatory demo prerequisites, fully read under `openspec/changes/archive/2026-10-09-add-local-session-demo/`: `proposal.md` (1–28), `design.md` (1–70), `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123).
11. `docs/mpmm-auth-rollout.md` (lines 1–58): complete release-status evidence.

## Provenance and integrity

SHA-256 was recomputed from saved bytes, not inferred from filenames or collection claims:

| Capture | Recomputed SHA-256 | Version/provenance boundary |
|---|---|---|
| jira-reports-details/r1 | `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c` | Matches assignment and metadata. Collection 2026-10-16T13:31:43.125Z. MOS-885 updated 2026-10-16T19:20:12.520+0800; MOS-919 updated 2026-10-15T14:16:14.331+0800. Both captured as Backlog, no comments/attachments. These are snapshot fields, not current external status verification. |
| wiki-241085838/r1 | `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74` | Matches assignment and metadata. Content and metadata agree on page version 3, 2026-09-09T17:12:02.625+08:00; body identifies contract v1.0 dated 08.09.2026. Captured 2026-10-16T13:31:51.607Z, status 200; linked by the two issue descriptions. |
| api-live/r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | Matches metadata. Captured 2026-10-16T11:13:29.451Z from the Swagger-linked `/api/control/openapi.json`; OpenAPI 3.1.0, service version 0.1.0. No ETag/Last-Modified. Metadata describes credential-free public-document capture; no business call or origin re-verification performed here. |

The Jira/wiki metadata describes parent verified-origin GET collection and expressly limits publication versus runtime/approval. This audit verifies local content integrity and internal version agreement, not the remote state or original collection process.

`docs/api/contracts/reports.md` SHA-256: `f7da16e382bd0dd53ce7fdf53e345fc6ffcc29f761630f5828a687e544aa9a89`. It says supplied `message.txt` lacked reports and no speculative methods/parameters/schemas were added. README names its separate 15.10.2026 live snapshot/hash and says reports are absent. These are local historical absence/provenance notes, **not negation of the newly captured wiki publication**, nor a report-specific saved contract.

## Key Code / Contract candidates

No code was inspected. The critical published request shape is a report-specific parameter object, not dialog selection:

```json
{
  "period": { "date_from": "YYYY-MM-DD", "date_to": "YYYY-MM-DD" },
  "channel_id": null,
  "field_codes": ["chat_id", "channel", "started_at"]
}
```

Wiki §1.1: dates inclusive, start not after end; null channel means all channels; at least one field, ordered `field_codes`. Wiki §2.4 describes POST `/api/control/api/analytics/v1/report-preview`; §2.5 describes POST `/api/control/api/analytics/v1/report-export` with the **same body**. These are positively supported wiki definitions, not endpoints confirmed in the saved live schema or at runtime.

| Candidate | Primary evidence | Existing exact plan/spec mapping | Supported versus unresolved |
|---|---|---|---|
| C919-01: server CSV uses the same logical report parameters as preview | MOS-919 description; MOS-885 requested DoD; wiki §§1.1, 2.4–2.5 | `design.md:47–48,60` E02/E03, B919.1; active spec `No simulated export side effects`, lines 21–28 | Period/channel/ordered fields positively described. Full report is not the 12 preview rows or first five displayed columns (§1.5). No frontend pagination/detail crawl or CSV reconstruction. Current-input/stale-preview protection remains required; no agreed advanced DTO extension is supplied. |
| C919-02: preserve selected column order and one row per dialog | MOS-919; MOS-885 DoD; wiki §§1.2,1.6 | `design.md:49–50,60–61` E04/E05, B919.1/B919.2 | `field_codes` determines preview and CSV order; row-per-dialog is explicit. A wrapped/multiline CSV cell must not become extra dialog records. |
| C919-03: preserve server-produced file format and name | MOS-919; wiki §§1.6,2.5 | `design.md:49,61–62` B919.2/B919.3; `proposal.md:14` | UTF-8 BOM, semicolon, quoted cells for quote/semicolon/newline, doubled embedded quotes, missing values empty. Constructor filename rule is `отчёт_YYYY-MM-DD_YYYY-MM-DD.csv`. Wiki specifies 200 and `text/csv; charset=utf-8`, no JSON wrapper. Header-level filename delivery/CORS exposure, response-length/cache/nosniff protocol, limits, empty-export behavior and formula escaping are not specified here. Do not invent them or weaken existing safety gates. |
| C919-04: failures are not downloads or success | wiki §2.8; existing B919.4 | `design.md:52,63`; `tasks.md:4,9,13`; spec lines 21–28 | Wiki documents 400 INVALID_ARGUMENT, 401 UNAUTHENTICATED, 403 FORBIDDEN, 404 NOT_FOUND (including unavailable channel), 422 VALIDATION_ERROR, 500 REPORT_BUILD_FAILED; envelope `code,data:null,message,errors[]`, optional error `field`. JSON/HTML/non-2xx/malformed successful response must not be saved as CSV. Keep parameters, pending/repeated-click protection, cleanup and truthful outcome; exact additional limits/statuses are not invented. |
| C919-05: no duplicate message-row or selected-IDs export | MOS-919 explicit exclusion | `proposal.md:14`; `design.md:53,65`; `tasks.md:13`; main `dialog-export/spec.md:9–35,61–96` | Those scopes belong to dialog-export; its selection/chat_ids and messages options are not report fields. Do not import its 24-column schema, include_parameters trailer, cardinality rules or HTTP status set into report-export by analogy. |
| C919-06: new conditions require agreed report DTO extension | MOS-919 explicit gate; wiki §1.1 bounded object | `design.md:38,58–60`; `tasks.md:13` | Existing B919.1 mentions period modes, surface, AND/OR, ranges, phrase scope and all-time. The captured report contract only supplies dates/channel/fields. Do not silently map surface to channel, pass dialog selection into report-export, drop advanced conditions, or claim advanced acceptance is supported. Keep this separate blocked dependency on MOS-1015. |
| C919-07: template export has separate UI ownership | wiki §2.6 only as dependency context; current plan boundary | `design.md:54,65`; `tasks.md:13` assign template selection/UI to MOS-916 B916.4 | Reuse of a future confirmed file path is a planning boundary, not permission to implement template export or scheduling here. MOS-916/MOS-1016 are not prerequisites for the current unavailable-action delivery (`design.md:36`). |

### Saved live schema comparison

Within `api-live/r1`:

- Path discovery found **no report path**, including no report-preview/report-export operation.
- Schema-name discovery found **no report schema** (case-insensitive `report`). Exact serialized checks for `report-preview`, `report-export`, `field_codes`, and `ReportParameters` were all absent.
- Analytics paths exist for dashboard, dashboard refresh, widgets and board. Their existence does not provide report-builder DTOs.
- Consequently no matching report operationId, request/response schema or referenced DTO closure can be extracted from this revision. No guessed DTO names or later revision were substituted.

The wiki, Jira requested scope, local historical absence notes and live snapshot answer different questions. No source is declared authoritative over another; absence from this saved schema does not disprove wiki publication or prove runtime unavailability.

### Requested backend scope is not actual delivery

MOS-885 requests backend templates/configuration/preview/metrics/CSV/validation/user visibility. It explicitly excludes real dialog-data integration and requests an isolated provider interface backed by fake data for implementation/testing. Its DoD wording is a requested acceptance target, **not proof these items are implemented**. Neither the Backlog capture, wiki publication nor saved OpenAPI establishes actual fake-provider delivery, real-data availability, deployment, successful export, or MOS-919 completion. Local Express fixtures are a separate frontend development facility and must not be equated with this requested backend fake provider.

## Architecture and preserved gates

Current active owner is `report-export-availability`: permanently explained disabled action, independent of valid/invalid draft; no HTTP export, local Blob/CSV, object URL/download, hidden Enter submit, success message or draft reset. B919.1–B919.4 are future acceptance criteria, explicitly not current implementation checkboxes. The captured wiki fills some facts formerly treated as unknown; it does not itself change that approved scope.

Main `dialog-export/spec.md:84–115` already protects server bytes, BOM, CSV MIME/UTF-8, filename sanitization, response headers/length, Object URL lifecycle and formula-protected content, with actionable missing-header errors. Preserve these existing dialog requirements unchanged. Report wiki silence about formula protection or its file-header protocol is a reconciliation gap, not permission to bypass safety or manufacture a report-specific protocol from dialog requirements. Shared transport reuse must retain security/error checks while report-specific compatibility is explicitly resolved; frontend CSV encoding or patching server bytes is not the remedy.

Mandatory auth/demo prerequisites establish:

- Configuration selects mock versus real; production and dev opt-out use real shared MPMM session. Hostname does not enable/disable auth. Credential destination safety remains separate.
- Permissions control UI only; reports remain explicit-wildcard-only until granular mapping is separately agreed. Wiki role labels do not create frontend role grants or new permissions. Backend owns object scope and request authorization; no request ACL/local synthetic 403 is introduced.
- Real binary requests share session preparation and permitted destinations; preserve 401 recovery without replay, 403 without refresh, owner/generation isolation, current-input checks and suppression of late downloads. An uncertain/cancelled response is not proof the server did nothing; no invented success or automatic replay.
- Local demo is credential-free, uses confirmed fixture principal and fixed response scenarios, does not enforce backend roles, and cannot turn unavailable API into successful export. No production mocks, refresh simulation, new auth model or role editor.

**Release status preserved:** `docs/mpmm-auth-rollout.md:3–5,24–34` and archived auth `tasks.md:48–52` record the user's 09.10.2026 approval (“Подтверждаю пункт и архивацию”). Do not reset that gate based on older proposal/design statements that it was open. The recorded basis is user confirmation, not agent-performed real HTTP/config/server checks; archiving did not establish deployment. This audit neither extends that prior approval to report endpoints, report-header/CORS behavior, fake-provider delivery or new deployment conditions, nor revokes it. No new runtime verification was performed.

## Start Here

Open `openspec/changes/mos-919-report-csv-export/design.md:38–65`, then its proposal/spec. That is the smallest owner for reconciling E02–E08/B919.1–B919.4 against the wiki without silently activating an export handler.

### Narrow factual correction / no-op questions for subsequent review

1. Can the MOS-919 rationale distinguish “report API is now described in captured wiki v1.0” from “absent in saved live OpenAPI and not connected/approved for this plan,” while retaining disabled/no-side-effects requirements? This is a factual-evidence correction candidate, not a proposed activation.
2. Can B919.1 explicitly separate the published baseline date/channel/field object from advanced conditions pending an agreed report DTO extension, without erasing original acceptance expectations?
3. Can B919.2/B919.3 mark MIME, BOM, delimiter, quoting, null and constructor filename rule as documented, while retaining unresolved file-header/CORS, formula-safety, size and empty-export questions? No file protocol should be inferred.
4. No-op: retain dialog-export ownership, template UI ownership, current-input/error/unknown-outcome checks, existing auth/demo constraints and prior release approval. Do not create duplicate tasks or close MOS-919 because its unavailable action is planned.

## Residual risks and validation limits

- Published report protocol lacks a matching operation/schema in the assigned live capture; no runtime claim can be made.
- Formula-safety and complete report file-delivery protocol remain unresolved; advanced conditions need explicit DTO agreement. These are future product/contract decisions, not blockers to completing this bounded report.
- Report implementation, delivery status and real-data availability were deliberately not audited. No product checks were run under this read-only assignment.
- Optional linked dialog wiki was not needed: existing main dialog-export spec supplies the ownership and preservation boundary; no linked credentials/examples were inspected.
- Hashes were verified locally; remote origin/state and working-tree/index state were not independently attested.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped seven bounded CSV candidates to MOS-919 E/B criteria, active requirements and dialog ownership; verified all three assigned capture hashes and preserved explicit residual gaps."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-919.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python hashlib/json inspection of assigned captured content and metadata","result":"passed","summary":"All three capture digests matched; wiki version 3/contract v1.0 identified; only MOS-885 and MOS-919 issue records analyzed."},
    {"command":"Read-only saved live path/schema discovery and exact report-symbol checks","result":"passed","summary":"No report paths/schema names; report-preview, report-export, field_codes and ReportParameters absent."},
    {"command":"Read-only artifact reads and local contract filename enumeration","result":"passed","summary":"Matching active artifacts, main dialog-export spec, mandatory auth/demo prerequisites and recorded release approval read; reports.md is an absence note, not a contract."},
    {"command":"Tests/build/browser/network/generation","result":"not-run","summary":"Forbidden by the bounded assignment; no implementation validation claimed."}
  ],
  "validationOutput": ["Positive wiki report contract evidence separated from live-schema absence and requested fake-provider scope.","Prior 09.10.2026 user release approval preserved without extending it to report delivery."],
  "residualRisks": ["Report runtime availability and backend fake-provider delivery remain unknown.","Advanced report DTO and complete file safety/delivery contract remain unresolved.","No application implementation or remote-state verification performed."],
  "diffSummary": "Only the authoritative report artifact written; no product/source/spec edits.",
  "reviewFindings": ["No blocker to bounded audit completion; future activation remains outside this report."],
  "manualNotes": "Supervisor resolved the missing-live-operation question by directing bounded absence reporting. No git/index attestation is made. Source HTML was read as inert text; no credentials were extracted."
}
```
