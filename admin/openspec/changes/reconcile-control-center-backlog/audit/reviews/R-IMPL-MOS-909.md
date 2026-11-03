# R-IMPL-MOS-909 — Independent static evidence review

## Review

**Verdict: REVISE — one mandatory evidence qualification in IMPL909-07.** The seven-versus-three discrepancy is independently confirmed.

- **Correct:** All ten IDs identify connected implementation and actual assertions. Tests are correctly distinguished from executed verification; auth/mock/runtime boundaries remain unexamined.
- **Fixed:** None. Read-only review.
- **Finding P1:** Four generic commands contradict the documented feature boundary; see IMPL909-03 below. No superseding approval was discovered within the bounded local search.
- **Finding P2:** IMPL909-07 must distinguish its non-409 refusal observation from the saved publication’s explicit **409 SKILL_CHECKS_BLOCKED**, which already enters the reread branch.
- **Merge verdict: BLOCK** for unconditional acceptance of the evidence report pending that qualification. This is not a product-remediation authorization.

Repository-relative aliases:

- **A** = `openspec/changes/reconcile-control-center-backlog/audit`
- **F** = `app/features/skill-lifecycle`
- **E** = `app/entities/skill`
- **W** = `app/widgets/skill-details/ui`
- **R** = `openspec/changes/archive/2026-10-02-mos-909-skill-lifecycle-rollout`

## Per-ID disposition

