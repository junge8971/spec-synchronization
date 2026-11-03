# Code Context

## Result and scope

REQ-G2-MOS-1254: bounded requirements extraction for question/option editing inside the survey-card draft. All seven saved Jira acceptance bullets are mapped below. No API, product-spec, implementation or delivery audit; no independent R/A/S/I completeness claim. Parent acceptance remains subject to independent review. Jira Backlog is identity context, not acceptance evidence.

## Files Retrieved

Paths below use `C = openspec/changes/reconcile-control-center-backlog` and `A = C/audit`; these are literal repository-relative path expansions.

1. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`: complete governing process inputs, not business-spec audit.
2. `A/work-items/G2-FEEDBACK-REQUIREMENTS-WAVE.md:1–31`: common contract and assignment; neighboring assignment headings were incidentally returned, not executed.
3. `A/decisions.md:1–13`: D-063 complete and next heading only. D063 is the work-item spelling of D-063.
4. `A/reports/JIRA-MOS-1246.md:1–56`: complete accepted membership report; MOS-1254 belongs to the observed MOS-1246 module. No new hierarchy inference.
5. `A/reports/G2-JIRA-MEMBER-JOINS.md:1–220`, plus scoped search excerpts at 277–286: actual read coverage, including the MOS-1254 unresolved scenario join and known adjacent boundaries. Remaining report not read; no repeat census. Existing MOS-1251/MOS-1258 surface-binding/conditions findings are not re-audited here.
6. `A/sources/jira-feedback/r1/metadata.json:1–11` and `content.json:50–58` only: complete assigned issue `/items/5`, including its full description and all seven embedded AC bullets. Other issue descriptions not read.
7. `A/sources/wiki-247734813/r1/metadata.json:1–11`, `content.json:1–136`: complete saved flattened text and link index returned by reads 1–100 and 101–136. Analysis limited to related clauses enumerated below; other text incidentally returned because `/text` is one physical line. No attachment, link target, original PDF, omitted comment, or executable prototype read/executed.

### Provenance and hash verification

- Jira source `jira-feedback`, revision 1, retrieved `2026-10-16T11:17:16.813Z`; issue updated `2026-10-12T20:49:05.464+0800`. Primary issue URL: `https://task.mos-team.ru/browse/MOS-1254`; packet metadata URL identifies the MOS-1246 grouping. Selected REST fields only; comments, attachments and custom acceptance fields omitted.
- Wiki source `wiki-247734813`, revision r1, page version 11, version time `2026-10-12T17:21:31.204+08:00`, retrieved `2026-10-16T11:17:53.564Z`; URL `https://wiki.mos-team.ru/spaces/KR/pages/247734813/`. `body.view` textContent/links extraction, not structurally complete HTML/tables.
- Actual `sha256sum` for Jira content: `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685`; matches metadata and assignment.
- Actual `sha256sum` for wiki content: `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7`; matches metadata. Hashes certify saved extraction bytes, not live freshness or original pages.

## Key Code — primary requirement locators, not code

`J` = `A/sources/jira-feedback/r1/content.json#/items/5/description` (physical line 57). `J.D1` is first description paragraph (“Добавить в draft карточки…”); `J.D2` starts “API: questions…”; `J.D3` starts “Зависимости…”. `J.AC1`–`J.AC7` are the seven `#` bullets under `h3. Критерии приёмки`, counted in saved order. These are exact description locators, not omitted custom AC fields.

`W` = `A/sources/wiki-247734813/r1/content.json#/text` (physical line 8). Because headings repeat, use the following section-plus-anchor locators:

| Alias | Exact section / anchor within W |
|---|---|
| W.F | Prototype `4.3. Вкладка «Форма»`, from “Две колонки” through the preview buttons, ending before `4.4. Вкладка «Правила показа»` |
| W.DND | Prototype `6.3. Drag-and-drop`, from “Реализован для” through “Сортировка обновляется автоматически после перетаскивания.” |
| W.TOAST | Prototype `6.1. Тост-уведомления` |
| W.MAP | Prototype `7. Соответствие модели данных`, entries `fb_questiondraft.questions[]` and `fb_question_optiondraft.questions[].options[]` |
| W.LIMIT | Prototype `8. Ограничения и не реализовано`, especially answer saving, in-memory/server-validation limits |
| W.FLOW | Prototype `9. Типичный сценарий работы`, “Вкладка «Форма»: отредактировать вопросы…” |
| W.Q | After `Таблицы1. Модель данных…`, section `3.2. fb_question`, ending before `3.3. fb_question_option` |
| W.O | Tables section `3.3. fb_question_option`, ending before `3.4. fb_display_rule` |
| W.RESPONSE | Tables sections `3.5. fb_response` and `3.6. fb_response_answer` |
| W.LOOKUP | Tables `5.2. Структура справочника`; `5.3. Состав справочников и значения`, the seven consecutive `fb_question_types` entries |

