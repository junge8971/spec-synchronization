# Code Context

## Result

MOS-916 has an existing active plan, not a missing plan: it deliberately supplies navigation plus an unavailable catalog, with full template behavior retained as blocked B916.1–B916.5. Newly inspected Jira/wiki evidence substantially specifies that continuation, but the saved OpenAPI contains none of the three template operations. Recommend a narrow evidence/decision correction, not activation, closure, API implementation, or an approved deferral. No application code was audited.

## Files Retrieved

Paths below are repository-relative. For JSON, exact JSON pointers and HTML heading IDs are more stable than the single long HTML source line.

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MOS-916.md` (lines 1–8): bounded assignment.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (main-capability inventory and active-change routing table): discovery only; its integrity/index assertions were not adopted.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-reports-details/r1/content.json`: `/items/0`, `/items/1`, `/items/2` only; corresponding `metadata.json` read completely.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241085838/r1/content.json`: `/version`, `/bodyView`, `/attachments`; corresponding `metadata.json` read completely. Inert HTML parsed as text, never executed. Analysis restricted to template list/detail/open/export references and their models/errors/access context.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`: `/info`, `/openapi`, complete `/paths` key inventory and `/components/schemas` name inventory for matching operations/DTOs; corresponding `metadata.json` read completely.
- `openspec/changes/mos-916-report-templates/proposal.md` (1–31), `design.md` (1–74), `tasks.md` (1–18), `specs/report-template-access/spec.md` (1–47): all read completely.
- `openspec/specs/control-center-permissions/spec.md` (1–91): current main policy, read completely. Main spec path discovery and scoped literal search found no report-template capability or MOS-916 reference; this is not a claim that every main spec was semantically audited.
- Complete mandatory archived auth prerequisites: `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52); its `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138).
- Complete mandatory archived demo prerequisites: `openspec/changes/archive/2026-10-09-add-local-session-demo/proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26); its `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123).
- `docs/mpmm-auth-rollout.md` (1–58): complete historical approval/rollout context. No credentials inspected.

## Evidence integrity and version dimensions

Recomputed SHA-256 over saved bytes with Python hashlib; all matched metadata and the two assignment-provided digests:

| Saved source | Bytes | SHA-256 |
| --- | ---: | --- |
| jira-reports-details/r1 | 12996 | `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c` |
| wiki-241085838/r1 | 37238 | `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74` |
| api-live/r1 | 413007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |

Metadata records parent verified-origin collection for Jira/wiki, and public Swagger-discovered OpenAPI capture. This run verifies local integrity and provenance records, not remote authenticity/freshness by a new request.

- Jira retrieval: 2026-10-16T13:31:43.125Z. Items 0/1/2 are MOS-777/MOS-885/MOS-916, all `Backlog`, no comments or attachments. Updated timestamps respectively `2026-10-09T15:04:12.908+0800`, `2026-10-16T19:20:12.520+0800`, `2026-10-15T14:16:19.727+0800`. Their `parent` fields are null; membership is collection provenance, not a parent-field assertion.
- Wiki retrieval: 2026-10-16T13:31:51.607Z; page 241085838 version **3**, published `2026-09-09T17:12:02.625+08:00`. Embedded contract is **v1.0**, history dated **08.09.2026**. Attachments response status 200, empty list/count 0, no next page. Page version, contract version/date, and capture revision r1 are distinct.
- OpenAPI retrieval: 2026-10-16T11:13:29.451Z; capture revision 1, OpenAPI **3.1.0**, service version **0.1.0**. Recounted 94 paths, 128 operations, 382 schemas; metadata has no ETag/Last-Modified. This capture predates the new Jira/wiki retrieval; no precedence or deployment conclusion follows.

## Key Code / Stable candidates

No code changes proposed here. Candidate IDs below are audit-local, not new approved requirements. `J` means the exact Jira content path above; `W` means the exact wiki content path above, `/bodyView`. Wiki heading IDs share prefix `APIконтрактмодуляотчётов-`.

