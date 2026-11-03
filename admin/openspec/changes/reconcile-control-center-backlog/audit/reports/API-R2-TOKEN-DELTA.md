# Code Context

## Disposition

**New publication; bounded documentation-update candidates only.** r2 publishes two business skill-token commands, six new schemas and token-bearing shared skill responses. This resolves the narrow r1 absence-of-publication finding, not MOS-1023 task 1.1, approved secret-handling semantics, deployment verification, or sandbox activation. Keep the existing `mos-1023-skill-environment-tokens` owner and all unchecked tasks. No duplicate change, implementation or feature closure is justified.

## Files Retrieved

Repository-relative paths; `A` = `openspec/changes/reconcile-control-center-backlog/audit`. JSON pointers below are exact selectors within single-line API content.

1. `A/work-items/API-R2-TOKEN-DELTA.md` (1–9): bounded assignment.
2. `A/sources/api-live/r1/content.json` and `A/sources/api-live/r2/content.json` (each line 1): selected token paths, six new schemas, complete recursively reachable schema definitions, shared skill DTO delta and security definitions. Corresponding `metadata.json` files read completely.
3. `A/sources/api-docs/r1/content.html` (1–32), corresponding `metadata.json` (complete): inert Swagger discovery receipt, not executed JavaScript.
4. `openspec/changes/mos-1023-skill-environment-tokens/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-environment-tokens/spec.md` (1–47): complete active owner proposal/design/spec/tasks.
5. `openspec/specs/skill-connection-settings/spec.md` (1–55): main connection capability, particularly line 11 prohibiting business-token secret as connection/anketa text. Discovery found no main `skill-environment-tokens` capability; it remains the active change's new capability, not a delivered main spec.
6. `openspec/specs/skill-checks-training/spec.md` (63–70), `openspec/specs/surface-lifecycle-publication/spec.md` (65–68): explicit readiness and no-sandbox-workflow boundaries.
7. `A/reports/REQ-MOS-1023.md` (1–89), `A/reviews/RECON-MOS-1023.md` (1–78): historical extraction plus corrective review, not independently re-extracted Jira/wiki evidence in this run.
8. `A/reports/SCENARIO-MOS-962.md` (1–108), `A/reviews/R-SCENARIO-MOS-962.md` (1–107), `A/decisions.md` (93–103, D-012): accepted sandbox findings only with mandatory review corrections.

### Provenance

Local SHA-256 matches both supplied digests and metadata:

- r1: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`; retrieved 2026-10-16T11:13:29.451Z; 94 paths / 128 operations / 382 schemas.
- r2: `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993`; retrieved 2026-10-19T08:11:44.238Z; 96 paths / 130 operations / 388 schemas.
- Discovery HTML: `02aecc4a486cd3b697887ca917500e2cbd031ee9e1177dfba17c1bf588873ece`; retrieved 2026-10-19T08:10:46.142Z. Line 17 configures `/api/control/openapi.json`, resolved in metadata to `https://nchat-a-tech.mos.ru/api/control/openapi.json`.

Counts are publication metadata, not endpoint execution. The new HTML receipt does not retroactively establish r1 acquisition. No business operations, credentials or examples were executed. A-publication does not prove T runtime equivalence.

## Key Code

### Exact before/after pointers

For this section `R1` / `R2` mean the respective `A/sources/api-live/r*/content.json`; `S` means `/components/schemas`; `K` is the exact schema key `tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`.

**New operations:** both R1 paths absent; R2 adds:

- `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1tokens~1{environment}~1reissue/post`
- `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1tokens~1{environment}~1revoke/post`

At each operation:

