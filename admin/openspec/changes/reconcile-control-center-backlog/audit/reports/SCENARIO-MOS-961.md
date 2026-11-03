# Code Context

## Scope and result

SCENARIO-MOS-961 — fresh local primary-evidence/spec analysis only. **Candidate requirements are supported; a sandbox conversation/event/history integration contract is not established by the inspected evidence.** Preserve transport/event-format agreement, chat/test-mode deferrals and all existing API/security gates. No activation, implementation assessment, task closure, source precedence decision or index attestation is made.

Paths below are repository-relative. `A` means `openspec/changes/reconcile-control-center-backlog/audit`; `S` means `A/sources`. JSON pointers and inert HTML heading/requirement locators identify primary evidence more precisely than the long serialized JSON lines. No embedded HTML was executed.

## Files Retrieved

### Primary evidence and provenance

Read `S/jira-sandbox-details/r1/metadata.json` and selected `content.json#/items/1` (MOS-961). Jira status is Backlog; updated `2026-10-15T14:47:13.597+0800`, item retrieval `2026-10-16T13:18:06.118Z`. Description explicitly requires chat input/examples/send/reply states; group/intent/domain/skill/confidence/ethics/stage timings; history time/author/result/version; agreed transport and event format; no predetermined HTTP/WebSocket/SSE and no local three-string HTML response simulation. Selected comments total=0, attachments=[], parent=null. Membership attribution is metadata, not proof from this null parent field. Custom fields and attachment bodies were not collected. One subsequent line-range read spilled into the adjacent MOS-962 item; that adjacent description is not used as evidence or analyzed here.

All six content files below were independently SHA-256 and byte-count checked against their accompanying metadata; all matched. This verifies saved bytes, not live freshness, deployment or approval.

| Saved content | Bytes | Version | SHA-256 |
|---|---:|---|---|
| `S/jira-sandbox-details/r1/content.json` | 4826 | saved r1 | `4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8` |
| `S/wiki-241080062/r1/content.json` | 481595 | Confluence 17, 2026-10-09 | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` |
| `S/wiki-245673187/r1/content.json` | 319614 | Confluence 18, 2026-10-09 | `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa` |
| `S/wiki-241097511/r2/content.json` | 73058 | Confluence 6, 2026-10-13 | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` |
| `S/wiki-241082009/r2/content.json` | 56040 | Confluence 5, 2026-09-08 | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` |
| `S/api-live/r1/content.json` | 413007 | OpenAPI info.version 0.1.0 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |

Metadata attributes the wiki captures to parent same-origin Confluence reads on 2026-10-16; skills/surfaces attachment metadata only, no attachment bodies. Successful r2 catalog/surface-contract captures retain earlier unsuccessful r1 provenance rather than explaining those failures. API metadata records capture from Swagger-discovered `https://nchat-a-tech.mos.ru/api/control/openapi.json` at `2026-10-16T11:13:29.451Z`, no ETag/Last-Modified, no business request. These provenance statements were read locally, not independently reproduced online. No credential values were sought.

After heading-outline inspection, relevant primary sections read:

- Skills `#/bodyView`: **Песочница (ПЕС)**, ПЕС-1–9 and ПРТ-ПЕС-1–7; **6.3. skill_sandbox_checks** including trace structure; **K. Песочница**, T-74–81. Sync/failure simulation/surface-context references retained only as dependencies.
- Surfaces `#/bodyView`: **3. Проверка в песочнице**; sandbox-related scenario excerpts and **Карточка поверхности → Общие для всех вкладок**, rows 8–9; sandbox checklist/history references. Also inspected the outlined **Вкладка: "4. Проверка"** to distinguish registration checks from sandbox tests. No separate chat/trace/history protocol emerged from these bounded sections.
- Catalog contract `#/bodyView`: method heading outline (domain/skill CRUD), **4. Открытые вопросы** and pertinent-link discovery only. Not a semantic audit of the entire catalog. No sandbox conversation conclusion is drawn from unrelated catalog branches.
- Surface contract `#/bodyView`: complete **2.6 Отправить конфигурацию в песочницу** and **2.7 Опубликовать поверхность** with subordinate request/response/error sections; **4. Открытые вопросы**. These concern configuration lifecycle, not chat transport.
- API: operation/path and schema-name discovery for chat/dialog/test/trace/history/sandbox/conversation/stream, then the detail/surface-sandbox branches and schemas listed below. A/B testing name matches were excluded as unrelated. This is not an exhaustive semantic proof that no API anywhere supports sandbox conversations.

### Local OpenSpec discovery and readings

