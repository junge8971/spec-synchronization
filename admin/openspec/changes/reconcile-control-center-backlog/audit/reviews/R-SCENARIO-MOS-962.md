# Code Context

## Verdict

**REVISE narrowly; no escalation blocker identified.** Seven candidates are substantively supported with the corrections below. Preserve the existing MOS-1023 gates and surface MVP exclusion. This review neither authorizes implementation nor closes tasks, activates sandbox, chooses source precedence, or attests index state.

## Files Retrieved

Repository-relative paths; `A` = `openspec/changes/reconcile-control-center-backlog/audit`. JSON pointers are authoritative within long JSON lines.

1. `A/work-items/R-SCENARIO-MOS-962.md` (1–8), `A/work-items/SCENARIO-MOS-962.md` (1–9), `A/reports/SCENARIO-MOS-962.md` (1–108), `A/reports/REQ-MOS-1023.md` (1–89), `A/reviews/RECON-MOS-1023.md` (1–78): assignment, reviewed assertions and prior corrective review.
2. `A/sources/jira-sandbox-details/r1/content.json` (47–67, `/items/2`, MOS-962), corresponding `metadata.json` (complete): selected primary issue and provenance.
3. `A/sources/api-live/r1/content.json` (1, selected operations and schemas below), corresponding `metadata.json` (complete): saved publication, not runtime verification.
4. `A/sources/wiki-241080062/r1/content.json` (1, `/bodyView`, selected headings/rows below), `A/sources/wiki-245673187/r1/content.json` (1, `/bodyView`, selected sections below), `A/sources/wiki-241097511/r2/content.json` (39, `/bodyView`), `A/sources/wiki-241082009/r2/content.json` (39, `/bodyView`); each corresponding `metadata.json` read completely.
5. `openspec/changes/mos-1023-skill-environment-tokens/.openspec.yaml` (1–2), `proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-environment-tokens/spec.md` (1–47): complete active owner change.
6. `openspec/changes/archive/2026-10-02-mos-1019-skill-checks-training/`: `.openspec.yaml`, `proposal.md`, `design.md`, `tasks.md`, `specs/skill-checks-training/spec.md` all read completely; `openspec/specs/skill-checks-training/spec.md` (1–70) and `openspec/specs/surface-lifecycle-publication/spec.md` (1–196): historical observation scope and sandbox exclusion.
7. Complete mandatory auth prerequisite set under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: `proposal.md` (1–38), `design.md` (1–171), `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138); additionally `tasks.md` (48–52).
8. Complete mandatory demo prerequisite set under `openspec/changes/archive/2026-10-09-add-local-session-demo/`: `proposal.md` (1–28), `design.md` (1–70), `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123). `docs/mpmm-auth-rollout.md` read completely, especially lines 3–33.

## Required corrections

### 1. Preserve recorded auth approval; do not reopen or export it

Replace the author's Architecture sentence “The approved real-integration release gate remains open/unchanged” with:

> The existing real-integration release gate was confirmed by the user on 09.10.2026, as recorded in archived auth tasks.md 48–52 and docs/mpmm-auth-rollout.md 3–5, 24–33. Its basis is user confirmation, not agent execution of real-environment checks; separate protocols were not supplied and archiving does not mean deployment. Preserve this approval without extending it to sandbox synchronization, token rotation, readiness, or operation-specific permission mapping.

The demo proposal/design contain historical open-gate language. Reading those alone is insufficient to describe the recorded outcome. No new auth approval, transport, grants, credential access, or deployment verification is requested by this review. Changed-deployment reconfirmation is already a documented condition, not evidence that the original approval is open.

### 2. Correct source coordinates and preserve the catalog version discrepancy

The blanket “Source content JSON is line 1” is false: Jira is formatted (MOS-962 key line 47, description line 50); both r2 wiki bodies are line 39. Use `/items/2/description` and `/bodyView` plus headings/rows.

Catalog `wiki-241097511/r2`, `/bodyView`, **Общая информация** labels the contract **v1.0**, while **3. История версий** contains **v1.1, 14.09.2026** and v1.0, 11.09.2026. Preserve both rather than report one unqualified contract version. Confluence version 6 is a separate page revision. Surface contract page revision 5 has body/history v1.0. Neither page dates nor revision numbers decide precedence.

### 3. Use the actual skill DTO reference and qualify historical absence

In the saved API, skill GET response resolves through `TsamResponseSchema_SkillResponse_.properties.data.$ref` to:

`#/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`

There is no plain `components.schemas.SkillResponse` key. Another namespaced SkillResponse belongs to dialogs and is not interchangeable. Correct the report's “Exact published contract pointers” accordingly.

