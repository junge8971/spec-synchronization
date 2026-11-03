## ADDED Requirements

### Requirement: System-state optional ownership exception

В дополнение к действующим адресным FSD-исключениям предметный код system-state SHALL размещаться в `app/optional/system-state/`, а серверные моки — в `mocks/system-state/` ради независимого удаления. Application composition SHALL подключать публичный API модуля, framework-конфигурация — штатные route entrypoints. Модуль SHALL зависеть только от собственного кода, shared и публичных API entities, а не от application internals или чужих pages/widgets/features. Shared, другие бизнес-слайсы и optional-модули MUST NOT импортировать system-state; system-state MUST NOT импортировать другие optional-модули. Ограничения SHALL применяться к алиасам, relative/type-only импортам и re-export.

Правила проекта, lint и исполняемые архитектурные проверки SHALL согласованно фиксировать только это адресное исключение, не отключая существующие проверки деклараций, компонентов и границ. Удаление модуля и документированных точек подключения MUST NOT требовать изменений предметного кода других разделов или удаления общих DTO.

#### Scenario: Allowed optional dependency

- **WHEN** system-state импортирует shared либо публичный API entities, а приложение подключает его публичный descriptor
- **THEN** архитектурная проверка разрешает эти зависимости и продолжает проверять размещение деклараций и компонентов

#### Scenario: Cross-module dependency

- **WHEN** база знаний импортирует system-state или system-state импортирует внутренний код другого optional-модуля, в том числе type-only или через re-export
- **THEN** архитектурная проверка отклоняет зависимость

#### Scenario: Remove the optional module

- **WHEN** удалены папки system-state и документированные точки регистрации
- **THEN** остальные разделы и общие контракты остаются сборочными без зависимости от удалённого бизнес-кода
