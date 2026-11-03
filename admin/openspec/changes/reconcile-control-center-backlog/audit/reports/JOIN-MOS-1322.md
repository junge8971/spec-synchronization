# JOIN-MOS-1322 — точечная сверка, gap тела требования

## Результат и границы

**Question / keep U.** Тело MOS-1322 не сохранено; атомарные бизнес-требования и их выполнение установить нельзя. Заголовок `[B] Реализовать раздел "База знаний"` не превращён в требования ко всему KB. Нового member-level покрытия нет. HEAD по контракту WAVE-D090-EIGHT: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (независимо не перепроверялся). Только локальное чтение и запись этого отчёта; без сети, браузера, тестов, git-операций и изменения ledgers/checkboxes. Статика не подтверждает deployment.

Ниже `audit/` означает `openspec/changes/reconcile-control-center-backlog/audit/`; JSON-индексы нулевые.

## Атомарные источники: expected / observed / unknown

| Локатор | Expected для точного join | Observed | Unknown |
|---|---|---|---|
| `audit/sources/jira-member-index/r1/content.json:1214`, `$.items[140]` | Запись именно MOS-1322 и её тело | `key=MOS-1322`, summary выше, type `Development task`, status `Hold`, updated `2026-10-14T14:03:51.688+0800`, subtasks `[]`; только шесть полей | Description, критерии приёмки, комментарии, вложения и точный backend/frontend scope отсутствуют |
| `audit/sources/jira-member-index/r1/metadata.json`, `$.fields`, `$.limitations`, `$.retrievedAt` | Происхождение и полнота | Снимок `2026-10-16T11:20:38.570Z`; явно не собраны descriptions/comments/attachments/custom acceptance | Пустой subtasks не доказывает отсутствие скрытых задач; Hold не доказывает реализацию либо её отсутствие |
| `audit/sources/jira-hierarchy/r1/content.json:30`, `$.results[22].children[0]` | Точная принадлежность | MOS-1322 — ребёнок MOS-1328; сосед MOS-1362 — другая задача | Parent отсутствует в самой записи index; тело/приёмка не следуют из иерархии |
| `audit/sources/jira-subtasks/r1/content.json`, `$.items[*]` | Точный detail либо связанный subtask | Во всех 16 элементах нет key MOS-1322 и нет parent MOS-1322/MOS-1328 | Никакого требования этого member из пакета извлечь нельзя |
| Все файлы `audit/sources/**` — локальный поиск точной строки `MOS-1322` | Другой сохранённый detail-пакет | Только hierarchy и member-index содержат ключ | Связь без ключа не заменяет exact-member evidence; внешнее получение запрещено |

**Число извлечённых атомарных бизнес-требований: 0.** Это ограниченный source gap, не обнаруженный дефект приложения. Перечисленные поля — атомарные факты источника, а не acceptance criteria.

## Сверка с владельцами и существующими доказательствами

- `audit/reports/JIRA-MOS-1328.md:21–38` уже фиксирует ровно этот gap; он перепроверен по исходным пакетам, а не принят по заголовку. `audit/reports/G2-JIRA-MEMBER-JOINS.md:270`: `MOS-1322 | I(140) | U`, объяснение «optional KB capability acceptance not exact member attribution». `audit/coverage.json#/members/overlays` не содержит перехода для MOS-1322; определение U — unresolved/unexamined join, **не** отсутствие реализации.
- Main-контекст: `openspec/specs/knowledge-base-module/spec.md` (Default section inclusion, Removable module ownership, Shell integration, Unsupported features, Accessible states); `knowledge-base-registry/spec.md` (Server-owned registry selection; Metadata-driven supported conditions); `knowledge-base-editor/spec.md` (Persisted aggregate semantics); `knowledge-base-export/spec.md` (Full selection CSV export). Это владельцы capabilities, **не подтверждённые владельцы неизвестных требований MOS-1322**.
- Archive-контекст принятого прежнего анализа: `openspec/changes/archive/2026-10-14-add-optional-knowledge-base/` и `openspec/changes/archive/2026-10-15-update-control-center-api-contracts/specs/knowledge-base-registry/spec.md`. `audit/reviews/R-OPTIONAL-DOMAINS-SEVEN.md:9–23` принимает IMPL-KB-REGISTRY/EDITOR/EXPORT: registry tasks 4–5, API migration 4.1–4.4, editor 2.2–2.4/6–8, export 9.1–9.3. Использовано как прежнее capability-level доказательство, без новой выдачи покрытия member.
- Текущий узкий delta owner: `openspec/changes/fix-knowledge-base-export-limit-feedback/specs/knowledge-base-export/spec.md:3–27` уточняет HTTP 422 + `EXPORT_LIMIT_EXCEEDED`, собственную подсказку сузить отбор, сохранение полей, отсутствие файла/ложного успеха; отдельный сценарий исключает другую 422-ошибку. `audit/coverage.json` decision D-087 прямо говорит capability-level evidence, no Jira population transition. Привязывать этот delta к MOS-1322 нельзя без тела.

## API и код/тесты: проверенная граница, не приёмка MOS-1322

Сохранённый OpenAPI `audit/sources/api-live/r2/content.json`, точные JSON pointers:

