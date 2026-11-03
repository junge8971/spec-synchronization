# JOIN-MOS-1323 — ограниченный gap точного member

## Результат и границы

**question / U: тело MOS-1323 в сохранённых пакетах отсутствует.** Атомарные бизнес-требования задачи восстановить нельзя; соответствие реализации и завершённость задачи не установлены. Заголовок `[B] Реализовать раздел "A/B Эксперименты"` не используется как спецификация backend или всего раздела.

Контракт: `audit/work-items/WAVE-D090-REVIEW-NEXT.md` и `WAVE-D090-EIGHT.md`. HEAD из контракта: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (в этом запуске Git не проверялся). Здесь `audit/` = `openspec/changes/reconcile-control-center-backlog/audit/`; JSON-индексы нулевые. Прочитаны локальные материалы; единственная запись — этот отчёт. Исторические ledger/checkboxes не изменены.

## Точные источники: expected / observed / unknown

| Атом доказательства | Expected | Observed | Unknown |
|---|---|---|---|
| Идентичность member | Найти точный ключ, не соседнюю FE-задачу | `audit/sources/jira-member-index/r1/content.json:$.items[142]`, строки 1229–1236: MOS-1323, Development task, Hold, updated `2026-10-14T14:03:53.543+0800`, subtasks=[] | Hold не доказывает состояние кода или развёртывания |
| Принадлежность | Установить родительский контекст независимо от summary | `audit/sources/jira-hierarchy/r1/content.json:$.results[23].children[0]`, строка 31: MOS-1329 → MOS-1323; children[1] — отдельный MOS-1384 | Полнота видимости Jira не установлена |
| Тело и acceptance | Прочитать description и извлечь атомарные требования | У `$.items[142]` отсутствует description; `jira-member-index/r1/metadata.json:$.fields,$.limitations` прямо исключает descriptions/comments/attachments/custom acceptance | Все предметные acceptance MOS-1323, связанные вложения, комментарии и критерии backend неизвестны; отсутствие поля не означает пустое тело в Jira |
| Дополнительный exact-body | Проверить subtask и прочие сохранённые пакеты | Все 16 `jira-subtasks/r1/content.json:$.items[*]` проверены: нет key или parent MOS-1323. Поиск `MOS-1323` во всех сохранённых `.json/.txt/.md` в sources дал только member-index и hierarchy | Не заявляется просмотр бинарных вложений; нет доказательства, что безымянные материалы являются телом MOS-1323 |

Итог: **0 доступных атомарных требований задачи**, а не «0 невыполненных требований». Нет основания приписать MOS-1323 CRUD, CSV, статистику, распределение трафика или конкретные поля DTO.

## Сопоставление owner / API / code — только контекст, не member coverage

1. **Main owner:** `openspec/specs/ab-testing-module/spec.md:9–58`, в частности `Configuration is not execution` (37–44): настройка и сохранение статусов не означают исполнение экспериментов. Связанные main capabilities — `openspec/specs/ab-testing-{registry,editor,export}/spec.md`. Их покрытие повторно не засчитывается MOS-1323.
2. **Archive:** `openspec/changes/archive/2026-10-15-add-optional-ab-testing/{proposal,design}.md` — исторический owner удаляемого configuration-only раздела. Использован принятый документальный разбор `audit/reports/DELTA-AB-TESTING-ROOT-DOC.md`, ABROOT-03/05/06/08, и его независимый `audit/reviews/R-DELTA-AB-TESTING-ROOT-DOC.md` с ACCEPT. Приёмка ограничена документальным supplement и явно не удостоверяет реализацию/member completion. Это reuse, не новая проверка архива или wiki-вложений.
3. **Active delta:** `openspec/changes/clarify-ab-testing-sample-size/specs/ab-testing-editor/spec.md:3–23` уточняет единственный nullable scalar min_sample_size «в каждой группе», без вычисления статистики/управления трафиком. `audit/coverage.json:$.activeChanges.additionalAcceptedChanges` (строка 325) фиксирует owner, D-087 / D-086. Привязка этой delta к MOS-1323 не доказана; новый дублирующий change не нужен.
4. **API observed:** `app/shared/api/schema.d.ts:1849–1929` содержит managed-resources/ab-testing metadata, POST experiments/search, GET/PUT/DELETE experiments/{entity_id}, list/detail export. Наличие локального generated-контракта опровергает лишь предположение «в проекте вообще нет A/B API», но не доказывает реализацию backend, полноту операций MOS-1323 или доступность сервера. Сравнение expected DTO/операций точной задачи невозможно без её тела; API не объявляется неприменимым.
5. **Code observed:** `app/optional/ab-testing/model/ab-testing-queries.ts:13–65` связывает search/detail/metadata/lookups с query API и существующими permissions/session-owner guards. Это frontend-интеграция; не доказательство серверного исполнения.
6. **Tests observed, не запускались:** `app/optional/ab-testing/api/ab-testing-client.test.ts:21–125` описывает проверки malformed envelope/detail, metadata/lookups, server search и локальной валидации, POST 201 / partial PUT с null и group identity, groups_count metadata. Fetch подменяется; эти тесты не являются acceptance MOS-1323 и не подтверждают live backend. Их успешность в текущем состоянии не проверялась.

