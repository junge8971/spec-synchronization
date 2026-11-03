# REQ-G2-MOS-1256 — lifecycle requirements extraction

Requirements-only candidate; parent acceptance and independent review pending. No implementation, API-contract or plan assessment. Current assignment authorizes available Astra low; historical Spark labels/failure are not analytical evidence.

## Inspected evidence and integrity

Base `A = openspec/changes/reconcile-control-center-backlog/audit`.

- Complete assignment: `A/work-items/G2-FEEDBACK-REQUIREMENTS-RESUME.md`.
- **J**: `A/sources/jira-feedback/r1/content.json`, lines 1–4 and 68–76: complete zero-based `/items/7`, MOS-1256, including description and all seven embedded AC. Other issue descriptions not inspected. `/items/7/status = Backlog` implies no implementation conclusion.
- **W**: `A/sources/wiki-247734813/r1/content.json`, lines 1–136 (whole saved extraction, including flattened `/text` and links). Semantic extraction limited to prototype §§3.1, 4.1–4.2, 5.1, 6.1–6.2, 7–9 and model §§3.1, 5.3 for lifecycle context. Other text read incidentally, not audited.
- Both complete `r1/metadata.json`; `A/reports/JIRA-MOS-1246.md` complete for accepted observed membership; `A/summary.md` complete; `A/decisions.md` lines 1–67 (D-070 through D-063).
- `sha256sum` verified J content **890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685**, matching assignment and metadata. W content **d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7**, matching metadata.
- Computed metadata hashes: J **5c8df75fde70960ff15b33d6e6d3cc6c57b9d06daeee383076c753101f94fa70**; W **b71995990f608abc716382b67f54a812322da9c4d2b62c8a78ee1835cdc0e49e**. No independent expected metadata digests supplied.
- J retrieved 2026-10-16T11:17:16.813Z; item updated 2026-10-12T21:13:38.503+0800. W retrieved 2026-10-16T11:17:53.564Z, version 11, versionWhen 2026-10-12T17:21:31.204+08:00. These are retained snapshots, not freshness checks.

## Atomic requirement rows

Every **J/ACn** locator below means exact JSON pointer `/items/7/description` in J, nth numbered criterion under `h3. Критерии приёмки`, followed by a verbatim quoted substring. AC numbering is a textual locator, not a fabricated JSON child. Actor is the existing administrative UI user managing a **saved survey**, unless row specifies system/test responsibility. “Not specified” means not established by this packet, not permission to invent behavior. Method words below transcribe Jira only: D-066 explicitly retains published PUT and classifies Jira PATCH as a historical discrepancy; this report authorizes neither method substitution nor API design.