- `$.paths["/api/control/api/v1/managed-resources/knowledge-base/metadata"].get`;
- `$.paths["/api/control/api/v1/managed-resources/knowledge-base/entries/search"].post`;
- `$.paths["/api/control/api/v1/managed-resources/knowledge-base/entries/{entity_id}"]` — get/put/delete;
- `$.paths["/api/control/api/v1/managed-resources/knowledge-base/entries"].post`;
- `$.paths["/api/control/api/v1/managed-resources/knowledge-base/entries/export"].post` и `$.paths["/api/control/api/v1/managed-resources/knowledge-base/entries/{entity_id}/export"].post`.

Observed: реальные декларации путей есть; generated-контракт `app/shared/api/schema.d.ts:1745–1808` также содержит metadata/search/detail/list export. `app/optional/knowledge-base/api/knowledge-base-client.ts:22–76` содержит metadata/lookups/search/detail/create/update с Zod-валидацией и ожидаемыми 200/201; это frontend client, не доказательство backend реализации. `api/knowledge-base-client.test.ts:27–98` содержит проверки detail/envelope/неверного DTO и статуса, metadata/lookups, defaults и невалидных search, POST 201/PUT null и массивов. Прочитаны определения тестов; запусков и утверждения «прошли» нет.

Expected для MOS-1322: сопоставить **каждую явно сформулированную операцию/границу** с API и реализацией. Unknown: какие из этих операций требуются именно MOS-1322, какие отсутствуют, какие backend-семантики и критерии успеха ожидались. Поэтому API не объявлен неприменимым, но requirement-to-API/code/test join заблокирован отсутствием body. Модульное покрытие и соседний MOS-1362 не заменяют этот join.

## Минимальная рекомендация

1. **keep:** сохранить U для MOS-1322 и существующие main/archive/delta владельцы без правок. Не менять исторические таблицы и checkbox-статусы.
2. **question:** нужен сохранённый detail MOS-1322 с description/acceptance и provenance; при наличии ссылок — их сохранённые тела. В этой волне внешнее получение не выполнять. До этого точный scope/owner остаётся unknown.
3. **update:** изменений specs/code/tasks по MOS-1322 не обосновано; допустима лишь фиксация этого source gap после независимого review.
4. **new:** новый corrective change не обоснован. Не дублировать уже принятый `fix-knowledge-base-export-limit-feedback` и не приписывать его этому member.

## SHA256 ключевых входов

Пути с префиксом `audit/` раскрываются как выше; SHA вычислены локально по байтам.

| Вход | SHA256 |
|---|---|
| `audit/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `audit/work-items/WAVE-D090-REVIEW-NEXT.md` | `fdf9ed7a57cc427bf9feb58639fe976fb2f76fb1bd9082c0f1626649cfdfcc72` |
| `audit/sources/jira-member-index/r1/content.json` | `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` |
| `audit/sources/jira-member-index/r1/metadata.json` | `6c93c19217dacdc18fbdffc95ecc2eaa326494a49eeab99559eca3b04647c89d` |
| `audit/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `audit/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `audit/sources/jira-hierarchy/r1/content.json` | `4d1881959ecbe13e4c2d4c27903b63a4ba71e1cba38e349dc33855a7e605fb77` |
| `audit/sources/api-live/r2/content.json` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `audit/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `audit/reports/JIRA-MOS-1328.md` | `e6bfae6a94f97c057b0e02ec87872d2fc5a8ce26bd74b4a2c1f3b26766e5c9d6` |
| `audit/reviews/R-OPTIONAL-DOMAINS-SEVEN.md` | `89358bd6009f0ca666439097083ff6aa24cd9acb858b7f09a3dc35e47b53a494` |
| `openspec/specs/knowledge-base-module/spec.md` | `7e9d5498dd603b9ef5e7b241f81857dc767c3532009fa68ede116f4e496809f0` |
| `openspec/changes/fix-knowledge-base-export-limit-feedback/specs/knowledge-base-export/spec.md` | `d811d2612b24415e32074c60397cf3d73b7669c6e1499f6f9e010fa170baded3` |
| `app/optional/knowledge-base/api/knowledge-base-client.ts` | `5d2301ed88ce900d775a9c6a6da559b4c45810b7703576ed022c3a75f1cb8971` |
| `app/optional/knowledge-base/api/knowledge-base-client.test.ts` | `9fc8a1824ad44bd17c02d6548ecc5aec5eddc1bda777f853a4d837d12fafab75` |
| `app/shared/api/schema.d.ts` | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Точный MOS-1322 проверен в сохранённых sources; отсутствие body явно ограничивает join; указаны owner/API/code/test контекст и минимальный question/keep."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-1322.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Локальные read/rg/find и Python JSON/SHA256 inspection","result":"passed","summary":"Точный ключ найден только в hierarchy/index; в 16 subtasks совпадений нет; SHA256 вычислены."},{"command":"Тесты, browser/network и git-операции","result":"not-run","summary":"Запрещены контрактом задания."}],
  "validationOutput": ["0 извлечённых бизнес-требований; U не повышен; capability evidence не присвоено member."],
  "residualRisks": ["Нет тела MOS-1322 и критериев приёмки; нельзя подтвердить полноту API/реализации для этой задачи.","Свежесть внешних систем и deployment не проверялись."],
  "noStagedFiles": true,
  "diffSummary": "Только отдельный отчёт; проектные файлы, ledgers и checkboxes не изменялись.",
  "reviewFindings": ["Source gap: description MOS-1322 отсутствует; новый corrective scope не обоснован."],
  "manualNotes": "Проверка статическая. noStagedFiles означает отсутствие staging в этом запуске, не независимую проверку git status. Отчёт требует отдельного пакетного review."
}
```
