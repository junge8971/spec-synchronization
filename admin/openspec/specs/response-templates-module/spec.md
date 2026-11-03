# response-templates-module Specification

## Purpose

Предоставить раздел управления шаблонами ответов в общей оболочке с независимым удалением, сохранением API-границ и честными состояниями интерфейса.

## Requirements

### Requirement: Default registration and direct navigation

Раздел SHALL подключаться без отдельного feature flag в mock и real режимах. Реестр `/response-templates`, создание `/response-templates/new` и карточка `/response-templates/:templateId` SHALL работать под действующим basename; пункт «Шаблоны ответов» SHALL находиться в группе «Контент», крошки и активный пункт меню SHALL соответствовать маршруту. Карточка SHALL загружаться отдельно от списка. Вкладки main/links SHALL восстанавливаться из URL; неизвестная вкладка SHALL открывать «Основное».

#### Scenario: Direct card link

- **WHEN** пользователь открывает разрешённую прямую ссылку карточки с `tab=links`, отсутствующей на текущей странице реестра
- **THEN** карточка загружается по ID, открываются «Связи», крошки ведут в реестр, пункт меню подсвечен

#### Scenario: Creation route

- **WHEN** пользователь открывает `/response-templates/new`
- **THEN** открывается форма создания и строка new не передаётся как ID API

### Requirement: Independently removable ownership

Предметный frontend SHALL принадлежать `app/optional/response-templates/`, предметные mock fixtures/validation/handlers SHALL принадлежать `mocks/response-templates/`. Раздел SHALL иметь минимальные документированные точки регистрации, включая оставшиеся shared mock composition points. Удаление модуля и этих точек SHALL сохранять сборку и работу других разделов без изменения их предметного кода. Общие DTO, HTTP-инфраструктура и общие lookup/saved-filter контракты SHALL сохраняться. Production SHALL включать раздел, но MUST NOT включать серверные моки или демонстрационные fixtures.

#### Scenario: Removal rehearsal

- **WHEN** в отдельной временной копии удалены обе папки и документированные подключения
- **THEN** typecheck и сборка оставшегося приложения проходят, остальные моки запускаются, общие контракты не удалены

### Requirement: Existing access boundary and truthful states

Раздел SHALL использовать существующие session/access и HTTP-механизмы без новых permissions или ролевых правил. UI SHALL различать загрузку, пустой реестр, отсутствие совпадений, 403, 404, некорректный ответ и повторяемую сетевую ошибку. Данные SHALL отображаться безопасно как текст; таблица, вкладки, выборы и диалоги SHALL быть доступны с клавиатуры и иметь доступные имена, состояние выбора и управление фокусом. Поздние ответы после смены запроса/карточки/session owner MUST NOT заменять актуальные данные. Новые вызовы MUST NOT выполняться за существующей запрещающей access boundary.

#### Scenario: Failure is not an empty registry

- **WHEN** загрузка списка возвращает ошибку вместо валидного пустого результата
- **THEN** UI показывает ошибку и безопасный повтор, не демонстрационные записи и не «Шаблонов пока нет»

#### Scenario: Accessible verification

- **WHEN** локальные browser-проверки разрешены и доступны
- **THEN** Playwright MCP проверяет переходы, клавиатуру, фокус и существенные error states на моках; результат документируется отдельно от unit/component и реальной интеграции

#### Scenario: Browser verification unavailable

- **WHEN** разрешение или инструменты browser-проверки отсутствуют
- **THEN** проверка явно остаётся незавершённой, просмотр прототипа и пройденные unit-тесты не выдаются за её выполнение
