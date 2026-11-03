# Code Context

## Result
REQ-G2-MOS-1258 only: all seven embedded Jira acceptance criteria mapped below. Requirements extraction, not implementation acceptance. No materially missing input blocks this bounded extraction.

## Files Retrieved / actual read scope
All relative paths below start at `openspec/changes/reconcile-control-center-backlog/audit/` (A).

- `A/work-items/G2-FEEDBACK-EDITOR-CONDITIONS.md`: complete assignment (all sections).
- **J** = `A/sources/jira-feedback/r1/content.json`, lines 1–100 returned. Target item is lines 86–94, `/items/9`; complete description and all seven AC are at line 93, `/items/9/description`. Earlier items and the beginning of item10 were incidentally returned, not re-extracted. No saved-filter AC read.
- **W** = `A/sources/wiki-247734813/r1/content.json`, lines 1–40 returned; the entire flattened `/text` is one physical line (8). Used only prototype §§3.2–3.6 and §4.4/model §3.4 for the search/display boundary; other text was incidentally returned, not audited. Remaining link list unread.
- `A/sources/jira-feedback/r1/metadata.json`, lines 1–11, complete; `A/sources/wiki-247734813/r1/metadata.json`, lines 1–11, complete.
- `A/reports/JIRA-MOS-1246.md`, complete: accepted membership inventory only; MOS-1258 row points to J:86–94. No hierarchy re-inventory.
- **B** = `A/reports/JOURNAL-FEEDBACK-AUDIENCE.md`, lines 1–100 returned; used Result, source-locator ownership evidence, candidate 03 and Architecture only. Embedded plan references/other conclusions were not independently followed or re-audited; final closing fence not read.

J is revision 1 captured 2026-10-16T11:17:16.813Z; target updated 2026-10-12T21:16:28.873+0800, Backlog. W is version 11, updated 2026-10-12T17:21:31.204+08:00, captured 2026-10-16T11:17:53.564Z. Assignment/metadata hashes are parent-attributed, not independently computed: J `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685`; W `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7`.

## Key requirements (not code)
**Locator convention:** J ACn means the nth `#` paragraph under `h3. Критерии приёмки` within the single JSON string `/items/9/description` (line 93), not an invented nested JSON pointer. Quotes below are verbatim source fragments.

| ID / AC | Atomic requirement or inseparable clause | Exact evidence |
|---|---|---|
| C1 / AC1 | Build field/operator choices from metadata; supported fields are name, code, description, type_code, status, audience_type, owner. Exactly one flat and/or group, at most 50 rows; no nested-group requirement. | “Поля/операторы строятся по metadata: name/code/description/type_code/status/audience_type/owner; одна плоская and/or группа до 50 строк.” |
| C2 / AC2,7 | in/not_in uses 1–100 unique lookup codes, each a string of 1–1000 characters; inactive codes remain usable for search. Removing the last code removes the condition, never sends an empty array. | AC2: “1–100 уникальных кодов справочника”; “Неактивные коды допустимы в поиске.” AC7: “1–100 уникальных строк по 1–1000 символов”; “Удаление последнего кода in/not_in удаляет условие; пустой массив не отправляется.” |
| C3 / AC2,7 | is_empty/is_not_empty needs no value: value may be absent or null. | AC2: “значение не требуется”; AC7: “value отсутствует либо null.” |
| C4 / AC7 | contains/not_contains/eq/ne/starts_with/ends_with requires string value length 1–1000; preserve whitespace, including whitespace-only strings as nonempty. | “value — строка 1–1000 символов”; “Пробелы не обрезаются, строка из пробелов не пуста.” |
| C5 / AC3 | Combine query and ordinary status/type_code with the group using AND, without silently changing group logic. Audience is an explicit condition inside that group, not an independent filter. | “query и обычные status/type_code объединяются с группой через AND; логика группы не меняется скрыто”; “Аудитория доступна как явное условие внутри группы, отдельного независимого фильтра нет.” |
| C6 / AC4 | Offer add/remove/apply/clear, an active-condition badge and active-condition panel. Keep unapplied condition draft out of search, export and saved filters. | “Есть добавление/удаление, применение, очистка, badge и панель активных условий”; “Неприменённый draft не попадает в поиск/экспорт/сохранённый фильтр.” |
| C7 / AC5 | Server evaluates conditions across the whole selection; counts/pagination correspond to search; changed selection resets offset. This is not local filtering of the current page. | “Условия исполняет сервер по всей выборке; counts/pagination соответствуют search, смена отбора сбрасывает offset.” AC6: “отсутствие локальной фильтрации страницы”. |
| C8 / AC5 | Restore complete conditions through URL/history/copy, integrated with registry-owned applied-search state. No wire encoding specified here. | “URL/history/copy полностью восстанавливают conditions.” |
| C9 / AC6 | Show a 422 JSON Pointer error at the affected condition while preserving input. | “422 с JSON Pointer отображается у условия без потери ввода.” |
| C10 / AC6,7 | Required unit/component coverage: status AND (A OR B), empty/invalid values, limit, URL, no local page filtering; 1/1000/1001 characters, whitespace without trim and clearing last value. These are required test scenarios, not claims of executed tests. | AC6: “Unit/component-тесты: status AND (A OR B), пустые/невалидные значения, лимит, URL и отсутствие локальной фильтрации страницы.” AC7: “Тесты: 1/1000/1001 символ, пробелы без trim и очистка последнего значения.” |