| ID | Actor / trigger → required behavior; error or limit | Exact locator / quote |
|---|---|---|
| 1256-R01 | UI / status selection → use lookup status codes draft, active, paused, disabled; unknown-code policy not specified. | J/AC1: “Коды статусов берутся из lookup: draft/active/paused/disabled.” |
| 1256-R02 | User / pause → status-change operation (Jira calls it PATCH); prototype identifies active→paused. | J/AC1: “Приостановка и возобновление — PATCH”; W `/text`, §4.1: “Переключает status между paused и active” |
| 1256-R03 | User / resume → status-change operation (Jira calls it PATCH); prototype identifies paused→active. | Same exact J/AC1 and W §4.1 quotes as R02. |
| 1256-R04 | User / switch off → send disabled, not archived. | J/AC1: “«Выключить» отправляет disabled, не archived.” |
| 1256-R05 | System / disabled survey → remains available in CRUD; not equivalent to deletion. | J/AC2: “disabled остаётся доступным в CRUD” |
| 1256-R06 | User / delete → soft deletion, distinct from switch-off; no restore method. | J/AC2: “DELETE — soft-delete без метода восстановления.” |
| 1256-R07 | User / switch-off → confirmation required. Both entry paths refined in R19–R20. | J/AC2: “Выключение и удаление требуют подтверждения.” |
| 1256-R08 | User / delete → confirmation required separately from switch-off. Dialog wording/cancel details not supplied. | J/AC2: “Выключение и удаление требуют подтверждения.” |
| 1256-R09 | User / lifecycle action with dirty draft → explicitly save first or cancel action. No silent discard mandated. | J/AC3: “При dirty draft сначала явное сохранение либо отмена действия.” |
| 1256-R10 | System / save error → retain user input. | J/AC3: “Ошибка сохранения/операции не уничтожает ввод.” |
| 1256-R11 | System / lifecycle operation error → retain user input. | J/AC3: “Ошибка сохранения/операции не уничтожает ввод.” |
| 1256-R12 | System / pending operation → prevent double submission. | J/AC4: “Pending исключает двойную отправку” |
| 1256-R13 | System / lifecycle request → no automatic retries. | J/AC4: “автоматических повторов нет.” |
| 1256-R14 | System / confirmed success → update detail. Unknown outcome is not confirmed success. | J/AC4: “После подтверждённого успеха обновляются detail, реестр и счётчики.” |
| 1256-R15 | System / confirmed success → update registry. | J/AC4: “После подтверждённого успеха обновляются detail, реестр и счётчики.” |
| 1256-R16 | System / confirmed success → update counters. Which counters not enumerated. | J/AC4: “После подтверждённого успеха обновляются detail, реестр и счётчики.” |
| 1256-R17 | System / post-deletion repeated DELETE, detail or export returns 404 → do not report current operation as successful. Export mentioned only at deletion boundary. | J/AC5: “404 повторного DELETE/detail/export после удаления не выдаётся за успех текущей операции.” |
| 1256-R18 | System / deleted survey → its code remains occupied. | J/AC5: “Код удалённого опросника остаётся занят.” |
| 1256-R19 | User / saved survey→disabled via button → mandatory confirmation. | J/AC7: “Подтверждение перехода сохранённого опросника в disabled обязательно через кнопку и через поле статуса + «Сохранить».” |
| 1256-R20 | User / saved survey→disabled via status field + Save → mandatory confirmation. | J/AC7: same complete quoted sentence as R19. |
| 1256-R21 | User / cancel disabled-transition confirmation → leave draft, send no request. Exact rollback of selected status not stated. | J/AC7: “Отмена оставляет draft без запроса” |
| 1256-R22 | User / agree during form save → one mutation containing status and other changes; Jira calls it PATCH. | J/AC7: “согласие при сохранении формы отправляет один PATCH со статусом и остальными изменениями.” |
| 1256-R23 | System / preliminary save already set separate action’s target status → no second status mutation needed. | J/AC7: “Если отдельному действию предшествовало сохранение, уже установившее целевой статус, второй PATCH не нужен.” |
| 1256-R24 | User / edit already-disabled survey without status change → no repeat disabled confirmation. | J/AC7: “Редактирование уже disabled без смены статуса повторного подтверждения не требует.” |
| 1256-R25 | UI / status change → requires ManagedResource:update. No new permission model inferred. | J/AC6: “Смена статуса требует ManagedResource:update” |
| 1256-R26 | UI / deletion → requires delete in existing UI. Source abbreviates permission name. | J/AC6: “удаление — delete в существующем UI.” |
| 1256-R27 | Component verification / lifecycle → distinguish disabled from delete. | J/AC6: “Component-тесты: disabled против delete” |
| 1256-R28 | Component verification / lifecycle → cover confirmation. | J/AC6: “подтверждение” |
| 1256-R29 | Component verification / lifecycle → cover dirty draft. | J/AC6: “dirty draft” |
| 1256-R30 | Component verification / lifecycle → cover 404. | J/AC6: “404/409” |
| 1256-R31 | Component verification / lifecycle → cover 409; precise user recovery not specified. | J/AC6: “404/409” |
| 1256-R32 | Component verification / lifecycle → cover unknown outcome; reconciliation mechanism not specified. | J/AC6: “неизвестный исход.” |
| 1256-R33 | Component verification / disabled transition → cover both button and field+Save paths. | J/AC7: “Component-тесты покрывают оба пути” |
| 1256-R34 | Component verification / disabled confirmation → cover cancellation. | J/AC7: “отмену” |
| 1256-R35 | Component verification / disabled transition → cover single request. | J/AC7: “один запрос” |
| 1256-R36 | Component verification / editing → cover unchanged disabled status. | J/AC7: “неизменённый disabled.” |

## Wiki evidence classification (not new product precedence)

All locators are W `/text`; headings disambiguate flattened clauses.

