# REQ-MOS-1018 — fresh source extraction

## Sources and exact locators

- **J**: `sources/jira-details-MOS-774/r1/content.json`, `$.items[7]` (`key = MOS-1018`), especially `$.items[7].description`. Summary: «[FE][Навыки] Подключить проверку конфликтов обучающих фраз»; status `Backlog`; updated `2026-10-16T19:22:30.987+0800`. No other Jira issue was extracted.
- **W**: `sources/wiki-241080062/r1/content.json`, `$.bodyView`, title `Админка. Навыки`. Locators below give exact heading plus requirement/table row, avoiding the large JSON's single-line HTML. The heading outline was inspected before extracting relevant sections; HTML was parsed only as inert text.
- Both corresponding `metadata.json` files read. J retrieved `2026-10-16T11:49:06.782Z`, SHA-256 `e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208`; W retrieved `2026-10-16T11:48:21.710Z`, version 17 dated `2026-10-09T23:32:41.029+08:00`, SHA-256 `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2`. Hashes are metadata provenance, not independently revalidated here.
- Snapshot limitations: Jira comments/custom fields/attachment bodies absent; wiki attachment metadata only and linked pages not implicitly included. Findings concern saved prose, not verified API behavior, application implementation, or prior audit conclusions.

## Atomic requirements

All `J` quotes below locate to `$.items[7].description`; all `W` quotes locate to `$.bodyView` under the named heading.

| Stable ID | Requirement supported by current sources | Primary evidence |
|---|---|---|
| MOS-1018-R01 | Use a server-side check over the entire permitted registry, not only the loaded page. | J: «Проверять фразы по всему допустимому реестру серверным методом»; «Локальное сравнение загруженной страницы не заменяет глобальную проверку». |
| MOS-1018-R02 | Check intersections with other skills directly in the wizard. | W → `Мастер подключения навыка (MAC)`, MAC-5: «прямо в мастере»; W → `C. Мастер подключения навыка`, T-18: «Онлайн-проверка пересечений фраз». This specifies an interaction location, not a single-phrase request schema. |
| MOS-1018-R03 | Check intersections when saving content. | W → `Карточка навыка: обучающие фразы (ФРА)`, ФРА-7: «При сохранении содержания выполняется проверка пересечений»; W → `E. Карточка навыка: обучающие фразы`, T-42: «BE: синхронная проверка». |
| MOS-1018-R04 | Present phrase, conflict type, similarity, competing skill and domain. | J: «Показать фразу, тип конфликта, близость, навык и домен»; W → `Карточка навыка: проверки (ПРВ)`, ПРВ-7: «Конфликты формулировок выводятся таблицей». |
| MOS-1018-R05 | Highlight conflicting phrases and identify the owning skill, subject to unresolved safe disclosure. | W → `Мастер подключения навыка (MAC)`, ПРТ-МАС-4: «Конфликтующие фразы подсвечиваются, показывается навык-владелец»; W → `Карточка навыка: обучающие фразы (ФРА)`, ПРТ-ФРА-1: «конфликтующие фразы подсвечиваются». |
| MOS-1018-R06 | Exact matches block send/forward movement, with an explanatory blocking error. | J: «Точное совпадение блокирует отправку»; W → `Мастер подключения навыка (MAC)`, MAC-6: «отправка на проверку блокируется»; W → `C. Мастер подключения навыка`, T-19: «disabled-состояние и сообщение»; W → `Карточка навыка: проверки (ПРВ)`, ПРВ-8: «блокирует отправку навыка дальше». Scope of “send” remains unresolved below. |
| MOS-1018-R07 | Semantic similarity warns but does not block progression/send. | J: «смысловая близость предупреждает»; W → `Карточка навыка: проверки (ПРВ)`, ПРВ-9: «движение не блокирует»; W → `Валидации и ошибки`, ПРТ-ВАЛ-5: «отправка не блокируется». |
| MOS-1018-R08 | Show conflict count on the checks tab; failing checks identify blocking effect and where to fix the issue. | W → `Карточка навыка: проверки (ПРВ)`, ПРВ-10: «Число конфликтов выводится на вкладке проверок»; ПРВ-2: «блокирует ли её результат движение»; ПРВ-3: «что именно не так и где это исправить». |
| MOS-1018-R09 | Resolve normalization rules and safe cross-team conflict disclosure; neither is specified sufficiently to implement from these sources alone. | J: «Нужны правила нормализации и безопасное раскрытие конфликта с объектом другой команды». This is an explicit open need, not an agreed algorithm or masking policy. |
| MOS-1018-R10 | Provide the wizard's send-for-check action separately from draft save; send leads to the checking state. | W → `Мастер подключения навыка (MAC)`, ПРТ-МАС-6: «Сохранить черновик» and «Отправить на проверку»; ПРТ-МАС-7: «в статусе “На проверке”» (source uses Russian angle quotes); MAC-11: «на проверку платформенной команде». |

## Current-source gates, disagreements and missing semantics

