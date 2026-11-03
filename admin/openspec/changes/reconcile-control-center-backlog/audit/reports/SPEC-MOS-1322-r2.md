# SPEC-MOS-1322-r2 — владельцы требований backend «База знаний»

## Результат и границы

Новый body позволяет выполнить **точный частичный requirement-to-spec join MOS-1322**. Найдены владельцы клиентских контрактов, UI и локальных моков, но **не установлен владелец полной backend-поставки**: таблиц/миграций, транзакционности, централизованного управления справочниками и серверной проверки доступа.

Это не отсутствие backend-реализации и не подтверждение её готовности. Статус Jira `Hold`, архивные задачи и спецификации frontend не доказывают выполнение MOS-1322.

Проверка ограничена SPEC-lane. Полностью прочитаны относящиеся proposal/design/tasks и KB/общие delta-specs указанных ниже владельцев, текущие main-specs. Код, OpenAPI и тестовая реализация повторно не аудировались. Запусков тестов, сети, браузера, Git-операций и записи файлов не было.

Обозначения:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`.
- `M` = `openspec/specs`.
- `K` = `openspec/changes/archive/2026-10-14-add-optional-knowledge-base`.
- `C` = `openspec/changes/archive/2026-10-15-update-control-center-api-contracts`.
- `F` = `openspec/changes/fix-knowledge-base-export-limit-feedback`.
- В таблице `Wn` — n-й пункт «Что делаем», `Dn` — n-й пункт DoD внутри `A/sources/jira-optional-backend-details/r1/content.json#/items/0/description`; нумерация с единицы. Это локаторы внутри сохранённой строки, не дополнительные JSON-поля.

## Источник и историческая граница

Точный источник: `content.json#/items/0`, ключ `MOS-1322`, summary `[B] Реализовать раздел "База знаний"`, updated `2026-10-14T14:03:51.688+0800`. Получен `2026-10-20T14:35:05.335Z`.

`metadata.json#/limitations` фиксирует отсутствие comments, attachments и custom acceptance fields. `parent:null` не опровергает модульную принадлежность. MOS-1142 указан зависимостью непосредственно в W1; его тело этим пакетом не собрано и в этой lane не открывалось.

Прочитаны:

- `A/decisions.md`, раздел D-091: новый пакет снимает только прежнюю предпосылку отсутствия body; исторические отчёты и failed provenance сохраняются.
- `A/reviews/R-D091-RECOVERY.md`, строка JOIN-MOS-1322 и поправка 7: прежний U был обусловлен именно старым пакетом; coverage нельзя повышать по одному модульному покрытию.
- `A/reports/JOIN-MOS-1322.md`: использован как карта владельцев, не как замена чтению артефактов.

Новый результат допустимо интегрировать отдельно как ограниченный SPEC-join после пакетного review. Он сам не меняет U/P, ledger или исторические статусы.

## Атомарное сопоставление