The skills DTO also requires `checks`; its items are `SkillCheckResponse` with `check_type/status/blocking/message/checked_at`. GET description states these are saved checks, not a launch; POST `/api/control/api/skills/v1/skills/{skill_id}/status` describes recalculation before forward transitions. `SkillCheckType` lists anketa, phrases, exact_conflicts, semantic_conflicts, endpoint. These are positive published metadata and lifecycle semantics—not stand sync, training-run completion, synchronized production revision, or executable sandbox readiness. The archived MOS-1019 status-observation limitation remains its approved historical delivery boundary, not proof that today's inspected API has no check results. Candidate 07 can remain, with this explicit qualification.

### 4. Keep absence findings strictly bounded

The positive surface operation and module/skill DTO findings are reproducible. Path-name search alone cannot establish source-global semantic absence. Independent inspection additionally searched operation content and schema content for sandbox/sync/reissue/revocation terms, and followed the relevant response references. Semantic hits also include skill status and surface-list descriptions, not just the sandbox-named path. The relevant inspected command/DTOs do not define MOS-962 stand-sync progress/result/revision or token issuance/revocation confirmation. Phrase the result that narrowly; it is not an exhaustive backend inventory or proof of nonexistence. A generic envelope success code/message does not supply missing business semantics.

## Key Code / Seven-candidate verification

Primary aliases: J = `A/sources/jira-sandbox-details/r1/content.json`, `/items/2/description`; W = skills wiki `/bodyView`; S = surfaces wiki `/bodyView`; C = catalog contract `/bodyView`; SC = surface contract `/bodyView`. All API references below refer to saved `api-live/r1/content.json`, line 1.

| Candidate | Independent finding and disposition |
|---|---|
| SCENARIO-MOS-962-01 | **Accept bounded distinction.** J requires real synchronization with version/time/result and identifies missing stand-to-prod progress. W **Песочница (ПЕС)** ПРТ-ПЕС-5 and **K. Песочница**, T-79 explicitly require sync of stand skill composition/settings. API `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1sandbox/post` is bodyless surface lifecycle send; description says status/time and no status persistence on external-service error. It is neither absent nor an established stand-sync protocol. |
| SCENARIO-MOS-962-02 | **Accept.** J forbids permanent “Синхронизирован” before confirmation. `SurfaceStatusResponse` declares only surface_id/status/updated_at; its envelope resolves directly to that schema. C **1.3**, **1.5**, **2.9** distinguish object optimistic-locking version and skill standard-contract version. None identifies the synchronized stand revision or completion time. Do not infer polling/progress/SSE from timestamps or reuse MOS-1019's five-second observation policy as sandbox approval. |
| SCENARIO-MOS-962-03 | **Accept/no duplicate task.** J requires new token **and confirmed old revocation**. W ПОД-7, T-52 and **5.2. skill_tokens** corroborate rotation/history. Existing MOS-1023 task 1.1 already includes old revocation and unknown-outcome recovery; design 11–22 and spec **Controlled disclosure and rotation** preserve confirmation/no optimistic success/no automatic repeat after lost response. Changed secret, revoked_at field, or admin refresh alone is not confirmation. |
| SCENARIO-MOS-962-04 | **Accept/no-op.** W **5.2. skill_tokens** includes verification-environment usage; ПРТ-ПЕС-5 includes reissue. Existing MOS-1023 design 13–17, tasks 2.1–2.4, spec **Server token metadata** and **Secret-safe sandbox integration** already gate one shared skill/environment model, disclosure, lifetime/scope, cleanup and secret-free skill-ID navigation. Prior RECON suggestions are not adopted requirements. |
| SCENARIO-MOS-962-05 | **Accept with strict metadata qualification.** J explicitly says disabled modules **and skills** affect stand warning; W ПРТ-ПЕС-6/T-81 and S **2.1. surface_skills** corroborate configuration/module context. `ModuleResponse.status/disable_impact_message/updated_at`, `ModuleSummaryResponse.banner/disabled_modules`, `ModuleStatus`, `SkillStatus.disabled` and `SurfaceDetailResponse.enabled_skills` exist. `SurfaceSkillResponse` has only skill_id/parameters; disabled-module summary items have id/name. Global metadata, membership, and timestamps do not establish selected-stand effective impact or propagation freshness. |
| SCENARIO-MOS-962-06 | **Accept, with correction 1.** J requests role access agreement; W role labels are not grants. Published surface send names `TSAM.Surface:send_to_sandbox`, not stand-sync or business-token rotation permission. Archived auth **Exact permission matching / Explicit feature policy** retains explicit-* UI policy for unmapped sandbox operations, backend request authorization and no request ACL. Demo **Full demo does not implement missing APIs** preserves unavailability. Do not reopen this policy or infer new grants. |
| SCENARIO-MOS-962-07 | **Accept with correction 3.** W ПЕС-8/9 requires completed classifier additional training and isolation. S **Карточка поверхности → Общие для всех вкладок**, row 9 explicitly leaves whose configuration is replaced unresolved. SC **1.1 / 2.6** publishes sent status/time, not execution readiness. Main skill-checks spec **Status observation does not establish readiness** and surface spec **Lifecycle status and actions / No sandbox workflow in MVP** preserve no status-only readiness and no visible/hidden sandbox launch. Published checks do not lift these boundaries. |

