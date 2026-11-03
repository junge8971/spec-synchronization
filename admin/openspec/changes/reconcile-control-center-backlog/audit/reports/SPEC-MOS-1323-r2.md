# SPEC-MOS-1323-r2 — владельцы требований backend A/B

## Результат и границы

Новое тело **MOS-1323** позволяет выполнить предметный source→spec join. Найдены существующие владельцы клиентского контракта, интерфейса и локальных моков, но **они не являются владельцами подтверждённой реализации backend**. Хранение, миграции, серверная атомарность, централизованное управление справочниками, проверка доступа и backend-тесты остаются неподтверждёнными этой lane.

Только локальное чтение документов и вычисление SHA256. Проектные файлы, исторические отчёты и отметки задач не изменялись; тесты, браузер, сеть, Git и вложенные агенты не использовались.

Обозначения:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`.
- `J` = `A/sources/jira-optional-backend-details/r1/content.json#/items/1`.
- `W1…W8` = последовательные пункты «Что делаем» внутри `J/description`.
- `D1…D10` = последовательные пункты DoD внутри того же поля. Нумерация здесь однозначно задаёт локаторы пунктов строкового Jira-description.
- `E/R/X/M` = `openspec/specs/ab-testing-{editor,registry,export,module}/spec.md` соответственно.
- `K` = `openspec/specs/control-center-mock-server/spec.md`.
- `I` = `openspec/specs/control-center-api-integration/spec.md`.

### Provenance

`J/key=MOS-1323`, summary `[B] Реализовать раздел "A/B Эксперименты"`, status `Hold`, updated `2026-10-14T14:03:53.543+0800`. Получение пакета: `2026-10-20T14:35:05.335Z`.

Metadata фиксирует selected-field-extraction: комментарии, вложения и custom acceptance fields не собраны. `parent:null` — поле subtask-parent, не отрицание модульной принадлежности. MOS-1142 указан как зависимость в теле; его содержание в этой lane не открывалось.

Прочитаны `A/decisions.md`, раздел **D-091**, и полностью `A/reviews/R-D091-RECOVERY.md`. Новый пакет снимает только прежнюю предпосылку отсутствия description. `JOIN-MOS-1323.md` остаётся корректным историческим отчётом о старом пакете; failed runtime provenance не пересматривается. Изменение coverage и принятие нового join принадлежат интегратору, не этому отчёту.

## Карта main / active / archive

Полностью прочитаны четыре main A/B specs, main `K` и `I`; относящиеся proposal/design/tasks и delta-specs владельцев ниже. Предыдущие `JOIN-MOS-1323.md` и `DELTA-AB-TESTING-ROOT-DOC.md` использованы как карта поиска, не как замена чтению.