Bounded LOCAL-001-style discovery used actual files under `openspec/specs` and non-archive `openspec/changes` excluding audit as product scope; searched sandbox/chat/test-mode/history-related terms, then read relevant artifacts. `A/work-items/LOCAL-001.md` lines 1–8 was read for its inventory-only boundary, not used as semantic proof. No fresh global inventory count or index acceptance is asserted.

1. `openspec/specs/skill-checks-training/spec.md` lines 1–70 — complete; current status observation is not sandbox readiness.
2. `openspec/specs/surface-lifecycle-publication/spec.md` lines 1–196 — complete; especially 37–68, 134–163, 179–196, no sandbox workflow or synthetic history in MVP.
3. `openspec/specs/surface-overview-connection/spec.md` lines 1–123 — complete; 80–99 excludes sandbox checklist and status-as-check-proof.
4. `openspec/specs/dialog-details/spec.md` lines 1–82; `openspec/specs/dialog-route/spec.md` lines 1–57; `openspec/specs/dialog-answer-insights/spec.md` lines 1–68 — complete; persisted dialog snapshot, route and answer semantics, not a sandbox sender or event stream.
5. `openspec/specs/control-center-shell/spec.md` lines 47–78, 216–238 (targeted discovery excerpts) — permission/route availability cannot turn missing functionality into working functionality.
6. `openspec/changes/mos-1023-skill-environment-tokens/proposal.md` lines 1–27; `design.md` lines 1–26; `tasks.md` lines 1–18; `specs/skill-environment-tokens/spec.md` lines 1–47 — complete dependency artifacts; token/security gate remains, dialog engine explicitly outside that change. No secret-operation design is proposed here.
7. Auth prerequisites: `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md` lines 1–38, `design.md` lines 1–171, `specs/mpmm-session/spec.md` lines 1–138; current `openspec/specs/control-center-permissions/spec.md` lines 1–91. Read to preserve approved boundaries, not to make new auth choices.
8. Demo prerequisites: `openspec/changes/archive/2026-10-09-add-local-session-demo/proposal.md` lines 1–28, `design.md` lines 1–70; current `openspec/specs/local-session-demo/spec.md` lines 1–125. Fixed HTTP response selection does not authorize missing sandbox APIs or local answer simulation.
9. `openspec/config.yaml` lines 1–38 — existing session, mode, security and no-browser-test constraints.

No dedicated MOS-961 active change or main sandbox-chat spec was identified in that discovery. This is a bounded finding, not proof of runtime absence. Neighboring active token work does not own chat implementation. Other unrelated active changes were not semantically audited.

## Key Code / Contract Evidence

No application code was inspected; the critical evidence is contract structure.

**K961-01 — analytics data model is a candidate, not an endpoint contract.** Skills §6.3 describes system-written `skill_sandbox_checks`:

```text
id, skill_id, author_user_id, result, trace?, created_at
trace: intent, domain, skill, confidence, ethics,
       timings {pre_router, domain_classifier, skill_service, total},
       calls [{system, url, code, duration_ms}],
       error {stage, code, message}
```

No version field is listed there. Jira MOS-961 requires a version in history. T-78 proposes `GET /api/v1/skills/{id}/sandbox/history`; this is an analytics decomposition reference, not evidence of a published/accepted request/response contract. It must not be implemented merely by copying this path.

**K961-02 — ordinary dialog detail is a persisted snapshot.** In `S/api-live/r1/content.json`:

- `#/paths/~1api~1control~1api~1dialogs~1v1~1dialogs~1{chat_id}/get`, operationId `get_dialog_api_control_api_dialogs_v1_dialogs__chat_id__get`: returns one card assembled from ЕСК and attachment information; personal-data read with audit. Description includes retention and scope limits and route-unavailable behavior. No send-message or sandbox-event format is specified by this operation.
- `#/components/schemas/DialogCardResponse`: chat/session IDs, times, user/operators/participants, messages, route and other dialog facts; no sandbox check version/result/author tuple.
- `#/components/schemas/MessageResponse`: author, occurred_at, text, attachments, rating, basis. Author of a persisted message is not established as sandbox test author.
- `#/components/schemas/RouteResponse`: available, steps, traced_sec, untraced_sec, operator_actions.
- `#/components/schemas/RouteStepResponse`: occurred_at, kind, component, action, detail, duration_ms, failed. No typed sandbox intent/domain/confidence/ethics or four-stage timing tuple is established by this schema.

Similar words such as “history”, “route”, “author” and “duration” do not establish compatible semantics or identifiers. A textual route detail must not be parsed into invented sandbox classification fields. `route.available=false` is not a successful empty sandbox trace. Compatibility remains **unknown**.

