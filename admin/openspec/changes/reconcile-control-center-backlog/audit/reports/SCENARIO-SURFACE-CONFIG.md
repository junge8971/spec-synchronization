# SCENARIO-SURFACE-CONFIG — contract/planning handoff

## Result

The saved current publication **does define greeting placeholders, link actions and configuration limits**. The MOS-959 assertion that exact placeholder names are unavailable is no longer supported by this publication. This removes a factual documentation gap, **not the approved configurator deferral or a product approval gate**. MOS-1237's validation request is materially described by the new schema and operation text; neither its `Ready for test` status nor publication proves runtime correctness or acceptance.

No active configurator proposal/design/spec/tasks was found within the discovery boundaries below. Supervisor explicitly confirmed that no additional authoritative path is known, authorized recording missing planning coverage, and required preserving the main-spec deferral. No existing task checkbox can responsibly be marked complete.

# Code Context

## Files Retrieved

All paths are repository-relative; `A` below means `openspec/changes/reconcile-control-center-backlog/audit` (abbreviation only).

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-SURFACE-CONFIG.md` (lines 1–8): scope and inputs.
2. `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-API-001.md` (lines 1–120), `openspec/changes/reconcile-control-center-backlog/audit/reports/API-SCHEMA-001.md` (1–224), `openspec/changes/reconcile-control-center-backlog/audit/reports/API-OPS-001.md` (1–134), `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (1–194): routing leads, independently checked against scoped sources rather than treated as contract authority.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/metadata.json` (1–19), `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1, parsed; four operation descriptions and listed schemas): current publication.
4. `docs/api/contracts/openapi-2026-10-15.raw` (line 1, parsed; same scoped operations/schemas): historical comparison.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/metadata.json` (1–8), `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/content.json` (71-line JSON; only `/items/2` MOS-1237 and `/items/3` MOS-959 content inspected): task evidence.
6. `openspec/specs/surface-registration/spec.md` (1–78), `openspec/specs/surface-overview-connection/spec.md` (1–123), `openspec/specs/surface-skill-selection/spec.md` (1–145): adjacent baseline ownership and scenarios.
7. `openspec/specs/surface-lifecycle-publication/spec.md` (177–198): deferral only, not a lifecycle reconciliation.

Discovery: `find` on OpenSpec surface/config names and proposal paths; scoped text inspection of nonarchive/non-audit active Markdown for MOS-959, MOS-1237, configurator, placeholder and greeting terms; targeted main-spec search. There are no matching active configurator artifacts in that pass, consistent with LOCAL-001's 21-active-proposal inventory. Archive directory names appeared in path discovery but archive contents were not reviewed. This is not an assertion that no historical plan exists.

## Key Code / exact source locators

JSON pointers resolve against current `A/sources/api-live/r1/content.json`, line 1, unless stated otherwise. Define:

- `S = /paths/~1api~1control~1api~1surfaces~1v1~1surfaces`
- `C = /components/schemas`

Concatenate the suffixes below literally. All four inspected `/description` values are absent at the identical pointers in historical raw. Description publication must not be mistaken for a deployment change.

### Jira evidence

- Jira `/items/2/key = MOS-1237`, `/items/2/status = Ready for test`. `/items/2/description`: “не имеет валидации, в т.ч. пропускает пустое значение или пробел”; requested fields are greeting, greeting_fallback, suggestions and card title/subtitle/action.value. The task does not itself specify numeric bounds or conditional fallback behavior. `/items/2/attachments/0` names `mos-1237-test-plan.md`; only metadata was captured, **not its 19,543-byte body**.
- Jira `/items/3/key = MOS-959`, `/items/3/status = Backlog`. `/items/3/description`: “до пяти саджестов и до четырёх карточек”; “Действия карточек: ссылка, навык или сообщение”; “Предпросмотр имеет «Приветствие» и «Диалог», подстановки заполняются явно примером.” Its recorded problem is “в API не определены: точные имена плейсхолдеров приветствия в доступном текстовом экспорте контракта”. The new publication resolves that specific absence, not all preview/product decisions. The linked Confluence page remains uncollected.

### Configuration contract reconciliation

| Topic | Exact pointer and verified evidence | Planning consequence, not approval |
|---|---|---|
| Appearance | `C/UpdateSurfaceConfigurationRequest/properties/accent_color/pattern = ^#[0-9a-fA-F]{6}$`; `S~1{surface_id}~1configuration/put/description` lists shape `round/moderate/strict`, font `moscow_sans/system/golos_text`. These appearance refs/pattern already existed historically. | MOS-959 appearance controls have a published vocabulary; visual fidelity, preview rendering and design choices are not established by an API enum. |
| Greeting placeholders | `S~1{surface_id}~1configuration/put/description`: “Допустимы подстановки `{имя}`, `{отчество}` и `{время суток}`; другие слова в фигурных скобках и непарная скобка отклоняются.” | Retire the exact-name-unknown blocker as a current-publication claim; candidate cases: each allowed token, unknown token, unmatched brace. Do not infer grammar for every nesting/escaping/case variant. |
| Fallback | Same description: “из подстановок допустима только `{время суток}`”; “Непусто, если в `greeting` есть `{имя}` или `{отчество}`, иначе может быть пустой строкой.” `C/UpdateSurfaceConfigurationRequest/required` includes greeting_fallback; its maxLength is 500 with no minLength. | Missing field is not empty string. MOS-1237's general concern about blanks cannot be converted into an unconditional nonempty fallback rule. Desired business behavior and described conditional validation must remain distinct pending approval. |
| Limits | `C/UpdateSurfaceConfigurationRequest/properties/greeting/{minLength,maxLength}` = 1/500; `greeting_fallback/maxLength` = 500; `suggestions/maxItems` = 5, `suggestions/items/{minLength,maxLength}` = 1/100; `cards/maxItems` = 4. `C/SurfaceCardRequest/properties/title/{minLength,maxLength}` = 1/100, subtitle = 1/200. | These bounds were absent historically. Description additionally requires suggestions “без повторов”; schema has no uniqueItems assertion. Empty suggestions/cards lists remain legal. Candidate tests should cover boundary and over-bound values, blanks and duplicate suggestions, not equate optional collections with required content. |
| Card actions | `C/SurfaceCardActionType/enum` changed from `[message,skill]` to `[message,skill,link]`; `C/SurfaceCardActionRequest/properties/value/minLength` newly 1. Configuration description: message ≤500; skill UUID canonical lowercase; link “абсолютный адрес `https`” ≤2000, query allowed, fragment and credentials forbidden. | The former missing-link enum obstacle is removed. Type-dependent message/link limits and URL safety are description-only, not encoded by value's generic string schema. Link opening policy and preview execution behavior remain product/UI questions; do not execute card actions merely to preview them. |
| Replacement and normalization | `S~1{surface_id}~1configuration/put/description`: “Конфигурация заменяется целиком”; “Текстовые значения сохраняются без пробельных символов по краям”. Widget token and embed code unchanged. All seven top-level configuration fields remain required at `C/UpdateSurfaceConfigurationRequest/required`. | Candidate editor owns a complete configuration draft, not a patch of one appearance field; preserve untouched content. Readback should reflect normalized values without changing server embed text. Whitespace-only inputs require boundary coverage; exact normalization-versus-length ordering is not specified. |
| Preview | Jira `/items/3/description` defines Greeting/Dialog and explicit sample substitution; none of these four API descriptions specifies a preview service or sample persona/time mapping. | Preserve Jira UI intent separately from persistence evidence; do not invent an API, real resident identity, or approved sample defaults. No main configurator preview scenario was found. |

