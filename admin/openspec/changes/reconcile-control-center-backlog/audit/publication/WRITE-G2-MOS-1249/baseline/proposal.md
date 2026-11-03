## Why

[Jira MOS-1249](https://task.mos-team.ru/browse/MOS-1249): [FE][Обратная связь] Подключить API опросников, справочных значений и метаданных.

Нужна отдельная реализуемая поставка этой FE-подзадачи по обновлённому API и принятой границе прототипа. План, приёмка и выполнение учитываются отдельно от остальных задач MOS-1246.

## What Changes

- Типизированные CRUD, поиск, lookup и metadata; contract/typegen, общая UI-policy и контрактные моки. Клиенты saved-filters и CSV реализуются соответственно в MOS-1259 и MOS-1260.
- Сохранить ограничения API, ввод при ошибках, доступность и действующую безопасность.

### Deferred scope

UI реестра/карточки и самостоятельные клиенты saved-filters/CSV принадлежат соседним задачам; общий CRUD справочников и база знаний не подключаются.

## Capabilities

### New Capabilities

- `feedback-api`: Типизированные CRUD, поиск, lookup и metadata; contract/typegen, общая UI-policy и контрактные моки. Клиенты saved-filters и CSV реализуются соответственно в MOS-1259 и MOS-1260.

### Modified Capabilities

Нет. Общие capabilities HTTP, permissions и MPMM сохраняются; scope соседних FE-подзадач сюда не переносится.

## Impact

entities/feedback, aggregate OpenAPI, generated DTO, UI policy и Express-моки.

Зависимости: Существующие HTTP/session механизмы проекта; переданные API-контракты.

Граница: UI по прототипу, операции по API, неподдержанное отложено. Исполнение правил и сбор реальных ответов пользователей не входят. Новые зависимости не требуются без отдельного обоснования. Это planning change: код приложения и Jira при разделении не меняются.
