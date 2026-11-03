# Code Context

## Result and boundary

Fresh local primary-evidence analysis for SCENARIO-MOS-920. **Keep MOS-920's draft/status-confirmation gate; no activation, task closure, source-precedence decision or new plan.** Five module operations are published in the saved OpenAPI, but their presence is not approval, deployed behavior or frontend completion. The principal reconciliation issue is that Jira/wiki require nonempty `user_message` and `confirm_impact=true`, whereas the saved OpenAPI permits omission/defaults and the main mock specification expressly describes weaker local conventions.

No product code was inspected. No network, MCP, browser, tests, build, generation, archive/sync or git mutation was performed. HTML was read only as inert source text. No index acceptance/count assertions are adopted. Only this report is an intended repository write.

## Files Retrieved

Paths below are relative to repository root. `A` means `openspec/changes/reconcile-control-center-backlog/audit`.

- `A/work-items/SCENARIO-MOS-920.md` (entire work item) and `A/work-items/LOCAL-001.md` (entire discovery instructions): bounded authority; LOCAL-001's historical inventory assertions were not re-attested.
- `A/sources/jira-operations-details/r1/content.json` (root provenance fields; **only `/items/0` MOS-717 and `/items/2` MOS-920**, keys at lines 13 and 62), and `metadata.json` (entire file): Jira descriptions/status/comments. Other issues' content was not analyzed.
- `A/sources/wiki-241088180/r1/content.json` (lines 1–64; `/bodyView` at line 39) and `metadata.json` (entire file): contract body, page version and attachment listing.
- `A/sources/api-live/r1/content.json` (line 1, minified): only module operations and their transitive referenced schemas; `info` inspected for document version. JSON pointers below identify exact objects within that line. No API metadata provenance attestation is made beyond this saved artifact.
- `openspec/specs/control-center-mock-server/spec.md` (lines 1–445, fully read): especially 138–191 module list/actions/derived views, 193–219 merged-contract ownership; not frontend completion evidence.
- `openspec/specs/control-center-shell/spec.md` (lines 1–315, fully read): especially 46–90 navigation/unfinished entrypoints, 179–214 tabs and 216 onward unfinished business content.
- `openspec/specs/control-center-permissions/spec.md` (lines 1–91, fully read): exact permissions, module matrix, UI-only checks and server-owned scopes.

Mandatory prerequisites read fully before conclusions about access or mock semantics:

- `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52).
- Under that same change, `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138).
- `openspec/changes/archive/2026-10-09-add-local-session-demo/proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26).
- Under that same change, `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123).

Discovery used file-path enumeration of main specs and active proposals, then scoped matching in direct active-change Markdown artifacts (excluding archive and the reconciliation/audit container). Exact issue keys, `assistant-modules`, and Russian global-module terms produced no corresponding active business-change owner. Main-spec matches locate existing mock coverage and shell/access ownership, not a dedicated global-module frontend capability. Historical module-contract archive directory names were discovered but not treated as active owners or semantically audited. Router implementation and shadcn composition are outside this lane; no conclusions or changes to either are proposed.

## Provenance and status distinctions

Locally recomputed SHA-256 and byte lengths match both task and metadata:

| Artifact | Bytes | SHA-256 |
|---|---:|---|
| Jira operations r1 content | 9933 | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| Wiki 241088180 r1 content | 36471 | `e1d5f5320e05d1e65354f2523341cab788adfacac8ac5acf6aaabf31003c18fc` |

Jira root `sourceId=jira-operations-details`, retrieval `2026-10-16T13:02:57.872Z`, and allowlist include both selected keys. Metadata records verified-origin GET collection and hierarchy membership; this run verifies local consistency, not external origin independently. MOS-717 `/items/0` is CLOSED, updated `2026-10-15T15:13:58.701+0800`. Both recorded comments are present (`total=2`):

- `/items/0/comments/items/0`, id `1131251`, created/updated `2026-10-15T14:53:23.231+0800`, links page **241088180**.
- `/items/0/comments/items/1`, id `1131293`, created/updated `2026-10-15T15:13:58.695+0800`, says **«Неактуально»**. Its object/scope is unspecified: not proven cancellation of MOS-920, not approval, and not a license to discard the contract.

MOS-920 `/items/2` is **Backlog**, updated `2026-10-15T14:46:59.601+0800`, with zero comments (`total=0`). Its description explicitly says contract draft, explicit methods exist, and status confirmation is required before integration acceptance. Empty attachments/subtasks in the selected records do not establish anything about uncollected custom fields or attachment bodies.

