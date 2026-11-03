# REQ-G2-MOS-1251 — editor requirements

Requirements extraction only; no implementation/API analysis or acceptance closure. All ten embedded AC covered below. D-066 remains in force: published **PUT**, despite quoted Jira PATCH wording; quotations below preserve source wording, not a proposal to change methods. **Q1 unknown-type options remains unselected**; continuation implies no decision.

## Files retrieved / actual read scope

Root `A = openspec/changes/reconcile-control-center-backlog/audit/` (all following paths relative to A):
- `work-items/G2-FEEDBACK-EDITOR-CONDITIONS.md`, complete, lines 1–23: assignment, constraints, parent-attributed hashes and dispositions.
- `sources/jira-feedback/r1/content.json`, lines 1–85 returned across two reads: complete assigned `/items/4` (lines 41–49; description line 48), plus adjacent items 0–8. Only item4 extracted as requirements; items2/5–8 used for dependency boundaries. Items9–11 not read.
- `sources/wiki-247734813/r1/content.json`, complete returned (lines 1–136): flattened `/text` is a single line 8, so full saved text was necessarily visible. Relevant clauses assessed: prototype §§2, 4.1–4.2, 4.4, 5.3, 6.2, 6.4, 7–9; model §§2.3–2.4, 3.1, 3.4. No question/preview/label requirements re-extracted.
- Both `sources/{jira-feedback,wiki-247734813}/r1/metadata.json`, complete lines 1–11: provenance/limits.
- `reports/JIRA-MOS-1246.md`, complete: accepted membership accounting only, not repeated inventory. MOS-1251 is an observed member, Development task, Backlog; empty subtasks are not evidence of absent hierarchy members.

Jira snapshot 2026-10-16T11:17:16.813Z; wiki v11, versionWhen 2026-10-12T17:21:31.204+08:00. SHA-256 values in assignment/metadata are **parent-attributed**, not independently computed. No audit history, plans, schemas, implementation, attachments or external links read; no network, execution, tests or project edits.

## Atomic editor requirements and exact source anchors

`J` = `A/sources/jira-feedback/r1/content.json#/items/4/description` (line 48). AC numbers below count the ten `#` paragraphs under `h3. Критерии приёмки`; they are textual locators, not separate JSON properties. `W` = `A/sources/wiki-247734813/r1/content.json#/text` (line 8). Quoted text is verbatim.

