# REPORTS-PLAN-CANDIDATES

Expected HEAD verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Proposed only; no project edits. D-078 accepted evidence reused, not re-audited. Full proposal/design/specs/tasks of both owners read. Publication requires parent decision and independent review.

## Exact replacements

Paths are repository-relative. Each oldText is a literal substring; replacements within a file are disjoint. Keep all checkboxes unchecked.

### C1 — MOS-1015 documentary boundary

Support: D-078 lines 5–9; IMPL-REPORT-CONSTRUCTOR, “Preserve corrected 1015 gates”; review, “Existing-owner documentary disposition”. Wiki publication is not saved OpenAPI support or deployed integration.

```json
{
  "path": "openspec/changes/mos-1015-report-constructor/proposal.md",
  "oldText": "`docs/api/contracts/reports.md` и `dialogs.md` явно сообщают об отсутствии операций; в `openapi.json` схем отчётности нет.",
  "newText": "Принятые документальные материалы содержат контракты диалогов и опубликованный wiki-контракт report-preview/report-export; в сохранённом OpenAPI соответствующие отчётные операции и DTO отсутствуют. Публикация wiki не подтверждает развёртывание или согласование отчётной интеграции."
}
```

### C2 — MOS-1015 reuse, not duplicate construction

Support: review “Constructor — ACCEPT” and owner-disposition row; verified `app/features/dialog-selection/types/dialog-selection.types.ts:4–31` (entity-owned group, local draft without particular-skill ID), `ui/dialog-selection.tsx:10–43` (existing editor). Compatibility remains unproven. Existing report-specific validation, dictionaries, phrase skill choice and tests remain work, not acceptance.

```json
[
  {
    "path": "openspec/changes/mos-1015-report-constructor/design.md",
    "oldText": "`features/dialog-selection` — управляемый редактор одной группы AND/OR с собственными типами и каталогом атрибутов.",
    "newText": "`features/dialog-selection` — существующий редактор одной группы AND/OR; переиспользовать и узко адаптировать его через публичный API, сохраняя владение общей моделью условий в `entities/dialog`, а UI-черновиком — в feature. Совместимость справочников, локального применения и выбора конкретного навыка проверить по delta specs; существующий серверный отбор страницы диалогов не переносить в отчётный черновик."
  },
  {
    "path": "openspec/changes/mos-1015-report-constructor/tasks.md",
    "oldText": "Добавить у владельцев типы, defaults и каталоги 24 колонок/35 атрибутов из delta specs",
    "newText": "Переиспользовать существующие типы и каталог условий у их владельцев, добавить недостающие defaults и каталог 24 колонок; сверить 35 атрибутов с delta specs"
  },
  {
    "path": "openspec/changes/mos-1015-report-constructor/tasks.md",
    "oldText": "Реализовать локальную схему одной группы AND/OR, типизированные операторы и очистку несовместимых значений",
    "newText": "Переиспользовать и при необходимости адаптировать существующую модель одной группы AND/OR из `entities/dialog` и локальную схему редактора, типизированные операторы и очистку несовместимых значений для отчётного черновика без серверного отбора"
  },
  {
    "path": "openspec/changes/mos-1015-report-constructor/tasks.md",
    "oldText": "Создать управляемый `features/dialog-selection`",
    "newText": "Переиспользовать и узко адаптировать существующий `features/dialog-selection` через публичный API для локального отчётного черновика"
  }
]
```

### C3 — MOS-1015 normal session/access boundary

Support: D-078 line 9 and review owner-disposition auth row. This carries forward accepted session boundary, not new auth policy. No session source re-audit needed or performed. Business authorization attributes remain data, not employee access controls.

