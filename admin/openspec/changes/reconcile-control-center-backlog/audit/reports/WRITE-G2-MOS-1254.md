# Code Context

## Result

WRITE-G2-MOS-1254 only: candidate documentary correction for active-only new type selections and nested parent-save 409/422 error targets/input retention. **Not applied.** Parent independently reviews, rechecks baselines and integrates. No Q1 policy chosen; no feature or global audit closure.

## Files Retrieved

Exact root abbreviations below expand literally: `C = openspec/changes/reconcile-control-center-backlog`, `A = openspec/changes/reconcile-control-center-backlog/audit`, `O = openspec/changes/mos-1254-feedback-questions`.

- `C/proposal.md` lines 1–30; `C/design.md` lines 1–133; `C/tasks.md` lines 1–45; `C/specs/control-center-backlog-reconciliation/spec.md` lines 1–108: governing contract, fully read (truncated shell beginning recovered from tool spool).
- `A/work-items/WRITE-G2-FEEDBACK-MINIMAL-PLANS.md` lines 1–25: common contract and assignments; only MOS-1254 executed.
- `A/decisions.md` lines 1–31: D-065–067 authority and original-review qualifications.
- `O/proposal.md` lines 1–34; `O/design.md` lines 1–53; `O/tasks.md` lines 1–10; `O/specs/feedback-questions/spec.md` lines 1–30; `O/.openspec.yaml` lines 1–2: complete owning artifacts.
- `A/reports/REQ-G2-MOS-1254.md` lines 1–133; `A/reviews/R-REQ-G2-MOS-1254.md` lines 1–66: accepted requirement evidence.
- `A/reports/SPEC-G2-MOS-1254.md` lines 1–160; `A/reviews/R-SPEC-G2-MOS-1254.md` lines 1–73: corrected report and original **REVISE**, not a fresh independent ACCEPT.
- `A/reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md` lines 1–162; `A/reviews/R-API-G2-FEEDBACK-SURVEY-MUTATIONS.md` lines 1–72: accepted API evidence and review. Primary Jira/wiki/API packets were not independently reread in this candidate-author lane; mappings below reuse these accepted reports explicitly.

## Key Code — clause/source/decision mappings

| Candidate clause (baseline locator) | Exact evidence and disposition |
|---|---|
| `O/design.md:29`, `O/specs/feedback-questions/spec.md:11`: any new choice, including changing an existing question, active-only; unchanged saved inactive type remains editable/reorderable | REQ ID27, with retained IDs25–26 (`A/reports/REQ-G2-MOS-1254.md:75–77`); primary locator `A/sources/jira-feedback/r1/content.json:57`, `/items/5/description`, AC5, as accepted in `A/reviews/R-REQ-G2-MOS-1254.md:25`. Corrected SPEC section “Inactive selection”; original review `A/reviews/R-SPEC-G2-MOS-1254.md:14`. Accepted API requirement-join Q25–29/Q06 cites `docs/api/contracts/crud-api.md:223–239` for new inactive vs unchanged saved references. D-065 and D-067 authorize this narrow clarification. |
| New scenario after `O/specs/feedback-questions/spec.md:21`: parent-save nested 409 or 422 points to relevant question/option, preserves all draft input, parent retains submit ownership | REQ IDs32–33 (`A/reports/REQ-G2-MOS-1254.md:82–83`), primary Jira AC6 at the same source locator; original SPEC review `A/reviews/R-SPEC-G2-MOS-1254.md:7,15,20` requires behavior, not fixture/algorithm. Accepted API Q32–33 join cites CRUD1199–1280, with formal 422/envelope divergence; API review lines16–17 preserves that limit. D-065–067 support scenario without inventing wire grammar, option-specific server guarantees or Q1 policy. |
| Existing tasks1.1 and2.1 verification (`O/tasks.md:3,8`) | ID27 verification and ID34 unit/component obligation (`A/reports/REQ-G2-MOS-1254.md:77,84`), constrained by IDs32–33 and original SPEC review lines7,14–15,20. D-067: minimum existing-task verification only, all five checkboxes remain unchecked. No new test family, fixture or mock task. |

D-066 resolves method authority to existing published PUT; this candidate leaves PUT untouched. UUID/FK rules already covered are not repeated. Opaque-options policy, cancel/undo, answer API, preview ownership, permissions and mock enforcement remain unchanged.

## Baseline SHA-256

Computed directly from current repository bytes; all three match the owner baselines recorded in the accepted evidence. Hashes are not source-freshness or deployment attestations.

| Target | SHA-256 |
|---|---|
| `openspec/changes/mos-1254-feedback-questions/design.md` | `181f2800f8e8f359147ef9c9d3a6eb4f3d4daafa20324dd3b8e1cf0c23d54e10` |
| `openspec/changes/mos-1254-feedback-questions/specs/feedback-questions/spec.md` | `eeb2d92c74667f09a97d933390176b2771d39a1596a4f0c21cf0e23e39c9d27c` |
| `openspec/changes/mos-1254-feedback-questions/tasks.md` | `2920f54aba3994e856679db78d4706c553e7a97be0c17d420643b7f3d72fba65` |