| Candidate | Exact primary locator and semantics | Existing plan coverage / gap |
| --- | --- | --- |
| C916-01 Available catalog | J `/items/2/description`, first sentence; W `2.2Получитьшаблоны`: GET `/api/control/api/analytics/v1/report-templates`, envelope `data.items`, only templates available to user. W `1.4Шаблон`: name/description. | Design T02, B916.1 (54, 68). Active spec 26–33 intentionally supplies unavailable, not a successful empty list. Wiki example supplies no pagination/total contract; do not invent one from B916.1's conditional wording. |
| C916-02 Schedule/manual | J `/items/2/description`, first sentence; W `1.4Шаблон`: nullable schedule; null means manual, otherwise five-field cron plus IANA timezone, Monday 09:00 example. | T03/B916.2 (55, 69); not active delta behavior. Text-rendering library recommendation is not permission to add a dependency. |
| C916-03 Last execution | J `/items/2/description`, first sentence; W `1.4Шаблон`: `last_run.at`, `by.id`, `by.name.{family_name,name,middle_name}`, `rows`. | T04/B916.2 (56, 69). Author is last-run actor, not template creator or current principal. Example user/time/count are not runtime fixtures or proof of execution. Background actor/display timezone questions remain. |
| C916-04 Never run vs zero rows | J `/items/2/description`, second paragraph; W `1.4Шаблон` and second item of `2.2Получитьшаблоны`: `last_run=null` means no executions. | T05/B916.2 (57, 69) already explicitly preserves null vs existing `rows=0`; retain without duplicate requirement. |
| C916-05 Open, not execute | J `/items/2/description`, second paragraph; W `1.4Шаблон`, `2.3Получитьшаблон`: GET `/api/control/api/analytics/v1/report-templates/{template_id}`, UUIDv7, `data.template.parameters` copied into builder preserving field order. Parameters here are date_from/date_to, nullable channel_id, ordered field_codes. | T06/B916.3 (58, 70). Existing spec 35–38 only navigates without a template. Important discrepancy: B916.3 also expects relative period/surface/AND–OR conditions/phrase/skill; those are not in this published template parameter model. Do not silently drop or fabricate them; constructor lane owns detailed reconciliation. No run-execution endpoint is described for the launch button. |
| C916-06 Export selected template | J `/items/2/description`, second paragraph; W `1.4Шаблон`, `2.6СформироватьCSVпошаблону`: POST `/api/control/api/analytics/v1/report-templates/{template_id}/export`, no body, server uses saved parameters and returns CSV. | T07/B916.4 (59, 71): ID selection belongs here; not current builder settings or another template's last file. MOS-919 owns detailed file transport/CSV audit. |
| C916-07 No browser scheduler | J `/items/2/description`, third paragraph. | T09/design 11, 45, 61, 69 and task 3.2 already retain prohibition. Displaying schedule neither schedules nor executes it; no schedule-write audit in this lane. |
| C916-08 Object/error boundary | W `2.7Доступ`, `2.8Форматошибок`: unavailable/hidden template returns 404; section 403, missing session 401, invalid input 400/422, build failure 500; JSON error envelope has null data. | T08/B916.5 (60, 72) already keeps failures distinct, preserves draft on failed opening and avoids false export success. Object 404 must not be turned into a claim that the user lacks the entire UI section. No live enforcement established. |

## Architecture and contract/spec comparison

Intended flow is server-filtered list → selected-ID detail → copy saved parameters into builder; selected-ID export is a separate server action. Opening parameters is not report execution and must not manufacture `last_run`. Schedule is display data, never a browser timer.

The exact three wiki operation paths above are **absent** from saved `api-live/r1/content.json /paths`. No path contains `report`; schema-name inspection found no report model. Consequently there are no corresponding operation refs from which to traverse a report DTO closure in this snapshot. Existing managed-resource `response-templates` operations and `tpl_*` DTOs are different resources and were not substituted. The analytics paths present are dashboard, dashboard/refresh, widgets, board—not reporting templates. Absence in this snapshot does not prove absence on the server or in every publication.

Current active plan is explicit: proposal 3, 9–15; design 21–25, 45, 64–74; tasks 8, 14–18; delta spec 26–38. All active tasks are unchecked. Its full requested behavior is retained in B916.1–B916.5 but intentionally outside the current apply. This is existing scope separation, not newly discovered missing acceptance criteria and not evidence the unavailable UI has been delivered. No missing-active-plan finding applies to MOS-916.

The newly retrieved wiki invalidates an unqualified claim that *no written template contract exists*. It does **not** establish agreement to integrate it, presence in saved OpenAPI, service availability, or suitability of its narrower parameter model. Preserve the distinction between published reference, agreed/generated integration contract, active spec, implementation, and release acceptance. Source ranking is not decided here.

### Requested fake provider is not delivery

J `/items/1/description` explicitly requests MOS-885 backend scenarios with data retrieval isolated behind an interface and a **fake implementation** for preview/metrics/CSV; real dialog data retrieval is excluded. Its DoD asks for list/detail, validation, CSV and user-scope checks. MOS-885 remains Backlog in this capture. This is requested backend scope—not proof of a delivered provider, local Express report handlers, passing tests, real analytic data, or backend enforcement. MOS-777's broader analytical goal and MOS-916's frontend request do not change that evidence limit. Even future successful fake-provider responses would not prove real-data integration.

