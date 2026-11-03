## 1. MOS-1259 — Реализовать серверные сохранённые фильтры опросников

- [ ] 1.1 Добавить клиентов POST/GET list/GET ID/PUT/DELETE saved-filters и contract mocks; resource=feedback-surveys, имя 1–150, полная search-схема. Проверка: пагинация списка фильтров, 201→GET, immutable resource, empty PUT/null, ошибки /search/... и 404.
- [ ] 1.2 Реализовать создание, выбор/применение с offset=0, явное обновление выбранного ID и удаление по соответствующим UI permissions. Проверка: одинаковые имена создают разные ID, PUT не меняет другой фильтр, восстанавливаются все условия/sort/limit, устаревшая схема не применяется частично, ошибки не вызывают localStorage fallback.

## 2. Приёмка подзадачи

- [ ] 2.1 Проверить FSD/public APIs, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты, без browser/E2E.
- [ ] 2.2 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`; при изменении API-типов — `yarn api:check`, при изменении сборки — `yarn build`. Проверка: записать реальные результаты; environment failures не считать успехом.
- [ ] 2.3 Перед выпуском проверить владение, пагинацию и CRUD saved-filters. Проверка: конкретные результаты согласованных HTTP-проверок либо подтверждение владельца стенда без секретов. При отсутствии evidence gate оставить открытым.
