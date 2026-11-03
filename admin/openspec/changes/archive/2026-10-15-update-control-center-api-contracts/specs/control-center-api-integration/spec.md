## ADDED Requirements

### Requirement: Current API is the authoritative contract snapshot

Контракты SHALL фиксировать воспроизводимый снимок текущего `/api/control/openapi.json`, URL источника, дату получения, SHA-256 исходных байтов и перечень всех структурных изменений. Live-пути, DTO и описания операций SHALL иметь приоритет над устаревшими локальными соглашениями и переданным CRUD Markdown. Описанные бизнес-ограничения SHALL сохраняться, даже если JSON-схема не выражает их полностью. Противоречия SHALL быть явно перечислены; неподтверждённая доступность операций MUST NOT объявляться проверенной интеграцией. Принятая нормализация обязательной пары AdminToken/AccessToken SHALL сохраняться по явному требованию обоих заголовков в описании live API.

Aggregate, самостоятельные разделы с замыканием ссылок и generated DTO SHALL соответствовать одному снимку. Проверки и генерация SHALL работать без сети, Downloads и соседнего checkout. Новые операции SHALL иметь явное mock-покрытие, старые handlers MUST NOT теряться при смене operationId. Исторические исключения SHALL удаляться, когда их заменяет опубликованный контракт, без потери защитных проверок.

#### Scenario: Full snapshot migration

- **WHEN** импортирован live-снимок с поверхностями, API registry, response templates, числовыми условиями и экспортами диалогов
- **THEN** все изменения отражены в aggregate/splits/types, consumers и документации; расхождение любого split или неразрешённая ссылка обнаруживается проверкой

#### Scenario: Conflicting saved-filter documentation

- **WHEN** live enum содержит api-endpoints и response-templates, а Markdown запрещает эти ресурсы
- **THEN** локальный контракт и моки принимают live enum и валидируют search по соответствующему ресурсу; расхождение и отсутствие проверки реального deployment явно задокументированы

#### Scenario: Business rule is absent from JSON Schema

- **WHEN** формальная схема экспорта допускает оба поля состава, а описание требует ровно одно
- **THEN** клиент и моки сохраняют бизнес-валидацию, не ослабляя её ради формального совпадения DTO

#### Scenario: Unspecified server error

- **WHEN** источник сообщает код DOMAIN_ALREADY_IN_USE без точного HTTP status и тела ошибки
- **THEN** отсутствие wire-примера фиксируется отдельно; mock convention не записывается в OpenAPI как доказанное поведение backend
