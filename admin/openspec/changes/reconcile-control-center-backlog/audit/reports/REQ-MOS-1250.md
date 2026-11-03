# REQ-MOS-1250 — registry requirements extraction

## Evidence and scope

Only MOS-1250 and wiki registry/search/filter/list prose are used as requirement evidence. No source precedence is assigned. “Required” below means required by the named source, not an adjudicated combined scope. “Contradictory” identifies a source disagreement without resolving it.

Files retrieved (repository-relative):
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/REQ-MOS-1250.md`, lines 1–9: assignment.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-feedback/r1/content.json`, lines 1–100: extraction packet; only `$.items[3]`, identified by `key = "MOS-1250"`, is used. Requirement text is `$.items[3].description`; `summary`, `status`, `updated` identify the row. Other returned rows are not requirement evidence.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-feedback/r1/metadata.json`, lines 1–11: selected-field provenance and exclusions.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247734813/r1/content.json`, lines 1–70: wiki text is one JSON string at `$.text` (line 8). Only “2. Общая структура” list/navigation statements and “3. Экран «Список опросников»” subsections 3.1–3.6 are used below; unrelated text returned with the string is not analyzed.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247734813/r1/metadata.json`, lines 1–11: flattened-text provenance and attachment limitation.

Locator shorthand: **J** = Jira file above, `$.items[3].description`. **J-D** = heading `h3. Описание`; **J-A1…7** = numbered items under `h3. Критерии приёмки` (numbered by order of `#` lines). **W** = wiki file above, `$.text`, with heading and exact quote supplied per entry. These are text locators, not inferred JSON subsection keys.

Jira row updated `2026-10-16T18:44:42.569+0800`, status `Development`; packet retrieved `2026-10-16T11:17:16.813Z`. Wiki version 11, versionWhen `2026-10-12T17:21:31.204+08:00`, retrieved `2026-10-16T11:17:53.564Z`. These dates/statuses do not establish precedence or implementation readiness.

## Atomic Jira requirements

