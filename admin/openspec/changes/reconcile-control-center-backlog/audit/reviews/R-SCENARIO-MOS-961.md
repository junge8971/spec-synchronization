# Code Context

## Verdict: REVISE

The seven candidate requirements and the central distinction between persisted ordinary dialogs and sandbox conversation/events/history are supported. Mandatory corrections concern prerequisite completeness, historical auth approval, and the unsupported index attestation. Preserve the original author report as historical evidence; this review does not edit it, authorize a writer, activate functionality, close tasks, or choose source/policy precedence. No execution blocker required supervisor intervention.

Paths below are repository-relative. `A` = `openspec/changes/reconcile-control-center-backlog/audit`; `S` = `A/sources`. JSON pointers and named inert HTML sections are primary-evidence locators (not rendered UI).

## Files Retrieved

- `A/work-items/R-SCENARIO-MOS-961.md` (complete, lines 1–8), `A/work-items/SCENARIO-MOS-961.md` (complete, lines 1–7), `A/reports/SCENARIO-MOS-961.md` (complete, lines 1–144).
- `S/jira-sandbox-details/r1/content.json#/items/1` only; accompanying `metadata.json` complete. MOS-961 description/status/comments and provenance, not adjacent scenarios.
- `S/wiki-241080062/r1/content.json#/bodyView`: heading outline, complete «Песочница (ПЕС)», §6.3 `skill_sandbox_checks`, «K. Песочница» T-74–81; complete metadata.
- `S/wiki-245673187/r1/content.json#/bodyView`: heading outline, §3 «Проверка в песочнице», registration «4. Проверка», card common requirements, Overview and History sections; complete metadata.
- `S/wiki-241097511/r2/content.json#/bodyView`: heading outline and complete §4 open questions only; complete metadata. No whole-catalog semantic audit.
- `S/wiki-241082009/r2/content.json#/bodyView`: heading outline, complete §§2.6–2.7 and §4; complete metadata.
- `S/api-live/r1/content.json`: info, pertinent operation/schema-name discovery, complete ordinary dialog detail GET and surface sandbox POST; `DialogCardResponse`, `MessageResponse`, `RouteResponse`, `RouteStepResponse`, `SurfaceStatusResponse`, `SurfaceStatus`; complete metadata.
- Complete main specs: `openspec/specs/skill-checks-training/spec.md` (1–70), `surface-lifecycle-publication/spec.md` (1–196), `surface-overview-connection/spec.md` (1–123), `dialog-details/spec.md` (1–82), `dialog-route/spec.md` (1–57), `dialog-answer-insights/spec.md` (1–68). Also `openspec/specs/control-center-shell/spec.md` (216–238) and scoped main/active text discovery, excluding archive/audit from active scope. Discovery is not exhaustive semantic absence proof.
- Complete `openspec/changes/mos-1023-skill-environment-tokens/{proposal.md,design.md,tasks.md}` (1–27, 1–26, 1–18) and `specs/skill-environment-tokens/spec.md` (1–47).

### Complete mandatory auth/demo prerequisites