| ID / locator | Required editor behavior | Exact quote / supporting locator |
|---|---|---|
| E01 — J description, AC1 | Three tabs «Основное», «Форма», «Правила показа» share one draft/save. Load by UUID independently of registry. Edit name, code, type_code, description, owner, active_since, status, audience_type; require name/code/type; defaults draft/all; empty questions allowed. | «единым draft и сохранением»; «Карточка загружается по UUID независимо от реестра»; «Required: name/code/type; defaults draft/all; пустые вопросы допустимы.» |
| E02 — J AC2 | Name 1–255; code ≤100 and `^[a-z][a-z0-9_]*$`; owner ≤200; date YYYY-MM-DD. Server determines code uniqueness; no name-uniqueness constraint. | «Уникальность кода подтверждается сервером, уникальность названия не вводится.» |
| E03 — J AC3 | Segment requires labels; surface requires 1–100 UUID. Explain rejected 101st selection and retain set. Paginated surface retrieval; one surface_ids across both tabs. Without Surface:view do not request or invent names; hiding fields does not remove relations. | «При попытке выбрать 101-ю поверхность UI объясняет лимит и сохраняет текущий набор.»; «без Surface:view нет запроса/фиктивных названий. Скрытие поля само не удаляет связи.» |
| E04 — J description, AC4 | Preserve/display responsible_user_id read-only, without fabricated names; user chooser deferred to user API. Display/preserve inactive saved lookup codes; restrict new selection to active codes. | «сохранённый responsible_user_id доступен только для чтения»; «Неактивные сохранённые lookup-коды видны и сохраняются; новый выбор только активных.» |
| E05 — J AC5; W §4.4 | Expose trigger_type, min_messages, min_duration_sec, delay_show_sec, pause_after_last_sec, max_per_session, max_per_day, max_per_user, cooldown_sec, skip_if_rated, quiet_hours_enabled, quiet_from, quiet_to, dialog_type, dialog_result, priority, exclusive_show. | «Все display_rules доступны»; Jira abbreviates two fields as «dialog_type/result»; W §4.4 explicitly names «dialog_type» and «dialog_result». |
| E06 — J AC6 | Minimums/delays/cooldown: integers ≥0 or null; frequency limits ≥1 or null; priority integer or null. Enabled quiet hours require both timezone-free boundaries, including cross-midnight intervals. Explanation distinguishes zero/empty and describes settings, not execution. | «тихие часы требуют обеих границ без timezone и допускают интервал через полночь»; «Пояснение различает 0/пустое и описывает конфигурацию, не её выполнение.» |
| E07 — J AC7 | Preserve replacement semantics of submitted questions/relations/display_rules; changing one rule must not reset others. Successful create/read or update refreshes baseline and ID. Method wording subject to D-066 PUT, not new interpretation. | «PATCH частичен только сверху: переданные вопросы/связи и display_rules заменяются целиком.»; «Сохранение одного правила не сбрасывает остальные; POST→GET/PATCH обновляет baseline и ID.» |
| E08 — J AC8 | Tab changes preserve input; protect dirty navigation; pending blocks duplicate submission. Errors land on correct tab with focus and retain draft. Required component coverage: success, boundary validation, failure, complete three-tab save. | «Вкладки сохраняют ввод; dirty-уход защищён.»; «ошибки показываются на нужной вкладке с фокусом и не очищают draft.» |
| E09 — J AC9 | Preserve explicit GET null in priority, skip_if_rated, quiet_hours_enabled, exclusive_show, dialog_type, dialog_result, quiet_from/quiet_to. Show “Не задано” distinct from false/0/any; nullable fields explicitly clearable. Defaults only for new/missing fields, not persisted null; trigger_type nonnullable. Required regression: GET null → one delay set to 0 → full update → GET preserves other values. | «UI показывает «Не задано» отдельно от false/0/any»; «Defaults применяются к новой записи/отсутствующим полям, не заменяют сохранённый null; trigger_type не nullable.» |
| E10 — J AC10 | Saved-card transition to disabled requires confirmation through button and status-field/save paths. Cancel: no request, draft retained. Confirm: one update with all edits. Already-disabled editing without status transition needs no repeat confirmation. Shared integration with MOS-1256, not separate lifecycle re-extraction. | «Отмена не отправляет запрос и сохраняет draft; согласие отправляет один PATCH со всеми изменениями.»; «Для уже disabled без смены статуса повторное подтверждение не требуется.» |

## Relevant wiki clauses: support versus prototype-only evidence

All locators below resolve inside W, line 8; headings disambiguate the two separately numbered document sections.
- Prototype §2 / §4: three-tab card; §4.1 header includes name/description/status/active_since/code/owner and created_at/updated_at. This is supplementary wiki presentation evidence, not a new system-field editing requirement.
- Prototype §4.4: surfaces «синхронизированы с вкладкой «Основное» через fb_survey_surface»; “Как это сработает” is «динамический список, пересобирается на каждое изменение полей». It covers trigger, dialog type, message constraints, quiet hours, limits, cooldown, exclusivity and priority. This supports E03/E05/E06, without specifying trigger execution.
- Model §3.4: «Связь одна к одной с опросником»; groups/surfaces normalized into relations. Model §3.1: «параметры "Приоритет" и "Эксклюзивный показ" хранятся только в fb_display_rule». These are source context, not an independent schema redesign.
- Prototype §6.2: «Выйти без сохранения?»; §7: «Объект draft + массив DATA». Supports dirty-exit/shared draft intent; browser-memory DATA is prototype mechanism, not production persistence requirement.
- Do not import superseded prototype behaviors: §4.1/§6.4 name uniqueness versus J AC2; §4.2/§5.3 responsible-name chooser versus J read-only deferral; archived versus disabled (MOS-1256 description); dynamic generated codes versus labels owner MOS-1257. No new precedence decision is made.
- Prototype §9 says «опросник начнёт показываться по заданным правилам»; **J description explicitly bounds editor scope:** «API хранит настройки, но не исполняет триггеры и не отправляет опросники пользователям.» Wiki examples/demo DATA (§5.4 six surveys), literal client DATA persistence, and model §3.4 “пошаговым примером” do not establish runtime delivery or sample-setting requirements.

