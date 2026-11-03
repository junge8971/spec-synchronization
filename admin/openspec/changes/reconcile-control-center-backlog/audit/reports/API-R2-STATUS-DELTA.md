# Code Context

## API-R2-STATUS-DELTA — exact saved-publication comparison

**Result:** one existing operation changes its 200 response reference; one existing namespaced skill DTO gains required `tokens`. The new status response retains every prior skill-card field and adds `tokens` plus required-nullable `issued_token`. Readiness, queue, errors, concurrency inputs and explicit three-command approval are unchanged. This is documentary impact evidence, not deployment proof or implementation authorization. Historical reports remain intact; only the specifically identified current-publication claims below require qualification.

## Files Retrieved

Repository-relative root **A** = `openspec/changes/reconcile-control-center-backlog/audit`. JSON content files are single-line documents: parsed locally in full for comparison, with semantic inspection restricted to the assigned operation/DTO and reference reachability.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/API-R2-STATUS-DELTA.md` (lines 1–11): assigned boundaries.
2. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` and `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r2/content.json` (line 1 each): exact diff, referenced schemas and consumers. Adjacent `metadata.json` files read completely.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-docs/r1/content.html` (lines 1–32) and adjacent `metadata.json` (complete): inert discovery receipt.
4. `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (lines 11–67): D-015–D-021.
5. `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-909.md` (lines 35–124), `openspec/changes/reconcile-control-center-backlog/audit/reports/IMPL-MOS-909.md` (lines 45–144): claim-specific context, not fresh code inspection.
6. `openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-MOS-1119.md` (lines 1–93), `openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-MOS-1119-TESTPLAN.md` (lines 1–122): storage/test-plan claims.
7. `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-909.md` (lines 1–91), `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-IMPL-MOS-909.md` (lines 1–106), `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-DELTA-MOS-1119.md` (lines 1–74), `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-DELTA-MOS-1119-TESTPLAN.md` (lines 1–90), `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-WRITE-MOS-909-RESTORE.md` (lines 1–90): accepted qualifications; numbered output recovered selectively after tool truncation.
8. `openspec/changes/mos-909-restore-approved-lifecycle-actions/proposal.md` (lines 1–27), `openspec/changes/mos-909-restore-approved-lifecycle-actions/design.md` (lines 1–38), `openspec/changes/mos-909-restore-approved-lifecycle-actions/tasks.md` (lines 1–14), `openspec/changes/mos-909-restore-approved-lifecycle-actions/specs/skill-lifecycle/spec.md` (lines 1–35): actual approved restoration scope.

### Provenance

Locally recomputed saved-byte SHA-256 matches both assigned values and metadata:

- r1: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`; captured `2026-10-16T11:13:29.451Z`, metadata 94 paths / 128 operations / 382 schemas.
- r2: `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993`; captured `2026-10-19T08:11:44.238Z`, metadata 96 / 130 / 388.
- Discovery HTML: `02aecc4a486cd3b697887ca917500e2cbd031ee9e1177dfba17c1bf588873ece`; captured `2026-10-19T08:10:46.142Z`. Its Swagger configuration literally says `url: '/api/control/openapi.json'`. Metadata resolves this to `https://nchat-a-tech.mos.ru/api/control/openapi.json`.

The new discovery receipt supports r2 discovery, not retroactive verification of r1 acquisition. No HTML/script execution or remote access occurred. Capture chronology establishes neither source precedence nor a common deployment revision.

## Key Code / exact semantic deltas

Pointers below are exact RFC 6901 paths in both saved JSON documents. Define:

- **OP** = `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`
- **S** = `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`
- **I** = `/components/schemas/SkillTokenIssuanceResponse`

Local parsed comparison of every pre-existing path member and schema found only OP and S changed; no removal was found in that comparison. The two added token operations and six new schemas are not independently analyzed here except the response linkage necessary to resolve OP/S.

### API-R2-STATUS-01 — success envelope retargeted

Exact pointer: **OP**`/responses/200/content/application~1json/schema/$ref`.

