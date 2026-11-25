## 1. MOS-1260 — Реализовать CSV-экспорт списка и карточки опросника

- [ ] 1.1 Добавить два binary API клиента и выбор/порядок fields из metadata, export_max_rows и передачу применённого search списка. Проверка: отбор больше страницы, поля без дублей/минимум одно, detail без search, пустая выборка, dirty/new card и сохранённые данные вместо draft.
- [ ] 1.2 Подключить реальное скачивание Blob с именем Content-Disposition, общей session isolation и освобождением object URL. Проверка: CSV/BOM и имя, JSON/HTML вместо файла, 404/403/422 EXPORT_LIMIT_EXCEEDED, сеть, отмена/смена owner; нет ложного скачивания и требований специфичных только для dialog export.

## 2. Приёмка подзадачи

- [ ] 2.1 Проверить владение реализации и тестов в `app/optional/feedback`, адресные границы/public index.ts, application composition и отдельные route entrypoints, отсутствие новых UI-policy/permission mappings, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты, без browser/E2E.
- [ ] 2.2 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`; при изменении API-типов — `yarn api:check`, при изменении сборки — `yarn build`. Проверка: записать реальные результаты; environment failures не считать успехом.
- [ ] 2.3 Перед выпуском проверить оба CSV, фактические серверные ошибки авторизации, CORS Content-Disposition и реальный лимит. Проверка: конкретные результаты согласованных HTTP-проверок либо подтверждение владельца стенда без секретов. При отсутствии evidence gate оставить открытым.
- [ ] 2.4 Проверить интеграцию двух экспортов с applied search реестра и сохранённой карточкой после указанных зависимостей. Проверка: component/mock HTTP сценарии общего отбора и dirty detail, `yarn api:check` при изменении типов и `yarn build`; закрытие остальных FE-changes сверх зависимостей экспорта не требуется, реальные CSV gates пункта 2.3 остаются открытыми до проверки.
