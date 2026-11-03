# Code Context

## Result

Completed the bounded root-document comparison: wiki **247742436, r1, page version 4**, all **319 readable lines** and **19 exact HTML chunks**. Existing optional A/B owners cover the configuration UI. This supplement records provenance and concrete differences, not a new execution capability, implementation audit, precedence decision, API/DTO proposal or whole-module completion.

## Files Retrieved

Exact repository-relative paths; aliases below abbreviate citations only:

- **S**: `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247742436-readable/r1/content.txt`, **1–319**, completely read.
- **H**: `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247742436-readable/r1/body-view-chunks.json`, **1–21**, completely read. Entries **[0]–[18]** occupy lines **2–20**. Initial read returned lines 1–11 before 50KB truncation; continuation 12–21 completed every entry.
- **OM**: `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247742436/r1/metadata.json`, **1–21**.
- **DM**: `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247742436-readable/r1/metadata.json`, **1–14**.
- **O**: `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247742436/r1/content.json`: metadata **1–10** inspected, attachment index **12–34** read; bodyView at **11** reviewed through all exact H entries, not executed/rendered.
- **M**: `openspec/specs/ab-testing-module/spec.md`, **1–58**.
- **R**: `openspec/specs/ab-testing-registry/spec.md`, **1–98**.
- **E**: `openspec/specs/ab-testing-editor/spec.md`, **1–114**.
- **X**: `openspec/specs/ab-testing-export/spec.md`, **1–44**.
- **P**: `openspec/changes/archive/2026-10-15-add-optional-ab-testing/proposal.md`, **1–34**.
- **D**: `openspec/changes/archive/2026-10-15-add-optional-ab-testing/design.md`, **1–123**.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/DELTA-AB-TESTING-ROOT-DOC.md`, completely read.

Scoped line-numbered searches verified citation boundaries after content reads; `wc -l` confirmed owner/metadata lengths. No application code or broader owner graph inspected.

## Key Code / stable source candidates

These are documentation candidates, not implementation findings. Every S/H reference is to the single source version above.

### ABROOT-01 — Registry: covered with explicit server differences

**Source:** S **10–44**, §§3.1–3.6; H **[0]–[2]**, lines **2–4**. Name+code, surface-name chips through `ab_experiment_surface`, `COUNT(ab_group)`, status display name and navigation; three-click sorting; search ≥2 characters over name/code/group tags; any-selected-surface matching; status filter, reset, count, create, named saved selection and copy URL.

**Owner:** R **9–21, 58–98** adds server pagination, complete URL/search and persistent saved filters. Current search also includes description, experiment tags and surface names; third click restores `-updated_at`. These extra guarantees are not stated by the root and must not be narrowed on its authority.

### ABROOT-02 — Conditions: concrete archived/current-owner difference

**Source:** S **30–35**, §3.4; H **[2]**, line **4**. AND/OR with name/code/owner/status/launch/audience/metric/group count/priority/surfaces; text, enum and numeric operators including between; applied summary/badge.

**Owner:** R **23–56** supports typed metadata-backed `groups_count`, inclusive finite numeric ranges and NULL exclusion; priority and surface conditions remain explicitly unavailable. **D 40 still lists group count among unavailable conditions**, unlike current R **25–27, 46**. Record this difference without selecting chronology precedence or expanding support. Root does not define numeric coercion, NULL handling, nesting or the 50-condition limit.

### ABROOT-03 — Editor, weights and validation: covered, not traffic execution

**Source:** S **45–103**, §§4.1–4.4; **135–147**, §§6.3–6.5; H **[3]–[5], [7]–[8]**, lines **5–7, 9–10**. Header/main fields, four tabs, group name/percent/tag, add/delete/reorder; sum=100 save gate, minimum two groups, one surface, unique name/code and per-experiment tags. Six-color preview; segment labels at ≥12%; legend name/tag/percent. Esc/backdrop modal closure.

**Owner:** E **9–49, 60–86, 102–114** covers these with integer 0–100 percentages, upper limits, code regex, server uniqueness, cross-field checks, preserved group IDs, accessible reorder, truthful invalid preview and dirty protection. Source `sort_order` and `draft.surfaces[]` (S **89–91, 151–152**) differ from E **39** array order and `surface_ids`; sort_order is not sent. Mathematical totals and previews do not establish actual allocation.

### ABROOT-04 — Lifecycle and group identity: source tension retained

**Source:** S **55–61**, §4.1; **158–165**, §8; **253–262**, Tables §3.2; H **[3], [8]–[9], [13]–[14]**, lines **5, 10–11, 15–16**. Pause toggles paused/active; completion sets completed with confirmation. Table note forbids changing tags after launch; limitations acknowledge prototype UI does not block it.

**Owner:** E **51–58, 88–100** uses saved status != draft for tag readonly, not ever-started history. Commands require saved clean records and server confirmation, do not set dates and do not prove traffic changes. Neither root nor owner establishes a complete backend transition machine. Source five-status list includes archived (S **119, 284–288**); M **46–53** keeps archived unavailable, never aliases disabled or DELETE. No new lifecycle operation follows.

### ABROOT-05 — Audience, metrics and windows: settings only

**Source:** S **2–3, 75–80, 103–122, 164–165, 222–236, 289–299**; H **[0], [4]–[7], [9], [12], [15]–[16]**, lines **2, 6–9, 11, 14, 17–18**. Audiences all/authorized/new/segment; metrics resolution_rate/response_time/csat/escalation_rate; immediate/scheduled/manual; segment, priority, stable bucketing, logging, return-to-control and auto-stop. `min_sample_size` is explicitly **per group** (S **227**); ended_on can be empty for manual completion (S **223**).

**Owner:** E **11, 20**, M **37–44**, D **13, 43, 75–81** limit this to configuration. Scheduled requires started_on date, not scheduled_at/timezone/timer. Root defines no cohort entity, allocation algorithm, measurement/attribution window, significance threshold or sample-size calculation. Dates are not inferred measurement windows. Per-group wording is a bounded semantic clarification candidate for the existing editor, not authorization to implement computation. Root algorithm-per-group/current-version prose and priority-arbitration expectation do not prove integration or identify a control group.

### ABROOT-06 — Storage, joins, defaults and nulls: retain naming/type differences

**Source:** S **148–157**, §7; Tables **181–319**, §§2.1, 3.1–3.2, 4.1–4.3, 5–6; H **[8], [10]–[18]**, lines **10, 12–20**:

- Seven proposed tables: experiment, group, experiment_surface and four code-keyed dictionaries.
- Join: UUID PK; experiment/surface UUID FKs, created_at, unique experiment+surface (S **190–196**). Surfaces are external, not created here.
- Experiment: UUID PK; unique code/name; owner string, removed team_id; external responsible UUID; optional description/dates/tags/hypothesis/metric/sample/auto-stop/launch/audience/segment/priority; required status and three switches; timestamps/deleted_at. Indexes on status/metric/audience (S **215–241**).
- Group: UUID PK/FK; name/percent/tag/sort_order/timestamps; experiment index, unique experiment+tag and sum=100 (S **252–262**).
- Dictionaries: code/display_name/description/sort_order/is_default/is_active/deleted_at/timestamps (S **271–281**). Four catalogs and exact enumerations (S **263–299**); FK/external-reference summary (S **300–309**).

**Owner:** E **11, 20, 39, 76** and D **33–51, 63–73** own API-facing aggregate behavior: responsible ID is external **string**, group order is array order, inactive/unknown references and optional nulls are preserved. Internal source mismatch: `return_to_control_on_stop` at S **114** versus `return_to_control` at **236**; owner uses latter. Source includes soft-delete fields, but S **160** says dictionary soft deletion unused: no migration/delete workflow inferred. Optional storage fields do not themselves specify API null-clearing semantics.

Root specifies no concrete new-form defaults or populated is_default flags. E **11**/D **51** explicitly choose draft/resolution_rate/immediate/all, priority 50, stable+log true, return false, auto_stop false, control+variant 50/50, sample null and empty surfaces. These are approved owner defaults attributed to its HTML source, **not independently established by this root body**.

### ABROOT-07 — Export, reporting and demo feedback: no execution proof

**Source:** S **44, 57, 126–144, 159–162**; H **[2]–[3], [7]–[9]**, lines **4–5, 9–11**. List field picker/detail section picker/export button; five in-memory demo records, two-second toast notices, client validation/static references, no journal beyond updated_at.

**Owner:** X **9–44**, D **83–87** requires real API CSV, whole selection, row-limit errors, ordered fields, saved detail ID, dirty warning, flat group_distribution/surface_names and honest file delivery; no nested tables/sections payload. Root picker/toast descriptions prove neither file generation nor persistence/execution. No results dashboard or reporting pipeline is stated. Attachment-specific mock/export branches were not inspected and are not asserted.

### ABROOT-08 — Optional packaging, permissions and activation boundary

**Source:** S **1–9, 166–176**; H **[0], [9]–[10]**, lines **2, 11–12**. Administrative section, navigation and editing workflow. Entire root has no grants matrix, module feature flag or activation approval procedure.

**Owner:** M **9–35, 37–58**, P **7–12, 18–21**, D **17–31**: removable `app/optional/ab-testing/`, mocks in `mocks/ab-testing/`; registration in normal dev/typegen/production **without separate feature flag**; production includes section runtime, excludes mocks; existing mock/real configuration and session/access policy unchanged. Denied screens do not start business loading. Application composition alone connects public module API; shared/public entities allowed, cross-optional/business dependencies forbidden. No new grants/auth model. Collection approval is not experiment activation; saving configuration/status is not starting/stopping traffic. Root silence cannot authorize new permissions or execution.

## Architecture and evidence boundaries

Bounded chain: root UX/storage description → four existing capabilities → approved removable configuration-only owner. No implementation conformance claim.

- OM **5–10** identifies page v4 dated `2026-10-14T15:05:13.679+08:00`, captured `2026-10-19T11:33:31.678Z`.
- H **[0]**, line **2**, contains the body macro referencing attachment 250800308, `АБ_Тестирование_Прот.html`, version 2. Dotted table-name hyperlinks are inert markup, not API endpoints.
- O **13–33** separately records attachment index status 200, start 0, limit 100, **size 2**, **next null**: 250800308 (`АБ_Тестирование_Прот.html`, v2 URL) and 247742415 (`Прототипчик.html`, v1 URL). Index evidence only; neither body read/downloaded. No PDF/attachment behavior independently covered.
- DM **2–10** supplies attributed hashes and **parent-verified** concatenation equality. This run did not recompute hashes or independently compare H concatenation with O bodyView. Complete H review is not an independent integrity attestation.
- S **4, 157** asserts PDF consistency; S **163, 262** attributes tag restrictions to PDF. These are root claims, not fresh PDF review. D's historical HTML/PDF/image review is owner history, not this run's attachment coverage.
- No KB/dictionary/template/skill semantics imported by analogy. No new defaults, DTOs, migrations, auth model, algorithm assignment, control-group identity, statistics/attribution algorithms or runtime guarantees inferred.

## Start Here

Open `openspec/specs/ab-testing-registry/spec.md` **23–56** alongside archived design **40**: group-count availability is the clearest concrete owner difference. ABROOT-05/06 retain bounded per-group sample wording and storage naming/type differences. Candidates remain with existing owners, without a new implementation or activation plan.

## Validation and residual risks

Manual local reads and scoped citation checks only; all readable lines and exact chunks consumed, including truncation continuation. File lengths confirmed with local `wc -l`. No browser/network, attachments, rendering/source execution, business calls, tests/build, application-code census or nested delegation. Sole write is this report; no owner/source/archive/task edits. Git staging uninspected: no staging-state attestation.

Residual risks: attachments/PDF unverified; hashes/roundtrip parent-attributed; runtime/API/implementation outside scope; archived/current-owner differences unresolved as to precedence. Body completeness does not close attachment coverage, the module or global backlog.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Reviewed 319 readable lines and all 19 HTML chunks; eight stable source-to-owner candidates include exact citations and residual boundaries."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-AB-TESTING-ROOT-DOC.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"wc -l on four scoped specs, archive proposal/design and two metadata files","result":"passed","summary":"Confirmed exact owner/metadata line counts."}],
  "validationOutput": ["H 1–11 then 12–21 consumed after truncation; S 1–319 and scoped owners read; citation boundaries checked by scoped grep."],
  "residualRisks": ["Attachments/PDF unreviewed; integrity parent-attributed; no runtime verification or precedence resolution."],
  "diffSummary": "Only authorized bounded audit report written.",
  "reviewFindings": ["D 40 lists groups_count unavailable; R 25–27 and 46 enable typed metadata-backed conditions."],
  "manualNotes": "Tests prohibited/not run. Staging uninspected, so no no-staged-files claim. No global closure."
}
```
