## Context

См. proposal.md. Существующий Express обслуживает бизнес-fixtures через Vite proxy. Частично добавлены `/me`, каталог профилей и dev config; demo bootstrap и controls ещё не завершены. Ранее запланированные TanStack Devtools и live-switch отменены пользователем. Новая модель permissions — представление UI; backend отвечает за авторизацию каждой операции.

## Goals / Non-Goals

**Goals:** выбрать профиль и фиксированный ответ операции, увидеть соответствующий UI, проверить обработку backend-ошибки без отдельного mock framework.

**Non-Goals:** Devtools platform, MSW, JWT/OIDC/refresh simulation, role editor, object scopes, request ACL, полноценная смена пользователя без reload, успешные заглушки отсутствующих API и закрытие gate реальной интеграции (Т — текущая площадка).

## Decisions

### 1. Существующий локальный запуск

`yarn dev` включает demo через вычисленный Vite `mocksEnabled`. После production build приложение должно использовать реальный API и сессию, даже с CONTROL_API_MOCKS=true. Сама сборка не запрашивает API и не читает пользовательскую сессию; start/preview обслуживают её артефакты без изменения режима. Текущий start с server bundle при ssr:false ещё требует исправления; это требование плана, не подтверждение рабочего запуска. `CONTROL_API_MOCKS=false` в dev выбирает реальный настроенный API/auth; отсутствие обязательной конфигурации даёт явную ошибку, не legacy/full access. Hostname не выбирает режим авторизации; Т — текущий backend deployment. Mock listener остаётся на loopback как локальный инструмент разработки. Внешний API override при mocks — ошибка конфигурации. Demo запросы идут на same-origin `/api/control/api/`, без credentials и внешних redirects. URL/storage не включают режим. Standalone createMockApp сохраняет sessionDemo=false по умолчанию. Отдельный флаг и новый сервер не нужны.

### 2. Серверные fixtures principal

Сохранить `GET /api/auth/v1/me` и `GET /api/__demo/session/profiles` на Express, доступные через прежний proxy. `/me` использует `X-Control-Demo-Profile` только для выбора fixture: default viewer, неизвестный ID — 400. Каталог возвращает ID/label. Envelope и principal соответствуют текущему контракту; dev endpoints не добавляются в production OpenAPI. Профиль не хранится глобально на сервере и не передаётся как credential бизнес-операциям.

| ID     | Подпись             | Permissions                                                      |
| ------ | ------------------- | ---------------------------------------------------------------- |
| none   | Демо: без прав      | пустой массив                                                    |
| viewer | Демо: просмотр      | Domain, Skill, Surface, Team, Module, Analytics — только `:view` |
| editor | Демо: редактор      | viewer + Domain/Skill/Surface `:create` и `:update`              |
| full   | Демо: полный доступ | явный `*`                                                        |

Каждый fixture имеет отдельный устойчивый user_id, синтетические имя/email на example.test, демонстрационную роль и пустые assignments. Роли ничего не разрешают; editor не получает status/lifecycle, team mutations или analytics configure/refresh. Наборы не объявляются production-ролями.

### 3. Presentation-policy и bootstrap

Demo загружает `/me` без MPMM token storage, refresh и redirects. Проверка principal и UI используют существующий session public API и общую presentation-policy. Она определяет видимость меню, вкладок, кнопок и содержимого прямого URL; disabled сохраняется только для бизнес-условий или pending-состояния. Непоказанная страница не монтирует свои data hooks. Это следствие композиции UI, не запрет запроса по URL/method.

Transport и mutation handlers не вычисляют разрешения из роли или permissions; у mock server нет RBAC. Существующие бизнес-валидация, состояние сессии, защита от результатов прежней настоящей сессии и обработка серверных ошибок сохраняются. 403 показывается как отказ backend и не ведёт к replay или расширению UI permissions. Проверка fixture не доказывает backend scopes/CORS/refresh rotation.

### 4. Смена профиля через reload

Панель сохраняет только выбранный ID в отдельном sessionStorage namespace вкладки, затем вызывает полную перезагрузку документа. Новый документ заново подтверждает `/me`; старые React state/cache/callbacks не переносятся. Переключатель блокируется после начала reload. Не добавлять demo generation machinery и живое A→B→A переключение. Уже отправленная серверу операция может завершиться: reload не отменяет серверный результат и не сбрасывает seed.