- Prototype §4.1: “В архивУстанавливает status = 'archived' (отображается как «Выключено») с подтверждением”; §6.2: “Подтверждение архивацииconfirm() - стандартный браузерный”. Supports historical confirmation intent, not a requirement to implement browser `confirm()`. J description explicitly says “Статус archived из прототипа заменён контрактным disabled.” Thus retain prototype discrepancy, do not resurrect archived.
- Prototype §4.2: “Статусselect из fb_statuses”; §5.1: “DICT_STATUSESfb_statuses4 (Черновик, Активен, Приостановлен, Выключено)”. Supports lookup-based status selection, not a hardcoded runtime dictionary.
- Prototype §8: “Soft delete (deleted_at) - поле присутствует в структуре, но кнопки удаления нет (только архивация).” This is a prototype limitation, not a ban on J’s separate delete action. Model §3.1: “deleted_atdatetimeнет-Дата мягкого удаления” supports soft-delete vocabulary, not verified backend behavior.
- Prototype §7 says archived’s code “остался стабильным”; model §5.3 has “fb_statusesarchivedАрхивfb_survey.status”. These conflict with J’s explicit disabled replacement; no broader precedence decision is made.
- Prototype §6.1: “Появляются в правом нижнем углу на 2 секунды” and “Сопровождают все значимые действия: добавление/удаление вопроса, варианта, ссылки, тега, сохранение, смена статуса, экспорт, применение фильтра.” Historical status-change toast behavior only; whether placement/duration are production requirements is not established by MOS-1256. No toast for failed/unknown operation inferred.
- Prototype §9: “При необходимости - «Приостановить» или «В архив».” Example flow, not exhaustive transition matrix. Prototype status colors, in-memory DATA, close-navigation behavior and demo records are not promoted into lifecycle requirements here.

## Boundaries and unresolved questions

1. No complete allowed-transition matrix: activation from draft, transitions out of disabled, and other from/to combinations are not established. Do not infer arbitrary transition permission from four lookup codes.
2. Jira’s PATCH wording is recorded, not implemented/reconciled here. Existing D-066 disposition retains published PUT; authoritative API evidence was deliberately not reopened. Description’s endpoint text was read but no API analysis performed.
3. Exact 409 handling, unknown-outcome reconciliation/manual retry, pending lifetime and user-facing error copy are absent. Required input retention, no automatic retry, no double submit and no false 404 success remain supported independently.
4. Confirmation text, delete cancellation specifics, and exact draft field state after canceling disabled confirmation are not supplied. “Отмена оставляет draft” is not a license to reset draft or silently discard edits.
5. Detail behavior/navigation after successful deletion and identities of refreshed counters are not specified. No fabricated post-delete detail fetch required.
6. UI deletion permission is written as `delete`, unlike fully qualified `ManagedResource:update`; exact permission-key expansion is not independently verified.
7. MOS-1250/MOS-1251 are named dependencies at J `/items/7/description`: “Зависимости: MOS-1250, MOS-1251.” Their scenarios are not re-extracted. No dependency on unresolved Q1 is introduced and no preserve/omit/block choice made.
8. Comments, attachments and custom acceptance fields are not included in J capture; wiki tables are flattened, linked attachment not fetched/executed, autolinks not evidence. These known capture limits do not indicate a changed/missing assigned material input; no stop was triggered. No live completeness/freshness claim.

Only lifecycle/deletion requirements extracted; accepted 1254/1255/1257/1259 units not repeated, MOS-1260 export behavior not assessed. No source execution, network/browser, credentials, tests/build, nested delegation, code/API/full-plan analysis or repository writes. Test rows are source requirements, not executed tests. No global/feature task closure.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Complete MOS-1256 description and seven AC extracted into 36 atomic rows with exact JSON pointer and quoted clause locators; source hashes matched and unresolved boundaries recorded."}],
  "changedFiles": [],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"sha256sum openspec/changes/reconcile-control-center-backlog/audit/sources/{jira-feedback,wiki-247734813}/r1/{content,metadata}.json","result":"passed","summary":"Both content digests match supplied expected values; metadata digests recorded."}],
  "validationOutput": ["Saved material-input integrity confirmed; no tests or implementation validation run."],
  "residualRisks": ["Saved-source omissions and flattened wiki; no external freshness verification.","Transition matrix and precise 409/unknown-outcome recovery unspecified.","Historical Jira PATCH discrepancy retained under D-066; no API reassessment.","Parent acceptance and independent review remain pending."],
  "noStagedFiles": true,
  "diffSummary": "Only configured external artifact written; no repository changes or staging performed.",
  "reviewFindings": ["No missing/changed assigned material input detected; product ambiguities retained without inference."],
  "manualNotes": "Requirements-only extraction. Inspected scope and exact evidence locations listed above; parent owns semantic acceptance. No Q1 policy selected."
}
```
