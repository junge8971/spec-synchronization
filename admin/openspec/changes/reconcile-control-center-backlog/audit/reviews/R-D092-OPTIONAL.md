# R-D092-OPTIONAL — независимое evidence review

## Решение

**Шесть отчётов — ACCEPT; два API-отчёта — REVISE перед интеграцией рекомендаций. ESCALATE не требуется.**

Новые bodies позволяют предметный частичный анализ MOS-1322/1323. Backend delivery, deployment и успешность backend-тестов не доказаны. Нового frontend corrective change не требуется.

Обозначение `A` = `openspec/changes/reconcile-control-center-backlog/audit`.

## Проверка источников и hashes

- HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`, соответствует заданию.
- Полностью прочитаны все восемь отчётов, новый content/metadata и recovery-review; проверено решение D-091.
- Проверены **122 строки SHA256** отчётов: **122 совпадения**, отсутствующих файлов и несовпадений нет. Это проверка всех опубликованных таблицами fingerprints, не утверждение, что таблицы перечисляют каждый упомянутый файл.
- Новый content соответствует `metadata.sha256`.
- Старые membership locators подтверждены: index `items[140]/[142]`; hierarchy `results[22]` содержит MOS-1322 под MOS-1328, `results[23]` — MOS-1323 под MOS-1329. `parent:null` нового пакета не опровергает эти связи.
- Bodies действительно содержат 7 W / 7 DoD для KB и 8 W / 10 DoD для A/B. REQ-атомизация 33/46 соответствует тексту; число 100, sample-size clarification и export-limit UI feedback не приписаны Jira-body.
- Независимое структурное сравнение JSON воспроизвело результаты:
  - KB: **18 path items, 27 операций, 65 достижимых schemas**.
  - A/B: **9 path items, 14 операций, 38 достижимых schemas**.
  - Отличий schemas и path objects после исключения security нет; соответствующие local path objects совпадают с merged contract.
- Прочитаны решающие mock handlers, A/B validation, основные editor specs, конкретные roundtrip/CSV assertions; проверены owner/non-goal и typed-condition locators. Это ограниченная независимая семантическая проверка, не повторный полный аудит optional-модулей.
- Тесты только читались, не запускались. Сеть, браузер, серверы, business requests и изменения файлов отсутствовали.

## Поотчётные результаты

| Отчёт | Вердикт | Finding и безопасное решение |
|---|---|---|
| REQ-MOS-1322-r2 | **ACCEPT** | 33 атома корректно разделяют storage/migrations, aggregate, CRUD, справочники, поиск, CSV, validation/access/tests. Верно: body не устанавливает partial PUT или сохранение link IDs. Keep; вопросы этой lane означают «не определено данным body», а не отсутствие ответа во всех действующих документах. |
| REQ-MOS-1323-r2 | **ACCEPT** | 46 атомов сохраняют partial PUT, replacement коллекций, existing group IDs/order и запрет тегов вне draft. Configuration ≠ execution выдержано. Keep; не переносить body-only неизвестности в интегральный список нерешённых контрактных решений. |
| API-MOS-1322-r2 | **REVISE** | Контрактный join и структурное сравнение подтверждены. Ошибка рекомендаций: уже согласованная AND-нормализация названа новым вопросом согласования. Нужны поправки C1–C3 ниже; операции/DTO менять не требуется. |
| API-MOS-1323-r2 | **REVISE** | 14 операций / 38 schemas подтверждены. Предложение «отдельно согласовать синхронизацию security OR/AND» повторно открывает известное решение. Нужны C1–C3; никаких изменений auth-модели. |
| SPEC-MOS-1322-r2 | **ACCEPT** | Клиентские, mock и contract owners отделены от backend delivery. Backend migrations исключены основным change; текущие typed conditions не подменены старым ограничением архива. Export-limit change остаётся самостоятельным capability-level owner. Keep, новый frontend scope не создавать. |
| SPEC-MOS-1323-r2 | **ACCEPT** | Корректны identity, saved-status boundary, partial PUT, replacement, отсутствие UI DELETE и configuration-only scope. Sample-size change не закрывает backend issue. Keep. Отсутствие найденного backend owner не означает отсутствие владельца вне исследованных артефактов. |
| IMPL-MOS-1322-r2 | **ACCEPT** | Handlers действительно валидируют до мутации, используют deletedIds и экспортируют search без page; roundtrip assertions проверяют IDs/order, CSV — весь отбор. Изолированные lookup не доказывают централизованное редактирование. Keep; backend-транзакции и серверные права неизвестны. |
| IMPL-MOS-1323-r2 | **ACCEPT** | Подтверждены верхнеуровневый merge, replacement массивов, сохранённый status в проверке tag, soft-delete и full-selection CSV. Отсутствие membership-проверки group ID в validateGroups описано осторожно, без объявления доказанного обхода. Keep; не требовать запрета штатного добавления/удаления групп. |

## Обязательные поправки

### C1. Оба API-отчёта: известная нормализация, не новый auth-вопрос

Нормативные основания:

- `docs/api/contracts/README.md`, «Правила объединения».
- `docs/api/contracts/access-session.md`, «Источники и согласование».
- `archive/2026-10-09-integrate-mpmm-auth-permissions/design.md`, §10.
- `archive/2026-10-13-update-control-center-contracts-put/design.md`, решение о сохранении AND.
- `archive/2026-10-15-update-control-center-api-contracts/design.md`, §1; tasks 1.2.

**Обязательная интегральная формулировка:**

> Live r2 сохраняет формальный OR, local/merged — уже согласованную нормализацию AND двух raw-заголовков X-Access-Token и X-Admin-Token. Это известное документированное отличие, не новая неопределённость модели доступа и не основание отменять нормализацию. Фактическое backend enforcement и deployment compatibility остаются отдельно неподтверждёнными.

Применить к summary, security finding и рекомендациям обоих API-отчётов. Сам факт структурного различия оставить.

### C2. Удалить повторное согласование принятого решения

- **API-MOS-1322-r2 / update:** исключить security из предложения «зафиксировать … как вопросы контрактного согласования».
- **API-MOS-1322-r2 / question:** удалить вопрос «Какова согласованная security-семантика OR/AND…». Сослаться на существующие owners; оставить лишь запрос серверных доказательств применения доступа.
- **API-MOS-1323-r2 / update:** заменить «Отдельно согласовать синхронизацию security OR/AND» на сохранение действующей нормализации и известных release gates.

Не создавать auth-change, не переносить OR в local, не предлагать новый permission enum или enforcement в бизнес-моках.

### C3. Отделить пробел JSON OpenAPI от отсутствия документированной семантики

API-таблицы справедливо ограничены L/C, но их итоговые вопросы нельзя интегрировать как отсутствие правил во всём контрактном наборе.

`docs/api/contracts/crud-api.md` уже содержит:

- §19.1: KB partial PUT, replacement, link IDs/order, HTTP(S), nullable-поля, soft-delete и reference error.
- §20.1: A/B сумма 100, уникальность, partial PUT/replacement, IDs/order, saved-status tag restriction и `409 / IMMUTABLE_FIELD / /groups`, правила аудитории/дат/null.
- Общий CSV-раздел и §§19.2/20.2: весь отбор независимо от limit/offset; лимит и `422 EXPORT_LIMIT_EXCEEDED`.

**Обязательное уточнение API-рекомендаций:**

> Перечисленные гарантии не выражены проверенными JSON operation/schema objects; часть уже описана supplementary CRUD-контрактом и принятыми specs. Запрашивается подтверждение backend соответствия этим правилам и оставшихся действительно неописанных случаев, а не повторное принятие существующей семантики.

Это не делает документацию runtime evidence. Не менять корректные body-only оговорки REQ и не приписывать supplemental правила самому Jira-description.

Поправки можно зафиксировать отдельным обязательным additive overlay при принятии, сохранив исходные отчёты и их fingerprints. Применять исходные ошибочные API-рекомендации без такого overlay нельзя.

## Coverage и безопасный no-op

Текущая база — D-091:

- `acceptedEvidenceThrough=D-091`;
- **84P / 1B / 88U**, всего 173;
- MOS-1322/1323 пока U;
- global **11/28** неизменён.

После принятия этого review и обязательных поправок допустимы **два additive U→P**:

- MOS-1322 — exact-body requirement/API/spec/local-evidence join.
- MOS-1323 — аналогичный join с отдельно прослеживаемыми aggregate invariants.

Ожидаемый итог исключительно этих двух переходов: **86P / 1B / 86U**. P означает substantive partial analysis, не выполнение backend DoD. Этот review ledger не изменяет.

**Planning/code/spec no-op:** не создавать дубли CRUD/export/editor, backend migrations внутри frontend, редактор справочников optional-модуля, mock RBAC, traffic execution или статистику экспериментов. Не присваивать KB export-limit и A/B sample-size changes этим backend members как точное выполнение Jira acceptance.

Старые missing-body отчёты и failed runtime provenance сохраняются исторически. Новый пакет снимает только прежнюю локальную предпосылку отсутствия description.

## Остаточные риски

Не установлены production storage/migrations, транзакции и concurrency, фактическое исполнение validation/access, центральное редактирование справочников, backend test results и deployment. Comments, attachments и custom acceptance не собраны. MOS-1142 зафиксирован зависимостью, но его body не открывался. Документация, mock HTTP assertions и frontend permissions не заменяют эти доказательства.

## Fingerprints

SHA256 полных байтов; отчёты относительно `A/reports/`.

| Файл | SHA256 |
|---|---|
| REQ-MOS-1322-r2.md | `ca5de13da3c6c47884a7d4ef10a8feb1c07189d02614e99c083337ad7f40a4a4` |
| REQ-MOS-1323-r2.md | `f77ee1bae78b827ad5b370eedd80184f768e65bdf08217e8685ebbf442868f28` |
| API-MOS-1322-r2.md | `d0b91e5c92bc6be8bace301a140bacd2226daf4c372dc22ab0f8dfb203a6425c` |
| API-MOS-1323-r2.md | `47bfa093a876e41f84fd446fcb7fca6fc3aa59c6cf02ed87ef23fecf7a22cba1` |
| SPEC-MOS-1322-r2.md | `dd2a035b1e7c459fa31560bce9af5ed7f3cc179e01d05a0dc19f391681637672` |
| SPEC-MOS-1323-r2.md | `3aef056baca11deb102591510103da94cc6d04ee18b60e6db2aafcd425f29d64` |
| IMPL-MOS-1322-r2.md | `c1a1f160e85c10a33065d21d1523bd9c6133015ff3f99ee7dc3a4ad15377d85e` |
| IMPL-MOS-1323-r2.md | `9d8d26f6ec4774664f9edd847567e9afbb1a8b9bbc885b7eaaee5de4b9b94358` |

| Дополнительный вход | SHA256 |
|---|---|
| A/sources/jira-optional-backend-details/r1/content.json | `3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618` |
| A/sources/jira-optional-backend-details/r1/metadata.json | `9357e481e237e04c47258fe4efb4bcc3d8377e2690e75963653d2275885ff4fc` |
| A/decisions.md | `fa7cffedb00f4d481efa2b523e8f1a1b4991b2750022c823c30c5370ab5cf945` |
| A/coverage.json | `5a6df86e79f00bd2d6054733eda3f3a012f694d88aff37fb375c4a0f4cfb564c` |
| docs/api/contracts/README.md | `cb452cf8caf22245c7a62af5f16880e7b5c1b5aa6d591c5aa3e88261632929b3` |
| docs/api/contracts/access-session.md | `7de0f5bf490429d6847885096b1b3aa829f3ee3016714eb671663efc613aa8a1` |
| docs/api/contracts/crud-api.md | `4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058` |
| archive/2026-10-09-integrate-mpmm-auth-permissions/design.md | `abad61fde268e29440a61ca3781c364ea925f5ff8dcc43b84b34eb55c7631357` |
| archive/2026-10-13-update-control-center-contracts-put/design.md | `1fc1af4a37931abb995788bdb4509d4e1b252b9ba84315f96fe9eb3e729aa4e2` |
| archive/2026-10-15-update-control-center-api-contracts/design.md | `58f8cdbd387508c10285387b3fcdbf208bfdb73559a8243997af676e38df6156` |

Archive paths in the last three rows are relative to `openspec/changes/`.