All the following were read completely, including retrieval of truncated inspection output, before validating access-policy conclusions. Prefix `H` = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`; prefix `D` = `openspec/changes/archive/2026-10-09-add-local-session-demo`.

- `H/proposal.md` 1–38; `H/design.md` 1–171; `H/tasks.md` 1–52.
- `H/specs/control-center-api-integration/spec.md` 1–64; `H/specs/control-center-http/spec.md` 1–71; `H/specs/control-center-mock-server/spec.md` 1–27; `H/specs/control-center-permissions/spec.md` 1–89; `H/specs/control-center-shell/spec.md` 1–101; `H/specs/mpmm-session/spec.md` 1–138.
- `D/proposal.md` 1–28; `D/design.md` 1–70; `D/tasks.md` 1–26; `D/specs/control-center-mock-server/spec.md` 1–106; `D/specs/control-center-shell/spec.md` 1–55; `D/specs/local-session-demo/spec.md` 1–123.
- `docs/mpmm-auth-rollout.md` 1–58.

## Key Code / independent primary verification

No application code was inspected.

### Provenance and saved-byte integrity

Fresh local SHA-256/byte calculation matched each accompanying metadata value and the author's table:

| Content under S | Bytes | SHA-256 |
|---|---:|---|
| jira-sandbox-details/r1/content.json | 4826 | 4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8 |
| wiki-241080062/r1/content.json | 481595 | 4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2 |
| wiki-245673187/r1/content.json | 319614 | d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa |
| wiki-241097511/r2/content.json | 73058 | 710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47 |
| wiki-241082009/r2/content.json | 56040 | 13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b |
| api-live/r1/content.json | 413007 | 549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06 |

Wiki metadata versions are respectively 17/2026-10-09, 18/2026-10-09, 6/2026-10-13, 5/2026-09-08. API info.version is 0.1.0, captured 2026-10-16T11:13:29.451Z from Swagger-discovered nchat-a documentation, with no ETag/Last-Modified. Jira item retrieval is 2026-10-16T13:18:06.118Z; updated 2026-10-15T14:47:13.597+0800; status Backlog. `parent:null`, zero returned comments/total and empty attachments do not prove missing hierarchy, global discussion or unavailable backend. Membership is metadata attribution; custom fields and attachment bodies were not collected. Capture methods and earlier failed r1 attempts are recorded provenance, not independently reproduced access or explained failures. Hash agreement proves saved-byte consistency, not live freshness, deployment, or approval.

### Seven candidates

| Candidate | Independent result / exact primary basis |
|---|---|
| C01 chat/examples/send-reply | Supported: Jira `/items/1/description`; skills ПЕС-1, ПРТ-ПЕС-1, T-74. No conversation identity, send contract, or event state machine established. |
| C02 group/intent/domain/skill/confidence/ethics | Supported as candidate fields: Jira description, skills ПРТ-ПЕС-2 and §6.3. §6.3 gives intent/domain/skill strings, confidence float, ethics boolean; it does not establish a separate group or group↔intent identity, range, or API nullability. Preserve those known analytics types rather than claiming all typing is absent. |
| C03 timings/calls | Supported: ПЕС-4, ПРТ-ПЕС-3, §6.3, T-76. Four timing members are `pre_router`, `domain_classifier`, `skill_service`, `total`; calls contain `system,url,code,duration_ms`. Calls explicitly identify milliseconds; timing-member units/correlation are not established by a sandbox API. Ordinary route totals in seconds are not substitutes. |
| C04 error | Supported: ПРТ-ПЕС-4, §6.3 `error {stage,code,message}`, T-77. Processing failure versus transport failure and terminal/partial event handling remain unagreed. |
| C05 history/version | Supported: Jira explicitly demands time/author/result/version; ПЕС-6–7, ПРТ-ПЕС-7 and T-78 support history and trace navigation. §6.3 lists required id, skill_id, author_user_id (СУДИР), result, created_at and optional trace; no version. Do not substitute message author or updated_at. T-78's `GET /api/v1/skills/{id}/sandbox/history` is analytics decomposition, not a published/agreed operation. |
| C06 transport/no synthetic answers | Explicit Jira gate. No HTTP/WS/SSE choice, local three-string answer selection, runtime call, or synthetic completion is justified. Demo fixed HTTP responses do not supply missing business APIs. |
| C07 isolation/readiness | Supported: ПЕС-8–9 require completed classifier training and separate contour without user impact. Surface card common row 9 explicitly leaves replacement for all users/sender/status-only unresolved. Main skill-checks-training 63–70 forbids readiness from status alone. Preserve ambiguity, not a deployment guarantee. |

### Schema/status challenge

`S/api-live/r1/content.json#/paths/~1api~1control~1api~1dialogs~1v1~1dialogs~1{chat_id}/get` documents a single assembled ordinary-dialog card, retention/scope constraints, and unavailable-route handling. Its 200 schema is **`TsamResponseSchema_DialogCardResponse_`**, not a bare card. `DialogCardResponse` carries messages and route; `MessageResponse.author` identifies a message author, not the tester. `RouteStepResponse.detail` is nullable text; `duration_ms` is integer; neither constitutes typed sandbox intent/confidence/ethics or four-stage timings. No compatibility is established. `route.available=false` means unavailable source, not successful empty sandbox trace.

`#/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1sandbox/post` has no requestBody and its 200 schema is **`TsamResponseSchema_SurfaceStatusResponse_`**. Payload `SurfaceStatusResponse` requires surface_id/status/updated_at; status references the full enum draft/configured/review/sandbox/prod/disabled/archived. The **operation description**, not a singleton schema enum, promises sandbox transition and permits every initial status including prod/archived; failure of the external surface service prevents status persistence. It establishes neither conversation transport nor successful checking. Report line 78 should describe envelope versus payload precisely.

Surface wiki §3 permits configured/review/sandbox inputs; common row 8 excludes prod; contract §2.7 describes previous checking and `409 SANDBOX_CHECK_REQUIRED`. Main surface-lifecycle-publication 37–68 and 134–138 omit sandbox execution and forbid hidden execution on that error. These are recorded differences, not a precedence ruling. Status alone cannot prove testing (surface-overview-connection 80–94).

## Mandatory corrections

