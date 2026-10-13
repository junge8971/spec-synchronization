## Context

Мотивация и границы согласования описаны в proposal.md. Это отдельно одобренный auth-change после этапа без сессии; прежний запрет остаётся действующим для несогласованных расширений.

Состояние рабочей копии после аудита 09.10.2026; это описание частичной реализации, не отметка о готовности:

- React Router 8 Framework SPA (`ssr:false`, basename `/tsam-panel/`); `app/root.tsx` — тонкий entrypoint, `ApplicationRoot` оборачивает Outlet в query provider и оболочку. Browser globals нельзя читать при build-time render.
- Бизнес-загрузки уже используют TanStack Query; `app/providers/query-client-provider.tsx` содержит singleton QueryClient и исключает retry для 4xx. Перенос всех страниц на route loaders не нужен.
- `app/shared/api/http-client.ts` имеет отдельные JSON и binary пути, общую обработку ошибок, AbortSignal и Idempotency-Key. Auth уже частично реализован с проверкой Т-origin и дополнительной request ACL. Эти ограничения расходятся с новым решением и подлежат замене; прежние тесты нужно сверить с новым scope.
- `getControlApiBaseUrl()` для production `mobile-t-tech.mos.ru` выбирает `https://nchat-t-tech.mos.ru/api/control/api`, а не same-origin. UI localStorage общий с MPMM только на mobile-origin.
- Навигация строится из общей таблицы существующих маршрутов. Permissions уже подключены к части меню, маршрутов и действий; требуется сохранить эту UI-политику, убрать request enforcement и заменить permission-disabled на скрытие.
- В MPMM reference есть `oidc-client-ts`, react-admin и async-mutex; они не установлены и не нужны в ЦАМ. Копирование reference целиком принесёт лишний OIDC-flow и гонку заголовков, сформированных до ожидания refresh.

Контрактные свидетельства:

- `message (1).txt`: точный `/api/control/api/auth/v1/me`, обязательные profile/roles/permissions/assignments, raw X-заголовки. Вложенное назначение содержит role_id/role_name/scopes/permissions. Старые scope/display_name отсутствуют.
- `message.txt`: refresh MPMM принимает четыре токена и возвращает result. Проверенные auth/roles части не отличаются от прежней выгрузки auth-openapi.json.
- Сообщения лида подтверждают вход через MPMM, список TSAM permissions, управление правами в MPMM; Т указан как текущий deployment, не условие включения auth.
- Формальное OR заголовков в OpenAPI противоречит явному тексту «оба». Описания аналитики ещё говорят об отсутствии permissions и Bearer. Выгрузка ЦАМ не включает восемь уже принятых путей диалогов. Эти несовпадения не скрываем за полной заменой контракта.

## Goals / Non-Goals

**Goals:** единая сессия с MPMM без дублирования входа; подготовка credentials до каждого бизнес-запроса; fail-closed UI при неизвестной сессии/правах; безопасная смена principal; одна проверяемая policy для маршрутов и действий.

**Non-Goals:** перенос business-data fetching на другой framework, универсальный RBAC/ABAC engine, клиентское вычисление object scopes, собственный logout/OIDC, создание недостающих API, управление правами через ЦАМ. Шесть ролей прототипа не являются enum или иерархией полномочий. Auth-зависимые ограничения не превращают недоступные бизнес-функции в доступные.

## Decisions

### 1. Режим задаёт dev/build конфигурация

`yarn dev` по умолчанию использует существующий mocksEnabled. `CONTROL_API_MOCKS=false` выбирает real API/auth. Production build/start/preview всегда используют real mode, даже при CONTROL_API_MOCKS=true. Hostname, query и storage не включают и не отключают auth. Prerender безопасен без window; это не runtime bypass.

Адреса Control API, MPMM login и refresh задаются конфигурацией окружения с текущими defaults. Существующий Control API resolver сохраняет VITE_CONTROL_API_BASE_URL и соответствия mobile a/c/t → nchat a/c/t; выбранный им адрес является configured/resolved destination. Выбор адреса и включение auth — отдельные решения. Не вводить framework конфигурации окружений. Изменение адреса требует проверки совместимости deployment, но не новой реализации auth. Mock principal и выбор ответов задаются add-local-session-demo; mock mode не читает MPMM credentials и не запускает refresh/login. Permissions UI применяется к principal обоих режимов.

