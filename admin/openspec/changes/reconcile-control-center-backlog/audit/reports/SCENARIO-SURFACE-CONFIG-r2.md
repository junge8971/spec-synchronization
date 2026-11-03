# SCENARIO-SURFACE-CONFIG-r2 — recovered configurator contract handoff

## Result and recovery disposition

Recovery of failed run `f4bd5cdc-8f3d-4339-a3b1-f49209398a4c`, restricted to the surface configurator. The prior report exists but remains **unaccepted recovery evidence**; it was read, not changed. Its SHA-256 on inspection was `65da3c4be69be5d1df7596749e81619a6b2544545a6130927f7df99365fac2dc`.

Independently checked material contract claims against the saved API JSON, historical raw JSON, the two authorized Jira records and main specs. The prior report's central findings hold: **exact greeting placeholders, link actions and configuration bounds are now published**. The MOS-959 exact-placeholder documentation blocker is factually outdated against this publication. This does **not** approve the configurator, establish backend deployment, complete MOS-1237, or supersede the main-spec deferral.

No active configurator planning artifact was found within the bounded discovery below. This report adds explicit candidate artifact ownership and distinguishes existing scenario locators from proposed scenarios/tasks. No existing checkbox or work-item status was changed. Independent review is still required before planning publication.

# Code Context

## Files Retrieved

Paths are repository-relative. `A` below expands exactly to `openspec/changes/reconcile-control-center-backlog/audit`.

1. `A/work-items/SCENARIO-SURFACE-CONFIG.md` (lines 1–8) and `A/reports/SCENARIO-SURFACE-CONFIG.md` (entire report): recovery instructions and unaccepted claims to verify.
2. `A/reviews/R-API-001.md` (lines 1–120), `A/reports/API-SCHEMA-001.md` (1–224), `A/reports/API-OPS-001.md` (1–134), `A/reports/LOCAL-001.md` (1–194): supplied routing/context, not substitutes for primary evidence. Unrelated scenario claims were not re-audited.
3. `A/sources/api-live/r1/metadata.json` (1–19) and `A/sources/api-live/r1/content.json` (line 1, parsed): all four scoped operation descriptions, configuration/card/create schemas, appearance enums and detail configuration reference.
4. `docs/api/contracts/openapi-2026-10-15.raw` (line 1, parsed): historical values for those descriptions, configuration/card constraints and appearance enums. Local aggregate/generated types were not audited.
5. `A/sources/jira-api-delta-scenarios/r1/metadata.json` (1–8), `A/sources/jira-api-delta-scenarios/r1/content.json` (43–69; parsed `/items/2` and `/items/3` only for semantic inspection): MOS-1237 and MOS-959. No other task was analyzed.
6. `openspec/specs/surface-registration/spec.md` (1–78): atomic optional configuration, defaults and creation recovery.
7. `openspec/specs/surface-overview-connection/spec.md` (1–123): saved server values and read/save separation; no separate lifecycle assessment.
8. `openspec/specs/surface-skill-selection/spec.md` (65–145): deduplication, draft preservation, skill persistence boundaries.
9. `openspec/specs/surface-lifecycle-publication/spec.md` (177–198): approved configurator deferral only.

### Discovery boundaries

Used `find` for `**/*surface*`, `**/*config*` under `openspec` and `**/proposal.md` under `openspec/changes`. Then searched 85 Markdown files in nonarchive, non-audit active changes for case-insensitive `MOS-959|MOS-1237|configurator|конфигуратор|placeholder|плейсхолдер|greeting`: **zero matches**, with 21 active proposals enumerated. No active configurator proposal/design/spec/tasks was found. Archive names appeared during discovery; archive contents were not read. This does not prove absence of historical plans or differently worded references elsewhere. Supervisor's task clarification confirms no known missing active-plan input and permits reporting this bounded absence.

## Key Code / primary evidence

All API pointers below resolve against `A/sources/api-live/r1/content.json`, line 1. Prefixes are literal RFC 6901 pointer abbreviations:

- `S` = `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces`
- `C` = `/components/schemas`
- `CREATE` = `S/post/description`
- `SAVE` = `S~1{surface_id}~1configuration/put/description`
- `DETAIL` = `S~1{surface_id}/get/description`
- `SKILLS` = `S~1{surface_id}~1enabled-skills/put/description`

All four description properties are absent at identical pointers in historical raw. This is newly published text, not evidence of newly deployed behavior. Quotes below retain wording but may collapse source line breaks.

### Jira task reconciliation

- `A/sources/jira-api-delta-scenarios/r1/content.json#/items/2`: key MOS-1237, status `Ready for test`. `/description` reports parameters that “не имеет валидации, в т.ч. пропускает пустое значение или пробел” and names greeting, greeting_fallback, suggestions, card title/subtitle/action.value. This task does not itself define numeric limits or unconditional nonempty fallback. `/attachments/0` identifies `mos-1237-test-plan.md`, size 19543: metadata only, body uncollected. Current publication materially describes the requested validation, but neither status nor documentation establishes tested correctness.
- Same source `#/items/3`: key MOS-959, status `Backlog`. `/description`: “до пяти саджестов и до четырёх карточек”; “Действия карточек: ссылка, навык или сообщение”; “Предпросмотр имеет «Приветствие» и «Диалог», подстановки заполняются явно примером.” The recorded issue “точные имена плейсхолдеров приветствия” being undefined is resolved as a publication gap by SAVE below. The linked Confluence page, comments and attachments remain uncollected; no complete product-spec claim follows.

### Constraints, appearance and preview

| Topic | Independently verified pointer/value or wording | Bounded consequence |
|---|---|---|
| Appearance | `C/UpdateSurfaceConfigurationRequest/properties/accent_color/pattern` = `^#[0-9a-fA-F]{6}$`; `C/SurfaceConfigurationShape/enum` = `[round,moderate,strict]`; `C/SurfaceConfigurationFont/enum` = `[moscow_sans,system,golos_text]`. Pattern, refs and enums unchanged historically. | Published vocabulary, not a new appearance API or proof of design/preview fidelity. |
| Greeting | `C/UpdateSurfaceConfigurationRequest/properties/greeting/minLength` = 1, `/maxLength` = 500, newly added. SAVE: “Допустимы подстановки `{имя}`, `{отчество}` и `{время суток}`”; other words in braces and unmatched braces rejected. | Exact-name blocker can be retired as a current-publication claim. Escaping, nesting, casing and complete parser grammar remain unspecified. |
| Fallback | `C/UpdateSurfaceConfigurationRequest/required` includes `greeting_fallback`; its `/properties/greeting_fallback/maxLength` newly 500, no minLength. SAVE: only `{время суток}` allowed; nonempty if greeting includes `{имя}` or `{отчество}`, otherwise may be empty. | Missing is not empty. Do not convert MOS-1237's broad blank-input concern into unconditional nonempty fallback validation. Resolve desired behavior explicitly if product expectations differ. |
| Suggestions/cards | `C/UpdateSurfaceConfigurationRequest/properties/suggestions/maxItems` newly 5; `/items/minLength` 1 and `/items/maxLength` 100; `/properties/cards/maxItems` newly 4. SAVE: suggestions “без повторов”; both lists may be empty. No schema uniqueItems. | Candidate edges: empty list versus blank item, exact bound/over-bound, duplicates. Duplicate equality/normalization rules not stated. |
| Card fields | `C/SurfaceCardRequest/properties/title/{minLength,maxLength}` newly 1/100; subtitle newly 1/200. `/required` includes title/subtitle/action; accent default false. | Blank title/subtitle must be treated separately from optional accent. Numeric bounds alone do not establish whitespace semantics. |
| Actions | `C/SurfaceCardActionType/enum`: historical `[message,skill]`, current `[message,skill,link]`; `C/SurfaceCardActionRequest/properties/value/minLength` newly 1. SAVE: message ≤500; skill UUID stored canonical lowercase; link absolute HTTPS ≤2000, query allowed, fragment and credentials forbidden. | Prior missing-link schema obstacle removed. Type-dependent bounds/URL safety are prose rules, not generic value schema constraints. Link opening and preview execution policy still need product/design ownership. |
| Replacement/trim | SAVE: “Конфигурация заменяется целиком”; “Текстовые значения сохраняются без пробельных символов по краям”. All seven top-level fields remain required in `C/UpdateSurfaceConfigurationRequest/required`. | Complete draft, not appearance-only patch. Preserve untouched fields and reflect saved normalization; trim-versus-length order and Unicode counting not established. |
| Preview | MOS-959 `/items/3/description` requires Greeting/Dialog with explicit example substitution. None of the four descriptions defines preview API, persona defaults or time-of-day mapping. | Candidate local preview requirement only. Do not invent resident identity, sample defaults, real action execution or a service endpoint. |