### Explicit Jira requirements

IDs have prefix `REQ-G2-MOS-1254-`. Actor for editing rows: administrative card editor; no role/permission policy is specified by this issue. Serialization/error rows describe behavior of that editor during parent-card saving/reloading, not a new transport owner. Verification column lists future checks, **none executed**. Unless stated, exact error copy, timing and UI mechanism are unspecified.

| ID | Trigger → expected behavior / boundary | Primary locator | Verification need |
|---|---|---|---|
| 01 | Edit questions/options → changes belong to the survey-card draft, including order and requiredness. No independent question editor persistence ownership. | J.D1; W.MAP | Draft edits remain parent-card state. |
| 02 | Parent save → questions belong to POST/PATCH `/api/control/api/v1/managed-resources/feedback/surveys`; no separate questions API is created. This records Jira's requirement only, not API verification. | J.D2–D3 | Later transport lane checks parent ownership. |
| 03 | Resolve question types → use `/catalogs/lookups/feedback`; dependencies explicitly MOS-1249 and MOS-1251 editor foundation. | J.D2–D3 | Later owning lanes confirm supplied catalog/editor seam. |
| 04 | Choose supported type → support stars, tags, text, boolean, scale, nps, emoji. | J.AC1; W.LOOKUP | Each of seven codes editable without substitution. |
| 05 | Edit question title → `title` editable. | J.AC1; W.Q | Change title in draft. |
| 06 | Edit question type → `type_code` editable, subject to 18, 25–28 below. | J.AC1 | Allowed type change. |
| 07 | Edit mandatory flag → `required` editable. | J.AC1; W.F, W.Q | Toggle both ways. |
| 08 | Add question → question can be added. | J.AC1 | New element plus count boundary. |
| 09 | Delete question → question can be removed. | J.AC1 | Removed element absent from final array. |
| 10 | Add/edit collection → at most 100 questions. Minimum question count not stated. | J.AC2 | 100 accepted, 101 invalid; no invented minimum. |
| 11 | Add/edit options → at most 100 options per question. | J.AC2 | 100/101 boundary per question. |
| 12 | Validate question → title length 1–500. Trimming/Unicode counting not specified. | J.AC2; W.Q | Lengths 0/1/500/501; normalization question retained. |
| 13 | Validate option → `option.text` length 1–255. | J.AC2; W.O | Lengths 0/1/255/256. |
| 14 | Validate tags question → at least one option. | J.AC2 | Empty tags options rejected; one valid option accepted. |
| 15 | Serialize other types → nonempty options are not sent. Does not choose omitted versus empty representation. Unknown-type corner case remains unresolved. | J.AC2 | Inspect non-tags final representation in later lane. |
| 16 | Reorder questions → drag-and-drop supported. | J.AC3; W.DND | Move first/middle/last without loss. |
| 17 | Reorder options → drag-and-drop supported. | J.AC3; W.DND | Move options without loss. |
| 18 | Change type that loses options → require confirmation. Cancellation, restoration and exact destructive transition set not specified. | J.AC3 | Confirmation appears before a loss-causing transition; no guessed cancel semantics. |
| 19 | Reorder questions → keyboard method supported. | J.AC3 | Keyboard-only reorder; key bindings unspecified. |
| 20 | Reorder options → keyboard method supported. | J.AC3 | Keyboard-only reorder; no imported prototype shortcut. |
| 21 | PATCH parent → send full final questions array. Not a partial question delta. | J.AC4 | Final added/edited/deleted/reordered collection represented. |
| 22 | Edit/reorder existing question → preserve UUID. | J.AC4 | Same question UUID before/after edits and movement. |
| 23 | Edit/reorder existing option → preserve UUID. | J.AC4 | Same option UUID before/after edits and movement. |
| 24 | Serialize new elements → no ID; serialize all elements → no `sort_order`, FK or local keys. | J.AC4 | New question/option have no ID; forbidden fields absent. |
| 25 | Existing inactive type → allow editing without changing the type. | J.AC5 | Existing inactive code retained on edit. |
| 26 | Existing inactive type → allow reorder without changing the type. | J.AC5 | Move question while retaining inactive code. |
| 27 | New type selection → restrict choices to active types. | J.AC5 | Inactive type cannot be newly selected. |
| 28 | Existing unknown type → preserve without substitution. | J.AC5 | Unknown code remains unchanged; option corner case unresolved. |
| 29 | Unknown type preview → explain limited preview. Actual fallback control not specified. | J.AC5 | Explanation present; full preview behavior belongs adjacent lane. |
| 30 | Repeat GET after saving → reproduce composition. | J.AC6 | Same final question/option membership. |
| 31 | Repeat GET after saving → reproduce order. | J.AC6 | Same question and option sequence. |
| 32 | Receive nested 409/422 → show error at the relevant question/option. Error path syntax/fallback not specified. | J.AC6 | Both statuses associated with appropriate nested item. |
| 33 | Receive nested 409/422 → preserve entered input. | J.AC6 | Unsaved inputs survive errors. |
| 34 | Verification deliverable → unit/component tests for reorder without ID loss, new element, deleted element, empty tags options, limits, errors. | J.AC7 | All six named scenario groups required; no test execution asserted. |

