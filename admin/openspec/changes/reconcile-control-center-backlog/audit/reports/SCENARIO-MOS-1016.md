# SCENARIO-MOS-1016 — saved report templates and schedule write

## Result

**Existing MOS-1016 local-draft boundary remains justified; no activation or feature closure.** The saved wiki publishes template **read** metadata, not creation, schedule-write or worker lifecycle. Saved OpenAPI does not publish even the six wiki report operations. MOS-885 requests a fake report-data provider and read/preview/export implementation; its Backlog status and DoD are not delivery evidence. MOS-1016 already preserves the substantive save/schedule acceptance in S01–S10 and B16.1–B16.5. The narrow documentation candidate is precision about published read models versus absent write/execution contracts, not a new plan or implementation.

No audit-input blocker encountered. Product/contract questions below remain for future owner reconciliation, not decisions needed to complete this report. Source precedence is not selected.

## Files retrieved and evidence integrity

Paths below are repository-relative. `A` means `openspec/changes/reconcile-control-center-backlog/audit`; JSON pointers/HTML section headings identify embedded evidence more accurately than a fabricated code line range.

| Primary evidence | Exact inspected content / revision | Independently computed SHA-256 |
| --- | --- | --- |
| `A/sources/jira-reports-details/r1/content.json` (133 lines); `metadata.json` (1–47) | Only `/items/1` MOS-885 and `/items/5` MOS-1016 interpreted; entire saved bytes hashed. Retrieved 2026-10-16T13:31:43.125Z. Both Backlog, no comments/attachments. Updated respectively 2026-10-16T19:20:12.520+0800 and 2026-10-09T15:04:07.048+0800. No invented Jira revision number. | `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c` — 12996 bytes; metadata and assignment match |
| `A/sources/wiki-241085838/r1/content.json` (63 lines); `metadata.json` (1–54) | `/version`, `/bodyView`: page revision **3**, 2026-09-09T17:12:02.625+08:00; body contract **v1.0**, history dated 08.09.2026. Read inert text, especially §§1.1, 1.4, 2.1–2.8 and history; no HTML execution. Attachment listing empty. | `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74` — 37238 bytes; metadata and assignment match |
| `A/sources/api-live/r1/content.json` (single-line JSON without trailing newline); `metadata.json` (1–19) | OpenAPI **3.1.0**, `info.version=0.1.0`; saved revision 1 retrieved 2026-10-16T11:13:29.451Z. Enumerated `/paths`, exact report-path method membership, analytics operation bodies and transitive schema references; inspected template-named DTO properties to exclude response-template false positives. | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` — 413007 bytes; metadata match. No ETag/Last-Modified. |

All conclusions concern these saved publications, not current remote state or runtime success.

### Local specification discovery and full reads

`A/work-items/LOCAL-001.md` (full) supplied discovery roots; performed fresh path discovery under `openspec/specs` and scoped active-change content discovery excluding archive/audit as product candidates. Did not reuse inventory acceptance as semantic proof. No report-specific main capability was found. Read complete matching report artifacts, not just search snippets:

| Owner path prefix | Files and full line ranges |
| --- | --- |
| `openspec/changes/mos-1016-report-template-scheduling/` | `proposal.md` 1–31; `design.md` 1–76; `tasks.md` 1–18; `specs/report-template-scheduling-draft/spec.md` 1–51; `.openspec.yaml` (schema spec-driven, created 2026-09-29) |
| `openspec/changes/mos-1015-report-constructor/` | `proposal.md` 1–33; `design.md` 1–100; `tasks.md` 1–27; `specs/report-constructor-draft/spec.md` 1–128; `specs/dialog-selection-draft/spec.md` 1–116 |
| `openspec/changes/mos-916-report-templates/` | `proposal.md` 1–31; `design.md` 1–74; `tasks.md` 1–18; `specs/report-template-access/spec.md` 1–47 |
| `openspec/changes/mos-919-report-csv-export/` | `proposal.md` 1–30; `design.md` 1–65; `tasks.md` 1–13; `specs/report-export-availability/spec.md` 1–28 |
| Main specs | `openspec/specs/control-center-permissions/spec.md` 1–91; `openspec/specs/dialog-selection-builder/spec.md` 1–67 |

Discovery also read `openspec/changes/mos-1030-skill-result-analytics/proposal.md` (1–28): explicitly excludes new reports; not an alternative scheduling owner. Dialog selection is a dependency only: its accepted main contract does not establish a report-template condition DTO. No duplicate list/CSV/condition-engine audit or code inspection performed.

### Mandatory access/demo prerequisites

Read **complete** proposal, design, every delta spec and tasks for both approved archived prerequisites (including continuation of tool output that was initially truncated):

- Prefix `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: `proposal.md` 1–38, `design.md` 1–171, `tasks.md` 1–52; `specs/control-center-api-integration/spec.md` 1–64, `specs/control-center-http/spec.md` 1–71, `specs/control-center-mock-server/spec.md` 1–27, `specs/control-center-permissions/spec.md` 1–89, `specs/control-center-shell/spec.md` 1–101, `specs/mpmm-session/spec.md` 1–138.
- Prefix `openspec/changes/archive/2026-10-09-add-local-session-demo/`: `proposal.md` 1–28, `design.md` 1–70, `tasks.md` 1–26; `specs/control-center-mock-server/spec.md` 1–106, `specs/control-center-shell/spec.md` 1–55, `specs/local-session-demo/spec.md` 1–123.
- `docs/mpmm-auth-rollout.md` 1–58, and full `A/decisions.md` (stable headings D-007, D-011, D-012 particularly relevant).

