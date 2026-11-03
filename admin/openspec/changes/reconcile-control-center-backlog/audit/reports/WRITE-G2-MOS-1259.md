# WRITE-G2-MOS-1259 — minimal documentary candidate

Candidate only; not applied. D-067 authorizes preparation; independent review and parent baseline verification/integration remain required.

## Code Context

### Files Retrieved

Literal aliases: `C = openspec/changes/reconcile-control-center-backlog`, `A = C/audit`, `O = openspec/changes/mos-1259-feedback-saved-filters`. All paths below expand literally.

- `A/work-items/WRITE-G2-FEEDBACK-MINIMAL-PLANS.md` (lines 1–25): common contract and assigned owner; other assignments not executed.
- `C/proposal.md` (1–30), `C/design.md` (1–133), `C/tasks.md` (1–45), `C/specs/control-center-backlog-reconciliation/spec.md` (1–108): governing contract. Truncated combined output was supplemented by separate proposal/design reads.
- `A/decisions.md` (1–32): D-065–067, including candidate-only authority and later API reconciliation.
- `O/proposal.md` (1–32), `O/design.md` (1–49), `O/tasks.md` (1–10), `O/specs/feedback-saved-filters/spec.md` (1–28): complete owner; scoped find confirmed one delta spec.
- `A/reports/REQ-G2-MOS-1259.md` (1–113), `A/reviews/R-REQ-G2-MOS-1259.md` (1–68): accepted requirement evidence.
- `A/reports/SPEC-G2-MOS-1259.md` (1–121), `A/reviews/R-SPEC-G2-MOS-1259.md` (1–82): corrected comparison and retained original **REVISE**, not a fresh independent ACCEPT.
- `A/reports/API-G2-FEEDBACK-SAVED-FILTERS.md` (1–140), `A/reviews/R-API-G2-FEEDBACK-SAVED-FILTERS.md` (1–74): accepted API evidence; reviewer explicitly pinpoints nested defaults at CRUD849–850.
- `docs/api/contracts/crud-api.md` (744–750,827–850): direct title/update primary clauses.
- `A/sources/jira-feedback/r1/content.json` (95–103), `/items/10/description`: complete assigned description and six AC; not a new source census.
- `openspec/changes/mos-1249-feedback-api/design.md` (5–23,49–54): delegated authority and existing published PUT ruling.

### Key Code / Architecture

No application code changed or independently audited. Existing flow is selected-ID UI update → published PUT → partial top-level `name`/`search` update; only a supplied `search` is fully replaced, with defaults for omitted nested parameters. UI's explicit update still sends its complete current search. This is not whole-resource replacement and does not change stale-search application policy.

CRUD827–830: “Пропущенные поля сохраняются, переданный `search` заменяется целиком.” CRUD849–850: “Название при этом сохраняется. Не переданные внутри `search` параметры получают значения по умолчанию, а не значения предыдущего поиска.” These are the precise basis for clarifying “PUT search SHALL заменять объект целиком,” not deleting replacement semantics based on HTTP conventions or Jira wording.

### Start Here

Open `O/specs/feedback-saved-filters/spec.md:9` alongside `docs/api/contracts/crud-api.md:827–850`; then `O/design.md:27` for the title ambiguity and UI/server distinction.

## Baseline SHA-256

Computed over complete target bytes; every proposed target is listed. Recheck before integration.

| Repository-relative target | SHA-256 |
|---|---|
| `openspec/changes/mos-1259-feedback-saved-filters/design.md` | `ffd8b183f81be81aee20d199b76cc7ad73ad196b604a41ead9d56019778b8e08` |
| `openspec/changes/mos-1259-feedback-saved-filters/specs/feedback-saved-filters/spec.md` | `4e9aee0264a677b7dd13a6d4a3bb2eb2bd648b52be1b877a19e86bc33e36655f` |

Directly inspected CRUD source SHA-256: `4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058`, matching accepted API evidence. Hashing does not establish live freshness.

## Changed-clause / source / decision mapping

| Candidate clause | Exact evidence and disposition |
|---|---|
| Design27: replace “1–150 непробельных символов” with length1–150/not whitespace-only | REQ R02, Jira AC1 (`/items/10/description`, physical102); CRUD747–748; corrected SPEC F2 and original review finding2 support narrow correction without an internal-space ban. D-065 and D-067 authorize this. No trimming, Unicode counting, normalization or new fixtures selected. Existing spec title wording stays unchanged. |
| Design27: clarify that complete-search submission is the UI update | REQ R15–R16, Jira AC3; existing spec18–19 and design27. API report/review distinguish server optional top-level fields from UI complete-search input. D-066/067 retain both. Only “в UI” is added; no new interaction. |
| Spec9: top-level omitted `name`/`search` retained; supplied search replaced; omitted nested values default; resource immutable | Direct CRUD827–850, accepted API report semantic joins and review finding2. D-066 resolves the earlier source-only uncertainty; D-067 authorizes exact semantic clarification. Preserves PUT and search replacement rather than treating PUT as whole-resource replacement. |

No proposal/task edits: all five owner tasks remain unchecked. Existing duplicate-name/new-ID, selected-ID targeting, full restoration, no-partial-apply, independent pagination, errors, permissions and release evidence clauses suffice and remain intact. No repeated fixtures/error/pagination tasks, mock task queue, endpoints, Jira edits, Q1 policy, answer API, role-enforced mocks or global closure.

## Minimal unified diff

