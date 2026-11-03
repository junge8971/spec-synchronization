# Code Context

## Verdict — ACCEPT

Independent documentary review of MOS-916 only. The original report is supported within its stated bounds. No mandatory correction to the original report was identified. Acceptance concerns the audit report, not implementation, API activation, task closure, deployment or approved product deferral. Preserve the original unchanged.

## Files Retrieved

All paths are repository-relative. JSON pointers/HTML heading IDs identify primary evidence more precisely than long serialized source lines.

- `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-916.md` (1–101), fully read, including acceptance report.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MOS-916.md` (1–8), `R-REPORTS-WAVE.md` (complete), `REPORTS-PUBLICATION-HANDOFF.md` (complete).
- `openspec/changes/mos-916-report-templates/proposal.md` (1–31), `design.md` (1–74), `tasks.md` (1–18), `specs/report-template-access/spec.md` (1–47), all complete.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-reports-details/r1/content.json`: complete `/items/0`, `/items/1`, `/items/2`; complete adjacent `metadata.json`.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241085838/r1/content.json`: `/version`, `/attachments`, complete inert `/bodyView`; complete adjacent `metadata.json`. No HTML execution.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`: `/info`, `/openapi`, complete path and schema-name inventories; complete adjacent `metadata.json`. No corresponding report operation exists to traverse.
- `openspec/specs/control-center-permissions/spec.md` (1–91), `docs/mpmm-auth-rollout.md` (1–58), `docs/api/contracts/reports.md` (1–5), complete.
- Complete archived prerequisites under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: `proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52), `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138).
- Complete archived prerequisites under `openspec/changes/archive/2026-10-09-add-local-session-demo/`: `proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26), `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123). Truncated combined output was subsequently read in contiguous chunks.

## Key Code / Independently verified candidates

No application code inspected. Below, J and W denote the exact Jira and wiki content paths listed above. Wiki IDs begin `APIконтрактмодуляотчётов-` within `/bodyView`.

| Candidate | Independent primary check | Disposition |
| --- | --- | --- |
| C916-01 Catalog | J `/items/2/description`; W `2.2Получитьшаблоны`: GET `/api/control/api/analytics/v1/report-templates`, `data.items`, only available templates | Correct. No pagination/total invented. Existing B916.1 at design:68 retains future successful empty/loading/error cases, distinct from unavailable. |
| C916-02 Schedule/manual | W `1.4Шаблон`: nullable schedule, five-field cron, IANA timezone | Correct read metadata, not schedule creation or execution. Monday 09:00 Europe/Moscow is an example, not a default. |
| C916-03 Last execution | W `1.4Шаблон`: `last_run.at`, `by.id`, structured `by.name`, integer `rows` | Correct: actor who launched the report, not creator/current principal. Background actor and display-time semantics remain unresolved. |
| C916-04 Null versus zero | J `/items/2/description`; W `1.4Шаблон`, `2.2Получитьшаблоны` second item | Correct: null means never run. Distinction from existing rows=0 is already explicit in B916.2, design:69; do not claim a new uncovered requirement. |
| C916-05 Open versus execute | W `2.3Получитьшаблон`: GET `/api/control/api/analytics/v1/report-templates/{template_id}`, UUIDv7, `data.template.parameters`; W `1.1Параметрыотчёта` and `1.4Шаблон` | Correct: transfer saved absolute period, nullable channel_id and ordered field_codes. Opening is not execution and cannot manufacture last_run. B916.3, design:70, additionally retains relative-period mode, surface and advanced conditions/phrase/skill roundtrip. Published channel_id must not be silently declared a complete equivalent to those richer criteria. Original correctly leaves reconciliation open. |
| C916-06 Selected-ID export | W `2.6СформироватьCSVпошаблону`: POST `/api/control/api/analytics/v1/report-templates/{template_id}/export`, no body, saved parameters | Correct selected server template, not current builder settings or another template's last file. B916.4, design:71, already owns selection; MOS-919 owns detailed transport. |
| C916-07 No browser scheduler | J `/items/2/description`, final requirement; design:11,45,61,69; tasks:14 | Correct and already retained. Schedule read metadata does not establish scheduler delivery. |
| C916-08 Error/object boundary | W `2.7Доступ`, `2.8Форматошибок`: hidden template 404; section 403; 401,400,422,500; error data=null | Correct. Object 404 is not section denial. Draft preservation and no false file/success are existing B916.5 criteria, design:72, not proven runtime behavior. |

### Integrity and precise version boundaries

Recomputed saved-byte SHA-256 independently; each matches adjacent metadata:

| Source under audit/sources | Bytes | SHA-256 |
| --- | ---: | --- |
| jira-reports-details/r1/content.json | 12996 | `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c` |
| wiki-241085838/r1/content.json | 37238 | `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74` |
| api-live/r1/content.json | 413007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |

Jira capture `2026-10-16T13:31:43.125Z`: items 0/1/2 are MOS-777/885/916, all Backlog with null parent, no comments/attachments. MOS-916 updated `2026-10-15T14:16:19.727+0800`. Wiki capture `2026-10-16T13:31:51.607Z`: page 241085838 version 3, publication timestamp `2026-09-09T17:12:02.625+08:00`; embedded contract v1.0/history 08.09.2026; empty attachment results, no next page. OpenAPI capture `2026-10-16T11:13:29.451Z`: revision 1, OpenAPI 3.1.0, service 0.1.0, 94 paths/128 operations/382 schemas; no ETag/Last-Modified. These dimensions agree with the original; none establishes current remote freshness or source precedence.

All three exact template paths above are absent from saved `/paths`; no path contains report and no schema name identifies a report model. Dashboard/refresh/widgets/board and managed-resource response-templates are not substitute report APIs. This is a valid inspection result, not a missing-input blocker. `docs/api/contracts/reports.md:5` records absence from historical message.txt, not absence of the later inspected wiki publication.

## Architecture / Preserved findings

The published flow is available list → selected-ID detail → builder parameter transfer; selected-ID export is separate. The active change instead plans URL tabs and unavailable catalog, without list/detail/export requests or mock fixtures. Proposal:9–15, design:21–25,64–74, tasks:8,14–18 and delta spec:26–38 explicitly retain B916.1–B916.5 outside current apply. Every MOS-916 task remains unchecked. This is an existing plan, not a missing-plan finding or proof of delivered UI.

MOS-885 `/items/1/description` requests an isolated fake backend data provider for preview/metrics/CSV and excludes real dialog retrieval. Its DoD and Backlog status are not delivery evidence. This backend request is distinct from frontend local Express mocks, approved demo profiles and actual real-data integration.

The original correctly preserves historical auth approval. Archived auth `tasks.md:48–52` and `docs/mpmm-auth-rollout.md:5,24–34` record user confirmation on 09.10.2026, not agent real-environment verification or deployment. Stale demo planning language cannot reopen that gate; it also cannot extend approval to report APIs. Main permissions spec:11,35–38,62,81 retains exact grants, explicit wildcard-only report UI, server object scope and no request ACL. Wiki business roles are not a frontend role-to-grant mapping. Demo full does not implement unsupported report APIs.

## Mandatory corrections / Unsupported claims

- **Original report: none.** No unsupported material assertion or severity-bearing defect identified in this bounded review.
- **Preserve the original's proposed later planning clarification, not an immediate edit:** qualify unbounded contract-absence wording such as design:9,45 and delta spec:32 as absence of the agreed/current integration contract, while recording the wiki publication and saved OpenAPI absence. Proposal:3 is already qualified to the local contract. Do not rewrite it as proof the API is deployed, activate blocked tasks or remove B916.3's richer criteria without owner agreement.
- **Index attestation:** original omits `noStagedFiles` and explicitly disclaims git/index attestation. That is appropriate. Index remains unverified in this review; reject any downstream addition of `noStagedFiles:true` based merely on not staging during a run.

## Start Here / Bounded owner questions

Start with `openspec/changes/mos-916-report-templates/design.md:47–74`, the existing coverage matrix and blocked acceptance owner. No new plan is needed for this audit.

Remaining owner decisions, not execution blockers: agreed integration publication/version; treatment of incompatible/richer saved parameters without silent loss; list pagination/count and last-run actor/timezone/update semantics; separately agreed report UI grants; separate evidence of fake-provider delivery and real-data work if later scoped. Companion builder/CSV/schedule-write audits and actual code/runtime remain outside this verdict. No source ranking or product deferral approved.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently verified eight MOS-916 candidates, complete active artifacts, saved primary hashes and archived approval prerequisites; bounded ACCEPT with no mandatory original-report corrections."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-916.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python hashlib/json/HTMLParser inspection and local file reads","result":"passed","summary":"Three hashes matched; exact template operations absent; 94 paths, 128 operations, 382 schemas."},{"command":"Tests/build/network/browser/MCP","result":"not-run","summary":"Forbidden by review scope."}],
  "validationOutput": ["Original fully read; relevant active and archived planning prerequisites read completely.","Eight candidate mappings supported; historical approval preserved without extension."],
  "residualRisks": ["No code/runtime/delivery verification or remote freshness check.","Saved-template parameter mismatch and report access policy require owner decisions.","Git index uninspected and unverified."],
  "diffSummary": "Only designated review artifact written; original, product and source evidence unchanged.",
  "reviewFindings": ["ACCEPT: no mandatory original-report correction; existing planning wording clarification remains owner-reviewed follow-up, not activation."],
  "manualNotes": "Documentary MOS-916 review only. Publication is not implementation or deployment; no index cleanliness attestation. No execution blocker occurred."
}
```