| Требование MOS-1322 | Наблюдаемый owner и точный локатор | Граница / unknown |
|---|---|---|
| W1: CRUD на общем механизме MOS-1142 | `K/proposal.md#What Changes`: подключение существующих managed-resource CRUD; `K/design.md`, решения 5–6; `K/tasks.md`, 2.1–2.4. Main: `knowledge-base-editor/spec.md`, **Persisted aggregate semantics** | Владение клиентским использованием, не реализацией общего backend-механизма. Точный owner MOS-1142 неизвестен |
| W2: таблица карточки | `K/proposal.md#Impact` прямо исключает backend-миграции; `K/design.md#Goals / Non-Goals` исключает backend-расширения | Backend owner таблицы не установлен |
| W2: таблица вложенных ссылок | Main editor, **Link editing and safe preview**, **Persisted aggregate semantics**; `K/tasks.md`, 2.2, 7.1–7.2 | Форма/payload не определяют физическую таблицу |
| W2: таблица связей с навыками | Main editor, **External skills and responsible user**; `K/tasks.md`, 7.4 | UI-связи по ID не доказывают модель хранения |
| D1: соответствие согласованной модели | Main editor описывает поля/коллекции; `K/design.md`, решения 4–6 | Согласованная именно backend-модель из body не приложена; соответствие неизвестно |
| D1: подготовленные миграции | `K/proposal.md#Impact`; `C/proposal.md#Impact`, `C/design.md#Goals / Non-Goals` исключают backend-миграции | Прямого владельца миграций среди прочитанных артефактов нет |
| W3: регистрация справочников централизованно | `K/design.md`, решения 5 и 8; `K/tasks.md`, 3.2; main mock, **Knowledge base mock contract fidelity** | Есть section-scoped lookup и bindings для локального контура; это не backend-регистрация центрального реестра |
| W3: начальные значения справочников | `K/design.md`, решения 4 и 8; `K/tasks.md`, 3.1–3.2 | Defaults UI и fixtures не доказывают начальное заполнение backend |
| W4: API справочников | Main mock, **Knowledge base mock contract fidelity / Metadata and lookup ready for editor**; `K/tasks.md`, 2.1, 3.2 | Прямой локальный контрактный owner; доступность настоящего backend неизвестна |
| W4: API метаданных привязки полей | Те же locators; `K/design.md`, решение 5: `data.entries`, `catalog_bindings`, `condition_fields`, `export_fields` | Клиентское потребление и mock-ответ, не доказательство backend |
| W5: поиск | Main registry, **Server-owned registry selection**; `K/tasks.md`, 4.1–4.2 | Специфицирована интеграция с серверным поиском |
| W5: обычные фильтры | То же requirement: категории/статусы и серверный отбор | Backend исполнение не установлено |
| W5: сложные условия | Main registry, **Metadata-driven supported conditions**; `C/specs/knowledge-base-registry/spec.md`, одноимённое requirement; `C/tasks.md`, 4.1–4.4 | Текущий owner включает `links_count` и `skill_names`; старое ограничение K историческое |
| W5: сохранённые фильтры общего механизма | Main registry, **Persistent saved filters**, **Typed conditions survive saved filters and export**; `K/tasks.md`, 5.4; `C/tasks.md`, 4.3–4.4 | Есть `resource=knowledge-base-entries`; хранение/исполнение backend неизвестно |
| W6: CSV всего отбора | Main export, **Full selection CSV export**; `K/tasks.md`, 9.1; main registry, **Typed conditions survive saved filters and export** | Прямой клиентский и mock owner; не backend-приёмка |
| W6: CSV отдельной карточки | Main export, **Saved detail export with visible unavailable sections**; `K/tasks.md`, 9.2 | Экспорт сохранённого ID, не черновика; вложенный экспорт не следует из body |
| W6: выбор полей | Оба предыдущих requirement; `K/design.md`, решение 7 | Выбор поддержанных metadata-полей; перечень полей не определён новым Jira body |
| W7: валидация полей | Main editor, **Field validation and reference preservation**, **Link editing and safe preview**; main mock, **Invalid mutation preserves data** | UI/mock-валидация не доказывает серверную |
| W7: валидация связей | Main editor, **External skills and responsible user**; main mock, **Invalid mutation preserves data**; `K/tasks.md`, 2.3, 3.3 | Есть локальные reference-сценарии; backend unknown |
| W7: уникальность | Main editor, **Field validation and reference preservation**; `K/design.md`, матрица решения 4: конфликт code, неподтверждённая уникальность name | Body не уточняет поля уникальности. Нельзя автоматически объявить name-дефект или снять предупреждение |
| W7: понятные полевые ошибки | Main editor, **Server rejects nested field**; `K/tasks.md`, 2.3 | Owner отображения ошибок найден; полнота backend errors — другая lane |
| D2: создание, просмотр, изменение | Main editor, **Persisted aggregate semantics**; `K/tasks.md`, 2.1, 6.1, 6.3 | Спецификация клиента, не backend completion |
| D2: поиск и фильтрация | Main registry, **Server-owned registry selection**, **Metadata-driven supported conditions** | Совпадает предметная операция, не доказано исполнение |
| D2: мягкое удаление | Main mock, **Knowledge base mock contract fidelity / Deleted code remains reserved**; `K/tasks.md`, 3.4 | Установлен mock owner. `K/design.md#Goals / Non-Goals` намеренно не добавляет кнопку удаления материала; это не противоречие backend issue |
| D3: атомарное сохранение карточки, ссылок, связей | Main editor, **Persisted aggregate semantics**; main mock, **Aggregate HTTP round trip**, **Invalid mutation preserves data** | Агрегатный payload и неизменность mock при ошибке не являются гарантией транзакции БД |
| D3: сохранение порядка ссылок | Main editor, **Persisted aggregate semantics / Reorder and clear**; `K/tasks.md`, 2.2, 7.2; main mock, **Aggregate HTTP round trip** | Прямой порядок массива в контрактной интеграции; backend unknown |
| D4: общий API справочников | `K/design.md`, решение 5; main mock, **Metadata and lookup ready for editor** | Клиент читает общий API |
| D4: централизованное управление значениями в «Справочниках» | `K/proposal.md#Impact`: нет редактора справочников; `K/design.md`, решение 4: lookup read-only, редактор категорий не добавляется | Полный owner управления не установлен. Возможное уточнение «централизованно» против «редактируемо» требует решения по источнику, не расширения KB UI |
| D5: сохранение условий поиска | Main registry, **Persistent saved filters**, **Typed conditions survive saved filters and export** | Прямой клиентский/mock owner |
| D5: экспорт списка/карточки с полями | Main export, два первых requirement | Повторяет W6; не дополнительное основание требовать вложенные таблицы |
| D6: префикс `/managed-resources/knowledge-base` | `K/design.md`, решение 5, точный search path; `K/tasks.md`, 2.1 | Есть контрактная интеграция; полная сверка путей относится к API-lane |
| D6: общий формат ответов | `K/tasks.md`, 2.1; main API integration, **Current API is the authoritative contract snapshot**; main mock, **Merged contract preserves accepted skill intents** | Owner контрактной совместимости, не backend-runtime |
| D6: проверка доступа | Main module, **Shell integration and deep links**; `K/tasks.md`, 1.4 — существующая UI boundary. Main mock, **Knowledge base mock contract fidelity** прямо исключает role enforcement | UI visibility и mock без credentials не закрывают backend authorization; owner исполнения неизвестен |
| D7: OpenAPI | Main API integration, **Current API is the authoritative contract snapshot**; `C/tasks.md`, 1.1–1.3; `K/tasks.md`, 2.1 | Owner импорта/согласованности контрактов найден. Наличие полного backend описания проверяется API-lane |
| D7: тесты основных сценариев и ошибок | `K/tasks.md`, 2–9; `C/tasks.md`, 4.1–4.4; main mock, **Mock regression safety** | Это задания на frontend/component/local HTTP tests, не доказательство backend-suite. Запуски не выполнялись |

