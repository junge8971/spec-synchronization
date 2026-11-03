## ADDED Requirements

### Requirement: API registry optional ownership exception

В дополнение к действующим адресным FSD-исключениям предметный код API registry SHALL размещаться в `app/optional/api-registry/`, а серверные моки — в `mocks/api-registry/` ради независимого удаления. Application composition SHALL подключать публичный API модуля, framework-конфигурация — штатные route entrypoints. Модуль SHALL зависеть только от собственного кода, shared и публичных API entities, а не от application internals или чужих pages/widgets/features. Shared, другие бизнес-слайсы и optional-модули MUST NOT импортировать API registry; API registry MUST NOT импортировать другие optional-модули. Ограничения SHALL применяться к алиасам, relative/type-only импортам и re-export.

Правила проекта, lint и исполняемые архитектурные проверки SHALL согласованно фиксировать только это адресное исключение, не отключая существующие проверки деклараций, компонентов и границ. Удаление модуля и документированных точек подключения MUST NOT требовать изменений предметного кода других разделов или удаления общих DTO.

#### Scenario: Allowed optional dependency

- **WHEN** API registry импортирует shared либо публичный API entities, а приложение подключает публичный descriptor
- **THEN** архитектурная проверка разрешает эти зависимости и продолжает проверять размещение деклараций и компонентов

#### Scenario: Cross-module dependency

- **WHEN** API registry импортирует базу знаний или другой optional-модуль импортирует API registry, в том числе через relative/type-only импорт или re-export
- **THEN** архитектурная проверка отклоняет зависимость, даже через публичный index.ts

#### Scenario: Remove the optional module

- **WHEN** папки API registry и документированные точки регистрации удалены в отдельной копии
- **THEN** остальные разделы и общие контракты остаются сборочными без зависимости от удалённого бизнес-кода
