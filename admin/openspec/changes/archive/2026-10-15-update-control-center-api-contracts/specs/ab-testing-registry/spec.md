## MODIFIED Requirements

### Requirement: Supported condition builder

Конструктор SHALL иметь draft/applied состояния, И/ИЛИ, добавление/удаление, очистку, Apply, badge и читаемую сводку. Поля name/code/owner/status/launch_mode/audience_code/metric_code/groups_count SHALL работать только с допустимыми metadata операторами и типами string/integer/number. Не более 50 условий, без вложенных групп. Неполные условия и пустые in/not_in SHALL блокировать Apply. Быстрые фильтры и query SHALL объединяться с группой условий через И; текстовые eq/ne SHALL сохранять серверную регистрозависимость.

groups_count SHALL поддерживать eq/ne/gt/gte/lt/lte/between с JSON-числами, включая ноль и дробные пороги. between SHALL принимать ровно две конечные границы с нижней не больше верхней, включая обе границы. Строки, boolean, null и нечисловые значения SHALL отклоняться; все numeric сравнения, включая ne, MUST NOT включать NULL. Новые условия SHALL работать до пагинации на сервере, не вычисляться по странице.

#### Scenario: Cancel condition draft

- **WHEN** условия изменены и закрыты без Apply
- **THEN** запрос и сводка не меняются, повторное открытие использует применённые условия

#### Scenario: Invalid enum selection

- **WHEN** in не содержит выбранных кодов
- **THEN** Apply объясняет ошибку и не отправляет запрос, условие не исчезает молча

#### Scenario: Group count range

- **WHEN** groups_count between [2, 4] объединён через OR с условием статуса
- **THEN** запрос сохраняет группу и числовой диапазон; [4, 2], строковые границы и неполный диапазон отклоняются

### Requirement: Unsupported conditions remain explicit

Приоритет и поверхности внутри конструктора SHALL оставаться недоступными пунктами с пояснением отсутствия API-поддержки. Количество групп SHALL стать доступным groups_count при наличии metadata; старое пояснение недоступности SHALL удаляться. UI MUST NOT вычислять условия по загруженной странице, заменять числовое сравнение строковым или переносить поверхность из ИЛИ-группы в отдельный AND-фильтр.

#### Scenario: Surface OR condition

- **WHEN** пользователь открывает поле «Поверхности» в конструкторе
- **THEN** оно недоступно с пояснением; наличие быстрого фильтра не объявляется эквивалентной поддержкой OR-условия

#### Scenario: Published group count

- **WHEN** metadata публикует groups_count с type=integer
- **THEN** количество групп доступно с разрешёнными числовыми операторами, без включения неподдержанного priority

### Requirement: URL round trip

Query, быстрые фильтры, полные условия с логикой, сортировка и пагинация SHALL восстанавливаться из URL и Back/Forward, включая числовые значения и диапазоны без преобразования в строки. Копирование SHALL включать весь применённый отбор под basename. Невалидный/неподдержанный URL SHALL объясняться с возможностью очистки, без молчаливого применения части отбора. Clipboard failure MUST NOT сообщать успех.

#### Scenario: Shared selection

- **WHEN** открыта ссылка с двумя OR-условиями, сортировкой и пагинацией
- **THEN** восстановлены все значения и логика, а не только их количество

#### Scenario: Supported persisted numeric condition

- **WHEN** URL содержит groups_count gt 2 с числовым value и поле доступно в metadata
- **THEN** отбор восстанавливается и отправляется серверу

#### Scenario: Unsupported persisted condition

- **WHEN** URL содержит priority gt 2, строковое значение groups_count либо повреждённый JSON
- **THEN** неподдержанный запрос не выполняется, показаны причина и действие очистки

## ADDED Requirements

### Requirement: Typed group conditions survive saved filters and export

Полный применённый search с groups_count SHALL одинаково использоваться в поиске, managed saved-filters и CSV. Сохранение/чтение/применение SHALL сохранять JSON-типы, логику и сортировку. CSV SHALL выгружать весь отбор независимо от пагинации. Старые валидные строковые условия SHALL сохранять поведение.

#### Scenario: Saved range across pagination

- **WHEN** фильтр с числовым диапазоном сохранён, восстановлен и экспортирован со второй страницы
- **THEN** запросы сохраняют числа и одинаковую семантику отбора, экспорт не ограничивается загруженной страницей
