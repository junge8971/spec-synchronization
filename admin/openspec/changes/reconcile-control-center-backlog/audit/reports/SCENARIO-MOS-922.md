# Code Context

## SCENARIO-MOS-922 — bounded evidence-to-plan findings

**Result:** Explicit library/edit/preview requirements and two publications exist, but no dedicated active product change or main capability was found by LOCAL-001-directed discovery. Publication differences remain unresolved. Neither publication establishes runtime availability, implementation approval or precedence. Preserve approved gates; no implementation plan, activation or task closure is authorized by this report.

## Files Retrieved

Paths are repository-relative; `A` = `openspec/changes/reconcile-control-center-backlog/audit`.

1. `A/work-items/SCENARIO-MOS-922.md` (lines 1–9): assignment.
2. `A/sources/jira-operations-details/r1/content.json` (lines 43–60, 79–96; `/items/1`, `/items/3` only semantically inspected), `metadata.json` (1–42): MOS-754 backend context and MOS-922.
3. `A/sources/wiki-241092242/r1/content.json` (1–64; HTML `/bodyView` is line 39), `metadata.json` (1–54): provenance and stub sections cited below. Inert HTML extraction incidentally displayed the entire body; maintenance form/lifecycle sections were not audited or used to expand scope.
4. `A/sources/api-live/r1/content.json` (line 1, exact JSON selectors below), `metadata.json` (1–19): stub operations, transitive schemas and security definitions only.
5. `A/reports/LOCAL-001.md` (1–173): discovery aid, not primary behavior/completeness evidence. Its lists directed a fresh local scan of `openspec/changes/*/proposal.md` and `openspec/specs/*/spec.md` for `MOS-922`, `заглуш`, `stubs`.
6. `openspec/specs/control-center-permissions/spec.md` (1–91), `openspec/specs/control-center-http/spec.md` (1–138), `openspec/specs/control-center-shell/spec.md` (211–240): current access, transport/recovery and unfinished-content gates. No router implementation analysis.
7. Mandatory auth prerequisite read before permission comparison: `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52), and its `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138). Full packet inspected; archived checkboxes are not fresh runtime proof.

No application code, demo implementation, routing implementation or shadcn analysis performed; those change prerequisites were not applicable to this comparison.

## Provenance and version distinctions

Read-only Python hashing independently matched saved bytes against supplied digests and metadata:

| Source | Bytes | SHA-256 |
|---|---:|---|
| jira-operations-details/r1 | 9,933 | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| wiki-241092242/r1 | 68,316 | `e7b78965be979f2bd450b25881574cf7e8b94cf424be5d052bb2be9df1995158` |
| api-live/r1 | 413,007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |

- Jira capture metadata: 2026-10-16T13:02:57.872Z, parent verified-origin GET. MOS-922 links exactly wiki page 241092242; **Backlog**, updated 2026-10-15T14:46:44.693+0800. MOS-754: **Review**, updated 2026-10-16T19:22:17.361+0800. Both selected records have zero comments and empty attachments. Workflow state is not acceptance or implementation. Custom fields/attachment bodies uncollected.
- Wiki capture: HTTP 200, 2026-10-16T13:03:14.883Z, `https://wiki.mos-team.ru/rest/api/content/241092242?expand=body.view,version`; page revision **4**, modified 2026-09-25T16:59:13.813+08:00. Body says **contract v1.0**, history dated 10.09.2026, first version. Revision 4 is neither contract v4 nor approval. Attachment collection: 200, count 0, no next page. No inspected field establishes business-contract approval.
- OpenAPI capture: 2026-10-16T11:13:29.451Z, `https://nchat-a-tech.mos.ru/api/control/openapi.json`, discovered from same-origin Swagger per metadata. OpenAPI **3.1.0**, service info **0.1.0**, capture **r1** are separate versions. No ETag/Last-Modified. Collection method/origin remain metadata attestations, not independently re-fetched here. No business operation called.

## Key Code / atomic candidate requirements

No code retrieved. Aliases: **J922** = Jira `/items/3/description`; **J754** = `/items/1/description`; **W** = wiki `/bodyView`, named section; **O** = saved OpenAPI. Candidate IDs are analysis labels, not approved tasks or requirements.

