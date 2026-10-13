## 1. Границы и запуск

- [x] 1.1 Сверить AGENTS.md/config и частичные demo-модули с уточнённым scope: UI-only permissions, без Devtools/request ACL; проверить diff, сохранить конфигурационный выбор режима и gate реальной интеграции (Т — текущая площадка).
- [x] 1.2 Завершить включение demo через mocksEnabled. Config/unit-тестами проверить dev, real API/auth при opt-out, ошибку отсутствующей конфигурации, внешний override, loopback listener, production build/preview и независимость режима от hostname и недоступность режима через URL/storage.

## 2. Principal и presentation

- [x] 2.1 Завершить server-owned none/viewer/editor/full и endpoints /me/profiles. HTTP/schema-тестами проверить default, unknown 400, независимые посетители, credential-free ответы и 404 вне demo.
- [x] 2.2 Подключить demo bootstrap без token storage/refresh/redirects. Unit/component-тестами проверить schema error, 401/403/500, retry, неизвестный профиль и отсутствие fallback в неподтверждённый полный доступ.
- [x] 2.3 Подключить общую presentation-policy для меню/страниц/вкладок/кнопок без request ACL и permission guards в handlers. Component-тестами проверить none/viewer/editor/full, прямой URL и обработку выбранного backend 403.

## 3. Профиль и простое управление моками

- [x] 3.1 Добавить header ФИО/email/roles из подтверждённого principal. Component-тестами проверить пустые поля, безопасный текст, checking/error, keyboard/focus и мобильную компоновку.
- [x] 3.2 Добавить local-only панель «Моки» на существующем UI kit вне session/page boundary, без новых зависимостей. Component-тестами проверить доступность при none и ошибках /me/каталога, loading/retry и отсутствие controls в режиме реальной сессии.
- [x] 3.3 Реализовать сохранение profile ID в sessionStorage и полный reload с понятной подписью. Unit/component-тестами проверить отсутствие live switch, блокировку повторного выбора, storage failure без ложного переключения и загрузку выбранного /me после reload.
- [x] 3.4 Сохранить demo drafts отдельно по режиму/окружению/user_id. Unit/component-тестами проверить A→reload B→reload A, отсутствие чужих/legacy/MPMM записей, ожидание principal и отсутствие replay мутаций.
- [x] 3.5 Добавить dev-only каталог операций и штатный/403/500/delay 1500 мс поверх existing handlers. HTTP-тестами проверить validation до сценария, отсутствие мутации при 403/500, задержку/отмену, binary, /me, unknown 400, disabled mode и независимость ответа от роли.
- [x] 3.6 Добавить выбор/reset сценария конкретной операции с sessionStorage и memory fallback для сценариев. Unit/component-тестами проверить method/path matching, query-independent выбор, независимость вкладок, storage errors, recovery /me и отсутствие reset seed/refetch/replay.

## 4. Проверки и документация

- [x] 4.1 Сохранить прежнее бизнес-покрытие, validation/version/idempotency и unavailable endpoints. Mock HTTP/contract-тестами проверить demo/standalone и минимум одну разрешённую через UI create/update операцию; не объявлять scopes/rotation проверенными.
- [x] 4.2 Обновить README/mocks docs: yarn dev/opt-out, роли как fixtures, простая панель, reload/storage failure, response scenarios, credential-free scope и незакрытый gate реальной интеграции (Т — текущая площадка). Сверить docs с фактическим кодом.
- [x] 4.3 Запустить yarn typecheck, yarn lint, yarn test, yarn format:check, yarn api:check, yarn build и build с CONTROL_API_MOCKS=true. Проверить отсутствие demo fixtures/controls/listener в production и auth/business-запросов во время сборки; результаты записать отдельно от неподтверждённых runtime-проверок. Browser/E2E не запускать.
- [x] 4.4 Просмотреть diff на scope/FSD/лишние зависимости и неизменность auth-openapi.json; выполнить openspec validate add-local-session-demo --strict. Не синхронизировать/архивировать changes и не закрывать чужой gate автоматически.
