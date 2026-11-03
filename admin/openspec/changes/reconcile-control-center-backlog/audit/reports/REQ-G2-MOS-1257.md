# Code Context

## Result and scope

REQ-G2-MOS-1257: bounded requirement extraction for survey **tags, segments and operator-group labels**. All six embedded Jira acceptance criteria are decomposed below. This is not an API, product OpenSpec or implementation audit, and not feature acceptance. Parent acceptance follows independent review.

`C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `C/audit`. All abbreviated paths below expand literally. Actor throughout: the administrative survey-card editor user; the inspected issue does not specify a permission/role matrix. Backend is an explicitly named normalization actor, not a verified implementation.

## Files Retrieved

1. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`, `C/tasks.md:1–45`: full governing process documents, not product coverage analysis.
2. `A/work-items/G2-FEEDBACK-REQUIREMENTS-WAVE.md:1–25`: complete common contract and wave file read; executed only MOS-1257 (§lines19–21). Other sections provide no extracted product requirements here.
3. `A/decisions.md:1–8`: focused D-063 search context, including bounded-register acceptance and no repeated census instruction. No full decisions-history read.
4. `A/reports/JIRA-MOS-1246.md:1–52`: accepted membership, source limits and MOS-1257 identity (row at line32). Membership reused, not re-enumerated.
5. `A/reports/G2-JIRA-MEMBER-JOINS.md:1–200`: read context; focused search additionally read lines275–285 and matching context at lines7,77–82. MOS-1257 row283 has unresolved member-scenario join, not proof of missing implementation. Known MOS-1251 shared-card and MOS-1258 boundary findings are not repeated here.
6. `A/sources/jira-feedback/r1/metadata.json:1–11`: full metadata. `A/sources/jira-feedback/r1/content.json:77–85`, JSON pointer `/items/8`: only assigned issue semantically read. Hashing parsed the packet but did not inspect other descriptions.
7. `A/sources/wiki-247734813/r1/metadata.json:1–11`: full metadata. `A/sources/wiki-247734813/r1/content.json#/text`: selected decoded-text slices listed below, and `#/links/0` through `#/links/30` read. No links followed or attachment fetched.

### Integrity and actual source coverage

SHA-256 recomputed over complete saved content bytes, matching both metadata and the assigned Jira expected hash:

- Jira: `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685`; retrieved `2026-10-16T11:17:16.813Z`; MOS-1257 updated `2026-10-12T20:49:41.953+0800`. Saved Backlog status is not acceptance evidence.
- Wiki: `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7`; retrieved `2026-10-16T11:17:53.564Z`, version11, versionWhen `2026-10-12T17:21:31.204+08:00`.

Wiki source URL: `https://wiki.mos-team.ru/spaces/KR/pages/247734813/`; assigned issue identity: MOS-1257 in the saved Jira packet (metadata URL names module MOS-1246). Hashes establish saved extraction integrity, not live freshness or full source-page fidelity.

Offsets below are **zero-based, half-open Python Unicode-character offsets in decoded `/text`**, not bytes or JSON-file lines. Exact contiguous slices printed/read: `[0:2500]`, `[3100:6100]`, `[6300:7400]`, `[7400:8500]`, `[9500:11900]`, `[12000:13050]`, `[13550:14090]`, `[14300:15750]`, `[20750:22330]`, `[26500:27166]`. An earlier keyword-context extraction was output-truncated (only tail lines23–112 displayed); it is discovery only, not a complete wiki read. Conclusions use the explicitly reread slices above. Neighboring preview/registry/model prose incidentally present is not independently audited.

Jira comments, attachments and custom acceptance fields were not captured; description-embedded acceptance criteria **are** present. Wiki is flattened body.view textContent; original table structure is unavailable, not reconstructed. `/links/0` is an HTML prototype attachment reference, unvisited/unexecuted; remaining links are field-name autolinks, not external evidence. No retained related packet was needed.

## Key Code — primary evidence, not application code

### Locator key