| Уровень / owner | Точные артефакты и назначение |
|---|---|
| Main | `E`: **Complete editor and initial values**, **Aggregate validation**, **Aggregate persistence and identity**, **Existing group tags follow saved status**, **Reference integrity**, **Persisted status commands**. Клиентское представление и сохранение конфигурационного агрегата. |
| Main | `R`: **Server-owned selection**, **Supported condition builder**, **Persistent saved filters**, **Typed group conditions survive saved filters and export**. Запросы серверного отбора, metadata и сохранённого search; не доказательство серверной реализации. |
| Main | `X`: **Full selection export**, **Flat saved detail export**, **Truthful file delivery**. Потребление CSV списка/карточки с выбранными полями. |
| Main | `M`: **Configuration is not execution**, **Shell routes and access**. Граница конфигурации и существующей UI/session policy. |
| Main | `K`: **A/B testing mock contract fidelity**, **Numeric conditions preserve typed semantics**. CRUD, soft delete, partial PUT, IDs/порядок, проверки и ошибки только локального Express. Бизнес-моки явно без credentials/role enforcement. |
| Main | `I`: **Current API is the authoritative contract snapshot**. Происхождение OpenAPI, согласованность документов/DTO и запрет считать опубликованный контракт проверенной интеграцией. |
| Archive: `2026-10-15-add-optional-ab-testing` | Прочитаны `proposal.md`, `design.md`, `tasks.md` и все шесть delta-specs: четыре A/B, `control-center-mock-server`, `code-quality-gates`. Proposal **Impact** использует существующий API; design **Goals / Non-Goals** прямо исключает backend migrations, execution engine и новую auth-модель. Tasks 2.1–2.4, 3.2–3.6, 4.1–4.4, 5.1–5.7, 6.1–6.3 — владельцы клиентской/mock-работы, не серверного DoD MOS-1323. |
| Archive: `2026-10-15-update-control-center-api-contracts` | Прочитаны proposal/design/tasks и относящиеся delta-specs `ab-testing-registry`, `control-center-api-integration`, `control-center-mock-server`. Design §§1, 4, 7; tasks 1.1–1.3 и 4.1–4.4 — обновление контрактов и typed `groups_count`. Здесь явно изменён прежний запрет числовых условий. |
| Archive: `2026-10-13-update-control-center-contracts-put` | Прочитаны proposal/design/tasks и относящаяся mock delta. Design §§2–4, tasks 1.2–1.3, 3.2 — исторический импорт managed API и временный mock 501. Это не актуальный запрет A/B CRUD: последующие A/B и contract changes заменяют соответствующее unavailable-покрытие. |
| Archive: `2026-10-16-fix-existing-scenarios-test-contour` | Прочитаны proposal/design/tasks. Proposal **Capabilities** прямо относит совместимость A/B metadata к существующим main specs; отдельной A/B delta нет. Tasks 1.3, 7.2 — локальные регрессии metadata, поиска и minimum-one поверхности; 6.5 и 7.4 сохраняют незавершённые проверки. Архивирование не означает завершения backend issue. |
| Active: `clarify-ab-testing-sample-size` | Полностью прочитаны proposal/design/tasks и `specs/ab-testing-editor/spec.md`. Единственная delta — доступное пояснение min_sample_size «в каждой группе», один nullable scalar без вычислений. Не владелец таблиц, миграций, серверного CRUD или исполнения эксперимента; в новом Jira-body это уточнение отдельно не сформулировано. |

Архивный `code-quality-gates` относится к размещению frontend/mock-кода, а не к backend acceptance. Чужие capability/specs этих широких changes не используются для покрытия MOS-1323.

## Атомарное сопоставление нового тела

В колонке «Наблюдение» указано **документальное соответствие**, не реализованность требования.