`yarn build` создаёт SPA-артефакты, не подтверждает пользовательскую сессию и не делает auth/business-запросы при build-time render. Real mode применяется после открытия собранного приложения. `start` и preview обслуживают эту сборку; runtime env не меняет встроенный выбор mock/real. Отдельный третий режим «без моков и без сессии» не вводится.

Текущий `start` указывает на `build/server/index.js` при `ssr: false`. Перед признанием production запуска рабочим проверить SPA artifacts и адресно согласовать serve-команду с ними; команда не должна включать mock listener.

### 2. Разделение технической сессии и предметных прав

Предлагаемое владение без нарушения FSD:

- `shared/auth/` — технический token storage, Base64URL/exp, refresh, поколение сессии и подписка на его изменения. Никаких ролей ЦАМ или импортов entities.
- `shared/config/` — dev/build режим, настроенные MPMM endpoints, допустимые Control API origins/path prefixes.
- `shared/api/` — общий низкоуровневый fetch, abort, заголовки и отдельные envelope ЦАМ/MPMM. Бизнес-клиенты продолжают существующий API.
- `entities/session/` — Zod principal, получение `/me`, чистое сопоставление permissions и публичный API principal и React hooks. Свой API не импортирует другие entities.
- `app/application/` и `app/providers/` — координация lifecycle, session/access boundary, QueryClient cleanup и Router revalidation.
- Features/widgets/pages используют только публичный API session-слайса; таблица технических маршрутов остаётся в shared config, но не импортирует entity. Application layer связывает её с policy; resource/action constants принадлежат session-слайсу.

Именованные types/constants/handlers размещаются в соответствующих сегментах владельца. Новые компоненты — по одному на файл. Не создавать глобальные свалки или provider-framework ради единственного источника.

Альтернатива — shared HTTP импортирует auth entity — отклонена из-за обратной зависимости. Вместо неё app соединяет техническую сессию и principal, а низкоуровневый транспорт остаётся независимым от UI.

### 3. Bootstrap через штатные механизмы Framework SPA

Добавить root `clientLoader` и отдельный HydrateFallback, делегирующие bootstrap application-модулю; сохранить тонкий entrypoint и typegen. Root boundary до подтверждения контекста не монтирует бизнес-Outlets. Последующее обновление сессии управляется application-provider и Router revalidation, а не самописным роутером или безусловной загрузкой в каждом page effect.

Корневой loader сам по себе не сериализует параллельные дочерние loaders: защищённые будущие clientLoader/clientAction обязаны ожидать тот же readiness boundary. Для существующих TanStack Query-загрузок gate монтирования и guards enabled предотвращают ранние запросы. Перед отправкой сохраняется техническая проверка текущей сессии и владельца операции; permissions в mutation handler не проверяются.

Только вход в чужое SPA MPMM использует document navigation на настроенный login URL MPMM (текущий default `https://mobile-t-tech.mos.ru/sa-admin`); внутренних auth URL и открытого returnUrl нет. После входа пользователь возвращается через кнопку MPMM.

### 4. Состояния сессии и отсутствие рекурсивного refresh

```text
mock mode ----------------------------> mock principal -> UI

checking --> missing/invalid token ---> MPMM /sa-admin
    |
    +--> exp near/expired --> refreshing --+
    |                                      |
    +--------------------------------------+
                                           v
                                      loading /me
                                           |
                    +----------------------+----------------+
                    v                      v                v
                  ready                  denied           error
                    |
          token change / refresh
                    |
                    v
          invalidate context --> checking
```

Denied при отсутствии permissions — подтверждённая сессия с отсутствующим бизнес-доступом, не повод логиниться снова. Error network/protocol/storage имеет доступный retry и не очищает общую MPMM-сессию.

Token preparation и principal readiness — разные стадии. Refresh использует raw MPMM client, никогда бизнес `apiRequest`. `/me` использует prepared-token transport без ожидания самого principal. Обычные бизнес-запросы ждут обе стадии. Это исключает цикл «refresh -> /me -> ожидание /me». Application composition может зарегистрировать один узкий readiness callback для business transport; raw auth/profile paths не проходят его. Не перехватывать глобальный window.fetch.

В рамках одного экземпляра single-flight Promise объединяет refresh и переподтверждение principal. Abort отдельного потребителя отсоединяет только его ожидание. Новый HTTP-запрос после abort не отправляется.

### 5. Refresh, storage и ошибки