| Evidence ID | Verdict | Independent evidence and corrections |
|---|---|---|
| **IMPL909-01** | **ACCEPT** | Route registration at `app/shared/config/constants/application-routes.constants.ts:40–45`, application composition and `app/routes.ts:6–9` lead through route/page adapters to `W/skill-details.tsx:13–55`. One observed detail query supplies the header, lifecycle, dedicated toggle and tabs. `W/skill-details-header.tsx:18–24` renders server status and record version. Actual assertions at `W/skill-details.test.tsx:80–114,148–203` cover labels, refetched values, wrapping class, persistent header and GET counts. These are not root/session or browser-layout verification. No correction. |
| **IMPL909-02** | **ACCEPT** | `E/model/constants/skill.constants.ts:3–32` recognizes nine statuses. `E/api/skill-details-client.ts:15–51` strictly validates status; `F/constants/skill-lifecycle.constants.ts:5–6` excludes disabled from progression. `F/ui/skill-lifecycle.tsx:33–46` marks only equality as current. `W/skill-lifecycle.test.tsx:48–85` affirmatively checks eight items and no selected stage for disabled; client tests `:200–210` cover enum acceptance and malformed status rejection. Obsolete disabled-as-unknown specification wording remains documentary debt, not a defect to reintroduce. |
| **IMPL909-03** | **ACCEPT; scope disposition escalated to parent** | `F/constants/skill-lifecycle.constants.ts:9–17` contains seven actions. Four additional edges are **checking→training, training→autotest, autotest→sandbox and review→whitelist** (`:11–13,15`). `F/model/use-skill-lifecycle.ts:28–35` selects them by status; `F/ui/skill-lifecycle.tsx:62–84` mounts permission-wrapped triggers; `F/handlers/skill-lifecycle-handlers.ts:24–30` submits their targets. `W/skill-lifecycle.test.tsx:68–80` explicitly requires each button; `:87–136` exercises all seven transitions. Main lifecycle spec `:11,49` and D-018 retain only three. Scope discrepancy confirmed, not merely dead constants or backend enum breadth. No code/specification correction authorized. |
| **IMPL909-04** | **ACCEPT** | Snapshot creation and synchronous lock are explicit in `F/handlers/skill-lifecycle-handlers.ts:10–30`; ID/version/status equality and read/pending/recovery guards are in `F/model/use-skill-lifecycle.ts:29–35`. Dialog content and pending/stale controls are in `F/ui/skill-lifecycle-confirmation.tsx:25–55`. Tests `W/skill-lifecycle.test.tsx:106–125,205–226,278–294` assert double-click suppression, cancellation/focus, version staleness and recovery from failed reads. ID-only/status-only stale cases are code-supported, not separately asserted there. No correction. |
| **IMPL909-05** | **ACCEPT** | `F/handlers/skill-lifecycle-handlers.ts:24–30` creates a fresh UUID per confirmation and sends snapshot version/target. `E/api/skill-details-client.ts:68–86` validates request inputs and response identity. `E/model/use-change-skill-status-mutation.ts:9–12` disables mutation retry. The inspected JSON request path in `app/shared/api/http-client.ts:44–125` has one business fetch, not a POST replay loop. Exact transport/input/error assertions occur at client test `:124–172`; conscious new-key recovery is asserted at lifecycle test `:172–203`. Session preparation and production credentials remain outside this conclusion. |
| **IMPL909-06** | **ACCEPT** | `E/model/use-change-skill-status-mutation.ts:13–21` awaits detail-query cancellation, calls the session-ownership guard, commits the returned DTO and invalidates non-detail skill queries. `F/handlers/skill-lifecycle-handlers.ts:31–36` distinguishes actual status from requested target. `W/skill-lifecycle.test.tsx:138–170` resolves an older GET after the POST and asserts that committed data remains; `:126–135,296–307` assert invalidation and mismatch messaging. Registry evidence concerns an inactive seeded cache entry, not visible row refetch/rendering. Session-guard invocation is observed, not independently certified. |
| **IMPL909-07** | **REVISE** | Numeric classification, recovery guards and test assertions are correctly described. However, the saved operation explicitly labels readiness refusal **409 SKILL_CHECKS_BLOCKED** (`A/sources/api-live-status-readable/r1/content.json:8`, `/operation/description`). Every 409 enters `conflict` in `E/model/skill-status-error.ts:5–10`; `F/handlers/skill-lifecycle-handlers.ts:42` attempts reread. The no-reread observation applies to the classifier’s **other 4xx except 408**, not to readiness refusal under this published mapping. See mandatory correction below. |
| **IMPL909-08** | **ACCEPT** | `E/model/use-skill-details-query.ts:7–20` enables five-second observation only for processing statuses and non-error state, with background polling disabled; constants are at `E/model/constants/skill.constants.ts:15–20`. Passive multi-query code has no timer. Actual assertions at `W/skill-details.test.tsx:1050–1148,1193–1224,1277–1299` cover intervals, visibility, unmount, ID-change cancellation, failed-read recovery and a passive observer. The “without commands” test `:1150–1191` proves GET-only observation and absence of sandbox/retrain buttons—not absence of the four extra generic commands. No correction. |
| **IMPL909-09** | **ACCEPT** | Toggle and lifecycle are sibling features in `W/skill-details.tsx:38–54`. `app/features/skill-global-toggle/ui/skill-global-toggle-content.tsx:13–18` restricts its display to prod/disabled. `E/api/skill-global-toggle-client.ts:13–36` uses dedicated action paths, reason/version and disable-only fallback text, checking response identity/action. `W/skill-global-toggle.test.tsx:58–103` asserts exact dedicated POST, fields, two GETs and server version +7. This remains limited call-boundary evidence, not a complete toggle/session/permission audit or runtime propagation attestation. |
| **IMPL909-10** | **ACCEPT** | `E/api/skill-details-client.ts:15–51` validates process strings/nullable metadata but declares no checks validator. `app/shared/api/schema.d.ts:5014–5071` likewise has no checks member. Saved namespaced response schema requires checks (`A/sources/api-live-status-readable/r1/content.json:852–888`). The loose schema can preserve extra fields; it does not validate their check structure. `W/skill-details-tabs.tsx:34–36` passes only status to checks UI; overview/checks components render placeholders, not check results. Client test `:175–198` checks process metadata, not readiness rendering. This supports bounded contract coverage and wording observations, not required activation or a demonstrated stale-readiness bug. |

## Mandatory correction — IMPL909-07

Replace the “Bounded gap” interpretation with an explicit distinction:

> The handler does not itself reread or invalidate after refusals classified as `rejected`—HTTP 4xx other than 408 and 409. The saved publication explicitly describes `SKILL_CHECKS_BLOCKED` as HTTP 409; the inspected classifier therefore treats that published response as a conflict and attempts a GET. Consequently, this evidence does not establish missing reread of persisted checks on published readiness refusal. Business-code-specific messaging is absent, and deployed behavior remains unverified.