### Create/edit/detail/enabled-skills asymmetries

1. **Optional atomic create versus complete edit:** `C/CreateSurfaceRequest/properties/configuration/anyOf/0/$ref` points to UpdateSurfaceConfigurationRequest, with nullable second branch and no configuration entry in required. `S/post/description` says omitted configuration uses accent `#B3121B`, shape `round`, font `moscow_sans`, greeting and fallback “Здравствуйте! Чем помочь?”, empty suggestions/cards. It also says surface fields are preserved without trimming while configuration is trimmed. Do not apply config trimming to all registration strings. Baseline separately specifies null uses defaults; publication's prose explicitly describes omission, not every null edge.
2. **Skill card references are weaker on create:** `S/post/description`: “Навык карточки `skill` в `configuration` проверяется только по формату UUID: его подключение к поверхности и существование проверит первое сохранение конфигурации.” Conversely `S~1{surface_id}~1configuration/put/description` requires connected/not-deleted skill at save time. A create may therefore accept a card UUID that later config save rejects. Do not claim atomic creation validates the complete card linkage, or silently emulate stricter create behavior without approval.
3. **Validation precedence differs:** Create description says errors belong to the first failing stage: body → permission/team access → team existence → skills → responsible users → surface fields → domain occupancy. Config PUT says invalid body precedes surface lookup (422 rather than 404); invalid body plus invalid path also returns 422, whereas invalid UUID path with valid body returns 400 INVALID_ARGUMENT. “Все ошибки тела приходят одним ответом.” Config error paths include `/greeting`, `/suggestions/0`, `/cards/1/action/value`; missing field code REQUIRED, otherwise INVALID, envelope VALIDATION_ERROR. Create body configuration paths are `/configuration/...`; later business errors use FAILED. Do not collapse these into one universal first-error or all-errors rule; auth ordering beyond the described stages is not proven.
4. **Detail is persisted evidence, not freshness-by-timestamp:** `S~1{surface_id}/get/description`: “Конфигурация отдаётся в том виде, в каком сохранена.” Config/enabled-skill saves do not change updated_at; it represents creation or latest status change. A successful save with the same timestamp is not evidence of failure. Config PUT preserves token/embed code; avoid client reconstruction. No preview-readback fidelity is demonstrated by this claim.
5. **Stale card references survive disconnect:** `S~1{surface_id}~1enabled-skills/put/description`: whole-list replacement, empty list disconnects all; “Карточки конфигурации, которые ссылаются на отключённый навык, не перепроверяются.” Subsequent configuration save applies the connected/not-deleted check. Candidate scenario: disconnect referenced skill, read retained card, then explicitly edit/save configuration and receive field rejection. API does not authorize automatic card removal or blocking disconnection as a product choice.
6. **Documented defect, not desired acceptance:** Create and enabled-skills descriptions say duplicate skill_id “не проверяется и заканчивается ответом `500`.” Preserve distinct defect/error evidence; do not plan intentional duplicate submission, expect a guaranteed 422, or label that 500 desired business validation. Existing UI deduplication requirement remains appropriate. No runtime reproduction was attempted.

