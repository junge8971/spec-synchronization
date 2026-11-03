# Independent review R-SCENARIO-MOS-923

## Result: REVISE

The 18 candidate atoms and Q01–Q07 are substantially supported by fresh local primary-source comparison. Two report corrections are required: preserve the recorded auth release approval explicitly, and classify overlap questions as scope ambiguity rather than an established rule contradiction. No implementation/plan authorization, precedence decision, task closure or feature activation follows from this review. No blocker prevented review; no supervisor decision was needed.

## Findings and safe corrections

1. **Material — historical approval is missing from the gate summary.** `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-923.md:88–92` correctly says this capture does not validate runtime, but leaves a misleading generic outstanding-auth-gate implication. `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/tasks.md:48–52` records checked 6.3 and the user's 09.10.2026 confirmation; `docs/mpmm-auth-rollout.md:3–5,24–33,53–56` explicitly distinguishes that approval from agent runtime tests and renewed confirmation for changed deployment. **Correction:** state that the prior release gate was closed by user confirmation, not independently tested by this review; applicability to a changed deployment or new maintenance integration remains unverified. Do not reopen the general gate merely because this capture lacks tests, and do not extend prior approval into maintenance delivery. Historical demo planning text about an open gate is not grounds to erase the later explicit confirmation.

2. **Material classification correction — conflict versus winner selection.** Report `:43,63` calls the relationship a “tension” and asks to “reconcile” it. In `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241092242/r1/content.json`, `/bodyView` §1.5 chooses the output winner among overlapping windows, with equal priority/equal specificity resolved by later `updated_at`; §§2.6 and 2.8 reject creation/edit producing equal-priority overlap with the **same scope**. Equal specificity is not necessarily identical scope; admission validation and output arbitration are different cases. No contradictory decision for a proven identical case is established. **Correction:** label Q03 a scope/applicability ambiguity; ask what same scope means (equal target sets, intersecting sets, hierarchy), when accepted same-specificity overlaps arise, and which states participate. Retain server authority, priority ordering and the documented conflict. Do not invent a client scheduler or resolve the question by choosing one rule.

3. **Precision — bounded discovery is not absence of ownership or approved deferral.** Report `:23,71,84–86` generally qualifies discovery correctly. My scoped pass of main specs and non-archived proposal/design/tasks/spec files likewise found shell/permissions and MOS-1026, not a dedicated MOS-923 CRUD plan. That does not prove no owner exists, no code exists, or product approved postponement. Jira `/items/4` contains no assignee field, and metadata explicitly says custom fields were uncollected; wiki `/version/by` identifies a revision author, not the accountable implementation/decision owner. **Correction:** make “DEFER” explicitly a bounded no-action recommendation for this audit, not an approved product disposition; request accountable ownership separately if future planning needs it. No forced plan creation follows from discovery absence.

4. **Minor wording — schema omission.** Report `:40` says the schema “cannot express state restrictions”; the inspected request DTO does not encode restrictions tied to existing server state. Prefer that precise formulation over a general claim about schema expressiveness. Report `:53–57` correctly rejects inferring deployed acceptance/enforcement from missing `minItems`, timezone validation, UUIDv7, interval order, domain errors or state constraints. Preserve those qualifications.

## Independent candidate/question check

Primary locators below refer to `A = openspec/changes/reconcile-control-center-backlog/audit`, `W = A/sources/wiki-241092242/r1/content.json /bodyView`, `S = A/sources/api-live/r1/content.json /components/schemas`, and `J = A/sources/jira-operations-details/r1/content.json /items/4/description`.

| Candidates | Fresh comparison and question disposition |
|---|---|
| C01 | W §2.5 and published collection GET agree on state, target_type, query, limit/offset and pagination. API limit 1–100/default 20 and offset ≥0/default 0 are explicit, not permission for hidden form defaults. |
| C02–C06 | J, W §§1.4/2.6 and S CreateMaintenanceWindowRequest support explicit title/timezone/start/end/warning. Strict start < end, valid timezone and nonnegative warning are already prose requirements; schema warning minimum 0 agrees. Q02 appropriately leaves DST, zone/offset agreement and boundary behavior unanswered, not newly required algorithms. |
| C07 | W §§1.2/2.6 require type/id/name and at least one affected scope; assistant key and other targets' UUIDv7 are explicit. S MaintenanceScopeRequest/TargetObjectRequest lack minItems and ID constraints. This is not evidence that invalid IDs or zero targets work. Q05's eligible-reference source remains a question, not proof no reference API exists. |
| C08–C10 | W §1.4 marks texts required-nullable in the window model; S MaintenanceWindowResponse agrees. S CreateMaintenanceWindowRequest makes the three nullable texts optional. W create example supplying them is not a formal request required-list. Q04 preserves omission/null/empty ambiguity; do not import ordinary-stub empty-string rules into window text automatically. |
| C11/C17 | J reserves overlap computation to server; W §1.5 supports active maintenance over ordinary stub, priority, specificity surface > skill > module > assistant, then updated_at; completed no longer affects output. Q03 needs finding 2's classification correction, not deletion. |
| C12/C13 | Five state values match S MaintenanceWindowState. W §1.1 defines draft, scheduled, active, automatic completion and manual cancellation; create example is scheduled. POST creates a summary, GET detail supplies timezone/scope/text/by. Q01 correctly leaves draft/publish commands unknown: neither request schema carries state; is_currently_applied is not established as a lifecycle switch. |
| C14/C15 | W §2.8 allows pre-start fields, freezes starts_at/timezone/scope.targets after start, permits ends_at/texts/warning, and prohibits terminal edits. S UpdateMaintenanceWindowRequest has optional-nullable fields including timezone/is_currently_applied. Active title/priority and application write authority are not explicitly resolved. Q04 is justified, without treating nullable input as permission to erase required detail fields. |
| C16 | W §2.9 limits cancel to draft/scheduled/active, excludes completed and stops text influence after cancel. Completion during request is a conflict with refresh, not success. S CancelMaintenanceWindowRequest requires a string reason without nonempty constraints. Q06 must keep that known race result while asking exact response/idempotency/repeated-cancel behavior, not reopen whether completed cancellation is allowed. |
| C18 | W §2.10 gives field errors and domain/status conflicts; published five operations document success plus HTTPValidationError 422 (`detail[].loc/msg/type`). Success envelopes reference ErrorItem; ResponseCode is string. Other undocumented HTTP responses may still occur. Q06 properly leaves concurrency tokens, idempotency and uncertain outcomes unproven, with no automatic mutation replay. |