- **J-D** = `A/sources/jira-feedback/r1/content.json#/items/8/description`, file line84, `h3. Описание`, paragraphs1–3. Exact field names: `tags`, `segments`, `operator_groups`. It names string fields in `POST/PATCH /api/control/api/v1/managed-resources/feedback/surveys`; this is a **Jira statement only**, not independently checked wire contract.
- **J-AC1…6** = same pointer/line, `h3. Критерии приёмки`, respective numbered `#` paragraphs.
- **W-UI** = wiki `/text[3844:4893]`, prototype §4.2 «Вкладка “Основное”».
- **W-GROUP** = wiki `/text[6300:7400]`, prototype §4.4 «Правила показа», “Триггеры показа”.
- **W-PROT** = wiki `/text[7848:8140]`, prototype §5.2 «Динамические лейблы».
- **W-DRAFT** = wiki `/text[9598:10514]`, prototype §7 «Соответствие модели данных».
- **W-LIMIT** = wiki `/text[10514:11134]`, prototype §8 «Ограничения и не реализовано».
- **W-TAG** = wiki `/text[12160:12573]`, model §2.1 `fb_survey_tag`.
- **W-SEG** = wiki `/text[12573:13012]`, model §2.2 `fb_survey_segment`.
- **W-OG** = wiki `/text[13579:14077]`, model §2.4 `fb_survey_operator_group`.
- **W-DYN** = wiki `/text[20813:22292]`, model §4 «Динамические лейблы раздела», including §4.1 `[21055:21401]`, §4.2 `[21401:21823]`, §4.3 `[21823:22292]`.
- **W-REGISTER** = wiki `/text[26522:27166]`, model §7 «Реестр таблиц раздела».

### Atomic Jira requirements

Each row states the trigger and expected behavior, with a future verification need (not an executed test). Constraints apply to the three fields unless the source explicitly singles out segments. Unspecified counting scope and mechanics remain questions below.

| ID | Trigger → explicit behavior / boundary | Primary locator | Verification need |
|---|---|---|---|
| REQ-G2-MOS-1257-01 | Editing labels → provide chips for tags, segments and operator groups **inside the unified survey card**; depend on editor foundation MOS-1251. | J-D ¶1,3 | All three controls participate in that card, not separate entity screens. |
| REQ-G2-MOS-1257-02 | Adding a label → each field allows addition from keyboard. | J-AC1 | Keyboard addition for all three; exact key binding unspecified. |
| REQ-G2-MOS-1257-03 | Removing a chip → each field allows removal from keyboard. | J-AC1 | Keyboard removal for all three; focus behavior is unspecified. |
| REQ-G2-MOS-1257-04 | Saving edited labels → changes belong to the **single card save**, not independent label CRUD. | J-AC1; J-D | Add/remove before unified save; no independent persistence assumption. |
| REQ-G2-MOS-1257-05 | Serializing values → send comma-separated **name strings**, not lookup codes; do not generate codes or UUID arrays. | J-D ¶2; J-AC2 | Name-string payload representation; no generated identifiers. |
| REQ-G2-MOS-1257-06 | Parsing input → comma is always a separator; quotes do not escape it. | J-AC2 | Quoted comma still divides names; no CSV quoting semantics invented. |
| REQ-G2-MOS-1257-07 | Clearing field → empty string clears its associations. | J-AC3 | Explicit `""` clears associated set; distinguish omitted field. |
| REQ-G2-MOS-1257-08 | Omitting field → retain its previous associations. | J-AC3 | Untouched/omitted field preservation, distinct from clear. |
| REQ-G2-MOS-1257-09 | Sending any label field → never send `null`. | J-AC3 | Clear and omitted branches produce no null field. |
| REQ-G2-MOS-1257-10 | Removing a chip → removal does **not** globally delete that label. | J-AC3 | Survey association removal without global label deletion. |
| REQ-G2-MOS-1257-11 | Handling label set → limit is **100 distinct labels**. | J-AC4 | 100/101 distinct boundary; duplicate treatment with -15; whether per field or aggregate unresolved. |
| REQ-G2-MOS-1257-12 | Validating name → limit is **150 characters after trim**. | J-AC4 | 150/151 after trim; whitespace-boundary case; character-count convention unresolved. |
| REQ-G2-MOS-1257-13 | Handling input → limit is **16000 input characters**. | J-AC4 | 16000/16001 input boundary; measurement point/scope unresolved. |
| REQ-G2-MOS-1257-14 | `audience_type=segment` → after parsing there must be at least one label. | J-AC4 | Empty parsed segment set versus one label; boundary handling of blank comma tokens needs clarification. No audience execution inferred. |
| REQ-G2-MOS-1257-15 | Backend processes submitted names → backend normalizes spaces and duplicates case-insensitively. | J-AC5 | Duplicate/case/whitespace cases; do not substitute a guessed client normalization algorithm. |
| REQ-G2-MOS-1257-16 | Save succeeds → UI adopts canonical names from the response. | J-AC5 | Submitted spelling differing from canonical response updates chips. Response shape is not specified here. |
| REQ-G2-MOS-1257-17 | Switching audience → switching alone does not remove saved associations. | J-AC5 | Switch away/back without implicitly clearing saved labels. Unsaved-draft restoration semantics not supplied. |
| REQ-G2-MOS-1257-18 | Error occurs → input is not cleared. | J-AC6 | Preserve entered values on failure; statuses/messages/retry not specified. |
| REQ-G2-MOS-1257-19 | Implementing this scenario → unit/component coverage must include duplicates/canonical response, empty set, length boundaries, audience change and absence of global CRUD requests. | J-AC6 | Future test obligations enumerated verbatim; none run in this lane. |
| REQ-G2-MOS-1257-20 | Operating labels → no separate registries/CRUD for these three entities; generic standard-dictionary editor is outside this task. | J-D ¶1; J-AC2,6 | No separate CRUD requests; do not create dictionary-management scope. |