## Minimal unified diff

```diff
--- a/openspec/changes/mos-1254-feedback-questions/design.md
+++ b/openspec/changes/mos-1254-feedback-questions/design.md
@@ -26,7 +26,7 @@
 
 ### Implementation decisions
 
-До 100 вопросов и 100 вариантов на вопрос; title 1–500, option.text 1–255. Для tags минимум один вариант, другие типы не содержат вариантов. Смена типа с потерей вариантов требует явного подтверждения, перемещение сохраняет идентичность. Новые вопросы нельзя создавать с неактивным типом; существующие можно править/переставлять без смены типа. Неизвестный backend type отображается с предупреждением и сохраняется без подмены; интерактивный preview такого вопроса недоступен.
+До 100 вопросов и 100 вариантов на вопрос; title 1–500, option.text 1–255. Для tags минимум один вариант, другие типы не содержат вариантов. Смена типа с потерей вариантов требует явного подтверждения, перемещение сохраняет идентичность. Любой новый выбор типа, включая смену типа существующего вопроса, ограничен активными типами; сохранённый неактивный тип допускает правку/перестановку вопроса без смены типа. Неизвестный backend type отображается с предупреждением и сохраняется без подмены; интерактивный preview такого вопроса недоступен.
 
 PUT частичен только сверху: questions, surface_ids заменяются целиком; display_rules передаётся полным итоговым объектом. Existing question/option UUID сохраняются, новые ID генерирует backend, порядок задаётся массивом. Не отправлять sort_order, timestamps, FK, локальные ключи и ответное display_rules.id. Не отправлять пустой PUT. Явные null допустимы только для очищаемых nullable полей по бизнес-правилам; не считать все nullable из OpenAPI разрешёнными к очистке.
 
--- a/openspec/changes/mos-1254-feedback-questions/specs/feedback-questions/spec.md
+++ b/openspec/changes/mos-1254-feedback-questions/specs/feedback-questions/spec.md
@@ -8,7 +8,7 @@
 
 Конструктор SHALL поддерживать stars, tags, text, boolean, scale, nps, emoji, изменение заголовка/типа/required, добавление, удаление и порядок вопросов/вариантов. Порядок SHALL изменяться перетаскиванием и доступными клавиатурными действиями. Лимиты SHALL быть 100 вопросов, 100 вариантов на вопрос, title 1–500, option.text 1–255. tags SHALL иметь минимум один вариант; остальные типы MUST NOT отправлять непустые options. Смена типа, удаляющая варианты, SHALL требовать подтверждения.
 
-PUT questions SHALL содержать полный итоговый массив с сохранёнными UUID существующих элементов и без ID новых. sort_order MUST NOT отправляться. Existing inactive type SHALL допускать изменение/перестановку без смены типа, новые вопросы с ним MUST NOT создаваться. Неизвестный type SHALL сохраняться без подмены и иметь явное ограничение preview.
+PUT questions SHALL содержать полный итоговый массив с сохранёнными UUID существующих элементов и без ID новых. sort_order MUST NOT отправляться. Existing inactive type SHALL допускать изменение/перестановку без смены типа. Любой новый выбор типа, включая смену типа существующего вопроса, SHALL быть ограничен активными типами. Неизвестный type SHALL сохраняться без подмены и иметь явное ограничение preview.
 
 #### Scenario: Reorder without identity loss
 
@@ -20,6 +20,11 @@
 - **WHEN** у вопроса tags удалён последний вариант
 - **THEN** сохранение не объявляется успешным, ошибка доступна рядом с вопросом и введённый текст остаётся
 
+#### Scenario: Nested errors on parent save
+
+- **WHEN** сохранение родительской карточки возвращает вложенную ошибку 409 или 422 для вопроса или варианта
+- **THEN** ошибка SHALL отображаться у соответствующего вопроса или варианта, весь введённый draft SHALL сохраняться; отправка остаётся ответственностью родительского редактора
+
 ### Requirement: Accessible questions interactions
 
 Область этой задачи — вопросы, варианты и их перестановка — SHALL поддерживать клавиатуру, доступные названия/ошибки, предсказуемый фокус и узкую компоновку. Приёмка SHALL проверять собственные элементы; реализация и приёмка соседних UI-возможностей MUST NOT требоваться для закрытия этой задачи сверх явно указанных зависимостей интеграции. Недоступные API MUST NOT имитироваться успешными заглушками.
--- a/openspec/changes/mos-1254-feedback-questions/tasks.md
+++ b/openspec/changes/mos-1254-feedback-questions/tasks.md
@@ -1,10 +1,10 @@
 ## 1. MOS-1254 — Реализовать конструктор вопросов и вариантов
 
-- [ ] 1.1 На foundation MOS-1251 (task 1.1) реализовать семь типов, title/required, добавление/удаление и варианты tags; контент не рендерить через HTML. Проверка: лимиты 100 вопросов/100 вариантов, 500/255 символов, пустые tags options, inactive/unknown type и подтверждение потери вариантов при смене типа.
+- [ ] 1.1 На foundation MOS-1251 (task 1.1) реализовать семь типов, title/required, добавление/удаление и варианты tags; контент не рендерить через HTML. Проверка: лимиты 100 вопросов/100 вариантов, 500/255 символов, пустые tags options, inactive/unknown type, активность любого нового выбора типа (в том числе при смене типа существующего вопроса), правка/перестановка с сохранением неактивного типа и подтверждение потери вариантов при смене типа.
 - [ ] 1.2 Добавить drag-and-drop и клавиатурное перемещение, сериализацию полного массива с исходными ID и без ID новых/sort_order. Проверка: перестановка вопроса/варианта сохраняет идентичность, удаление отражается в payload, повторный GET воспроизводит порядок.
 
 ## 2. Приёмка подзадачи
 
-- [ ] 2.1 Проверить FSD/public APIs, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты, без browser/E2E.
+- [ ] 2.1 Проверить FSD/public APIs, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты, включая вложенные 409/422 при родительском сохранении: ошибка у соответствующего вопроса/варианта и сохранение всего введённого draft; без browser/E2E.
 - [ ] 2.2 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`; при изменении API-типов — `yarn api:check`, при изменении сборки — `yarn build`. Проверка: записать реальные результаты; environment failures не считать успехом.
 - [ ] 2.3 Перед выпуском проверить сохранение вопросов/вариантов, порядка и UUID через POST/PUT→GET. Проверка: конкретные результаты согласованных HTTP-проверок либо подтверждение владельца стенда без секретов. При отсутствии evidence gate оставить открытым.