| Атом источника / требование | Наблюдение в owners | Неизвестное / безопасное решение |
|---|---|---|
| `J/W1`: CRUD на механизме MOS-1142 | `E` **Aggregate persistence and identity**; `K` **A/B testing mock contract fidelity**; archive add-optional tasks 2.1, 3.3 | Backend reuse MOS-1142 неизвестен. **keep** клиентских/mock owners; **question** о серверном владельце зависимости. |
| `J/W2`: таблица карточки | Archive add-optional design **Non-Goals** исключает backend migrations | Серверная таблица и её owner не установлены. **question**, не frontend gap. |
| `J/W2`: таблицы групп | `E` описывает API-facing groups, не DDL | Схема хранения групп неизвестна. **question**. |
| `J/W2`: связи с поверхностями | `E` **Reference integrity**, **Aggregate persistence and identity** описывает `surface_ids` | Серверные связи/FK неизвестны. **question**. |
| `J/D1`: модель соответствует согласованной модели; подготовлены миграции | В прочитанных владельцах нет backend-плана миграций; у основного архива это non-goal | Ни соответствие хранения, ни миграции не доказаны. **question** о принятой серверной модели/миграциях. |
| `J/W3`: настройка аудитории | `E` **Complete editor and initial values**, **Aggregate validation**: audience_code/segment | **keep**; backend сохранение и проверка не установлены. |
| `J/W3`: целевая метрика | `E` **Complete editor and initial values**: metric_code | **keep** как настройку, не сбор/расчёт метрик. |
| `J/W3`: режим запуска | То же requirement: launch_mode; `M` **Configuration is not execution** | **keep** без scheduler/engine. |
| `J/W3`: даты | `E` **Aggregate validation**, **Persisted status commands** | **keep**; не выводить таймеры и автоматическое назначение дат из body. |
| `J/W3`: статус | `E` **Complete editor and initial values**, **Persisted status commands** | **keep**; полная backend-машина переходов body не определена. |
| `J/W4`: подключение справочников к централизованному реестру | `K` требует четыре section-scoped lookup; archive add-optional tasks 3.2 | Lookup/mock seed не доказывают регистрацию backend-справочников. **question**. |
| `J/W4`: начальные значения справочников | Archive add-optional design §3 задаёт UI defaults; §8 — mock seed | UI defaults и seed не равны серверному initial-data migration. **question**, не переносить значения автоматически. |
| `J/W5`: API справочников | `E` **Reference integrity**; `K` сценарий **Metadata and lookup** | Клиент/mock owner найден; backend unknown. **keep**. |
| `J/W5`: metadata для привязки полей | `K` требует `data.experiments` и bindings; archive add-optional tasks 2.1, 3.2 | **keep**; фактическая server metadata относится к API/IMPL lanes. |
| `J/D7`: общий API и централизованное управление значениями в «Справочниках» | A/B editor потребляет lookup; archive add-optional design **Non-Goals** исключает редактор справочников | Централизованное управление значениями этим owner не покрывается. **question** о точном catalog/backend owner и допустимых изменениях; новый A/B редактор справочников не предлагать. |
| `J/W6`, `J/D2`: поиск | `R` **Server-owned selection**; archive add-optional task 3.4 | **keep**. Server execution неизвестен. |
| `J/W6`, `J/D2`: обычные фильтры | То же requirement, фильтры статусов/поверхностей | **keep**, не считать локальную пагинацию backend evidence. |
| `J/W6`: сложные условия | `R` **Supported condition builder**, **Unsupported conditions remain explicit**; archive contract-update tasks 4.1–4.4 | **keep** typed groups_count; body не разрешает автоматически priority/surface conditions или произвольную вложенность. |
| `J/W6`, `J/D8`: сохранение условий поиска | `R` **Persistent saved filters**, resource `ab-experiments`; `K` A/B fidelity | **keep** общий механизм. Серверная персистентность неизвестна. |
| `J/W7`, `J/D8`: CSV всего отбора с выбором полей | `X` **Full selection export**, `R` **Typed group conditions survive saved filters and export** | **keep**. Body не задаёт новый лимит или иной wire payload. |
| `J/W7`, `J/D8`: CSV отдельной карточки с выбором полей | `X` **Flat saved detail export** | **keep** плоский контракт. Вложенный экспорт из формулировки не следует. |
| `J/W8`, `J/D4`: распределение/сумма долей | `E` **Aggregate validation**; `K` A/B fidelity | **keep** соответствующие правила; фактический backend enforcement неизвестен. |
| `J/W8`, `J/D4`: аудитория и обязательные параметры | `E` **Aggregate validation**, сценарий **Cross-field validation** | **keep**; не изобретать дополнительные типы аудитории. |
| `J/W8`, `J/D4`: корректность дат | То же requirement: scheduled/started_on и ended_on | **keep**, серверное исполнение неизвестно. |
| `J/W8`: связи и уникальность | `E` **Aggregate validation**, **Reference integrity**; `K` A/B fidelity | **keep**. Backend constraint/index evidence отсутствует. |
| `J/W8`: понятные ошибки по полям | `E` **Aggregate validation**, сценарий **Server conflict**; `K` **Rejected aggregate preserves state** | **keep** mapping ошибок. Не утверждать точные backend status/envelope только на основании UI spec. |
| `J/D2`: создание, просмотр, изменение | `E` **Aggregate persistence and identity**; `K` A/B fidelity | **keep** existing owners; backend CRUD unknown. |
| `J/D2`: мягкое удаление | `K` явно требует soft DELETE; `E` **Persisted status commands** запрещает добавлять DELETE в UI | **Нет противоречия:** backend операция и отсутствие UI-кнопки — разные уровни. **keep**, не добавлять кнопку из backend body. |
| `J/D3`: атомарное сохранение карточки, групп и поверхностей | `K` **Rejected aggregate preserves state**; archive add-optional task 3.3; `E` работает с агрегатом | Отказ без частичной mock-мутации не доказывает DB transaction. **question** о backend-транзакции и её тестах. |
| `J/D3`: сохранение порядка групп | `E` **Aggregate persistence and identity**, сценарий **Reorder and rename**; `K` **Aggregate round trip** | **keep** API-array order; не переносить frontend отсутствие sort_order на устройство БД. |
| `J/D3`: сохранение ID существующих групп | Те же requirements/scenarios; archive add-optional tasks 2.3, 5.2 | **keep**. Серверное сохранение identity unknown. |
| `J/D4`: уникальность тегов | `E` **Aggregate validation**; `K` A/B fidelity | **keep**; отсутствие дублей в mock не удостоверяет backend constraint. |
| `J/D5`: запрет изменения тегов существующих групп вне «Черновика» | `E` **Existing group tags follow saved status**; `K` A/B fidelity; archive add-optional design §5 | Прямое семантическое соответствие. **keep** saved-status boundary, без правила «когда-либо запускался». Backend enforcement unknown. |
| `J/D6`: частичный PUT на верхнем уровне | `E` **Aggregate persistence and identity**; `K` A/B fidelity; archive add-optional design §5 | Прямое соответствие. **keep**, не трактовать PUT как полную замену карточки. |
| `J/D6`: переданные группы заменяются целиком | Те же requirements; archive task 2.3 | **keep** полный переданный массив с сохранением existing IDs. |
| `J/D6`: переданные поверхности заменяются целиком | Те же requirements: replacement `surface_ids` | **keep**. Пропущенная коллекция не означает очистку. |
| `J/D9`: общий managed-resources prefix | Archive add-optional proposal **Impact** указывает `/api/control/api/v1/managed-resources/ab-testing` | Client-contract owner найден; точный API join оставлен API lane. **keep**. |
| `J/D9`: общий формат ответов | Archive add-optional tasks 2.1, 3.3; `I` **Current API is the authoritative contract snapshot** | Contract/schema intent есть; backend соответствие неизвестно. **keep**. |
| `J/D9`: проверка доступа | `M` **Shell routes and access** сохраняет UI policy, тогда как `K` исключает role enforcement | **Не засчитывать UI visibility или mock 403 как backend authorization. question** о серверных проверках. |
| `J/D10`: OpenAPI | `I` snapshot requirement; archive contract-update tasks 1.1–1.3 | Документальный owner найден. Полноту операций/DTO проверяет отдельная API lane. |
| `J/D10`: тесты основных сценариев и ошибок | Archive add-optional tasks 2–6, contract-update §4 задают frontend/mock tests | Это не backend test suite. **question** о серверных тестах; текущая успешность любых тестов здесь не проверялась. |