**Q07 verified:** exactly five maintenance-window operations are published under `/api/control/api/maintenance/v1/maintenance-windows` (GET/POST), `/{window_id}` (GET/PUT), `/{window_id}/cancel` (POST), versus W §§2.5–2.9 `/api/control/api/assistant-ops/v1/maintenance-windows`. This is a genuine path discrepancy, not absent API or runtime proof. Page revision 4, wiki contract v1.0, OpenAPI 0.1.0 and Jira statuses are different provenance dimensions, not precedence.

## Existing boundaries retained

- `openspec/specs/control-center-shell/spec.md:144–218,266–267`: existing canonical tab, legacy redirect, query/history/access and honest unfinished-content boundary. KEEP means preserve specified capability, not certify runtime implementation.
- `openspec/specs/control-center-permissions/spec.md:1–91`: confirmed explicit `*` for maintenance reads/writes; roles do not grant rights; object access remains server-owned. No invented Maintenance resource or reuse of Module grants. Saved security alternatives do not undo approved paired raw headers.
- `openspec/changes/mos-1026-skill-operations-info/proposal.md:1–27`, `design.md:1–26`, `tasks.md:1–18`, `specs/skill-operations-info/spec.md:1–47`: read-only period/reason and wider operational sources, with an existing API gate. Collection target_type is not a skill-ID projection; list summaries omit scope. Neither publication nor this review closes MOS-1026 or converts it into a window editor.
- MOS-754 `/items/1` requests contract preparation/examples and is Review; MOS-923 `/items/4` is Backlog. Neither proves acceptance or delivery. Stub overlap was inspected only as dependency context, not a whole stub/code audit.

## Evidence and files retrieved

Fresh local SHA-256 checks matched saved metadata exactly:

| Content file under A/sources | Bytes | SHA-256 |
|---|---:|---|
| `jira-operations-details/r1/content.json` | 9,933 | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| `wiki-241092242/r1/content.json` | 68,316 | `e7b78965be979f2bd450b25881574cf7e8b94cf424be5d052bb2be9df1995158` |
| `api-live/r1/content.json` | 413,007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |

Read corresponding metadata in full (42/54/19 lines). Verified Jira item keys/status/update times and empty comments/attachments/subtasks for items 1/4; wiki capture status 200, revision 4 at 2026-09-25T16:59:13.813+08:00, contract v1.0 and attachments count 0; API title/version, capture URL/time and null ETag/Last-Modified. Metadata provenance remains a collector claim, not a repeated network verification. JSON pointers above identify exact inspected content; API content is one serialized line. Wiki HTML was decoded only as inert text.

Prerequisites read before access/security conclusions: all proposal/design/spec files of `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/` and `openspec/changes/archive/2026-10-09-add-local-session-demo/`, plus both tasks files. Especially auth design §§7–10 and migration/release requirements; demo specs preserve credential-free mocks, fixed profiles, presentation-only permissions, no invented API success and production isolation. Historical rollout confirmation was independently read as cited above. Report and exact assignment were read in full. Local discovery was limited to names and main/active planning documents; source/runtime implementation was not inspected.

## Start here / residual risks

First correct report lines 88–92 against archived auth tasks 48–52 and rollout status 3–5. Then narrow Q03 using the distinct wiki cases. Keep Q01–Q07 as unresolved consumer-contract questions, not settled product requirements. Runtime enforcement, deployment applicability, scope reference completeness and accountable decision ownership remain unverified. This review grants no writer authorization. Only this review report was intentionally written; no network/MCP/browser/tests/build/generation, source/product/code edits, task mutation, archive/sync or index inspection/attestation occurred.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent primary-source comparison covers C01–C18/Q01–Q07, provenance checks, approval distinction, corrections and residual risks."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-923.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local Python JSON/hash inspection and scoped planning-document search; read/find/nl/wc inspection","result":"passed","summary":"All three source hashes match; five window operations and contract differences independently verified."},{"command":"tests/build/browser/network","result":"not-run","summary":"Prohibited by assignment."}],
  "validationOutput": ["Decision: REVISE; historical approval and overlap classification corrections required."],
  "residualRisks": ["No runtime or deployment verification; contract questions and accountable ownership remain unresolved."],
  "diffSummary": "Only designated independent review report written; no source or product changes.",
  "reviewFindings": ["Material: report 88–92 omits recorded auth release approval.","Material classification: report 43/63 conflates same-scope admission conflict with same-specificity output arbitration."],
  "manualNotes": "Read-only local evidence review apart from bound report. No index state inspected or attested; no task closure or activation authorized."
}
```
