# R-SURFACE-CONFIG — independent review

## Decision

**ACCEPT** `reports/SCENARIO-SURFACE-CONFIG-r2.md` as a bounded contract/planning-evidence handoff. All material claims checked below are supported, including its qualifications. No blocking revision. Acceptance does not activate the configurator, establish deployment/runtime correctness, complete Jira work, or supersede the approved deferral. No earlier audit was used as authority.

# Code Context

## Files Retrieved

Paths are repository-relative; `A` expands to `openspec/changes/reconcile-control-center-backlog/audit`.

1. `A/work-items/R-SURFACE-CONFIG.md` (1–6): assignment.
2. `A/reports/SCENARIO-SURFACE-CONFIG-r2.md` (1–130): review target, not primary evidence.
3. `A/sources/api-live/r1/content.json` (1, selected JSON pointers) and `docs/api/contracts/openapi-2026-10-15.raw` (1, corresponding pointers): current/historical scoped operations and schemas.
4. `A/sources/jira-api-delta-scenarios/r1/content.json` (43–69; `/items/2`, `/items/3`): MOS-1237 and MOS-959 only.
5. `A/sources/api-live/r1/metadata.json` (1–19), `A/sources/jira-api-delta-scenarios/r1/metadata.json` (1–8): provenance.
6. `openspec/specs/surface-registration/spec.md` (1–78, especially 23–59): atomic optional configuration and recovery.
7. `openspec/specs/surface-overview-connection/spec.md` (1–123; relied on 9–45, 56–78, 101–123): saved values, exact embed text, skill-save recovery ownership. No separate lifecycle/checklist review.
8. `openspec/specs/surface-skill-selection/spec.md` (65–145): draft, deduplication and persistence boundaries.
9. `openspec/specs/surface-lifecycle-publication/spec.md` (177–198, especially 179–192): configurator deferral only.

## Key Code / evidence and dispositions

API pointers below apply to current JSON line 1 and historical raw line 1. Literal prefixes: `S=/paths/~1api~1control~1api~1surfaces~1v1~1surfaces`, `C=/components/schemas`. Concatenate suffixes literally: `CREATE=S/post/description`, `SAVE=S~1{surface_id}~1configuration/put/description`, `DETAIL=S~1{surface_id}/get/description`, `SKILLS=S~1{surface_id}~1enabled-skills/put/description`. All four descriptions are absent historically.