## Выводы lane и безопасные предложения

**keep**

- Сохранить существующее владение `E/R/X/M`, mock fidelity и contract snapshot; новый body непосредственно согласуется с partial PUT, полным replacement коллекций, group IDs/order и запретом изменения existing tags вне draft.
- Сохранить configuration ≠ execution. Настройка аудитории, метрики, режима, дат и статуса не задаёт scheduler, bucketing engine, сбор статистики или автостоп.
- Сохранить отличие soft-delete backend API от отсутствия UI DELETE; не расширять интерфейс.
- Сохранить active sample-size delta самостоятельным bounded уточнением, не приписывать ей выполнение MOS-1323.

**update**

- Добавить новый evidence-join к точному backend member после независимого review; не переписывать старый missing-body отчёт.
- В новом join явно различать frontend owner, mock owner, contract owner и неподтверждённый backend owner.
- Использовать текущую цепочку typed groups_count: архив add-optional содержал запрет, но contract-update delta и main specs его адресно заменили. Исторические design/tasks не исправлять задним числом.

**new**

- Новая frontend capability или дублирующий module change **не обоснованы**.
- Серверный план по хранению/миграциям, централизованным справочникам, транзакциям, доступу и backend tests допустим только после установления существующего backend owner и отдельного согласования. Это предложение маршрутизации доказательств, не поручение реализовать backend в данном репозитории.

**question**

- Где находятся точные backend owner/DDL/migrations/test artifacts MOS-1323 и подтверждение использования MOS-1142?
- Какой согласованный серверный документ определяет модель и начальные значения A/B-справочников, а также границы их централизованного управления?
- Какие серверные свидетельства подтверждают транзакционность, неизменность existing group IDs/tags и authorization?
- Есть ли дополнительные acceptance в невыгруженных comments/attachments/custom fields?