## Ownership / integration boundaries

Exact Jira pointers refer to the same saved source as J:
- **MOS-1251:** foundation, shared draft/baseline, general card and display-rule inputs, tab error focus, cross-tab save and E10 integration. J description: «Сначала foundation редактора; затем встраивание конструктора MOS-1254 и меток MOS-1257 для окончательной приёмки.» Foundation alone is not final editor acceptance.
- **MOS-1249** `/items/2/description`, line 30: existing HTTP/session, lookup/metadata and common error/permission integration. «Новая auth/session/RBAC-модель не входит в задачу.» Existing UI-policy supplies ManagedResource read/create/update/delete/export; backend checks global scope. Editor-specific surface guard is E03; do not invent a second auth model or additional access rules. Common transport error details remain dependency-owned; editor owns their presentation without losing input.
- **MOS-1254** `/items/5/description`, line 57: «Добавить в draft карточки редактирование вопросов и вариантов»; «Собственный API вопросов не создаётся.» Builder owns question/option mechanics and their errors; editor integrates its final state and tab navigation. Q1 remains undecided.
- **MOS-1255** `/items/6/description`, line 66: «Пробные ответы существуют только локально, отдельно от draft опросника»; depends on builder and shared editor draft. Preview rendering/answers are not editor-rule execution or persisted draft answers.
- **MOS-1256** `/items/7/description`, line 75: lifecycle/actions/deletion owner, depending on registry/editor. AC7 overlaps J AC10 and adds «Если отдельному действию предшествовало сохранение, уже установившее целевой статус, второй PATCH не нужен.» Integrate one confirmed outcome; do not duplicate lifecycle extraction or infer a new conflict from the save/action paths.
- **MOS-1257** `/items/8/description`, line 84: chips/labels owner inside shared card; «Это свободные метки, не lookup-коды.» Tags/segments/groups and serialization remain there; editor owns inclusion in shared save, audience prerequisites and relation preservation. No independent label CRUD inferred.
- **MOS-1250** `/items/3/description`, line 39: registry/routes/search owner, separate from independent UUID detail loading. MOS-1258 advanced search conditions are not display-rule conditions. Export remains MOS-1260 (accepted membership report only; its AC not read).

## Genuine unknowns and limits

- Q1 unknown-type options policy is still an explicit nondecision; no selection, suppression or preservation policy beyond accepted boundaries is inferred here.
- Exact per-field default values beyond draft/all and the new/missing-versus-null rule are not supplied by the assigned AC; no defaults guessed. Quiet-hour cross-midnight is explicit; equal-boundary meaning is not specified here.
- Snapshot excludes comments, attachments and custom acceptance fields. Wiki tables are flattened textContent; original HTML attachment was not fetched/executed, so layout/interaction fidelity cannot be independently attested. Saved membership does not prove absence of hidden/permission-filtered issues. These are retained evidence limits, not new automatic blockers.
- No material missing input blocks the ten-AC extraction. No conclusion is offered about runtime/API correctness, implementation completion, exact unseen designs, or release readiness. D-066 provenance is the assignment, not a reread of decision history.

## Start here

For review, open Jira `/items/4/description` (line 48), then W prototype §4.4 and model §3.4. Review E07/E09 under the preserved PUT disposition and E10 jointly with the lifecycle owner.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped all ten MOS-1251 AC to E01–E10 with exact JSON pointers and quoted textual locators; recorded scope, ownership and unresolved limits."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/b3601c18-e859-4cb1-a7c8-e4c6228c3213/req-1251.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [],
  "validationOutput": ["Manual source comparison: all ten embedded AC covered; Q1 unselected; D-066 PUT preserved."],
  "residualRisks": ["Saved selected-field Jira and flattened wiki only; comments/custom AC/attachments unavailable.","Q1 and unspecified defaults/equal quiet-hour boundaries not decided."],
  "noStagedFiles": true,
  "diffSummary": "External requirements report only; no project edits.",
  "reviewFindings": [],
  "manualNotes": "Read-only source extraction plus configured external artifact write; no network, tests, code/API analysis or acceptance closure. Hashes parent-attributed. No staging performed."
}
```