AC coverage: AC1→02/03/04; AC2→05/06/20; AC3→07/08/09/10; AC4→11/12/13/14; AC5→15/16/17; AC6→18/19/20. Description→01/05/20. This covers saved description/AC, not omitted issue fields.

### Wiki clauses, purpose and classification

| ID | Saved clause | Classification and boundary |
|---|---|---|
| REQ-G2-MOS-1257-W01 | W-DYN introduction: these tables “не являются справочниками и не входят в каталог справочников”; dynamically created by parsing comma-separated user input at resource creation. | Explicit model statement supporting freeform dynamic labels, not catalog CRUD. Does not independently define update transport or client code generation. |
| REQ-G2-MOS-1257-W02 | W-TAG, W-DYN §4.1: tags support survey search/grouping; card «Основное» → «Теги». | Field purpose/placement; search execution belongs outside this lane. |
| REQ-G2-MOS-1257-W03 | W-SEG, W-DYN §4.2: segments target users; card «Основное» → «Сегменты», registry «Аудитория». W-UI shows segment editor only when type is `segment`. | Model placement plus prototype-only visibility behavior. Not permission to clear hidden associations or evaluate audience membership. |
| REQ-G2-MOS-1257-W04 | W-OG, W-DYN §4.3: operator groups target display; card «Правила показа» → «Триггеры показа» → «Для каких групп операторов». W-GROUP describes dynamically created chips. | Placement/purpose, not real operator directory management or delivery execution. |
| REQ-G2-MOS-1257-W05 | W-TAG/W-SEG/W-OG describe survey associations and uniqueness of `(survey_id, tag_id/segment_id/operator_group_id)`. | Persistence ownership is survey association; internal model UUID relations do not imply client UUID-array payload. Storage-model inconsistency retained below. |
| REQ-G2-MOS-1257-W06 | W-DYN §4.1–4.3 give `display_name varchar(150)` and `code varchar(64)` primary keys, with timestamps. | Model statement, not permission to send/generate codes in UI. Jira adds after-trim semantics and other limits. |
| REQ-G2-MOS-1257-W07 | W-UI: clickable selected/unselected chips, “+ Добавить” prompt, transliteration-generated unique codes displayed beside names. W-PROT adds snake_case and in-memory arrays; W-DRAFT represents associations by code arrays. | **Prototype example behavior**, conflicting with Jira if adopted as current input/persistence contract. Not silently promoted to requirement. |
| REQ-G2-MOS-1257-W08 | W-DYN §4.2 sample segments «ЖКХ, Транспорт, активные»; §4.3 sample groups «ЖКХ, первая линия». | Explicit “Значения из прототипа”: examples, not exhaustive catalog, defaults or required test fixtures. |
| REQ-G2-MOS-1257-W09 | W-LIMIT says client-only validation and in-browser memory lost on reload. | Prototype limitation, **not** approved product deferral of backend normalization/persistence and not desired production behavior. |

## Architecture — ownership and boundaries

The requirement flow is user chip edits → unified survey-card state/save (MOS-1251 foundation explicitly named) → name-string fields → backend normalization → response canonical names adopted by UI. It is extracted intent, not an implementation diagram. Association removal/clear is local to the survey; the label's global lifetime is not controlled by chip deletion. Hidden fields after audience selection must not be presumed deleted.

Owner: MOS-1257 for these controls; MOS-1251 for unified editor foundation (J-D). The accepted membership report identifies MOS-1231 as backend feedback dependency and MOS-1249 as FE API foundation, but this extraction does not assign their detailed responsibilities or certify their delivery. Accountable product person is not named in the inspected issue. Known shared audience/display-rule boundary is already indexed at `G2-JIRA-MEMBER-JOINS.md:78,279,284`; no repeat registry/audience audit performed.

Excluded: generic dictionary editor/CRUD, full survey editor and save transport audit, surface selection, actual audience targeting/eligibility and display execution, registry search/filter implementation, answer-option “Теги” controls, real answer collection, full API/schema/product-spec/code comparison. No new approved product deferral is established by these sources.

## Discrepancies and unresolved questions

