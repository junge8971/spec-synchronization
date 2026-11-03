# Independent review — MOS-1016

## Verdict: ACCEPT

Accept **only the bounded evidence assessment and eleven-candidate mapping** in `audit/reports/SCENARIO-MOS-1016.md`, not implementation, activation, source precedence, deployment or Jira closure. No substantive unsupported claim or mandatory correction to the original report was established. Preserve the original. Its existing publication/timezone/auth qualifications are necessary, not optional permission to bypass the current boundaries.

## Code Context / files retrieved

Paths below are repository-relative; `A` = `openspec/changes/reconcile-control-center-backlog/audit`. No product code was inspected. Full reads, including continuations after truncated tool output:

- `A/reports/SCENARIO-MOS-1016.md` lines 1–143; `A/work-items/SCENARIO-MOS-1016.md` 1–5; `A/work-items/R-REPORTS-WAVE.md` 1–13; `A/work-items/REPORTS-PUBLICATION-HANDOFF.md` 1–7; `A/work-items/LOCAL-001.md` complete; `A/decisions.md` 1–95.
- `openspec/changes/mos-1016-report-template-scheduling/`: `proposal.md` 1–31, `design.md` 1–76, `tasks.md` 1–18, `specs/report-template-scheduling-draft/spec.md` 1–51.
- `openspec/changes/mos-1015-report-constructor/`: `proposal.md` 1–33, `design.md` 1–100, `tasks.md` 1–27, `specs/report-constructor-draft/spec.md` 1–128, `specs/dialog-selection-draft/spec.md` 1–116.
- `openspec/changes/mos-916-report-templates/`: `proposal.md` 1–31, `design.md` 1–74, `tasks.md` 1–18, `specs/report-template-access/spec.md` 1–47.
- `openspec/changes/mos-919-report-csv-export/`: `proposal.md` 1–30, `design.md` 1–65, `tasks.md` 1–13, `specs/report-export-availability/spec.md` 1–28.
- `openspec/specs/control-center-permissions/spec.md` 1–91; `openspec/specs/dialog-selection-builder/spec.md` 1–67; `openspec/changes/mos-1030-skill-result-analytics/proposal.md` 1–28.
- Complete archived prerequisites under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: proposal 1–38, design 1–171, tasks 1–52; specs `control-center-api-integration` 1–64, `control-center-http` 1–71, `control-center-mock-server` 1–27, `control-center-permissions` 1–89, `control-center-shell` 1–101, `mpmm-session` 1–138 (each `specs/<name>/spec.md`).
- Complete archived prerequisites under `openspec/changes/archive/2026-10-09-add-local-session-demo/`: proposal 1–28, design 1–70, tasks 1–26; specs `control-center-mock-server` 1–106, `control-center-shell` 1–55, `local-session-demo` 1–123. `docs/mpmm-auth-rollout.md` 1–58.
- Primary `A/sources/jira-reports-details/r1/content.json`: independently parsed only `/items/1` and `/items/5`; metadata complete. `A/sources/wiki-241085838/r1/content.json`: complete inert `/bodyView` and `/version`; metadata complete. `A/sources/api-live/r1/content.json`: `/paths`, five analytics operation bodies, their transitive schema-property/required-field closure, response-template schemas and exact report-path membership; metadata complete. JSON pointers and wiki section headings are the precise primary locators, not invented line ranges within embedded HTML or single-line OpenAPI.

Fresh bounded discovery of active proposals identified the same four report owners; main report-named capability discovery found none. MOS-1030 expressly excludes new reports. Inventory acceptance was not used as semantic proof.

## Independently verified primary evidence