AC coverage: AC1→04–09; AC2→10–15; AC3→16–20; AC4→21–24; AC5→25–29; AC6→30–33; AC7→34. Description→01–03. ID24 contains two separately checkable serialization constraints under the same ownership boundary; neither implies transport implementation acceptance.

### Related wiki clauses: explicit documentary content, not automatically promoted prototype UI

The wiki calls this a prototype. The following are recorded separately from Jira-required behavior; neither source is declared superior.

| ID | Wiki clause / classification | Locator | Verification or boundary |
|---|---|---|---|
| W01 | Form tab has constructor left and live preview right. Each question is a card with title contenteditable input, type selector, required checkbox, right-side sort-order indicator, deletion cross and drag handle `⠿`. **Prototype UI example.** | W.F “Каждый вопрос - карточка” | Later design review can compare layout; exact controls/colors not silently mandated by this extraction. |
| W02 | Tags shows an answer-options block beneath the card; options have editable text. **Explicit prototype editing behavior**, consistent with option-text validation. | W.F “Если тип «Теги»”; W.O | Text editing in tags block. Do not confuse answer options with survey labels MOS-1257. |
| W03 | Options may be deleted. **Explicit prototype behavior.** | W.F “список вариантов… и удалением” | Remove one option; tags minimum remains separate Jira constraint. |
| W04 | “+ Добавить вариант” adds an option with automatic sort_order. **Prototype behavior/model detail.** | W.F | Addition recorded; this does not authorize transmitting sort_order. |
| W05 | “＋ Добавить вопрос” uses the `add-type` selector and appends at end. **Prototype behavior.** | W.F | Append position/type selection; selector identifier is example-only. |
| W06 | Question/option drag updates order automatically; grey dragging source/red drop-target border. **Prototype ordering behavior and visual example.** | W.DND | Order update matches Jira reorder requirement; colors are not separately adopted product requirements. |
| W07 | Question/option addition/removal produces bottom-right two-second toasts. **Prototype example only.** | W.TOAST | Do not infer required production notification copy/timing. |
| W08 | Question data belongs to `draft.questions[]`; option data to `draft.questions[].options[]`. **Documentary ownership**, consistent with J.D1. | W.MAP | Parent draft, nested options; no standalone questions save. |
| W09 | Question model: UUID id, survey FK, required title varchar(500), type-code FK, boolean required, integer display order, created/updated timestamps; question belongs to survey. **Model documentation, not request shape.** | W.Q | Preserves distinction between persisted model and Jira outbound exclusions. Flattening does not prove omitted structural constraints. |
| W10 | Options are for tags: UUID id, owning question FK, required text varchar(255), integer display order, creation timestamp. **Model documentation.** | W.O | Option identity/owner/order understood; no request FK inferred. |
| W11 | Type catalog codes map to stars (1–5), tags (multiple options), text (free comment), boolean (yes/no), scale (0–10), nps (0–10), emoji. Catalog code is stable PK; is_active denotes availability. **Documentary meanings.** | W.LOOKUP | Does not add answer storage or override Jira legacy-type retention. |
| W12 | Preview uses draft title/description, typed controls, tags option chips/multiselect, required marker; submit only toasts. **Adjacent preview example**, not question-editor answer collection. | W.F preview subsection | MOS-1255 scope; only 29 crosses as a stated editor explanation obligation. |
| W13 | Response/answer entities are not implemented in UI; response model is unconfirmed by a viewing screen, fields/statuses need clarification; answer value is jsonb for number/text/tags/boolean. **Documented prototype omission/model uncertainty**, not approved permanent deferral. | W.MAP; W.LIMIT; W.RESPONSE | No answer collection, execution, persistence or export requirements assigned to MOS-1254. |
| W14 | Typical Form-tab flow edits title/type/requiredness/order and adds tags options before viewing preview and parent Save. **Prototype flow.** | W.FLOW | Reinforces parent draft; no autosave or independent submit invented. |

