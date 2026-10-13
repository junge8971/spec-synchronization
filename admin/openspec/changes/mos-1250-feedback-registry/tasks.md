## 1. MOS-1250 — Реализовать реестр опросников и базовый отбор

- [ ] 1.1 Добавить /feedback, /feedback/new, /feedback/:surveyId, навигацию и крошки через существующую route configuration. Проверка: unit/component-тест basename, static new, detail URL, возврата и отказа доступа без бизнес-загрузки.
- [ ] 1.2 Реализовать таблицу названия/кода, типа, аудитории и статуса с lookup-labels, пагинацией и loading/empty/no matches/error. Проверка: серверный total отличается от размера страницы; неизвестный код и ошибка справочника не превращаются в вымышленные значения.
- [ ] 1.3 Реализовать query 2–200, мультиселекты status/type_code и поддержанные sort; одна модель search и URL с местом для conditions MOS-1258. Проверка: очистка/один символ, OR внутри фильтра, offset reset, stale responses, валидное восстановление URL/history/copy и отказ clipboard.

## 2. Приёмка подзадачи

- [ ] 2.1 Проверить FSD/public APIs, размещение declarations, доступность клавиатуры/ошибок/фокуса в затронутом UI и отсутствие небезопасного HTML/production mocks. Проверка: diff review и целевые unit/component-тесты, без browser/E2E.
- [ ] 2.2 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`; при изменении API-типов — `yarn api:check`, при изменении сборки — `yarn build`. Проверка: записать реальные результаты; environment failures не считать успехом.
- [ ] 2.3 Перед выпуском проверить серверный поиск, счётчики, пагинацию и lookup. Проверка: конкретные результаты согласованных HTTP-проверок либо подтверждение владельца стенда без секретов. При отсутствии evidence gate оставить открытым.
