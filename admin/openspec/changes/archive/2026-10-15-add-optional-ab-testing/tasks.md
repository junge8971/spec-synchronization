## 1. Изолированное подключение

- [x] 1.1 Добавить адресное исключение A/B в архитектурные правила и AGENTS.md, сохранив остальные правила; проверить lint-fixtures для разрешённых shared/entities и запрещённых A/B↔KB, application internals, aliases, relative/type-only/re-export импортов.
- [x] 1.2 Добавить лёгкий публичный descriptor и три framework route entrypoint в `app/optional/ab-testing/`, подключить через application registry; проверить typegen и route tests для new/detail, basename, неизменных base/KB routes и отсутствия UI imports из descriptor.
- [x] 1.3 Подключить меню, крошки и tab deep links через существующую оболочку/session boundary; component tests должны подтвердить groups deep link, unknown-tab fallback, активный пункт и отсутствие бизнес-загрузок при запрете доступа.

## 2. Контрактный слой

- [x] 2.1 Добавить локальные A/B DTO/runtime schemas и клиенты metadata/lookups/search/detail/create/PUT на существующем transport; unit tests должны проверять envelope, data.experiments, malformed responses и отсутствие ручных изменений generated DTO.
- [x] 2.2 Добавить namespace queries/mutations с штатной отменой, session-owner semantics и отключённым mutation retry; тестами проверить late response, invalidation, двойную отправку и отсутствие повторного POST после подтверждённого ID при ошибке GET.
- [x] 2.3 Реализовать mapping snapshot/form/create/patch с явными defaults, nullability, полным replacement групп/поверхностей и сохранением IDs; unit tests должны покрыть пустой diff, reorder, nullable round trip, forbidden null и отсутствие sort_order/fake IDs.
- [x] 2.4 Реализовать локальную валидацию и mapping полевых ошибок с выбором вкладки; тестами проверить границы строк/int32, 1/2/100/101 групп, суммы 99/100/101, допустимый 0%, дроби, дубли тегов/IDs, scheduled, segment, даты и серверный конфликт name/code.

## 3. Предметные HTTP-моки

- [x] 3.1 Перед mock-работами прочитать proposal/design/specs архивных integrate-mpmm-auth-permissions и add-local-session-demo; создать изолированный A/B seed с существующими surface/user IDs и подключить nested tests в yarn test, проверив reset seed и отсутствие credentials/role enforcement.
- [x] 3.2 Реализовать metadata experiments/bindings и четыре A/B lookup-набора с inactive values; HTTP tests должны последовательно проверить A/B, KB и прочие lookup без взаимного перехвата регистраций.
- [x] 3.3 Реализовать A/B create/get/PUT/delete с проверкой полного агрегата, уникальности name/code, references, replacement и immutable tag по сохранённому статусу; HTTP tests должны подтвердить round trip, soft delete и отсутствие любых мутаций/timestamp changes при ошибке.
- [x] 3.4 Реализовать server search/sort/pagination и summaries с названиями поверхностей/групп; проверить query по всем документированным полям, AND/OR, регистрозависимые equality, несколько surface IDs без дубликатов и offset за концом.
- [x] 3.5 Подключить валидацию managed saved-filters resource=ab-experiments без зависимости от mocks/knowledge-base; проверить create/list/detail/update/delete, pagination и отказ неподдержанного search без изменения сохранённого фильтра.
- [x] 3.6 Реализовать A/B CSV обоих endpoints через общие технические helpers с документированными fields/headers/encoding/filename/limit; HTTP tests должны проверить full-selection export, quotes/formula safety, display names, group_distribution, предел и отказ вложенного payload.
- [x] 3.7 Обновить mock-документацию и coverage checks для восьми A/B-операций без возврата чужого CRUD к 501; прогнать существующие managed/KB tests и подтвердить отсутствие runtime timers, вымышленных метрик и archived seed.

## 4. Реестр и отбор