## Architecture / baseline scenario ownership

Configuration DTO is reused by optional create and standalone PUT; card-action enum also reaches detail through SurfaceConfigurationResponse → SurfaceCardResponse → SurfaceCardActionResponse. This allows new structural constraints to affect create, edit and detail interpretation without changing operation request/response references. Description-only rules must accompany schema evidence.

Relevant existing scenario/task locators (not assertions of implementation):

- `openspec/specs/surface-registration/spec.md:23–40`, **Creation supports an atomic optional configuration** → **Configuration is provided**, **Default configuration**, **Detail cannot be read after creation**. Preserve one POST, omitted/null defaults and GET retry without second POST. Add candidate normalization/card-reference asymmetry coverage here only after planning approval. Lines 42–59, **Rejections are distinct from unknown creation outcomes**, preserve input and reliable field mapping; new published error pointers do not turn an unknown response into proof of noncreation.
- `openspec/specs/surface-overview-connection/spec.md:9–45`, **Connection displays saved server values** / **Exact copy with truthful feedback**: token/embed invariance is compatible with exact server-text handling. Lines 56–78, **Read after registration** / **Incomplete response is not empty data**, and 101–123, **Failed refresh after successful save** / **Recovery and tab switching**: route saved trimmed values and unchanged timestamps without falsely reporting save failure. These existing scenarios concern overview/skill draft, not a completed configuration editor.
- `openspec/specs/surface-skill-selection/spec.md:71–83`, **Parameter ownership and draft preservation**, requires each selected skill once. Lines 128–145, **Registration and existing surface persistence** → **Edit and clear existing surface**, explicitly says enabled-skills save must not change appearance via configuration. Preserve this boundary when documenting stale references. The baseline's prod-only selection/minimum-one registration policy is not canceled by permissive backend descriptions; no product precedence decision is made here.
- **Approved deferral:** `openspec/specs/surface-lifecycle-publication/spec.md:179–192`, **MVP editing and deferred functionality boundaries** → **Configuration editor is not available** and **Draft remains a draft after saving skills**. Exact text: “Существующий контракт PUT configuration SHALL сохраняться для отдельного конфигуратора.” It forbids fake PUT/default payloads and hidden config saves. New publication does not activate this deferred UI scope. Other lifecycle and listing semantics are explicitly outside this item.
- **Active plan/tasks:** unavailable in the scoped discovery; no configurator proposal/design/spec/task number can be cited. Supervisor approved reporting this absence rather than inventing an artifact. Historical plans were not searched broadly.

## Minimal candidate planning deltas

