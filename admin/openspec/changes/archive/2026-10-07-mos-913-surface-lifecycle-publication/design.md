# Design

## Context

См. `proposal.md` и `specs/surface-lifecycle-publication/spec.md`. В текущем MOS-913 `useSurfaceDetailsQuery` получает detail поверхности через общий HTTP-клиент, runtime-схема уже проверяет `connection`, `configuration`, `status` и даты, а `SurfaceDetailsConnection` отображает серверный `embed_code` и копирует его без изменения. Вкладка «Конфигуратор» остаётся placeholder, lifecycle API-клиента нет, а обратная связь копирования пока локальная inline-разметка.

OpenAPI `docs/api/contracts/surfaces.openapi.json` и generated `app/shared/api/schema.d.ts` уже описывают:

- `GET /surfaces/v1/surfaces/{surface_id}` с `connection.embed_code` и `SurfaceStatus`;
- `PUT /surfaces/v1/surfaces/{surface_id}/configuration` с `UpdateSurfaceConfigurationRequest/Response`;
- шесть POST-операций `/sandbox`, `/publish`, `/disable`, `/enable`, `/archive`, `/restore`, каждая с `SurfaceStatusResponse`.

Отдельной операции генерации embed-кода, таблицы переходов, причины действия или idempotency key в контракте нет. `mocks/surfaces.mjs` уже регистрирует шесть операций; mock сохраняет предыдущий статус для `disable`/`archive` и возвращает его для `enable`/`restore`, но это локальная dev-конвенция. Все записи seed сейчас имеют nullable `connection.embed_code`, поэтому mock не должен добавлять фиктивный credential только ради прототипа.

## Goals / Non-Goals

**Goals:**

- Подключить существующие surface business API к карточке, сохранив generated-контракт и runtime-валидацию.
- Дать пользователю наблюдаемый lifecycle-блок, подтверждение публикации, доступную обратную связь, обновление полной карточки и повтор после ошибки.
- Сохранить серверное владение embed-кодом и различие между отсутствующим кодом, ошибкой чтения и успешным копированием.
- Разместить новую логику в текущем FSD-владельце: API и query/mutation-модель у `entities/surface`, presentation/action handlers у `widgets/surface-details`.
- Проверить существенные пути component/unit-тестами и mock server tests без browser/E2E.

**Non-Goals:**

- Новый endpoint, DTO или генератор embed-кода; frontend не сможет получить код, которого нет в detail-ответе.
- Авторизация, session bootstrap, permissions, RBAC и скрытие действий по пользователю.
- Новая state machine с неподтверждёнными правилами переходов, фоновые polling/release процессы, история операций и полноценный редактор всех полей конфигуратора.
- Новая библиотека toast/modal: используются существующие `Dialog` и widget-owned доступный live-region, если общий toast primitive в проекте отсутствует.

## Decisions

### 1. Расширить существующий surface API слой, не дублируя DTO

Добавить в `entities/surface/api/surface-registry-client.ts` typed-функции для шести POST-операций и `PUT /configuration`, используя `components['schemas']` из generated API types и Zod-схемы для ответов. Для lifecycle ответа достаточно строго проверить `surface_id`, enum `status` и `updated_at`; detail продолжает валидироваться существующей схемой.

Мутационный hook у `entities/surface/model` принимает `surfaceId` и литеральное действие, направляя его только на соответствующий endpoint. Это сохраняет общий HTTP transport и позволяет query cache оставаться единым для detail и списка.

Рассматривалась отдельная feature с ручными DTO и отдельным store. Она отвергнута: транспорт, ключи query и серверная модель уже принадлежат entity, а второй источник состояния создал бы расхождение с `useSurfaceDetailsQuery`.

### 2. Состояние lifecycle хранит серверный snapshot, а не локальную state machine

`SurfaceDetailsContent` остаётся координатором карточки. Lifecycle-представление получает `surface` через props; именованные props размещаются в `ui/types/*.types.ts`, обработчики — в `ui/.../handlers/`, приватные компоненты — рядом с `surface-details`.

Все шесть действий видимы в блоке и доступны, когда нет другой mutation. Кнопки блокируются только на время текущей mutation и при недоступности `surfaceId`; клиент не будет скрывать или блокировать действие на основании самостоятельно придуманной полной матрицы переходов. Ответ сервера является источником целевого статуса. Если backend отклонит неподходящий переход, ошибка отображается и старый snapshot сохраняется.

После успешной mutation ответ `SurfaceStatusResponse` используется для немедленного отображения нового `status`/`updated_at`, затем выполняется refetch detail для актуальных configuration, connection и enabled skills. Успех операции и ошибка обновления snapshot различаются: при сбое refetch не отменять подтверждённую серверную операцию, но показывать предупреждение и retry чтения.

Альтернатива — разрешать действия только в guessed mapping вроде `prod → disabled → prod`. Она отвергнута, потому что текущий OpenAPI не определяет source status, а UI мог бы скрыть поддержанное backend-действие или выдать локальный запрет за бизнес-правило.

### 3. Публикация использует существующий Dialog как двухфазный UI

Нажатие «Опубликовать конфигурацию» открывает controlled `Dialog` с понятным описанием последствия и кнопками «Отмена»/«Опубликовать». До подтверждения POST не выполняется. После подтверждённого успешного publish и запуска refresh тот же widget-owned dialog переходит в success-состояние с явным закрытием.

Ошибку publish не показывать как success modal. Её сообщение и retry остаются в lifecycle-блоке; повтор использует сохранённое действие и не создаёт вторую параллельную mutation. Для `disable` и `archive` не изобретать request-body с подтверждением: OpenAPI его не описывает. Если бизнес-контракт позже потребует confirm/reason, это отдельная дельта API.