- `/parameters/0`: required path `skill_id`, string format `uuid7`.
- `/parameters/1`: required path `environment` → `#/components/schemas/SkillTokenEnvironmentCode`.
- `/parameters/2`: required header `Idempotency-Key`, string format `uuid`.
- `/requestBody`: required JSON → `SkillTokenMutationRequest`; required `expected_version` integer, minimum 1. No request secret field. No explicit additional-property rejection follows from this schema.
- `/responses/200/content/application~1json/schema`: reissue → `TsamResponseSchema_SkillTokenIssuanceResponse_`; revoke → existing `TsamResponseSchema_SkillResponse_`.
- `/responses/422/content/application~1json/schema` → unchanged `HTTPValidationError` → `ValidationError`.
- No operation description. The only success extensions are `x-success-message`: «Токен навыка перевыпущен.» / «Токен навыка отозван.». Neither is an old-credential invalidation guarantee or execution evidence.
- `/security` is published as `[{"AdminToken":[]},{"AccessToken":[]}]`. `/components/securitySchemes` is unchanged from r1, with X-Admin-Token / X-Access-Token header definitions and descriptions requesting both raw tokens. This report does not reinterpret admin auth or change agreed transport constraints. Do not derive new transport or operation grants from these declarations; no token-operation permission name is documented here.

**All six new schemas:** each absent at the identical R1 `S/<name>` pointer, present at R2:

| Schema | Exact structure relevant to MOS-1023 |
|---|---|
| `SkillTokenEnvironmentCode` | enum exactly `sandbox`, `whitelist`, `prod`. Environment codes, not scope vocabulary or skill-state selection rules. |
| `SkillTokenMutationRequest` | object with required `expected_version: integer >= 1`. |
| `SkillTokenResponse` | All seven fields required: `id` UUID, `environment` enum reference, `is_active` boolean, `issued_at` date-time, `revoked_at` date-time-or-null, `issued_by` string, `token_value` string-or-null. Required does not mean non-null. No scope/expiry field, `skill_id` field, issuer UUID constraint, active-record uniqueness or lifecycle invariants. |
| `IssuedSkillTokenResponse` | Same seven required fields; `token_value` is non-null string, but no minLength/pattern/one-time-disclosure rule. `is_active` is not constrained true; `revoked_at` remains nullable. |
| `SkillTokenIssuanceResponse` | Full shared skill properties plus required `issued_token`, whose value is `IssuedSkillTokenResponse` **or null**. Includes required `tokens`, `version`, `checks`, status and other skill fields. Not just a secret payload. |
| `TsamResponseSchema_SkillTokenIssuanceResponse_` | Required `code`, `data`, `message`; `data` references issuance response. Optional array `errors` → unchanged `ErrorItem`. `ResponseCode` is an unconstrained string. |

**Shared DTO delta and sibling coordination:** R1 `S/K/properties/tokens` absent; R2 adds required array `tokens`, items → `SkillTokenResponse`; `S/K/required` adds `tokens`. This is the only change within that DTO. Existing `S/TsamResponseSchema_SkillResponse_/properties/data/$ref` remains `#/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`. Never substitute nonexistent plain `SkillResponse` or dialogs' namespaced DTO. The ordinary skill GET and revoke response thus reach potentially secret-bearing records. Status-operation analysis remains the sibling's scope; the shared dependency is exactly this DTO pointer, not a separate token model or duplicated status review.

**Reachable errors:** both commands explicitly list only HTTP 200 and 422. `HTTPValidationError.properties.detail.items` references `ValidationError` (required loc/msg/type; optional unconstrained input and ctx). `ErrorItem` requires message, with optional nullable field/code/details; details permits arbitrary properties. No token-specific conflict/authorization/not-found/audit error matrix, idempotent replay retention rule, response-loss recovery, or error-redaction guarantee appears in these operation/DTO definitions. Do not borrow another skill command's 409 codes or replay policy as token-operation guarantees. Preserve safe diagnostics; schema openness is not proof a secret will leak.

Other recursively reachable schemas (domain/team/contact/name, materials, connection/parameter/auth-type, intents/phrases/entity types, SkillStatus and check types/status/results) are unchanged from r1. Their existence supplies no revocation or readiness protocol.

## Architecture

