# REQ-G2-MOS-1260 — source-only extraction

Pending independent review and parent acceptance. Only survey list/card CSV export; no report subsystem, dialog export, implementation, API-contract comparison or product-precedence decision. Current assignment authorizes available Astra low, superseding historical Spark labels; no previous analytical report reused.

## Inspected evidence

Base `A = openspec/changes/reconcile-control-center-backlog/audit`.

- `A/work-items/G2-FEEDBACK-REQUIREMENTS-RESUME.md`: complete assignment.
- `A/sources/jira-feedback/r1/content.json`: lines 1–4 (container), 104–115 (complete zero-based item 11, MOS-1260, including entire description and all seven AC). Pointer `/items/11/description`, abbreviated **J** below; AC numbers denote ordered `#` paragraphs under `h3. Критерии приёмки`, not separate JSON properties. Identity `/items/11/key`; status Backlog is not implementation evidence.
- `A/sources/jira-feedback/r1/metadata.json`: complete. Selected-field snapshot retrieved 2026-10-16T11:17:16.813Z; comments, attachments and custom acceptance fields absent.
- `A/sources/wiki-247734813/r1/content.json`: complete saved JSON read (lines 1–137); semantically inspected export-related `/text` clauses: prototype §§3.6, 4.1, 6.1, 6.2, 6.5 and table §§3.1, 3.5–3.6; surrounding text supplies prototype context only. **W** below means `/text` plus exact quoted locator. Links inspected as saved metadata, not followed.
- `A/sources/wiki-247734813/r1/metadata.json`: complete; version 11, versionWhen 2026-10-12T17:21:31.204+08:00, retrieved 2026-10-16T11:17:53.564Z. Flattened body.view text; linked original attachment not fetched/executed.
- `A/reports/JIRA-MOS-1246.md`: complete membership inventory read; MOS-1260 is one of 11 observed members, not inferred from standard parent field. No hierarchy re-inventory.
- `A/summary.md`: complete; `A/decisions.md` lines 1–67: D-063 through D-070 complete. Existing accepted units not re-extracted; Q1 untouched; no global closure.

SHA-256 independently computed with `sha256sum`:

| Saved content | Expected | Actual / result |
|---|---|---|
| jira-feedback/r1 | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` (assignment and metadata) | same — MATCH |
| wiki-247734813/r1 | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` (metadata) | same — MATCH |

No missing/changed material input encountered. Snapshot integrity does not establish external freshness.

## Atomic Jira requirement rows

IDs are local extraction IDs, not delivered features. Actor is administrative export user unless a row explicitly names frontend/backend. Trigger is list/card export unless narrowed. “Not specified” means no additional error behavior/limit in that clause; shared error requirements R21–R29 still apply. Each locator is within J.

