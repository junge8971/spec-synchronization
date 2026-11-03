# WRITE-G2-MOS-1249 — candidate ready for independent review

Implemented only D-061 F1/F2 in the isolated candidate `tasks.md`, lines 3, 6 and 14. No integration or feature closure. F5 excluded. Seven unchecked checkboxes and every other line preserved.

## Authority and reading

Using change: `mos-1249-feedback-api`, exclusively the assigned publication candidate (changing the target requires a new parent assignment). Read `.agents/skills/openspec-update-change/SKILL.md`; explicit D-061 and this assignment authorize these exact edits. The staging-copy contract overrides ordinary active-root artifact editing: no OpenSpec root/config was created.

Fully read the assignment, accepted SPEC report and independent review, target proposal/design/tasks/sole delta spec, governing design/spec and D-061. The initial combined shell read was truncated; target proposal/design were recovered through complete reads, and candidate tasks were read completely and verified byte-identical to active/baseline before editing. No auth policy interpretation or change was performed; auth/demo prerequisites were not independently reread for this wording-only execution.

Sources: `audit/decisions.md`, D-061; `audit/reports/SPEC-G2-MOS-1249.md`, F1/F2; `audit/reviews/R-SPEC-G2-MOS-1249.md`, F1/F2. Target `design.md:21–23` explicitly supplies the successor contract, published dialog export, security normalization and existing-handler baseline. `proposal.md:9–24` keeps adjacent clients/UI deferred; `specs/feedback-api/spec.md:7–38` keeps API/error/permission requirements unchanged. Governing design sections 5–7 and spec “Safe OpenSpec publication” require isolated writing, independent review and parent integration.

## Hashes and preservation

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matched).
Accepted report SHA-256: `9f2ae005c83fe0d71c1d2fac32573bf4ec84efa0185a1928036724657adacebd` (matched assignment).
Review SHA-256: `1d7f593184e863c63a266862badb3435a0ab297e32fecdbbfb352f50388e87c7`.

| Artifact | Active/baseline and candidate before | Candidate after |
|---|---|---|
| proposal.md | `5cc397bd1aab8722961df260fbc16216069816d3fe02d2a82eab09b9e41506ac` | unchanged |
| design.md | `0b15bcebfea15e35aca35a90c835a00efd892bb9a962fc16401892ca6017d91d` | unchanged |
| specs/feedback-api/spec.md | `a783836ee1f191457d5331e87e2befaf809740fe39125ab302457645b9a591a3` | unchanged |
| tasks.md | `21dbfcf3e2d71406070ee374fbb77c76955928326297ec0ca97af4690a2354dd` | `c0b8d2a4337d3c92ec0998b958b7148ad9a0da295f496290c80a03b95160daa3` |

All four active/baseline hashes match the accepted report before and after editing. Metadata copies were identical. Historical source hashes remain untouched in design. Exact replacements changed only the three authorized lines; task acceptance, release gate, credentials/role-enforcement exclusions, production exclusion, profiles and unrelated CRUD prohibition remain intact.

Four-artifact coherence checked: revised tasks now follow design's explicit migration while leaving proposal ownership and delta behavior unchanged. No additional artifact change is needed. Existing handlers are a review baseline, not a claim that feedback-specific implementation/testing is complete. No unsupported-API behavior elsewhere was changed.

## Exact candidate diff

```diff
--- baseline/tasks.md
+++ candidate/tasks.md
@@ -1,9 +1,9 @@
 ## 1. MOS-1249 — Подключить API опросников, справочных значений и метаданных
 
-- [ ] 1.1 Проверить актуальные CRUD/OpenAPI источники из design.md и их provenance в проекте; сохранить HTML/PDF источники. Использовать уже обновлённый aggregate и standalone managed-resources, сохранив старые пути и экспортное дополнение. Проверка: разрешение всех $ref, отсутствие потери старых операций, `yarn api:generate` и `yarn api:check`.
+- [ ] 1.1 Проверить актуальные CRUD/OpenAPI источники из design.md и их provenance в проекте; сохранить HTML/PDF источники. Использовать актуальные aggregate и standalone managed-resources, сохранив опубликованные операции, включая экспорт диалогов, и нормализацию security AND двух заголовков; не восстанавливать заменённое опубликованным контрактом локальное экспортное дополнение. Проверка: разрешение всех $ref, отсутствие потери старых операций, `yarn api:generate` и `yarn api:check`.
 - [ ] 1.2 Добавить entities/feedback с публичным API, DTO/runtime schemas и клиентами CRUD, search, lookup, metadata; использовать существующий transport. Проверка: unit-тесты путей/тел, POST→GET, полной карточки PUT, 409/422 JSON Pointer, невалидного ответа, отмены и отсутствия автоматического replay.
 - [ ] 1.3 Подключить опубликованную UI-policy ManagedResource read/create/update/delete/export через существующие mappings, сохранив session owner/generation. Проверка: unit-тест матрицы read-only principal и запрещённых actions; server 403 и поздний ответ другой сессии; фактические маршруты/скрытие элементов проверяются в changes владельцев UI; request ACL не появляется.
-- [ ] 1.4 Добавить контрактные feedback/lookup/metadata handlers и fixtures в существующий Express, без credentials/role enforcement и без production-включения. Проверка: mock HTTP-тест успешного создания/чтения и конфликтов; existing session profiles/fixed-error механизмы сохраняются.
+- [ ] 1.4 Проверить и при необходимости дополнить существующие контрактные feedback/lookup/metadata handlers и fixtures в существующем Express, без credentials/role enforcement и без production-включения. Проверка: mock HTTP-тест успешного создания/чтения и конфликтов; existing session profiles/fixed-error механизмы сохраняются.
 
 ## 2. Приёмка подзадачи
 
@@ -11,4 +11,4 @@
 - [ ] 2.2 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`; при изменении API-типов — `yarn api:check`, при изменении сборки — `yarn build`. Проверка: записать реальные результаты; environment failures не считать успехом.
 - [ ] 2.3 Перед выпуском проверить реальные CRUD/search/lookup/metadata, envelope ошибок/null, MPMM и глобальный scope. Проверка: конкретные результаты согласованных HTTP-проверок либо подтверждение владельца стенда без секретов. При отсутствии evidence gate оставить открытым.
 