| Candidate ID | Atomic candidate and source pointer | Coverage/disposition; owner |
|---|---|---|
| MOS922-C01 | Library entries for `assistant/module/skill/surface`. J922 sentence 1; J754 catalog bullet; W §§1.2, 2.1. | **Defer** dedicated product behavior pending ownership; MOS-922 FE and MOS-754 contract owner. Shell gate is not library coverage. |
| MOS922-C02 | Show `full_stub_text`. J922 sentence 1; W §1.3. | **Defer** dedicated specification; required nullable O response field. |
| MOS922-C03 | Show `substitute_response_text`. Same pointers. | **Defer**, same ownership/coverage distinction. |
| MOS922-C04 | Show `warning_banner_text`. Same pointers. | **Defer**, same ownership/coverage distinction. |
| MOS922-C05 | Inline save updates an **existing record**. J922 sentence 2; W §§2.2–2.3. | **Question/update candidate:** align GET/PUT contract first; no create/upsert/delete promise. |
| MOS922-C06 | `is_applied=false` saves a draft. J922 sentence 3; W §2.3 rules. | **Question:** distinguish persisted draft from effective preview/previous live value; separate versions not modeled. |
| MOS922-C07 | `is_applied=true` requests immediate application subject to maintenance. J922 sentence 3; W business rules, §2.3. | **Keep** source requirement, **defer** activation; saved flag is not proof of effective text. |
| MOS922-C08 | Preview is server-effective output, not merely editor input. J922 sentence 4; W §2.4 purpose; O preview GET. | **Keep** server authority; **question** draft/unsaved-preview UX. No client priority engine. |
| MOS922-C09 | Active maintenance overrides ordinary stub on affected targets. W business rules, §1.5. | **Keep** dependency; backend owns resolution; MOS-923 owns maintenance UI outside this report. |
| MOS922-C10 | Windows resolve by greater `priority`, specificity `surface > skill > module > assistant`, later `updated_at`; completed window has no influence. W §1.5. Cancellation ceases influence: W §2.9 rule only. | **Keep** published explanation, not frontend computation/runtime proof; backend resolves applicability/ties. |
| MOS922-C11 | Catalog filters `target_type`, `is_applied`, name `query`, `limit`, `offset`, with pagination. W §2.1; O catalog GET. | **Defer** UI detail choice; **keep** published query semantics. No sorting/target-directory API inferred. |
| MOS922-C12 | Edit one/several/all texts; empty string forbidden. W §2.3 rules. | **Question/update candidate:** reconcile null/omission/empty/whitespace validation with O before relaxing constraints. |
| MOS922-C13 | Preserve last-change metadata. W business rules “who/when/what”, §§1.3, 2.3; O settings/summary. | **Question:** `by.id`/`updated_at` cover who/when; no inspected stub delta/history field covers “what”. No invented audit endpoint. |
| MOS922-C14 | Restricted collections; inaccessible target returns 404. W §§2.10–2.11. | **Keep** server scope; **question** permission mapping with auth owner. Wiki roles do not grant UI access. |

### Exact methods and field differences

**W-base:** `/api/control/api/assistant-ops/v1`. **O-base:** `/api/control/api/maintenance/v1`. This prefix difference is unresolved, not a fallback/redirect instruction.

| Operation | Wiki | O exact selector and success schema |
|---|---|---|
| Catalog | §2.1 `GET W-base/stubs/catalog` | `/paths/[O-base/stubs/catalog]/get`; 200 `TsamResponseSchema_StubCatalogResponse_`. |
| Settings | §2.2 `GET W-base/stubs/{target_type}/{target_id}` | `/paths/[O-base/stubs/{target_type}/{target_id}]/get`; 200 `TsamResponseSchema_StubSettingsResponse_`. |
| Existing-record save | §2.3 `PUT W-base/stubs/{target_type}/{target_id}` | Same O path `/put`; required body `UpdateStubSettingsRequest`; 200 `TsamResponseSchema_StubSettingsSummaryResponse_`. |
| Effective preview | §2.4 `GET W-base/stubs/{target_type}/{target_id}/preview` | `/paths/[O-base/stubs/{target_type}/{target_id}/preview]/get`; 200 `TsamResponseSchema_StubPreviewCardResponse_`. Only path parameters, no unsaved draft body/sample-message query. |

Schema names below are exact O `/components/schemas/<name>` pointers:

- `MaintenanceTargetType` enumerates exactly four target types. `StubTargetResponse` requires enum `type`, string `id`, string `name`. W §§1.2/2.2 requires stable `assistant` ID for assistant, **UUIDv7** for other types; O path `target_id` and response ID are unrestricted strings, without conditional UUID/version validation. Do not manufacture an assistant UUID.
- `StubSettingsSummaryResponse` requires target, three nullable text strings, boolean `is_applied`, date-time `updated_at`, `by`. `ByResponse.id` is required string with no UUID format; W says UUID. `StubSettingsResponse` additionally requires `preview`.
- `UpdateStubSettingsRequest` requires **only `is_applied`**. Three texts are optional nullable strings, with no minLength/maxLength/pattern/whitespace rule. W allows partial text editing and prohibits empty string but does not define null-versus-omitted updates. O does not encode empty-string prohibition. Neither establishes maximum length, markup support/sanitization or clearing protocol. Flag-only/empty-body semantics need clarification, not guessed rejection/acceptance.
- `StubPreviewResponse` requires nullable `sample_user_message`, `result_message`, `banner_message`; W §1.3 marks these nested fields optional. `StubPreviewCardResponse` requires target, all three nullable message fields, `preview_state` enum **normal/warning**, and string `source`. W §2.4 shows `warning`/`maintenance_window` as examples, not full enumerations. Do not hard-code `source` as a one-value enum or invent a third preview state.
- Catalog defaults agree: limit 20/offset 0. O additionally bounds limit **1–100**, offset **>=0**. Optional query schemas allow null; shared HTTP forbids serializing undefined/null as literal query strings. `StubCatalogResponse` requires items of `StubSettingsSummaryResponse` and `PaginationDto`; pagination requires limit/offset/current_page/total_items/total_pages. No inferred totals or filtering only a loaded page.
- PUT response is settings **summary**, not effective preview. Future UI must distinguish save acknowledgement from separately refreshed server preview; read atomicity, freshness, polling and subscriptions are not published. Preview failure cannot negate or disprove a separately acknowledged save.

### Errors, concurrency and security

- W §2.10 publishes 400 `INVALID_ARGUMENT`, 401 `UNAUTHENTICATED`, 403 `FORBIDDEN`, 404 `NOT_FOUND`, 409 `STUB_TARGET_CONFLICT` (already changed or incompatible with active window), 422 `VALIDATION_ERROR`. Maintenance-only conflict codes are not adopted as stub-editor requirements.
- W says every response uses `code/data/message/errors`, error data null, with field/details error elements. O stub operations declare only **200 and 422**; 422 uses `HTTPValidationError.detail[]` → `ValidationError` with required `loc/msg/type`, optional input/ctx, not W's envelope. O success envelopes require code/data/message; errors is optional. `ResponseCode` is plain string. Missing status declarations do not prove other errors impossible.
- No expected_version/revision, ETag/If-Match, idempotency parameter or conflict-resolution protocol appears in inspected stub operations. `updated_at` is metadata, not a documented precondition. Do not borrow skill version fields or promise backend idempotency. Ask MOS-754 owner about stale writes and uncertain-result recovery.
- O security formally lists `[{AdminToken:[]},{AccessToken:[]}]` (OR), but both security-scheme descriptions require **both raw tokens**, headers `X-Admin-Token`/`X-Access-Token`. Approved auth/current HTTP requires both. Record discrepancy; do not weaken credentials or declare enforcement verified.
- W §2.11 gives super-administrator/platform administrator view/edit and quality analyst view-only. Current permissions policy uses confirmed exact grants, **explicit `*` for unmapped stub UI**, never role names; backend scope/403/404 remain final. No precedence or new mapping decided here. Ask permission owner for approved granular resource/actions rather than inventing permissions or recommending wildcard grants to unlock the feature.

## Architecture / owner and coverage mapping

| Existing owner/boundary | Coverage found | Bounded disposition |
|---|---|---|
| MOS-922 dedicated product change | No corresponding active proposal in fresh `openspec/changes/*/proposal.md` scan; LOCAL-001 main list and fresh main-spec scan identify shared gates, not dedicated library/editor specification. | **Question/defer:** parent/product owner assigns ownership outside audit. No existing MOS-922 proposal/design/spec/tasks packet discovered to revise. This is not implementation-completeness evidence. |
| MOS-754 | Selected backend task plus published wiki/OpenAPI. | **Update candidates/questions:** prefix, update/null semantics, errors, preview and conflicts. No contract edits/API calls. |
| `control-center-http` | Contract-aligned requests, errors/cancellation/no replay, both tokens; lines 102–109 explicitly prevent publication from activating screens. | **Keep** gates; any reconciliation needs owner review, not blanket replacement. |
| `control-center-permissions` | Exact confirmed grants, wildcard-only unmapped UI, server scope, no transport ACL. | **Keep**; **question** approved view/edit/preview mapping, not role adoption. |
| `control-center-shell` | Line 218 forbids unfinished operations content from simulating working business operations. | **Keep** until separately approved integration; no routing/menu change proposed. |
| Archived auth change | Full session/recovery/security packet; tasks line 52 records user confirmation on 09.10.2026 and explicitly no agent real-backend testing. | **Keep** historical approval and original scope; do not recast it as runtime proof for stub operations. |
| MOS-923 | Only necessary effective-preview priority/influence dependency used. | **Defer** maintenance form/lifecycle/scheduling audit to its separate analyst. |