Ни один найденный документальный join не закрывает backend DoD или deployment. Точный backend owner в исследованном наборе **не установлен**, что не означает его отсутствия во внешнем проекте.

## SHA256 входов

Хэши вычислены локально по байтам `sha256sum`.

| Вход | SHA256 |
|---|---|
| `A/sources/jira-optional-backend-details/r1/content.json` | `3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618` |
| `A/sources/jira-optional-backend-details/r1/metadata.json` | `9357e481e237e04c47258fe4efb4bcc3d8377e2690e75963653d2275885ff4fc` |
| `A/decisions.md` | `fa7cffedb00f4d481efa2b523e8f1a1b4991b2750022c823c30c5370ab5cf945` |
| `A/reviews/R-D091-RECOVERY.md` | `f6fb801733ee223979debb0277de15e8f97448a3a69db6a2fb0f42f35c03e45d` |
| `A/reports/JOIN-MOS-1323.md` | `86a89f81d8b8baa87b6566f85abe71e68b0eebb22d1916229db7339de4ef653b` |
| `M` | `0013ea05d4c913d321baae18dca1076029792bf58ffc06e6a1715d53eca60366` |
| `R` | `f23569188a872ab976bbe1ae8be032a667c854ed4a544404f068e1d6e4a59bd5` |
| `E` | `7cffebc09d33477bc300ec9c76f2989c9e095846e2a90fc74747b3393c2d13e9` |
| `X` | `d672a8a81e8847e28f91910e2b34510ff320ebf7a3a81df219923195ec5801ca` |
| `K` | `54cd451a911c13129fbf8be64b06f920a837d4c816255f6ee6f5ee65f4406588` |
| `I` | `697c9c5fcb5e55e361662f93785ce5c2eb55ea8efd4992d18825c36b0107db09` |

Пути следующих таблиц относительно `openspec/changes/`.

| Owner / артефакт | SHA256 |
|---|---|
| `archive/2026-10-15-add-optional-ab-testing/proposal.md` | `93d219f6c749cda697f3b1dcc231e3d4dbf2ea71b99267f7d610b19ba390edfd` |
| `archive/2026-10-15-add-optional-ab-testing/design.md` | `fba208c2d27c670ff0e981d5fa17d2121df16ff67ca66d8df0adf255fff2cee6` |
| `archive/2026-10-15-add-optional-ab-testing/tasks.md` | `e005921905e56e00cead68fd3c58d7ae30b9ffb79d6313de3162734ec30f1073` |
| `archive/2026-10-15-update-control-center-api-contracts/proposal.md` | `6ece6e82490038d5ce491f19acf089c10a27dc845f74c2cf035ac37826c13bd8` |
| `archive/2026-10-15-update-control-center-api-contracts/design.md` | `58f8cdbd387508c10285387b3fcdbf208bfdb73559a8243997af676e38df6156` |
| `archive/2026-10-15-update-control-center-api-contracts/tasks.md` | `6002750f35319a52ce0c9fcd50731385ada811844c6edc3499943d87051dd478` |
| `clarify-ab-testing-sample-size/proposal.md` | `954782185e03b5e6395f149c295a539a3157262d3ff2cebd8bb8441760945ec1` |
| `clarify-ab-testing-sample-size/design.md` | `7cfeb9eb60671afa465c6a29024c35b259f3595d6654aaa191e1e6da86a6e360` |
| `clarify-ab-testing-sample-size/tasks.md` | `cbf39a5ca1a4a2067cae448e9b68d762e342484377a8bdeb5146894a80a9ed27` |
| `clarify-ab-testing-sample-size/specs/ab-testing-editor/spec.md` | `b1741fd5bde9283f4cdccf85078f8f09e0b4d223c145b5b217fac0980e2508fe` |

## Проверки и остаточные риски

Выполнены read/find/grep, `wc -l` и `sha256sum`; совпадение SHA нового source с metadata подтверждено. Main mock spec дочитан после ограничения вывода. Тесты, сборки и валидация OpenSpec намеренно не запускались по контракту задачи. Git/staging не проверялся.

Остаются неизвестными backend implementation, миграции, фактические права, транзакции, backend tests, deployment и дополнительные несобранные acceptance. Архивные результаты прогонов не перепроверялись и не переносятся на текущий backend issue.