| Claim | Disposition and independently verified evidence |
|---|---|
| Exact-name documentation blocker resolved | **Accept.** SAVE allows `{имя}`, `{отчество}`, `{время суток}` and rejects other words in braces/unpaired braces. Jira `/items/3/description` names missing exact placeholders as a possible issue. Only the publication gap is resolved, not full parser semantics or product approval. |
| MOS-1237 is not completed by publication | **Accept.** Jira `/items/2/status` is `Ready for test`; description names greeting/fallback/suggestions/card validation and blank/space concerns. `/attachments/0` describes `mos-1237-test-plan.md`, not its contents. Numeric limits come from API, not this task. |
| Greeting and conditional fallback | **Accept.** `C/UpdateSurfaceConfigurationRequest/properties/greeting` adds lengths 1–500; fallback adds maxLength 500 without minLength. `/required` includes fallback. SAVE permits only time-of-day substitution in fallback; it must be nonempty with name/patronymic in greeting, otherwise may be empty. Missing and empty differ. Unconditional nonempty fallback is not supported. |
| Suggestions/cards bounds | **Accept.** Same schema `/properties/suggestions` adds maxItems 5 and item lengths 1–100; `/properties/cards/maxItems=4`. SAVE allows empty lists and prohibits repeated suggestions; no uniqueItems or comparison algorithm. `C/SurfaceCardRequest/properties/title` adds lengths 1–100, subtitle 1–200; required title/subtitle/action and accent default false remain. |
| Appearance vocabulary | **Accept.** Update request accent pattern `^#[0-9a-fA-F]{6}$`; `C/SurfaceConfigurationShape/enum=[round,moderate,strict]`, `C/SurfaceConfigurationFont/enum=[moscow_sans,system,golos_text]`, unchanged historically. No design/preview fidelity follows. |
| Actions and safety | **Accept.** `C/SurfaceCardActionType/enum` expands `[message,skill]` to `[message,skill,link]`; `C/SurfaceCardActionRequest/properties/value/minLength=1` is new. SAVE supplies message ≤500, canonical lowercase skill UUID, absolute HTTPS link ≤2000, query allowed, credentials/fragments forbidden. Type-dependent limits are prose rules, not generic value schema constraints. Opening context and preview execution remain unspecified. |
| Optional create/full save | **Accept.** `C/CreateSurfaceRequest/properties/configuration/anyOf` references the update DTO or null; configuration is absent from required. CREATE gives defaults #B3121B, round, moscow_sans, both greetings “Здравствуйте! Чем помочь?”, empty lists. Registration spec 23–40 explicitly covers omission/null and one POST. SAVE replaces all configuration; seven top-level fields are required historically and currently. No hidden default-filled PUT follows. |
| Create/save asymmetry | **Accept.** CREATE validates card skill UUID format only, deferring existence/connection to first save. SAVE requires connected, not deleted at save time. Atomic creation does not imply full reference integrity; silently tightening create policy is not authorized. |
| Normalization | **Accept with report's qualification.** SAVE trims text edges; CREATE distinguishes untrimmed surface fields from configuration. Skill UUID canonicalization is explicit. Trim/length ordering, Unicode counting and duplicate equality are not established. Do not weaken documented nonempty rules merely because whitespace-edge sequencing remains untested. |
| Error mapping/precedence | **Accept.** CREATE lists first failing stage and `/configuration/...` errors under 422 VALIDATION_ERROR. SAVE checks body before surface lookup; invalid path with valid body →400 INVALID_ARGUMENT at `/surface_id`, both invalid →422; all body errors together, missing field REQUIRED otherwise INVALID. Examples `/greeting`, `/suggestions/0`, `/cards/1/action/value`. No universal first-error/all-errors or authentication-order guarantee follows. |
| Stale references | **Accept as explicitly qualified implication.** SKILLS replaces all skills, empty disconnects all, and says cards referencing disconnected skills are not rechecked. SAVE checks connection/deletion later. Retained-card/read/rejected-save is a justified candidate sequence, not runtime observation or an explicit requirement for automatic cleanup/blocking disconnect. |
| Readback/timestamps | **Accept.** DETAIL returns saved configuration; SAVE preserves token and embed_code. SAVE/DETAIL describe updated_at as creation/latest status change, not config save; SKILLS leaves it unchanged too. Unchanged timestamp is not proof of save failure. Overview spec 29–45 independently requires exact server embed text. |
| Duplicate-skill 500 | **Accept, narrow handoff only.** CREATE/SKILLS document unchecked repeated skill_id ending in 500. Skill-selection 71–83 requires each skill once. This is documented defect behavior, not desired 422 acceptance behavior or permission to send duplicates. |
| Preview | **Accept.** Jira `/items/3/description` specifies Greeting/Dialog with explicitly populated substitution examples. The four scoped API descriptions establish no preview endpoint, persona defaults, time mapping or execution policy. No invented resident identity or service endpoint follows. |
| Ownership/deferral | **Accept.** Registration 23–59 owns atomic creation and unknown-outcome protection; skill-selection 128–145 forbids configuration writes during skill saves; overview 101–123 concerns skill drafts/saves, not an implemented editor. Lifecycle 179–192 reserves PUT configuration for a separate configurator and prohibits fake/default writes. r2's candidate capability and cross-capability deltas preserve these boundaries. |

## Architecture

Create optionally embeds `UpdateSurfaceConfigurationRequest`, the same complete DTO used by configuration PUT. Cards reference `SurfaceCardRequest → SurfaceCardActionRequest → SurfaceCardActionType`. Independently checked read references: `C/SurfaceDetailResponse/properties/configuration/$ref → SurfaceConfigurationResponse`, `/properties/cards/items/$ref → SurfaceCardResponse`, `/properties/action/$ref → SurfaceCardActionResponse`, `/properties/type/$ref → SurfaceCardActionType`. Shared action enum expansion affects reads; request-only length limits do not automatically constrain responses. Description-only rules must accompany schema-derived planning.