### Narrow correction candidates / owner questions

1. **MOS-754/API owner:** Which prefix belongs to the agreed frontend contract? Are publications aliases or different snapshots? No automatic fallback or source precedence selected.
2. **MOS-754/API owner:** Define omitted/null/empty/whitespace texts, lengths, plain-text versus markup, always-required `is_applied`, and what happens to previous live text when a draft is saved.
3. **MOS-754/MOS-922 owners:** Does draft preview intentionally show effective current live/maintenance output? No operation accepts unsaved edits. Clarify labeling, save versus preview failure, freshness and warning-before-start behavior without presenting local input as server-effective output.
4. **MOS-754/API owner:** Confirm 422 shape, 409/precondition contract, explicit retry and uncertain-result handling, and any idempotency support. Keep input/error rather than silently overwriting/replaying.
5. **MOS-754/backend and MOS-923 owner:** Confirm source provenance, target applicability and exact ties after all documented priority tie-breakers. No client approximation from partial window lists.
6. **Permission owner:** Approve resource/actions for library/settings/preview/edit and references; explain role prose versus confirmed grants/scopes. Preserve existing conservative policy/backend authorization meanwhile.
7. **Product owner/parent:** Assign candidate requirements to approved ownership outside this audit. Do not silently create a change, close MOS-922, activate endpoints or replace unfinished-content gates.

### Preserved validation / recovery / security gates

- Empty-string prohibition remains a source candidate despite absent schema minimums. Ambiguity does not permit relaxed validation. Distinguish null/missing/empty, request failure and valid empty catalog.
- Preserve loading/error/retry/unavailable/denied and failed-save input; malformed successful bodies/application errors are not success. No invented error-free local fallback.
- Approved recovery forbids automatic mutation replay after 401/network error. Retain original logical-operation parameters where applicable; preserve same confirmed user's draft across refresh, isolate other users and ignore stale responses. Do not invent version/idempotency fields in stub payloads.
- Preserve session boundary, trusted credential destinations, both token headers, backend access/scope authority and safe text rendering. Source HTML remains inert. Permission availability does not establish API availability or business admissibility.
- Existing auth release confirmation remains approval evidence with its original scope; neither it nor saved OpenAPI proves stub runtime behavior. No new release gate declared satisfied.

## Start Here

Read wiki `/bodyView` §§2.3–2.4 with O `UpdateStubSettingsRequest` and the three stub paths. First resolve prefix, update semantics and effective-preview meaning with owners, not implementation or a client priority calculator.

## Limits / verification

Local read-only JSON/HTML inspection, saved-byte hashing, selective schema traversal and scoped discovery only. No network/MCP/browser/tests/build/generation/git inspection or mutation, source/code edits, nested agents, archive/sync or new product plan. Sole intentional write: this report. No staged/index-state attestation. No blocker to bounded reporting; unresolved owner questions block inference, not this evidence result. Independent review remains required.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Verified three saved-source hashes; extracted MOS922-C01–C14 with exact Jira/wiki/OpenAPI pointers, publication differences, ownership limits and preserved approved gates."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-922.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python SHA-256 and JSON inspection","result":"passed","summary":"All three digests and byte counts match metadata and assignment."},
    {"command":"Inert HTML extraction and stub OpenAPI reference traversal","result":"passed","summary":"Only stub behavior and necessary priority dependencies analyzed; extraction incidentally displayed other maintenance sections, not audited."},
    {"command":"LOCAL-001-directed find/scoped proposal and main-spec scan; wc/nl citation checks","result":"passed","summary":"No dedicated MOS-922 product packet found; shared gates identified and cited."},
    {"command":"Tests/build/generation/network/browser/git","result":"not-run","summary":"Outside or forbidden by bounded read-only assignment."}
  ],
  "validationOutput": ["Jira 9933, wiki 68316, OpenAPI 413007 bytes; all hashes matched.","Wiki revision 4, body v1.0, OpenAPI info 0.1.0 and capture r1 kept distinct."],
  "residualRisks": ["Prefix, partial/null update semantics, errors/concurrency and draft/effective preview need owner clarification.","No runtime or implementation-completeness verification; no dedicated active MOS-922 packet discovered.","Granular permission mapping unresolved; independent review pending."],
  "diffSummary": "Only bounded report written; no product/source/spec/code edits.",
  "reviewFindings": ["No reporting blocker; no activation, precedence, task closure or client priority computation inferred."],
  "manualNotes": "Auth proposal/design/all delta specs/tasks inspected before permission comparison. Historical user release confirmation remains approval evidence, not fresh backend testing. No index-state claim."
}
```
