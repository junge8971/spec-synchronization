# Code Context

## Verdict: revise (bounded report corrections)

The twelve candidates and the five-operation inventory are materially supported. Preserve the draft/status gate. Two report corrections are required: explicitly limit the schema-default inference to schema expressiveness, and remove the unsupported index attestation. No execution blocker arose; unresolved product questions do not prevent this evidence review. Original report preserved.

Paths below are repository-relative. `A` = `openspec/changes/reconcile-control-center-backlog/audit`; `J` = `A/sources/jira-operations-details/r1/content.json`; `W` = `A/sources/wiki-241088180/r1/content.json`; `O` = `A/sources/api-live/r1/content.json`. JSON pointers identify exact source objects (O is one minified line).

## Files Retrieved

- `A/work-items/R-SCENARIO-MOS-920.md` (1–6), `A/work-items/SCENARIO-MOS-920.md` (1–8), `A/reports/SCENARIO-MOS-920.md` (1–142): assignment and reviewed claims.
- J: root provenance and only `/items/0` and `/items/2`; corresponding `metadata.json` fully. W (1–64): `/version`, `/bodyView`, `/attachments` and provenance; corresponding metadata fully. HTML parsed solely as inert text.
- O (line 1): `/info`, all five assistant-modules path objects and complete recursively referenced schema closure; no other business operations analyzed.
- `openspec/specs/control-center-mock-server/spec.md` (138–219), `openspec/specs/control-center-shell/spec.md` (179–243), `openspec/specs/control-center-permissions/spec.md` (1–91): existing normative mock, shell and UI-access coverage.
- Required prerequisites read before mock/access comparison, under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: `proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52), `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138).
- Required prerequisites under `openspec/changes/archive/2026-10-09-add-local-session-demo/`: `proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26), `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123).
- Path discovery enumerated proposals; scoped text discovery examined 81 Markdown files under direct active change directories excluding archive and reconciliation. No implementation files inspected.

## Corrections and challenges

### R1 — distinguish omitted schema validation from business permission

`A/reports/SCENARIO-MOS-920.md:5,98–99` should explicitly say: **the saved schema does not encode mandatory nonempty message or unconditional true confirmation; it does not prove that backend business validation permits omission, empty text or false confirmation.** Defaults are annotations, not evidence of server execution or successful mutation.

Exact evidence: O `#/components/schemas/DisableModuleRequest` requires only `expected_version` (integer minimum 1), declares `confirm_impact` boolean/default false and `user_message` string/default empty, without minLength. J `/items/0/description`, `/items/2/description`, and W `/bodyView`, business rules and §2.4, require message/confirmation (nonempty explicitly in MOS-717 and wiki).

There IS a normative local-mock distinction, independently of that schema omission: `openspec/specs/control-center-mock-server/spec.md:159–176` expressly stores empty default text, permits fallback text, and requires true confirmation only with nonempty impact text; line 161 uses 409 and allows repeated target-state mutations with current version. Wiki §2.6 describes 422 confirmation/message errors and 409 invalid transition. Preserve this as local mock convention versus intended business contract, not proof that production is weaker or permission to rewrite either source. Whitespace and maximum-length rules remain unspecified.

### R2 — reject unsupported index assertion

`A/reports/SCENARIO-MOS-920.md:137` states `noStagedFiles: true`, while its manual note says the index was not inspected. Delete that assertion in any corrected downstream artifact. Not staging files does not prove an empty index. This review makes no index-state assertion and performs no git mutation.

### R3 — bound no-owner claims, not universal absence

Report lines 102 and 107 are acceptable only with their discovery qualifier. Fresh scoped search of the 81 active Markdown artifacts for `MOS-920`, `MOS-717`, `assistant-modules`, and Russian global-module wording found no matches. This supports **no matching dedicated active owner discovered in that scope**, not no implementation, no historical owner, or a mandate to create a new change. Historical module-contract proposal paths exist in archive; their contents were not audited here. Existing mock/shell/permissions coverage is positive ownership evidence. No code audit was authorized.

## Key Code / contract verification

### Provenance and distinct version axes

Read-only Python recomputation matched supplied assignment hashes and local metadata:

| Source | Bytes | SHA-256 |
| --- | ---: | --- |
| J | 9933 | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| W | 36471 | `e1d5f5320e05d1e65354f2523341cab788adfacac8ac5acf6aaabf31003c18fc` |
| O | 413007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |

O hash is a local fingerprint only; its metadata was not independently attested. J retrieval `2026-10-16T13:02:57.872Z`; W retrieval `2026-10-16T13:03:14.658Z`. Metadata's verified-origin collection statement is recorded provenance, not a new external-origin verification.

J `/items/0` is MOS-717 CLOSED, updated `2026-10-15T15:13:58.701+0800`; two complete recorded comments: id 1131251 links wiki page 241088180, id 1131293 says «Неактуально». The latter does not identify what it retires. J `/items/2` is MOS-920 Backlog, updated `2026-10-15T14:46:59.601+0800`, zero recorded comments; description explicitly retains contract draft/status-confirmation before integration acceptance. Neither closure nor comment establishes cancellation or approval of MOS-920.

W `/version/number` = 4, `/version/when` = `2026-09-25T19:33:43.672+08:00`; body contract v1.1, URL `/assistant-modules/v1`, and O `/info/version` = 0.1.0 are separate axes, not precedence. W attachment listing is 200, results empty, size 0; metadata agrees. No explicit module approval resolving Jira's gate was found.

### Five operations, not API absence

Let B = `/api/control/api/assistant-modules/v1/modules`. O `#/paths` and W `/bodyView` §§2.1–2.5 agree:

| Operation | 200 data schema | Other declared responses |
| --- | --- | --- |
| GET B | ModuleListResponse | 422 HTTPValidationError |
| GET B/summary | ModuleSummaryResponse | none |
| GET B/preview | ModulePreviewResponse | none |
| POST B/{module_id}/disable | ModuleResponse | 422 HTTPValidationError |
| POST B/{module_id}/enable | ModuleResponse | 422 HTTPValidationError |

Each 200 uses the corresponding `TsamResponseSchema_*` wrapper. No extra method appeared under this saved module path family; this is not universal API absence. Wiki §1 assigns history to audit Query API without specifying an endpoint here.

- O list `parameters`: nullable string query/status; array sort referencing `ModuleListSort`, no explicit style/explode override; limit 1–100/default20, offset minimum0/default0. Wiki §2.1 specifies comma-separated status/sort, default name,id and backend-added stable id. Standard query-array default serialization is form/explode=true (repeated sort keys); actual backend comma/repeated support and stable ordering remain unverified. Main mock spec 140–150 explicitly uses repeated sort and exact single status matching. Do not classify all these as missing API.
- O `ModuleResponse`, mutation path parameters: UUID, not UUIDv7. Wiki §§1.2,2.4–2.5 says UUIDv7. O `ModuleActorResponse.id` is plain string, versus wiki UUID. `ModuleResponse.by` is optional/nullable; impact and user text are required nullable fields. Preserve these distinctions without synthesizing an actor.
- O wrappers require code/data/message, not errors; `ResponseCode` is string, not SUCCESS enum. Wiki general envelope and §2.6 describe business errors 400/401/403/404/409/422. Those business codes/envelopes are not declared by these operations; the declared 422 shape is HTTPValidationError. Undeclared errors are not proven impossible backend responses.
- Summary and preview schema closure matches the report's totals, healthy/degraded state, success/warning banner and fallback-card fields. Examples and coherent mock derivation are not deployed calculation evidence.
- Saved operation security is formal OR (`[{AdminToken:[]},{AccessToken:[]}]`). Auth design 145–149 and auth mock delta 5–7 explicitly retain the approved AND correction. No transport/security weakening or automatic source-precedence decision follows.

### All twelve candidates checked