| Stable ID | Classification | Requirement | Precise locator / quote |
|---|---|---|---|
| REQ-1250-1 | Required — Jira | Provide the Feedback entry point and registry in the common shell. | J-D: “Добавить точку входа «Обратная связь», реестр” / “в общей оболочке”. |
| REQ-1250-2 | Required — Jira | Provide navigation to creation and detail. | J-D: “переходы в создание/карточку”. |
| REQ-1250-3 | Required — Jira | Mount `/feedback`, `/feedback/new`, `/feedback/:surveyId` under the existing basename. | J-D: “Маршруты /feedback, /feedback/new, /feedback/:surveyId под действующим basename.” |
| REQ-1250-4 | Required — Jira | Use the named server search endpoint. | J-D: “POST /api/control/api/v1/managed-resources/feedback/surveys/search”. |
| REQ-1250-5 | Required — Jira | Obtain feedback lookups via the named GET endpoint. | J-D: “GET /catalogs/lookups/feedback … относительно managed-resources”. |
| REQ-1250-6 | Required — Jira | Obtain feedback metadata via the named GET endpoint. | J-D: “и /feedback/metadata относительно managed-resources”. |
| REQ-1250-7 | Required — Jira | Display name/code, type, audience and status columns. | J-A1: “Таблица показывает название/код, тип, аудиторию и статус.” |
| REQ-1250-8 | Required — Jira | Resolve labels from lookup data. | J-A1: “Подписи из lookup”. |
| REQ-1250-9 | Required — Jira | Show unknown codes without invented replacements. | J-A1: “неизвестный код отображается без выдуманной замены”. |
| REQ-1250-10 | Required — Jira | Allow keyboard opening of a card. | J-A1: “Карточка открывается с клавиатуры.” |
| REQ-1250-11 | Required — Jira | Support server query length 2–200 characters. | J-A2: “Работают серверные query 2–200 символов”. |
| REQ-1250-12 | Required — Jira | Support status multiselect filtering. | J-A2: “мультиселекты status/type_code”. |
| REQ-1250-13 | Required — Jira | Support type_code multiselect filtering. | J-A2: “мультиселекты status/type_code”. |
| REQ-1250-14 | Required — Jira | Omit a cleared query. | J-A2: “Очищенный query исключается”. |
| REQ-1250-15 | Required — Jira | Do not send a one-character query. | J-A2: “один символ не отправляется”. |
| REQ-1250-16 | Required — Jira | Do not represent a one-character query as an applied search. | J-A2: “не выдаётся за применённый поиск”. |
| REQ-1250-17 | Required — Jira | Support server sorts name, type_code, status, updated_at and their minus-prefixed variants. | J-A3: “Сортировки: name, type_code, status, updated_at и варианты с минусом”. |
| REQ-1250-18 | Required — Jira | Default to `-updated_at`. | J-A3: “default -updated_at”. |
| REQ-1250-19 | Required — Jira | Do not substitute page-local sorting for server sorting. | J-A3: “Локальная сортировка только страницы не подменяет серверную.” |
| REQ-1250-20 | Required — Jira | Use API pagination with limit 1–100 and offset. | J-A4: “Пагинация limit 1–100/offset … берутся из API”. |
| REQ-1250-21 | Required — Jira | Take counters from the API. | J-A4: “и счётчики берутся из API”. |
| REQ-1250-22 | Required — Jira | Reset offset when selection changes. | J-A4: “Изменение отбора сбрасывает offset”. |
| REQ-1250-23 | Required — Jira | Prevent late responses from replacing current results. | J-A4: “поздние ответы не заменяют актуальные”. |
| REQ-1250-24 | Required — Jira | URL/history restores the complete applied search. | J-A5: “URL/history … восстанавливают полный применённый search”. |
| REQ-1250-25 | Required — Jira; contradictory to W 3.5's narrower link description | Copied links restore the complete applied search. | J-A5: “и копирование ссылки восстанавливают полный применённый search”. |
| REQ-1250-26 | Required — Jira, conditional future integration | Include conditions in restoration after MOS-1258. | J-A5: “включая conditions после MOS-1258”. |
| REQ-1250-27 | Required — Jira | Explain a damaged URL. | J-A5: “Повреждённый URL имеет пояснение”. |
| REQ-1250-28 | Required — Jira | Report clipboard success only after a successful write. | J-A5: “clipboard success только после успешной записи”. |
| REQ-1250-29 | Required — Jira | Distinguish loading. | J-A6: “Различаются loading, пустой реестр, отсутствие совпадений и error/retry.” |
| REQ-1250-30 | Required — Jira | Distinguish an empty registry from no matches. | J-A6: “пустой реестр, отсутствие совпадений”. |
| REQ-1250-31 | Required — Jira | Provide a distinct error/retry state. | J-A6: “error/retry”. |
| REQ-1250-32 | Required — Jira | Direct detail loading is independent of the current registry page. | J-A6: “Прямой detail не зависит от текущей страницы”. |
| REQ-1250-33 | Required — Jira | Do not interpret `new` as a survey ID. | J-A6: “new не трактуется как ID”. |
| REQ-1250-34 | Required — Jira | Cover multifilters, short/empty query, pagination, URL and error with unit/component tests. | J-A7: “Unit/component-тесты покрывают мультифильтры, короткий/пустой query, пагинацию, URL и ошибку.” Extraction only; no tests run. |
| REQ-1250-35 | Required — Jira | Use existing UI-policy for read access. | J-A7: “Read-доступ использует существующую UI-policy.” |

MOS-1250 explicitly owns basic filters and the common search/URL model (J-D: “Эта задача владеет базовыми фильтрами и общей моделью search/URL”). Its declared dependency is MOS-1249 (J-D: “Зависимости: MOS-1249”); no content or readiness of that issue is inferred.

## Explicit deferrals and prototype conflicts

Each row below records the Jira deferral separately; none is converted into a current implementation obligation.

