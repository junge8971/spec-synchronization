# IMPL-MOS-920 — точное сопоставление UI / transport / mock / tests

## Результат и граница

**MOS-920 не подтверждён как реализованный пользовательский сценарий:** текущая страница эксплуатации показывает честную заглушку без бизнес-запросов. При этом пять операций модулей подключены в локальном mock server; существуют предметные тесты списка, мутаций, производных представлений и отказов.

Это новое implementation/test evidence к `SCENARIO-MOS-920`, а не повторный аудит требований. **Draft/status gate сохранён; интеграционная приёмка, закрытие задачи и deployment не подтверждены.** Никаких публикаций, изменений файлов, запусков тестов, сети, браузера или операций git не выполнялось. Отчёт возвращён для сохранения runtime в `audit/reports/IMPL-MOS-920.md`; кандидаты предназначены только родителю для `pending-publication.md`.

`A` далее — `openspec/changes/reconcile-control-center-backlog/audit`.

## Источники и воспроизводимость

Прочитаны назначение `A/work-items/WAVE-D093-LOCAL-EIGHT.md`, прежний отчёт и независимый review. Учтены исправления review:

- отсутствие ограничения в схеме **не доказывает**, что production backend принимает пустой текст или отсутствие подтверждения;
- состояние git index не проверялось и не аттестуется;
- отсутствие предметного клиента ниже ограничено просмотренным UI и поиском в `app`, а не всеми возможными сервисами.

Первичный источник: `A/sources/jira-operations-details/r1/content.json#/items/2`, строки 62–78:

- `key=MOS-920`, `status=Backlog`;
- `updated=2026-10-15T14:46:59.601+0800`;
- `retrievedAt=2026-10-16T13:02:57.740Z`;
- `/description`: сводка, список, «Что видит пользователь»; draft и подтверждение статуса перед интеграционной приёмкой; обязательные `user_message`, `confirm_impact=true`; ограничение `disable_allowed`; общая задача прав;
- `/comments/total=0`.

Метаданные r1 фиксируют общий сбор `2026-10-16T13:02:57.872Z`, неполученные custom fields/attachment bodies и отсутствие доказательства runtime/approval. Это **исторический cutoff сохранённого источника**, не текущий Jira-status.

Локально пересчитаны SHA-256:

| Вход | SHA-256 |
|---|---|
| WAVE-D093-LOCAL-EIGHT.md | `bfed26db7f9865a85e19e0cdfbeb0b92fc7b2b16999be3dac4d1cb92bd5eaf4e` |
| reports/SCENARIO-MOS-920.md | `d1587adf7b366f8c03ac97197f978ca7fab114515d47fb9c80d32571ecfe9883` |
| reviews/R-SCENARIO-MOS-920.md | `d1efb5f0b29510b6961d04185899c5b92532ff636ee24db3edf18824d8de11a9` |
| Jira r1 content.json, 9933 байта | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| Jira r1 metadata.json | `73e55adae262fba4222f1a701fe3152b001503ff5c0b3c10988a65bc575bbf8e` |
| app/pages/operations/ui/operations-page.tsx | `6100902a8833602c9d6fcc461429b9185079b7cdb6893829f30d588ee74753e9` |
| app/routes/entry-points.test.tsx | `3c6e58565c0f38e15452ab4487fa0f193ae07fa98a8cd6083300229c4dc654aa` |
| app/shared/api/http-client.ts | `e3ca2dbf67139ed26e86220a44dc18503068835d390f659c0eb2577fed5f1514` |
| app/shared/api/types/http-client.types.ts | `19a47a1a17c2d67a87b0b83366f441307d746bf026deba75d7131140f2cc3aee` |
| app/shared/api/schema.d.ts | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |
| mocks/assistant-modules.mjs | `0694eaff9bc872fc1fcd252d4fe76bbf7edd158c4495f78d402b311201f9ef23` |
| mocks/assistant-modules.test.mjs | `10f817be8e813fa4a03b50fdbbe6e471d0c4cabd729c932e612c816f8cbf5242` |
| mocks/app.mjs | `b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0` |
| mocks/contract.mjs | `ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371` |
| mocks/seed.json | `916f455f01ed4e106f85cf5b2224e7dbb653f559d4e72b722fd0845e4375763f` |
| docs/api/contracts/openapi.json | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| openspec/specs/control-center-mock-server/spec.md | `54cd451a911c13129fbf8be64b06f920a837d4c816255f6ee6f5ee65f4406588` |

Хеш текущего объединённого контракта — не хеш исторического `api-live/r1`. Их тождество не заявляется.

## Новое точное evidence

### 1. UI: опубликованная точка входа не является управлением модулями

**Expected:** Jira `/items/2/description` требует три бизнес-представления и управление disable с ограничениями.

**Observed:**