The current plan owns a shared business model/API in `app/entities/skill/`, consumed by the connection card and eventual gated sandbox receiver. Navigation passes only skill ID. Business skill-token rotation is not admin-session refresh. This review makes no admin-policy interpretation; existing transport constraints and historical approval remain unchanged. D-012 explicitly preserves the recorded 09.10.2026 user approval without exporting it to sandbox or treating it as agent deployment verification.

Important integration risk: the plan permits ordinary metadata caching, but r2's ordinary `SkillTokenResponse.token_value` may contain a string. A full skill response cannot automatically be classified as nonsecret metadata. Any future authorized integration must separate/sanitize secret-bearing data before general cache, persistence, logs or telemetry; clearing only `issued_token` is insufficient. This is a contract-impact finding, not an implementation audit or authorization to change cache behavior now.

### Stable candidate register — existing owner and remaining gates

| ID | Resolved publication gap / candidate | Owner and retained question |
|---|---|---|
| **API-R2-TOKEN-01** | Replace a present-tense blanket “no token operations/DTOs published” with the exact two paths and six schemas above, while retaining r1 provenance. | Existing MOS-1023 proposal Impact and design/task 1.1. Documentation update candidate only; no task check-off or local-contract regeneration. |
| **API-R2-TOKEN-02** | Environment route codes and mutation input shape are now explicit: sandbox/whitelist/prod, expected_version and required UUID idempotency header. | MOS-1023 task 1.1: confirm expected_version ownership/increment behavior, stale-version errors, key scope/retention, replay payload (especially secret), reuse conflicts and unknown-outcome reconciliation. Header presence does not authorize automatic reissue after timeout. |
| **API-R2-TOKEN-03** | Lifecycle metadata and nullable value have a concrete DTO; shared skill response now requires tokens. | MOS-1023 Server token metadata / task 2.1: define empty list, absent environment, inactive/revoked versus explicitly unissued, current-state selection, history completeness and uniqueness. Neither null token_value nor false is_active nor empty tokens proves “не выдан”. Issued_at/revoked_at are not expiry; environment is not scope. |
| **API-R2-TOKEN-04** | Reissue distinguishes required-but-nullable issued_token from the ordinary tokens array; non-null issued_token has a non-null string token_value. | Existing disclosure/security gate and tasks 2.2/2.4: when is issued_token null, when can ordinary token_value be present, masking/reveal/copy permissions, one-time versus repeat display, cleanup and safe diagnostics? No display, clipboard or permanent-secret-storage permission follows from publication. Secret separation risk described above. |
| **API-R2-TOKEN-05** | Explicit revoke command and reissue command now exist, with updated skill/issuance response shapes. | Existing task 1.1 and accepted SCENARIO-MOS-962-03: does reissue atomically revoke the prior token, which prior record, immediate versus overlap/propagation, authoritative invalidation confirmation, already-revoked/no-token behavior, partial/lost response and audit responsibilities? There is **no explicit revocation guarantee** in the inspected operation/DTO prose, and separately no deployment evidence. A changed value, is_active/revoked_at, or success message alone does not close MOS-962. Do not synthesize a revoke-then-reissue sequence. |
| **API-R2-TOKEN-06** | Shared response path permits documenting integration impact on card/sandbox and the sibling status consumer. | MOS-1023 shared model and secret-free navigation remain; sandbox target/binding, readiness, stand sync and operation permission mapping remain unresolved. Main surface MVP still excludes visible/hidden launch. No new UI activation, token fetch or session model. |

### Targeted stale-for-current mapping

Historical sources stay intact; these are annotations/corrections for a separately authorized writer, not retroactive edits or automatic source precedence.

