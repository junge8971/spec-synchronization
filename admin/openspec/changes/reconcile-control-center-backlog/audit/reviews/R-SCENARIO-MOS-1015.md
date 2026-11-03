# Independent review — MOS-1015

**Designated artifact:** `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-1015.md`

**Verdict: ACCEPT WITH CORRECTIONS.** The substantive field/selection reconciliation is supported. The original report’s index attestation is expressly rejected. Acceptance is limited to documentary analysis, not implementation, runtime availability, task closure or source precedence.

Original and repository files were not edited.

## Files Retrieved

`A` = `openspec/changes/reconcile-control-center-backlog/audit`.

- `A/reports/SCENARIO-MOS-1015.md` (1–134), `A/work-items/SCENARIO-MOS-1015.md` (complete), `A/work-items/R-REPORTS-WAVE.md` (complete), `A/work-items/REPORTS-PUBLICATION-HANDOFF.md` (1–7).
- `A/sources/jira-reports-details/r1/content.json`, `/items/1` and `/items/4`, and complete metadata.
- `A/sources/wiki-241085838/r1/content.json` (version and line 39 `/bodyView`, including §§1.1–1.3, 1.5, 2.1, 2.4), and complete metadata.
- `A/sources/wiki-241085439/r1/content.json` (line 39 `/bodyView`, §§2.4.1–2.4.5, 2.5.4–2.5.6 and relevant §2.7 mappings), and complete metadata.
- `A/sources/api-live/r1/content.json` (line 1: paths, operation IDs, schemas, complete selection/card dependency definitions), and complete metadata.
- `openspec/changes/mos-1015-report-constructor/proposal.md` (1–33), `design.md` (1–100), `tasks.md` (1–27), `specs/report-constructor-draft/spec.md` (1–128), `specs/dialog-selection-draft/spec.md` (1–116): complete.
- `openspec/specs/dialog-selection-builder/spec.md` (1–67), `openspec/specs/dialog-registry/spec.md` (1–101): complete.
- Complete archived auth prerequisites: `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md` (1–38), `design.md` (1–171), and all six specs: `control-center-api-integration` (1–64), `control-center-http` (1–71), `control-center-mock-server` (1–27), `control-center-permissions` (1–89), `control-center-shell` (1–101), `mpmm-session` (1–138). Historical tasks closing paragraph also inspected.
- Complete archived demo prerequisites: `openspec/changes/archive/2026-10-09-add-local-session-demo/proposal.md` (1–28), `design.md` (1–70), and specs `control-center-mock-server` (1–106), `control-center-shell` (1–55), `local-session-demo` (1–123).
- `docs/mpmm-auth-rollout.md` (1–58), `docs/api/contracts/reports.md` (complete).

## Mandatory corrections

### 1. Unsupported index attestation — high severity

**Location:** Original report lines 129 and 132.

`"noStagedFiles": true` contradicts the explicit disclaimer that the index was not inspected. Redefining this field as “no staging by this run” does not establish an empty index.

**Required correction:** In the publication/acceptance record, remove this positive attestation or mark index status explicitly unknown using the supported schema. Preserve the original as historical evidence and attach this review’s correction. Do not claim either staged-file presence or absence.

### 2. Builder agreement must not imply inspected implementation — medium severity

**Locations:** Original report lines 87–94.

The report generally separates requirements from delivery, but “do not … treat it as unavailable globally” can imply an existing usable implementation. No product code was inspected.

**Required replacement qualification:**

> The main specification records acceptance of selection semantics and shared builder requirements. This review does not establish that a reusable builder implementation exists, is complete, or is operational. Reconcile the report plan with that agreed ownership; implementation reuse requires separate code inspection.

**Evidence:** `openspec/specs/dialog-selection-builder/spec.md:9–20,32–57`; `openspec/changes/mos-1015-report-constructor/tasks.md:9–11`.

### 3. Preserve published missing-value evidence while leaving report DTO nullability unresolved — low severity

**Locations:** Original report field table and remaining mapping questions.

The report correctly identifies nullable dialog fields, but should explicitly preserve the report wiki’s already-published CSV missing-value convention rather than leaving every “null convention” apparently undefined.

**Required clarification:**

> Report wiki §1.2 specifies an empty CSV string for every listed field when no value exists. Preview §1.5 demonstrates `operator_rating: null`. These facts do not define exhaustive JSON nullability or approve conversions from dialog DTOs for all 24 UI columns.

**Primary locator:** `A/sources/wiki-241085838/r1/content.json:39`, `/bodyView`, §§1.2 and 1.5.

## Independently verified findings

### Fields: 24 UI rows, 18 published fields

The 24-row list comes from `report-constructor-draft/spec.md:73–100`; Jira requests 24 but does not enumerate all names.

The report wiki §1.2 publishes exactly:

`chat_id`, `session_id`, `sso_id`, `channel`, `started_at`, `dialog_transcript`, `user_messages`, `operator_messages`, `ended_at`, `bot_duration`, `end_reason`, `ended_by`, `operator_rating`, `rating_comment`, `low_rating_reason`, `topic_categories`, `error_target_answer`, `widget_button`.

Exactly six UI rows lack report-field rows:

| UI row | Missing concept | Dialog-only evidence |
|---|---|---|
| 4 | Authorization | `UserResponse.authorization`, `authorized_at` |
| 6 | Participants | `DialogCardResponse.participants` |
| 13 | Dialog steps | `step_count`, distinct from `skill_step_count` |
| 14 | Attachments | `attachment_counts.total` |
| 15 | Attachments to operator | `attachment_counts.to_operator` |
| 18 | Assistant answer ratings | `messages[].rating`, skill/subsystem authors |

These are **six absent rows, not six sufficient additions**:

- `bot_duration` explicitly means time with the robot, not full `duration_sec`.
- `low_rating_reason` is labeled “Причина низкой оценки ответа”; it cannot silently become operator-rating reason.
- `rating_comment` does not establish operator ownership.
- `topic_categories` includes topic and categories, requiring presentation agreement.
- `ended_at`, `error_target_answer`, and `widget_button` already exist in report publication.
- Dialog `user.sso_id`, `ended_at`, `ended_by`, `end_reason`, and operator rating/reason/comment are nullable. Report JSON conversions remain unapproved.

Primary evidence: report wiki §1.2; dialog wiki §§2.4.5, 2.5.4–2.5.6; saved OpenAPI `/components/schemas/{DialogCardResponse,UserResponse,AttachmentCountsResponse,MessageResponse,RatingResponse}`.

### Selection and phrase scope

The report request publishes only `period`, nullable `channel_id`, and ordered nonempty `field_codes`. It does not publish advanced selection.

Dialog selection has one all/any condition group, no nested groups, bounded conditions/text/lists, and AND composition with quick filters. `ConditionBody` has no per-condition skill ID. `scope=skill` covers skill replies collectively; global `skill_ids` selects dialogs with participating skills, not messages from one selected speaker.

Thus the particular-skill requirement in `dialog-selection-draft/spec.md:100–107` remains a genuine unresolved difference. No invented field or global-filter substitution is justified.

### Preview and metrics

Report wiki §§1.5/2.4 specify the first five selected columns, first twelve rows, full-selection `total`, and empty metrics `0/0/0/null`. §1.3 defines shares in `[0,1]` and absent average rating as a dash.

The active design already preserves the all-column prototype versus five-column publication conflict and whole-selection metric/formula gates: `design.md:90–96`. This is an existing plan, not missing planning. Neither the generic `average_rating` name nor preview examples prove operator-only averaging, complete denominators, or implementation.

### Publication versus delivery

All four recomputed SHA-256 values match metadata and the original report:

- Jira: `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c`
- Report wiki v3: `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74`
- Dialog wiki v15: `974ea35aaf44b9ec7c14c573ba58bdf7ed55397a9ca47d62b37fb39d9886f8bc`
- OpenAPI 0.1.0: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`

Saved OpenAPI contains no report paths, report operation IDs or report-named schemas. Existing analytics dashboard/widget/board paths are not report operations. Absence is a valid finding, not an execution blocker or proof of backend absence.

MOS-885 requests an isolated fake backend provider, explicitly excluding real dialog retrieval. Its Backlog status and requested DoD prove neither delivery nor enforcement. That provider is distinct from frontend Express/demo fixtures. MOS-1015 remains Hold; “Переключился на навыки” is not cancellation.

## Preserved auth and planning boundaries

Stale report wording is real: proposal line 16 broadly claims dialog-contract absence; report spec lines 9–14, design line 53, and tasks line 15 prohibit auth requests without distinguishing shell bootstrap.

The original report correctly requests reconciliation, not an auth bypass or new permission model. Archived shell requires business UI after session/access boundary; permissions spec lines 23–36 retains explicit `*` for reports. Demo full access does not create unavailable APIs.

**Historical approval remains closed:** `docs/mpmm-auth-rollout.md:5,24–33` and the archived auth tasks closing paragraph record the user’s 09.10.2026 confirmation. Earlier prerequisite wording about an open gate does not reopen that later confirmation. Approval is not agent-run backend verification, deployment evidence, or approval of missing report operations.

## Start Here / bounded owner questions

First read `openspec/changes/mos-1015-report-constructor/design.md:90–96`, then apply the three documentary corrections above through the parent-owned publication workflow.

Remaining integration questions are limited to the 24-field wire/type/null/display matrix, duration/rating ownership, report selection/timezone/all-time support, particular-skill phrases, preview limits, whole-selection formulas, and provider/API delivery evidence. None blocks this review. No implementation activation, product deferral or source precedence is inferred.