- `app/routes/operations.tsx:1` экспортирует `OperationsPage`.
- `app/pages/operations/ui/operations-page.tsx:6–29`: URL-вкладки, заголовок «Состояние системы»; для каждой вкладки только «Раздел в разработке». Нет списка, сводки, preview, toggle или формы подтверждения.
- `app/shared/config/constants/section-tabs.constants.ts:20–27`: `modules` — default, подпись «Модули и навыки».
- `app/routes/entry-points.test.tsx:17–42` прямо проверяет заглушку и отсутствие `fetch`; строки 49–64 включают `/ops` с default/`modules`/unknown и повторно проверяют отсутствие запросов.
- Это согласуется с существующим владельцем оболочки: `openspec/specs/control-center-shell/spec.md:179–218`, особенно требованием честных незавершённых entrypoints.

**Unknown:** поведение развернутого приложения. Прочитанные тесты не запускались.

**Вывод:** отсутствие предметного UI подтверждено непосредственным кодом и assertions, а не предположением по названию маршрута.

### 2. Transport: типизированный контракт есть, предметного подключения в просмотренном UI нет

**Observed:**

- `app/shared/api/schema.d.ts:600–684` содержит GET list/summary/preview и POST disable/enable.
- Поиск `assistant-modules`, `ModuleSummary`, `ModulePreview`, `disableModule` в `app` обнаружил соответствующие контрактные декларации, но не предметный клиент этих операций. Это ограниченный отрицательный результат; положительное основание — сам `OperationsPage` без data hooks.
- Общий `apiRequest` существует: `app/shared/api/http-client.ts`, функции `buildUrl`, `prepareRequest`, `apiRequest`, `readResponse`.
- `app/shared/api/types/http-client.types.ts:3–12` допускает только скалярные query values. `buildUrl` использует `searchParams.set(key, String(value))`, не массив повторённых `sort`.
- `app/shared/api/http-client.test.ts:91–110` проверяет общий URL, query и signal на пути skills, **не** подключение модулей.

**Expected/граница:** mock-spec `:138–150` требует повторённые `sort=status&sort=-name`. Общий scalar query API сам по себе не является доказательством поддержки такого предметного вызова. Сейчас нет просмотренного module caller, для которого можно констатировать пользовательскую поломку.

**Unknown:** будущий способ сериализации module query и фактическое поведение backend. Расширение transport не предлагается автоматически.

### 3. Mock: доказана цепочка регистрации всех пяти операций

Текущий `docs/api/contracts/openapi.json#/paths` содержит базу  
`/api/control/api/assistant-modules/v1/modules`, её `/summary`, `/preview`, `/{module_id}/disable`, `/{module_id}/enable` с соответствующими `operationId`.

Точный join:

1. `mocks/contract.mjs:6–8` читает именно `docs/api/contracts/openapi.json`.
2. `mocks/app.mjs:52` включает `assistantModulesHandlers(state)`.
3. `mocks/app.mjs:62–77` находит handler по `operationId`, преобразует путь и ставит контрактный validator перед handler.
4. `mocks/contract.mjs:71–73` удаляет `/api/control/api`; `mocks/app.mjs` монтирует router на `/api`.
5. `mocks/assistant-modules.mjs:77–94` предоставляет все пять именованных handlers.
6. `mocks/assistant-modules.test.mjs:8–32` обращается к `/api/assistant-modules/v1/modules` в тестовом Express app.

Это подключение локального server-контракта, **не подключение frontend и не production transport evidence**.

### 4. Список / summary / preview: реализации и конкретные assertions

| Expected, существующий owner | Observed implementation | Прочитанные tests |
|---|---|---|
| Mock list: поиск, фильтр, сортировки до пагинации; spec `:138–155` | `mocks/assistant-modules.mjs:4–14`: поиск по code/name/description без учёта регистра, точный status, default name, затем page | `assistant-modules.test.mjs:35–92`: одиночный и повторённый sort, регистр поиска, limit/offset, unknown/empty status, отсутствующий результат, offset за концом |
| Coherent summary; spec `:157–176` | `assistant-modules.mjs:16–36`: totals по коллекции, healthy/degraded, banner, disabled ids | `test.mjs:102–131`: totals, state, tone, множество disabled ids |
| Preview «Что видит пользователь» как локальная модель; spec `:168–176` | `assistant-modules.mjs:38–51`: одна fallback-card на disabled module, сохранённый текст либо локальный default | `test.mjs:102–131`: ids, число cards, type, name, message, sample |
| Все представления после мутаций и restart | Общий `state.modules`; `mocks/state.mjs:11–16` клонирует seed | `test.mjs:133–180`: disable/enable, повторные переходы, healthy/degraded, новый server восстанавливает исходные views |

**Unknown:** реальные пользовательские ответы ассистента и глобальная доставка состояния на поверхности. Согласованность трёх mock views этого не доказывает.

### 5. Disable/enable: ограничения, версии и важная граница бизнес-семантики

**Expected:** Jira требует `disable_allowed`, `user_message`, `confirm_impact=true`; локальная mock-spec `:161` отдельно устанавливает более слабую конвенцию текста/подтверждения.