| Stable ID | Classification | Jira locator | Relevant wiki comparison |
|---|---|---|---|
| REQ-1250-36 | Deferred — Jira; contradictory scope | J-D: “Поиск по тегам/сегментам/поверхностям/названию типа … отложены”, tags portion. | W “3.2. Поиск”: “тегам (fb_tag.display_name)” is included in prototype search. |
| REQ-1250-37 | Deferred — Jira; contradictory scope | Same J-D sentence, segments portion. | W 3.2: “сегментам (fb_segment.display_name)”. |
| REQ-1250-38 | Deferred — Jira; contradictory scope | Same J-D sentence, surfaces portion. | W 3.2: “поверхностям (surfaces.display_name)”. |
| REQ-1250-39 | Deferred — Jira; contradictory scope | Same J-D sentence, type-name portion. | W 3.2: “отображаемому названию типа”. Type-code multiselect remains separately required by J-A2; this is not a deferral of that filter. |
| REQ-1250-40 | Deferred — Jira; contradictory scope | J-D: “сортировка аудитории … отложены”. | W “3.1. Таблица”, flattened table row: “Аудиторияfb_survey.audience_type + fb_survey_segment / fb_survey_surface✓” (whitespace normalized here); checkmark is in the “Сортировка” column. |
| REQ-1250-41 | Deferred — Jira; contradictory scope | J-D: “отдельный независимый фильтр аудитории отложены”. | W “3.3. Мультиселект-фильтры”: “Три выпадающих фильтра с чекбоксами (мультивыбор)” and “Вся аудитория”. This does not defer display of the audience column. |
| REQ-1250-42 | Deferred to MOS-1258 — Jira; broader prototype scope | J-D: “расширенные conditions добавляются в MOS-1258”. | W “3.4. Расширенный фильтр «⚙ Условия»”: “Открывает панель с конструктором произвольных условий”. Prototype includes И/ИЛИ, fields/operators, add/remove/clear, applied bar and badge; not extracted as MOS-1250 implementation requirements. Future URL preservation remains REQ-1250-26. |

Additional URL disagreement: W “3.5. Меню «⋮»” states “Скопировать ссылку на отбор - формирует URL с параметрами q, status, type и копирует в буфер.” J-A5 requires complete applied search, explicitly including future conditions. The documented three-parameter copy description is narrower. Neither text establishes actual attachment behavior; no encoding scheme or resolution is chosen.

## Relevant wiki-only or corroborating registry requirements

These are required by prototype prose only unless Jira corroboration is stated. Absence in MOS-1250 is not labeled a deferral or contradiction.