| Existing assertion / exact locator | r2 correction and what remains valid |
|---|---|
| `A/reviews/RECON-MOS-1023.md`, **Key Code / Primary evidence**, “No path name contains token … no token-named schema”; C2 row | Valid for r1; false if reused as r2 inventory. Cite API-R2-TOKEN-01 and precise before/after pointers. Prior gate/state/disclosure recommendations remain recommendations, not adopted requirements. |
| `A/reports/REQ-MOS-1023.md`, C2 and REQ-03/08/13–16 | The saved Jira/wiki statements are historical source assertions, not claims to rewrite. New reissue/revoke publication narrows the integration gap; it does not settle initial issuance trigger, disclosure, lifetime, scope or rotation consequences. Wiki rotate route is not the newly published reissue route. |
| `A/reports/SCENARIO-MOS-962.md`, **Exact published contract pointers**, final bullet; candidates 03/04 | “No … token lifecycle schema” remains r1-valid only. r2 has lifecycle metadata and commands. Candidate 03's demand for confirmed old revocation and candidate 04's shared-model/security gate remain valid. Read with independent review and D-012, never its superseded open-auth-gate sentence. |
| `A/reviews/R-SCENARIO-MOS-962.md`, required correction 4; `A/decisions.md` D-012 lines 101–103 | Preserve snapshot bounding and all accepted approval/sandbox corrections. r2 resolves operation/DTO absence, not missing confirmed revocation semantics or deployment proof. |
| `openspec/changes/mos-1023-skill-environment-tokens/proposal.md` lines 21–27; design lines 11–17; tasks lines 1–6 | Proposal explicitly cites local `docs/api/contracts/openapi.json`, which was not inspected here. Do **not** declare that local-file claim false based on remote r2. Candidate: add separately dated r2 evidence and partition resolved shape questions from remaining task-1.1 security/behavior gates. Preserve unavailable/blocked implementation until agreement, all unchecked tasks and independent acceptance. |

## Start Here

Open `openspec/changes/mos-1023-skill-environment-tokens/design.md` (11–17), then task 1.1 (`tasks.md` 1–6), alongside the R2 shared DTO and issued_token pointers. The next authorized documentation step should distinguish newly published shapes from unresolved safe disclosure/revocation/recovery semantics, not start implementation. No required audit input was unavailable; the remaining questions are owner decisions inside existing gates, not blockers to this report.

## Validation and residual risks

Local read-only file discovery, selected JSON traversal/comparison and SHA-256 checks only. No actual tokens, network/browser/MCP, tests/builds, source/code/spec/task edits, API generation, sync/archive or nested delegation. Only this authoritative report was written. No index-state inspection or no-staged-files attestation. Runtime support, secret-return policy, revocation guarantee and idempotent recovery remain unverified; no implementation-compliance conclusion is made.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Compared verified r1/r2 snapshots, both new token operations and six schemas with the complete MOS-1023 plan and accepted MOS-962/D-012 boundaries; supplied six stable candidates and targeted historical/current claim mappings."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/API-R2-TOKEN-DELTA.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local file discovery/read and Python JSON traversal/comparison/SHA-256","result":"passed","summary":"Both API hashes and Swagger HTML hash match metadata; reachable schemas inspected and shared required tokens delta verified."},
    {"command":"Tests/build/network/browser/API execution","result":"not-run","summary":"Prohibited by assignment; documentation-only analysis."}
  ],
  "validationOutput": ["Publication now includes reissue/revoke and six token schemas; existing implementation/security/sandbox gates retained.","Ordinary token_value is nullable but potentially secret-bearing; issued_token itself is required and nullable."],
  "residualRisks": ["No runtime/deployment or old-token invalidation evidence.","Disclosure, scope/lifetime, state mapping, idempotency/recovery, operation authorization mapping and revocation consequences remain unresolved.","Ordinary skill responses may carry secrets; no implementation/cache audit performed."],
  "diffSummary": "Only the authoritative report written; no product/code/spec/task changes.",
  "reviewFindings": ["Bounded documentation-update candidates only; no duplicate plan, UI activation or task closure."],
  "manualNotes": "Historical r1 findings preserved, accepted MOS-962 review/D-012 corrections retained. Admin transport not reinterpreted; index state not inspected. No credentials retrieved."
}
```
