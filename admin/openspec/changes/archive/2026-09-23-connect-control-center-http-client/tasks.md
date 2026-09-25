## 1. Контрактная основа

- [x] 1.1 Зафиксировать в `mocks/README.md` матрицу 28 method/path операций, переносимых runtime-моков и отсутствующих контрактных полей по `design.md`; проверить инвентаризацией всех API-клиентов/потребителей в `app/`, что ни один runtime mock не пропущен, а статьи справки и test doubles явно исключены.
- [x] 1.2 Добавить devDependencies Express, типы Express, openapi-typescript и Ajv 2020-12 с проверкой форматов; обновить lockfile и проверить успешный `yarn install --immutable` после установки.
- [x] 1.3 Сгенерировать type-only DTO из `docs/api/contracts/openapi.json`, добавить команды генерации/проверки дрейфа; проверить повторную генерацию без diff и падение проверки на временно устаревшем generated output, не изменяя исходный контракт.

## 2. Общий HTTP transport

- [x] 2.1 Реализовать fetch transport в `app/shared/api/` с base URL, URLSearchParams, method/body/headers и AbortSignal; проверить тестами кириллицу, пропуск optional query, отсутствие `/tsam-panel/` в API URL и передачу signal.
- [x] 2.2 Добавить Zod-проверку envelope/потребляемых DTO и единые HTTP/protocol errors; проверить 200 с произвольным code, непустой errors, 204, 401/403/422, HTML 500, malformed JSON и сетевую ошибку без подмены пустыми данными.
- [x] 2.3 Добавить token provider и поддержку Idempotency-Key для требующих его операций без автоматического retry мутаций; проверить передачу заголовков, сохранение явно переданного ключа и отсутствие mock credentials/localStorage/logging вне mock-dev режима.
- [x] 2.4 Настроить Query retry без повторов 4xx/abort и обеспечить передачу signal из query functions; проверить отмену устаревшего запроса и отсутствие замены актуальных данных его ответом.

## 3. Express mock API

- [x] 3.1 Создать изолируемое Express-приложение в `mocks/` и связанный seed, перенести допустимые данные старых реестров/карточек/справочников/профиля с UUID/UUIDv7, integer version и ISO date-time; проверить схемы seed, связи ID, nullable поля и независимость двух экземпляров состояния.
- [x] 3.2 Реализовать Bearer guard, контрактную валидацию path/query/body/header, JSON-ошибки и 404; проверить невалидные enum/UUID/UUIDv7, limit 0/101, отрицательный offset, отсутствие обязательных полей/Idempotency-Key и Bearer, включая schema check описанных 422.
- [x] 3.3 Реализовать `GET /auth/v1/me` с контрактными full_name/roles/scope; проверить успешный ответ по CurrentPrincipalResponse и отказ без Bearer.
- [x] 3.4 Реализовать четыре операции Domains (list/create/detail/update) с query/team_id/zone/sort/limit/offset; проверить каждую операцию по OpenAPI и create/update→detail/list, фильтрацию до пагинации и offset за концом списка.
- [x] 3.5 Реализовать четыре операции Skills (create/list/detail/update) с domain_id/team_id и контрактными nested/null полями; проверить все ответы по OpenAPI, сортировку, create/update→detail/list и detail навыка вне первой страницы.
- [x] 3.6 Реализовать идемпотентность POST/PATCH доменов/навыков по method/path/key; проверить повтор одного body без второй мутации и mock 409 для другого body с тем же ключом, задокументировать конвенцию.
- [x] 3.7 Реализовать пять операций Surfaces: create/list/detail/configuration/enabled-skills; проверить ответы по OpenAPI, новые enum/sort, пагинацию и чтение изменённой конфигурации/набора навыков.
- [x] 3.8 Реализовать шесть surface actions sandbox/publish/disable/enable/archive/restore с mock-семантикой из design; проверить каждую операцию и согласованность status в последующих list/detail, явно описать отличие dev-конвенций от неподтверждённых правил backend.
- [x] 3.9 Реализовать четыре операции Teams list/create/detail/update; проверить схемы ответов, query/sort/pagination и согласованность связанных team-представлений после мутации.
- [x] 3.10 Реализовать четыре операции участников команды list/add/update/remove; проверить обязательные тела и параметры, последующее чтение состава и member_count, изоляцию команд и все ответы по OpenAPI.

## 4. Автозапуск и Vite rewrite