Historical auth release gate **was confirmed by the user on 09.10.2026** (auth tasks final paragraph; rollout Status). This is preserved, not reopened and not extended to reports or scheduler delivery. No independent runtime verification is claimed. Older demo prose saying the gate remains open does not erase the recorded confirmation.

## Exact contract coverage

### Wiki read models are real publication evidence, not a write protocol

`wiki /bodyView §1.1` defines `parameters.period.date_from/date_to` as inclusive calendar dates, nullable `channel_id` (all channels), and ordered `field_codes` with at least one field. It does **not** define a surface-ID mapping, complex conditions or relative run-period representation.

`§1.4` defines a template with `id` (UUIDv7), `name`, `description`, `parameters`, nullable `schedule`, and nullable `last_run`:

```text
schedule = null | { cron: five-field string, timezone: IANA string }
last_run = null | { at: datetime, by: { id: UUID, name: person-name object }, rows: integer }
```

`null` schedule means manual launch; `null` last_run means no prior launches. The example `0 9 * * 1` / `Europe/Moscow` is explained as Monday 09:00 in that timezone. This is positive evidence of the **read representation**, not an agreed default for MOS-1016, a weekly/monthly write policy, DST handling or permission to synthesize cron. `last_run.by` is the launching user, **not template ownership**. No job state, run identifier, retained-result/file retrieval protocol or automatic-run principal is established.

`§1.4` explicitly says “launch” opens the template in the constructor; `§2.3` transfers saved parameters preserving field order. `§2.6` directly returns CSV using saved parameters with no request body. Neither action specifies a background-job launch command. No browser timer authority follows from either.

### Exact operation inventory

Base: `/api/control/api/analytics/v1`.

| Method and suffix | Wiki | Saved OpenAPI r1 |
| --- | --- | --- |
| GET `/report-constructor` | §2.1 | Absent |
| GET `/report-templates` | §2.2 | Absent |
| GET `/report-templates/{template_id}` | §2.3 | Absent |
| POST `/report-preview` | §2.4 | Absent |
| POST `/report-export` | §2.5 | Absent |
| POST `/report-templates/{template_id}/export` | §2.6, bodyless | Absent |
| Template create/update, schedule-write, relative-period-write, background launch/result operations | No such operation in the complete wiki method section | No corresponding report path. Explicit membership checks also found no POST collection or PUT/PATCH detail at the above template paths; these checked spellings are **not proposed endpoints**. |

This is a publication gap, not proof that deployed backend routes do not exist. No corresponding report operation DTO can be extracted from saved OpenAPI. Schema-property inspection found no `schedule`, `cron`, `last_run` or `field_codes` property in its schema definitions.

To avoid relying on names alone, inspected all five published analytics operations and their reference closure: GET `/dashboard`, POST `/dashboard/refresh`, GET `/widgets`, GET/PUT `/board`. `DashboardFilterRequest` contains nullable `started_from`, `started_to`, `channel_id`; `SaveBoardRequest` requires `version` and `widgets`; `BoardResponse` requires `version`, `is_default`, `widgets`; `RefreshDashboardResponse` requires `sample`, `calculated_at`. Descriptions and schemas establish dashboard refresh/personal widget-board persistence, **not report-template save or scheduling**. Their period/permissions cannot be borrowed for MOS-1016. `ResponseTemplateCreate/ResponseTemplateResponse` concern text response templates (`code`, `type_code`, `scope_code`, `text`, skill/surface links), not saved report parameters. No substitute operation or DTO is selected.

## Stable candidate map

Candidates are extracted requirements, not newly approved behavior. `J16` = Jira `/items/5/description`; `J885` = `/items/1/description`; `W` = wiki `/bodyView`. Local `S`/`B16` locators are `mos-1016.../design.md` lines 55–74. Active delta-spec coverage denotes **planned local UI**, not delivery; all six MOS-1016 implementation checkboxes remain unchecked.

