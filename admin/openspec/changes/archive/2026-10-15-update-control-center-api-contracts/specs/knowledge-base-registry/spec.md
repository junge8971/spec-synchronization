## MODIFIED Requirements

### Requirement: Metadata-driven supported conditions

Конструктор SHALL разделять draft и applied условия, предоставлять И/ИЛИ, добавление/удаление, очистку, Apply, badge количества и читаемую сводку. Для name/code/category_code/status/material_type/language/skill_names/links_count SHALL использоваться только разрешённые metadata операторы и тип поля string/integer/number. Неполное условие SHALL блокировать Apply с ошибкой, а не игнорироваться. Ограничение SHALL составлять 50 условий без вложенных групп. Текстовые eq/ne SHALL сохранять серверную регистрозависимость; in/not_in SHALL использовать непустые наборы кодов. Быстрые фильтры и группа условий SHALL объединяться AND.

links_count SHALL поддерживать eq/ne/gt/gte/lt/lte/between с JSON-числами, включая ноль и дробные пороги. between SHALL принимать ровно две конечные числовые границы в возрастающем порядке или равные, включая обе границы. Строки, boolean, null и нечисловые значения SHALL отклоняться; numeric ne также MUST NOT включать NULL. skill_names SHALL сравнивать строку названий связанных неудалённых навыков: contains без учёта регистра, eq всю строку, is_empty отсутствие таких навыков. Поле MUST NOT подменяться skill_ids.

#### Scenario: Cancel draft conditions

- **WHEN** условия изменены и панель закрыта без Apply
- **THEN** запрос и сводка остаются прежними; повторное открытие редактирует применённый отбор

#### Scenario: Invalid condition

- **WHEN** у in не выбрано значений либо превышено 50 условий
- **THEN** Apply не отправляет запрос, объяснено необходимое исправление

#### Scenario: Numeric boundaries

- **WHEN** пользователь применяет links_count between [0, 2.5] либо [2, 2]
- **THEN** запрос передаёт числа и включает обе границы; обратный диапазон и пустая граница блокируют Apply без преобразования пустоты в ноль

#### Scenario: Skill name in OR group

- **WHEN** skill_names contains «ЖКХ» объединён через OR с links_count gte 1
- **THEN** отправляются оба условия внутри одной группы, без локальной фильтрации страницы или отдельного AND-фильтра skill_ids

### Requirement: Unsupported prototype conditions are disclosed

Поля «Ссылок» и «Навыки» SHALL быть доступны по текущим metadata как links_count и skill_names; старые пояснения об отсутствии API-поддержки SHALL отсутствовать. Неподдержанные поля или сочетания операторов MUST NOT отправляться. UI MUST NOT вычислять условия по странице, подменять числовое сравнение строковым либо заменять текстовое условие по навыкам отдельным AND-фильтром skill_ids внутри OR-группы. Наличие skill_names MUST NOT использоваться для восстановления идентичности навыков разбиением строки по запятым.

#### Scenario: Link count condition

- **WHEN** metadata публикует links_count с числовыми операторами
- **THEN** «Ссылок» доступно, редактор принимает число или диапазон согласно оператору без устаревшего unavailable-пояснения

### Requirement: URL selection round trip

Применённые query, категории, статусы, условия с логикой, сортировка и пагинация SHALL восстанавливаться из URL и при Back/Forward, включая числовые значения и диапазоны без превращения в строки. «Скопировать ссылку на отбор» SHALL копировать полный воспроизводимый отбор под basename. Некорректный или неподдержанный отбор SHALL объясняться без отправки невалидного запроса и без молчаливого применения части условий. Clipboard failure MUST NOT показывать успех.

#### Scenario: Shared OR selection

- **WHEN** другой пользователь открывает скопированную ссылку с двумя OR-условиями и сортировкой
- **THEN** восстанавливаются значения обоих условий и логика, не только их количество

#### Scenario: Supported persisted numeric selection

- **WHEN** URL содержит links_count gt 2 с числовым value и поле доступно в metadata
- **THEN** отбор восстанавливается и выполняется без устаревшего отказа

#### Scenario: Unsupported persisted selection

- **WHEN** URL содержит неизвестное поле, строковое значение числового сравнения либо повреждённый JSON
- **THEN** видна причина неприменимости и действие очистки, неподдержанный запрос не выполняется

## ADDED Requirements

### Requirement: Typed conditions survive saved filters and export

Полный применённый search с links_count и skill_names SHALL одинаково использоваться в поиске, managed saved-filters и CSV экспорте. Сохранение/чтение/применение SHALL сохранять JSON-типы и логику группы; экспорт SHALL выгружать весь отбор, не только страницу. Старые валидные строковые условия SHALL продолжать работать.

#### Scenario: Numeric saved filter exported

- **WHEN** сохранён фильтр с between, затем прочитан, применён и экспортирован на второй странице
- **THEN** границы остаются числами, поиск и CSV имеют один отбор, CSV не ограничен пагинацией