```json
[
  {
    "path": "openspec/changes/mos-1015-report-constructor/specs/report-constructor-draft/spec.md",
    "oldText": "Редактирование SHALL оставаться доступным без запросов профиля или проверки роли.",
    "newText": "Доступ к редактированию SHALL сохранять штатную границу сессии и доступа приложения; конструктор MUST NOT добавлять собственные запросы профиля или проверки роли."
  },
  {
    "path": "openspec/changes/mos-1015-report-constructor/specs/report-constructor-draft/spec.md",
    "oldText": "уведомление о локальном черновике и отсутствие auth- и report-запросов",
    "newText": "уведомление о локальном черновике и отсутствие отчётных запросов и собственных auth-запросов конструктора; штатная сессия и доступ приложения сохраняются"
  },
  {
    "path": "openspec/changes/mos-1015-report-constructor/design.md",
    "oldText": "Отдельно проверять, что реальные справочники запрашиваются, но отчётные/auth endpoints — нет; запрет всех fetch подряд был бы неверным.",
    "newText": "Отдельно проверять, что реальные справочники запрашиваются, но конструктор не выполняет отчётные или собственные auth-запросы; штатная сессия и доступ приложения сохраняются, запрет всех fetch подряд был бы неверным."
  },
  {
    "path": "openspec/changes/mos-1015-report-constructor/tasks.md",
    "oldText": "в оболочке с правильным basename без auth-запросов.",
    "newText": "в оболочке с правильным basename и штатной границей сессии/доступа, без собственных auth-запросов конструктора."
  }
]
```

### C4 — MOS-919 qualified rationale

Support: corrected IMPL-REPORT-CSV “Architecture and evidence layers”; review CSV P2 and D-078. Verified `app/shared/lib/handlers/download-attachment.ts:1–11` and `app/features/dialog-export/model/use-dialog-export.ts:21–46`. Link helper/dialog flow do not establish a general report-compatible file client.

```json
[
  {
    "path": "openspec/changes/mos-919-report-csv-export/proposal.md",
    "oldText": "MOS-919 требует серверной CSV-выгрузки, но локальные `reports.md` и OpenAPI не содержат контракта экспорта.",
    "newText": "MOS-919 требует серверной CSV-выгрузки. Принятые документальные материалы содержат опубликованный wiki-контракт report-preview/report-export, но в сохранённом OpenAPI соответствующие отчётные операции и DTO отсутствуют; публикация не подтверждает развёртывание или согласование отчётной интеграции."
  },
  {
    "path": "openspec/changes/mos-919-report-csv-export/design.md",
    "oldText": "`shared/api/http-client.ts` принимает JSON и проверяет envelope; ни API экспорта, ни общего файлового клиента сейчас нет.",
    "newText": "`shared/api/http-client.ts` принимает JSON и проверяет envelope. Существуют общий helper скачивания по ссылке и отдельная выгрузка диалогов; они не подтверждают наличие общего файлового клиента, совместимого с отчётами. Wiki-контракт отчётного экспорта опубликован, но соответствующие операции отсутствуют в сохранённом OpenAPI, отчётная выгрузка не подключена, а её развёртывание не проверено."
  }
]
```

## Explicit no-ops / preserved gates

- MOS-919 `design.md:23` scoped no-handler/download-helper restriction is sufficient and stays unchanged. No new transport/helper or report mock authorized.
- MOS-919 tasks and export-availability spec already own missing disabled action, prerequisite and no-side-effect scenarios: no new tasks or feature acceptance. Spec API-absence wording describes current unavailable integration, not a claim that no wiki document exists.
- MOS-1015 dialog-selection spec remains unchanged: required local behavior/particular-skill choice/privacy are not satisfied merely by existing editor. Its business-authorization scenario prohibits an effect of editing that field, not normal shell access.
- Remaining MOS-1015 tasks/specs and C01–C12/B15.1–B15.5, MOS-919 E01–E09/B919.1–B919.4 remain sufficient and open. No wire matrix, advanced DTO, timezone, metrics, limits, header/CORS, empty export or formula-safety decision invented.
- Verified `app/routes/reports.tsx:1–5` still returns PlaceholderPage. Missing constructor/unavailable export already has unchecked tasks; no duplicate backlog. MOS-916 template ownership and MOS-1016 persistence/scheduling unchanged. No auth/API activation, no deployment/test claim.

## Input SHA256 and freshness

Prefixes: `A=openspec/changes/reconcile-control-center-backlog/audit/`, `C=openspec/changes/mos-1015-report-constructor/`, `E=openspec/changes/mos-919-report-csv-export/`.

