## Purpose

Перевести существующие экраны Центра управления на HTTP и актуальные API-данные, сохраняя понятные состояния интерфейса и явно обозначая отсутствующую в контрактах функциональность.

## ADDED Requirements

### Requirement: Existing screens consume HTTP data

Реестры навыков и поверхностей, карточка навыка, справочники фильтров и профиль шапки SHALL получать серверные данные через общий HTTP transport. Runtime-клиенты MUST NOT возвращать встроенные fixtures, генерировать дополнения карточки или заменять ошибки локальным успехом. Статические статьи справки, навигация, локализация и test doubles не относятся к runtime mock API.

#### Scenario: Registry request failure

- **WHEN** запрос реестра завершается сетевой ошибкой
- **THEN** пользователь видит error/retry, а не старые встроенные mock-записи

#### Scenario: Detail outside a loaded page

- **WHEN** открыта ссылка на корректный skill UUID, которого нет на загруженной странице списка
- **THEN** выполняется отдельный detail-запрос; карточка не зависит от поиска в текущей или полной локальной выборке

#### Scenario: Missing or malformed detail identifier

- **WHEN** сервер возвращает 404 для detail либо ссылка содержит старый невалидный slug-ID
- **THEN** интерфейс показывает отсутствие/некорректность ресурса без синтетической карточки; прочие HTTP-ошибки не маскируются как 404

### Requirement: Contract-compatible filters and pagination

UI SHALL использовать контрактные ID, фильтры и сортировки: UUID domain_id вместо фиксированного slug domain, limit/offset вместо page/pageSize на wire, SurfaceStatus `review`, SurfaceType `mobile_application`, SurfaceListSort с `-field`. Неподдержанный status-фильтр/сортировка навыков MUST NOT отправляться или вычисляться только по загруженной странице. Устаревшие URL filter/sort values SHALL нормализоваться к поддержанным значениям/defaults.

#### Scenario: Selecting a domain and another page

- **WHEN** пользователь выбирает домен и затем страницу 3 с размером 10
- **THEN** API получает выбранный domain_id, limit 10, offset 20; количество записей и страниц берётся из ответа, а не локального seed

#### Scenario: Domain options exceed one API page

- **WHEN** число доменов превышает размер страницы справочника
- **THEN** пользователь может выбрать домен за пределами первой страницы; варианты не ограничены фиксированным массивом

#### Scenario: Surface filter and sorting

- **WHEN** выбраны «Проверка», «мобильное приложение» и убывание даты изменения
- **THEN** API получает status=review, type=mobile_application и sort=-updated_at

#### Scenario: Legacy URL parameters

- **WHEN** открыта ссылка со старым skill status sort, slug домена или устаревшими surface enum
- **THEN** URL-state нормализуется без отправки неподдержанного значения backend и без скрытой локальной фильтрации

### Requirement: Truthful representation of contract fields

UI SHALL отображать integer version, nullable service_id/channel_id/connection, вложенные domain/team/contact, zones и surface stats согласно DTO. Отсутствующие в контракте статусы/готовность/метрики навыков, ревью, интенты, проверки, история и токены MUST NOT синтезироваться или выдаваться за API-данные. Сохраняемые неподдержанные блоки SHALL показывать явное unavailable-состояние, а соответствующие действия/фильтры SHALL быть недоступны или удалены.

#### Scenario: Missing skill lifecycle API

- **WHEN** открыта карточка с валидным SkillResponse без review, intents, checks, history и tokens
- **THEN** поддерживаемые поля отображаются, а неподдержанные блоки сообщают «Не поддерживается текущим API» без mock review, успешных проверок или фиктивных токенов

#### Scenario: Null versus zero

- **WHEN** dialogs_30d равен null, а у другой поверхности равен 0
- **THEN** первая показывает отсутствие данных, вторая — реальный ноль; nullable connection/service_id не ломают карточку

### Requirement: Current principal in the header

Шапка SHALL отображать имя и роли из `/auth/v1/me`, а не фиксированного администратора. Загрузка, ошибка и отсутствие подтверждённых прав SHALL быть различимы; приложение MUST NOT выдавать ошибку профиля за пользователя с административными правами.

#### Scenario: Principal returned

- **WHEN** `/me` возвращает display_name/full_name, roles и scope
- **THEN** шапка использует эти значения и соответствующие инициалы/подписи без захардкоженного имени и роли

#### Scenario: Principal access denied

- **WHEN** `/me` возвращает 401 или 403
- **THEN** отображается ошибка доступа без fallback на фиктивного администратора

### Requirement: User-visible network states and integration verification

Существующие экраны SHALL различать loading, error с повтором, empty и unavailable. Проверки интеграции SHALL проходить по реальному HTTP-пути браузер → dev proxy/rewrite → mock server, а production build SHALL проверяться независимо от dev-моков.

#### Scenario: Empty data versus failed request

- **WHEN** API возвращает валидный пустой список либо завершается ошибкой
- **THEN** первый случай показывает empty, второй — error/retry; повтор ошибки действительно выполняет новый HTTP-запрос

#### Scenario: Browser smoke test

- **WHEN** E2E открывает навыки, карточку, поверхности и шапку через `yarn dev`
- **THEN** наблюдаются запросы по `/api/control/api`, отображаются ответы mock server и проходят проверки фильтрации, сортировки, пагинации и detail без импортов runtime fixtures в приложение