| ID | Actor / trigger → required behavior; error or limit | Exact quoted locator |
|---|---|---|
| R01 | User requests export → actual CSV download, not a simulated success. | Description: “Добавить реальное скачивание CSV” |
| R02 | User selects columns → available columns and labels come from metadata export_fields. | AC1: “Колонки и подписи берутся из metadata export_fields” |
| R03 | User selects fields → at least one required. | AC1: “Минимум одно поле” |
| R04 | User selects fields → duplicates prohibited. | AC1: “без дублей” |
| R05 | User orders fields → fields order determines CSV column order. | AC1: “порядок fields задаёт порядок CSV” |
| R06 | List export → backend exports entire applied selection. | AC2: “Список выгружается сервером целиком по применённому search” |
| R07 | Paginated list export → current page and limit/offset do not constrain file. | AC2: “не по текущей странице; limit/offset не ограничивают файл” |
| R08 | List has unapplied conditions → exclude them from export. | AC2: “Неприменённые условия не попадают в экспорт” |
| R09 | Saved card export → exactly one saved record, without search. | AC3: “Карточка выгружает одну сохранённую запись без search” |
| R10 | New card without ID → export unavailable. | AC3: “Для новой без ID export недоступен” |
| R11 | Dirty draft export → explicitly indicate file contains saved data. | AC3: “при dirty draft явно указано, что файл содержит сохранённые данные” |
| R12 | Backend produces file → CSV UTF-8 with BOM. | AC4: “Файл — серверный CSV UTF-8 с BOM” |
| R13 | Backend produces CSV → semicolon separator. | AC4: “разделителем «;»” |
| R14 | Successful download → filename from Content-Disposition. | AC4: “имя из Content-Disposition” |
| R15 | Frontend handles export → do not rebuild CSV. | AC4: “Фронтенд не пересобирает CSV” |
| R16 | Backend produces values → perform escaping. | AC4: “escaping и защита формул выполняются backend” |
| R17 | Backend produces values → perform formula protection. | AC4: “escaping и защита формул выполняются backend” |
| R18 | Export size limit → metadata export_max_rows, default 10000. | AC5: “Предел из metadata export_max_rows, по умолчанию 10000” |
| R19 | Empty selection → header-only file allowed. | AC5: “Пустой отбор допускает файл только с заголовками” |
| R20 | Limit exceeded → 422 EXPORT_LIMIT_EXCEEDED, no file. | AC5: “превышение — 422 EXPORT_LIMIT_EXCEEDED без файла” |
| R21 | JSON instead of CSV → handle without false file/success. | AC6: “Обработаны JSON/HTML вместо CSV” + “нет ложного файла/успеха” |
| R22 | HTML instead of CSV → handle without false file/success. | AC6: “Обработаны JSON/HTML вместо CSV” + “нет ложного файла/успеха” |
| R23 | Missing valid filename → handle without false file/success. | AC6: “отсутствие корректного имени” + “нет ложного файла/успеха” |
| R24 | 403 response → handle without false file/success. | AC6: “403/404/422” + “нет ложного файла/успеха” |
| R25 | 404 response → handle without false file/success. | AC6: “403/404/422” + “нет ложного файла/успеха” |
| R26 | 422 response → handle without false file/success (specific limit case R20). | AC6: “403/404/422” + “нет ложного файла/успеха” |
| R27 | Network failure → handle without false file/success. | AC6: “сеть” + “нет ложного файла/успеха” |
| R28 | Cancellation → handle without false file/success. | AC6: “отмена” + “нет ложного файла/успеха” |
| R29 | Owner changes → handle without false file/success; exact owner meaning not defined here. | AC6: “смена owner” + “нет ложного файла/успеха” |
| R30 | Frontend uses Blob URL → release it; timing unspecified. | AC6: “Blob URL освобождается” |
| R31 | UI export access → requires ManagedResource:export. | AC7: “UI требует ManagedResource:export и read” |
| R32 | UI export access → also requires read. | AC7: “UI требует ManagedResource:export и read” |
| R33 | Stage-one scope → nested questions excluded. | Description: “Вложенные вопросы, варианты, правила и ответы пользователей не экспортируются в первом этапе” |
| R34 | Stage-one scope → options excluded. | Same description quote as R33 |
| R35 | Stage-one scope → rules excluded. | Same description quote as R33 |
| R36 | Stage-one scope → user responses excluded. | Same description quote as R33 |
| R37 | Export scope → do not import unpublished dialog-export headers requirements. | AC7: “Не переносятся непубликуемые требования headers экспорта диалогов” |
| R38 | Verification obligation → unit/component coverage of entire selection larger than a page. | AC7: “Unit/component-тесты: весь отбор больше страницы” |
| R39 | Verification obligation → detail/dirty-draft coverage. | AC7: “detail/dirty draft” |
| R40 | Verification obligation → limit coverage. | AC7: “лимит” |
| R41 | Verification obligation → malformed-response coverage. | AC7: “malformed response” |
| R42 | Verification obligation → session-isolation coverage. | AC7: “session isolation” |

Source-only interface statement (not API validation or implementation recommendation): J description says “API prefix /api/control/api/v1/managed-resources: POST /feedback/surveys/export с fields/search; POST /feedback/surveys/{id}/export только с fields. Metadata — GET /feedback/metadata.” Its named dependencies are MOS-1249, MOS-1250, MOS-1251, MOS-1258; their contents were not inspected. Current field inventory “сейчас name/code/type_code/audience_type/status” is a snapshot qualification of metadata, not permission to hard-code a permanent whitelist.

## Wiki clauses — separately attributed, no precedence chosen

These are prototype-source requirements/behaviors, not silently merged into Jira AC. All W locators use `/text`.