## Main / archive / active: разграничение владельцев

**Main.** Предметные владельцы — `knowledge-base-registry`, `knowledge-base-editor`, `knowledge-base-export`. `knowledge-base-module` владеет подключением, доступностью и честными ограничениями UI, не серверной моделью. Общие `control-center-api-integration` и `control-center-mock-server` владеют соответственно контрактной интеграцией и локальным HTTP-контуром. `code-quality-gates / Application code respects FSD ownership and public APIs` определяет размещение optional-модуля, а не выполнение backend DoD.

**Archive K.** Полный набор — proposal/design/tasks и шесть specs: четыре KB, mock-server, code-quality-gates. Это поставка frontend + mock. Её явные исключения — backend-миграции, редактор справочников, новая permission-модель. Исторические задачи нельзя переименовать в реализацию MOS-1322.

**Archive C.** Proposal/design/tasks и относящиеся specs `knowledge-base-registry`, `control-center-mock-server`, `control-center-api-integration` уточняют типизированные условия, metadata, сохранённые фильтры/экспорт и воспроизводимость контрактов. Они заменяют старый запрет numeric/skill-name условий из K. Это не основание переписывать K и не серверная миграция.

**Active F.** Полностью прочитаны proposal/design/tasks/spec. Единственный owner — уточнение существующего `knowledge-base-export / Full selection CSV export`: HTTP 422 + `EXPORT_LIMIT_EXCEEDED`, локальная подсказка сузить отбор, сохранение полей, отрицательный сценарий другой 422. Новый body MOS-1322 подтверждает требование CSV, **но не требует именно этой UI-подсказки или конкретного envelope**. F остаётся самостоятельным capability-level исправлением, не закрытием backend issue и не новым backend acceptance.

Поиск точных `MOS-1322`/`MOS-1142` в main и change Markdown вне audit не дал прямого именованного владельца. Это ограниченный результат поиска, не доказательство отсутствия backend-владельца во внешней системе.

## Безопасные рекомендации

- **keep:** сохранить main-владельцев и границы K/C/F. Не добавлять кнопку удаления, редактор справочников, новые permissions, вложенный CSV или backend-миграции в frontend по этому анализу.
- **update:** добавить после review точные связи MOS-1322 → существующие capability owners с маркировкой «клиент / mock / контракт». Старый missing-body вывод заменить только новым additive observation, исторические отчёты не менять.
- **new:** новый corrective change в этом frontend-репозитории сейчас не обоснован. Отдельный backend owner может потребоваться, если подтверждённо отсутствует, но создать его по предположению нельзя.
- **question:** установить владельца MOS-1142 и backend-поставки MOS-1322; получить согласованную модель/миграции, доказательства транзакционности, серверного soft-delete и authorization, backend test evidence.
- **question:** уточнить поля и область уникальности; означает ли управление справочниками возможность редактировать системные значения либо лишь централизованное хранение/чтение. Не выводить ответ из frontend defaults.
- **coverage:** допустим bounded substantive SPEC-join, но только parent после API/REQ/IMPL lanes и независимого review решает overlay. Полное покрытие, delivery и deployment не подтверждены.

## SHA256 входов

Хэши вычислены локально по полным байтам; пути раскрываются через обозначения выше.

