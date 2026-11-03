# REQ-MOS-959 — fresh configurator requirements extraction

## Code Context / Files Retrieved

All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/` (A).

1. `work-items/REQ-MOS-959.md`, lines 1–7: bound scope and acceptance.
2. `sources/jira-api-delta-scenarios/r1/content.json`, lines 43–69, ONLY `/items/2` (MOS-1237) and `/items/3` (MOS-959); `metadata.json`, lines 1–8.
3. `sources/wiki-245673187/r1/content.json`, single logical line 1: `/bodyView`, heading outline first, then only configuration-related sections identified below; `metadata.json`, lines 1–14.
4. `reviews/R-SURFACE-CONFIG.md`, lines 1–111: optional secondary question-finding context only, not authority for extracted requirements or API claims.

Jira capture: 2026-10-16T11:23:51.742Z, selected description/attachment metadata, no comments/custom fields/attachment bodies. MOS-959 is `Backlog`; MOS-1237 is `Ready for test` (respective `/status` pointers). Wiki: version 18, versionWhen 2026-10-09T23:34:11.543+08:00, retrieved 2026-10-16T11:45:08.223Z. HTML was parsed as inert text only. No attachments or linked contracts were opened. Source precedence is not selected.

## Exact locator key

Each W locator is within the wiki `/bodyView` at line 1; use the exact heading ID and table row label/field below, not rendered line numbers. Table numbering is preserved, including the source's `0` row.

- **W-C**: `Функциональные требования → Карточка поверхности → Вкладка "Конфигуратор"`, heading ID `id-Бизнесанализ:Поверхности-Вкладка"Конфигуратор"`.
- **W-G**: same parent, `Общие для всех вкладок`, ID `id-Бизнесанализ:Поверхности-Общиедлявсехвкладок.1` (not registration's similarly named section).
- **W-D**: `4. Справочники раздела → 4.3. Состав справочников и значения`, ID `id-Бизнесанализ:Поверхности-4.3.Составсправочниковизначения`.
- **W-J**: `5. Структура JSON-полей → 5.1. surfaces.configuration`, ID `id-Бизнесанализ:Поверхности-5.1.surfaces.configuration`.
- **W-K**: same parent, `5.2. surfaces.configuration.cards[]`, ID `id-Бизнесанализ:Поверхности-5.2.surfaces.configuration.cards[]`.
- **J959**: Jira `/items/3/description`, key verified at `/items/3/key`.
- **J1237**: Jira `/items/2/description`, key verified at `/items/2/key`.

## Key requirements — stable candidate IDs, not activated scope

Each row is an independently traceable candidate requirement. Quotes are primary-source excerpts; they do not assert implementation.

| ID | Atomic requirement / exact evidence |
|---|---|
| REQ-MOS-959-001 | Show appearance controls for accent, shape, font. W-C #1: «настройки акцентного цвета, формы элементов и шрифта»; J959: «акцентный цвет, форму элементов, шрифт». |
| REQ-MOS-959-002 | Offer exactly the listed color presets. W-C #2: «#B3121B, #0B6B3A, #1E4FA3, #7A3E9D, #B5651D». W-D `surface_accent_colors` labels: Красный, Зелёный, Синий, Фиолетовый, Оранжевый respectively. |
| REQ-MOS-959-003 | Show manual HEX input. W-C #3: «поле ручного ввода HEX-значения»; accepted formats remain explicitly undecided (#26). |
| REQ-MOS-959-004 | Default shape to rounded. W-C #4: «по умолчанию "Скруглённая"». |
| REQ-MOS-959-005 | Offer dictionary shapes. W-C #5: «согласно справочнику форм»; W-D `surface_shapes`: `round`/«Скруглённая», `moderate`/«Умеренная», `strict`/«Прямая». |
| REQ-MOS-959-006 | Shape selection changes preview shape. W-C #4: «меняет форму элементов в блоке предпросмотра». |
| REQ-MOS-959-007 | Default font to Moscow Sans. W-C #6: «по умолчанию "Moscow Sans"». |
| REQ-MOS-959-008 | Offer dictionary fonts. W-C #7 and W-D `surface_fonts`: `moscow_sans`/«Moscow Sans», `system`/«Системный», `golos_text`/«Golos Text». |
| REQ-MOS-959-009 | Group content into greeting, quick suggestions, greeting cards. W-C #8: «"Приветствие", "Саджесты быстрых ответов", "Карточки экрана приветствия"». |
| REQ-MOS-959-010 | Greeting initial value is «Здравствуйте! Чем помочь?». W-C #9. |
| REQ-MOS-959-011 | Provide greeting insertion buttons for the three exact tokens. W-C #0: «"{имя}", "{отчество}", "{время суток}"»; W-J `greeting` confirms them. |
| REQ-MOS-959-012 | Include fallback greeting content. J959: «приветствие и fallback»; W-J `greeting_fallback`: «Резервный текст приветствия, если имя неизвестно». No editor placement/default/conditional validation is supplied here. |
| REQ-MOS-959-013 | Show suggestion add control. W-C #11: «с кнопкой "Добавить"». |
| REQ-MOS-959-014 | Empty suggestion list displays «Саджестов нет». W-C #12. |
| REQ-MOS-959-015 | Adding a suggestion creates a field with «Например: Когда отключат воду». W-C #13. This is an input hint, not a prescribed saved suggestion. |
| REQ-MOS-959-016 | Each suggestion has deletion control. W-C #14: «для каждого саджеста кнопку удаления». |
| REQ-MOS-959-017 | Limit suggestions to five and disable Add at the cap. W-C #15: «до 5; по достижении лимита кнопка "Добавить" блокируется»; J959 «до пяти»; W-J `suggestions` «не более 5». |
| REQ-MOS-959-018 | Show card add control. W-C #16: «с кнопкой "Добавить карточку"». |
| REQ-MOS-959-019 | Empty card list displays «Карточек нет: пользователь увидит только приветствие и саджесты». W-C #17. |
| REQ-MOS-959-020 | Adding a card creates title/subtitle fields with corresponding «Заголовок»/«Подзаголовок» placeholders and action selector. W-C #18: «и выбором действия». |
| REQ-MOS-959-021 | Each card has deletion control. W-C #19: «для каждой карточки ... кнопку удаления». |
| REQ-MOS-959-022 | Limit cards to four and disable Add card at the cap. W-C #20: «до 4; ... "Добавить карточку" блокируется»; J959 «до четырёх»; W-J `cards` «не более 4». |
| REQ-MOS-959-023 | Offer message action with value hint «Текст сообщения». W-C #21 «Отправка сообщения в чат»; W-D `surface_card_action_types` code `message`. |
| REQ-MOS-959-024 | Offer link action with value hint «Адрес страницы». W-C #21 «Переход по ссылке»; W-D code `link`. |
| REQ-MOS-959-025 | Offer skill action with value hint «Навык». W-C #21 «Запуск навыка»; W-D code `skill`. W-K `action.value` says «код навыка», without defining its syntax. |
| REQ-MOS-959-026 | Preview has Greeting and Dialog tabs. W-C #22: «"Приветствие" и "Диалог"»; also J959. |
| REQ-MOS-959-027 | Greeting preview shows substituted greeting, suggestions and cards with selected styling/color/font. W-C #23: «с подстановкой моковых значений» and «с учётом выбранных оформления, цвета и шрифта». |
| REQ-MOS-959-028 | Dialog preview shows message bubbles, assistant greeting first with mock substitutions, then suggestions. W-C #24: «первое сообщение от ассистента содержит приветствие ... далее ... саджесты». |
| REQ-MOS-959-029 | Preview updates without saving. W-C #25: «в предпросмотре без сохранения». |
| REQ-MOS-959-030 | Populate preview substitutions explicitly with examples. J959: «подстановки заполняются явно примером». Neither source supplies the actual sample name/patronymic/time values. |
| REQ-MOS-959-031 | Configurator is the default surface-card tab. W-G #7: «открывает вкладку "Конфигуратор" по умолчанию». This is candidate UI evidence, not permission to undo deferral. |
| REQ-MOS-959-032 | Display Save changes when there are unsaved changes. W-G #13: «кнопку "Сохранить изменения" при наличии несохранённых изменений». No dirty-state equality algorithm is specified. |
| REQ-MOS-959-033 | Configuration changes are described as requiring no surface release/re-embedding. W-G #14 informational text: «Изменения конфигурации применяются без релиза поверхности, повторное встраивание кода не требуется». Not evidence of deployment or exact save/apply timing. |
| REQ-MOS-959-034 | Add validation for greeting values. J1237 lists `"greeting"`; motivation: «пропускает пустое значение или пробел». |
| REQ-MOS-959-035 | Add validation for fallback values. J1237 lists `"greeting_fallback"`; no exception/condition algorithm is stated. |
| REQ-MOS-959-036 | Add validation for suggestions. J1237 lists `"suggestions"`; does not distinguish list-level versus item-level rules. |
| REQ-MOS-959-037 | Add validation for card title. J1237 `"cards"` fragment lists `"title"`. |
| REQ-MOS-959-038 | Add validation for card subtitle. J1237 `"cards"` fragment lists `"subtitle"`. |
| REQ-MOS-959-039 | Add validation for card action value. J1237 `"cards" → "action" → "value"` fragment. These are literal description fields, not nested JSON pointers into the capture. |

## Architecture / data evidence boundaries

W-J identifies `SurfaceConfiguration` (`jsonb`): `accent_color`, `shape`, `font`, `greeting`, `greeting_fallback` are strings; `suggestions` is `array[string]`; `cards` is `array[object]`. Every field's obligation cell is «нет». W-K identifies `SurfaceConfigurationCard`, with string `title`, `subtitle`, `action.type`, `action.value`, also all «нет». W-K summarizes action values as «текст сообщения, код навыка или ссылка». These are wiki data-model statements, not an update-request schema or proof that an incomplete save is permitted.

Appearance dictionaries feed controls; editable content feeds two unsaved previews. W-J explicitly lists appearance/content/preview as uses of configuration. Save-button visibility is specified separately. No request sequencing, endpoint invocation, state library, preview service, real action execution or runtime validation behavior follows from this extraction.

## Disagreements, omissions and unresolved choices

1. **Exact placeholders: newly supplied wiki evidence, not source override.** J959 flags «в API не определены: точные имена плейсхолдеров приветствия в доступном текстовом экспорте контракта». W-C #0 and W-J `greeting` explicitly name all three. This is an API-export availability concern versus positive wiki UI vocabulary, not conflicting token sets. No API was re-audited. W-C #23 literally contains `{время суток)` (missing closing brace); preserve this textual defect, do not infer a fourth token or repair parser rules from it.
2. **Explicitly unresolved color validation.** W-C #26 starts «Требует уточнения» and asks whether arbitrary values or only presets are allowed and which formats: «6-символьный HEX, с # или без». Manual input (#3) is definite; its accepted domain is not. No chosen regex, normalization, case handling or default accent color is established by these scoped sources.
3. **Preview examples remain unspecified.** Jira requires explicit examples; wiki requires mock substitution. These agree at intent level. Exact persona/time examples, whether samples are editable, time-of-day mapping, fallback preview selection, action interactivity and whether links/messages/skills execute remain absent. No live resident data or real skill execution is authorized.
4. **Fallback editor gap, not rejection.** Jira requires fallback and W-J explains its use when name is unknown, but W-C does not describe a fallback field. Decide layout/help/defaults and preview representation separately; do not silently remove fallback or claim unconditional requiredness.
5. **Validation detail absent; optionality is not empty-string permission.** J1237 identifies blank/space acceptance as a problem and requests validation; it provides no numeric text bounds or exact rejection algorithm. Wiki model says fields optional. Missing fields, empty strings and whitespace-only strings are distinct; this is unresolved layering, not sufficient proof of a direct contradiction. No inferred minimum/maximum text lengths, duplicate-suggestion rule, URL scheme, UUID format or cross-field fallback condition is imported from the earlier API review.
6. **Normalization:** no scoped statement trims content, defines Unicode length, lowercases values, deduplicates suggestions or orders normalization and validation. W-D's closing prose says dictionary values «приведены к формулировкам, которые показывает прототип»; this concerns displayed labels, not runtime input normalization.
7. **Stale skill references:** no scoped statement requires checking connected/deleted skills, retaining/removing stale cards, blocking skill disconnection or displaying recovery errors. W-K's «код навыка» is the full value description here. Stale-card remediation remains a product/contract follow-up, not an extracted requirement.
8. **Limits actually present:** five suggestions, four cards, preset colors, enumerated shapes/fonts/actions. No text length limits, reorder behavior, duplicate equality, greeting escaping/nesting/case policy or sample identity values appear in the selected requirements/data sections or the two issue descriptions.
9. **Save semantics bounded:** W-G #13 specifies visibility, not persistence method, partial/full replacement, defaults, dirty-state reset, cancel/navigation prompts, errors or unknown-outcome recovery. W-G #9 says sandbox click saves but marks the configuration audience «Требует уточнения» (all users, sender only, or configuration status only); #12 says publish saves. These are adjacent save dependencies only, not extracted lifecycle scope or authorization to implement those flows.
10. **No completion claim:** MOS-1237's test-plan attachment is metadata only at `/items/2/attachments/0`; its body was not inspected. `Ready for test` does not prove validation works. MOS-959 remains captured as `Backlog`.

## Start Here / scope disposition

Start with wiki W-C #0, #23–26 alongside J959: they add exact UI tokens and live-preview behavior while retaining explicit color and sample decisions. Use the candidate IDs above for subsequent planning; reconcile independently with the existing contract handoff only in an authorized follow-up.

Approved configurator deferral remains unchanged. This report neither activates MOS-959 nor chooses wiki/Jira/API precedence; it changes no implementation, spec, Jira state or lifecycle policy. Surface registry, general registration/lifecycle and unrelated skill management are excluded. Only directly relevant save references are retained. The optional prior review supplied question categories, not primary requirements. No input/infrastructure blocker was encountered.

## Verification and residual risks

Read-only local JSON selection and inert HTML heading/table parsing completed. Only this report was written. No network, MCP, browser, tests, generation, nested agents, source edits or status updates. No API or implementation inventory was repeated. Attachments, live behavior and out-of-scope source sections cannot settle the open choices here; the selected evidence is a historical capture, not production verification. Git index state was not inspected or changed by this work.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Extracted 39 stable candidate requirements with exact Jira JSON pointers and wiki heading/row locators; recorded source gaps, explicit color ambiguity, preview samples, normalization/stale-reference omissions and unchanged deferral."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-959.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read-only Python JSON selection and HTMLParser outline/selected-section inspection","result":"passed","summary":"Only MOS-959/MOS-1237 issue content and relevant wiki configuration/dictionary/data/save sections extracted; saved HTML not executed."},
    {"command":"wc -l and bounded numbered-line inspection of source JSON","result":"passed","summary":"Confirmed Jira 71 lines and wiki single logical JSON line without trailing newline; exact pointers/heading locators supplied."},
    {"command":"tests / browser / network / generation","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Fresh primary-source requirements extraction complete; no API re-audit or scope activation."],
  "residualRisks": ["HEX validation explicitly unresolved; preview sample values and action execution policy absent.","Validation/normalization and stale-reference policies cannot be derived from these scoped sources.","Attachment bodies and runtime correctness unverified; no source precedence selected."],
  "diffSummary": "Only the bound requirements report written.",
  "reviewFindings": ["No input blocker; fallback UI coverage and placeholder typo retained as source issues."],
  "manualNotes": "Primary sources inspected independently after wiki outline. Earlier review consulted only to identify missing question categories. Deferral preserved; git index not inspected."
}
```