| ID | Candidate / primary evidence | Exact local coverage and remaining contract gap |
| --- | --- | --- |
| MOS1016-01 | Save a template name (J16). | S01/S03, B16.1/B16.5; delta `Local template settings` and `Save remains unavailable`, tasks 1.1–1.2/2.1 cover local nonblank validation and disabled save. W §1.4 has a read name, no create DTO, uniqueness/length or write errors. |
| MOS1016-02 | Persist chosen fields (J16); order is explicit in W §§1.1, 2.3. | S03/S05, B16.2 preserves ordered round trip. W only has its 18-field read parameter catalog; constructor's 24 UI fields are not automatically wire-compatible. No write mapping established. |
| MOS1016-03 | Persist selected surface (J16). | S03/S05, B16.2 and MOS-1015 `Surface reference without invented report mapping`. W uses nullable `channel_id`, not an established surface-ID mapping. |
| MOS1016-04 | Persist complex selection (J16). | S03/S05, B16.2 retains AND/OR, typed values/ranges and phrase scope/mode/skill. W parameters omit conditions; accepted dialog selection does not authorize serialization into a report-template DTO. |
| MOS1016-05 | Manual / daily 09:00 / Monday / first day of month, under agreed settings (J16). | S02/S07, B16.3; delta `Local template settings` and `Schedule intent is not execution configuration`, task 1.3. Four UI choices covered; no schedule write, weekly/monthly time, timezone default or execution policy approved. W read cron example is not a substitute. |
| MOS1016-06 | Agree each automatic run's period; do not silently repeat saved absolute dates as a new monthly report (J16). | S06/S07, B16.3; `Monthly selection preserves report period` explicitly preserves local absolute dates. W §§1.1/1.4 only stores absolute dates. Relative-period rule, boundary evaluation and serialized mode remain absent; “previous month” is not inferred. |
| MOS1016-07 | Obtain write API and durable save of complete settings (J16). | S03/S04/S05, B16.1/B16.2. Existing continuation already requires create/read, reread/reload visibility and no duplicate creation after a successful write followed by failed GET. W publishes limited reads only; no write contract in either saved publication. |
| MOS1016-08 | Define visibility and ownership rights (J16). | S08/B16.4 plus main `Server owned resource scope`. W §2.7 publishes accessible-only templates, team-skill/surface scope and hidden-object 404; that does not specify created-template owner/sharing/edit rights or scheduled-run identity/scope. |
| MOS1016-09 | Define background-run result (J16). | S08/B16.4 already requires agreed server status/result location, author/time/rows/file without client-faked last_run. W read last_run and direct CSV export do not establish worker lifecycle, result storage/delivery or failures. |
| MOS1016-10 | Frontend only supplies settings, never executes the schedule (J16). | S09, B16.3/B16.4; delta scheduling requirement and task 3.2 prohibit timer, next-run claims and hidden defaults. Covered boundary; no correction needed. |
| MOS1016-11 | Do not claim fake-provider request as delivery (J885). | Proposal lines 11–17 and design lines 68–76 separate local UI from full server acceptance. MOS-885 requests isolated fake data for preview/metrics/CSV, validation and scope, template list/detail; no scheduler implementation is specified/proven. Keep separate from credential-free frontend business mocks. |

Existing S10/B16.5 adds valuable preservation/error acceptance from the local plan beyond J16's terse description: failure must retain all input, not add a fake card or show success; name conflicts, retry and idempotency must follow an agreed contract. No need to duplicate or weaken it.

## Conflicts, boundaries and narrow disposition

1. **Qualify blanket absence, do not enable saving.** Wiki publication supplies template read shape, nullable schedule and last-run semantics. Local MOS-1016 proposal/design/tasks still correctly withhold write/execution. A future documentation-only correction could say “published limited read model; no agreed create/round-trip/schedule-write contract” rather than imply no read model exists anywhere. The wiki/API publication mismatch must remain explicit; do not select either source by date or silently sync it.
2. **Timezone precision.** MOS-1016 design lines 27–31 and spec scheduling requirement say timezone/calculation are not agreed. Preserve this as the **new schedule-write/run policy** gap; avoid claiming the wiki has no timezone representation. Its IANA field and Moscow example do not choose a default, DST behavior, daily/monthly boundaries or next-run algorithm.
3. **Dependency auth wording needs qualification, not an auth reopen.** MOS-1015 delta `Report constructor entry and draft lifetime` (lines 7–15) says editing without profile checks/auth requests; task 3.1 likewise says no auth requests. Read literally for the whole page, that conflicts with approved session/bootstrap and wildcard-only report UI. Narrow future clarification: no *additional report-owned* auth model/requests; normal application session/access boundary remains. MOS-1016 must not inherit a bypass. No new permissions or role-derived grants are proposed.
4. **Wiki access prose versus approved UI policy are different layers.** W §2.7 names platform admin/team owner/surface owner/quality analyst and server object scopes. Main permissions spec lines 23–39 requires explicit `*` for report UI, not Analytics:view and not role-name matching. Do not equate them or claim backend enforcement verified. Ownership/write authorization remains genuinely unspecified.
5. **Mock distinctions.** MOS-885 fake-provider scope is a backend request, not proof of a deployed provider, production data or scheduler. Approved local demo controls choose fixtures/fixed responses; credential-free business mocks do not enforce roles or make missing operations succeed. Neither full demo profile nor `*` permits a fake persisted template. Production isolation and configured real-session rules remain unchanged.
6. **No duplicated owner.** MOS-1015 owns constructor/conditions dependency; MOS-916 owns list/detail/opening/selected-template export; MOS-919 owns export availability/file continuation. MOS-1016 owns settings/save/schedule boundary. Existing B16 acceptance is sufficient to retain the missing work; no new task package, source precedence, task closure or activation follows.