```

## Architecture

MOS-1254 remains the private nested editor feeding MOS-1251's draft and single save; MOS-1249 owns API transport and MOS-1255 preview. The added scenario specifies UI response to a returned nested error, not that every nested field is guaranteed to produce both statuses. Existing accessibility/focus rules continue without a new addressing algorithm or prescribed fixture.

## Start Here

Review `openspec/changes/mos-1254-feedback-questions/specs/feedback-questions/spec.md:9–25` against the diff and the original SPEC review's lines7,14–15. Recheck all three hashes before integration.

## Validation and limits

- Read-only Python generated the diff in memory from current target bytes; asserted each replaced substring occurs exactly once. Thus old/context hunk lines originate exactly from baseline, not reconstructed source quotes. No candidate files written in the repository or elsewhere apart from this requested Markdown.
- Manual diff review: only two supported corrections and bounded existing-task verification; all five unchecked task states retained; proposal/metadata/code/contracts/main specs untouched.
- `git diff --cached --name-only` returned empty. Ignored OpenSpec files are not certified by Git staging status.
- `git apply --check`, OpenSpec strict validation/doctor and formatting checks **not run**: candidate is external/unapplied; parent validates after independent review. No passed apply-check claimed.
- No network/browser/business calls, tests, typecheck, lint, build, typegen or nested agents. Test wording is a future obligation, not executed evidence.
- Q1 remains unresolved; existing ambiguous opaque-options/no-blocking-question text is intentionally not changed by this authorized patch. Formal422 versus business error-envelope divergence, actual index handling, saved-source freshness and runtime/deployment behavior remain unverified. No opaque-options preserve/omit/block policy is selected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"External minimal three-target diff, directly computed baseline hashes, exact source/decision mappings and explicit unrun validation/residual risks supplied."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/a764f7bc-1d09-48a2-950a-3cd1247e5cd5/WRITE-G2-MOS-1254.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"read/find/scoped grep/nl/wc; read-only Python hashlib/difflib generation with unique-old-text assertions","result":"passed","summary":"Required documents/evidence read; three target hashes computed; old hunk lines derived directly from baseline."},
    {"command":"git diff --cached --name-only","result":"passed","summary":"Empty staged-file list."},
    {"command":"git apply --check; OpenSpec validation/doctor; format check","result":"not-run","summary":"Unapplied external candidate; parent review/integration validation pending."},
    {"command":"tests/typecheck/lint/build/typegen/network/browser","result":"not-run","summary":"Outside or prohibited by read-only documentary assignment."}
  ],
  "validationOutput": ["Five task checkboxes remain unchecked in candidate; no repository file written.","In-memory diff generation and baseline text assertions succeeded; apply-check not claimed."],
  "residualRisks": ["Q1 unresolved and untouched.","Actual nested-error envelope/index behavior and deployment unverified.","Saved sources not refreshed; parent must recheck hashes and independently review before integration."],
  "noStagedFiles": true,
  "diffSummary": "External Markdown only; proposes active-only selection clarification, nested parent-save error scenario, and bounded existing verification wording.",
  "reviewFindings": ["No self-acceptance of publication; fresh independent review pending."],
  "manualNotes": "Read corrected SPEC report together with its original REVISE disposition. Optional identity/fixture/cancel refinements deliberately excluded; PUT and Q1 policy unchanged. Repository remained read-only."
}
```