## Architecture — ownership and unresolved boundaries

The documentary flow is MOS-1249 catalog/shared foundation → MOS-1251 parent survey-card draft → MOS-1254 nested questions/options → parent POST/PATCH → repeated GET composition/order. These are issue-named dependencies, not verified API/code architecture. MOS-1255 is the adjacent preview owner named by assignment/membership; neither its complete issue nor its implementation was analyzed. MOS-1246 is a membership grouping, not an accountable person. Individual product decision owner is unknown.

### Differences not resolved by precedence

- Wiki internal/model `sort_order`, survey/question FKs and draft arrays versus Jira's outbound exclusion are **different representation boundaries**, not proof of a contradiction. Keep model fields and no-wire-fields requirements separately; do not send model columns because the prototype displays them.
- Wiki client-only validation/in-memory DATA and Jira POST/PATCH/GET plus nested server errors describe distinct documentary behavior. The prototype's limitations do not remove Jira requirements, nor is a production implementation claimed from Jira. Full save transport and parent close/unsaved-change behavior are outside this assignment.
- No confirmed same-boundary contradiction is established in the read question-editor clauses. Omitted structures are unknown, not reconstructed; no source precedence or explicit approved product deferral was found or invented.

### Material unresolved case Q1

**If an existing unknown type has nonempty options, should saving preserve opaque options, omit them, or block save?** J.AC2 excludes nonempty options for other types; J.AC5 preserves unknown types without substitution. W.F/W.O describe options only for tags; neither the flattened wiki nor the assigned Jira description supplies an explicit reconciliation for that case. No destructive clearing, cancellation or restoration behavior is inferred.

Supervisor was consulted and confirmed retaining the exact question unresolved, completing independent extraction, and not expanding collection. This is **not resolved by this lane's inspected sources**, not a claim that no approved rule exists anywhere. Later full owning-change/spec analysis may provide an approved rule; parent seeks product clarification only if it does not. No dependent implementation/planning conclusion is made here.

Other unspecified details: minimum question count; length normalization/Unicode counting; duplicate option text; defaults for new question/option; exact keyboard controls/focus; what constitutes loss on each type transition; confirmation cancel/restore rules; whether non-tags serialize empty versus absent options; nested-error addressing after reorder/deletion; reload failure/retry/concurrency behavior; precise unknown-type preview. These are verification questions, not invented requirements or proven missing API features.

## Start Here

Open `A/sources/jira-feedback/r1/content.json:50–58`, especially `/items/5/description` AC2/AC5 for Q1, then wiki `/text` W.F/W.Q/W.O. Independent reviewer should verify all seven AC joins and maintain parent-draft, option identity/order/type boundaries. Do not transfer acceptance from shared MOS-1249 or known audience findings.

## Validation and residual risks

Manual source/locator review and two content SHA-256 checks completed. No network/browser, code/API/spec audit, tests/build, source execution, nested agents, source snapshots or project edits occurred. Only this configured report was written. Unit/component verification listed above is future evidence, not performed. Flattened tables, omitted attachments/comments/custom AC fields, source freshness and Q1 remain limitations. Parent acceptance and independent review are pending.
