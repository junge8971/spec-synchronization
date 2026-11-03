## Context

Мотивация и scope — в proposal.md. Дизайн нужен из-за нескольких точек композиции, переноса существующих моков и единого черновика с навигационной защитой.

Наблюдения по репозиторию:

- `app/application/constants/application-routes.constants.ts` собирает optional descriptors; `app/routes.ts` использует общий реестр. `app/optional/knowledge-base/` — образец владения, не библиотека для импорта.
- `knowledge-base/model/use-knowledge-base-editor.ts` уже использует React Hook Form/Zod, React Router useBlocker/useBeforeUnload, URL-вкладки и принятие сохранённого snapshot. `knowledge-base-form.test.ts` покрывает unknown codes, отсутствие ложного diff, replacement/clear связей.
- `knowledge-base/api/knowledge-base-directory-client.ts` показывает существующий API поиска пользователей и managed saved filters. Нужны собственные тонкие клиенты response-templates через shared HTTP, не импорт из KB.
- `app/shared/api/{http-client,file-response,read-csv-file}.ts` дают общий транспорт и работу с файлами. Public API skill/surface дают существующие запросы выбора сущностей; не обращаться к internal-файлам и не вводить альтернативный HTTP-клиент.
- `mocks/response-templates.mjs` содержит проверку связей; descriptor и metadata находятся в `managed-registry-model.mjs`, fixtures/catalogs — в `managed-registry-seed.mjs`, регистрация/валидация — в общих handlers, тесты — в `managed-registry.test.mjs`. Это перенос предметного владения, не второй сервер.
- `scripts/eslint-fsd-config.mjs` перечисляет optional-модули явно. `code-quality-gates` и AGENTS требуют адресного исключения; согласование пользователя относится только к response-templates. Расширить правила точечно, не исправлять несвязанные исторические расхождения других optional-модулей.
- `app/application/model/route-access.ts` использует консервативный unmapped fallback. У шаблонов нет согласованного отдельного grant; сохранить этот fallback, не добавлять пустой permission list, не заимствовать права KB/skills и не расширять auth scope. Это означает доступность только там, где существующая политика разрешает непокрытые маршруты.

### Evidence and precedence

