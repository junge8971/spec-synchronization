# IMPL-MOS-923 — точное сопоставление реализации окон технических работ

## Результат и границы

**Наблюдается частичное техническое покрытие, но не реализованный пользовательский сценарий:** вкладка содержит заглушку; пять операций представлены в generated-типах и Express-моках; имеются исходники HTTP-тестов. Клиентский список, форма и вызовы maintenance API в исследованном пути страницы не обнаружены.

Новое доказательство этого отчёта — связка **MOS-923 → текущая страница → контрактные типы → конкретные mock handlers → конкретные assertions**, а не повтор C01–C18 из `SCENARIO-MOS-923`.

Проверен только MOS-923. MOS-920, редактор заглушек MOS-922 и read-only MOS-1026 не присваиваются этому исполнителю. Исходники не изменялись; публикаций, запуска тестов, сети, браузера и git-команд не было. Отчёт предназначен для сохранения runtime в `audit/reports/IMPL-MOS-923.md`. Кандидаты ниже передаются parent для очереди `pending-publication.md`, которая здесь не изменялась.

## Источники и точные привязки

Здесь `A` = `openspec/changes/reconcile-control-center-backlog/audit`.

- **Jira:** `A/sources/jira-operations-details/r1/content.json`, `/items/4/key`, `/items/4/description`, `/items/4/status`, `/items/4/updated`. Точный member — MOS-923, Backlog, обновлён `2026-10-15T14:46:40.107+0800`; сохранён `2026-10-16T13:02:57.871Z`.
- **Ожидаемое из тела:** список и форма с title, timezone, starts_at/ends_at, warning_ahead_minutes, scope.targets, текстами и priority; пять API-состояний; редактирование и отмена; без скрытых случайных defaults; расчёт пересечений сервером.
- **Wiki, только необходимые ограничения:** `A/sources/wiki-241092242/r1/content.json`, `/bodyView`, §2.8 «Правила изменения», §2.9 «Правила отмены». Содержимое HTML разобрано как инертный текст.
- **Контракт текущего дерева:** `docs/api/contracts/openapi.json`, `/paths/~1api~1control~1api~1maintenance~1v1~1maintenance-windows` и пути с `/{window_id}`, `/{window_id}/cancel`; `/components/schemas/CreateMaintenanceWindowRequest`.
- **Карты discovery:** `A/reports/SCENARIO-MOS-923.md` и `A/reviews/R-SCENARIO-MOS-923.md`. Review имеет решение **REVISE**, поэтому исходный отчёт не выдаётся за безусловно принятый. Поправки review сохранены: историческое auth-подтверждение не отменяется; одинаковая specificity не приравнивается к одинаковому scope; отсутствие найденного плана не означает отсутствие владельца.

### SHA-256 фактически прочитанных входов

Все значения вычислены заново локально.

