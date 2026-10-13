## Why

Локально нужен простой выбор ответа `/me` для проверки доступного UI под разными тестовыми профилями. Пользователь отменил дорогой Devtools-стек и уточнил: permissions управляют представлением, авторизация запросов принадлежит backend.

## What Changes

- Включать mock principal вместе с существующими бизнес-моками через `mocksEnabled` в `yarn dev`; сохранять local-only и production isolation.
- Сохранить Express, fixtures и четыре фиксированных профиля none/viewer/editor/full. `/me` определяет permissions для UI; названия ролей остаются подписями.
- Добавить простую локальную панель «Моки» на существующем UI kit: профиль, конкретная операция, штатный ответ, фиксированные 403/500, задержка 1500 мс и сброс сценариев. Без TanStack Devtools, Query Devtools, MSW и новых зависимостей.
- При смене профиля сохранять ID в sessionStorage и полностью перезагружать страницу. Не реализовывать live-switch state machine. Сохранить отдельные demo-черновики по подтверждённому владельцу.
- Показывать подтверждённые ФИО/email/roles в шапке для реальной сессии и demo. Mock controls доступны отдельно, в том числе при none и ошибке `/me`.
- Использовать общую presentation-policy для меню, вкладок, страниц и кнопок. Не добавлять permission guards в transport, request handlers или business mocks. 403 проверяется как выбранный ответ backend, а не вычисляется из роли.
- Не симулировать MPMM credentials/refresh, object scopes и отсутствующие бизнес-API; сохранить валидацию, idempotency и обработку ошибок.

## Capabilities

### New Capabilities

- `local-session-demo`: локальный mock principal, фиксированные профили, простой выбор ответов и UI по permissions.

### Modified Capabilities

- `control-center-shell`: подтверждённый пользователь в шапке и отдельные локальные mock controls.
- `control-center-mock-server`: `/me`, серверные fixtures профилей и фиксированные сценарии поверх существующих handlers.

## Impact

Затрагиваются `vite.config.ts`, `mocks/`, session bootstrap/config, header, локальная панель и хранение demo-черновиков. Новые зависимости не нужны; существующий TanStack Query сохраняется. Production DTO и MPMM endpoints не меняются. Build создаёт артефакты без auth/business-запросов; реальный API используется при работе production-приложения. Режим выбирается dev/build-конфигурацией, не hostname; Т — текущий backend deployment. Изменение опирается на уточнённый `integrate-mpmm-auth-permissions` с UI-only permissions, а не на прежний request ACL. При будущей штатной синхронизации сначала auth-change, затем demo. gate реальной интеграции (Т — текущая площадка) остаётся открытым. Проверки — unit/component, mock HTTP/config и build; browser/E2E требуют отдельного разрешения.