Wiki content/metadata agree on `sourceId=wiki-241088180`, HTTP status 200, retrieval `2026-10-16T13:03:14.658Z`, and URL `https://wiki.mos-team.ru/rest/api/content/241088180?expand=body.view,version`. Page version is **4**, timestamp `2026-09-25T19:33:43.672+08:00`; body heading is **contract v1.1**. These are different version axes; `/assistant-modules/v1` is a third, URL version. The saved OpenAPI `info.version=0.1.0` is a document version, not evidence that it supersedes the wiki. Wiki attachment listing is HTTP 200, `results=[]`, `size=0`, metadata count 0/next null. The body has no explicit approval that resolves Jira's draft gate. Publication, page revision, Jira closure and runtime readiness remain separate.

## Key Code / contract evidence

No implementation code was audited. Relevant contract shapes:

```text
DisableModuleRequest.required = [expected_version]
expected_version: integer, minimum 1
confirm_impact: boolean, default false
user_message: string, default ""     # no minLength
EnableModuleRequest.required = [expected_version]
ModuleResponse.status = enabled | disabled
ModuleResponse.disable_allowed: boolean (required)
```

### Exact operation inventory

All paths below exist in `A/sources/api-live/r1/content.json#/paths` (escape `/` as `~1` for literal JSON Pointer traversal). Base `B=/api/control/api/assistant-modules/v1/modules`:

| Method/path | Response schema at `responses/200/content/application~1json/schema/$ref` | Other declared responses |
|---|---|---|
| GET B | `#/components/schemas/TsamResponseSchema_ModuleListResponse_` | 422 HTTPValidationError |
| GET B/summary | `#/components/schemas/TsamResponseSchema_ModuleSummaryResponse_` | none |
| GET B/preview | `#/components/schemas/TsamResponseSchema_ModulePreviewResponse_` | none |
| POST B/{module_id}/disable | `#/components/schemas/TsamResponseSchema_ModuleResponse_` | 422 HTTPValidationError |
| POST B/{module_id}/enable | `#/components/schemas/TsamResponseSchema_ModuleResponse_` | 422 HTTPValidationError |

Wiki `/bodyView` sections **2.1–2.5** publish those same five explicit methods. No additional module detail, edit-message-only, history, bulk or surface-specific method was found under the module path family. Wiki §1 explicitly assigns action history to audit Query API, outside this contract; no audit endpoint is invented here.

OpenAPI GET B `parameters` has nullable string `query` and `status`, array `sort` referencing `ModuleListSort` (name/-name/status/-status/updated_at/-updated_at), limit 1–100 default 20, offset >=0 default 0. Wiki §2.1 instead describes comma-separated status and sort strings, default `name,id` with backend-added stable id. The schema does not establish the wiki's matching, comma parsing or stable ordering behavior.

`#/components/schemas/ModuleResponse` requires id/version/code/name/description/status/disable_allowed/disable_impact_message/user_message/updated_at. Impact and user message are nullable; `by` is optional/nullable. Actor name is structured family_name/name/middle_name. Module IDs and mutation path IDs are UUID in OpenAPI, versus UUIDv7 prose in wiki; actor id is a plain string in schema versus UUID prose. These differences should be preserved rather than strengthened by inference.

Summary closure: `ModuleSummaryResponse` requires system_state, totals, banner, disabled_modules; `ModuleSystemState` is healthy/degraded; `ModuleSummaryTotalsResponse` has total/enabled/disabled/disable_allowed/not_disable_allowed; banner tone success/warning. Preview closure: `ModulePreviewResponse` requires state/caption/cards; each `ModulePreviewCardResponse` requires module_id/module_name/type/sample_user_message/assistant_message; type enum is fallback. Examples and mock derivation rules are not proof of production calculations.

Wiki §2.6 lists 400 INVALID_ARGUMENT, 401 UNAUTHENTICATED, 403 FORBIDDEN, 404 NOT_FOUND, 409 MODULE_NOT_DISABLEABLE / INVALID_STATE_TRANSITION / VERSION_CONFLICT, and 422 USER_MESSAGE_REQUIRED / IMPACT_CONFIRMATION_REQUIRED. These specific error responses/codes are **not declared** in the five OpenAPI operations; 422 uses HTTPValidationError, not the wiki's universal business envelope. Success wrappers require code/data/message, not errors; `ResponseCode` is unconstrained string, not a SUCCESS-only enum. Error detail ownership must remain explicit.

