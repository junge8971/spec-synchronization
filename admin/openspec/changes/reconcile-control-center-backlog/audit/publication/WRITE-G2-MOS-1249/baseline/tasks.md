## 1. MOS-1249 — Подключить API опросников, справочных значений и метаданных

- [ ] 1.1 Проверить актуальные CRUD/OpenAPI источники из design.md и их provenance в проекте; сохранить HTML/PDF источники. Использовать уже обновлённый aggregate и standalone managed-resources, сохранив старые пути и экспортное дополнение. Проверка: разрешение всех $ref, отсутствие потери старых операций, `yarn api:generate` и `yarn api:check`.
- [ ] 1.2 Добавить entities/feedback с публичным API, DTO/runtime schemas и клиентами CRUD, search, lookup, metadata; использовать существующий transport. Проверка: unit-тесты путей/тел, POST→GET, полной карточки PUT, 409/422 JSON Pointer, невалидного ответа, отмены и отсутствия автоматического replay.
- [ ] 1.3 Подключить опубликованную UI-policy ManagedResource read/create/update/delete/export через существующие mappings, сохранив session owner/generation. Проверка: unit-тест матрицы read-only principal и запрещённых actions; server 403 и поздний ответ другой сессии; фактические маршруты/скрытие элементов проверяются в changes владельцев UI; request ACL не появляется.
- [ ] 1.4 Добавить контрактные feedback/lookup/metadata handlers и fixtures в существующий Express, без credentials/role enforcement и без production-включения. Проверка: mock HTTP-тест успешного создания/чтения и конфликтов; existing session profiles/fixed-error механизмы сохраняются.

## 2. Приёмка подзадачи

- [ ] 2.1 Проверить FSD/public APIs, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты, без browser/E2E.
- [ ] 2.2 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`; при изменении API-типов — `yarn api:check`, при изменении сборки — `yarn build`. Проверка: записать реальные результаты; environment failures не считать успехом.
- [ ] 2.3 Перед выпуском проверить реальные CRUD/search/lookup/metadata, envelope ошибок/null, MPMM и глобальный scope. Проверка: конкретные результаты согласованных HTTP-проверок либо подтверждение владельца стенда без секретов. При отсутствии evidence gate оставить открытым.

Актуальный источник уже включён в aggregate change `update-control-center-contracts-put`; проверять его согласованность, не возвращать старую выгрузку. При реализации feedback handlers удалить соответствующие операции из явного unavailable-перечня. Остальные CRUD-разделы не реализовывать в этой задаче.
