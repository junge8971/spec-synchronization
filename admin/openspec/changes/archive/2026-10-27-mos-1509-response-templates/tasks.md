## 1. Контракт и адресные границы

- [x] 1.1 Сверить локальные response-template/search/export/saved-filter/user DTO с прочитанным актуальным OpenAPI T; при необходимости обновить только относящиеся к change контракты штатным генератором и описать расхождения. Проверка: contract assertions для resource enum, девяти CSV fields, 2–200 query, лимитов связей и строкового responsible ID; `yarn api:check`, без ручных правок generated schema.
- [x] 1.2 Добавить адресное response-templates optional-исключение в проектные инструкции и `scripts/eslint-fsd-config.mjs`, не ослабляя прочие правила. Проверка: тесты в `scripts/eslint-fsd-config.test.mjs` разрешают composition/shared/entities и запрещают cross-optional, application internals, deep imports, relative/type-only/re-export обходы.

## 2. Изоляция существующих моков

- [x] 2.1 Перенести template validator из `mocks/response-templates.mjs`, descriptor, fixtures и tpl-каталоги из shared registry-файлов в `mocks/response-templates/`, подключить через минимальные composition points. Перед mock-работами прочитать согласованные add-local-session-demo артефакты. Проверка: прежние восемь операций шаблонов, lookup и saved-filter HTTP-тесты проходят без второго сервера и без credentials.
- [x] 2.2 Перенести предметные template-тесты к владельцу, сохранить общие API registry regressions и обновить test registration. Проверка: CRUD, atomic reject, replacement/clear, duplicate/missing IDs, inactive references, metadata/search/CSV и изоляция saved filters; регрессии других managed resources проходят.

## 3. Модуль, транспорт и маршруты

- [x] 3.1 Добавить `app/optional/response-templates/` с публичным descriptor и framework entrypoints, подключить в application routes группу «Контент». Проверка: route/config tests для реестра/new/ID, basename, menu/breadcrumbs, tab=links/неизвестного tab, прямой карточки вне страницы списка и существующей unmapped access boundary без новых grants.
- [x] 3.2 Реализовать тонкие resource/metadata/lookups/saved-filters клиенты с runtime validation через shared HTTP и существующие query-механизмы. Проверка: client tests для корректных envelope, 403/404/422, invalid response, отмены/позднего ответа и корректного PUT вместо PATCH.
- [x] 3.3 Подключить поиск ответственных и публичные API entities для skills/surfaces без импорта KB; при необходимости минимально экспортировать существующий read-helper через entity index. Проверка: query/pagination tests, внешний строковый ID, сохранение выбранного ID без подписи, failed directory load и отсутствие credentials в локальных моках.

## 4. Реестр и сохранённые отборы

- [x] 4.1 Реализовать search schema и URL codec для query, типов/статусов/областей, условий, sort/limit/offset. Проверка: round trip полного OR/AND отбора, 1/2/200/201 символ, 50/51 условие, invalid URL, default sort и offset reset.
- [x] 4.2 Собрать таблицу, серверный счётчик, поиск, мультиселекты, конструктор условий с явным применением, active-condition bar, reset и пагинацию. Проверка: component tests подтверждают единый серверный отбор, сортировку в три шага, отсутствие локальной фильтрации страницы, loading/empty/no-matches/error и клавиатурную доступность.
- [x] 4.3 Добавить копирование полной ссылки и серверные именованные фильтры с пагинацией их списка. Проверка: component/client tests для clipboard failure, reload/apply с offset=0, invalid saved search без изменения текущего отбора, create/delete failure и отсутствия неявного overwrite.

## 5. Редактор и связи

