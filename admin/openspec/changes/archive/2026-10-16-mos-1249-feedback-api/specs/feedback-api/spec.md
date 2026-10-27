## Purpose

Подключить API опросников, справочных значений и метаданных в разделе обратной связи ЦАМ по опубликованному API, с отдельной приёмкой и сохранением ограничений первого этапа.

## ADDED Requirements

### Requirement: Contract aligned feedback operations

Раздел SHALL использовать `/api/control/api/v1/managed-resources`: CRUD `/feedback/surveys`, POST `/feedback/surveys/search`, lookup `/catalogs/lookups/feedback`, metadata `/feedback/metadata`; клиенты saved-filters и CSV добавляются отдельными changes на том же transport. JSON-ответы SHALL проверяться с сохранением HTTP status, code, message и всех errors, включая вложенные JSON Pointer. После создания SHALL выполняться GET по data.id; PUT SHALL возвращать новый baseline полной карточки. Системные поля, sort_order, FK и локальные ключи MUST NOT отправляться. Чтение SHALL поддерживать отмену; мутации MUST NOT автоматически повторяться.

#### Scenario: Created survey receives server identifiers

- **WHEN** POST опросника вернул 201 и data.id
- **THEN** отдельный GET получает сохранённую карточку и ID её вопросов/вариантов; повторный POST ради получения detail не выполняется

#### Scenario: Validation and inactive references

- **WHEN** сохранение вернуло 409 NOT_UNIQUE/REFERENCE_NOT_FOUND/REFERENCE_INACTIVE либо 422 с несколькими вложенными ошибками
- **THEN** клиент сохраняет status/code/message и все JSON Pointer для потребителя; ошибочный ответ не превращается в успех, а отображение и сохранение draft проверяются в MOS-1251/MOS-1254

#### Scenario: Object and form validation errors

- **WHEN** сервер возвращает 422 с ошибкой объекта или формы вместо точного пути поля
- **THEN** клиент сохраняет исходные status/code/message/errors без выдуманного leaf-пути; точные пути конфликтов ссылок и уникальности по опубликованному контракту по-прежнему сохраняются

#### Scenario: Unknown mutation outcome

- **WHEN** ответ мутации потерян или устарел относительно текущей сессии
- **THEN** UI не объявляет гарантированный успех/отмену и не повторяет мутацию автоматически; актуальное состояние можно перечитать явным действием

### Requirement: Removable feedback module boundary

Весь раздел SHALL принадлежать `app/optional/feedback`, включая API, runtime-схемы, модель, типы, константы и тесты. Модуль SHALL использовать shared и публичные API entities; внешние потребители SHALL обращаться через публичный `index.ts`. Зависимости от application/FSD UI-слоёв/других optional-модулей и обратные зависимости нижних FSD-слоёв SHALL отклоняться архитектурной проверкой. Точки подключения и удаления SHALL быть документированы; MOS-1249 MUST NOT подключать UI, saved-filters или CSV-клиенты.

#### Scenario: Import boundary is enforced

- **WHEN** application использует публичный API feedback, а внутренний код импортирует собственный модуль напрямую
- **THEN** архитектурная проверка разрешает импорты и отклоняет private imports, type-only/re-export обходы и зависимости между optional-модулями

### Requirement: Existing transport and session protection

Клиенты SHALL переиспользовать общий transport, обработку ошибок и существующие session owner/generation механизмы. Поставка MUST NOT добавлять UI-policy, mappings permissions, auth/session/RBAC или новые ограничения интерфейса по пользователю. Существующие защитные механизмы SHALL сохраняться; backend SHALL проверять глобальный scope.

#### Scenario: Server denial and stale response

- **WHEN** сервер вернул 403 либо ответ относится к устаревшей сессии
- **THEN** ошибка остаётся различимой, поздний ответ не публикуется в cache и запрос не повторяется автоматически

### Requirement: Contract feedback mock operations

Существующий Express SHALL обслуживать feedback CRUD/search/lookup/metadata с runtime- и бизнес-валидацией и штатным envelope без credentials/role enforcement. Специализированные handlers SHALL использовать существующие механизмы вместо generic feedback CRUD. Fixed-error/session-demo SHALL сохраняться; CSV/saved-filters и другие разделы MUST NOT расширяться этой поставкой. Моки MUST NOT попадать в production.

#### Scenario: Survey round trip and invalid reference

- **WHEN** создаётся валидный опросник и затем обновляется через PUT либо передаётся неизвестная/неактивная ссылка
- **THEN** локальный HTTP возвращает серверные ID/полную карточку либо соответствующий конфликт с JSON Pointer; невалидная операция не меняет сохранённые данные

### Requirement: Evidence and accepted environment limitations

Приёмка SHALL сохранять фактические результаты стенда и явно отделять успешные сценарии, известные проблемы и непроверенные ограничения. Закрытие MOS-1249 с принятыми пользователем исключениями MUST NOT объявлять неуспешные или невыполненные проверки успешными и MUST NOT менять бизнес-валидацию, обработку ошибок, session protection или запрет replay.

#### Scenario: Closure with documented known issues

- **WHEN** пользователь после отчёта контура Т от 15.10.2026 (run `mos1249_1792078927540_77d6ebe5`, 117 HTTP-запросов, 28 PASS / 7 FAIL / 1 SKIP / 2 OWNER) явно поручает зафиксировать известную проблему и закрыть задачу
- **THEN** задача 2.3 завершается как согласованная приёмка с исключениями: два GET 503 после отклонённых PUT оставляют атомарность этих двух сценариев неподтверждённой; пять несовпадений leaf-путей ручного скрипта не считаются доказанными дефектами API; неактивная ссылка, ограниченная глобальная область и обновление MPMM-сессии остаются непроверенными и явно описанными в design