## Candidate ownership and discovery

`find` of `openspec/changes/**/proposal.md` found 21 nonarchive proposals, none a configurator plan. Read-only search of all 85 nonarchive/non-audit active Markdown files for `MOS-959|MOS-1237|configurator|конфигуратор|placeholder|плейсхолдер|greeting` returned zero matches. Archive contents were not inspected. This supports bounded absence, not universal absence of differently worded plans.

**Accept** r2's hypothetical `openspec/changes/mos-959-surface-configurator/` proposal/design/tasks and `specs/surface-configurator/spec.md` ownership only. No active change or completed task is established. Existing registration, skill-selection and overview scenario locators are suitable cross-capability anchors; changing the lifecycle deferral requires separate activation approval.

## Safe corrections versus unresolved decisions

**Safe planning correction now:** record that saved current publication resolves exact-placeholder and missing-link documentation obstacles; record numeric/conditional constraints and create/save distinctions; retain MOS-1237 as unverified implementation/test work; preserve existing defaults, recovery, deduplication and deferral. This review edits no Jira status, checkbox, source or spec.

**Product/design decisions:** activating MOS-959; preview sample/time semantics and execution policy; stricter create integrity policy; stale-card remediation UX. **Contract clarification/verification:** escaping/nesting/casing, length counting/trim ordering, duplicate equality. Runtime deployment and error-envelope fidelity require runtime evidence, not a planning decision.

**Reject unsupported downstream interpretations (not claims made by r2):** publication means deployment/approval; unconditional nonempty fallback; automatic stale-card removal; timestamps prove save success/failure; existing skill-save recovery already implements configurator recovery; candidate paths are approved active work.

## Start Here

Open `openspec/specs/surface-lifecycle-publication/spec.md:179–192`, then SAVE in the saved API. These separate available contract detail from implementation authorization.

## Verification and residual risks

Scoped read-only JSON inspection compared the four descriptions and relevant schemas against historical bytes. SHA-256 matches metadata: API `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`; Jira `b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed`. Capture dates: 2026-10-16T11:13:29.451Z and 2026-10-16T11:23:51.742Z, not new retrievals. No input/infrastructure blocker occurred.

Only this bound report was written. No network/MCP/browser, tests, generation, nested agents, source/spec edits or unrelated completed-audit review. Attachment bodies, Confluence, comments and custom fields remain uncollected; no backend behavior was observed. No assertion about pre-existing git index state.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently verified material configurator claims against primary saved sources; precise pointers, dispositions, safe corrections and unresolved decisions recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SURFACE-CONFIG.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python scoped current/historical JSON inspection and SHA-256 verification","result":"passed","summary":"Four descriptions, constraints, appearance enums, response references and saved-source hashes verified."},
    {"command":"find proposals and read-only active Markdown search","result":"passed","summary":"21 active proposals; 85 nonarchive/non-audit Markdown files; zero scoped term matches."},
    {"command":"wc -l review target and work item","result":"passed","summary":"Confirmed 130 and 6 lines respectively."},
    {"command":"tests / generation / network / MCP / browser","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Accept r2 as bounded evidence handoff; no blocking revision.","Publication does not activate configurator or supersede deferral."],
  "residualRisks": ["Publication does not establish deployment/runtime correctness.","Attachment bodies, Confluence, comments and custom fields unavailable.","Parser/normalization edges, preview and stale-reference UX unresolved; active-plan discovery bounded."],
  "diffSummary": "Only bound independent review report written.",
  "reviewFindings": ["No blockers in reviewed claims; unsupported downstream interpretations explicitly rejected."],
  "manualNotes": "Primary sources independently inspected. No source edits or runtime checks; no claim about pre-existing staged files. Acceptance limited to evidence handoff."
}
```
