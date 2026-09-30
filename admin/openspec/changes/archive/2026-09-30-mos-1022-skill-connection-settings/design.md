## Context

См. proposal.md. `connection-tab.tsx` выводит поддержанные поля и параметры. Nullable connection сейчас ошибочно объясняется отсутствием поддержки API. Источник wire-схем — `docs/api/contracts/openapi.json`.

## Goals / Non-Goals

**Goals:** отдельная форма connection с переиспользованием mutation навыка.

**Non-Goals:** секрет токена, новые parameter types, переписывание конфигуратора поверхности или общей анкеты.

## Decisions

- Предметная feature формы подключается widget; API PATCH принадлежит entities/skill (переиспользовать MOS-944, если уже применён). Не импортировать форму анкеты из соседней feature.
- Пользователь подтвердил: PATCH заменяет объект `connection` целиком, без merge вложенных полей. Для изменения endpoint форма отправляет полный connection с остальными сохранёнными полями и параметрами, а не только `{ endpoint }`. Удаление всего подключения через `connection: null` не реализуется.
- Сохранять только expected_version и connection; не пересылать старую анкету. Обработка ошибок/ключа идемпотентности общая с PATCH навыка, dirty connection не затирать фоновым refetch.
- `type` фиксирован как select. `default` допускает string/integer/null по схеме: не превращать integer в строку при round-trip и не использовать truthiness, теряющую 0. `options` и parameters могут отсутствовать; различать отсутствие и пустое значение.
- Параметры отображать по их key/title, а не по специальному kb_section. Не создавать конфигурацию «на будущее» для text/number/boolean типов.
- Documentation использует `/docs?article=skill-params` через существующую навигацию и basename. Auth-shaped поля здесь описывают бизнес-подключение, не сессию посетителя.

## Contract gate

Пользователь согласовал полную замену `connection` и проверку на frontend только типов по OpenAPI. Бизнес-ограничения совместимости auth_required/auth_type, уникальности key, содержимого options и связи default/options проверяет backend. Его ошибки отображаются без потери черновика. Contract gate для сохранения объекта снят; удаление всего подключения через `connection: null` не добавляется.

- Не вводить regex/непустоту/уникальность key, URL-ограничение endpoint или проверку вхождения default в options, отсутствующие в OpenAPI. Например, `default: 0` с `options: ["0"]` отправляется без преобразования default; решение о допустимости принимает backend.
- Сохранять отсутствие optional полей при неизменённом вводе, отличать `options: []` от отсутствующего options, `default: null` от отсутствующего default и `default: "0"` от `default: 0`. Для integer проверять точность представления JavaScript; дробь и выход за safe integer не отправлять.
- Пустой текст после редактирования endpoint/contract_version передаётся как строка `""`; неизменённые null/отсутствие сохраняются. Выбор «Не указан» вместо transport_token задаёт nullable auth_type в null. auth_required не меняет auth_type автоматически.
- Удаление последнего существующего параметра/варианта отправляет пустой массив в полном connection. Пример: `{ expected_version: 2, connection: { auth_required: false, parameters: [] } }` заменяет настройку без пересылки анкеты.
- Не считать mock поведение обязательным backend-правилом и не добавлять поля вручную в generated schema.

## Risks / Trade-offs

- Конкурирующая анкета MOS-944 → expected_version, сохранение draft при конфликте, без blind retry.
- Null connection → понятное «Подключение не настроено» и доступная форма настройки; не показывать ложный unavailable.

## Migration Plan

Дополнить вкладку без миграции данных. Проверить несколько параметров, null и default=0. Откат возвращает read-only отображение, не удаляя серверное connection.