- r1: `"#/components/schemas/TsamResponseSchema_SkillResponse_"`
- r2: `"#/components/schemas/TsamResponseSchema_SkillTokenIssuanceResponse_"`

Old envelope `/components/schemas/TsamResponseSchema_SkillResponse_/properties/data/$ref` remains `"#/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse"` in both documents; it is no longer OP's response envelope in r2.

New envelope `/components/schemas/TsamResponseSchema_SkillTokenIssuanceResponse_/properties/data/$ref` is `"#/components/schemas/SkillTokenIssuanceResponse"` (absent in r1). Both envelopes require `code`, `data`, `message`; optional `errors` remains an array of ErrorItem. This is not a replacement of the card by a token-only response.

### API-R2-STATUS-02 — required token collection on existing detail DTO

Exact pointer **S**`/properties/tokens`:

- r1: absent.
- r2: `{"items":{"$ref":"#/components/schemas/SkillTokenResponse"},"type":"array","title":"Tokens"}`.

Exact pointer **S**`/required`: r2 inserts `"tokens"` at index 18, after `"intents"` and before `"status"`; r1 index 18 is `"status"`, which moves to 19. The old required set is otherwise identical (27 → 28 entries). This is one required-member insertion, not multiple semantic changes caused by shifted indices.

`tokens` is required, non-null, without a default or minimum count: an empty array is permitted, omission/null is not described as valid. No cardinality, ordering or one-token-per-environment guarantee follows. All other S properties, including checks, status/version and process metadata, are exactly unchanged.

Linkage only: `/components/schemas/SkillTokenResponse` requires `id`, `environment`, `is_active`, `issued_at`, `revoked_at`, `issued_by`, `token_value`; its `token_value` is string-or-null. `environment` references SkillTokenEnvironmentCode. Token operation policy belongs to the other lane; this DTO alone does not establish issuance timing, access/redaction behavior or safe display/storage policy.

### API-R2-STATUS-03 — resolved status payload is a card plus issuance field

I is absent in r1. In r2 all 28 properties in S compare exactly equal to their counterparts in I; I additionally has:

- **I**`/properties/issued_token` = `{"anyOf":[{"$ref":"#/components/schemas/IssuedSkillTokenResponse"},{"type":"null"}]}`.
- **I**`/required/28` = `"issued_token"`; its required list is S's list followed by that member.

Thus status success now structurally requires both new fields: `tokens` and `issued_token`. Required does not mean non-null issuance: `issued_token: null` is allowed. Its non-null branch references IssuedSkillTokenResponse, whose `/properties/token_value` is `{"type":"string","title":"Token Value"}` (unlike the nullable value in SkillTokenResponse). No source token values were accessed. Do not infer that every transition issues a token, that a particular approved edge must issue one, or that replay returns/redacts the same token: OP prose did not gain those semantics.

### API-R2-STATUS-04 — unchanged command semantics, explicitly verified

Every OP member other than the response reference in STATUS-01 compares equal, including `/description`, `/parameters`, `/requestBody`, `/security`, `/operationId`, `/responses/422` and `/x-success-message`. All pre-existing referenced schema definitions other than S compare equal, including ChangeSkillStatusRequest, SkillStatus, SkillCheckResponse and HTTPValidationError.

Exact unchanged OP `/description` excerpts:

- `Ответ - карточка навыка с \`checks\`.` — still true, but no longer a complete account of the response fields.
- `Переход \`draft -> checking\` и возвраты \`review -> draft\`, \`whitelist -> review\` проверок не требуют` — no new frontend transitions authorized.
- `При отказе статус, версия и история статусов не меняются, а пересчитанные результаты сохраняются` — not whole-card rollback.
- `ждёт своей очереди не дольше 10 секунд. Переходы в \`draft\`, \`checking\` и \`disabled\` очереди не ждут.` — not dedicated-toggle bypass proof.
- `409 (SKILL_CHECKS_BLOCKED)`, `409 (VERSION_CONFLICT)`, `409 (PHRASE_REGISTRY_BUSY)`, `409 (IDEMPOTENCY_KEY_REUSED)` remain prose mappings; explicit responses remain only 200/422.

