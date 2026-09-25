## Context

См. `proposal.md` для мотивации и границ изменения. `app/shared/api/` пуст; три runtime-клиента (`skill-registry-client.ts`, `skill-details-client.ts`, `surface-registry-client.ts`) возвращают/генерируют локальные данные. Карточка навыка ищет запись через полный реестр. React Query уже установлен; query functions не передают AbortSignal. В шапке фиксированы имя и роль. Статьи `documentation-articles.ts` — встроенная справка, не mock API.

Vite использует React Router plugin и `base: '/tsam-panel/'`, но не proxy. Playwright запускает production build/server, поэтому dev proxy там сейчас не работает. Vitest включает только `app/**/*.test.{ts,tsx}` и использует jsdom.

Источник — `docs/api/contracts/openapi.json`: 20 paths, 28 операций, 93 схемы, HTTP Bearer. Доступны Access (1), Domains/Skills (8), Surfaces (11), Teams (8). Семь разделов не предоставлены. Успешные ответы обёрнуты в `code/data/message/errors`, данные списков — `items/pagination`. `ResponseCode` — произвольная строка, а не enum успеха. HTTP 422 описан отдельно через `HTTPValidationError`; детальная семантика 401/403/404/409 и переходов состояний не задана.

## Goals / Non-Goals

**Goals:**
- Один сетевой путь для dev и backend; смена окружения не переключает entity clients на локальные данные.
- Самостоятельный Express HTTP listener с корректным lifecycle Vite, воспроизводимыми fixtures и проверками против OpenAPI.
- Разделить wire DTO и модели представления, не поддерживать параллельно старый mock-протокол.

**Non-Goals:**
- Полная SSO-сессия, refresh/login/logout и RBAC не могут быть выведены из одного `/me`.
- Не строить новые страницы CRUD, универсальный SDK runtime, БД, автоматическую генерацию business logic из OpenAPI или поддержку несуществующих API.
- Не переносить встроенную справку, UI-константы и test doubles на dev-only сервер.

## Decisions

### 1. Источник типов и проверки

Генерировать TypeScript declarations через `openapi-typescript` из полного OpenAPI в `app/shared/api/`; результат коммитить, добавить команды генерации и проверки отсутствия дрейфа. Использовать type-only импорты DTO в клиентах и серверных fixtures. Ручная копия всех 93 схем дороже и быстрее расходится с источником; генератор runtime SDK не нужен.

На HTTP-границе проверять envelope и потребляемые данные имеющимся Zod, не доверять `as T` вместо проверки. Для контрактных серверных тестов использовать Ajv с JSON Schema 2020-12 и проверкой форматов (`uuid`, `date-time`, отдельная проверка `uuid7`); не отключать неизвестные форматы молча. Эти зависимости остаются dev-only. Поддерживать OpenAPI 3.1, а не преобразовывать источник в OpenAPI 3.0.

### 2. Минимальный общий fetch-клиент

`app/shared/api/` отвечает за base URL, URLSearchParams без undefined/null, HTTP method/body/headers, AbortSignal, JSON и единый объект ошибки. По умолчанию base URL — `/api/control/api`, независимо от UI base `/tsam-panel/`; entity clients используют относительные к API пути (`/skills/v1/skills`). Переопределение base URL через `VITE_CONTROL_API_BASE_URL` предназначено для адреса, не для секретов.

Транспорт возвращает проверенный `data`; ошибку сохраняет с HTTP status, исходными `code`, `message`, `errors`/validation details, если они есть. Не объявлять строку `code === 'success'` единственным признаком успеха: такого условия в источнике нет. Non-2xx и непустой `errors` считаются ошибкой; пустое/не-JSON тело ошибки не должно скрывать HTTP status. Успешный 204 допустим для транспорта без JSON-парсинга, хотя текущие операции возвращают JSON. Некорректное успешное тело — ошибка протокола, не пустой список.

Токен передаётся через минимальный настраиваемый provider в памяти; не сохранять его в localStorage и не добавлять production-token в `VITE_*`. Dev bootstrap предоставляет фиксированный явно фиктивный mock Bearer только при включённых dev-моках; при отключении моков используются переданные приложению credentials, без mock fallback. 401/403 отображаются как ошибки доступа, без автоматического refresh и придуманного logout. Будущая реальная SSO-интеграция подключится к этому provider, но не является условием локального dev.