| Stable ID | Classification | Atomic requirement and exact W locator | Jira relation |
|---|---|---|---|
| REQ-1250-43 | Required — wiki | Start on the survey list: “2. Общая структура”: “Список опросников - стартовый экран с таблицей, поиском, фильтрами и кнопкой создания.” | Corroborates registry entry. |
| REQ-1250-44 | Required — wiki | Open a card by clicking its row: W 2: “по клику на строку таблицы (открыть)”. | Adds mouse navigation detail; Jira explicitly adds keyboard access. |
| REQ-1250-45 | Required — wiki | Return using breadcrumbs: W 2: “по хлебным крошкам (вернуться)”. | Not specified in MOS-1250. |
| REQ-1250-46 | Required — wiki | Include the trailing arrow column: W 3.1: “Стрелка «›»”. | Jira names only the four business columns. |
| REQ-1250-47 | Required — wiki | Color statuses: W 3.1: “Активен - зелёныйПриостановлен - жёлтыйЧерновик - светлыйВыключено (код archived) - серый”. | Jira requires lookup labels, not fixed colors/codes. No disabled-versus-archived conflict can be established from MOS-1250 alone. |
| REQ-1250-48 | Required — wiki | Search names: W 3.2: “Поле поиска (минимум 2 символа) ищет по:названию”. | Jira corroborates minimum length, does not enumerate query fields. |
| REQ-1250-49 | Required — wiki | Search service codes: W 3.2: “служебному коду”. | Query field coverage unspecified in MOS-1250. |
| REQ-1250-50 | Required — wiki | Search descriptions: W 3.2: “описанию”. | Query field coverage unspecified in MOS-1250. |
| REQ-1250-51 | Required — wiki | Show each filter value's code in monospace: W 3.3: “У каждого значения рядом с названием выводится код (monospace).” | Not specified in MOS-1250. |
| REQ-1250-52 | Required — wiki | Clear a multiselect via its All button: W 3.3: “Кнопка «Все ...» очищает фильтр.” | Jira supports status/type multiselects without prescribing this affordance. |
| REQ-1250-53 | Required — wiki | Show Reset only when filters are active: W “3.6. Прочее”: “Кнопка «Сбросить» - видна, только если есть активные фильтры.” | Not specified in MOS-1250. |
| REQ-1250-54 | Required — wiki | Show found-count at the right: W 3.6: “Счётчик справа - сколько опросников найдено.” | Jira requires API-derived counters; no position specified. |
| REQ-1250-55 | Required — wiki | Create opens an empty card with defaults: W 3.6: “Кнопка «＋ Создать опросник» - открывает пустую карточку с дефолтными значениями.” | Jira requires creation navigation; form defaults not in this assignment. |
| REQ-1250-56 | Required — wiki | Empty registry prompts creation: W 3.6: “Пустое состояние - подсказка создать первый опросник.” | Jira additionally distinguishes no matches, loading and error/retry. |

W 3.1 corroborates name/code, type, audience and status columns and sorting for name/type/status. W 3.3 corroborates status/type multiselects but its “5 типов опросников” is prototype content, not a fixed Jira requirement. Relevant wiki sections do not specify pagination, limit/offset, default sort, stale-response protection, history restoration, malformed URL treatment or clipboard failure handling. This is missing detail, not evidence of opposing behavior.

Boundary only: W 3.5 also describes “Сохранить текущий фильтр” and “Сохранённые фильтры”; W 3.6 describes “Кнопка «⤓ Экспорт»”. These are not basic search/URL/pagination requirements and are not expanded here. MOS-1250 itself does not explicitly defer these features or name their owners; ownership must not be inferred from other Jira rows.

## Evidence limits and residual risks

- Jira metadata describes a selected-field extraction; comments, attachments and custom acceptance fields are absent and were not inspected. Standard description criteria above are not a substitute for those missing materials.
- Wiki metadata describes `body.view` textContent and links extraction. Tables are flattened; original HTML prototype attachment was linked but not fetched, read or executed. Comparisons are to wiki descriptions of the prototype, not observed runtime behavior.
- No implementation, API schema, other OpenSpec content or other Jira issue requirements were analyzed. Endpoint statements are source requirements, not claims that a backend exists or is ready.
- MOS-1250 does not specify URL parameter encoding, pagination defaults, exact invalid-URL recovery, query trimming/debounce or query matching fields. Do not invent these details from the limited evidence.
- No source precedence decisions, tests, network/MCP calls, generation or nested agents. Only this authorized report was written; no source edits.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Extracted REQ-1250-1 through REQ-1250-56 with exact JSON row/text locators, explicit deferrals, unresolved prototype disagreements and evidence limits."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-1250.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [],
  "validationOutput": ["Manual source comparison limited to MOS-1250 and relevant wiki list sections; no executable validation requested or run."],
  "residualRisks": ["Comments/custom acceptance fields/attachments unavailable or not inspected.","Prototype behavior is represented by flattened wiki prose, not verified attachment execution.","Source disagreements remain unresolved; no precedence selected."],
  "noStagedFiles": true,
  "diffSummary": "Wrote only the authorized requirements report; no implementation changes.",
  "reviewFindings": [],
  "manualNotes": "Requirements extraction only. No staging operations performed; repository staging state was not inspected. Other rows/sections returned by packet reads were excluded from requirement analysis."
}
```
