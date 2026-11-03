# Code Context

## Disposition

**Revise narrowly; retain the existing API/security gate and adequate coverage.** The extraction is substantively supported, but its “Explicit deferrals” label conflates analyst recommendations, review boundaries and source statements. The current change already covers server-authoritative availability, disclosure/rotation gates, expiry/scopes, shared sandbox metadata and secret-free navigation. Do not duplicate these or close implementation tasks.

## Files Retrieved

Paths below are repository-relative; source JSON files are single-line documents, so JSON selectors and wiki heading/row locators provide precision within line 1.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/RECON-MOS-1023.md` (lines 1–8): assigned scope and constraints.
2. `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-1023.md` (complete report): claims independently checked below.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-details-MOS-774/r1/content.json` (line 1, `$.items[12]`, key verified MOS-1023): description and identity only.
4. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-details-MOS-774/r1/metadata.json` (lines 1–10): snapshot provenance and limitations.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json` (line 1, `$.bodyView`): selected token/environment and sandbox-prerequisite passages, parsed as inert text.
6. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/metadata.json` (lines 1–13): version 17 and evidence limits.
7. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1): path names, schema names and token-related schema definitions only.
8. `openspec/changes/mos-1023-skill-environment-tokens/proposal.md` (lines 1–27), `design.md` (lines 1–26), `tasks.md` (lines 1–18), `specs/skill-environment-tokens/spec.md` (lines 1–47), `.openspec.yaml` (lines 1–2): complete assigned change.

## Key Code / Primary evidence

No implementation review was performed. Critical contract definitions in the saved API are `$.components.schemas.SkillConnectionSchema.properties.auth_type` → `SkillAuthType`, whose enum is `["transport_token"]`. Connection properties are endpoint, contract_version, auth_required, auth_type and parameters—not skill-token lifecycle metadata. No path name contains `token`, no token-named schema exists, and the only schema containing the string `token` is SkillAuthType. The skill paths under `/api/control/api/skills/v1/skills` contain no token operation. This supports absence of a published token contract **in this snapshot**, not a claim that backend functionality does not exist. The repository `docs/api/contracts/openapi.json` was not an assigned input and was not independently verified.

Source aliases below: J = Jira `$.items[12].description`; W = wiki `$.bodyView`, exact heading plus requirement/table row.

| Claims | Disposition and independently checked evidence |
|---|---|
| REQ-01–02; C1 | **Accept, retain conflict.** J explicitly requires server availability and “не выдан” only by server state. W “Карточка навыка: подключение (ПОД)”, ПРТ-ПОД-2 says inactive is marked unissued. Neither establishes that revoked/expired/inactive means never issued. Existing design Decisions and spec Server token metadata already prohibit treating error/unknown as unissued; keep them. Add the source conflict to the gate, not automatic precedence. |
| REQ-03–05, 11–12 | **Accept as source/model statements, not DTO mandates.** W ПОД-4–5 and ПРТ-ПОД-1 require environment cards and current-state active highlighting. W “7.3. Состав справочников и значения”, skill_token_environments rows give sandbox/whitelist/prod. W “5.2. skill_tokens” gives system-generated values, lifecycle fields, unique token_value and one active record per skill/environment. No frontend database schema or all-fields-visible requirement follows. Selection mapping remains undefined. |
| REQ-06–09, 21 | **Accept; plan under-explicit on copy and sandbox reissue.** W ПОД-6–7, ПРТ-ПОД-3; “G. Карточка навыка: подключение”, T-51 specifies Clipboard API and success toast; T-52 specifies confirmation/update. W “Песочница (ПЕС)”, ПРТ-ПЕС-5 explicitly includes reissue. Copy does not settle reveal permissions or value-return rules. Current rotation confirmation/unknown-outcome handling is sufficient and must remain. |
| REQ-10 | **Accept with ownership qualification.** W “5.2. skill_tokens” purpose requires issuance/revocation history; G/T-52 requires audit; “Аудит и история”, АУД-1–2 confirms token changes and history fields. This is a backend contract/audit obligation, not authority to add a new history UI or log secrets. |
| REQ-13–16; C3/G1 | **Accept unresolved policy, not explicit source deferral.** J asks for disclosure rules, validity periods, scopes and rotation consequences. W model has no expiry/scope definition; revoked_at is not expiry and environment is not scope. Existing design gate and task 1.1 adequately retain these questions. |
| REQ-17–18 | **Accept / keep existing coverage.** J explicitly requires skill ID without URL secret and shared token model; W “5.2. skill_tokens” usage selects verification-environment token. Existing spec Secret-safe sandbox integration and tasks 2.3–2.4 are adequate. Temporary-state cleanup, persistent-cache/log restrictions are existing plan decisions, not explicit Jira/wiki prescriptions; preserve them. |
| REQ-19–20, 22; G2 | **Accept narrowly.** W ПЕС-8 requires completed classifier training, ПЕС-9 isolation, ПЕС-5 connection context; ПОД-9 marks missing service address explicitly. These do not establish a full prerequisite matrix or prove missing endpoint/token blocks execution. Preserve proposal assignment of sandbox availability to MOS-1019; do not expand this change into sandbox engine or lifecycle review. |
| C2 | **Accept, independently corroborated against published snapshot.** W G/T-50 proposes GET/POST `/api/v1/skills/{id}/tokens`; T-52 proposes POST `.../tokens/{env}/rotate`. J says issue/reveal/revoke/reissue are undefined in API. Saved API has no skill-token operations/schema as detailed above. Wiki design is not publication evidence. |
| G3 | **Accept positive requirement; qualify negative inventory claim.** ПОД-7 explicitly says connection rotation is not shown in prototype, not deferred from delivery; ПРТ-ПЕС-5 explicitly requires sandbox reissue. The claimed omission from K/T-74–81 was not needed for disposition and was not independently re-audited. Do not use that omission to cancel or defer the positive requirement. |

## Architecture

The existing plan places one shared business-token model/API in `entities/skill`, used by connection and sandbox. Navigation passes skill ID; sandbox obtains authorized data through the eventual agreed API. Metadata may use normal Query cache; revealed values remain temporary and excluded from persistent storage/diagnostics. These are business integration tokens, not application-session auth. Unknown backend readiness remains a reporting limitation, not a blocker to this planning review.

## Minimal proposed planning corrections

These are recommendations only; no plan/source/task-status edits were made.

1. **Extraction report, “Explicit deferrals and scope decisions”:** rename to “Analyst recommendations, existing-plan gates and review boundaries”. Replace item 1 with: “Jira leaves disclosure, lifetime, scopes and rotation consequences unresolved; deferring implementation pending agreement is the current change’s design/task-1.1 gate, not an explicit source delivery deferral.” Keep capabilities required, other-work-item boundaries and all existing security decisions.
2. **`design.md`, first Decisions bullet; `tasks.md`, task 1.1:** extend the existing gate, rather than add a parallel workstream: “Reconcile ПРТ-ПОД-2 inactive→unissued with Jira server-state wording; agree explicit unissued/inactive/revoked/expired mapping and current-skill-state active selection. Confirm sandbox/whitelist/prod labels/codes; issuance trigger, disclosure-authorized copy, separate revoke versus rotate semantics, sandbox reissue target and backend issuance/revocation audit responsibility.” Record wiki endpoints as proposals, not adopted routes. Existing expiry/scopes and unknown-outcome clauses stay unchanged. These are missing source-policy details or plan traceability, distinct from absent published API.
3. **`specs/skill-environment-tokens/spec.md`, Server token metadata; `tasks.md`, 2.1:** add gated environment-card/current-active highlighting acceptance using the agreed mapping. Include a scenario where an inactive/revoked record is not silently relabeled unissued without the approved mapping. Do not invent extra environments or derive scopes from their names.
4. **Same spec, Controlled disclosure and rotation; `tasks.md`, 2.2:** explicitly include one-action Clipboard API copy for an active token when disclosure permits, success feedback only after successful copy, and safe failure feedback without exposing the value. Add copy success/failure and unavailable-disclosure component scenarios. Keep confirmation, cleanup, no optimistic rotation and no retry-after-timeout behavior. Failure feedback is a safety recommendation, not a quoted wiki requirement.
5. **`tasks.md`, 2.3 and corresponding spec sandbox scenario:** make the already scoped token integration include sandbox verification-environment selection and sandbox reissue using the same agreed rotation model/confirmation, without secret-bearing navigation. State that it preserves MOS-1019 readiness/isolation ownership and does not implement a new dialog engine. This closes the explicit ПРТ-ПЕС-5 traceability gap, not the whole sandbox backlog.
6. **Backend audit:** include history/audit confirmation in task 1.1 contract acceptance (item 2 above); no new FE history screen, secret storage field or audit API should be invented. No additional implementation task is justified before ownership/contract agreement.

**No-op areas:** proposal’s scope boundaries; unavailable pending API; explicit server not-issued state; expiry/scopes gate; confirmed rotation with unknown-outcome recovery; shared entity ownership; URL/storage/log protection; existing unchecked task statuses and validation plan.

## Open decisions / residual risks

- Product/backend must reconcile inactive versus unissued, current-state highlighting, disclosure/copy rules, expiry/scopes and rotation consequences without date-based or automatic source precedence.
- Issuance trigger, independent revoke action, sandbox reissue target, audit contract and readiness source remain unsettled. Do not synthesize endpoints from wiki suggestions.
- Snapshots exclude Jira comments/custom fields/attachment bodies and linked contract contents. No conclusion about live deployment or implementation compliance is made.
- No tests, generation, browser, network or source/status edits were performed; only the bound report was written.

## Start Here

Open `openspec/changes/mos-1023-skill-environment-tokens/design.md` (lines 11–17): extend its existing gate with the precise source conflict and missing copy/environment/sandbox/audit decisions, then mirror only those deltas into existing spec/task entries.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently checked MOS-1023, relevant wiki passages, saved API publication and complete assigned plan; supplied scoped accept/revise dispositions and minimal planning corrections."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-1023.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only local Python JSON/HTMLParser inspection of assigned primary snapshots and schema definitions","result":"passed","summary":"Verified Jira selection, token/environment/prerequisite passages and lack of published skill-token operations/schema; HTML inert, no credential values inspected."}],
  "validationOutput": ["Complete assigned change read; existing gates retained; no tests run because prohibited."],
  "residualRisks": ["Source state conflict and disclosure/lifetime/scopes/rotation decisions remain open.","Saved API absence does not establish live backend absence; linked contracts and omitted Jira evidence were not available within scope."],
  "diffSummary": "Only bound review report written; no source, spec or task-status edits.",
  "reviewFindings": ["Revise analyst-deferral attribution and make copy, active selection, sandbox reissue and backend audit traceability explicit within existing gated plan."],
  "manualNotes": "Independent source-to-plan review only; no module inventory, auth-policy decision, secret extraction, network, generation or test execution. No implementation task was closed."
}
```
