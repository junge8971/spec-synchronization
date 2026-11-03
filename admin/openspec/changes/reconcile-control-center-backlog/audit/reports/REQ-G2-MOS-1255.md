# Code Context

## Result and scope

REQ-G2-MOS-1255: bounded requirements extraction for interactive survey preview only. Parent acceptance after independent review remains required. No API, product-spec or implementation audit; no feature closure or full R/A/S/I completeness claim.

Owner: **MOS-1255** within accepted MOS-1246 membership. Its description explicitly names prerequisites **MOS-1254** (question constructor) and **MOS-1251** (single survey draft). No accountable person is identified in these selected sources. No neighboring issue body was analyzed.

## Files Retrieved

Paths below are repository-relative. `C = openspec/changes/reconcile-control-center-backlog`; `A = C/audit` (these abbreviations expand literally for every locator below).

1. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`, `C/tasks.md:1–45`: complete governing process documents, not business coverage audit.
2. `A/work-items/G2-FEEDBACK-REQUIREMENTS-WAVE.md:1–25`: complete file returned; common contract and MOS-1255 section executed exclusively.
3. `A/decisions.md:1–10`: D-063 bounded ownership acceptance, no repeated census.
4. `A/reports/JIRA-MOS-1246.md:1–53`: complete accepted membership report; MOS-1255 row references primary lines59–67.
5. `A/reports/G2-JIRA-MEMBER-JOINS.md:1–180`, plus scoped matches with context at77–79 and278–285: known preview unresolved join at281; existing shared audience boundary only reused, not re-audited. Remaining report not read.
6. `A/sources/jira-feedback/r1/metadata.json:1–11`: complete metadata. `A/sources/jira-feedback/r1/content.json#/items/6` (physical lines59–67): entire assigned record extracted locally, including full description and six acceptance criteria. Other issue bodies not printed/read; whole file bytes parsed for extraction/hash only.
7. `A/sources/wiki-247734813/r1/metadata.json:1–10`: complete metadata. `A/sources/wiki-247734813/r1/content.json:1–8` returned the full flattened `/text` on line8. Preview-relevant portions were also extracted selectively using decoded character offsets below. Entire `/links` array (indices0–30) printed locally. Other wiki clauses incidentally visible in the flattened line were not independently audited.

Actual selective `/text` reads (zero-based Unicode character offsets, end-exclusive): `[0:1321]`, `[4513:7216]`, `[9204:12544]`, `[15876:18034]`, `[21337:23271]`; then exact sections `[469:869]`, `[3174:3844]`, `[4893:6286]`, `[9513:9598]`, `[9598:11134]`, `[15826:17362]`. Final line8 read exposed the complete text; this is not claimed as complete semantic analysis of the wiki.

### Primary source integrity and locator vocabulary

- **J** = `A/sources/jira-feedback/r1/content.json#/items/6/description`, line66. J.D1/D2/D3 refer respectively to the three paragraphs under `h3. Описание`; J.AC1–AC6 refer to the six `#` items under `h3. Критерии приёмки`. Record key is MOS-1255, saved update `2026-10-12T20:49:12.702+0800`. Retrieved `2026-10-16T11:17:16.813Z`. SHA-256 recomputed **890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685**, matches metadata and assignment.
- **W** = `A/sources/wiki-247734813/r1/content.json#/text`, line8; title `Раздел "Обратная связь"`, version11, versionWhen `2026-10-12T17:21:31.204+08:00`, retrieved `2026-10-16T11:17:53.564Z`. SHA-256 recomputed **d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7**, matches metadata.
- **W.Form** = first narrative §4.3 `Вкладка «Форма»`, `/text[4893:6286]`, bounded by §4.4. All visual details cited below occur in its `Предпросмотр - тёмная карточка…` paragraph.
- **W.Exit** = narrative §2 `/text[469:869]`, §4.1 `/text[3174:3844]`, §6.5 `/text[9513:9598]`; §6.2 `Подтверждение выхода` also visible on line8.
- **W.Limits** = narrative §§7–8 `/text[9598:11134]`.
- **W.Questions** = later `Таблицы`, §§3.2–3.3 `/text[15826:17362]`: question required/order and option order vocabulary, not a wire contract.