- Проверять строковые поля набора через Zod; id_token допускает пустую строку согласно response schema MPMM. Сохранять полный валидный result, включая дополнительные поля; неизвестные поля не служат правами.
- Декодировать JWT как Base64URL с проверкой числового конечного exp. Refresh начинается за 30 секунд до exp. Это подсказка клиенту, подпись проверяет сервер.
- Перед отправкой запроса перечитывать набор после ожидания refresh. Не формировать Headers заранее как в reference.
- Проверять status и result/error_code/error_message MPMM. Пустое/невалидное тело, отказ storage write и сеть не превращаются в «успешно обновили».
- При business 401 вернуть исходную ошибку, запустить одну общую recovery-попытку и `/me`, не replay исходный запрос. Для уже отклонённого восстановленного поколения повторная recovery запрещена: вход MPMM вместо бесконечного цикла. Мутации не имеют автоматического retry вообще; GET также не переотправляется скрытно ради refresh.
- 403 не меняет сессию. 401 refresh или `/me` прекращает локальный контекст и ведёт в MPMM. Не вызывать logout и не удалять общий storage ради локального отказа — MPMM владеет входом и глобальным выходом. Пользователь сможет вернуться после её восстановления сессии.
- На network/5xx/protocol failure заморозить protected UI с retry, сохраняя токены. Не очищать storage по широкому catch.

### 6. Смена principal и stale responses

Техническая сессия имеет монотонное поколение, без токенов в query keys. Изменение raw набора через storage event, focus-check или pre-request check инвалидирует principal до чтения новых данных. Собственный успешный refresh тоже перечитывает `/me`, чтобы не оставлять отозванные permissions.

App сначала блокирует бизнес-UI, отменяет QueryClient-запросы, очищает пользовательский query/mutation cache и file/object URL state, затем переподтверждает контекст. Сравнение поколения не позволяет поздним ответам, игнорирующим AbortSignal, попасть в новое состояние, инициировать скачивание или записать черновик. Безопаснее сначала очищать весь business cache, чем изобретать классификацию «точно общих» справочников.

Обновление технического поколения не тождественно смене пользователя. Пока идёт refresh/проверка `/me`, локальное состояние редакторов может сохраняться отдельно от доступности бизнес-UI, но не предоставляет старых прав: содержимое скрыто, обработчики и новые бизнес-запросы заблокированы. После подтверждения того же `user_id` сохраняются черновик и параметры прежней логической операции (тело, версия и Idempotency-Key); повтор возможен только явно через видимое по актуальным permissions действие с сохранением бизнес-ограничений. Размонтирование boundary или очистка mutation cache не должны сами создавать новую попытку с новым ключом. Отмена/отбрасывание ответа не доказывают, что сервер не выполнил запись; существующие состояния неопределённого результата и восстановления сохраняются. При другом `user_id` или утрате сессии прежнее состояние редакторов не переносится в новый контекст. После отзыва права UI скрывает форму и действие продолжения сохранённой операции; запросы независимо авторизует backend.

Локальный черновик регистрации навыка в real mode хранится в пространстве окружения и подтверждённого `user_id`, а не технического поколения или токенов. До подтверждения principal пользовательская запись не читается. Автосохранение и поздние завершения проверяют актуальность контекста перед изменением storage; нельзя записать данные прежней формы в запись нового пользователя. Существующие записи без владельца не импортируются, не показываются и не удаляются автоматически в защищённом режиме. Записи другого владельца также не переносятся и не удаляются; после возвращения подтверждённого владельца его черновик восстанавливается по действующим бизнес-правилам. Mock-черновики используют отдельное пространство согласно add-local-session-demo, без чтения MPMM token. Это изоляция приложения, не шифрование localStorage и не защита от XSS.

Перед записью refresh сравнивается текущее storage со снимком на старте. Если MPMM уже заменила/удалила token, ответ не записывается. Такая проверка снижает риск, но не является атомарной compare-and-swap между вкладками: MPMM не использует общий lock. Не добавлять фиктивную гарантию межприложенной сериализации.

### 7. Permission policy и UX

Нормативная матрица находится в delta control-center-permissions; не дублировать её в каждой feature. Чистая функция проверяет точное action/resource/`*`, без универсального wildcard parser. Для непокрытых операций отдельное правило «explicit wildcard only», не выдуманный permission, который позже можно случайно выдать.

Скрывать запрещённые menu items и tabs. На прямом существующем URL — «Нет доступа» с доступными ссылками; неверный URL остаётся 404. На доступной странице кнопки и формы запрещённых действий скрываются. Disabled и пояснения сохраняются для бизнес-валидации, pending и контрактно недоступных функций, а не для отсутствующих permissions. Permission-проверок в mutation handlers и HTTP transport нет; backend авторизует каждый запрос и возвращает собственный 403/404. После обновления `/me` UI заново вычисляет видимость, включая открытые диалоги.