### Relevant wiki corroboration and differences
All W locators are `/text` (line 8), named heading plus exact quote:

- §3.4 `Расширенный фильтр «⚙ Условия»`: “Логика: И (все условия) / ИЛИ (любое условие).” Text operators “содержит, не содержит, равно, не равно, начинается с, заканчивается на, пусто, не пусто”; enum “входит в, не входит в (с чипсами-значениями)”. Corroborates builder semantics, not a JSON grammar or exhaustive per-field operator matrix.
- Same §3.4: “Условия добавляются, удаляются, очищаются”; “Применённые условия отображаются в панели-баре под фильтрами с кнопкой «Сбросить всё»”; “бейдж с числом активных условий”. Supports active-count badge and applied-condition presentation.
- §3.4 field list includes “Теги” and omits description; J explicitly lists description and defers tags in its dependency paragraph. Do not union the lists or silently enable tags.
- §3.3 says “Три выпадающих фильтра” including “Вся аудитория”; J explicitly excludes that independent filter. §3.2 broader prototype search and §3.1 audience sorting are not newly extracted requirements.
- §3.5 says saved filter includes “поиск, мультиселекты и расширенные условия”; link text mentions only “q, status, type”. J AC5 expressly requires conditions restoration; this does not establish any additional URL parameter spelling or serializer. Saved-filter name/overwrite behavior is outside this extraction.
- §4.4 “Условия” means “Тип диалога… Результат диалога… Приоритет… Эксклюзивный показ” on the card, with fields bound to `fb_display_rule`; model §3.4 calls these “настройки показа опросника”. These are NOT registry search conditions.

## Architecture / ownership boundaries (requirements only)
- **MOS-1258:** condition editing and its applied-search contribution, as C1–C10. J description: “Добавить конструктор условий И/ИЛИ к общей модели search реестра.” Description names conditions in search/export search and metadata `condition_fields`; no endpoint/schema analysis performed.
- **MOS-1250:** base status/type_code multiselects and shared registry search/URL application. J explicitly says these “принадлежат MOS-1250 и здесь не дублируются”. C5/C7/C8 describe integration obligations, not a second registry owner.
- **MOS-1249:** declared dependency for shared integration/metadata; no transport or permission policy re-extracted.
- **MOS-1259:** saved-filter behavior remains separately owned; only exclusion of unapplied draft is extracted here. **MOS-1260:** export owner per accepted membership inventory; only applied-condition boundary is assigned here.
- **MOS-1251:** card audience/surface binding and display-rule configuration. B Result says “MOS-1258 concerns registry search conditions, not these card controls”; B candidate JOURNAL-FEEDBACK-AUDIENCE-03 is an ownership guard, not a new audience audit. Its historical duplicate-control question supplies no search semantics and no authorization to remove controls or create another relation.
- Explicit deferrals in J description: “Независимый фильтр аудитории одновременно с OR-группой, условия tags и сортировка аудитории отложены.” No product choice made to reverse them. No DSL, nesting, serializer, trigger execution or UI-role policy invented.

## Start Here
Read J `/items/9/description` (physical line 93) alongside W `/text` §3.4. Those are the direct builder evidence; retain the owner boundaries above rather than reopening accepted registry/saved-filter extraction.

## Genuine unknowns / residual limits
- Exact metadata field/operator compatibility matrix and wire/URL serialization are not defined in these retained prose clauses; no schema or implementation was inspected. No conclusion on their shape, normalization beyond explicit no-trim, uniqueness comparison rules, or error-pointer syntax is made.
- Empty-group representation and whether clear immediately applies versus edits a draft are not specified here. Preserve the explicit unapplied-draft boundary without choosing a product interaction.
- Jira capture omits comments, attachments and custom acceptance fields. Wiki is flattened textContent; original attachment was not fetched/executed. No live-source freshness claim or prototype visual behavior verification.
- Accepted membership is observed hierarchy membership, not inferred from empty parent/subtask fields or proof against hidden issues. B is secondary bounded ownership evidence; its plans, journal source and hash were not independently rechecked.
- No affected supported conclusion needed to stop; unknown details remain unselected, not automatic new blockers. Independent parent review/registry integration still required.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped all seven MOS-1258 AC to C1–C10 with exact JSON-string locators and quotes, scoped wiki differences, ownership boundaries and actual read coverage."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/b3601c18-e859-4cb1-a7c8-e4c6228c3213/req-1258.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [],
  "validationOutput": ["Manual source-to-table coverage: AC1 C1; AC2 C2/C3; AC3 C5; AC4 C6; AC5 C7/C8; AC6 C7/C9/C10; AC7 C2/C3/C4/C10.","No network, execution, tests, code/API/plan analysis or project edits performed."],
  "residualRisks": ["Flattened saved snapshots and omitted Jira evidence limit completeness beyond the assigned prose.","Metadata compatibility, serialization, empty-group and clear/apply details remain unspecified; no policy selected."],
  "diffSummary": "External report only; no repository edits or staging operations.",
  "reviewFindings": ["No material missing input for bounded extraction; independent review remains pending."],
  "manualNotes": "Read complete assignment and complete item9 description/AC. Broader JSON strings were incidentally returned as disclosed; registry/saved-filter requirements were not re-extracted. Hashes parent-attributed only. No git/index inspection performed."
}
```