These are hashes of retained extractions, not original pages or attachments. Jira comments, attachments and custom acceptance fields were not collected. Wiki tables are flattened, not structurally complete. `/links/0` names `ПротоОбратнаяСвязь.html` attachment version1; it was **not fetched, read or executed**. Other links are field-name autolinks, not traversed. No inference from executable prototype semantics or missing structural detail.

## Key Code — atomic requirement ledger (no application code inspected)

Actor for each row: administrative survey-card editor trying the questionnaire, not a real respondent. **R** = explicit Jira obligation. **V** = documented prototype visual reference, not independently established mandatory production styling. Verification entries are future checks, not executed tests.

| ID | Class / trigger | Expected behavior and explicit boundary | Primary locator | Verification need |
|---|---|---|---|---|
| MOS1255-R01 | R: open constructor | Live preview alongside constructor; not a separate real-answer collection flow. | J.D1 `Добавить рядом с конструктором живой preview по HTML-прототипу`; W.Form | Render constructor and preview together. |
| MOS1255-R02 | R: edit survey name | Preview immediately reflects current draft name; no save prerequisite. | J.AC1 `Изменения названия/описания…сразу видны`; W.Form `из черновика` | Change name without saving. |
| MOS1255-R03 | R: edit description | Preview immediately reflects draft description. | J.AC1; W.Form | Change/clear description without saving. |
| MOS1255-R04 | R: edit questions | Preview immediately reflects question changes. | J.AC1 `вопросов`; W.Form | Add/edit/delete draft question. |
| MOS1255-R05 | R: change type | Preview immediately renders the changed question type. | J.AC1 `типов` | Change type in draft; pair with R18. |
| MOS1255-R06 | R: edit options | Preview immediately reflects changed answer options. | J.AC1 `вариантов`; W.Form tags | Add/edit/delete option; pair with R17. |
| MOS1255-R07 | R: change required | Preview immediately reflects required flag. | J.AC1 `required` | Toggle flag and try submit. |
| MOS1255-R08 | R: reorder | Preview immediately reflects draft order; wiki documents question and option sort_order. | J.AC1 `порядка`; W.Form; W.Questions | Reorder questions and tag options. No answer identity algorithm prescribed. |
| MOS1255-R09 | R: answer stars | Interactive stars with values **1–5**. | J.AC2 `stars 1–5`; W.Form | Select each endpoint and intermediate value. |
| MOS1255-R10 | R: answer scale | Interactive scale with values **0–10**. | J.AC2 `scale/NPS 0–10`; W.Form | Select endpoints, especially zero. |
| MOS1255-R11 | R: answer NPS | Interactive NPS with values **0–10**, a distinct listed type. | J.AC2; W.Form | Exercise NPS independently from scale. |
| MOS1255-R12 | R: answer emoji | Interactive emoji. Wiki reference specifies two buttons 👍 / 👎; no numeric encoding is prescribed. | J.AC2 `emoji`; W.Form | Exercise both choices without inventing wire values. |
| MOS1255-R13 | R: answer yes/no | Interactive yes/no. | J.AC2 `да/нет`; W.Form | Both choices, particularly false. |
| MOS1255-R14 | R: answer tags | Interactive multiple tag-option selection, not survey-label editing. | J.AC2 `multi tags`; W.Form `чипсы из вариантов ответа…мультивыбор` | Select multiple options; verify local state. |
| MOS1255-R15 | R: answer text | Interactive text input; wiki reference uses textarea. No response text length/normalization specified here. | J.AC2 `text`; W.Form | Enter/change text. |
| MOS1255-R16 | R: delete question | Clear incompatible trial answers when a question is removed. | J.AC3 `Удаление вопроса/варианта…очищают несовместимые ответы` | Answer then delete question; removed answer cannot satisfy validation. |
| MOS1255-R17 | R: delete option | Clear incompatible trial answers when an option is removed. | J.AC3 | Select option then remove it; treatment of unrelated compatible selections is unspecified. |
| MOS1255-R18 | R: change type after answer | Clear incompatible trial answers on type change. Does not require clearing every compatible answer. | J.AC3 | Enter old-type answer then change type; compatibility matrix needs definition if material. |
| MOS1255-R19 | R: interact with preview | Trial answers exist only locally, separately from survey draft; do not mutate card. | J.D1 `только локально, отдельно от draft`; J.AC3 `не изменяют карточку` | Compare card/draft before and after trial interactions. |
| MOS1255-R20 | R: trial send | No network sending of answers, no server persistence; user-response API is outside scope. Not a ban on unrelated editor reads/saves. | J.D2 `preview сетевых запросов отправки не делает`; J.AC3 | Assert absence of answer-send request during trial submit. |
| MOS1255-R21 | R: trial send | Validate required questions. Exact field-error placement, copy and focus behavior are not stated. | J.AC4 `Пробная отправка проверяет обязательность` | Required unanswered versus answered; do not conflate with card name/code save validation. |
| MOS1255-R22 | R: required numeric zero | **0 counts as filled**, including scale/NPS. | J.AC4 `значения 0 и false считаются заполненными` | Required scale/NPS zero passes presence check. |
| MOS1255-R23 | R: required boolean false | **false counts as filled**. | J.AC4 | Required “нет” passes presence check. |
| MOS1255-R24 | R: trial-send feedback | Message refers to preview checking, not saving a real response. Exact final copy unspecified. | J.AC4 `Сообщение относится к проверке preview, не к сохранению реального ответа` | Check meaning for trial validation feedback. |
| MOS1255-R25 | R: click Skip | `«Пропустить» сбрасывает пробные ответы`; not real skip registration or card discard. No navigation/closing behavior prescribed. | J.AC5 | Fill several types, click Skip, verify trial answers reset and draft unchanged. |
| MOS1255-R26 | R: view preview | Mode explicitly identified as preview. | J.AC5 `Режим явно обозначен как предпросмотр` | Visible mode identification; final wording not prescribed. |
| MOS1255-R27 | R: no questions | Explicit empty-questionnaire state. | J.AC2 `Пустая анкета…имеют явные состояния` | Empty draft renders explicit state; submit availability unspecified. |
| MOS1255-R28 | R: unknown question type | Explicit unknown-type state; no fallback type invented. | J.AC2 `неизвестный тип` | Unknown type visibly handled; required/submit interaction remains unspecified. |
| MOS1255-R29 | R: keyboard operation | Keyboard supported. Exact key bindings/focus model/ARIA roles not enumerated. | J.AC6 `Клавиатура…поддержаны` | Operate controls without pointer; do not substitute prototype modal Esc for this requirement. |
| MOS1255-R30 | R: narrow screen | Narrow-screen operation supported. Breakpoint and stacking prescription absent. | J.AC6 `узкий экран поддержаны` | Verify usable preview and controls at narrow width; not fixed desktop columns everywhere. |
| MOS1255-R31 | R: verification deliverable | Component tests cover **all types**, required with **0/false**, draft changes, and absence of network submission. | J.AC6 second sentence | Required future component suite; no test executed in this lane. |