## Owner questions for future contract reconciliation

- **Report API/backend owner:** Which approved create/read/update contract preserves name, field order, surface mapping, full selection and period mode? What are write validation, conflict and retry/idempotency rules? Publish operation/DTO evidence rather than derive it from read examples.
- **Report product + scheduler/backend owners:** Which relative-period rules and evaluation boundaries apply to each automatic run? What are agreed weekly/monthly times, timezone and relevant clock/DST semantics? Which values are configurable? This report chooses none.
- **Backend/security owners:** Who owns/shares/edits a created template, and under whose authorization and object scope does an automatic run execute, including changed access? Existing last_run.by is insufficient.
- **Scheduler/result owner:** Where does UI read confirmed background status/result/failure and obtain a file, and how are those linked to a run? No polling cadence, queue, cron writer, worker protocol or browser lifecycle is inferred.
- **API publication owner:** Reconcile wiki's six report methods and models with their absence from saved OpenAPI, and identify actual delivery evidence separately from MOS-885's Backlog request. Do not resolve by chronology alone.

## Architecture / start here

Open `openspec/changes/mos-1016-report-template-scheduling/design.md` **lines 49–76** first: S01–S10 and B16.1–B16.5 already bind the full acceptance without making it executable in the current apply. Proposed local settings share the MOS-1015 constructor draft; page-owned state survives MOS-916 tab changes but not reload. Server template creation and execution have no accepted wire connection in the inspected evidence. The client must not bridge that gap with local cards, storage, invented DTOs or timers.

## Validation and residual risks

Executed only local discovery, selective/full documentation reads, inert HTML text extraction, JSON parsing, SHA-256/byte verification, exact method membership and schema-reference inspection. No source/code/product edits, network/MCP/browser, tests/build/generation, credentials, git mutation, archive or sync. Only this bound report was intentionally written. Index state is **uninspected**; no index attestation.

Residual risks: runtime implementation and deployment remain unverified; Jira comments are empty and attachment bodies are not supplied; read contracts cannot demonstrate persistence/ownership or background execution; publication disagreement remains unresolved. Existing source references to historical HTML/backlog were not independently audited or treated as fresh primary evidence. Main selection contract was read solely to prevent conflating dialog support with report serialization.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Verified all three saved hashes/versions; mapped 11 stable candidates to existing MOS-1016/spec dependencies; distinguished read metadata, missing writes and fake-provider requested scope from delivery."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1016.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python hashlib/json inspection of three saved primary sources","result":"passed","summary":"All byte counts and SHA-256 digests matched saved metadata; Jira items 1/5 and wiki page/body versions verified."},
    {"command":"Local exact paths/method membership and analytics DTO reference-closure inspection","result":"passed","summary":"Six wiki report methods absent from saved OpenAPI; available analytics board/refresh DTOs do not establish report scheduling."},
    {"command":"Tests/build/browser/network","result":"not-run","summary":"Forbidden by bounded assignment."}
  ],
  "validationOutput": ["Report-only audit; no product activation or task closure.","Complete mandatory auth/demo prerequisites read; historical 09.10.2026 approval preserved without extension."],
  "residualRisks": ["No runtime/backend delivery verified.","Report write/relative-period/ownership/background-result contracts remain unresolved.","Wiki/OpenAPI report publication gap remains unresolved."],
  "diffSummary": "Only bound report intentionally written; repository index not inspected.",
  "reviewFindings": ["No missing-input blocker; narrow publication/auth-wording corrections identified, not applied."],
  "manualNotes": "Fresh local primary/spec analysis; no code audit or execution. Independent review remains required. No source precedence selected."
}
```