### Create/save/detail/enabled-skills distinctions

1. **Optional create versus required complete save.** `C/CreateSurfaceRequest/properties/configuration/anyOf/0/$ref` points to `#/components/schemas/UpdateSurfaceConfigurationRequest`; branch 1 is null; configuration is absent from `/required`. CREATE documents defaults: accent `#B3121B`, shape `round`, font `moscow_sans`, greeting and fallback “Здравствуйте! Чем помочь?”, empty suggestions/cards. Its prose describes absence; main baseline separately states omission **or null** uses defaults. Do not claim a runtime null experiment occurred. CREATE also says surface fields remain untrimmed while configuration values lose edge spaces; do not generalize configuration normalization to registration strings.
2. **Create card linkage is weaker.** CREATE: “Навык карточки `skill` в `configuration` проверяется только по формату UUID”; existence and connection checked at first configuration save. SAVE requires skill connected to the surface and not deleted at save time. A UUID may pass create and fail later save. Atomic creation does not imply complete reference integrity; silently tightening create policy is not authorized.
3. **Validation precedence and field mapping.** CREATE describes first failing stage: body → permission/team access → team existence → skills → responsible → surface fields → domain occupancy. Configuration body errors use `/configuration/...`, `422 VALIDATION_ERROR`; later business errors use `FAILED`. SAVE checks body before surface lookup: invalid body for missing surface gives 422 rather than 404. Invalid path UUID with valid body gives 400 INVALID_ARGUMENT at `/surface_id`; both invalid give 422. “Все ошибки тела приходят одним ответом.” SAVE uses `/greeting`, `/suggestions/0`, `/cards/1/action/value`, missing field REQUIRED, otherwise INVALID, envelope VALIDATION_ERROR. Do not impose one universal first-error/all-errors policy or infer authentication ordering beyond the published wording. SKILLS additionally describes invalid skills checked before surface lookup (422 rather than 404); this is relevant only to the disconnect handoff here.
4. **Persisted readback and unchanged timestamps.** DETAIL: “Конфигурация отдаётся в том виде, в каком сохранена.” SAVE preserves widget token and `connection.embed_code`; SAVE and DETAIL say updated_at represents creation/latest status change, not config save. SKILLS likewise does not change updated_at. Same timestamp is not save failure. Preserve server embed text, not reconstructed client text. This says nothing about proven preview fidelity.
5. **Stale card references.** SKILLS replaces the entire skill list; empty disconnects all. “Карточки конфигурации, которые ссылаются на отключённый навык, не перепроверяются.” SAVE subsequently checks connected/not-deleted reference. Candidate sequence: disconnect referenced skill → read retained card → explicit configuration save receives field rejection. Retention is the described implication, not a runtime observation. Automatic card removal or blocking disconnect would require an explicit product decision.
6. **Documented backend defect versus desired validation.** CREATE and SKILLS say repeated skill_id is unchecked and ends in 500. Preserve this as documented defect behavior, not desired acceptance or a promise of 422. Existing UI deduplication remains appropriate. No duplicate request was submitted or backend issue acceptance established.

## Architecture and existing scenario ownership