## Provenance verification

All six freshly computed SHA-256 values match their metadata; Jira also matches the assignment digest:

- `jira-sandbox-details/r1`: `4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8`
- `api-live/r1`: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`
- `wiki-241080062/r1`: `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2`
- `wiki-245673187/r1`: `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa`
- `wiki-241097511/r2`: `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47`
- `wiki-241082009/r2`: `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b`

API info.version is 0.1.0, captured from documented A deployment on 2026-10-16, not proof of T behavior. Wiki page versions are 17/18/6/5 respectively. Jira MOS-962 is saved as Backlog, updated 2026-10-15T14:46:47.097+0800, with empty attachments and comment total 0; custom fields/attachment bodies were not collected. Capture integrity does not establish business correctness, implementation, approval or task completion.

## Architecture / Open questions

One existing MOS-1023 business-token model remains the owner; admin-session refresh is separate technical infrastructure. Approved auth/demo UI boundaries neither implement missing APIs nor prove selected-stand readiness. No new shared token task, transport or permission engine is warranted.

The author's four owner questions remain genuine: stand identity/revision/confirmation and unknown-outcome recovery; token target and authoritative old-revocation evidence; selected-stand disabled-impact/freshness and replacement scope; granular operation permission mapping. These are bounded owner gaps, not new source-approved delivery deferrals. MOS-1019's explicit readiness deferral and surface MVP's explicit sandbox exclusion are existing scope decisions, not evidence cancelling MOS-962. No actual blocker required a supervisor decision; material corrections were communicated through the supervisor channel.

## Start Here

Correct `A/reports/SCENARIO-MOS-962.md`, **Architecture / Existing ownership**, against auth `tasks.md` 48–52 and `docs/mpmm-auth-rollout.md` 3–33 first. Then fix JSON coordinates, catalog version discrepancy and skill DTO/checks qualification. No product/spec/task edits are authorized here.

## Limitations

Read-only local inspection and inert HTML parsing only. No code audit, live deployment calls, credentials, tests/build/browser/network/MCP, generation, source edits or index inspection. Large prerequisite output was continued until complete. An initial direct `SkillResponse` lookup failed and was corrected by following the envelope to the actual namespaced schema; this exposed a report precision defect, not a missing skill endpoint. Search results outside relevant business operations were not treated as sandbox evidence. No implementation compliance or exhaustive ownership inventory is claimed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently checked seven candidates against primary snapshots and complete mandatory prerequisites; delivered revise verdict, precise corrections and limitations."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-962.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local file reads, Python JSON/SHA-256 and inert HTMLParser inspection","result":"passed","summary":"Six content hashes matched; primary passages and referenced DTOs checked; complete prerequisite reads continued after truncation."},
    {"command":"Initial direct components.schemas.SkillResponse lookup","result":"failed","summary":"Key absent; recovered by following actual envelope reference to namespaced skills DTO and inspected checks."},
    {"command":"Tests/build/browser/network","result":"not-run","summary":"Prohibited by bounded assignment."}
  ],
  "validationOutput": ["Prior user auth release approval preserved without extension to sandbox.","Seven candidates retained subject to factual precision corrections; no activation or task closure."],
  "residualRisks": ["Saved publication does not establish runtime availability or backend nonexistence.","Stand sync, confirmed token revocation, warning scope/freshness and granular operation mapping require owner evidence within existing gates.","Catalog body-label/history discrepancy remains unresolved; no source precedence chosen."],
  "diffSummary": "Only authoritative bound review report written; no source/product/code/spec/task edits.",
  "reviewFindings": ["Revise incorrect open auth gate, inaccurate JSON line locators, flattened catalog contract version, and ambiguous skill DTO/readiness publication wording."],
  "manualNotes": "All mandatory auth/demo proposal/design/specs read completely before auth conclusions. No genuine blocker required escalation. No index-state attestation. Review only, not writer authorization."
}
```