| Файл | SHA-256 |
|---|---|
| `A/work-items/WAVE-D093-LOCAL-EIGHT.md` | `bfed26db7f9865a85e19e0cdfbeb0b92fc7b2b16999be3dac4d1cb92bd5eaf4e` |
| `A/reports/SCENARIO-MOS-923.md` | `1abac025006e86bcb7e2dfd2355a1b289db27ccdf0f35a2ff96ce6bbf240bd96` |
| `A/reviews/R-SCENARIO-MOS-923.md` | `49e6f4a97816235da21ea347955f5d822d8aa51037349514f558e402aaa0a565` |
| `A/sources/jira-operations-details/r1/content.json` | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| `A/sources/wiki-241092242/r1/content.json` | `e7b78965be979f2bd450b25881574cf7e8b94cf424be5d052bb2be9df1995158` |
| `A/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `app/pages/operations/ui/operations-page.tsx` | `6100902a8833602c9d6fcc461429b9185079b7cdb6893829f30d588ee74753e9` |
| `app/routes/operations.tsx` | `2041de44a524f1ddc86469ecddf128efc8ae8e6fecb0589c81040d04f032dffc` |
| `app/routes/entry-points.test.tsx` | `3c6e58565c0f38e15452ab4487fa0f193ae07fa98a8cd6083300229c4dc654aa` |
| `app/shared/api/schema.d.ts` | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `mocks/maintenance.mjs` | `1e64344fc0ae29188155e0f32168d60d5d5051dfa500b658dad897517965e646` |
| `mocks/api-update.test.mjs` | `793fb807cae6203c3d1336c15be1fd0b09d785b949e601a7dca75ee9c1e74ddb` |
| `mocks/contract.test.mjs` | `a7096b8cf8ff74a162245ae96260cb282b09cdb21e278ccafaca298406c441d0` |
| `mocks/app.mjs` | `b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0` |
| `mocks/contract.mjs` | `ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371` |

## Expected / observed / unknown

| Область | Expected | Observed — новое implementation/test evidence | Unknown / предел вывода |
|---|---|---|---|
| UI списка и формы | Поля и действия из `/items/4/description` | `app/routes/operations.tsx:1` экспортирует OperationsPage. `app/pages/operations/ui/operations-page.tsx:6–29` создаёт вкладки, а каждый panel выводит «Раздел в разработке». Ни формы, ни загрузки окон здесь нет. | Не подтверждается доставка сценария в иной ветке или deployment. |
| UI-тест | Сценарий создания/изменения/отмены | `app/routes/entry-points.test.tsx:44–64`, включая maintenance на строке 52, проверяет выбранную вкладку, заглушку и **отсутствие fetch**. Это тест честного unfinished-state, не CRUD. | Тесты не запускались; их прохождение не заявляется. |
| Типы и transport | Пять контрактных операций | `app/shared/api/schema.d.ts:1260–1312` содержит GET/POST collection, GET/PUT detail, POST cancel; DTO — `4398–4429`, state enum — `4611–4614`, operation definitions — `9163–9331`. Поиск `maintenance|Maintenance` в `app` не выявил отдельного потребителя этих операций помимо схемы и shell/access references. | Generated-типы не являются исполняемым transport-клиентом или backend-проверкой. |
| Express wiring | Доступные локальные операции | `mocks/app.mjs:35–78`: подключение `maintenanceHandlers`, регистрация по operationId и request validation. `mocks/contract.mjs:6–8,72–74` читает текущий OpenAPI и удаляет префикс `/api/control/api`; `app.mjs:104` монтирует `/api`. Локальный путь поэтому `/api/maintenance/v1/maintenance-windows`. | Это mock transport, не свидетельство реального маршрута сервера. |
| Создание и базовая валидация | Явные обязательные поля; валидные интервал/timezone/scope | `mocks/maintenance.mjs:14–37,45–63`: строгий порядок времени, проверка timezone через Intl, непустые известные targets, создание объекта; nullable тексты нормализуются в null. Требуемые поля и warning minimum 0 заданы `CreateMaintenanceWindowRequest`, проверяются общим AJV. | Каталог `syncStubSettings` — локальное решение мока, не согласованный production API выбора targets. |
| Проверки границ | Ошибочный ввод не создаёт/не портит запись | `mocks/api-update.test.mjs:239–265`: равные даты, неверная timezone, отрицательное предупреждение и пустой scope ожидают 422; массив остаётся пустым. Невалидный объединённый интервал PUT сохраняет прежнюю запись. | Это найденные assertions, не результаты исполнения. |
| List/detail/edit/cancel | Основной связный сценарий | `mocks/contract.test.mjs:405–433`: create → PUT → GET → filtered list → cancel; проверяются title, total_items, canceled и false application. `mocks/api-update.test.mjs:266–296`: защита id/by/created_at, сохранение title при null, очистка banner_text, фильтры, обязательный reason, сохранённая причина, canceled-edit 409, missing GET 404 и invalid state 422. | Не покрывает active/completed lifecycle, гонку окончания или конфликт пересечений. |
| Состояния во времени | API draft/scheduled/active/completed/canceled | `mocks/maintenance.mjs:39–43` вычисляет только scheduled/active/completed; create и update используют эту функцию. GET/list (`89–110`) возвращают сохранённое состояние без пересчёта времени. Cancel выставляет canceled (`115–123`). | Draft-команда не установлена; автоматический переход с течением времени этим кодом не реализован. Нельзя превращать mock clock logic в клиентскую политику. |
| Ограничения изменения | Wiki §2.8 запрещает terminal edits и изменение starts_at/timezone/targets после старта | `mocks/maintenance.mjs:65–84` блокирует только canceled; другие разрешённые схемой поля объединяются с записью независимо от active/completed. | Статическое расхождение мока с wiki; не доказанный production backend defect. |
| Отмена | Wiki §2.9 исключает completed, требует конфликт при завершении во время запроса | `mocks/maintenance.mjs:115–123` после проверки существования отменяет запись без проверки состояния или времени. | В найденных тестах нет completed-cancel/race assertions. Повторная отмена также не ограничена этим handler. |
| Пересечения и приоритеты | Jira оставляет расчёт серверу | В `validateWindow/createWindow/updateWindow` нет сравнения с другими окнами по priority/scope. | Это не реализованный серверный алгоритм и не подтверждение допустимости пересечения. Уточнение определения «той же области» остаётся вопросом, а не доказанным противоречием правил. |

## Минимальные решения и кандидаты для parent

### KEEP

1. **Сохранить честную заглушку и существующий shell-тест** до отдельной реализации MOS-923. Их наличие не закрывает Jira.
2. **Сохранить имеющиеся типы, mock CRUD и проверки базового ввода** как частичное покрытие. Не называть API отсутствующим и не выдавать мок за готовый UI.
3. **Сохранить серверное владение приоритетами и пересечениями.** Не добавлять клиентский scheduler по результатам этого отчёта.

### UPDATE — кандидат текста состояния MOS-923

> В текущем дереве вкладка «Технические работы» остаётся заглушкой без бизнес-запросов. Пять операций описаны generated-типами и реализованы локальными HTTP-моками; исходники тестов покрывают базовый CRUD и часть валидации. Пользовательские список/форма/редактирование/отмена не реализованы в исследованном entrypoint. Mock lifecycle не покрывает ограничения active/completed, автоматическое течение состояний и пересечения. Интеграционная приёмка и deployment этим покрытием не подтверждены.

Обоснование: этот текст добавляет отсутствовавшее implementation evidence без повторного requirement audit и без нового U→P. Ранее известная публикация API остаётся прежним P.

### NEW — только новый evidence-gap внутри существующего MOS-923

Предложить parent добавить к очереди проверки реализации, **не создавать отдельную задачу или утверждённый план автоматически**:

- запрет изменения starts_at/timezone/targets после старта;
- запрет изменения и отмены completed, сохранность записи при отказе;
- завершение между открытием карточки и cancel;
- отражение изменения API-состояния с течением времени;
- согласованные серверные conflict-ответы при пересечениях.

Основание — конкретные пропуски `mocks/maintenance.mjs:65–84,89–123` относительно wiki §§2.8–2.9 и отсутствие соответствующих assertions в двух прочитанных maintenance-блоках тестов. Это не требование воспроизвести весь production scheduler в моках.

### QUESTION

До реализации требуется решение владельцев, уже обозначенное прежним review:

- какой источник определяет namespace: wiki `assistant-ops/v1` или опубликованный/current local contract `maintenance/v1`;
- как создаётся draft и переводится в scheduled;
- каков согласованный уровень точности локального lifecycle-мока;
- кто отвечает за решение этих контрактных вопросов.

Здесь не выбираются новые API, auth-политики, правила null/defaults или алгоритмы пересечений. Ответ для завершения данного read-only сопоставления не требовался.

## Исторические и deployment-ограничения

- Jira — сохранённый срез **16.10.2026**, не текущее состояние сервиса. `/limitations` фиксирует отсутствие custom fields и тел attachments. Отсутствие assignee в сохранённом объекте не означает отсутствия владельца.
- Wiki — историческая revision 4; прежняя публикация OpenAPI не превращается в новое подтверждение доступности.
- `docs/mpmm-auth-rollout.md:3–5,24–33` прямо фиксирует **подтверждение release gate пользователем 09.10.2026**, а не runtime-проверки агента. Этот gate не переоткрывается данным отчётом; его переносимость на изменённое deployment и новую maintenance-интеграцию не проверена.
- Локальные файлы идентифицированы хешами. Baseline HEAD из задания не перепроверялся git-командой.
- Тесты, сборка, typecheck/lint/API-check и browser/network проверки не запускались по запрету задания. Состояние индекса не проверялось. Никакой вывод о безопасности, корректности deployed backend или доставке MOS-923 из mock-кода не следует.
- Блокеров доступности обязательных локальных источников не возникло.