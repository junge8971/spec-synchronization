## Context

См. proposal.md: задача [MOS-1249](https://task.mos-team.ru/browse/MOS-1249). Выделена из общего анализа MOS-1246 без расширения согласованного поведения. Исходный анализ: 12.10.2026; feedback implementation отсутствует, используются существующие механизмы проекта.

### Sources and precedence

1. Пользователь согласовал первый этап: UI по прототипу, операции по API, неподдержанное отложить; затем разрешил создание отдельных changes по 10 FE-задачам.
2. Wire DTO/пути — `docs/api/contracts/managed-resources.openapi.json`; бизнес-семантика операций — `docs/api/contracts/crud-api.md`, разделы 1–17 и ограничения справочников в 18. Эти документы не подтверждают доступность deployment.
3. UI — `/home/user/Загрузки/ПротоОбратнаяСвязь.html`; аналитика — `/home/user/Загрузки/247734813_929050b18a6d4376b451473b7c9acd47-121026-2022-1378.pdf`. Онлайн-источник аналитики: https://wiki.mos-team.ru/spaces/KR/pages/247734813 .
4. HTML содержит локальные DATA/RESPONSIBLE_USERS, изменение draft и демонстрационный doExport без скачивания. Это ориентир композиции и сценариев, не production-код и не API-контракт.

SHA-256 входных файлов для воспроизводимости:

| Файл                    | SHA-256                                                            |
| ----------------------- | ------------------------------------------------------------------ |
| crud-api (2).md         | `ac3e2a999828c47310f957f07c4b7596b199cc532fe0cef2610e1a324e45ac27` |
| newcontract.json        | `f28289e0ddddd3c9cf05dcb232cc94a7894d7ffb620fa1d58d2c6f597e6e20f7` |
| ПротоОбратнаяСвязь.html | `8f3c162fd20dfd0bfe84f95175eaefdbe3ec613865850afc4f1373ad773ac80f` |
| PDF аналитика           | `97ee2ee177ca9596e7dfad844d3cb5fe9036b6625e6cb41233a2d4b4ff956e96` |

Контракт обновлён change `update-control-center-contracts-put`: общий OpenAPI содержит 111 операций и 351 схему, managed-resources.openapi.json — 43 операции. Источники и их provenance сохранены в docs/api/contracts; hashes таблицы относятся к входным файлам до форматирования. Не импортировать повторно старый managed-resource.openapi.json и не заменять экспортное дополнение диалогов. `scripts/generate-api-types.mjs` читает общий контракт.

В MOS-1249 использовать опубликованные PUT-операции. Реализуемые здесь feedback CRUD/search/lookup/metadata handlers заменить в явном unavailable-перечне моков; остальные managed-resource операции оставить недоступными до их отдельных задач. Это обновление источника не отмечает клиентскую или mock-реализацию MOS-1249 выполненной.

## Goals / Non-Goals

**Goals:** отдельная реализация и проверка области MOS-1249; общие интерфейсы с зависимостями сохраняются.

**Non-Goals:** реализация соседних задач, новая auth-модель и расширение backend. UI реестра/карточки и самостоятельные клиенты saved-filters/CSV принадлежат соседним задачам; общий CRUD справочников и база знаний не подключаются.

## Decisions

### Dependencies and ownership

Существующие HTTP/session механизмы проекта; переданные API-контракты.

`entities/feedback` владеет API, runtime-проверками DTO, ключами запросов, предметными типами и нормализованным отбором. Pages/widgets компонуют реестр и редактор; связанные приватные редакторы вопросов, правил, меток и preview остаются у владельца draft. Независимые features отбора, сохранённых фильтров и экспорта обращаются к публичному API entity, не импортируют друг друга. FSD-направление и index.ts обязательны; именованные types/constants/handlers размещаются по правилам проекта. Не переносить весь HTML, ручной router, DOM innerHTML или самодельную таблицу состояния.

Использовать существующие React Router, TanStack Query/Table, React Hook Form, Zod и UI kit. Для порядка вопросов/вариантов обязательны доступные кнопки перемещения; drag-and-drop использует возможности платформы, пока новая библиотека не обоснована. Универсальный движок managed resources не нужен: доступен один предметный раздел.

### Implementation decisions

API prefix `/api/control/api/v1/managed-resources`; относительно существующего Control API base `/api/control/api` клиенты используют `/v1/managed-resources`. Не добавлять UI basename, не создавать новый fetch/auth path. Переиспользовать `apiRequest`, `apiBinaryRequest`, session owner/generation checks и `readResponseFilename`.

| Операция                         | Путь относительно managed-resources                                                    |
| -------------------------------- | -------------------------------------------------------------------------------------- |
| Создать; поиск                   | `POST /feedback/surveys`; `POST /feedback/surveys/search`                              |
| Читать; изменить; удалить        | `GET/PUT/DELETE /feedback/surveys/{entity_id}`                                         |
| Справочные значения; метаданные  | `GET /catalogs/lookups/feedback`; `GET /feedback/metadata`                             |
| Экспорт отбора; карточки         | `POST /feedback/surveys/export`; `POST /feedback/surveys/{entity_id}/export`           |
| Создать; список фильтров         | `POST /saved-filters`; `GET /saved-filters?resource=feedback-surveys&limit=…&offset=…` |
| Читать; изменить; удалить фильтр | `GET/PUT/DELETE /saved-filters/{filter_id}`                                            |

Успех POST создания — 201 и `data.id`, после него GET; PUT — 200 с полной карточкой. JSON-envelope сохраняет `code/message/errors`; ошибки полей используют JSON Pointer, включая `/questions/0/options/0/text` и `/search/conditions/items/0/value`. Валидация ответа, 400/401/403/404/409/422/5xx, отмена чтения и stale responses остаются различимыми. Не повторять автоматически мутации; сервер не публикует optimistic locking/idempotency этого ресурса. При неизвестном исходе — явное перечитывание перед дальнейшим решением, без автоматического повторного создания.

Новая feature policy использует уже опубликованные бизнес-права `TSAM.ManagedResource:read/create/update/delete/export`, не вводит новые права или auth-модель. Реестр, detail, lookup, metadata и список своих фильтров — read; создание опросника/фильтра — create; сохранение, статус, обновление фильтра — update; удаление опросника/фильтра — delete; оба CSV — export. Действия требуют также read содержащего экрана. Сопоставление action/resource/`*`, скрытие недоступных действий, отказ прямого URL и изоляция owner/generation — существующие.

Выбор поверхностей требует существующего `TSAM.Surface:view`. Без него не загружать список; сохранённые UUID показывать без вымышленных названий и сохранять. Уже полученная карточка не должна становиться недоступной из-за необязательной загрузки поверхностей. Backend проверяет глобальную область и владельца фильтра; frontend не вычисляет объединённый scope и не добавляет permission ACL в transport/handlers. Server 403 остаётся окончательным.

### Existing safety and verification

Существующие HTTP transport, MPMM-сессия, owner/generation и UI-only permissions сохраняются. Backend проверяет scope. FSD и публичные index.ts обязательны; новые auth-модель, role editor и request ACL не вводятся. Unit/component и mock HTTP проверки разрешены; browser/E2E — только по отдельному разрешению. Dev-моки остаются в Express без credentials/role enforcement; production их не содержит.

Общая политика feature permissions определена [API change](../mos-1249-feedback-api/specs/feedback-api/spec.md); доступность UI проверяется в спецификации и tasks владельца соответствующего интерфейса. Соседние feature-модули не импортируют друг друга: данные проходят через владельца draft либо публичную entity.

## Risks / Trade-offs

- [HTML шире API] → ограничить UI опубликованными возможностями; ограничения Deferred scope из proposal сохраняются в приёмке.
- [Нет optimistic locking] → не обещать защиту от чужой параллельной записи; сохранять baseline и пояснять неизвестный исход, не делать слепой повтор.
- [Неизвестные/неактивные справочные коды] → сохранить исходные данные, не подставлять defaults поверх сохранённого значения; новые неподдержанные renderers не выдумывать.
- [Ошибки OpenAPI допускают null шире бизнес-правил; autogenerated 422 описан иначе envelope] → generated DTO дополняются runtime-проверками и документированными бизнес-ограничениями; не переписывать исходник без provenance, фактический ответ проверить на интеграции.
- [Раздел 10.2 CRUD говорит о правах экспорта как чтения, раздел 1 публикует отдельный export] → UI использует явную матрицу с export; серверную достаточность прав подтвердить перед релизом, не ослаблять политику по неоднозначной фразе.
- [Inputs находятся в Downloads] → в apply перенести точные источники в docs с хешами до контрактных изменений; обновление источников требует повторной сверки.

## Migration Plan

Реализовать только tasks этой подзадачи после указанных prerequisites. Моки не подтверждают доступность реального API. Перед выпуском проверить операции этой задачи на стенде; rollback — предыдущий frontend bundle без удаления серверных данных. Backend schema migration не входит.

## Open Questions

Блокирующих продуктовых решений в согласованном первом этапе нет. Перед выпуском остаётся подтверждение фактических endpoint/errors/permissions/CORS для операций задачи. Иное поведение требует уточнения контракта, не скрытого расширения scope.