**K961-03 — surface sandbox POST is lifecycle, not conversation.** `#/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1sandbox/post`, operationId `send_surface_to_sandbox_api_control_api_surfaces_v1_surfaces__surface_id__sandbox_post`, returns `SurfaceStatusResponse` (`surface_id`, `status`, `updated_at`). The inspected operation documents a transition forwarded to an external surface service, creation-style validation and no source-status check. It supplies neither test messages nor trace/history/version semantics. HTTP for this lifecycle operation does **not** settle HTTP versus WebSocket versus SSE for MOS-961.

## Architecture / Coverage and Gaps

“Covered” below means source/spec evidence exists, never implementation or deployed success.

| Stable ID | Candidate requirement and exact basis | Covered versus missing; bounded owner |
|---|---|---|
| MOS961-C01 | Chat input, examples, send/reply states: Jira `/items/1/description`; skills ПЕС-1, ПРТ-ПЕС-1, T-74 | UI intent covered. Conversation identity, sending/receiving contract and state/event semantics not established. MOS-961 FE scenario owner with backend/ЕСК contract owner; MOS-960 supplies context only. |
| MOS961-C02 | Group/intent, domain, skill, confidence, ethics: Jira description; ПЕС-2–3, ПРТ-ПЕС-2, §6.3, T-75 | Candidate fields covered. Wiki has intent but no distinct group field; group↔intent meaning, identifiers, optionality and units/ranges are not reconciled. Do not substitute ordinary dialog participants or answer basis. MOS-961 + classifier/trace contract owner. |
| MOS961-C03 | Stage timings and external calls: ПЕС-4, ПРТ-ПЕС-3, §6.3, T-76; Jira stage timing requirement | Four named stages and calls fields covered by analytics. Units for each timings member and per-reply correlation/event ordering remain unestablished by a sandbox API; calls explicitly use duration_ms. Do not reuse traced_sec as total or sum ordinary route steps. MOS-961 + trace contract owner. |
| MOS961-C04 | Processing error with stage/code: ПРТ-ПЕС-4, §6.3 trace.error, T-77 | Candidate error block covered. Transport error versus processing error, terminal/partial event semantics and safe diagnostics need contract agreement; no invented retries or simulated successful recovery. MOS-961 + backend owner. |
| MOS961-C05 | History time/author/result/version and opening trace: Jira description; ПЕС-6–7, ПРТ-ПЕС-7, §6.3, T-78 | Time/author/result/trace reference supported conceptually; version absent from §6.3. Which version (skill, classifier, configuration or synchronization), persistence/list/detail protocol and relation to each reply remain unknown. MOS-961 + persistence/product owner; last-check card projection is a dependency, not permission to rewrite that card. |
| MOS961-C06 | Agreed transport/event format; no fixed-three-answer simulation: Jira description | Explicit gate, not missing design to be supplied by this audit. No selection of HTTP/WebSocket/SSE, runtime call, local synthetic conversation or demo completion. MOS-961 product/API owners. |
| MOS961-C07 | Separate test contour and trained-classifier prerequisite: ПЕС-8–9; main skill-checks-training 63–70 | Preserve non-production intent and no-readiness-from-status rule. Wiki surface context leaves who receives replaced configuration unresolved. Isolation/readiness cannot be certified by a status transition. Context/readiness owners (MOS-960/MOS-1019), not a new chat gate implementation. |

### Conflicts and ambiguities retained

- **MOS961-A01 — version gap:** explicit Jira history version versus no version field in skills §6.3. Missing source detail, not permission to invent a version or map `updated_at` to one.
- **MOS961-A02 — isolation uncertainty:** skills ПЕС-9 says a separate contour does not affect users; surfaces card common rows 8–9 explicitly ask whether sending replaces configuration for everyone, the sender, or only changes status. Do not turn either passage into a deployment guarantee.
- **MOS961-A03 — status transitions differ:** surfaces user-path §3 gives configured/review/sandbox inputs and UI common row 8 excludes prod; inspected live surface sandbox description allows any status including prod/archived. Current main spec prohibits launching the sandbox entirely. This audit records different source/product boundaries without choosing precedence or broadening UI actions.
- **MOS961-A04 — publication prerequisite differs:** wiki surface contract §2.7 requires prior sandbox checking and describes `409 SANDBOX_CHECK_REQUIRED`; current main surface specs deliberately omit sandbox workflow/checklist and forbid hidden execution even on that error. No gate removal or new publication precondition is proposed.
- **MOS961-A05 — permissions are not portable:** inspected live ordinary-dialog GET describes `TSAM.Dialog:view`; current approved UI policy keeps unmapped dialogs/sandbox explicit-wildcard-only pending agreement. This is not authority to borrow Dialog:view, Surface:send_to_sandbox, prototype role names, or wildcard access to activate sandbox chat. Permissions remain UI policy; backend authorizes requests. New mapping and any transport-specific credential behavior require separate agreement.