Раздел `/skills` доступен при доступе хотя бы к одной вкладке; Domain:view без Skill:view открывает domains при отсутствующем/неизвестном tab. Явно запрещённый tab даёт отказ. Корневой `/` сохраняет канонический redirect `/skills`; если раздел недоступен, показывается отказ с доступными ссылками, не redirect-loop.

Ревью требует Skill:view + change_status. Change_status остаётся общим для разрешённых текущей бизнес-логикой переходов; новых переходов не добавляем. Аналитические view/refresh/configure используем по сообщению лида как клиентскую политику, отмечая конфликт backend-description.

UI вспомогательных справочников также учитывает permissions; скрытый UI не запускает свою загрузку, транспорт отдельно не проверяет права. Пример: создание навыка требует Skill:create и доступа к содержащему экрану; обязательные Domain/Team справочники требуют своих view. При недостатке не выдавать весь справочник по предположению и не подставлять fake option; показывать конкретную недостающую возможность. Селектор навыков поверхности требует Skill:view, сохранение — Surface:update. При наличии embedded данных в уже разрешённом DTO отображение не требует дополнительного запроса.

Реализованный request ACL (`application/model/request-permissions.ts`, `application/constants/request-permissions.constants.ts`, callback authorize в session binding) подлежит удалению: frontend не определяет доступность endpoint по method/path и не требует `*` для неизвестного запроса. `assertPermissions` и permission-часть `usePermissionGuard` не вызываются из request/mutation handlers. Проверки owner/snapshot/generation, отмены, stale responses и черновиков сохраняются отдельно; смена контекста означает техническую отмену, не синтетический backend 403. Матрица относится только к UI и не управляет доступностью сервисов.

### 8. Scopes остаются серверными

Assignments сохраняются без flatten permissions/scopes в новую object-policy. Агрегированные permissions используются только для функционального UI. Серверные ответы определяют доступ к конкретным объектам и данным, даже для `*`.

Не запрашивать `/internal/authorization/context` из браузера, не использовать X-Service-Authorization. ScopeResponse аналитики (all/team_skills/surface, notice) отображается как серверный результат, не как основание самостоятельно запросить более широкие данные.

### 9. Адреса, credentials и CORS

В real mode credentials допускаются только на configured/resolved HTTPS Control API из существующего resolver с проверкой origin/path boundary; refresh — только на настроенный HTTPS refresh URL. Текущий адрес API на Т: `https://nchat-t-tech.mos.ru/api/control/api` (сохранить существующие resolver mappings и override); defaults MPMM: login `https://mobile-t-tech.mos.ru/sa-admin`, refresh `https://mobile-t-tech.mos.ru/gateway/admin/api/v1/auth/refresh`. Конфигурация доверенных адресов задаётся окружением, не query/storage и не произвольным адресом вызывающего кода. Проверка destination защищает credentials и не включает auth по hostname. VITE_CONTROL_API_BASE_URL — доверенная build-time конфигурация: валидный HTTPS override заменяет destination, а не отклоняется за отличие от Т. Относительный base URL разрешается относительно origin приложения. Для каждого запроса проверяется соответствие итоговому origin и границе API path; чужой URL из аргумента запроса, query или storage не расширяет destination. Проверка выполняется до отправки credentials. Credential-bearing fetch использует `redirect:'error'`.

Не отправлять токены на внешние PDF/image URLs: только согласованные content endpoints. JSON и binary должны сходиться на одном механизме auth-preparation, сохраняя разные Accept/response handling. Нельзя подменять бизнес origin на same-origin без подтверждения маршрутизации.

localStorage ограничен origin: настройка удалённого login/refresh URL сама не переносит token между origin. Реальная интеграция использует согласованное размещение MPMM и ЦАМ; новый механизм передачи токенов между origin в scope не входит. Это ограничение интеграции, не причина отключать auth на другом hostname.

До выката владелец deployment подтверждает доступность общей MPMM-сессии для UI origin и preflight/actual responses между настроенными UI/API origins: разрешённый Origin, X-Access-Token, X-Admin-Token, Content-Type, Idempotency-Key и используемые методы. Не добавлять credentials:include без cookie-контракта. Проверка конфигурации и HTTP допустима без browser tests, но тестовые секреты не запрашиваются и не сохраняются в артефактах.

### 10. Контрактное обновление и совместимость спецификаций