- [x] 4.1 Добавить dev-only Vite plugin с запуском Express listener до ready и cleanup на shutdown/restart/ошибке; проверить один `yarn dev`, остановку/повторный запуск на том же порте и понятный отказ при занятом порте.
- [x] 4.2 Настроить proxy/rewrite `/api/control/api` → `/api` в `vite.config.ts`, CONTROL_API_MOCK_PORT и CONTROL_API_MOCKS; интеграционным HTTP-тестом проверить GET query, POST body/Authorization/Idempotency-Key и отсутствие перехвата `/tsam-panel/`, ассетов и похожих префиксов.
- [x] 4.3 Подключить фиктивный dev token только при активных моках и исключить сервер из build/preview; проверить dev opt-out, production/preview без mock listener/token и отсутствие seed/handlers в клиентской сборке.

## 5. Миграция существующих экранов

- [x] 5.1 Перевести skill registry/detail/filter clients на общий HTTP transport, добавить потребляемые API доменов/команд и адаптеры DTO; тестами реального HTTP проверить прямой detail, все страницы справочников, limit/offset и отсутствие локального поиска/генерации карточек.
- [x] 5.2 Обновить модели навыков, URL-state, query keys, фильтры и таблицу под UUID domain_id, purpose/service_id/integer version и поддерживаемую сортировку; UI-тестами проверить фильтрацию/пагинацию, нормализацию старых URL и отсутствие выдуманного status sort/filter.
- [x] 5.3 Адаптировать карточку навыка к SkillResponse/connection/zones/contact; удалить синтетические lifecycle/review/intents/checks/history/tokens, оставив явные unavailable-блоки и недоступные действия; проверить null-значения, неизвестный ID, HTTP error и отсутствие фиктивных успешных проверок/токенов.
- [x] 5.4 Перевести surface registry client и модели/фильтры/сортировку/URL-state на HTTP и новые DTO; проверить review/mobile_application/-updated_at, nullable channel_id, stats.dialogs_30d, серверную пагинацию и различие null/0 в UI.
- [x] 5.5 Подключить `/me` к шапке через query и заменить фиксированное имя/роль/инициалы; проверить успешный профиль, loading и 401/403 без fallback на администратора.
- [x] 5.6 Удалить оставшиеся runtime fixtures, mock supplement generators и локальную серверную фильтрацию из `app/`, обновить старые тесты «без HTTP»; проверить поиском и dependency graph отсутствие импортов `mocks/` вне тестов и наличие отдельных loading/error-retry/empty/unavailable состояний.

## 6. Сквозные проверки и документация

- [x] 6.1 Настроить Node-тесты сервера наряду с jsdom UI-тестами и контрактную проверку покрытия всех 28 операций; проверить успешные/описанные validation responses через JSON Schema 2020-12, обязательные форматы включая uuid7 и падение проверки при пропущенном handler/scenario.
- [x] 6.2 Переключить Playwright на dev-сервер с автозапуском моков и обновить UUID/контрактные ожидания E2E; проверить навыки, прямую карточку, поверхности, профиль, фильтры/сортировку/пагинацию через реальный Vite rewrite и UI base `/tsam-panel/`.
- [x] 6.3 Обновить README и `mocks/README.md`: одна команда dev, переменные/opt-out, base URL, token provider, reset, mock error/sort/state conventions и отсутствующие API; проверить команды по инструкции на чистом запуске без ручного старта второго процесса.
- [x] 6.4 Выполнить генерацию без дрейфа, `yarn typecheck`, `yarn lint`, `yarn test`, `yarn test:e2e`, `yarn build` и production/preview smoke без моков; зафиксировать результаты, проверить `git diff --check` и неизменность исходного OpenAPI.
  - Проверено: `yarn api:generate` + `yarn api:check` (generated DTO не изменились), `yarn typecheck`, `yarn lint` (0 ошибок, 8 предупреждений complexity), `yarn test` (86 Vitest + 5 Node), `yarn test:e2e` (2 Chromium), `yarn build` — успешно.
  - Production `yarn start` и `vite preview`: `/tsam-panel/` HTTP 200; mock-порт закрыт, mock API не отвечает; в сборке нет mock token/seed. `git diff --check` — успешно. SHA-256 `docs/api/contracts/openapi.json` до и после проверок: `17ab96a9e9db25e15678c0b9ec606134f4f78e6c5aad251b4263caabbdba7443`.