Request still references ChangeSkillStatusRequest, requiring status and integer expected_version ≥1, optional nullable reason, plus required UUID Idempotency-Key and UUIDv7 path ID. Checks still have no minimum count/all-five structural guarantee; training/autotest remain non-null unconstrained strings; ETA/note required-nullable strings with no ETA format. No new history array or current-phrase revision binding appears. Prose still calls for recalculating all five checks on applicable forward transitions, missing results do not pass, and semantic-conflict warnings do not block. Nothing adds error priority, exactly-once delivery, replay retention, automatic POST retry or distributed audit atomicity.

## Architecture / reference reachability only

Tracing `$ref` recursively from operations gives these consumers of S:

| Consumer | r1 | r2 / bounded impact |
|---|---|---|
| GET `/api/control/api/skills/v1/skills/{skill_id}` | reaches S | reaches S; required tokens added transitively despite unchanged operation text |
| PUT same path | reaches S | same transitive change |
| PATCH same path | reaches S | same transitive change |
| POST same path + `/status` | reaches S through old envelope | no longer references S; reaches I with identical card properties plus issued_token |
| POST same path + `/tokens/{environment}/revoke` | absent | reaches S; linkage only, token lane owns semantics |

The issuance response duplicates the card structure rather than referencing S by inheritance; comparing properties is necessary to avoid falsely concluding that status lost its checks/status/version fields. Existing operation equality is not sufficient to claim unchanged resolved DTOs for GET/PUT/PATCH.

Accepted implementation evidence (not re-inspected code) identifies shared `app/entities/skill/api/skill-details-client.ts` and `app/entities/skill/model/use-change-skill-status-mutation.ts` as the status-validation/cache seam used by lifecycle, separate review and bulk rollout. IMPL909-10 reports a loose object validator and IMPL909-06 reports committing the returned DTO. Therefore the new fields warrant a separately scoped response-validation/cache-retention review; neither a guaranteed break nor safe token handling is established by old tests. No source-callsite or runtime audit was performed here.

## Targeted prior-claim disposition

“Stale-for-current” below means only reuse against r2 needs qualification, not erasure of historically valid evidence.

| Evidence / decision | Specific disposition |
|---|---|
| SCENARIO-MOS-909 lines 41–44; R-SCENARIO-MOS-909 lines 67–75; D-018 | **Stale-for-current:** exact assertion that OP 200 resolves through TsamResponseSchema_SkillResponse_ to S. Replace only that linkage in a future authorized current-publication supplement with STATUS-01/03. **Historical-valid:** r1 chain. C05's available checks/process metadata and its no-readiness-activation boundary remain supported; fields survive in I. C01–C04/C06–C08 are not invalidated. |
| DELTA-MOS-1119-TESTPLAN line 39; R-DELTA-MOS-1119-TESTPLAN lines 61–65; D-017 | Same narrowly stale response-chain assertion. TP01's skill updated_at versus dictionary updated_at distinction remains valid. TP02/04/05/07 readiness prerequisites, optional reason, error-schema distinction and persisted-check exception are unchanged. TP03/08 storage/cohort/reader limitations are untouched. |
| MOS1119-TP06, report lines 75–79 and review line 51; D-017 | Historical test-plan replay/concurrency expectations remain valid as expectations, not proven behavior. **Current qualification needed:** response-equality questions must now explicitly include required tokens/nullable issued_token and the non-null issuance branch; r2 supplies no replay disclosure/redaction rule. No new contradiction or exactly-once guarantee inferred. |
| DELTA-MOS-1119 D01–D06 and R-DELTA-MOS-1119; D-016 | No claim invalidation by these deltas: storage seeds, nullable history fields, immutable-storage requests and reader/restoration questions are separate from new card fields. Historical unread-attachment qualifications remain dated evidence, not current collection inventory. |
| IMPL909-05/06/10; R-IMPL-MOS-909 lines 29–34; D-019 | Historical static client/cache/checks findings remain valid for inspected files and r1. **Not sufficient as current r2 compatibility evidence:** old fixture/DTO coverage says nothing about tokens/issued_token validation, preservation or handling. Checks gap is not repaired by r2. Do not silently turn old assertions into a claim of safe issuance-payload caching, or a proven deployed failure. |
| Corrected IMPL909-07; R-IMPL-MOS-909 lines 36–46; D-019 | Still valid under unchanged 409 SKILL_CHECKS_BLOCKED mapping: published readiness refusal enters the previously inspected conflict GET branch. No missing-readiness-reread remediation follows. Historical reviewer REVISE and parent-qualified acceptance remain distinct. |
| D-015 (decisions lines 57–67) | No invalidation of approved dedicated prod→disabled→prod UI, auth approval, reason/restoration questions, generic-disabled queue caution or status/history versus audit distinctions. This lane makes no whole-toggle-response or global history-inventory freshness claim. |
| D-018–D-021; R-WRITE-MOS-909-RESTORE lines 26–76; restoration proposal/design/tasks/spec | **Approval remains current and explicit:** only draft→checking, sandbox→review, whitelist→prod in generic lifecycle; four extra generic actions removed by future bounded remediation. r2 changes neither the request nor frontend authority. Two-file action-map/regression plan remains coherent; “no shared API/DTO changes needed” is valid for that narrow matrix correction, not blanket certification of r2 response handling. Keep separate review/toggle/shared transport boundaries and all six unchecked tasks. No automatic reopening, expansion, apply authority or API regeneration. |