Во время реализации сохранить минимальный refresh OpenAPI со всеми зависимыми схемами в `docs/api/contracts/mpmm-auth.openapi.json` и документировать provenance. Не копировать весь огромный Gateway ради одной операции. `/me` и dependency closure обновить в полном Control API и соответствующих самостоятельных разделах. Сохранить остальные схемы и восемь путей диалогов из repo; regenerated DTO получают новые principal types без ручной правки schema.d.ts.

Исправить security pair OR -> AND как явно обоснованную нормализацию, а не новое требование backend. Для диалогов применение пары заголовков опирается на сообщение лида «все endpoints», при этом отсутствие этих путей в выгрузке отмечается как release verification item. Старая проза Bearer и отсутствие analytics permissions отмечаются в документации; не переписывать неподтверждённые серверные гарантии.

Delta-specs заменяют прежние требования запрета auth только в защищённом режиме. Текущие бизнес-specs продолжают описывать поведение после успешного session/access boundary; mock режим не использует реальную MPMM-сессию, но получает тестовый principal по add-local-session-demo. В рамках apply адресно обновить AGENTS.md и openspec/config.yaml, чтобы зафиксировать разрешение именно этого change, не снять общий запрет и не ослабить другие quality/security правила.

## Risks / Trade-offs

- [Токены в localStorage доступны при XSS] -> это совместимость с MPMM; не логировать секреты, не рендерить небезопасный HTML, не расширять destination allowlist. HttpOnly/BFF требует отдельной backend-модели.
- [Общий token, refresh из двух SPA/вкладок] -> single-flight внутри ЦАМ, storage generation checks; невозможность полной координации явно признаётся. Совместимость refresh rotation — release gate, не обещание фронта.
- [Permissions UI не являются security boundary] -> object access и фильтрацию данных обеспечивает backend; release требует серверной проверки restricted account, без ложного объявления безопасности по component-тестам.
- [Непокрытые действия доступны только `*`] -> намеренное временное сужение UX. Не просить выдавать wildcard ради обычного доступа; новые granular permissions добавляются отдельным согласованием.
- [Общий change_status шире ролей прототипа] -> явно не обещать разделения reviewer/platform; серверный отказ сохраняется.
- [Часть документации отстаёт от реализации] -> хранить evidence/conflicts в repo, проверять фактическую интеграцию перед выпуском, не размывать контракт догадками.
- [Очистка кэша после refresh увеличит число чтений] -> цена корректности и отзыва прав; оптимизировать лишь при доказанной проблеме.
- [Refresh может размонтировать редактор и потерять ключ операции] -> отделить сброс серверного кэша от сохранения локальной операции того же подтверждённого пользователя; проверить сохранение тела/версии/ключа и отсутствие автоматического replay.
- [Старый локальный черновик не имеет владельца] -> в real mode не назначать его текущему пользователю и не удалять автоматически; новое пространство ключей по окружению и `user_id`, mock namespace задаётся отдельно.
- [Чтение scopes не объясняет их семантику] -> клиент не вычисляет область; assignments остаются доступны без небезопасного объединения.

## Migration Plan

1. Реализовывать согласованные delta-specs в рамках этого change, сохранить источники контрактов в repo и адресно обновить инструкции о разрешённом auth-этапе. Синхронизация основных specs выполняется штатным отдельным workflow, не ручной заменой во время реализации.
2. Реализовать техническую сессию и защищённый транспорт; покрыть их unit-тестами до подключения UI. Mock credentials не добавлять; выбор fixtures описан отдельным change.
3. Подключить Framework bootstrap, generation cleanup и permission matrix к видимости существующих страниц/действий UI, затем component-тесты прямых URL и негативных сценариев.
4. Выполнить typecheck, lint без warnings, test, format:check, api:check и build. Browser/E2E не запускать и не менять.
5. Перед выпуском получить от владельцев deployment подтверждение доступности общей MPMM-сессии, CORS, refresh rotation между MPMM/ЦАМ, `/me` и server-side permission/object-scope enforcement, включая диалоги. Это отдельный release gate; план и реализация не требуют выдумывать их поведение. Без подтверждения отметить rollout blocked, не маскировать через mock или отключение guard.
6. Развёртывать с подтверждённой конфигурацией real API/auth. Rollback — откат bundle/доступности ЦАМ владельцем deployment; rollback фронта не предоставляет серверных прав. Не добавлять клиентский переключатель обхода auth. MPMM storage и назначения ролей при откате не удаляются.
