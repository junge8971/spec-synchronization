# JOIN-MOS-1150 — число модулей в ответе реестра

## Граница и источники

Проверка только MOS-1150, статическая, по сохранённым материалам. HEAD по контракту `WAVE-D090-EIGHT.md`: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (самостоятельно git не проверялся). Ни runtime, ни deployment, ни закрытие Jira не подтверждаются. Далее `audit/` означает `openspec/changes/reconcile-control-center-backlog/audit/`.

- **Тело прочитано:** `audit/sources/jira-subtasks/r1/content.json#/items/1/description`, строка 33; идентичность `/items/1/key`, `/parent`, `/status`, строки 26–32: MOS-1150 → MOS-816, Ready for test. Снимок от 2026-10-16T11:23:01.951Z, обновление задачи 2026-10-09T15:06:03.028+0800.
- Независимый locator членства: `audit/sources/jira-member-index/r1/content.json#/items/44/subtasks/0`, строки 364–377. Это не источник требований.
- `audit/sources/jira-subtasks/r1/metadata.json`: selected-field-redacted-extraction; bearer заменён на `[REDACTED]`; вложения не скачаны, комментарии/custom acceptance fields отсутствуют.
- Повторно использована только инвентарная граница `audit/reports/JIRA-MOS-771.md:17–37`; `G2-JIRA-MEMBER-JOINS.md:297` оставлял MOS-1150 в U, а не доказывал реализацию. `coverage.json#/modules` прямо не сертифицирует полноту семантического анализа. Покрытие родительского модуля не подменяет этот join.

## Атомарное требование и сверка

| Атом / locator | Expected из тела | Observed в текущем репозитории | Unknown |
| --- | --- | --- | --- |
| R1 — `/items/1/description`, запрос и ОР | `GET /api/control/api/assistant-modules/v1/modules?limit=20&offset=0`: при шести найденных модулях `data.items` содержит все 6 | API содержит этот GET и массив `ModuleListResponse.items`. Mock передаёт весь отфильтрованный массив в `page`, а тот возвращает `slice(0,20)`; при входных 6 элементах статически получается 6 | Реальный ответ backend, состав шести модулей и исправление исходного дефекта не доступны |
| R2 — тот же locator, ФР/ОР | `pagination.total_items=6` не должен сочетаться с единственным элементом первой страницы при limit=20 | `mocks/list.mjs:3–15`: items и total_items вычисляются из одного массива; total_items — размер всей выборки. Тест `mocks/assistant-modules.test.mjs:34–91` проверяет все 3 seed-модуля с total_items=3, отдельную страницу и выход за конец | Нет прочитанного точного теста с шестью модулями; существующий тест не исполнялся. Схема сама по себе не запрещает расхождение длины items и total_items |

R1/R2 — две проверяемые стороны одного дефекта, не два новых feature scope. Нельзя обобщать ОР до `items.length === total_items` на всех страницах: это верно здесь из-за offset=0 и limit=20 > 6.

ФР в сохранённом теле: total_items=6, items содержит один модуль; корреляция `x-request-id: d25144135c46c57e0c040f5d1fccd1ff`. Это свидетельство исторического сообщения, не воспроизведение сейчас. Тело **не отсутствует**. Ограниченный source gap: `content.json#/items/1/attachments/0` (строки 35–41), JSON 831194, и `/attachments/1` (42–48), PNG 831195, сохранены только как metadata. Поэтому нельзя проверять конкретные ID, содержимое JSON-ответа и изображение; JSON-вложение не следует считать screenshot-only.

## API, owner, code/tests

- Контракт: `docs/api/contracts/assistant-modules.openapi.json#/paths/~1api~1control~1api~1assistant-modules~1v1~1modules/get` (operationId `get_module_list_api_control_api_assistant_modules_v1_modules_get`), `/parameters/3` — limit 1–100/default20, `/parameters/4` — offset>=0/default0; `/responses/200` → `TsamResponseSchema_ModuleListResponse_`; `#/components/schemas/ModuleListResponse` требует items и pagination. Ограничения равенства/кардинальности между полями нет. Человекочитаемая версия: `docs/api/contracts/assistant-modules.md:23–33`.
- Исторический bearer-пример не предписывает возврат прежней auth-модели: текущий GET использует AdminToken + AccessToken. Это не предмет MOS-1150; согласованная политика не пересматривается.
- **Main owner локального поведения:** `openspec/specs/control-center-mock-server/spec.md:138–156`, Requirement `Module registry query behavior`: фильтрация/сортировка до пагинации, запрошенный срез и согласованные totals, пустая страница за концом. Это явно mock-конвенция, а не обещание исправленного production backend.
- **Archive provenance:** `openspec/changes/archive/2026-09-28-update-assistant-modules-contract/specs/control-center-mock-server/spec.md:29–47` содержит тот же добавленный requirement. Архив не переписывать. Отдельного активного delta-владельца MOS-1150 по поиску ключа и module-list требования не найдено; создавать дублирующий UI-change оснований нет.
- **Реализация:** `mocks/assistant-modules.mjs:4–14` — фильтрация, сортировка, page; `:76–79` — handler списка; `mocks/list.mjs:3–15` — срез и totals. Это локальный Express mock, не исходники backend MOS-816.
- **Тестовая связь:** `mocks/assistant-modules.test.mjs:34–91` — конкретный список и пагинация, включая empty/past-end. Три элемента, не шесть; статическое свидетельство алгоритма, не новый passed-test. Поиск `assistant-modules` и `modules/v1/modules` в app нашёл только generated API declarations (`app/shared/api/schema.d.ts:600–616` для GET списка), не UI-потребителя, который мог бы восстановить недостающие элементы ответа.