Create optionally embeds the same request DTO used for standalone complete configuration PUT. Cards use `UpdateSurfaceConfigurationRequest → SurfaceCardRequest → SurfaceCardActionRequest → SurfaceCardActionType`. Detail uses `SurfaceDetailResponse/properties/configuration/$ref → SurfaceConfigurationResponse/properties/cards/items/$ref → SurfaceCardResponse/properties/action/$ref → SurfaceCardActionResponse/properties/type/$ref → SurfaceCardActionType`, each component under `C`. Shared enum expansion affects detail interpretation, but request length limits are not automatically response constraints. Description-only validation must travel alongside schema routing.

Existing requirements/scenarios are locators, not implementation claims:

| Existing artifact and exact locator | Ownership to preserve |
|---|---|
| `openspec/specs/surface-registration/spec.md:23–40`, **Creation supports an atomic optional configuration** / **Configuration is provided**, **Default configuration**, **Detail cannot be read after creation** | One POST; omit/null backend defaults; retain ID and retry GET, not POST. Candidate create/save asymmetry coverage belongs in a future delta here. |
| Same file `42–59`, **Rejections are distinct from unknown creation outcomes** / **Lost response** | Reliable field errors preserve input; unknown response does not prove noncreation. New error prose does not authorize blind replay. |
| `openspec/specs/surface-overview-connection/spec.md:9–45`, **Connection displays saved server values**, **Exact copy with truthful feedback**; `56–78`, **Read after registration**, **Incomplete response is not empty data** | Saved values and exact server embed text; missing data not synthesized. |
| Same file `101–123`, **Read failures preserve saved information and drafts** / **Failed refresh after successful save**, **Recovery and tab switching** | Current scenarios concern skill draft/save, not an implemented configuration editor. Future editor should separately own its successful-write/failed-read scenario rather than silently broadening the existing requirement. |
| `openspec/specs/surface-skill-selection/spec.md:71–83`, **Parameter ownership and draft preservation**; `128–145`, **Registration and existing surface persistence** / **Edit and clear existing surface**, **Save rejected** | Each skill once; enabled-skills save never writes appearance/configuration. Existing prod selection and minimum-one registration policies are not canceled by permissive backend prose. |
| `openspec/specs/surface-lifecycle-publication/spec.md:179–192`, **MVP editing and deferred functionality boundaries** / **Configuration editor is not available**, **Draft remains a draft after saving skills** | “Существующий контракт PUT configuration SHALL сохраняться для отдельного конфигуратора.” No fake/default configuration PUT or hidden save to force a status. Deferral remains intact. No lifecycle/listing reconciliation performed. |

## Minimal proposed planning deltas and explicit artifact ownership

**All paths below are candidates only, not existing/approved plans.** No task IDs can be cited for an active configurator change because none was found. Scenario names in this section are proposed labels, not completed tasks.

1. **Evidence correction now:** this managing audit's recovered report owns the publication-gap correction for MOS-959 and MOS-1237. Supervisor/independent review owns acceptance and any later planning publication. Do not edit Jira status, checkboxes, main specs or archive from this result.
2. **If product explicitly activates MOS-959:** candidate new change root `openspec/changes/mos-959-surface-configurator/`:
   - `proposal.md`: activation request, appearance/content/preview scope, dependencies and explicit treatment of current deferral. API publication is evidence, not approval.
   - `design.md`: complete-draft replacement, normalization/readback, placeholder parser boundaries, preview examples/action safety, error mapping and stale-reference handling decisions.
   - `specs/surface-configurator/spec.md`: proposed owning capability for appearance/content/preview. Candidate scenarios: Allowed and rejected placeholders; Conditional fallback; Empty collections versus blank entries; Exact and exceeded limits; Duplicate suggestions; Safe link actions; Complete save preserves untouched fields; Trimmed readback with unchanged timestamp; Successful write followed by failed read; Stale card rejected on explicit save. Missing Unicode/escaping/sample decisions stay open, not invented SHALLs.
   - `tasks.md`: after scope approval, separate contract evidence/decision closure, scenario specifications, UI/API integration and permitted unit/component verification. No checkbox completion inferred from this audit; no tests run here.