### Prototype presentation references, kept distinct from R obligations

All exact locators: **W.Form** (narrative §4.3, `/text[4893:6286]`). Jira D1 references an HTML prototype, but its attachment was not read; these are saved prose descriptions, not proof of executable behavior or pixel-perfect requirements.

| ID | Documented reference |
|---|---|
| MOS1255-V01 | Form tab uses two columns: constructor left, live preview right. Preview is a dark card imitating the user form. No precise dimensions, mobile transformation or colors beyond this description. |
| MOS1255-V02 | Stars: five clickable stars with highlighting. |
| MOS1255-V03 | Scale: eleven buttons, endpoint captions `Совсем плохо / Отлично`. |
| MOS1255-V04 | NPS: eleven buttons, endpoint captions `Не рекомендую / Обязательно рекомендую`. |
| MOS1255-V05 | Emoji: two buttons 👍 / 👎; yes/no: two buttons; tags: option chips with multiple selection; text: textarea. These expand the R12–R15 interaction references, not answer serialization. |
| MOS1255-V06 | Required questions have a red asterisk. This alone does not establish keyboard/accessibility compliance. |
| MOS1255-V07 | Buttons `Пропустить` / `Отправить`; Send shows toast `Спасибо за обратную связь!` in the described prototype. Do not infer an answer was actually saved. |

## Architecture — requirements data flow and boundaries