-Актуальный источник уже включён в aggregate change `update-control-center-contracts-put`; проверять его согласованность, не возвращать старую выгрузку. При реализации feedback handlers удалить соответствующие операции из явного unavailable-перечня. Остальные CRUD-разделы не реализовывать в этой задаче.
+Актуальный источник уже включён в aggregate change `update-control-center-api-contracts`; проверять его согласованность, не возвращать старую выгрузку. Проверить и переиспользовать существующие feedback handlers, добавляя только необходимые feedback-specific fixtures, валидацию и тесты; не восстанавливать прежний общий unavailable-перечень. Остальные CRUD-разделы не реализовывать в этой задаче.
```

## Validation and remaining gates

Ran only local read/discovery/hash/diff/index inspection and in-memory assertions. Assertions verified 14 lines, exactly changed lines [3,6,14], seven unchecked tasks, unchanged active/baseline and other candidate artifacts. Git index output was empty; Git status alone does not account for ignored audit files.

OpenSpec status/strict validation were not run: this verified-copy candidate is not an active OpenSpec change/root. Validating the active root would validate the unchanged original, not this candidate; no temporary root/config or invented CLI target was used. Parent must run supported strict validation after reviewed integration. Tests, build, typegen, typecheck, lint, formatting, browser/network, credentials and nested delegation were not run, as prohibited or outside this tasks-only assignment. No runtime/deployment claims are made. Main HTTP historical residue remains separately owned, unchanged and not a prerequisite here.

Recommended next step: fresh independent candidate review, then parent hash recheck/integration/strict validation. No blocking scope question identified.

```acceptance-report
{
  "criteriaSatisfied": [
    {
      "id": "criterion-1",
      "status": "satisfied",
      "evidence": "Only D061 F1/F2 candidate lines 3,6,14 changed; all seven unchecked tasks preserved."
    },
    {
      "id": "criterion-2",
      "status": "satisfied",
      "evidence": "Before/after hashes, exact diff, source citations, preservation assertions and skipped checks recorded."
    }
  ],
  "changedFiles": [
    "openspec/changes/reconcile-control-center-backlog/audit/publication/WRITE-G2-MOS-1249/candidate/tasks.md",
    "openspec/changes/reconcile-control-center-backlog/audit/reports/WRITE-G2-MOS-1249.md"
  ],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {
      "command": "Local read/find/rg and git rev-parse HEAD",
      "result": "passed",
      "summary": "Required planning inputs read; HEAD matched."
    },
    {
      "command": "Python hashlib/difflib and preservation assertions",
      "result": "passed",
      "summary": "All four active/baseline hashes matched accepted report; only candidate lines 3,6,14 changed."
    },
    {
      "command": "git diff --cached --name-only; git status --short",
      "result": "passed",
      "summary": "Empty index and status output; ignored files verified directly."
    },
    {
      "command": "OpenSpec validation; application tests/build/typegen/typecheck/lint/format; browser/network",
      "result": "not-run",
      "summary": "Candidate is not a supported active root; remaining execution forbidden or out of scope."
    }
  ],
  "validationOutput": [
    "Seven unchecked tasks preserved; four-artifact coherence checked; exact diff recorded."
  ],
  "residualRisks": [
    "Fresh independent review and parent integration/strict validation pending.",
    "Runtime, deployment and external freshness not verified."
  ],
  "noStagedFiles": true,
  "diffSummary": "Three minimal wording corrections in isolated tasks candidate plus required execution report.",
  "reviewFindings": [
    "No writer-identified blockers; independent reviewer gate remains pending."
  ]
}
```
