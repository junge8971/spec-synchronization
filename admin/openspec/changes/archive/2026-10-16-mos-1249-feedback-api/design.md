## Context

См. proposal.md: задача [MOS-1249](https://task.mos-team.ru/browse/MOS-1249). Реализуется API-фундамент обособленного раздела по примеру `app/optional/knowledge-base`, без расширения бизнес-scope.

### Sources and precedence

1. Пользователь согласовал первый этап: UI по прототипу, операции по API, неподдержанное отложить; затем разрешил создание отдельных changes по 10 FE-задачам.
2. Wire DTO/пути — `docs/api/contracts/managed-resources.openapi.json`; бизнес-семантика операций — `docs/api/contracts/crud-api.md`, разделы 1–17 и ограничения справочников в 18. Эти документы не подтверждают доступность deployment.
3. UI — `/Users/lisa-codesrc/Downloads/ПротоОбратнаяСвязь.html`; аналитика — предоставленная пользователем выгрузка `/Users/lisa-codesrc/Downloads/247734813_87fa5d741e1a4c5daba003796da65f8d-151026-1846-1994.pdf`. Это внешние исходные материалы: в репозиторий не копируются и в поставку не входят. SHA-256 записаны ниже. Онлайн-источник аналитики: https://wiki.mos-team.ru/spaces/KR/pages/247734813 .
4. HTML содержит локальные DATA/RESPONSIBLE_USERS, изменение draft и демонстрационный doExport без скачивания. Это ориентир композиции и сценариев, не production-код и не API-контракт.

SHA-256 входных файлов для воспроизводимости; исторические байты API-выгрузок и старого PDF отдельно не подменяются новыми файлами:

| Файл                                               | SHA-256                                                            |
| -------------------------------------------------- | ------------------------------------------------------------------ |
| crud-api (2).md                                    | `ac3e2a999828c47310f957f07c4b7596b199cc532fe0cef2610e1a324e45ac27` |
| newcontract.json                                   | `f28289e0ddddd3c9cf05dcb232cc94a7894d7ffb620fa1d58d2c6f597e6e20f7` |
| ПротоОбратнаяСвязь.html                            | `8f3c162fd20dfd0bfe84f95175eaefdbe3ec613865850afc4f1373ad773ac80f` |
| PDF аналитика, предоставленная выгрузка 15.10.2026 | `1371ed94fa92d2521287fe23eddd15b18b269811e6c6982c468a04d2282cee7c` |

Историческая выгрузка PDF `247734813_929050b18a6d4376b451473b7c9acd47-121026-2022-1378.pdf` имела hash `97ee2ee177ca9596e7dfad844d3cb5fe9036b6625e6cb41233a2d4b4ff956e96`; её точные байты не предоставлены. Текущий PDF записан как отдельный источник, без заявления о побайтовом совпадении со старым. HTML совпал с ранее записанным hash. Оба доступных оригинала проверены в Downloads через SHA-256; по просьбе пользователя копии из документации удалены.

Актуальный локальный aggregate содержит 112 операций и 353 схемы, managed-resources.openapi.json — 43 операции. API-источники и их provenance сохранены в docs/api/contracts; hashes API-выгрузок в таблице относятся к историческим входным файлам до форматирования. Не импортировать повторно старый managed-resource.openapi.json и не заменять экспортное дополнение диалогов. `scripts/generate-api-types.mjs` читает общий контракт. HTML и предоставленный PDF доступны по указанным выше внешним путям в Downloads.

В MOS-1249 использовать опубликованные PUT-операции. В фактическом Express уже существуют generic managed-resource handlers, включая feedback и CSV; явный unavailable-перечень отсутствует. Добавить специализацию feedback CRUD/search/lookup/metadata по примеру knowledge-base, сохранив существующее поведение соседних операций. Не добавлять вымышленный unavailable-перечень или новую реализацию CSV/saved-filters.

## Goals / Non-Goals

**Goals:** CRUD опросников, search, lookup, metadata, runtime-валидация и Express-моки; адресная проверяемая граница модуля.

**Non-Goals:** UI, клиенты saved-filters (MOS-1259), CSV (MOS-1260), другие managed-resource разделы, новая UI-policy и mappings permissions, auth/session/RBAC и новые ограничения интерфейса по пользователю.

## Decisions

### Dependencies and ownership

Существующие HTTP/session механизмы проекта; переданные API-контракты.

Владелец всего раздела — `app/optional/feedback`: API, runtime-схемы, модель, типы, константы, тесты и будущий UI остаются внутри. Выбран существующий подход базы знаний вместо разнесения feedback по entities/features/widgets/pages: это позволяет подключить и удалить весь раздел без зависимостей между optional-модулями. Связанные приватные редакторы вопросов, правил, меток и preview остаются у владельца draft.

Адресная граница в `scripts/eslint-fsd-config.mjs` разрешает feedback импортировать `shared` и публичные `index.ts` entities (включая существующий session API). Запрещены зависимости от application/providers/routes/root, pages, widgets, features и других optional-модулей, а также private entity imports. Слои shared/entities/features/widgets/pages не импортируют optional. Application импортирует feedback только через публичный `index.ts`; внутренний код использует прямые импорты. Правила действуют для alias/relative/type-only/re-export, без отключения проверок и широких исключений. Основное FSD-направление сохраняется; optional — адресный обособленный модуль композиции приложения по примеру базы знаний. Именованные declarations размещаются в `types/*.types.ts`, предметные константы — в `constants/*.constants.ts`.

Публичный API MOS-1249 экспортирует клиенты CRUD/search/lookup/metadata, предметные DTO, query/mutation hooks и нормализацию search. Приватные схемы и helpers остаются внутри. В MOS-1249 routes/tabs не добавляются. В будущем application получает descriptors через `index.ts` в `app/application/constants/application-routes.constants.ts`; `app/routes.ts` регистрирует framework route entrypoints строками, как у базы знаний. Descriptor не импортирует runtime UI. Shared navigation не импортирует optional. Интеграционная документация описывает текущее подключение и удаление: убрать application imports/route registrations (когда появятся), mock registration, test glob, адресные boundary rules/tests, затем каталоги. Общие transport/session и опубликованные контракты сохраняются.

Использовать существующие React Router, TanStack Query/Table, React Hook Form, Zod и UI kit. Для порядка вопросов/вариантов обязательны доступные кнопки перемещения; drag-and-drop использует возможности платформы, пока новая библиотека не обоснована. Универсальный движок managed resources не нужен: доступен один предметный раздел.

### Implementation decisions

API prefix `/api/control/api/v1/managed-resources`; относительно существующего Control API base `/api/control/api` клиенты используют `/v1/managed-resources`. Не добавлять UI basename или новый fetch/auth path. Переиспользовать `apiRequest`, `ApiError`, session owner/generation checks и TanStack Query; binary transport/filename helpers потребуются соседней задаче CSV.

| Операция                         | Путь относительно managed-resources                                                    |
| -------------------------------- | -------------------------------------------------------------------------------------- |
| Создать; поиск                   | `POST /feedback/surveys`; `POST /feedback/surveys/search`                              |
| Читать; изменить; удалить        | `GET/PUT/DELETE /feedback/surveys/{entity_id}`                                         |
| Справочные значения; метаданные  | `GET /catalogs/lookups/feedback`; `GET /feedback/metadata`                             |
| Экспорт отбора; карточки         | `POST /feedback/surveys/export`; `POST /feedback/surveys/{entity_id}/export`           |
| Создать; список фильтров         | `POST /saved-filters`; `GET /saved-filters?resource=feedback-surveys&limit=…&offset=…` |
| Читать; изменить; удалить фильтр | `GET/PUT/DELETE /saved-filters/{filter_id}`                                            |

Успех POST создания — 201 и `data.id`, после него GET; PUT — 200 с полной карточкой. JSON-envelope сохраняет `code/message/errors`; ошибки полей используют JSON Pointer, включая `/questions/0/options/0/text` и `/search/conditions/items/0/value`. Валидация ответа, 400/401/403/404/409/422/5xx, отмена чтения и stale responses остаются различимыми. Не повторять автоматически мутации; сервер не публикует optimistic locking/idempotency этого ресурса. При неизвестном исходе — явное перечитывание перед дальнейшим решением, без автоматического повторного создания.

Новая UI-policy, mappings permissions и пользовательские ограничения не добавляются. Backend проверяет глобальную область и владельца фильтра; frontend не вычисляет объединённый scope и не добавляет ACL в transport/handlers. Server 403 сохраняется как ошибка общего transport.

Zod проверяет payload/ответы, UUID, размеры, null semantics, search/conditions и вложенные поля. Обязательные итоговые поля не принимают null несмотря на permissive generated Patch; nullable бизнес-поля сохраняют явный null. Переданные questions и display_rules заменяются целиком, omission сохраняет значение. Чтение не заменяет неизвестные справочные коды default. Системные поля, sort_order, FK и локальные ключи не отправляются. После POST модель сохраняет подтверждённый ID: ошибка последующего GET допускает явное повторное чтение без нового POST. PUT/DELETE проверяют ID подтверждения; cache обновляется только после существующих owner/generation checks.

### Existing safety and verification

Существующие HTTP transport, MPMM-сессия, owner/generation и UI-only permissions сохраняются. Backend проверяет scope. FSD и публичные index.ts обязательны; новые auth-модель, role editor и request ACL не вводятся. Unit/component и mock HTTP проверки разрешены; browser/E2E — только по отдельному разрешению. Dev-моки остаются в Express без credentials/role enforcement; production их не содержит.

Express-модуль `mocks/feedback` использует существующие contract validation, search/pagination и fixed-error/session-demo механизмы. Unit/mock HTTP и ESLint boundary тесты проверяют существенные и граничные сценарии. Browser/E2E не создавать, не менять и не запускать.

Для полного test gate исправляются две существующие KB component-проверки: Select ожидает фактического появления listbox после асинхронного открытия Base UI, а сценарий создания отдельно проверяет два GET мутации и штатный GET нового detail-маршрута. Точные assertions сохраняют отсутствие повторного POST; production freshness/retry и thresholds не меняются.

CRUD раздел 11 явно требует `quiet_from`/`quiet_to` без часового пояса (`22:00:00`), тогда как Ajv `format: time` в формальном OpenAPI требует зону. Runtime и адресный mock-адаптер feedback следуют явной бизнес-семантике: проверяют локальное время без зоны, не меняют published JSON, общие time formats и validation соседних разделов. Предоставленный пользователем прогон на контуре Т подтвердил сохранение времени без зоны и замену правил целиком; формальный OpenAPI при этом не меняется.

### Real-environment evidence and accepted known issues — 2026-10-15

Пользователь предоставил результат ручного HTTP-прогона на контуре Т: run `mos1249_1792078927540_77d6ebe5`, с `2026-10-15T15:42:07.540Z` по `2026-10-15T15:43:14.062Z`. Выполнено 117 запросов; исходный итог сохранён без переклассификации в успех: 28 PASS, 7 FAIL, 1 SKIP, 2 OWNER. Источник — внешнее вложение `/Users/lisa-codesrc/.codex/attachments/4b7a1001-c0ec-440c-a036-ea8cd4db3a84/Вставленный текст.txt`, SHA-256 `b9c25f2c7782f5c5de9201dee95214e4ceb25680130bf196102623f0c0ecd44e`. Сам отчёт не копируется в репозиторий; токены и пользовательские данные не сохраняются.

Подтверждены CRUD, partial PUT, nullable-поля, вложенные ID/порядок/замена, нормализация меток, тихие часы без timezone, search/filters/conditions/pagination, metadata, восемь lookup, конфликты 409 и большинство проверок 422. Анонимный GET получил 401. Browser fetch с существующей сессией подтвердил доступность использованных операций и CORS в этом прогоне. Оба тестовых опросника удалены, GET вернул 404, `remaining=[]`, `unconfirmedCreateCodes=[]`. Мягкое удаление сохраняет занятые коды и созданные тестовые метки по контракту.

Известная проблема стенда: запросы №43 и №70 — GET `/feedback/surveys/c6f53e12-f3e0-41de-a6e1-2b7d7e240f4b` — вернули HTTP 503, `code=FAILED`. Они выполнялись после PUT с меткой длиной 151 символ и с `display_rules.max_per_day=0`. Оба PUT вернули ожидаемые 422 с `/tags` и `/display_rules/max_per_day`, но последующее чтение не подтвердило атомарность этих двух сценариев. Причина и устранение 503 не установлены; исходников backend в этой поставке нет. Дальнейшая диагностика по логам стенда и точечная повторная проверка относятся к владельцу стенда, автоматический replay мутаций не добавляется.

Ещё пять FAIL вызваны строгими Console assertions, а не подтверждённым нарушением бизнес-валидации. Во всех пяти случаях получен 422; для четырёх PUT проверена неизменность карточки, для query — отклонение запроса поиска:

| Сценарий                           | Ожидание скрипта            | Фактический `field` |
| ---------------------------------- | --------------------------- | ------------------- |
| `tags` без вариантов               | `/questions/0/options`      | `/questions/0`      |
| Тихие часы без времени             | `/display_rules/quiet_from` | `/display_rules`    |
| Аудитория surface без поверхностей | `/surface_ids`              | `/`                 |
| Аудитория segment без сегментов    | `/segments`                 | `/`                 |
| `query` длиной 1                   | `/query`                    | `/`                 |

CRUD разделы 12.1 и 16 не гарантируют эти точные leaf-пути для cross-field 422; они допускают ошибки объекта/формы. `/` зафиксирован как наблюдаемое серверное обозначение общей ошибки, а не корректный корень RFC JSON Pointer (корень — пустая строка). Клиент сохраняет исходные ошибки и не придумывает более точное поле. Для 409 ссылок/уникальности требования точных путей остаются; проверки прошли. Тесты реализации и runtime-проверки не ослабляются ради результата ручного скрипта.

Не подтверждены на стенде: 409 для неактивного `feedback_type` (в lookup нет такого fixture), 403 для действующей учётки с read без глобальной области, штатное обновление MPMM-сессии (ручной fetch его не запускает). Локальные тесты не подменяют эти evidence. По явному решению пользователя «Зафиксируй это в спеках как известную проблему и закрывай задачу» они приняты как известные ограничения закрытия MOS-1249; успешными не считаются. Исправление 503 и оставшиеся стендовые подтверждения не заявляются выполненными и не расширяют эту FE-поставку новыми auth/API/UI работами.

## Risks / Trade-offs

- [HTML шире API] → ограничить UI опубликованными возможностями; ограничения Deferred scope из proposal сохраняются в приёмке.
- [Нет optimistic locking] → не обещать защиту от чужой параллельной записи; сохранять baseline и пояснять неизвестный исход, не делать слепой повтор.
- [Неизвестные/неактивные справочные коды] → сохранить исходные данные, не подставлять defaults поверх сохранённого значения; новые неподдержанные renderers не выдумывать.
- [Ошибки OpenAPI допускают null шире бизнес-правил; autogenerated 422 описан иначе envelope] → generated DTO дополняются runtime-проверками и документированными бизнес-ограничениями; не переписывать исходник без provenance, фактический ответ проверить на интеграции.
- [Прототип и аналитика шире опубликованного API] → внешние источники используются для UI и предметного контекста; исходные DTO/операции MOS-1249 определяются локальным OpenAPI и CRUD-документом. Новая выгрузка PDF не подтверждает доступность backend.

## Migration Plan

Реализованы только tasks этой подзадачи после указанных prerequisites. Моки не подтверждают доступность реального API. HTTP-прогон на контуре Т и принятое пользователем закрытие с известной проблемой/ограничениями зафиксированы выше; это не подтверждение полного прохождения стенда. Rollback — предыдущий frontend bundle без удаления серверных данных. Backend schema migration не входит.

## Open Questions

Блокирующих продуктовых решений в согласованном первом этапе нет. MOS-1249 закрыта по решению пользователя с указанными известной проблемой и ограничениями; открытых задач реализации в этом change нет. Причина GET 503 и отсутствующие стендовые подтверждения остаются явно непроверенными. Новые расхождения API требуют уточнения контракта, не скрытого расширения scope.