1. **R961-01 — incomplete prerequisite evidence (author lines 46–47).** The author's listed readings omit five archived auth delta specs and all three archived demo delta specs. Current individual main specs are not a substitute for the required complete archived proposal/design/specs. Record the original limitation and the complete independent verification above; do not retroactively claim the author read them.
2. **R961-02 — explicit historical gate-status precision (author line 104 / preserved-gate wording).** Add: “The existing MPMM release gate was confirmed by the user on 09.10.2026; archived auth task 6.3 is checked, and tasks line 52 plus docs/mpmm-auth-rollout.md 3–5, 24–33 identify user approval as the basis. The agent did not independently execute real-environment checks, and separate protocols were not supplied. This review neither reopens that approval because tests were not run nor extends it to sandbox transport, credentials, permissions or deployment.” Demo proposal line 28/design line 70/tasks 4.2 retain earlier open-gate wording; acknowledge this historical wording without silently replacing the explicit recorded approval or deciding general source precedence.
3. **R961-03 — reject index attestation (author lines 139, 142).** `noStagedFiles:true` is unsupported: no index inspection was performed. “I did not stage” does not establish “there are no staged files.” Omit the field from downstream attestations and state index uninspected. Preserve the original report unchanged as historical evidence. This review makes no index/clean-tree assertion.
4. **R961-04 — schema precision (author lines 68–78).** Explicitly distinguish 200 response envelopes from payload schemas; distinguish full SurfaceStatus enum from operation transition prose. Retain known §6.3 analytics types/requiredness while keeping API-specific optionality and compatibility unknown. This refines rather than reverses the author's central conclusion.

## Architecture / boundaries

Jira supplies the requested FE scenario and transport/event agreement gate. Skills analytics supplies candidate trace/history data, not a runnable protocol. Surface sandbox API changes lifecycle state; ordinary dialog API supplies a persisted snapshot. Neither bridge to sandbox conversations is proven. Main specs preserve unavailable/readiness/no-synthetic-history boundaries; no dedicated MOS-961 main/active artifact was identified by bounded discovery, which is not global backend absence. Named chat/test-mode deferral must not be presented as a newly discovered dedicated spec: the directly verified prohibitions here are readiness/status, surface workflow, and absent-API behavior.

Complete auth prerequisites confirm configuration-selected real/mock modes, credential destination validation separate from mode, permissions for UI only and backend request authorization. Archived permissions 23–36/60 reserve unmapped sandbox UI for explicit `*` without activating missing functionality. `TSAM.Dialog:view`, `TSAM.Surface:send_to_sandbox`, role labels and wildcard must not be repurposed as new granular sandbox grants. Existing approval introduces no stream-auth or token model. MOS-1023 proposal 25–26/design 13–17/tasks 1–5 retain token API/security boundaries and exclude the dialog engine; its metadata cannot prove completed sandbox tests.

## Start Here

Read `docs/mpmm-auth-rollout.md` 3–5 and archived auth `tasks.md` 44–52 first to correct gate-status ambiguity, then Jira MOS-961 description and skills §6.3 to retain the unresolved version/transport contract.

Remaining owner questions are limited to sandbox conversation/event/history agreement, version identity, group↔intent semantics and timing/correlation, and isolation/configuration recipient semantics. They are not blockers to this documentary review and were not answered by inventing transport, grants or precedence. No new supervisor decision was necessary.

## Validation / limitations

Read-only local JSON parsing, inert HTML outline/section extraction, metadata/hash comparison and specification reading only. No network/MCP/browser, tests/build/generation, credentials extraction, application-code audit, git/index inspection or mutation, nested agents, task closure or activation. Only this authoritative report was intentionally written. Captured docs may diverge from deployment; attachment bodies/uncollected fields remain unavailable; bounded name discovery cannot prove global API absence. No runtime or implementation acceptance is claimed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent primary/spec review verifies C01–C07 and records mandatory corrections R961-01–04 with precise evidence and preserved historical auth approval."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-961.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python JSON/hash/byte and inert HTML-section inspection","result":"passed","summary":"All six saved content hashes and byte counts matched metadata; bounded candidate/schema evidence read."},
    {"command":"Local find/grep/nl and complete archived prerequisite/spec reading","result":"passed","summary":"Complete auth/demo proposal/design/specs/tasks and rollout documentation read; truncated output recovered."},
    {"command":"Tests/build/browser/network","result":"not-run","summary":"Prohibited by bounded review instructions."}
  ],
  "validationOutput": ["Verdict REVISE; seven candidate requirements supported without sandbox API compatibility or readiness attestation."],
  "residualRisks": ["Sandbox transport/events/history version, semantic mapping and isolation remain unagreed.","Saved evidence is not live deployment verification; uncollected fields and attachments limit conclusions.","Index uninspected; original noStagedFiles assertion rejected."],
  "diffSummary": "Only authoritative independent review report written; historical author report and product/source files unchanged by this reviewer.",
  "reviewFindings": ["R961-01 prerequisite coverage incomplete in author report.","R961-02 preserve explicit prior user auth release approval without sandbox extension.","R961-03 omit unsupported index attestation.","R961-04 distinguish response envelopes, payload schemas and operation status semantics."],
  "manualNotes": "Manual documentary review only. No execution blocker; no policy precedence, task closure, activation or writer authorization. Index-attestation field intentionally omitted."
}
```