Для copy и остальных lifecycle действий общего toast primitive в проекте нет. Добавить локальный feedback-компонент владельца виджета с `role="status"` для успеха, `role="alert"` для ошибки, `aria-live`, клавиатурной доступностью и возможностью закрытия/повтора. Не создавать shared API только ради одного потребителя и не добавлять зависимость.

### 4. Embed-код только читается из detail

Текущий connection component продолжает выводить `embed_code` через текстовый `pre/code`; lifecycle change не меняет строки, не вставляет `dangerouslySetInnerHTML` и не строит fallback по `channel_id`, domain или surface UUID. Кнопка copy принимает оригинальную строку и выставляет success feedback только после resolve Clipboard API.

Если `embed_code` nullable или whitespace-only, отображать «код не сохранён» и disabled button. Не добавлять в seed строку с вымышленным `data-token`. Для happy-path component-тесты передают серверный fixture напрямую; mock contract test отдельно подтверждает, что null остаётся null. Получение кода после publish возможно только если detail API реально вернул новое значение.

### 5. `PUT /configuration` остаётся отдельной mutation

Добавить client/schema coverage существующего `PUT /configuration`, но не вызывать его автоматически перед publish: publish API не принимает body, а подмена сохранения конфигурации lifecycle POST нарушила бы контракт. Если в текущей ветке появится форма конфигуратора, её сохранение отправляет контрактный payload в `PUT /configuration`, обновляет query и затем refetches detail. В рамках этого change не создавать фиктивный редактор вместо существующего placeholder.

После config save или lifecycle success не очищать query data и не сбрасывать черновики сценариев. При ошибке refetch показывать последний snapshot с retry; при первичной ошибке detail остаётся в существующем fallback.

### 6. Ошибки и retry не маскируют неизвестный исход

Для каждой mutation хранить последнюю целевую action и `surfaceId`, чтобы кнопка retry повторяла именно её. На время запроса использовать один общий pending guard, чтобы двойной клик не создал параллельные операции. Ошибка 4xx/5xx и сетевой reject маппятся на понятный текст без auth-flow.

Контракт не содержит idempotency key для surface lifecycle. Поэтому после transport error UI не заявляет, что операция не произошла; сначала detail retry позволяет увидеть серверный статус, а повтор действия остаётся явно доступным. Это ограничение фиксируется тестом и не решается локальным генератором request ID.

### 7. Mock API проверяет контракт, но не выдумывает production semantics

Сохранить существующие handler paths в `mocks/surfaces.mjs`. Расширить server tests так, чтобы они проверяли ответы всех шести операций по `SurfaceStatusResponse`, обновление team relation и состояние после последующего GET, а также 404/validation/error retry path. Mock fallback для `enable`/`restore` документировать как dev-конвенцию.

Изменять seed `embed_code` только при наличии согласованного server-owned значения без секретоподобного выдуманного token. Иначе тестировать null fixture и component happy path через server response double; production OpenAPI не расширять ради визуального прототипа.

### 8. Verification follows project gates

Добавить component tests для:

- exact copy, success-after-resolve, failure/unavailable Clipboard API;
- publish cancel/success/error and success modal;
- each lifecycle action request, pending guard, status refresh, stale snapshot and retry;
- null embed code and absence of synthetic token.

Добавить unit tests для endpoint mapping/error schemas и Node server tests для mock handlers. Не создавать и не запускать E2E/browser tests. После реализации пройти `yarn typecheck`, `yarn lint --max-warnings 0`, `yarn test`, `yarn format:check`; `yarn api:check` — при изменении OpenAPI/generated output.

## Risks / Trade-offs

- **[Risk]** Backend может разрешать другой набор переходов, чем локальная mock-конвенция → **Mitigation:** не внедрять guessed state machine; принимать серверный ответ, показывать ошибку, вынести согласованную матрицу в отдельную API/spec дельту.
- **[Risk]** Network error после принятой сервером mutation оставляет неизвестный исход → **Mitigation:** сохранять старую карточку, предлагать detail retry, явно не утверждать rollback/idempotency; повторять только по явному действию пользователя.
- **[Risk]** `embed_code` остаётся `null`, и прототип ожидает код → **Mitigation:** честное unavailable-состояние; не добавлять fake token. Генерация требует backend contract decision.
- **[Risk]** Refetch после mutation падает → **Mitigation:** сохранить последний snapshot, отобразить подтверждённый response status отдельно от ошибки refresh и дать retry.
- **[Risk]** Локальный feedback-компонент может разойтись с будущим общим toast-паттерном → **Mitigation:** ограничить его surface-details, использовать стандартные роли/классы и не делать новый shared API.
- **[Risk]** `PUT /configuration` UI пока placeholder → **Mitigation:** покрыть typed client/contract и не выдумывать поля редактора; publish не вызывает configuration PUT без фактического сохранения.

## Migration Plan

Миграции данных и новые зависимости не требуются. Реализация добавляется поверх существующих detail/query keys и endpoint paths; при откате lifecycle block, publish dialog и mutation client удаляются, read-only connection/overview MOS-913 продолжают работать. Mock остаётся dev-only и не включается в production build. Перед apply необходимо получить решение по таблице переходов и источнику/моменту генерации embed-кода либо принять зафиксированный fallback «только server-returned value».

## Open Questions

- Backend/product должны подтвердить матрицу `source status → allowed action → resulting status`, особенно для `sandbox`, повторной `publish`, `enable` после `disable`, `archive` и `restore`; до этого действует консервативный сервер-авторитетный режим из Decisions 2.
- Backend должен подтвердить, генерируется ли embed-код при создании/сохранении конфигурации и возвращается ли он в detail после lifecycle-операции. В текущем change допустимо только чтение nullable `connection.embed_code`; отдельная генерация или новая ручка не предполагаются.