## Start Here / bounded next work

Start with `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r2/content.json` at OP's 200 reference and I, alongside D-020 in `decisions.md:19–23`. This separates a real response-contract delta from unchanged product authority.

1. Parent/independent review should accept or qualify these stable delta IDs before reusing old exact-linkage claims for the new publication. Preserve originals and dated provenance.
2. Coordinate the issuance/replay/nullability questions with the token-delta lane using the linkage above; do not duplicate its endpoint/policy analysis.
3. If separately authorized, inspect generated types, validator behavior, actual cache consumers and synthetic fixtures for required tokens and issued_token across status/detail/update flows. Include null/empty and non-null issuance cases without real credentials or token values. Do not preselect logging, display, persistence or redaction policy from DTO shape.
4. Keep the D-020 corrective plan independent. No change to its matrix or transport/error boundaries is justified by this diff. Escalate an actual implementation scope conflict only if later evidence establishes one.

No tests, build, network/browser/MCP, business endpoint calls, credentials access, source/spec edits, sync/archive, nested delegation or global task closure occurred. Only this report was written. Index/worktree state is uninspected; no empty-index attestation. Deployment, token policy, runtime replay and implementation compatibility remain unverified.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Exact saved r1/r2 hashes matched; four stable delta IDs record pointers, resolved payload semantics, unchanged command clauses and claim-specific prior-evidence dispositions."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/API-R2-STATUS-DELTA.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local find/read/grep and numbered documentary reads","result":"passed","summary":"Inspected assigned evidence, D-015–D-021, targeted accepted reports/reviews and actual restoration plan."},
    {"command":"Read-only Python JSON comparison, SHA-256 and recursive reference traversal","result":"passed","summary":"Both assigned hashes and discovery hash matched; only existing status operation and namespaced SkillResponse changed; resolved card fields preserved."},
    {"command":"Tests/builds, network/browser/MCP, endpoint or credential operations","result":"not-run","summary":"Prohibited; no runtime validation claimed."}
  ],
  "validationOutput": ["r1 549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06", "r2 ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993", "Existing operation delta: success response reference only; existing DTO delta: required tokens only."],
  "residualRisks": ["Independent review and parent disposition pending.", "No deployment or current implementation compatibility proof; old static findings remain attributed.", "Issuance/replay disclosure semantics unresolved in unchanged status prose; token endpoint policy belongs to the other lane.", "Index/worktree state uninspected."],
  "diffSummary":"Designated findings report only; historical evidence, decisions and approved restoration artifacts preserved.",
  "reviewFindings":["No blocker to bounded documentary result; do not reuse old exact 200 response-chain claims as r2 facts."],
  "manualNotes":"D-020 explicit three-command approval and D-021 planning acceptance remain intact. No global task, implementation or feature closure follows; no source precedence selected."
}
```