## Минимальные решения

1. **keep:** main requirement, API shape, текущий mock и существующий тест. Подтверждённого дефекта frontend/mock для данного кейса нет; нельзя синтезировать отсутствующие backend-модули по total_items.
2. **question:** оставить backend-выполнение MOS-1150 неподтверждённым. Для закрытия нужен сохранённый ответ точного GET при шести найденных модулях и проверка всех шести элементов/total_items; текущий статус Jira этого не доказывает. Внешний сбор в этой работе не выполняется.
3. **update (необязательное точечное усиление доказательств, не реализовано):** если требуется буквальный regression join, дополнить `mocks/assistant-modules.test.mjs` кейсом с 6 уникальными модулями, явными limit=20/offset=0, проверкой идентичностей всех items и total_items=6; сохранить существующие граничные проверки пагинации. Такой тест докажет только локальный mock.
4. **new:** новый change/spec/UI не требуется на основании прочитанного тела. Ledger, checkbox и исторические отчёты не менять до независимого review.

## SHA256 ключевых прочитанных входов

Хэши вычислены локально по байтам, не взяты на веру из metadata.

| Файл | SHA256 |
| --- | --- |
| audit/work-items/WAVE-D090-REVIEW-NEXT.md | fdf9ed7a57cc427bf9feb58639fe976fb2f76fb1bd9082c0f1626649cfdfcc72 |
| audit/work-items/WAVE-D090-EIGHT.md | 98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b |
| audit/sources/jira-subtasks/r1/content.json | c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e |
| audit/sources/jira-subtasks/r1/metadata.json | d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20 |
| audit/sources/jira-member-index/r1/content.json | dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043 |
| audit/coverage.json | e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b |
| audit/reports/JIRA-MOS-771.md | 1b911c0bd65d28ccdf03bc8efe10a8a6bfe58cf23d6aef9c7a1e91f3f3aba899 |
| openspec/specs/control-center-mock-server/spec.md | 54cd451a911c13129fbf8be64b06f920a837d4c816255f6ee6f5ee65f4406588 |
| openspec/changes/archive/2026-09-28-update-assistant-modules-contract/specs/control-center-mock-server/spec.md | 53b521df7c1621fc12bca39d35f6490de9ff39078003b7e3e7a18a1ed629a6cb |
| docs/api/contracts/assistant-modules.openapi.json | 79b96aff9cd84c88c2aee843a5d3f87f83ee999c25ee6e3e361f4bcb7a708052 |
| docs/api/contracts/assistant-modules.md | 07390fd25dcba4be87387af11a60116a6709afcd559d9214908c2e1945fe4933 |
| mocks/assistant-modules.mjs | 0694eaff9bc872fc1fcd252d4fe76bbf7edd158c4495f78d402b311201f9ef23 |
| mocks/list.mjs | e1af394687dd92e656f0e0def06e3206a9eb217a43a5f366e6d410d622a34b7c |
| mocks/assistant-modules.test.mjs | 10f817be8e813fa4a03b50fdbbe6e471d0c4cabd729c932e612c816f8cbf5242 |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Точное тело MOS-1150 /items/1/description сопоставлено с GET API, main/archive owner и конкретным алгоритмом/тестом; unknown отделены от наблюдений."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-1150.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Локальный Python: чтение JSON операции/схемы и SHA256 ключевых файлов","result":"passed","summary":"Параметры, response shape и хэши прочитаны без внешнего доступа."},{"command":"Тесты, typecheck, lint, build","result":"not-run","summary":"Запрещены заданием; анализ read-only."}],
  "validationOutput": ["Тело задачи доступно; mock использует общий массив для среза и total_items; точного шестимодульного runtime-свидетельства нет."],
  "residualRisks": ["Исправление реального backend и deployment неизвестны.","Вложения 831194/831195, комментарии и custom acceptance fields отсутствуют.","Существующие тесты прочитаны, но не запускались; fixture содержит 3 модуля."],
  "noStagedFiles": true,
  "diffSummary": "Только назначенный аналитический отчёт; код, контракты, исторические реестры и checkbox не изменены.",
  "reviewFindings": ["Нет основания для нового frontend-change; backend completion требует отдельного доказательства."],
  "manualNotes": "Сеть, браузер, тесты, git mutations и child fanout не использовались. noStagedFiles означает отсутствие staging действий в этом запуске, не самостоятельный git-status аудит. Требуется независимый пакетный review."
}
```