```diff
--- a/openspec/changes/mos-1259-feedback-saved-filters/design.md
+++ b/openspec/changes/mos-1259-feedback-saved-filters/design.md
@@ -25,5 +25,5 @@
 ### Implementation decisions
 
-MOS-1259: серверные персональные filters с `resource=feedback-surveys`, именем 1–150 непробельных символов и search. Список имеет собственную пагинацию, не совпадает с пагинацией опросников. Создать новый фильтр и обновить выбранный по ID — разные действия; одинаковое имя не вызывает автоматический PUT. Обновление передаёт полный search, resource неизменяем. Применение сохраняет настройки и limit, начинает с offset=0. Неизвестный/чужой ID одинаково 404; показать недоступность без предположений о владельце. Ошибки не заменяются localStorage fallback.
+MOS-1259: серверные персональные filters с `resource=feedback-surveys`, именем длиной 1–150 символов, не состоящим только из пробельных символов, и search. Список имеет собственную пагинацию, не совпадает с пагинацией опросников. Создать новый фильтр и обновить выбранный по ID — разные действия; одинаковое имя не вызывает автоматический PUT. Обновление в UI передаёт полный search, resource неизменяем. Применение сохраняет настройки и limit, начинает с offset=0. Неизвестный/чужой ID одинаково 404; показать недоступность без предположений о владельце. Ошибки не заменяются localStorage fallback.
 
 ### Existing safety and verification
--- a/openspec/changes/mos-1259-feedback-saved-filters/specs/feedback-saved-filters/spec.md
+++ b/openspec/changes/mos-1259-feedback-saved-filters/specs/feedback-saved-filters/spec.md
@@ -7,5 +7,5 @@
 ### Requirement: Personal saved searches
 
-Фильтры SHALL храниться сервером через /saved-filters с resource=feedback-surveys и полным search. Имя SHALL иметь 1–150 символов и не состоять из пробелов. UI SHALL предоставлять создание, постраничный список, применение, явное обновление выбранного по ID и удаление. Одинаковые имена SHALL допускаться и MUST NOT вызывать автоматическую перезапись. PUT search SHALL заменять объект целиком; resource MUST NOT изменяться. При применении SHALL восстанавливаться query, обычные фильтры, conditions, sort, limit с offset=0. Недоступный фильтр SHALL обрабатываться как 404; устаревший search SHALL показывать ошибку без молчаливого частичного применения/localStorage fallback.
+Фильтры SHALL храниться сервером через /saved-filters с resource=feedback-surveys и полным search. Имя SHALL иметь 1–150 символов и не состоять из пробелов. UI SHALL предоставлять создание, постраничный список, применение, явное обновление выбранного по ID и удаление. Одинаковые имена SHALL допускаться и MUST NOT вызывать автоматическую перезапись. PUT SHALL частично обновлять поля верхнего уровня name и search: пропущенное поле SHALL сохранять прежнее значение; переданный search SHALL целиком заменять прежний search, а пропущенные внутри него параметры SHALL получать значения по умолчанию, не значения предыдущего поиска; resource MUST NOT изменяться. При применении SHALL восстанавливаться query, обычные фильтры, conditions, sort, limit с offset=0. Недоступный фильтр SHALL обрабатываться как 404; устаревший search SHALL показывать ошибку без молчаливого частичного применения/localStorage fallback.
 
 #### Scenario: Duplicate names
```

## Validation and limits

- Read-only file discovery/inspection and SHA-256 completed; Git index listing returned no staged paths.
- Old/context hunk lines and hunk counts are checked against baseline by a read-only parser after artifact creation; no candidate file is materialized in the repository.
- `git apply --check` not run; parent may independently check after baseline verification. No application of this diff.
- OpenSpec strict validation/doctor and format check not run: external candidate only, no integrated target. Parent owns post-review validation. No application tests/typecheck/lint/build/API checks/typegen, network/browser/business calls or nested agents run.
- API report ACCEPT is retained as evidence, not a new independent API census; original SPEC review remains REVISE with parent-corrected findings under D-065, later narrowed by D-066. Live freshness, actual defaults/error grammar/deployment remain unverified. Null/empty PUT versus formal schema mismatch is not silently resolved here.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"External two-file minimal documentary diff with baseline SHA-256, exact CRUD827–850/accepted-report joins, D-065–067 mappings and explicit validation limits."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/a764f7bc-1d09-48a2-950a-3cd1247e5cd5/WRITE-G2-MOS-1259.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read/find/scoped grep; nl/sed/wc; sha256sum; git diff --cached --name-only","result":"passed","summary":"Complete owner and required documentary evidence inspected; target/CRUD hashes recorded; index listing empty."},
    {"command":"git apply --check; OpenSpec validation/doctor; format and application checks","result":"not-run","summary":"External candidate only; parent reviews, checks baseline and validates integration. No tests/typegen/network/browser executed."}
  ],
  "validationOutput": ["Candidate changes only design27 and spec9; tasks/proposal/code untouched.","Published PUT, full UI search, duplicate-ID and no-partial-apply behavior retained."],
  "residualRisks": ["Independent candidate review, apply-check and parent integration remain pending.","Saved evidence does not establish current live freshness, deployed defaults or error grammar; no runtime checks performed."],
  "noStagedFiles": true,
  "diffSummary": "Repository unchanged. External candidate clarifies title wording and two-level PUT update semantics in two existing owner paragraphs.",
  "reviewFindings": ["No new policy or scope proposed; earlier whole-object ambiguity reconciled directly with accepted CRUD evidence."],
  "manualNotes": "No repository candidates written/applied and no checkbox edits. Q1 unselected. Parent retains acceptance and publication authority. Verification obligations are not executed test evidence."
}
```