Supporting assertions at `W/skill-lifecycle.test.tsx:256–275` expect **GET/POST/GET for 409**, **GET/POST for 422**, and exactly one POST in both cases. They use a generic validation-shaped rejection fixture—not a `SKILL_CHECKS_BLOCKED` response or persisted-check fixture.

The publication provides a concrete HTTP mapping in prose even though its explicit response schemas enumerate only 200/422. Preserve both facts. “Real backend mapping unverified” is appropriate for deployment, but must not obscure the saved mapping.

This correction changes evidence interpretation only. It does not authorize changing error handling, adding checks UI or tests, or regenerating DTOs.

## Independent challenge of seven versus three

### Confirmed contract contradiction

The mounted generic matrix is broader than the documented feature contract. Its four additional buttons share the normal permission wrapper; no per-stage restriction in the inspected feature removes them.

The separate review approval does **not** supersede that boundary:

`openspec/changes/archive/2026-10-02-mos-1020-skill-review/design.md:19` explicitly says **not to expand `skill-lifecycle`**, assigning review→whitelist to the review capability rather than the ordinary card.

Likewise:

- `R/design.md:17–30` explicitly rejects a linear “Next” action and lists no generic command for checking/training/autotest/review.
- `openspec/changes/archive/2026-10-02-mos-1019-skill-checks-training/proposal.md:21,27` preserves existing commands and adds observation, not transitions.
- D-018 retains the three-command/current-state MVP.
- Broader published backend transitions and affirmative implementation tests establish neither frontend approval nor source precedence.

### Search boundary

Local searches covered:

1. Current main lifecycle and global-toggle specifications, read completely.
2. `openspec/changes/**/proposal.md` and `**/design.md`, searching `MOS-909`, `skill-lifecycle` and the additional processing transitions.
3. Archived Markdown with those same lifecycle identifiers/transitions.
4. Discovery of all `openspec/changes/**/specs/skill-lifecycle/spec.md`.
5. D-018 and the complete accepted SCENARIO-MOS-909 report/review.

The initial broader changes search reached its result limit; narrower proposal/design/archive searches supplied bounded, non-result-count-truncated results. Relevant rollout/review designs and observation proposal were read fully rather than relying on truncated matching lines.

**No explicit superseding local approval was discovered within these bounds.** This is not proof that no approval exists in external conversations or undiscovered artifacts. Parent retains the unresolved approval/disposition question. The concrete mismatch against current local requirements is established without choosing a remedy.

## Publication and provenance

Compared local DTO/validator/UI only with the saved `api-live-status-readable/r1` packet and its original metadata. Independently read the relevant request, status enum, envelope/reference chain, check response and namespaced detail schema, plus operation prose.

Preserved distinctions:

- Checks is a required array without a minimum count/all-five guarantee.
- Training/autotest are strings; ETA/note are required nullable strings.
- These fields establish neither completed lifecycle history nor current-phrase-revision binding.
- Readiness refusal can preserve recalculated checks without changing status/version/history.
- None of this proves deployed behavior or requires readiness UI activation.

Original metadata records retrieval on **2026-10-16T11:13:29.451Z**. The readable packet is a later local derivation, not a fresh publication inventory. Metadata hashes and the author’s working-file hashes/HEAD are **attributed, not independently recomputed or verified by this reviewer**. No Git cleanliness or committed-range attestation is made.

## Review boundaries

Read the complete assigned report/work-items, D-018, accepted scenario report/review, both main specifications, complete lifecycle feature files, detail client/tests, mutation/error/query files, and the cited widget/toggle/route/schema ranges. Widget test inspection covered `:1–205` and `:1043–1302`; no complete widget-test-suite review is claimed.

Explicitly unexamined:

- Auth/session enforcement and permission implementation.
- Express handlers, mock/demo selection and production packaging.
- Full dedicated-toggle, review and bulk business flows.
- Backend transition enforcement, readiness execution, replay, queues, history and runtime propagation.

Permission wrappers and session-helper calls are dependency observations only. Historical auth/toggle approvals remain preserved, not reopened or re-attested.

**No project edits, test/build execution, network/browser activity, endpoint calls, credentials operations or delegation occurred.** Existing assertions were read, not passed. No remediation, specification expansion, feature/task closure or archive/sync action is authorized.