```text
fad748870836d29d1d115a6efab7ab60aa1f7d5a8e2a926893cc661a7b4bbcea A/reports/IMPL-REPORT-CONSTRUCTOR.md
4e6a92044518c9e7878357e1103fa20854913cb1e6521fcc60537333d69de411 A/reports/IMPL-REPORT-CSV.md
899dd2d4ce7e16897623caf512840196217a893bef6158112b138cdbfb9aa2d3 A/reviews/R-REPORTS-IMPLEMENTATION-BATCH.md
6bf6ede0d264fb0719a96a5044090272ef1f12e7960c6584d1d99ed587120075 A/decisions.md
861fbf568514355c6b5bb251bef2697e4197533f0b3f10b72204d5454fad2c09 C/proposal.md
7b45547f74f69aeac21f5357628ce94f373c4e61a737c7b47fe43fb292bd9d4f C/design.md
119a9e51350cebc6dd1b3417389d07b3e92be65262b2de26940d9687916a98e9 C/tasks.md
cff8f90dcd26c4e52e96c9d8c7fa214ca4bc6f3780eed58fd59811b777b6af07 C/specs/dialog-selection-draft/spec.md
07f81f1887a214bb005e85061a813de573484196c7faf3eb9a0bbb87ab92b132 C/specs/report-constructor-draft/spec.md
261e54647980a4e36846da478e758ef3dfed5ec408f1532a591e4ab185ee3c80 E/proposal.md
78b1d7657f6bd8e4a8146deadf77ad88dec8cefcaff3a45f977a3961f14d578c E/design.md
503bf4ba27ecd972a60ed29b57c15360db6d3a54fd753b196ab4fa9bb67f18e5 E/tasks.md
db3b4fffc78e6d7bfbd545f797e73e20095e84b231da19f828d5cb4e6d9fa33e E/specs/report-export-availability/spec.md
973307cb3f74e7de4f666234ad96b376dcf532ede510c5d7541044e174bafc20 app/features/dialog-selection/types/dialog-selection.types.ts
05152b6497e50da143a89c64a96b2d297b7126e5179bfecf354ff94a7b34b707 app/features/dialog-selection/ui/dialog-selection.tsx
6612b821320ddfe761b2021e34d51de44e7c09bd8dbfa89ec874c15211f0f350 app/shared/lib/handlers/download-attachment.ts
cadf75f0340f6d22174cb38c9c007f09a8a77e29ed0d44578d58faabad6e73d1 app/features/dialog-export/model/use-dialog-export.ts
8ed43a501f208f16fef1cd4f34ed4d3f5a507aa4b69b67750a03b15dfb3b4c23 app/routes/reports.tsx
```

All candidates depend on unchanged D-078 disposition and batch review. C1/C4 publication claims depend on the accepted reports, not newly acquired wiki/OpenAPI evidence. C2 additionally depends on both builder source hashes; C4 on helper/dialog-export hashes. C3 depends on the accepted session-boundary correction, not inferred new permission policy. No-op/missing-delivery disposition depends on the route and full owner plans. Before publishing, recheck HEAD, target hashes, exact unique matches and these dependencies; changes require reconciliation, not blind patching. Hashes cover full files; only D-078 was read from decisions.md.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Four bounded candidate groups with exact replacements, support, input hashes, freshness dependencies and explicit no-ops; no feature task closed."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/41058f2c-933e-4270-b642-540c49e06309/reports-plan-candidates-astra-low.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD; sha256sum scoped inputs; git diff --cached --name-only","result":"passed","summary":"Expected HEAD, recorded input hashes, empty staged-path listing."},
    {"command":"Local bounded read/find/grep","result":"passed","summary":"Read D-078, accepted reports/review and complete owner plans; verified only narrow source locators."},
    {"command":"Tests/build/network/browser","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["All proposed changes are documentary; blocked continuation and unchecked feature tasks preserved."],
  "residualRisks": ["Deployment/runtime and test outcomes unverified.","Documentary publication/schema findings reused from accepted evidence, not reacquired.","Builder compatibility remains implementation work; parent publication and independent review still required."],
  "noStagedFiles": true,
  "diffSummary": "Only configured output artifact written; no project modifications.",
  "reviewFindings": ["No scope conflict requiring escalation."],
  "manualNotes": "Read-only reconciliation, not repeated audit or implementation acceptance. Prior failed model attempt was not retried."
}
```