1. **Q1257-01 — freeform input versus prototype selection/code behavior.** Jira J-D/AC2 explicitly says free labels, name strings, no code generation; W-UI/W-PROT/W-DRAFT describe selectable code-bearing chips, client code generation and code arrays. Which prototype presentation/selection behavior, if any, remains intended under freeform-name editing? Must suggestions exist, may existing labels be selected, should any code be displayed? The inspected set does not settle these UI semantics. Do not infer a catalog, mandatory suggestions, code-generation algorithm or persisted code-array representation.
   - Supervisor consulted on this material discrepancy: preserve both positions, finish independent extraction, and do **not** choose precedence. It is unresolved **by this inspected source set**, not necessarily a new product-decision blocker: a later full MOS-1257 planning/approved-decision comparison may already resolve it. Any proposed change dependent on disputed semantics waits for that reconciliation or user clarification. No such comparison performed here.
2. **Q1257-02 — model identity inconsistency.** W-TAG/W-SEG/W-OG refer to UUID `*.id`; W-DYN describes `code` as primary key without `id`. W-REGISTER calls the same tables “Справочник-данные”, whereas W-DYN explicitly excludes them from dictionaries/catalog. Preserve documentary inconsistency; do not repair storage design or infer UI UUID/code submission. Neither inconsistency nullifies the explicit name-input extraction.
3. **Q1257-03 — validation precision.** Are 100 distinct labels and 16000 input characters per field or across the card? Which character-count convention is intended? Are blank tokens ignored, rejected or normalized; how are only commas/whitespace handled; when is the raw-input limit measured? Source gives maxima and post-parse nonempty-segment rule, not these mechanics. Do not invent truncation, silent dropping or ordering rules.
4. **Q1257-04 — normalization and state precision.** Exact whitespace folding, Unicode/case handling, canonical spelling choice/order, client-side prevalidation timing, duplicate feedback, and server validation messages are unspecified. Audience switch explicitly preserves **saved** associations; preservation/restoration of unsaved draft edits and treatment of hidden pending input are not separately defined. Failure retains input, but retry/concurrency/partial-success semantics are not provided.
5. **Q1257-05 — inaccessible evidence.** Omitted comments/custom fields and flattened table structure are unavailable evidence, not proof that requirements never exist. Prototype attachment was not inspected. Current API representation, local plan resolution and code behavior remain unexamined, not missing.

## Start Here

Open `A/sources/jira-feedback/r1/content.json:77–85` (`/items/8/description`) first: it contains the complete assigned description and six AC. Then compare W-UI/W-PROT/W-DRAFT and W-DYN at the saved exact offsets above; do not resolve the prototype discrepancy from status, timestamp, mock or DTO.

## Validation and residual risks

Manual inspection mapped every saved AC to stable atomic IDs and separated explicit requirements from prototype examples, model clauses and unavailable evidence. Two saved primary hashes match. Only this configured report was written; no project/source/plan edits, staging, network, browser, business calls, credentials, tests/build, source-example execution or nested agents. Unit/component verification above is prospective, not executed. Independent review and parent acceptance remain pending. Residual risks: unresolved prototype/model semantics, flattened/omitted evidence, and unknown resolution in uninspected approved plans.

```acceptance-report
{
  "criteriaSatisfied": [
    {"id":"criterion-1","status":"satisfied","evidence":"Extracted all six saved MOS-1257 AC into 20 atomic Jira requirements, with exact primary locators, nine wiki clauses, explicit boundaries and unresolved questions."}
  ],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1257.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python JSON extraction and SHA-256 calculation for jira-feedback/r1 and wiki-247734813/r1","result":"passed","summary":"Both content hashes match metadata; assigned issue and relevant decoded wiki sections inspected."},
    {"command":"Application tests/build/browser/E2E","result":"not-run","summary":"Forbidden and unnecessary for this requirement-only assignment."}
  ],
  "validationOutput": ["Jira SHA-256 890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685", "Wiki SHA-256 d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7", "AC1–AC6 fully mapped; no product/API/spec/code completeness claim."],
  "residualRisks": ["Prototype code-generation/selection semantics conflict with explicit Jira name-input constraints; existing-plan reconciliation or clarification needed before dependent changes.", "Flattened wiki and omitted comments/attachments/custom fields limit evidence.", "No implementation, API or product-plan verification; independent review and parent acceptance pending."],
  "noStagedFiles": true,
  "diffSummary": "Configured requirement report only; no staging operations performed.",
  "reviewFindings": ["No blocker to bounded extraction; disputed conclusions remain unresolved, not silently selected."],
  "manualNotes": "Supervisor confirmed preservation of the material source discrepancy without inventing precedence or a new product gate. All checks were local documentary inspection, not application tests."
}
```