- [x] 4.1 Реализовать URL search codec и applied/draft separation; unit tests должны покрыть полное AND/OR round trip, сортировку/пагинацию, malformed JSON, неизвестные поля, лимиты и неподдержанные числовые/surface conditions без частичного применения.
- [x] 4.2 Реализовать таблицу, query от двух символов, status/surface multi-filters, трёхпозиционный sort и серверную пагинацию; component tests должны подтвердить total, offset reset, one-character query, empty/no-matches/error и keyboard opening карточки.
- [x] 4.3 Реализовать conditions UI для семи поддержанных полей с metadata operators, badge/summary, Apply/Cancel и недоступными пунктами групп/приоритета/поверхностей; проверить неполное условие, пустой in, 50/51 условий и отсутствие локальной фильтрации страницы.
- [x] 4.4 Реализовать сохранение/применение/удаление фильтров и копирование полного URL; component tests должны проверить reload selection, saved-filter pagination, совпадающие имена без upsert и clipboard/delete failures без ложного успеха.

## 5. Карточка и группы

- [x] 5.1 Реализовать единую форму четырёх вкладок, шапку и поля основного блока на существующих shared UI; component tests должны подтвердить defaults, серверные даты, null-preservation, missing/inactive lookup и отсутствие archived-перехода.
- [x] 5.2 Реализовать группы с добавлением/удалением, DnD за ручку и кнопками вверх/вниз; тестами проверить server IDs после reorder, лимит 100, пустые поля и readonly tag по сохранённому non-draft snapshot даже при локальном выборе draft.
- [x] 5.3 Реализовать распределение/легенду и ошибки суммы без скрытой нормализации; тестами проверить 20/20 с остатком 60, превышение 100, невалидный ввод, 0% группу, порог подписи 12% и идентификацию без цвета.
- [x] 5.4 Реализовать paginated выбор поверхностей через публичный entities API и ответственного через существующий user search; тестами проверить выбор за первой страницей, лимит 100 поверхностей, сохранение неизвестных IDs и reference lookup error без сброса draft.
- [x] 5.5 Реализовать правила запуска, условный segment, cross-tab validation и динамическое описание настроек с пояснениями границы API; component tests должны проверить scheduled без даты, segment без значения, log_group=false и отсутствие обещаний исполнения/назначения контрольной группы.
- [x] 5.6 Подключить Save с pending, error focus и create-to-detail recovery; тестами подтвердить POST/GET/PUT flow, hidden-tab error, сохранение snapshot и draft при 409/422/invalid response и отсутствие автоматического replay при неизвестном исходе.
- [x] 5.7 Реализовать подтверждённые PUT-команды паузы/возобновления/завершения по spec, без автоматической даты окончания; тестами проверить dirty/new blockers, cancel confirmation, completed no-op и серверный отказ без смены статуса или ложного уведомления.
- [x] 5.8 Реализовать защиту draft при уходе через close/крошки/sidebar/Back/другой ID и beforeunload; component tests должны проверить leave/stay, чистую форму, смену вкладок, refetch, same-user refresh и смену session owner через существующие механизмы.

## 6. Экспорт

- [x] 6.1 Реализовать выбор metadata fields и экспорт всего применённого отбора; тестами проверить порядок полей, пустой выбор, экспорт со второй страницы и ошибку export_max_rows без усечения.
- [x] 6.2 Реализовать пять групп выбора полей карточки с текстовыми сводками групп/поверхностей и недоступным вложенным экспортом; component tests должны подтвердить new disabled, dirty warning и отсутствие draft/sections в запросе.
- [x] 6.3 Подключить штатную доставку CSV с безопасным именем и cleanup; тестами проверить HTTP/download failure, pending double-click и смену session owner без доставки старого файла.

## 7. Приёмка и удаляемость

- [x] 7.1 Добавить проверку production route manifest/module graph для A/B с сохранением KB-проверки; обычная сборка, в том числе с CONTROL_API_MOCKS=true, должна содержать три A/B маршрута и не содержать mock/test fixtures.
- [x] 7.2 Написать application integration/removal guide с точным перечнем внешних imports/registrations/tests/scripts/globs/lint исключений; проверить отсоединение A/B в временной копии через typegen/build и архитектурные тесты без правок предметного кода KB/основных разделов.
- [x] 7.3 Сопоставить результаты с четырьмя A/B specs и матрицей прототип/API; сохранить краткий verification report с исполненными сценариями и честными ограничениями, не объявляя mocks подтверждением стенда.
- [x] 7.4 Выполнить yarn typecheck, yarn lint без warnings, yarn test, yarn format:check, yarn api:check, yarn build и OpenSpec validate; просмотреть итоговый diff и указать отдельно пройденные/упавшие/не запущенные проверки. E2E/browser не создавать, не редактировать и не запускать без отдельного разрешения.
