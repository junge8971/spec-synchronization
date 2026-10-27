## Context

См. proposal.md. `connection-tab.tsx` выводит поддержанные поля и параметры. Nullable connection сейчас ошибочно объясняется отсутствием поддержки API. Источник wire-схем — `docs/api/contracts/openapi.json`.

## Goals / Non-Goals

**Goals:** отдельная форма connection с переиспользованием mutation навыка.

**Non-Goals:** секрет токена, новые parameter types, переписывание конфигуратора поверхности или общей анкеты.

## Decisions

- Предметная feature формы подключается widget; API PATCH принадлежит entities/skill (переиспользовать MOS-944, если уже применён). Не импортировать форму анкеты из соседней feature.
- Сохранять только expected_version и connection; не пересылать старую анкету. Обработка ошибок/ключа идемпотентности общая с PATCH навыка, dirty connection не затирать фоновым refetch.
- `type` фиксирован как select. `default` допускает string/integer/null по схеме: не превращать integer в строку при round-trip и не использовать truthiness, теряющую 0. `options` и parameters могут отсутствовать; различать отсутствие и пустое значение.
- Параметры отображать по их key/title, а не по специальному kb_section. Не создавать конфигурацию «на будущее» для text/number/boolean типов.
- Documentation использует `/docs?article=skill-params` через существующую навигацию и basename. Auth-shaped поля здесь описывают бизнес-подключение, не сессию посетителя.

## Contract gate

До сохранения полного connection согласовать merge/replace вложенного объекта, очистку null, совместимость auth_required/auth_type, уникальность key, ограничения options и связь default/options (options — строки, default также integer). Не вводить произвольное преобразование default и не считать mock поведение обязательным backend-правилом. При необходимости расширения контракта сначала пересмотреть план, не добавлять поля вручную в generated schema.

## Risks / Trade-offs

- Конкурирующая анкета MOS-944 → expected_version, сохранение draft при конфликте, без blind retry.
- Null connection → понятное «Подключение не настроено» и доступная форма настройки; не показывать ложный unavailable.

## Migration Plan

Дополнить вкладку без миграции данных. Проверить несколько параметров, null и default=0. Откат возвращает read-only отображение, не удаляя серверное connection.
