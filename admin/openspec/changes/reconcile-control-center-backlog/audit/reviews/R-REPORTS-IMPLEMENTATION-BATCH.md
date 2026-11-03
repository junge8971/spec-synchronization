# Consolidated reports implementation review

## Review

**Verdicts:** constructor **ACCEPT**; CSV **REVISE** (one narrow evidentiary correction); scheduling **ACCEPT**. **ESCALATE: none.** Acceptance concerns static analysis only, not feature delivery.

Read all three complete candidates, complete current owner proposal/design/tasks/specs, corresponding SCENARIO reports/reviews, and relevant accepted IMPL916/root-document boundaries. Candidate hashes and checkout baseline are **parent-attributed** from the assignment; not independently recomputed. Prior publication, auth and historical approval conclusions remain attributed accepted evidence. No new auth assessment or policy interpretation performed.

### Independently verified shared boundary

Verified the registration chain once:

- `app/routes.ts:6–9`
- `app/application/constants/application-routes.constants.ts:1–6`
- `app/shared/config/application-routes.ts:9`
- `app/shared/config/constants/application-routes.constants.ts:104–113`
- `app/routes/reports.tsx:1–5`
- `app/pages/placeholder/index.ts:1`
- `app/pages/placeholder/ui/placeholder-page.tsx:1–10`

The connected report leaf contains only generic headings. It supplies neither constructor settings nor explicitly unavailable results/export/save UI. No report draft, action, transport or scheduler follows from that leaf. This is conditional on existing shell access, not an unconditional-visibility finding.

Written assertions independently checked:
- Navigation/config tests establish report link, active state and title—not report behavior.
- `app/application/ui/application-layout.test.tsx:49–57` mounts synthetic `Page content`; its no-fetch assertion at lines 15–30 is not report or application-bootstrap coverage.
- Candidate search-based absence claims remain bounded and attributed; this review did not repeat their inventories or establish repository-wide absence.

## Per-report disposition

### Constructor — ACCEPT

**Correct:** Existing builder implementation is established, but report compatibility/delivery is not.

`app/features/dialog-selection/index.ts:1`, `ui/dialog-selection.tsx:10–43` and `types/dialog-selection.types.ts:11–34` expose an actual editor with entity condition-group inputs and an apply callback. Its draft has phrase scope but no particular-skill identifier.

`app/pages/dialogs/ui/dialog-registry.tsx:18–24,38–75` connects it to dialog selection/query restart. That execution behavior must not be transplanted into the report-local draft.

Independently read `dialog-selection.test.tsx:62–183`: assertions cover unapplied edits, clear/apply, partial errors, 35 attributes/three disabled attributes, hidden-value cleanup, invalid ranges, keyboard focus and submitted-row error correspondence. They do not establish report integration or report-specific dictionary/privacy compatibility.

**Mandatory report fixes:** none.

### CSV — REVISE

**Correct:** No report CSV or planned unavailable-export action is mounted. Generic download and dialog-export evidence is correctly excluded from report delivery.

`app/shared/lib/handlers/download-attachment.ts:1–11` creates/clicks/removes an anchor. Its tests at lines 7–23 check URL/name forwarding and removal, including click failure—not HTTP, bytes, headers or report compatibility.

`app/features/dialog-export/model/use-dialog-export.ts:21–46` calls dialog APIs and manages object URLs. `ui/dialog-export.test.tsx:78–111` asserts dialog selection, 24 fields, parameter trailer and download cleanup—not report export.

**Finding: P2 — inaccurate stale-clause attribution.**

Candidate section **“Architecture and evidence layers”** says:

> Owner prose that no general file helper exists (`design.md:3`) is stale…

The actual MOS-919 `design.md:3` says:

> «ни API экспорта, ни общего файлового клиента сейчас нет»

A download-link helper is not a general file client. Separately, `design.md:23` says there is no export handler/download helper **in the current scope**; that scoped statement remains consistent with the unavailable-action plan.

**Smallest exact report correction:**

> A generic download-link helper and a separate dialog-export flow already exist. They do not establish a general report-compatible file client. MOS-919 design.md:3 should distinguish report-export absence from existing dialog-export infrastructure; design.md:23 remains valid as a current-scope restriction. No new helper or transport is authorized.

Keep the candidate’s remaining CSV findings and gates unchanged.

`mocks/analytics.mjs:42–105` independently confirms dashboard/refresh/widgets/board handlers; its “reporting sample” label is not report CSV/provider delivery. Registration at `mocks/app.mjs:41–78` does not change that distinction.

### Scheduling — ACCEPT

**Correct:** Local intention, durable configuration and scheduler execution remain separate states. The mounted placeholder demonstrates none of them.

MOS-1016 `tasks.md:3–9` explicitly requires the MOS-1015 base and component evidence before adding local name/intent controls. `specs/report-template-scheduling-draft/spec.md:21–51` requires disabled save, unchanged dates, no timer/hidden timezone and memory-only lifecycle. Missing controls cannot satisfy those positive obligations merely because no mutation occurs.

**Mandatory report fixes:** none. The disclosed empty external artifact is neither project mutation nor evidence.

## Existing-owner documentary disposition

| Clause | Smallest safe disposition |
|---|---|
| MOS-1015 `tasks.md:9–11`, especially “Создать управляемый `features/dialog-selection`”; `design.md:23` describing its own types/catalog | **Update through existing owner:** reconcile reuse/adaptation of the existing feature and entity-owned condition model. Retain unmet report integration/tests and particular-skill semantics. Do not recreate the builder or mark these tasks complete. |
| MOS-1015 `proposal.md:16`: blanket assertion that reports/dialogs documents report no operations | **Update factual rationale:** accepted documentary review establishes dialog contracts and published report documentation; saved report-schema absence and unapproved report integration remain separate. No activation follows. |
| MOS-1015 report spec `:9–14`, `design.md:53`, `tasks.md:15`: blanket no-profile/no-auth wording | **Carry forward the already accepted correction:** preserve normal application session/access boundary; do not interpret these clauses as a bypass. No new auth interpretation performed here. |
| MOS-919 `design.md:3` versus scoped `:23` | **Update only the overbroad rationale**, using the correction above. **Keep** the scoped no-handler/helper restriction and prohibition on speculative infrastructure. |
| MOS-1016 write/execution/timezone language | **Keep.** Published read metadata does not establish write/run policy. No additional plan correction is demonstrated by this implementation review. |

## Consolidated tasks and gates

- **MOS-1015:** keep current local-UI tasks open and B15.1–B15.5 blocked continuation separate.
- **MOS-919:** keep tasks 1.1–2.2 open; its mounted MOS-1015 prerequisite is unmet. Preserve B919.1–B919.4.
- **MOS-1016:** keep all six tasks open; preserve the same prerequisite and B16.1–B16.5.
- **MOS-916:** retain accepted template ownership/boundaries without repeating its audit.
- Named people/teams, runtime deployment, backend/fake-provider delivery and passing-test status remain unknown.

**Merge verdict:** **OK with notes** for the bounded evidence batch after the CSV wording correction; no feature/task/global G2 closure. No changes to Q1, permissions, API contracts or scope.

No project edits, shell commands, network, execution, tests/builds/browser/E2E or nested agents were used. No fixes applied.

**Artifact:** `/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/e600f884-0be1-4fc0-b94b-b9507c5a0887/reports-batch-review.md`