| Saved source | SHA-256 / bytes | Version |
| --- | --- | --- |
| Jira reports details r1 | `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c` / 12996 | Items 1 and 5 Backlog; no comments or attachments for either |
| Wiki 241085838 r1 | `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74` / 37238 | Page revision 3, 2026-09-09T17:12:02.625+08:00; body v1.0, history 08.09.2026 |
| API live r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` / 413007 | OpenAPI 3.1.0, info.version 0.1.0; no ETag/Last-Modified |

All hashes and lengths matched saved metadata. Nothing here establishes the current remote publication or runtime.

Under `/api/control/api/analytics/v1`, wiki §§2.1–2.6 publish exactly:

1. GET `/report-constructor`
2. GET `/report-templates`
3. GET `/report-templates/{template_id}`
4. POST `/report-preview`
5. POST `/report-export`
6. POST `/report-templates/{template_id}/export`

Exact method/path membership was false for all six in saved OpenAPI. Explicit POST collection and PUT/PATCH detail checks were also false; these are verification spellings, not proposed APIs. This is a legitimate publication gap, not missing audit input or proof of backend nonexistence.

Wiki §1.4 positively defines nullable schedule, five-field cron, IANA timezone, nullable last_run, and launching-user/time/row-count metadata. Its Monday 09:00 Europe/Moscow example is **read representation**, not a default schedule-write policy. `last_run.by` is not ownership. No create/write, relative-period, worker lifecycle, run identity or stored-result retrieval protocol is supplied. Wiki §2.3 restores its limited parameters in order; §2.6 is bodyless direct CSV from saved parameters, not a background launch command. Absolute dates in §1.1 cannot silently become a recurring relative period.

The five published analytics operations are dashboard GET, dashboard refresh POST, widgets GET and board GET/PUT. Their operation descriptions and DTOs describe aggregates and personal widget-board composition. `SaveBoardRequest` requires version/widgets; `BoardResponse` requires version/is_default/widgets; `RefreshDashboardResponse` requires sample/calculated_at. None supplies report-template persistence or scheduler semantics. ResponseTemplateCreate/ResponseTemplateResponse have text/type/scope and skill/surface links: response templates, not reports. Schema definitions have no schedule/cron/last_run/field_codes properties. No dashboard grant, period rule or retry policy is transferable by analogy.

## Candidate coverage / key planning evidence

All eleven original IDs are supported as extracted candidates, not new approvals:

| IDs | Verified coverage and limit |
| --- | --- |
| MOS1016-01 | Name: S01/S03, B16.1/B16.5; local validation does not enable save. |
| MOS1016-02–04 | Ordered fields, surface and complex selection: S03/S05, B16.2. Wiki's 18-field parameters do not establish a 24-field mapping, surface-ID/channel-ID equivalence or condition serialization. |
| MOS1016-05 | Four intentions: S02/S07, B16.3; no agreed execution timezone/default or weekly/monthly time follows from read cron. |
| MOS1016-06 | Per-run period: S06/S07, B16.3; local monthly selection preserves absolute dates without promising their repetition or choosing “previous month.” |
| MOS1016-07 | Durable complete save/reread: S03–S05, B16.1/B16.2. Successful write followed by failed GET must not duplicate creation. |
| MOS1016-08–09 | Visibility/ownership and background result: S08/B16.4. Accessible-only reads and launching actor do not settle creation/sharing/edit rights, scheduled principal, failures or result storage. |
| MOS1016-10 | Settings-only frontend: S09/B16.3/B16.4; no browser timer authority. |
| MOS1016-11 | Jira `/items/1/description` requests an isolated fake backend provider for preview/metrics/CSV, validation/scope and template reads. Backlog/DoD is not delivery evidence; no scheduler delivery is specified or proven. |

Exact local acceptance: `mos-1016-report-template-scheduling/design.md` 55–74; active delta spec 7–51; six unchecked tasks at `tasks.md` 3–14. S10/B16.5 already preserves input/error/conflict/idempotency acceptance. **There is an existing plan and preserved continuation, not a missing-plan finding.** No duplicate plan is justified.

## Corrections, severity and preserved boundaries

**Mandatory corrections to original report: none. Unsupported material claims: none established.** No unsupported `noStagedFiles:true` appears in this report; it expressly leaves the index uninspected. That statement must remain: absence of staging actions cannot establish an empty index.

The following precision is mandatory for any downstream disposition, and is already substantially present in the report:

- Keep “published limited read model; no agreed full write/round-trip/execution contract,” not universal absence of template metadata. Primary locators: wiki §§1.1/1.4/2.2/2.3 versus saved OpenAPI `/paths`; local design 47 and 68–74.
- Qualify timezone/calculation absence as missing **new schedule-write/run policy**, not missing wiki timezone representation. Local design 27–31 and delta spec 30–42 versus wiki §1.4.
- Preserve existing application session/access boundary. MOS-1015 spec 9–14 and tasks 15 contain overly broad no-profile/no-auth prose. The report correctly identifies this; if a later authorized documentation correction occurs, also cover `mos-1015-report-constructor/design.md` line 53, which repeats the no-auth-endpoints test wording. This is an additional correction locator, not a new auth gate or a substantive defect in the review target.
- Prior auth release approval remains closed: archived auth tasks final paragraph and `docs/mpmm-auth-rollout.md` 3–5 explicitly record user confirmation on 09.10.2026, not agent runtime verification. It is neither reopened by stale demo prose nor extended to reports/scheduling.
- Main permissions spec 23–39 requires explicit `*` for report UI, not Analytics:view or role names. Backend object scope remains server-owned. Approved credential-free frontend mocks and fixed responses do not prove delivery of MOS-885's requested backend fake provider, and neither can fabricate successful persistence or missing operations.

## Architecture / Start Here

Start with `openspec/changes/mos-1016-report-template-scheduling/design.md` 49–76. It already binds local settings to the MOS-1015 draft and preserves full server acceptance. MOS-916 owns list/open/selected-template actions; MOS-919 owns file continuation. These are planning dependencies, not inspected implementation. No accepted write connection permits bridging the gap through local cards, storage, guessed DTOs or timers.

## Bounded owner questions and evidence limits

Future reconciliation still needs report API owners to publish complete write/read/error/idempotency schemas; product/scheduler owners to agree relative-period boundaries and execution timezone/times; backend/security owners to define ownership and automatic-run identity/scope; result owners to define confirmed status/file/failure retrieval; publication owners to reconcile the wiki/OpenAPI discrepancy without chronology-based precedence. None blocks this evidence review or authorizes new implementation.

Runtime, deployed fake provider, actual persistence, worker execution and product code remain unverified. No source precedence, product deferral, activation, task closure or general auth reopening follows. No network/browser/MCP, tests/builds, credentials or Git/index inspection was performed. Only this designated review artifact was written; original and product files were not edited. An initial handoff-path read failed; path discovery found the existing file under `audit/work-items/`, which was then read completely.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Full original and relevant planning/prerequisite reads; independent saved-source hashes, six exact operation checks, false-positive DTO analysis and eleven-candidate coverage support bounded ACCEPT."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-1016.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python hashlib/json/HTMLParser primary-evidence inspection","result":"passed","summary":"All three hashes/byte counts matched metadata; wiki six operations and positive read metadata independently inspected."},
    {"command":"Local exact OpenAPI membership and analytics reference-closure inspection","result":"passed","summary":"Six report operations absent; dashboard/board and response-template evidence does not establish report scheduling."},
    {"command":"Initial cat audit/REPORTS-PUBLICATION-HANDOFF.md","result":"failed","summary":"Incorrect presumed location; find located audit/work-items/REPORTS-PUBLICATION-HANDOFF.md and complete read succeeded."},
    {"command":"Tests/build/browser/network","result":"not-run","summary":"Outside permitted review scope."}
  ],
  "validationOutput": ["ACCEPT for evidence/mapping only; no substantive mandatory correction to original.","Historical auth confirmation preserved; index state unverified."],
  "residualRisks": ["Runtime, deployment and implementation not inspected.","Write/ownership/relative-period/background-result contracts unresolved.","Wiki/OpenAPI publication disagreement unresolved."],
  "diffSummary": "Designated review artifact only; no original or product edits and no Git/index attestation.",
  "reviewFindings": ["No blockers or unsupported material claims established.","Additional downstream auth-wording correction locator: MOS-1015 design.md:53, alongside already identified spec/tasks wording."],
  "manualNotes": "Independent documentation/primary-publication review, not a runtime audit. All truncated read outputs were continued. No source precedence, activation or closure approved."
}
```