`MOS-1251 single draft → MOS-1254 question/options editing → MOS-1255 immediate visual projection`; trial answers are separate local preview state. Trial Send performs required checking without answer delivery. Skip clears trial answers, not the parent draft. Source: J.D1–D3 and AC1–AC5, W.Form. This is requirement ownership, not a code architecture finding.

**Saved versus draft:** W.Form expressly says title/description come from draft; J.AC1 extends immediate change reflection to questions/types/options/required/order. W.Limits describes prototype `draft` and `DATA`, in-memory storage and data loss on reload. Those prototype internals do not require a particular production store, server endpoint, saved-only preview, browser persistence mechanism or global card-save policy. Preview is not a frozen saved record. Draft load/save transport remains MOS-1251 territory, not established here.

**Exit boundary:** Jira specifies only Skip's reset (R25), not exiting the preview or page. W.Exit §2 describes breadcrumb return and loss of unsaved changes on closing without confirmation; §4.1 names Close → `Выйти без сохранения?`, §6.2 names `Нет`/`Да`, and §6.5 names Esc/backdrop closing a modal. These are parent-card/prototype context, not permission to discard the draft through Skip, make Esc exit preview, or invent a new preview modal. The wording tension in §2 versus the explicit confirmation description is preserved, not settled here. Parent-card exit policy belongs with MOS-1251; this report does not repeat a full editor audit. Trial-answer retention on tab changes, card close/reopen, survey switch, save and reload is not specified beyond locality and the explicit reset/incompatibility clauses.

**Excluded versus deferred:** J.D2 expressly excludes user-answer API from scope; W.Limits §§7–8 describes `fb_response`/`fb_response_answer` UI/persistence as not implemented in the prototype. Neither establishes approval, release timing or acceptance of future real response collection. No delivery execution, trigger/cooldown enforcement, respondent identity, response export, real Skip registration, or status change is inferred from this preview. The wiki typical-workflow sentence about a survey starting to show after saving is not a delivery requirement assigned to MOS-1255. No new product deferral is invented.

## Errors, uncertainties and decisions not made

1. **Trial-submit copy:** J.AC4 imposes preview-only meaning; W.Form supplies the exact prototype thank-you toast. These are not proven incompatible mandatory requirements. Supervisor consulted through `need_decision`: retain prototype example separately, do not invent final production copy, and do not automatically block extraction on unspecified wording. Owning-plan/reconciliation lane can check existing approved wording and whether the example is normative. No source precedence selected.
2. **Validation detail unknown:** required whitespace-only text, empty tag selection semantics, unknown-required type submit handling, field-error placement, disabled submit, focus on error, successful-submit reset and duplicate-click behavior are not explicitly settled by the retained clauses. Presence checks for numeric zero and boolean false are explicit and must not be weakened. No backend/network-error contract belongs to trial answer sending because that sending is forbidden.
3. **State compatibility unknown:** removal/type-change cleanup is mandatory, but stable answer identity, cross-type compatible-value rules, preservation of unaffected values, and retained state across parent lifecycle events are unspecified. Do not infer index-keyed state or unconditional resets from prototype code that was not read.
4. **Accessibility/layout limits:** keyboard and narrow screen are explicit; exact responsive breakpoint, control semantics, focus traversal, screen-reader announcements and color contrast details are not enumerated here. A dark card or red asterisk is not evidence of accessible delivery.
5. **Unavailable detail is not missing functionality:** flattened wiki structure, unread attachment and omitted Jira comments/custom fields prevent a claim of full source sufficiency. This report identifies no absent API/spec/code behavior and no implementation acceptance from Backlog status.

## Start Here

For review, open `A/sources/jira-feedback/r1/content.json` lines59–67 (`/items/6/description`) and compare each of its six acceptance criteria against R01–R31. Then read W.Form at line8 using the exact decoded offsets to verify presentation references and draft provenance. Follow with W.Exit/W.Limits for non-preview boundaries. Independent reviewer should check source classification and requirement coverage, not infer implementation.

## Validation and residual risks

Manual checks: both retained source hashes match metadata (Jira also matches work-item hash); all six Jira AC items mapped; the seven listed types are individually represented; exact preview-only submit/reset boundaries retained. Only the configured report was written. No network/browser, source-example execution, tests, builds, application edits, API audit, product-spec audit or nested agents. No staging operation performed. Parent review/acceptance remains outstanding; omitted primary material and unspecified interaction detail remain residual risks.