**Expected для member:** неизвестен. **Observed:** сохранённый member без тела и существующий ограниченный frontend/API owner. **Unknown:** точный join требований MOS-1323 → main/delta/archive → endpoint → code/test. Это ограниченный source gap, не обнаруженный дефект продукта.

## Минимальные решения

- **keep:** сохранить действующие A/B owners и границу configuration ≠ execution; исторические отчёты/статусы не переписывать. Согласуется с `audit/reports/JIRA-MOS-1329.md:21–37` и `audit/reports/G2-JIRA-MEMBER-JOINS.md:272` (I(142), U/U0).
- **question:** необходим сохранённый полный issue MOS-1323: description, acceptance/custom fields, комментарии и индекс/содержимое релевантных вложений. Получение извне в этом запуске запрещено и не выполнялось. До появления такого источника оставить exact-member join неизвестным.
- **update:** только evidence-join после появления тела и независимой приёмки; сейчас нет обоснованного изменения spec/code.
- **new:** не предлагать новую capability/change на основании заголовка либо чужого module coverage.

## SHA256 ключевых входов

Вычислены локально по байтам Python hashlib; первые пять источников и coverage расположены под `audit/`.

| Вход | SHA256 |
|---|---|
| sources/jira-member-index/r1/content.json | dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043 |
| sources/jira-member-index/r1/metadata.json | 6c93c19217dacdc18fbdffc95ecc2eaa326494a49eeab99559eca3b04647c89d |
| sources/jira-subtasks/r1/content.json | c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e |
| sources/jira-subtasks/r1/metadata.json | d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20 |
| sources/jira-hierarchy/r1/content.json | 4d1881959ecbe13e4c2d4c27903b63a4ba71e1cba38e349dc33855a7e605fb77 |
| coverage.json | e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b |
| audit/reports/DELTA-AB-TESTING-ROOT-DOC.md | cd8cb41cc08c0f2400a03dc842f089eec3f1c393e8db8070ffc11f65f91fea69 |
| audit/reviews/R-DELTA-AB-TESTING-ROOT-DOC.md | 3db6568ae32989577ee8271a092d41c44abf9fd2c1bb6e3f705c10ceb2b9ce82 |
| openspec/specs/ab-testing-module/spec.md | 0013ea05d4c913d321baae18dca1076029792bf58ffc06e6a1715d53eca60366 |
| openspec/changes/clarify-ab-testing-sample-size/specs/ab-testing-editor/spec.md | b1741fd5bde9283f4cdccf85078f8f09e0b4d223c145b5b217fac0980e2508fe |
| app/optional/ab-testing/model/ab-testing-queries.ts | b547e01fd47b3e6e2be26ecdd070ca9be5377117a50b82687009392f147afbca |
| app/optional/ab-testing/api/ab-testing-client.test.ts | 7cb9da6526132daf9a744b4d9c529de1105a4fe8d6bdd527edadcb61a466dc9d |
| app/shared/api/schema.d.ts | 394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d |

## Проверки и риски

Только read/grep/find и read-only Python для точного поиска, JSON и SHA256. Нет браузера/сети, запуска тестов, business API, Git-мутаций, child fanout или утверждений о deployment. Staging не проверялся. Главный остаточный риск — отсутствие тела задачи; принятые module-отчёты этот gap не закрывают.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Точный member I(142), отсутствие тела, owner/API/code контекст и ограниченный question зафиксированы без подмены module coverage."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-1323.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"read-only Python: exact-key source search, JSON member/subtask inspection and hashlib.sha256","result":"passed","summary":"Один member I(142), 0 совпадений key/parent среди 16 subtasks; source mentions только в index/hierarchy; вычислены SHA256."}],
  "validationOutput": ["description отсутствует в сохранённой записи; metadata явно исключает сбор тела."],
  "residualRisks": ["Acceptance MOS-1323 неизвестен без тела; полнота backend и runtime не проверялась.","Git/staging и успешность тестов не проверены."],
  "diffSummary": "Только назначенный отчёт; проектные и исторические артефакты не изменялись.",
  "reviewFindings": ["question: требуется полный сохранённый issue MOS-1323; оснований для нового spec/code change нет."],
  "manualNotes": "Локальная статическая сверка; тесты и внешние обращения запрещены и не выполнялись. Нет утверждения о завершённости member или deployment."
}
```