3. **Narrow cross-capability delta ownership within that candidate change:**
   - `specs/surface-registration/spec.md`: extend the existing atomic optional configuration scenarios for create-only UUID validation, optional/null defaults and `/configuration/...` mapping. Preserve one POST and unknown-outcome protection.
   - `specs/surface-skill-selection/spec.md`: record disconnect/reference handoff beside **Edit and clear existing surface**, without hidden configuration writes or automatic card mutation. Keep duplicate-500 defect separate from desired deduplication behavior.
   - `specs/surface-overview-connection/spec.md`: only if needed, clarify saved readback/unchanged timestamp and exact embed invariance; new editor draft/save handling stays with the new configurator capability.
   - `specs/surface-lifecycle-publication/spec.md`: any future change to **MVP editing and deferred functionality boundaries** requires explicit activation approval and a narrowly reviewed delta. Until then retain the current main spec unchanged; no wider lifecycle redesign belongs here.

## Start Here

Open `openspec/specs/surface-lifecycle-publication/spec.md:179–192` to preserve the approved boundary, then SAVE in the saved API JSON. These distinguish a resolved documentation blocker from authorization to build.

## Independent verification, limitations and residual risks

- Independently read the complete four scoped descriptions; compared historical/current request constraints, action enum, appearance enums and relevant reference edges; checked the two Jira records and baseline scenario text. Prior report's material claims were supported. Clarifications added here: explicit candidate artifact paths/owners, request-versus-response constraint distinction, and no automatic extension of skill-save recovery scenarios to an editor.
- Saved API bytes hash to `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`; saved Jira bytes hash to `b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed`, matching their metadata. Capture timestamps are respectively `2026-10-16T11:13:29.451Z` and `2026-10-16T11:23:51.742Z`: saved provenance, not new retrievals.
- Confluence, comments, attachment bodies and custom fields uncollected. MOS-1237 test-plan content could refine intended boundaries. No final completeness claim.
- Open decisions: preview samples and safe action behavior; exact placeholder escaping/nesting/case/time semantics; Unicode length, trim-versus-validation order and duplicate comparison; desired remediation of stale references and create/edit asymmetry; observed error-envelope fidelity. Do not infer these from schema publication.
- No implementation audit, backend request, deployment/runtime validation, network/MCP/browser, tests, generation, source/spec/main/archive edits, staging or work-item edits. Only this bound report was written. No infrastructure failure occurred in this recovery. No independent claim about pre-existing git index state.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Recovered the bounded surface-configurator handoff by checking primary saved API/Jira/main-spec sources; exact pointers, existing scenario locators, candidate artifact ownership and residual risks recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-SURFACE-CONFIG-r2.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python scoped API historical/current description/schema and selected Jira inspection with SHA-256","result":"passed","summary":"Four descriptions and configuration constraints independently verified; API and Jira hashes match metadata; prior-report fingerprint recorded."},
    {"command":"find path discovery and read-only Python nonarchive/non-audit active Markdown search","result":"passed","summary":"21 active proposals; 85 active Markdown files searched; zero configurator/Jira-key/greeting-term matches; appearance enums and detail configuration reference checked."},
    {"command":"tests / generation / network / MCP / browser","result":"not-run","summary":"Prohibited by bounded recovery task."}
  ],
  "validationOutput": ["Exact placeholders and link support published; MOS-959 documentation absence is outdated, not product approval.","Main-spec deferral preserved; no active configurator task completion asserted.","Prior report preserved as unaccepted evidence; only r2 output authorized."],
  "residualRisks": ["Publication does not prove deployment, runtime correctness or product acceptance.","Confluence/comments/attachment bodies uncollected; no completeness claim.","Discovery bounded to named paths/terms; preview and normalization edge decisions remain open."],
  "diffSummary": "Only recovered report written; no source/spec/archive/work-item changes.",
  "reviewFindings": ["Independent review required before planning publication.","Duplicate-skill 500 remains documented defect behavior, not desired validation.","Candidate new planning ownership is explicitly separated from approval."],
  "manualNotes": "Prior report was not accepted by its existence or reused as authority. Primary-source checks support its central claims; r2 adds concrete candidate ownership and narrower scenario/response distinctions. No staging commands or repository-index assertions."
}
```
