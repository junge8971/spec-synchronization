## Why

Т — текущий deployment backend ЦАМ и MPMM, а не условие включения auth. Приложение из production-сборки использует реальный API и MPMM; yarn dev по умолчанию использует локальные моки. Сама команда build создаёт артефакты без пользовательской сессии и сетевых auth/business-запросов. Отдельно согласованный в этой переписке auth-этап подключает существующую сессию MPMM и серверные permissions, не создавая вторую систему входа или управления ролями.

## What Changes

- **BREAKING (real mode, включая production build/start):** до отображения бизнес-страниц требуется пригодная общая сессия MPMM и валидный `/api/control/api/auth/v1/me`; без токенов выполняется переход на настроенный login URL MPMM с текущим default `https://mobile-t-tech.mos.ru/sa-admin`.
- Подключить чтение `localStorage["token"]`, проверку `exp` admin JWT, single-flight refresh через MPMM и передачу двух raw-заголовков `X-Access-Token` / `X-Admin-Token` для JSON и файловых запросов к разрешённым API.
- Применять permissions точного действия, целого ресурса или `*` к видимости меню, прямым URL, вкладкам и элементам действий UI. Запрещённые по permissions действия скрывать. Не вводить frontend ACL по method/path, permission-проверки в request/mutation handlers или локальные HTTP 403; авторизацию запросов выполняет backend. Не использовать названия ролей как источник полномочий; scopes и ограничение данных остаются ответственностью backend.
- Использовать опубликованную гранулярность `TSAM.Skill:change_status` без обещания разделения согласования и выката. Непокрытые матрицей разделы/действия доступны только с явным `*` до отдельного расширения.
- Точечно обновить контракт `/me` и security metadata, сохранить все принятые бизнес-операции, включая диалоги; зафиксировать минимальный auth-контракт MPMM в репозитории.
- Ввести отдельные состояния проверки сессии, временной ошибки и отказа доступа; исключить утечку старого пользовательского кэша при смене общей сессии.
- В real mode изолировать локальные черновики регистрации навыка по подтверждённому `user_id` и окружению; старые записи без владельца не присваивать пользователю, не открывать и не удалять автоматически. После refresh того же пользователя сохранять черновики и параметры незавершённых логических операций, включая Idempotency-Key, без автоматического replay; при смене пользователя не переносить их в новый контекст.
- Выбирать режим по dev/build конфигурации, не по hostname: yarn dev использует существующий mocksEnabled; CONTROL_API_MOCKS=false включает real API/auth. Production build/start/preview всегда real mode, даже при CONTROL_API_MOCKS=true. Детали mock `/me` и выбора fixtures задаёт add-local-session-demo; реальные credentials в mock mode не читаются.
- Не добавлять собственный OIDC-flow, logout endpoint/UI, редактор ролей, backend-политики, новые бизнес-функции или browser/E2E-тесты.

## Capabilities

### New Capabilities

- `mpmm-session`: lifecycle общей сессии, `/me`, refresh, разрешённые адреса, обработка ошибок и выбор real/mock режима по конфигурации.
- `control-center-permissions`: точные правила permissions, матрица UI, отказ по умолчанию и серверное владение областями данных.

### Modified Capabilities

- `control-center-http`: два auth-заголовка в защищённом режиме, общий путь JSON/файлов, сохранение идемпотентности и запрет автоматического replay мутаций.
- `control-center-shell`: согласованное исключение для auth-этапа, session/access boundary, меню и вкладки с учётом прав без смены канонических URL.
- `control-center-api-integration`: bootstrap `/me`, изоляция query-cache и проверки real/mock режимов.
- `control-center-mock-server`: правила точечного обновления объединённого контракта при сохранении бизнес-моков без auth.

## Impact

- `app/root.tsx`, `app/application`, `app/providers/query-client-provider.tsx`, navigation/section tabs и вызывающие бизнес-действия features/widgets/pages.
- `app/shared/api/http-client.ts`, shared technical auth/config segments; новые session/principal entity API и permissions policy с публичными FSD-границами.
- `docs/api/contracts`, generated `app/shared/api/schema.d.ts`, contract tests, unit/component tests, документация real/mock запуска.
- Адрес real API выбирает существующий resolver с сохранением VITE_CONTROL_API_BASE_URL и mobile a/c/t → nchat a/c/t; MPMM login и refresh задаются конфигурацией окружения. Текущий API на Т и defaults MPMM: `https://nchat-t-tech.mos.ru/api/control/api`, `https://mobile-t-tech.mos.ru/sa-admin`, `https://mobile-t-tech.mos.ru/gateway/admin/api/v1/auth/refresh`. CORS, доступность общей MPMM-сессии и серверная защита требуют подтверждения для фактического deployment; hostname не отключает auth.
- Новые runtime-зависимости не требуются: используются fetch, Promise, React Router Framework SPA, TanStack Query и Zod. MPMM и backend ЦАМ в этом change не изменяются.
- Источники решения: сообщения лида, предоставленные OpenAPI `message (1).txt` (ЦАМ) и `message.txt` (Gateway), локальный MPMM `src/auth-providers/openid.ts`. Во время реализации необходимые контрактные фрагменты переносятся в repo; сборка не должна зависеть от Downloads или соседнего checkout.