- [x] 5.1 Реализовать form mapping/defaults/validation и create/partial PUT payload builders. Проверка: draft с пустыми связями; обязательные поля и границы длины/code regex; unknown/inactive read values; null vs omission vs []; 100/101 связей, дубли, отсутствие empty PUT и атомарная отправка изменений.
- [x] 5.2 Собрать «Основное» с метаданными и безопасным живым предпросмотром текста. Проверка: component tests сохраняют текст/переносы/неизвестные placeholders, не исполняют HTML, показывают пояснение о неподлежающей подстановке переменной и переводят фокус к ошибочному полю.
- [x] 5.3 Собрать «Связи» и выбор ответственного с поиском/пагинацией. Проверка: выбор по ID переживает смену вкладки, страницы и ошибку загрузки; изменение scope не меняет связи; пустой выбор не объявляется «все», историческое значение не заменяется default.
- [x] 5.4 Связать select/toggle/кнопки статуса с общим черновиком и подтверждением архива. Проверка: до Save нет запросов/успешных уведомлений, archive cancel не меняет draft, переключатель не портит draft/archived; отдельное is_active и DELETE не отправляются.
- [x] 5.5 Реализовать explicit save, pending protection, серверные field errors, принятие сохранённого snapshot и переход после create. Проверка: duplicate-name/code conflict, failed atomic save сохраняет форму, success снимает dirty, двойная отправка исключена; сбой GET после успешного POST не вызывает повторное создание.
- [x] 5.6 Добавить dirty-only router blocker и beforeunload: «Остаться»/«Выйти без сохранения», без autosave. Проверка: component tests для menu/breadcrumb/Back, clean/dirty/reverted/saved/failed-save состояний, сохранения черновика при смене tab и корректного фокуса диалога.

## 6. CSV

- [x] 6.1 Реализовать list/detail export adapters на shared file helpers с выбором опубликованных полей и полным отбором. Проверка: client tests для text/csv, nine-field allowlist, пустого fields, export limit, JSON/error/неожиданного content type, отсутствия page-only export и очистки временных ресурсов.
- [x] 6.2 Добавить диалоги экспорта списка и сохранённой карточки, пояснение для dirty и недоступность до первого сохранения. Проверка: component tests подтверждают отсутствие автосохранения, сохранение выбранных полей после ошибки, клавиатурный фокус и отсутствие фиктивного успеха.

## 7. Интеграционная приёмка и удаляемость

- [ ] 7.1 Написать инструкцию интеграции/удаления с полным списком frontend/mock/test registrations. Проверка: в отдельной временной копии удалить только перечисленное, выполнить typecheck/build и запуск/регрессии оставшихся моков; сохранить общие контракты. Основной рабочий checkout не удалять.
- [x] 7.2 Проверить production route/build graph: раздел включён без флага, моки и fixtures отсутствуют в клиентском графе. Проверка: build/manifest assertions и `yarn build`; текущие маршруты других разделов не изменены.
- [ ] 7.3 После отдельного разрешения по действующим правилам выполнить Playwright MCP на локальном приложении с моками: deep links, реестр/полный отбор/сохранённые фильтры, создание и связи, текстовый preview, status-before-save, dirty navigation, CSV, клавиатура и основные ошибки. Проверка: acceptance-отчёт по сценариям design с фактическими результатами; при отсутствии разрешения/инструментов оставить задачу незавершённой с blocker. Не создавать автоматизированные E2E и не проверять внешний UI без отдельного согласования. На 27.10 разрешение получено; после исправлений повторно проверены реальные локальные CSV-загрузки, создание, фильтры, tab/Back/Stay/Leave/revert, клавиатурный выбор, узкий экран и ошибка справочника. CSV, router warning и неразличимые поверхности исправлены. Задача остаётся открытой для browser readback clipboard (ограничение разрешений/инструмента), полного клавиатурного обхода и выбора связей со второй страницы (в текущем seed нет второй страницы; component-проверка есть). Результаты: `app/optional/response-templates/ACCEPTANCE.md`.
- [x] 7.4 Выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check`, `yarn api:check`, `yarn build`, просмотреть итоговый diff и обновить acceptance-отчёт. Проверка: команды, успешные/упавшие/не запущенные проверки и причины явно перечислены; отсутствие live-интеграционной проверки не скрыто результатами моков.

## 8. Исправления по результатам browser smoke и замечаниям к UI

- [x] 8.1 Исправить обязательные CSV-заголовки в общем mock helper и утечку useBlocker при Activity hide/show; не ослаблять shared file reader, session boundary или assertions. Проверка: реальный HTTP → shared CSV reader, граничные filename/empty export, Activity regression, успешные скачивания списка/карточки на диск и отсутствие warning при tab/Back/Stay/Leave.
- [x] 8.2 Привести реестр, карточку и связи к композиции переданного прототипа и дизайн-коду соседних разделов через существующие shared Select/Card/Tabs/Bubble/SelectionChip, без импорта KB и собственной темы. Различать одинаковые названия компактным ID, при совпадении суффиксов оставлять полный ID; полный ID также доступен в подсказке и accessible name. Проверка: component tests, keyboard selection/focus, desktop/mobile browser inspection и обновлённые screenshots/acceptance.
