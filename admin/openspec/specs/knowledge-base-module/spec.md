# Knowledge Base Module Specification

## Purpose

Обеспечить подключение базы знаний к Центру управления без дополнительной конфигурации, сохраняя изоляцию для удаления и честное отображение ограничений API.

## Requirements

### Requirement: Default section inclusion

Раздел SHALL регистрироваться при обычном запуске, typegen и сборке без отдельного флага. Маршруты и меню SHALL использовать общий application-level реестр независимо от mock/real режима. Существующие ограничения session/access SHALL сохраняться. Production SHALL содержать маршруты и runtime-модули KB, но MUST NOT содержать mock handlers или fixtures. Общие DTO и существующие упоминания базы знаний в других разделах SHALL сохраняться.

#### Scenario: Default build

- **WHEN** приложение собрано обычной командой без настроек включения KB
- **THEN** три маршрута KB присутствуют в route manifest и выходном графе, раздел доступен через меню и прямые ссылки после разрешённого доступа

#### Scenario: Either API mode

- **WHEN** выбран mock либо real режим
- **THEN** раздел зарегистрирован и использует существующий соответствующий API/session режим, без принудительного включения моков

### Requirement: Removable module ownership

Новый предметный код KB SHALL принадлежать отдельной папке `app/optional/knowledge-base/`, server-only fixtures/handlers — `mocks/knowledge-base/`. Внешние подключения SHALL быть минимальны и перечислены в инструкции удаления. Другие бизнес-разделы MUST NOT зависеть от KB; удаление её регистрации MUST NOT нарушать существующие разделы. Проверки границ SHALL сохраняться согласно code-quality-gates.

#### Scenario: Remove the optional section

- **WHEN** удалены KB-папки и документированные точки регистрации
- **THEN** существующие разделы собираются без исправлений их предметного кода, общие контракты не удаляются

### Requirement: Shell integration and deep links

KB SHALL предоставлять `/knowledge-base`, `/knowledge-base/new`, `/knowledge-base/:entryId` под basename `/tsam-panel/`, пункт «База знаний» в группе «Контент», согласованные крошки и подсветку вложенных маршрутов. Карточка SHALL восстанавливать вкладку main/links/skills/rules из tab; неизвестная вкладка выбирает main. Существующая session/access boundary и консервативная политика непокрытых операций SHALL сохраняться без новых permissions.

#### Scenario: Direct card link

- **WHEN** разрешён прямой вход на карточку с tab=links, которой нет на загруженной странице списка
- **THEN** отдельный запрос загружает карточку, открыты «Материалы», крошки ведут в реестр и sidebar подсвечивает KB

#### Scenario: Creation and missing access

- **WHEN** открыт new либо существующий запрещённый маршрут KB
- **THEN** new не используется как entity ID; запрещённый экран не запускает бизнес-загрузки и использует существующее состояние отказа

### Requirement: Unsupported features remain visible and truthful

Функциональный состав прототипа/PDF SHALL сохраняться. Неподдержанные API-функции SHALL оставаться видимыми с недоступным действием и постоянным пояснением непосредственно рядом, доступным без hover и программно связанным с контролом. UI MUST NOT выдавать локальную имитацию за сохранение/экспорт, заменять архив отключением или удалением, исполнять неподтверждённые запросы. Ошибка сети SHALL отличаться от отсутствия API-функции.

#### Scenario: Archive unavailable

- **WHEN** пользователь видит «В архив» или архивный вариант фильтра при текущем контракте
- **THEN** действие/новый выбор недоступны, рядом указано отсутствие поддержки статуса «Архив»; disabled и DELETE не отправляются вместо archived

#### Scenario: Supported endpoint fails

- **WHEN** поддержанный запрос вернул 500
- **THEN** показана ошибка с возможностью безопасного повтора чтения, а не label «API не реализовано» или фиктивные данные

### Requirement: Accessible states without fabricated data

Раздел SHALL различать loading, empty, no matches, invalid response, 403, 404 и retryable error, сохранять клавиатурную доступность таблицы, вкладок, форм и modal focus. Данные SHALL отображаться как текст. Runtime browser fixtures MUST NOT подменять API. Ошибки и поздние ответы SHALL соблюдать существующую session-owner границу.

#### Scenario: Empty result versus error

- **WHEN** поиск возвращает пустой валидный отбор либо сетевую ошибку
- **THEN** первый случай предлагает изменить фильтры/создать запись по контексту, второй показывает ошибку и повтор без фиктивных строк