`Idempotency-Key` обязателен только для POST/PATCH доменов и навыков согласно OpenAPI. Caller может передать ключ; иначе он создаётся один раз на логическую мутацию, а не на каждую попытку. Не делать автоматические retries мутаций. React Query остаётся владельцем кэша и политики повторов; 4xx и abort не ретраить, AbortSignal передавать до fetch. Не логировать Bearer или чувствительные тела.

### 3. Dev lifecycle и точный rewrite

Express в `mocks/` экспортирует создание приложения отдельно от запуска listener. Dev-only Vite plugin (`apply: 'serve'`, исключение preview) динамически импортирует сервер, запускает его на loopback до готовности dev-сервера и закрывает listener/connections при shutdown, restart и ошибке запуска. При занятом порте завершать запуск понятной ошибкой, не использовать неизвестный процесс.

Настройки: `CONTROL_API_MOCKS` включён по умолчанию для `yarn dev`, значение `false` отключает сервер и mock token; `CONTROL_API_MOCK_PORT` по умолчанию 3001. Express монтирует маршруты под `/api`; Vite proxy в `vite.config.ts` сопоставляет только `^/api/control/api(?:/|$)` и переписывает префикс в `/api`:

`/api/control/api/skills/v1/skills?limit=20&offset=0` → `http://127.0.0.1:3001/api/skills/v1/skills?limit=20&offset=0`.

Query string, методы, body, Bearer и Idempotency-Key сохраняются. `/tsam-panel/`, ассеты и похожие префиксы не перехватываются. В production, preview и при `CONTROL_API_MOCKS=false` моковый listener/rewrite не активны. Для реального backend вне dev используется same-origin API либо явно заданный base URL; production routing остаётся ответственностью окружения.

Альтернативы: встраивание Express в Vite middleware не выполняет требование отдельного mock target/rewrite; отдельный subprocess с concurrently требует лишнего supervisor. Listener в процессе Vite даёт реальный HTTP и один lifecycle.

### 4. Серверные данные и 28 операций

Разделить handlers по четырём разделам контрактов; хранить один связанный in-memory seed пользователей, команд, доменов, навыков, поверхностей. Сохранить узнаваемые названия/описания старых моков, заменить slug-ID фиксированными валидными UUID (UUIDv7 для skill/domain path), версии целыми числами и даты ISO date-time. Не импортировать runtime-fixtures в `app/`.

Покрыть все 28 method/path пар, включая чтение `/me`, create/update доменов/навыков/команд, участников, конфигурации/навыки поверхностей и шесть surface action endpoints. Мутации реально изменяют состояние, последующие list/detail согласованы. Один reset при создании приложения/перезапуске; тесты создают изолированные приложения, публичный reset endpoint не нужен. Для недокументированных переходов достаточно явно описанной mock-семантики: sandbox→sandbox, publish→prod, disable→disabled, enable→предыдущее активное состояние (для seed без истории — prod), archive→archived, restore→состояние до archive (для seed без истории — draft). Это dev-поведение, не утверждение о business rules backend.

Валидация обязательных заголовков, body, enum, UUID и `limit` (1–100)/`offset` (>=0) следует контракту; отсутствующий Bearer даёт 401, неизвестный ID — 404. Документировать mock-only error conventions там, где ответ не описан источником, не изменяя OpenAPI. Проверять обязательность Bearer для всех операций; не имитировать SSO/RBAC.

Сервер применяет фильтры/сортировку перед пагинацией. Для `sort`, заданного свободной строкой, документировать поддерживаемые существующие поля и `-field`, не объявляя это закрытым backend enum. При offset за концом выдавать пустую страницу, не тихо возвращать последнюю. Для заголовка идемпотентности хранить результат по method/path/key: повтор одинакового body возвращает прежний результат, другой body — mock conflict 409. Это явная dev-конвенция до подтверждения backend.

### 5. Миграция UI без поддельных полей