### Preserved constraints

Existing auth/demo prerequisites remain intact: mode is selected by launch configuration, credential destination validation is separate, real integration/release verification is not proven by this audit or mocks, and fixed HTTP demo responses do not implement missing business APIs. No credential extraction, role model, client request ACL, stream-auth mechanism, token revocation semantics or new storage policy is introduced.

MOS-960 context and MOS-962 synchronization/token operations are dependency boundaries only. MOS-1023's complete active artifacts retain their own API/security gate and explicit exclusion of the dialog engine. No claim is made that synchronization/token metadata proves a completed test, or that a frontend rollback restores a revoked token.

## Start Here

Start with `S/jira-sandbox-details/r1/content.json#/items/1/description`, then skills **Песочница (ПЕС)** and **§6.3**, alongside `openspec/specs/skill-checks-training/spec.md` lines 63–70. Together they explain the requested behavior and why status/history lookalikes cannot activate it.

### Narrow correction / no-op candidates (not applied)

1. **MOS961-N01:** Any reconciliation claim that no trace/history API exists at all should be narrowed: ordinary persisted dialog detail/route is published in the saved API, but sandbox conversation/test-history compatibility is unproven. This is a conditional wording correction; no existing report/index was audited for that wording.
2. **MOS961-N02:** Record the explicit MOS-961 version requirement and §6.3 omission as an unresolved mapping, not “history covered” merely because time/author/result appear.
3. **MOS961-N03:** Keep T-78's proposed history path marked analytics-only; keep surface sandbox POST marked lifecycle-only. Neither closes MOS-961's transport/event gate.
4. **MOS961-N04:** No product/spec/code edit is justified by this bounded analysis alone. Preserve chat/test-mode deferral, current main-spec prohibitions and existing unchecked tasks. A separately approved contract/ownership decision is needed before implementation; no new product artifacts were created.

## Validation and residual risks

Local parsing, heading discovery, targeted source/spec reading and hash/byte assertions completed. No network/MCP/browser, tests, build, generation, runtime call, source/code/product edit, git mutation or nested agent was performed. Only this bound report was written. No staging-state inspection or clean-tree attestation was performed.

Residual risks: transport/events and sandbox history/version semantics remain unagreed; API discovery is name/path scoped, not proof of global absence; captured documentation may differ from deployment; attachment bodies and uncollected Jira fields were unavailable; ordinary-dialog compatibility and isolation remain unverified. Relevant current main specs and the active token dependency were read, but unrelated specs/active changes were not audited. Independent review remains required.

```acceptance-report
{
  "criteriaSatisfied": [
    {"id":"criterion-1","status":"satisfied","evidence":"Bounded primary/spec report identifies MOS961-C01–C07, ambiguities A01–A05 and no-op/correction candidates N01–N04 with exact source pointers and preserved gates."}
  ],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-961.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python JSON/HTML-outline and pertinent API-branch inspection","result":"passed","summary":"Read inert saved evidence; no runtime or network operation."},
    {"command":"Local SHA-256 and byte-count assertions against six metadata files","result":"passed","summary":"All six designated content hashes and sizes matched."},
    {"command":"Tests/build/browser checks","result":"not-run","summary":"Explicitly prohibited; report-only evidence analysis."}
  ],
  "validationOutput": ["Six saved content files matched metadata SHA-256 and byte counts.","No sandbox conversation compatibility or deployment readiness attested."],
  "residualRisks": ["Unagreed sandbox transport/events/history-version mapping.","Bounded discovery cannot prove global API absence or runtime behavior.","Source conflicts and independent review remain open."],
  "noStagedFiles": true,
  "diffSummary": "Sole bound report written; no source/product edits or staging operations performed; pre-existing staging state not inspected.",
  "reviewFindings": ["No execution blocker; unresolved contract/product issues are retained, not resolved by this audit."],
  "manualNotes": "Manual primary-source/spec analysis only. One line-range read exposed adjacent MOS-962 source text without using it as evidence; no duplicated scenario analysis. No index acceptance, activation or task closure. noStagedFiles records no staging by this agent, not a repository clean-state assertion."
}
```