Если запись sessionStorage недоступна, показать ошибку и сохранить текущий профиль без ложного переключения. Default viewer остаётся доступен при отсутствии сохранённого выбора; неизвестный сохранённый ID даёт ошибку `/me` и доступный выбор известного профиля. Demo-черновики отделены по режиму, окружению и подтверждённому user_id. Не читать/присваивать/удалять legacy, MPMM и чужие записи; до principal черновик не читается. Повторная загрузка того же профиля восстанавливает только его сохранённый черновик; незаписанный ввод при reload теряется, о reload сообщает панель. Повторы мутаций только явные, неопределённый результат не объявляется отменой.

### 5. Обычная локальная панель и header

Небольшая панель «Моки» на установленном UI kit монтируется application layer вне session/page presentation boundary. Она доступна на desktop/mobile, при none, недоступной странице и ошибке bootstrap. Каталоги загружаются независимо от `/me`; loading/error/retry не выдумывают варианты. Dev-only dynamic import и Vite gating исключают controls и fixtures из production. Отдельные Devtools plugins и зависимости не добавляются.

Header получает только подтверждённый principal через session public API: ФИО, email, roles. Пустое имя заменяется email, пустые роли — «Роли не назначены». Строки — текст; токены и assignments не выводятся. При checking/error старые данные скрыты. Mock controls и маркировка «Локальное демо» находятся в панели, не в header. Сохранить accessibility, keyboard/focus и мобильную навигацию; без logout и редактора ролей.

### 6. Минимальный выбор HTTP-ответа

Использовать существующие OpenAPI method/path templates и handlers для dev-only каталога операций. Для каждой операции выбирать штатный handler, фиксированный HTTP 403, HTTP 500 либо задержку 1500 мс перед штатным handler. Штатный ответ может быть существующим unavailable: отсутствующий API не становится успешным. `/me` и binary поддерживаются; management-каталоги не подчиняются выбранным сценариям.

Выбор хранится по method/path template в sessionStorage вкладки; query не влияет. Узкая dev-only добавка к общему JSON/binary запросу передаёт несекретный scenario header только локальному mock API. Она выбирает ответ, не проверяет permissions. Неизвестный сценарий — 400; вне demo header игнорируется и каталоги недоступны. Сервер не хранит общий выбор посетителя.

Сценарий применяется после контрактной валидации и до handler/idempotency. 403/500 не меняют state, не выводятся из профиля и возвращают фиксированное error envelope. Задержка сохраняет бизнес-проверки; обнаруженная отмена до handler предотвращает его запуск. Сброс меняет только будущие запросы, без seed reset, refetch и replay. При недоступном storage сценарий может оставаться в памяти текущего документа с предупреждением; профиль так переключать нельзя из-за обязательного reload. Произвольный JSON-редактор, универсальная сценарная платформа и новый mock framework не нужны.

## Risks / Trade-offs

- [Demo попадает в production] → local-only server, Vite gating, проверка build с CONTROL_API_MOCKS=true.
- [Reload теряет несохранённый ввод] → явная подпись рядом с выбором, owner-scoped сохранённые demo drafts.
- [Mock 403 принимают за RBAC] → независимый фиксированный сценарий; business handlers не проверяют роль.
- [None/ошибка блокируют recovery] → панель и каталоги вне business boundary.
- [Изменение backend data во время reload] → не обещать отмену уже отправленной операции, не выполнять автоматические повторы.

## Migration Plan

1. Согласовать существующие частичные demo-модули с новым планом; не отмечать незавершённую реализацию готовой.
2. Завершить fixtures/bootstrap и UI-only policy поверх уточнённого auth-change, без request ACL.
3. Добавить простые controls, reload, owner-scoped drafts и фиксированные response scenarios.
4. Обновить docs и unit/component/HTTP/config tests, выполнить quality/build gates без browser/E2E.
5. Opt-out: CONTROL_API_MOCKS=false yarn dev выбирает настроенные real API/auth; неполная конфигурация даёт ошибку. Не удалять чужие drafts/MPMM token. Синхронизация specs: auth → demo; gate реальной интеграции (Т — текущая площадка) не закрывать.