| Candidate | Review result and primary anchor |
| --- | --- |
| C01 summary | Supported: J items2 description; W §2.2; O GET summary. Mock 157–191 is local coverage only. |
| C02 registry/search/filter/sort/page | Supported: J items0 description; W §§1,2.1; O GET B. Retain serialization/default questions above. |
| C03 state/eligibility/message/actor/time | Supported: J items0 description; W §§1.1–1.2; O ModuleResponse. Preserve optional actor and formats. |
| C04 user-facing preview | Supported: J items2 description; W §2.3; O GET preview. No new message-authoring endpoint implied. |
| C05 global disable | Supported intent: J items0 description; W business rule 1. Mock coherence does not prove propagation to real surfaces. |
| C06 disable_allowed | Supported: both selected Jira descriptions; W business rule 2; O required boolean. No core/classifier name-based allowlist. |
| C07 nonempty user_message | Supported intent: J items0, W business rule 3/§2.4; J items2 requires field. Apply R1; mock distinction is explicit. |
| C08 confirm_impact=true | Supported: J items2; J items0 consequences; W business rule 3/§§1.2,2.4. Apply R1; mock conditional requirement differs. |
| C09 expected_version / enable input | Supported: W business rules 4–5/§§2.4–2.5; O both request schemas. Enable is not an empty-body call; no invented idempotency header. |
| C10 metadata/failures | Supported: J items0; W business rule 6/§2.6; mock 161,178–186. Error and repeat-transition semantics require clarification, not inferred production behavior. |
| C11 draft gate | Supported: J items2 description and unresolved items0 comment. Remains separate from auth release confirmation. Apply R3 to owner statement. |
| C12 common rights ownership | Supported: J items2; W §2.7; main permissions 9–37,60–91. Role prose is evidence, not authority to invent UI grants or backend ACL. |

## Architecture / approval boundary

Published wire definitions, intended MOS-920 UX, approved mock/shell/access scope, and runtime acceptance are separate. Main mock spec owns local behavior; shell 179–218 owns `/ops` modules entrypoint and honest unfinished content; permissions owns exact `TSAM.Module:view/enable/disable`, resource grant or explicit `*`, with UI-only enforcement and backend-owned authorization/scopes. Credential-free business mocks do not implement role enforcement.

Auth `tasks.md:48–52` records the user's 09.10.2026 confirmation of 6.3 and archiving, expressly not agent real-backend testing. Preserve that historical release decision despite older demo proposal/design open-gate wording. It is neither fresh runtime verification nor module-specific contract approval. No tasks are closed, gate lifted, module activated, source reconciled, or implementation plan authorized here.

## Start Here

Review `openspec/specs/control-center-mock-server/spec.md:159–176` beside J `/items/2/description`, W business rules/§2.4 and O DisableModuleRequest. Correct the report's inference language and index assertion, leaving source/product artifacts unchanged.

Residual questions: what «Неактуально» retires; who confirms module contract status; actual backend message/confirmation/error/transition/serialization rules; evidence of global effects and accessible-object filtering. These need owner evidence before integration acceptance, not guesses in this review. No actual blocker required supervisor decision.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Fresh local primary comparison checked twelve candidates, five operations, hashes/version axes, normative mock differences and approval boundaries; revise verdict identifies exact report corrections."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-920.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python hashlib/JSON/HTMLParser evidence inspection","result":"passed","summary":"Jira/wiki hashes match; five module paths and schema closure inspected; HTML inert."},
    {"command":"Scoped path enumeration and active Markdown matching","result":"passed","summary":"81 bounded active Markdown files searched; no selected module-owner terms matched."},
    {"command":"Tests/build/network/MCP/browser/code audit","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Twelve candidates supported with explicit limitations.","Required revisions: schema omission is not backend permission; remove uninspected-index assertion."],
  "residualRisks": ["Module draft approval and Неактуально scope unresolved.","Backend validation, serialization, global effects and runtime implementation unverified.","Owner discovery is bounded; no universal absence or index-state attestation."],
  "diffSummary": "Only the authorized independent review report written; original report and product/source artifacts preserved.",
  "reviewFindings": ["revise: report line 5 and C07/C08 need explicit schema-versus-business validation distinction.","revise: report line 137 asserts uninspected index state.","No execution blocker; preserve module status gate and historical auth confirmation."],
  "manualNotes": "Required auth/demo artifacts read before access/mock comparison. No automatic precedence, task closure, activation or fresh runtime approval claimed. No index inspection or staging performed."
}
```