**Observed:**

- `mocks/assistant-modules.mjs:53–57`: запрет при `disable_allowed=false`; подтверждение требуется только при непустом `disable_impact_message`.
- `:59–75`: сначала 404, затем версия/409; отказ до мутации; успех увеличивает version, обновляет timestamp, назначает фиксированного `state.users[0]`, disable сохраняет `user_message ?? ''`, enable ставит null.
- `mocks/seed.json#/modules/0`: разрешённый search с impact; `/modules/1`: recommendations без impact; `/modules/2`: запрещённый core. Отдельный classifier seed в просмотренном массиве отсутствует; запрет в handler универсальный по флагу, не по имени.
- `docs/api/contracts/openapi.json#/components/schemas/DisableModuleRequest`: required только expected_version, minimum 1; confirm default false, message default empty. Это выразительность схемы, **не разрешение production backend**.
- `mocks/contract.mjs:139–178` валидирует обязательное тело и схему до handler; `:180–197` проверяет success envelope по response schema.

Новые точные test anchors:

- `mocks/assistant-modules.test.mjs:133–156`: disable с сообщением/подтверждением, version/time/actor и последующие views.
- `:157–165`: повторный disable с актуальной версией **без user_message**, ожидаются новая версия и пустая строка.
- `:166–172`: enable и повторный enable с актуальной версией.
- `:173–177`: recommendations без impact выключается **без confirm_impact и user_message**.
- `:182–246`: invalid query/body/UUID → 422; отсутствующий id → 404; stale version → 409; отсутствие/false impact confirmation и protected module → `MODULE_CONFLICT`; строковый confirm и null message → 422; финальные assertions сохраняют `state.modules` и все views.

Таким образом, ослабленная локальная конвенция подтверждена не только прежней спецификацией, но и конкретной реализацией/assertions. **Это не новый дефект относительно принятой mock-spec и не основание менять её без согласования.**

### 6. Ownership

- `/ops` и честная заглушка: shell / `pages/operations`.
- Запросы общего назначения: `shared/api`; предметный module transport не обнаружен указанным поиском.
- Локальные пять операций: `mocks/assistant-modules.mjs`, регистрация в `mocks/app.mjs`, owner `control-center-mock-server`.
- Доступ вкладки: `app/application/constants/route-access.constants.ts:21` использует `p.moduleView`. Это locator существующего общего ownership прав, не аудит его полного enforcement.
- Никакие роли, auth-модели, request ACL или правила production здесь не вводятся. Mock actor — бизнес-fixture, не подтверждённый посетитель.

Прочитаны proposal/design и mock delta `archive/2026-10-09-add-local-session-demo`; сохранена граница credential-free business mocks и UI-only permissions. Исторические auth approvals из discovery map не переаттестовывались и не превращались в module approval.

## Минимальные решения для очереди родителя

| Решение | Кандидат и основание |
|---|---|
| **keep** | Сохранить MOS-920 Backlog/draft gate как исторически зафиксированный статус; не закрывать по наличию пяти mock handlers или generated types. Свежего Jira/approval нет. |
| **update** | Дополнить evidence MOS-920 точной формулировкой: «UI остаётся заглушкой без запросов; локальные list/summary/preview/enable/disable зарегистрированы и имеют предметные тесты, прочитанные, но не запущенные». Anchors — разделы 1–5. |
| **update** | Уточнить прежний вопрос C07/C08: conditional confirmation/empty message подтверждены текущим mock-кодом и тестами `:157–177`; это принятая локальная конвенция, не доказанная production-семантика. |
| **question** | Перед будущим предметным подключением уточнить утверждённые disable semantics и способ сериализации multi-sort; существующий scalar query transport не доказывает поддержку повторённых параметров. Политику здесь не выбирать. |
| **new: нет** | Отдельная новая задача/смена owner не обоснована: MOS-920 уже содержит недостающий UI, mock-конвенции имеют существующего владельца. Новое здесь — evidence, не новый business scope. |

Кандидаты **не опубликованы и не записаны в очередь** этим агентом. Переход U→P и повторный зачёт ранее установленного P не заявляются.

## Проверки и ограничения

Выполнены только чтение, локальный поиск, SHA-256 и выборочная JSON-инспекция текущего контракта. Попытка поиска в `tests/` показала отсутствие такого каталога; тесты найдены рядом с исходниками. Полные quality gates, mock HTTP tests, browser/E2E, build и network не запускались по запрету задания.

Обязательные локальные источники доступны; execution blocker отсутствует. Product ambiguity зарегистрирована, но не разрешалась. Исторический источник ограничен r1 от 16.10.2026; текущие файлы идентифицированы хешами, baseline HEAD из задания независимо не проверялся. Ни локальный код, ни тестовые assertions не удостоверяют deployment, успешность тестового прогона, глобальные эффекты или интеграционную приёмку.