### Access and historical approval preserved

Current `openspec/specs/control-center-permissions/spec.md:9–38,60–91` retains explicit `*` for report UI, exact permission matching, no role-name grants, server-owned object scopes, and no request ACL. Wiki §2.7 names platform administrator/team owner/surface owner/quality analyst and describes scope filtering; this is a published business-access statement, not a new frontend role-to-grant mapping or authorization to reuse Analytics permissions. Access reconciliation remains an owner question.

Archived prerequisites were read completely before these conclusions. They preserve config-selected real/mock modes, real-session readiness and credential destination checks, UI-only permissions, server authorization, and no mock credentials/role enforcement. Demo `full` does not enable unsupported report APIs. MOS-885's backend fake provider is distinct from the approved local demo system.

Historical auth task 6.3 is checked and explicitly records user confirmation on **09.10.2026** (`tasks.md:48–52`); `docs/mpmm-auth-rollout.md:3–5,23–34` records the approval basis and absence of agent real-environment verification. Preserve that closed historical gate; stale demo planning prose saying the gate remains open does not justify reopening it. Equally, do not extend that approval to newly published report operations, new scopes, report fake-provider delivery, or a changed deployment. No deployment completion is asserted.

## Start Here / Narrow disposition

First open `openspec/changes/mos-916-report-templates/design.md:47–74`: it already owns the continuation matrix. Suggested later owner-reviewed correction (not performed): add these provenance/version references, qualify blanket contract-absence language, and record the saved-OpenAPI absence and narrower wiki parameter model against B916.1–B916.5. Leave active unavailable spec/tasks and task status unchanged until explicit agreement. No-op for already-retained null/zero distinction, selected-ID export, launch-not-execute and no-browser-timer requirements. Do not promote blocked criteria into apply automatically.

Owner questions for follow-up, not blockers to this audit:

1. API/product owners: what is the agreed report integration contract/version and scope given wiki v1.0 versus this OpenAPI snapshot's absence? Supply an agreed operation/DTO/error publication before activation; no source precedence chosen here.
2. MOS-916/MOS-1015 owners: retain the richer B916.3 saved-parameter round trip, or explicitly narrow it to published absolute dates/channel/field_codes? How are incompatible saved templates surfaced without silent loss?
3. API/product owners: is list pagination/total intentionally absent; what actor/timezone semantics apply to scheduled last runs, and which documented event updates last_run? Opening the builder must not be treated as execution.
4. Access owners: how should the wiki's business roles map to a separately agreed report UI permission policy while retaining backend object filtering? No wildcard issuance workaround or invented grants.
5. Delivery owner: provide distinct evidence for fake-provider implementation, real-data integration if later in scope, and acceptance; neither Backlog status nor publication supplies it.

No actual local blocker occurred. No network/MCP/browser, tests/build/generation, code audit, credential extraction, git mutation, archive/sync, or source/product edits performed. Only this report was written. Main-spec semantic coverage beyond the stated policy and report-specific discovery is bounded; companion builder/CSV/schedule-write lanes remain outside this report.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Eight stable candidates mapped to exact primary locators and B916 coverage; verified three saved hashes, absent template OpenAPI operations, requested fake-provider boundary and historical auth approval."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-916.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python hashlib/json/path inspection and inert HTMLParser extraction; selective file reads and numbered listings","result":"passed","summary":"All three saved digests matched; 94 paths/128 operations/382 schemas; list/detail/template-export paths absent."},{"command":"Tests/build/browser/network","result":"not-run","summary":"Prohibited by bounded assignment."}],
  "validationOutput": ["Jira/wiki/API capture versions distinguished from publication and delivery.","Complete archived auth/demo prerequisites plus historical tasks/rollout read; prior approval preserved without extension."],
  "residualRisks": ["No runtime or delivery verification; backend fake-provider scope is only requested.","Published template parameters differ from richer blocked round-trip criteria; owner reconciliation required.","Saved OpenAPI lacks report operations; snapshot absence does not prove server absence.","No role mapping, source precedence, activation or completion decision made."],
  "diffSummary": "Sole designated report written; no product/source/code changes.",
  "reviewFindings": ["No audit execution blocker; contract-publication wording needs qualification, not automatic API activation."],
  "manualNotes": "Local primary evidence and active-plan analysis only. No git/index attestation. Independent review remains pending."
}
```