| Сейчас | Новый источник / поведение |
| --- | --- |
| SkillRegistry локальный массив, `status:asc`, slug доменов | `GET /skills/v1/skills`, `domain_id`/`team_id`, `limit`/`offset`, default `-updated_at`; убрать неподдержанный status filter/sort |
| Фиксированный список доменов | `GET /skills/v1/domains`, UUID и серверные названия; корректно загрузить все страницы справочника, не ограничить варианты первой страницей |
| Карточка ищет навык в полном реестре | Прямой `GET /skills/v1/skills/{skill_id}`; 404 отдельно от транспортной ошибки |
| `description`/`identifier`/строковая version списка | `purpose`, nullable `service_id`, integer `version`; описание карточки не подменяет purpose |
| Skill статусы, готовность, диалоги, conflicts, review, intents, checks, history, tokens | В контракте отсутствуют: убрать фиктивные значения, неподдержанные действия/фильтры; блоки карточки показывают «Не поддерживается текущим API» |
| Skill connection/workArea/contact | `connection.endpoint`, `contract_version`, `auth_required`/`auth_type`/parameters, `zones`, `contact`; учитывать nullable данные, не выдавать отсутствие за успешную настройку |
| Surface `checking`, `mobile_app` | Канонические `review`, `mobile_application`; русские подписи остаются UI-константами |
| Surface camelCase и `field:desc` | DTO `configuration_name`, `channel_id`, `stats.dialogs_30d`, `updated_at`; API sort `-updated_at` и остальные значения `SurfaceListSort` |
| Page/pageSize | На запросе `offset=(page-1)*pageSize`, `limit=pageSize`; ответ через `pagination.total_items/current_page/total_pages` |
| Имя/роль в шапке | `/auth/v1/me`, `display_name`, `full_name`, `roles`/`scope`; без константной роли «Администратор платформы» |

Сохранять простые adapters, если это сокращает изменения существующих компонентов, но DTO не содержат старые поля. Не подменять неизвестные enum значениями по умолчанию. Для отсутствующих значений различать «нет данных» и реальный ноль.

Обновить URL-state parsers и query keys вместе с UI; нормализовать старые неподдержанные фильтры/сортировки к новым defaults. Устаревшие slug detail-ссылки не искать в локальной таблице совместимости: показать невалидный/не найденный ресурс. Отменять устаревшие запросы. Состояния loading, error/retry, empty и unavailable должны остаться различимыми. Не превращать ошибку `/me` в гостя с полномочиями.

### 6. Проверки и команды

Добавить Node-окружение Vitest для серверных контрактных тестов, сохранить jsdom для UI. Поднимать Express на случайном свободном порте в тестах; исключить общий изменяемый сервер для параллельных тестов. Существующие проверки «без HTTP» заменить проверками реальных request/response; UI test doubles допустимы только в тестах.

Contract tests перечисляют все 28 операций из OpenAPI и требуют явного сценария для каждой; валидируют успешные ответы и описанные 422, данные seed и отсутствующие обязательные поля/неверные enum. Это не только snapshot внешнего вида. Отдельно проверить мутацию→чтение, идемпотентность, errors и две формы pagination schema.

Playwright переключить на `yarn dev --host 127.0.0.1` с автозапуском моков и проверить HTTP именно через Vite rewrite. Production build оставить самостоятельной проверкой: он не должен включать mock seed, запускать Express или требовать порт 3001. Проверить остановку/restart dev и повторный старт на том же порте.

## Risks / Trade-offs

- [В OpenAPI нет ряда уже нарисованных возможностей] → явные unavailable-состояния вместо расширения backend DTO; перечислить пробелы в README моков.
- [Нет формального success code и схем ряда ошибок] → использовать HTTP status/непустой errors, сохранять исходные поля; mock-конвенции маркировать отдельно.
- [Production SSO не предоставлен] → только token provider, без секретов в сборке; подключение настоящего источника токена — отдельная интеграция.
- [In-memory данные исчезают при restart и не моделируют конкурентный backend] → документировать reset и ceiling `ponytail:`; БД добавлять только при реальной потребности в долговечности dev-данных.
- [SSR/preview случайно запускают моки] → dev-only plugin, динамический import, отдельная проверка production build и preview.
- [Генератор типов не валидирует runtime] → Zod для потребляемых ответов и schema-based серверные тесты.
- [Старые E2E зависят от mock slug и выдуманных статусов] → обновить fixtures, assertions и base-path проверки вместе с UI, не оставлять fallback клиентов.

## Migration Plan

1. Зафиксировать матрицу операций/моков, сгенерировать DTO, подготовить HTTP transport и Express fixtures/handlers.
2. Подключить lifecycle/proxy, затем мигрировать текущие клиенты, query hooks, модели, URL-state и все потребляющие компоненты единым переходом.
3. Обновить HTTP/contract/UI/E2E-тесты и документацию; проверить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn test:e2e`, `yarn build`, генерацию без дрейфа и отсутствие моков в production.
4. Для отката откатывать изменение целиком (клиенты, UI, dev tooling), а не включать скрытый runtime fallback на старые моки. Источник OpenAPI не меняется.