| Вход | SHA256 |
|---|---|
| `A/sources/jira-optional-backend-details/r1/content.json` | `3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618` |
| `A/sources/jira-optional-backend-details/r1/metadata.json` | `9357e481e237e04c47258fe4efb4bcc3d8377e2690e75963653d2275885ff4fc` |
| `A/work-items/WAVE-D092-OPTIONAL-BODIES.md` | `c2aed44985c2515b20c54e238d589ab997592c5c3d39d896bb1d3bb3485a15b3` |
| `A/decisions.md` | `fa7cffedb00f4d481efa2b523e8f1a1b4991b2750022c823c30c5370ab5cf945` |
| `A/reviews/R-D091-RECOVERY.md` | `f6fb801733ee223979debb0277de15e8f97448a3a69db6a2fb0f42f35c03e45d` |
| `A/reports/JOIN-MOS-1322.md` | `7a4d665bb17b268b3228a4dbc6d725f8235d7375ab957211a9e8c03b687a87c0` |
| `M/knowledge-base-module/spec.md` | `7e9d5498dd603b9ef5e7b241f81857dc767c3532009fa68ede116f4e496809f0` |
| `M/knowledge-base-registry/spec.md` | `909cde42dadfff0bad8caa5a75e09c01f5b3c538b6c2033c8cfe2d4a6b1f1733` |
| `M/knowledge-base-editor/spec.md` | `c2729b5220fc690b2866fd760bde2751fb43de1e13d70e4749f60438c72fbc36` |
| `M/knowledge-base-export/spec.md` | `87733e1890d135f29ef5629b8e1b2a3735e4f8fa3e8c9fdbad995a491c400973` |
| `M/control-center-mock-server/spec.md` | `54cd451a911c13129fbf8be64b06f920a837d4c816255f6ee6f5ee65f4406588` |
| `M/control-center-api-integration/spec.md` | `697c9c5fcb5e55e361662f93785ce5c2eb55ea8efd4992d18825c36b0107db09` |
| `M/code-quality-gates/spec.md` | `1e55e2fe646805cbe206f6a8ae6de00e38354657fc541bf3b39a2415a4797494` |
| `K/proposal.md` | `2ad551556756d7a32617702fba28b14302f5212546d96e66291f7d993b63e095` |
| `K/design.md` | `76110bb2afca215e8404fcd00c81c1ddc9f0c29caddef3af07a0a833beff2667` |
| `K/tasks.md` | `8da528d3d8cc27463bfea88b49dcb002aa07f2969bb0721531c5178045097e6d` |
| `K/specs/knowledge-base-module/spec.md` | `1aaad0aad54ba9222a4198a1aaf009a39aa4e6ea57c43d19facc5ebb3b3a8dd1` |
| `K/specs/knowledge-base-registry/spec.md` | `da86d44db2851bfe471819fd01975a648250c25717916ee60dd9960105b48c39` |
| `K/specs/knowledge-base-editor/spec.md` | `878e640610727625339945dbad63b3a12e681ca1c06b3d932c9a410b515362e4` |
| `K/specs/knowledge-base-export/spec.md` | `bf212f9c9d3c1b0801be80fc63f7b08c5f47edbaf294188f6b11980819ed6b62` |
| `K/specs/code-quality-gates/spec.md` | `f14b53e8e4e32c375bc54de6443599f2bf003dabbf5ab2d5ab06f22045b9f570` |
| `K/specs/control-center-mock-server/spec.md` | `74f740817881e745262ea22e8ca4a1233935ce9f49a5207a7fda7a3dc77e847e` |
| `C/proposal.md` | `6ece6e82490038d5ce491f19acf089c10a27dc845f74c2cf035ac37826c13bd8` |
| `C/design.md` | `58f8cdbd387508c10285387b3fcdbf208bfdb73559a8243997af676e38df6156` |
| `C/tasks.md` | `6002750f35319a52ce0c9fcd50731385ada811844c6edc3499943d87051dd478` |
| `C/specs/control-center-api-integration/spec.md` | `3c852185ac73c7b68a17ee03406953c2910b2ccabff864961d1530b279e12560` |
| `C/specs/knowledge-base-registry/spec.md` | `d15bfbc57ee26f736eaa47aa417180d7f63f26b4da516d279546e48cfe7ae107` |
| `C/specs/control-center-mock-server/spec.md` | `2441e5c89518d3c68f9edae32a788ca63bc4b6a5ffeb9fd5515a396f601ad4f8` |
| `F/proposal.md` | `8aac481ba21906ae1df106d3d4a65c0740d090ff4be503724edc99a068d998c8` |
| `F/design.md` | `7fc0c3ce641d76d24006590749d95ff458f236b33abc4b9bede66eebe9e5f7d4` |
| `F/tasks.md` | `0e3cf32ae03d54915f15618663ad4bbece0f7dbecbf159d35a80287efa26e95b` |
| `F/specs/knowledge-base-export/spec.md` | `d811d2612b24415e32074c60397cf3d73b7669c6e1499f6f9e010fa170baded3` |