1. Update backlog evidence for MOS-959: exact placeholders and link support are now published, while deferred activation still requires product approval. Record publication provenance and keep the unavailable Confluence/attachment evidence explicit. Do not mark the feature or MOS-1237 accepted.
2. If configurator scope is activated, give a new change explicit ownership of appearance/content/preview and complete-draft replacement. Candidate scenarios: allowed/invalid placeholders and conditional fallback; exact limits versus over-limit/whitespace values; duplicate suggestions; each action including unsafe URL; preservation of untouched config fields; server-trimmed readback; unchanged embed/token/timestamp. These are proposed scenario labels, not existing task IDs or approved requirements.
3. Add narrow cross-scenario handoff candidates to registration and skill selection: create-versus-save card validation; create `/configuration/...` versus edit field pointers; multi-error body precedence; retained card after disconnect and subsequent save rejection. Keep backend duplicate-500 defect distinct from prevention and recovery requirements. Do not introduce automatic card mutation or stricter create validation without a decision.
4. Preserve existing deferral, separate save/read failure handling and UI/backend distinctions. No lifecycle graph, listing behavior, publication readiness or implementation completion conclusion belongs to this report.

## Start Here

Open `openspec/specs/surface-lifecycle-publication/spec.md:179–192` first to preserve the approved boundary, then current configuration PUT description at `S~1{surface_id}~1configuration/put/description`. Together they explain why missing API evidence can be corrected without authorizing implementation.

## Validation, unknowns and residual risks

- Read-only Python parsed saved JSON and independently compared scoped historical/current schemas and four descriptions. SHA-256 of current API and Jira content matches each saved metadata value. Capture times are API `2026-10-16T11:13:29.451Z`, Jira `2026-10-16T11:23:51.742Z`; they are saved provenance, not new observations. Jira update/status does not demonstrate QA completion.
- No source implementation audit, backend invocation, network/MCP/browser, tests, generation, source/spec/archive edits or staging commands occurred. Only this report was written. No infrastructure failure occurred; missing active-plan ambiguity was resolved by supervisor.
- Confluence, comments, attachment bodies and Jira custom fields remain uncollected. In particular MOS-1237's test plan could refine intended edges. No final completeness claim is possible.
- Unresolved: preview sample values and safe action behavior; placeholder escaping/nesting/case and time-of-day semantics; duplicate comparison case/normalization rules; exact Unicode length and trim/validation ordering; desired remediation of stale cards and create/edit validation asymmetry; observed error-envelope fidelity. Published docs do not settle these through inference.
- No deployment readiness, backend availability, product precedence or release acceptance is inferred. Existing approved deferrals remain intact.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Rechecked four current/historical operation descriptions and configurator schemas against MOS-1237/MOS-959; documented exact pointers, baseline scenario locators, missing active planning coverage, preserved deferral and candidate deltas."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-SURFACE-CONFIG.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python scoped JSON/schema/description inspection and active Markdown discovery","result":"passed","summary":"Current constraints and four newly published descriptions independently inspected; only the two authorized Jira task contents reviewed."},
    {"command":"Read-only Python SHA-256 and source/scenario locator inspection","result":"passed","summary":"API and Jira content match saved metadata digests; exact main-spec scenario lines located."},
    {"command":"tests / generation / network / browser","result":"not-run","summary":"Prohibited by task."}
  ],
  "validationOutput": ["Placeholder names, conditional fallback, link constraints, whole replacement, validation precedence and stale-card asymmetry confirmed in saved publication.","No active configurator plan/task located; supervisor authorized explicit absence finding and preservation of main-spec deferral."],
  "residualRisks": ["Publication is not runtime or deployment evidence.","Confluence/comments/attachment bodies remain uncollected; no completeness claim.","Preview policy, edge normalization semantics and product resolution of create/edit and stale-card behavior remain open."],
  "noStagedFiles": true,
  "diffSummary": "Only runtime-bound report written; no application/spec/generated/archive changes.",
  "reviewFindings": ["MOS-959 exact-placeholder documentation blocker is outdated against current publication, not an approval to implement.","Missing active configurator planning coverage and approved deferral remain explicit.","Duplicate-skill 500 is documented backend defect behavior, not desired business validation."],
  "manualNotes": "Supervisor resolved absent-active-plan ambiguity; no alternative input was invented. noStagedFiles means this worker performed no staging; pre-existing index state was not inspected. Analysis stayed within configuration handoff scope."
}
```