The module operations' saved security arrays list separate `{AdminToken:[]}` and `{AccessToken:[]}` alternatives (formal OR). Approved auth artifacts explicitly retain the correction to both raw headers (AND) and prohibit using that source mismatch to weaken transport. This report does not change security metadata or infer runtime enforcement.

## Atomic candidates and existing-owner coverage

Candidate IDs are audit identifiers, not approved requirements or implementation tasks. W means wiki `content.json#/bodyView`, J means selected Jira item description.

| ID | Atomic candidate / exact evidence | Existing coverage and disposition |
|---|---|---|
| MOS920-C01 | Show system summary. J `/items/2/description`; W §2.2; OpenAPI GET B/summary + ModuleSummaryResponse. | Main mock spec 157–191 covers derived summary; shell is only an entrypoint. **Keep intent; defer business integration acceptance** pending gate. |
| MOS920-C02 | Show searchable/filterable/sortable paginated module registry. J items0/description; W §§1,2.1; GET B. | Main mock spec 138–155 covers local query semantics. **Keep**, flag wire-format/default sorting questions; do not turn mock conventions into backend rules. |
| MOS920-C03 | Represent each module's enabled/disabled state, disable eligibility, user message and last actor/time. J items0/description; W §§1.1–1.2; ModuleResponse. | Mock actions describe version/actor/time. **Keep**, preserve nullable/optional actor and UUID differences for clarification; no invented actor. |
| MOS920-C04 | Display «Что видит пользователь» from preview response. J items2/description; W §2.3; GET B/preview. | Mock spec 159,168–176 covers coherent fallback preview. **Keep**; examples are not a new authored-message API or production fallback guarantee. |
| MOS920-C05 | Disable affects all surfaces, not selected surface only. J items0/description; W business rule 1. | Mock state is coherent, but it is not real global propagation proof. **Keep intent; question runtime applicability/evidence**, no frontend surface-scoping substitute. |
| MOS920-C06 | Permit disable only when `disable_allowed=true`; toggle appearance must not permit core/classifier disable against API. J items0 and items2 descriptions; W business rule 2; ModuleResponse. | Mock spec 161 rejects false eligibility; permissions additionally constrain visibility. **Keep**, not a hard-coded module-name allowlist. |
| MOS920-C07 | Disable requires a **nonempty user_message**. J items0 and items2 descriptions; W business rule 3 and §2.4. | OpenAPI defaults empty; mock spec 161 explicitly stores empty default. **Question/update candidate for future agreed reconciliation**, not permission to relax intended UX or edit mock now. Whitespace/length rules remain unspecified. |
| MOS920-C08 | Disable requires **confirm_impact=true**, with consequences shown using disable_impact_message. Same J/W pointers, W §1.2. | OpenAPI optional false default; mock spec 161 only requires true when impact message is nonempty and uses 409. **Question/update candidate**, unconditional intended confirmation must not silently become conditional. |
| MOS920-C09 | Both mutations send expected_version; enable needs no additional business input. W business rules 4–5, §§2.4–2.5; DisableModuleRequest / EnableModuleRequest. | Main mock spec 161 requires >=1 and models version increments/conflict. **Keep**; “no extra input” is not an empty-body enable. No unprovided Idempotency-Key requirement is added to these operations. |
| MOS920-C10 | Changes update who/when; failures remain failures and do not imply successful state change. J items0/description; W business rule 6, §2.6. | Main mock spec 161,178–186 covers state-preserving rejections, but exact errors/transitions differ. **Keep metadata intent; question error wire format and repeat-target behavior** (mock permits repeat with current version, wiki lists invalid transition). |
| MOS920-C11 | Require contract-status confirmation before integration acceptance. J items2/description; items0/comments/items1 unresolved. | No dedicated active MOS-920 business owner found. **Keep gate, defer acceptance**; not canceled by CLOSED or published endpoints. |
| MOS920-C12 | Access matrix belongs to common rights ownership, not new feature roles. J items2/description; W §2.7; approved control-center-permissions 9–37,60–91. | **Keep/no-op ownership**: Module:view, Module:enable/disable through confirmed permissions; backend owns object access/404 and authorization. Do not implement role-name grants. Wiki's super-admin write/platform-admin and quality-analyst read matrix remains source evidence, not a new approved frontend policy. |

## Architecture / distinctions to preserve