| ID | Actor / trigger → source behavior; limits/ambiguity | Exact quoted locator |
|---|---|---|
| W01 | User clicks list Export → field-selection modal for fb_survey; validation unspecified. | §3.6: “Кнопка «⤓ Экспорт» - открывает модалку выбора полей (fb_survey).” |
| W02 | User clicks card Export → section-selection modal, broader than Jira stage one; unresolved mismatch, not adopted. | §4.1: “⤓ ЭкспортМодалка выбора разделов (fb_survey, fb_tag, fb_segment/fb_surface, fb_question, fb_question_option, fb_display_rule)” |
| W03 | User enters export modal → field/section checkboxes. | §6.2: “Экспорт списка/карточкиЧекбоксы полей/разделов, кнопка «Выгрузить»” |
| W04 | User enters export modal → “Выгрузить” action. | Same §6.2 quote as W03 |
| W05 | Export notification → bottom-right toast. | §6.1: “Появляются в правом нижнем углу на 2 секунды.” + “экспорт” in significant-actions list |
| W06 | Export toast → two-second duration; success timing/copy not defined. | Same §6.1 quote as W05 |
| W07 | User presses Esc in modal → close modal; in-flight cancellation unspecified. | §6.5: “Esc - закрыть модалку.” |
| W08 | User clicks backdrop → close modal; in-flight cancellation unspecified. | §6.5: “Клик по бэкдропу - закрыть модалку.” |

Additional boundary evidence: table §3.1 “модалка экспорта - состав полей выгрузки.” confirms survey-field relevance. Table §3.5 mentions “экспорт - выгрузка результатов” but also “Состав полей и перечень статусов подлежат уточнению.” Table §3.6 mentions “экспорт - выгрузки и аналитика ответов.” Those are broader model references, not authorization to add results/report export to this unit; Jira explicitly excludes responses at stage one. Demo arrays, local DATA storage and linked prototype attachment are not production/export implementation requirements.

## Unresolved questions and limits

1. Wiki card section selection includes tags, segments/surfaces and nested entities; Jira describes metadata columns and explicitly excludes questions/options/rules/responses at stage one. No source-precedence choice made. Whether any wiki-only section selection or prototype toast/modal details carry forward remains unresolved; no expanded export scope inferred.
2. “смена owner” is undefined in item11: session isolation is explicitly tested, but whether owner means authenticated principal, resource owner, UI owner or another context cannot be conclusively derived here. No Q1 dependency or choice.
3. Correct filename criteria, malformed-content detection rules, error text, cancel UX, Blob URL cleanup timing, invalid/missing metadata handling and exact read permission identifier are not supplied by these clauses. Default row limit is stated; handling malformed limit values is not.
4. Column value representation (codes versus labels), row ordering and detailed CSV escaping/formula-protection policy are not defined here. Metadata controls column labels; that does not establish value transformation rules.
5. No comments/custom AC/attachment content, live freshness, backend availability, implementation completeness or full owning-plan coverage verified. These omissions do not prevent supported source-only extraction; no missing-input escalation needed.

No project edits, source execution, network/browser, credentials, tests/build or delegation. Test rows record requested future evidence, not executed tests. Only this external artifact was written. Parent acceptance and independent review remain pending; no register/feature/global-task closure.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Extracted 42 atomic Jira rows and 8 separately attributed prototype rows with exact description/text pointers and quoted locators; documented inspected scope, matching digests and unresolved questions."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/364fdded-cf7e-4946-9882-609bc8c11459/req-1260.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"sha256sum openspec/changes/reconcile-control-center-backlog/audit/sources/{jira-feedback,wiki-247734813}/r1/content.json","result":"passed","summary":"Both source hashes match expected saved values."}],
  "validationOutput": ["Complete assigned Jira description and seven AC inspected; source-only extraction, no runtime validation."],
  "residualRisks": ["Flattened wiki and absent comments/attachments/custom acceptance fields; live freshness unverified.","Wiki section export versus Jira stage-one scope remains attributed rather than resolved; owner semantics and response details remain unspecified."],
  "noStagedFiles": true,
  "diffSummary": "External report only; no project changes or staging actions.",
  "reviewFindings": ["No missing/changed material inputs; independent review and parent acceptance pending."],
  "manualNotes": "Self-attestation covers bounded extraction only, not parent acceptance. No code/API/full-plan review, tests, source execution or Q1 decision. No git staging inspection performed; no staging actions taken."
}
```