26.10.2026 через Playwright прочитаны [MOS-1509](https://task.mos-team.ru/browse/MOS-1509), [MOS-1388](https://task.mos-team.ru/browse/MOS-1388), [Wiki](https://wiki.mos-team.ru/spaces/KR/pages/247744768), HTML-вложение `Шаблоны_Ответов_Прототип.html` и [OpenAPI T](https://nchat-t-tech.mos.ru/api/control/openapi.json). В Swagger прочитаны операции response-templates, saved-filters, users search и их схемы; бизнес-запросы не выполнялись. Source text + DOM-навигация прототипа подтвердили структуру экранов; обычные клики зависали из-за hidden-вкладки, поэтому это не полноценная usability/accessibility проверка.

Приоритет: явные решения пользователя по поведению; актуальная опубликованная схема для API; Jira/Wiki для сценариев; прототип для композиции, но не как эталон persistence. В частности:

| Расхождение                                                             | Решение                                                                                  |
| ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| CRUD §22 запрещает saved filters, live enum содержит response-templates | Использовать live managed saved filters; проверка публикации не равна backend acceptance |
| Прототип показывает успешный export без файла                           | Только серверный text/csv и проверенный download                                         |
| Экспорт карточки предлагает разделы                                     | Только девять опубликованных fields, без связей/ответственного                           |
| Кнопки статуса уведомляют до записи                                     | Изменение единого черновика; успех после Save                                            |
| Wiki обещает применение в диалоге сразу                                 | Не обещать runtime-публикацию, этот API управляет записью                                |
| edu/health против education/healthcare                                  | Использовать фактические lookups, не массив прототипа                                    |
| Wiki моделирует responsible как UUID                                    | Live допускает строковый внешний ID                                                      |

## Goals / Non-Goals

**Goals:** переиспользовать штатные транспорт, форму, маршрутизацию и query-инфраструктуру; отделить состояние списка, черновика и сохранённой записи; обеспечить изолированное удаление и отсутствие регрессий shared mocks.

**Non-Goals:** универсальный CRUD-конструктор, новые зависимости, новая auth/permission-модель, импорт внутренних функций KB, преобразование всех optional-модулей, исполнение шаблонов/подстановка переменных, soft-delete UI, журнал и произвольные архивные ограничения. Не импортировать несвязанные дельты актуального Swagger, например system-state, только ради полного обновления снимка.

## Decisions

### 1. Module seam and composition

Структура владельца: `api/`, `model/`, `ui/`, `routes/`, `handlers/`, `constants/`, `types/`, публичный `index.ts`. Composition импортирует только descriptor публичного index; route entrypoints тонко подключают собственные экраны. Маршруты используют текущий basename, не закрепляют `/tsam-panel/` из старой KB-спеки. Внешняя инструкция удаления — рядом с существующей `app/application/knowledge-base-integration.md`.

Альтернатива — обычные глобальные FSD-слайсы — хуже удовлетворяет согласованному независимому удалению. Альтернатива — импорт editor/registry из KB — нарушает независимость. Переиспользовать только уже подходящие shared primitive/API и публичные entities; не выносить новый универсальный движок ради двух похожих форм.

### 2. Existing framework and data patterns

Сохранить React Router Framework entrypoints/typegen. URL управляется useSearchParams/навигацией React Router; серверное состояние — существующим query-слоем, не собственными useEffect-fetch/cache. Editor использует установленный React Hook Form с Zod и существующий механизм mutation/HTTP ошибок. Это следует соседнему модулю и не требует миграции приложения на иной способ загрузки.

Список имеет единую проверяемую модель search; codec URL и saved-filter validation используют ту же модель. Условия редактируются отдельно до «Применить». Один символ в query не отправляется; UI показывает минимум два символа. Последний валидный результат не выдавать за результат неотправленного поиска. Query keys включают полный валидный search; отмена/устаревшие ответы не заменяют текущий отбор. Default sort `-updated_at`; третье нажатие заголовка возвращает этот default. Saved filters сохраняют отбор/сортировку и page size, но применяются с offset=0. URL включает текущую страницу.

Альтернатива — хранить фильтры только в памяти прототипа — теряет deep links и межсессионное сохранение. Автоматическое overwrite одинакового имени не требуется: backend-ошибку показать явно; не создавать неописанный upsert.

### 3. Contract adapters and boundary validation

Базовый ресурс `/api/control/api/v1/managed-resources/response-templates`: GET metadata, POST search/create/export, GET/PUT detail, POST detail/export. Existing shared HTTP сам формирует конфигурируемые адреса; не складывать URL вручную с новым auth-правилом. Metadata key `response-templates`; lookups section `response-templates` связывает tpl_types/tpl_scopes/tpl_statuses. Runtime-схемы проверяют ответы и обязательные поля, generated DTO используются без ручных исправлений.

GET `/api/control/api/users/v1/search` принимает query 1–200, limit 1–100, offset; возвращает items/total, ID строковый. Для skills/surfaces использовать соответствующие существующие entity public APIs с их pagination, не справочник из static HTML. Если конкретный нужный read-helper пока не экспортирован, допустимо минимально расширить public API entities существующей функцией без обхода границ. Сохранённые ID показываются даже без доступной подписи; поиск пользователя не является гарантированным lookup по произвольному ID, не придумывать endpoint hydration.

Альтернатива — валидировать всё только на клиенте — не обеспечивает уникальность и актуальность связей. Client проверяет форму, backend остаётся окончательным валидатором; поддержать errors с field pointers и стандартный 422 loc, фокус ошибки на нужной вкладке.

### 4. One draft and explicit save

```text
GET detail --> saved snapshot --> form draft
                                  | text / links / status
                                  v
                                Save
                                  |
                            POST or PUT
                           /           \
                       success        failure
                         |               |
                 accept snapshot    retain draft/errors
```

Все контролы статуса обновляют тот же draft. Archive confirmation не отправляет запрос. Toggle ON устанавливает active, OFF переводит active в paused и не трогает draft/archived, когда уже выключен. Не вводить отдельное поле активности или дополнительные lifecycle endpoint. Статусы выбираются из lookups; не накладывать непубликованные ограничения восстановления архива.

Построитель payload различает отсутствующее поле, null и пустой массив. Изменённые массивы отправляются целиком в одном PUT с остальными изменениями; неизменённые не очищаются из-за неполной загрузки directory. Не отправлять `{}`. Nullable optional text fields очищать согласованным null; не превращать обязательные поля в null только потому, что Patch допускает nullable union. Создание возвращает ID, после которого получить сохранённую карточку; не повторять POST автоматически при ошибке последующего GET. Пока идёт сохранение, повторная отправка и редактирование блокируются, чтобы успешный ответ не затёр более свежий ввод.

Dirty рассчитывать относительно принятого сохранённого состояния с учётом семантически одинаковых наборов ID. Router blocker защищает уход с карточки, но не смену tab; beforeunload — штатное предупреждение. Во время pending защищать уход отдельно от обычного dirty. На отказе записи не сбрасывать форму; на успехе обновлять snapshot и invalidate registry/detail. Никакой local optimistic-success публикации.

Альтернатива немедленных status mutations отвергнута пользователем: она смешивала бы сохранённый статус с несохранённым текстом.

### 5. Preview and export semantics

Предпросмотр — React text children с переносами, без innerHTML, интерполяции и выполнения HTML. Подпись поясняет, что переменные не подставляются. Типы/коды и placeholders не подменяются display labels в сохраняемом тексте.

Экспорт использует shared binary/CSV helpers, metadata labels и allowlist DTO. Список передаёт search без ограничения открытой страницей в соответствии с export semantics; проверить export_max_rows из metadata и ошибки лимита, не склеивать частичные страницы тайно. Карточка экспортирует сохранённую серверную версию; явная подпись при dirty и недоступность до первого сохранения. Предлагаемый default выбора полей — все доступные поля; пользователь может снять часть, но не все. Не считать уведомление «файл готов» подтверждением download без ответа text/csv.

### 6. Mock relocation rather than duplication

Переместить template validator, fixtures, catalog definitions и descriptor в `mocks/response-templates/`; сохранить общий Express routing/search/CSV и catalog/saved-filter infrastructure. Общая композиция регистрирует экспорт модуля. Из `managed-registry-handlers` убрать предметное ветвление, которое после удаления продолжало бы требовать template-файл; использовать существующую resource registration структуру с минимальным расширением, не новый plugin framework.

Сохранить прежние HTTP contract tests для API endpoints; template tests переместить к владельцу и добавить editor-critical failure/atomicity сценарии. Общие каталоги получают tpl-наборы через документированную регистрацию; после удаления раздела они не должны ломать другие ресурсы. Общие OpenAPI DTO/resource enum остаются, не удаляются вместе с UI. Runtime fixture data не попадают в browser build.

### 7. Quality and acceptance mapping

| Story                   | Основные проверки                                                                                                        |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Открыть раздел/карточку | route manifest, basename, new vs ID, tab deep link, existing denied boundary                                             |
| Найти/поделиться        | query boundary 1/2/200, OR/AND, сортировка, offset reset, full URL round trip, clipboard failure                         |
| Сохранить отбор         | API resource, pagination списка фильтров, reload, invalid stored search, deletion failure                                |
| Создать/редактировать   | draft defaults, unique conflict, поля/лимиты, atomic clear/replace, 422 field focus, pending, failed reload after create |
| Статус/выход            | no request before Save, archive cancel, dirty/no-dirty/revert, tab change, Back/menu/breadcrumb                          |
| Предпросмотр/связи      | буквальные HTML/placeholders, inactive/unknown codes, selected IDs вне страницы, 100/101 IDs, unavailable directory      |
| Экспорт                 | nine fields, entire search, limit, dirty saved version, CSV vs JSON, new record unavailable                              |
| Изоляция                | allowed/denied imports включая type-only/re-export, production без mocks, removal rehearsal                              |

Unit/component и mock HTTP обязательны. После отдельного разрешения по применимым AGENTS правилам — интерактивный Playwright MCP нового локального UI с моками по строкам таблицы, включая клавиатуру и error states. Не создавать автоматизированные E2E. Если инструменты/разрешение отсутствуют, записать blocker, не считать браузерную часть выполненной. Не приравнивать исследование HTML или mock checks к live-интеграции. Проверки `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`, `yarn api:check`, `yarn build` и удаляемость завершают реализацию, а не этот planning workflow.

## Risks / Trade-offs

- [Unmapped access] → Сохранить действующую консервативную политику; отсутствие отдельного grant не обходить. Расширение доступа потребует отдельного согласования.
- [Live schema не доказывает runtime/business semantics] → На выпуске отдельно подтвердить интеграцию в разрешённом контуре; до этого явно разделять schema coverage и реальные запросы.
- [Различие документации и spec config по browser approval] → Следовать применимым проектным запретам, запросить отдельное разрешение на проверку реализации; текущее разрешение исследовать прототип не переносить автоматически.
- [Shared mocks случайно сохранят template-зависимости] → Removal rehearsal в временной копии, HTTP-регрессии других ресурсов и полный список registration points.
- [Concurrent edits без expected_version] → Не обещать предотвращение lost update; сохранять серверные ошибки и пользовательский черновик, не придумывать version headers.
- [Нет lookup-by-ID ответственного] → Сохранить ID и показать его при отсутствии имени; не очищать и не угадывать соответствие.
- [Повтор похожего кода KB] → Допустимы небольшие предметные adapters; переиспользовать существующее shared, но не связывать optional-модули и не вводить общий CRUD-engine.

## Migration Plan

1. Добавить адресное правило изоляции, contract checks и перенести template-часть моков с сохранением existing tests.
2. Добавить модуль и публичный descriptor, затем подключить его в общий реестр без feature flag. Не менять существующие маршруты и режимы запуска.
3. Доставлять UI только с корректными contract/runtime schemas и проверками; импортировать лишь необходимые изменения API через генератор.
4. Выполнить acceptance matrix, сборку, boundary/removal проверки; для browser/live шагов записать разрешение и фактический результат либо blocker.
5. Rollback: удалить документированные registrations и module folders, сохранив общие API-контракты; изменения backend данных/миграции этим frontend change не выполняются.