The documents separate four layers: published module wire contract; intended MOS-920 business UX; accepted shell/session/permissions and mock infrastructure; actual implementation/runtime acceptance. Existing main ownership is **control-center-mock-server** for local contract coverage, **control-center-shell** for `/ops` / modules entrypoint, and **control-center-permissions** for access presentation. None supplies proof of completed MOS-920 frontend behavior. There is no inspected dedicated active frontend change to update in place.

Approved permissions allow exact `TSAM.Module:view`, `TSAM.Module:enable`, `TSAM.Module:disable`, corresponding resource grant or explicit `*`; role labels do not grant access. Actions also need screen access and business validity. UI hides unauthorized actions; disabled states remain for business restrictions/pending/unavailable. Transport/mutation handlers must not add permission ACL or synthetic 403; backend decides requests and object scope. Mock business operations remain credential-free without role enforcement. Published role prose does not justify replacing this ownership.

Auth gate distinction: archived auth `tasks.md` lines 48–52 records user confirmation of 6.3 and archiving, expressly **not agent testing of real backend**. Preserve that approved decision; do not reopen or relabel it because demo proposal/design retain older “gate open” language. Conversely that confirmation is not module-specific draft approval, a fresh runtime attestation, or closure of MOS-920's separate gate. No automatic precedence rule is adopted for these status statements.

## Minimal correction candidates / questions

1. **No-op** on source, product, tasks, auth, router and mock code in this lane. Keep existing owner boundaries and unavailable/placeholder honesty.
2. Candidate evidence annotation for future owner review: distinguish “published methods present” from “draft approval unresolved”; retain both MOS-717 comments, MOS-920 Backlog and wiki page/body versions. This is not a new implementation plan.
3. Candidate reconciliation note for future owner review: tabulate nonempty message/unconditional confirmation versus OpenAPI defaults and accepted mock conventions, along with query serialization, UUID/actor nullability and errors. Do not silently rewrite one source to match another.
4. Required owner questions before integration acceptance: What exactly does «Неактуально» retire? Is wiki page4/body v1.1 approved for MOS-920, and by whom? Which request validation/error/transition semantics are intended for backend integration? What serialization/stable-order semantics does backend support? How are server-side accessible modules and global effects evidenced? No business call or new permission model is authorized by these questions.
5. No technical blocker prevented this bounded report. Product ambiguity is reported rather than resolved; actual acceptance remains deferred. Independent review is still expected.

## Start Here

Open `openspec/specs/control-center-mock-server/spec.md` lines **138–191** beside Jira `/items/2/description` and wiki `/bodyView` business rules/§2.4: they expose the material validation mismatch without requiring a code audit. Then use `openspec/specs/control-center-permissions/spec.md` to retain access ownership. Do not start by implementing the toggle or treating `/ops` navigation as completion.

## Validation and residual risks

Manual checks: exact selected Jira keys/comments/timestamps; wiki link identity/version/empty attachments; both bounded hashes and lengths; parsed five OpenAPI operation objects plus referenced-schema closure; scoped active-owner discovery and full main/prerequisite document reading. No tests or runtime checks were run (explicitly prohibited). Absence findings are bounded to inspected active artifacts and the saved module path family, not all possible server services. Saved publication is not live deployment evidence; draft meaning, status contradiction and schema/prose differences remain unresolved. No index inventory attestation is claimed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Bounded primary-evidence report contains verified hashes, atomic MOS920-C01–C12, exact source/schema pointers, owner coverage, preserved gates and unresolved conflicts."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-920.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python SHA-256/JSON inspection and scoped find/read/grep discovery","result":"passed","summary":"Both supplied hashes/byte lengths match; five module operations and their schema closure inspected."},{"command":"Tests/build/network/browser/generation","result":"not-run","summary":"Prohibited by work-item boundary."}],
  "validationOutput": ["Jira 9933 bytes and wiki 36471 bytes match supplied SHA-256 values.","Five module methods present; disable message/confirmation schema constraints do not establish Jira/wiki business requirements."],
  "residualRisks": ["MOS-717 Неактуально meaning and MOS-920 draft approval unresolved.","Schema/wiki/mock validation and error semantics differ; no precedence chosen.","Implementation and deployed module behavior not audited; existing auth approval is not fresh runtime proof."],
  "noStagedFiles": true,
  "diffSummary": "Sole intended repository write is this audit report; no source/product changes or staging performed.",
  "reviewFindings": ["Integration acceptance remains gated; publication is insufficient.","No execution blocker for bounded evidence analysis."],
  "manualNotes": "Fresh local reads only; source HTML inert. Auth/demo prerequisites read fully. No inventory-index claims or task closures; no git staging was performed (index state was not independently inspected)."
}
```