1. **Global scope versus visibility/disclosure.** R01 requires the entire *permitted* registry. W → `Общие принципы раздела`: «Команда навыка видит только свои навыки и домены; продуктовая команда видит все». MAC-6 nevertheless requires «с указанием навыка-владельца фразы»; J expressly asks for safe disclosure of another team's object. The sources do not define whether permission limits the comparison corpus, returned identities, or both. Preserve this tension; do not choose unrestricted disclosure or limit checking to visible rows.
2. **Normalization remains open.** J asks for rules. W → `4.4. skill_conflicts`, row `normalized_phrase`: «Нормализованная фраза», optional (`нет`). A storage field does not define case folding, whitespace, punctuation, Unicode, morphological equivalence, or the exact/semantic boundary. No thresholds or similarity scale are established by the selected prose.
3. **Single/current-input and full-input binding are not established.** “Онлайн-проверка” (T-18) supports in-wizard checking, not a promise that one checked phrase certifies all groups or all current edits. No inspected passage defines single versus batch input, checked-input identity/version, inclusion of unsaved additions/deletions, or reuse of results across domain/skill changes. These are unresolved questions, not newly accepted requirements.
4. **Freshness gate is unspecified.** Save-time checking (R03) is explicit; freshness TTL, invalidation after edit, out-of-order result handling, loading/error/unavailable-check behavior, and a mandatory immediately-before-send recheck are not specified. W → `4.4. skill_conflicts` has «Дата обнаружения» and «Дата последнего изменения» (`created_at`, `updated_at`), but these timestamps do not bind a result to current input. Do not infer that an old clear result authorizes send or invent a blocking policy for an unavailable check.
5. **Exact conflict blocks send, not necessarily save.** MAC-6 / ПРВ-8 / J block send or forward movement. W → `Карточка навыка: обучающие фразы (ФРА)`, ПРТ-ФРА-5: «сохранение возможно, но навык попадает на доработку с указанием конфликта». Distinct save/send operations could explain this, but the source does not specify the full transition interaction; do not silently turn send blocking into save blocking or discard the allowed-save passage.
6. **Training timing disagreement.** W → `Общие принципы раздела`: «Если фраза уже занята другим навыком, обучение модели не запускается». W → `Карточка навыка: обучающие фразы (ФРА)`, ПРТ-ФРА-4: «При сохранении фраз запускается дообучение классификатора»; ФРА-6: changes to a running skill cause «повторную проверку». T-23 under `C. Мастер подключения навыка` describes send as «Перевод в checking, постановка задач на дообучение». No precedence is selected between unconditional-sounding training statements and the conflict prerequisite.
7. **Which required send?** Wizard MAC-11 describes transfer to the platform team; W → `Жизненный цикл навыка`, state «На проверке»: «идут автоматические проверки. Переводит система»; ПРВ-8 says broader «дальше». T-23 names `/submit`, but the prose does not settle all downstream forward actions or whether rechecking a running skill requires an explicit submit versus save-triggered transition. Preserve both team handoff and automatic-check descriptions rather than choosing one as authoritative.
8. **Contract gate explicitly raised by Jira.** J: «в API не определены: проверка точных и смысловых конфликтов, severity, similarity и доступное описание чужого навыка». W's decomposition names check/conflict operations, but that does not resolve Jira's reported contract gaps. This extraction does not independently assert that a current backend lacks those capabilities.

## Deferrals and adjacent references (not retrieved)

- Explicit outstanding needs: normalization and safe disclosure (R09), plus Jira's listed contract gaps. No inspected passage expressly defers the conflict feature, a freshness solution, or full-input binding to a later release. Absence of specification is not evidence of an agreed deferral.
- Explicit adjacent scope exclusion: W → `Общие принципы раздела`: «Управление командами и пользователями - вне границ раздела “Навыки”» (source uses angle quotes). Use existing visibility context; this task does not authorize a new role/team administration model.
- J links the contract page `https://wiki.mos-team.ru/spaces/KR/pages/241097511/` titled `API-контракт реестра доменов и каталога навыков`; not retrieved.
- Relevant W decomposition references: T-18 `POST /api/v1/skills/check-phrases`, T-19 send blocking, T-23 `POST /api/v1/skills/{id}/submit`, T-42 save-time synchronous checking, T-47 `GET /api/v1/skills/{id}/conflicts`. These are primary-source references, not verified contracts or an API inventory. No endpoint calls, linked-page retrieval, or application-code audit performed.

## Result and residual risks

The sources support global server checks, wizard/save triggers, conflict presentation, exact blocking, semantic warnings and a distinct send action. They do **not** settle single/current-input certification, full-input binding, freshness, normalization, safe disclosure, or the complete boundary of “send”. Save/training/lifecycle statements remain in tension. Product/API clarification is needed before treating those omissions as resolved; no new product decisions are made here.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "Extracted MOS-1018-R01–R10 from only MOS-1018 and selected saved wiki passages, with exact JSON/heading/row locators and primary quotes; recorded unresolved gates and disagreements."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-1018.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command": "Local Python JSON inspection and inert HTMLParser heading/selected-passage extraction", "result": "passed", "summary": "Read the bound sources; selected wiki sections by heading; no saved commands or HTML executed."}],
  "validationOutput": ["Work item and both source metadata files inspected; only designated report written. Tests, generation, network and browser actions not run."],
  "residualRisks": ["Normalization, safe disclosure, current/full-input binding and freshness are unspecified.", "Save/send/training and lifecycle handoff wording cannot be reconciled by selecting precedence without a product decision.", "Saved sources exclude comments and attachment bodies; linked contract not retrieved."],
  "noStagedFiles": true,
  "diffSummary": "Only the bound requirement-extraction report was written; no source or status edits.",
  "reviewFindings": [],
  "manualNotes": "Fresh primary-source extraction, not an implementation/API audit. No tests were appropriate or permitted; no staging operations performed."
}
```
