## MODIFIED Requirements

### Requirement: Documentation dropdown reuses article navigation

Кнопка «Документация» внизу sidebar SHALL открывать выпадающее меню первых шести существующих статей в порядке каталога и пункта «Все разделы». Ссылки SHALL использовать `/docs?article=<id>` и `/docs` с сохранением deployment basename. Старый `/documentation` SHALL перенаправлять на `/docs` с сохранением query, включая `article` и `q`. Выбор статьи SHALL закрывать меню и мобильный sidebar. Неизвестный article без фильтра SHALL сохранять существующий fallback на первую статью полного каталога. При поиске выбор и fallback SHALL определяться documentation-search: первая статья выдачи при недопустимом выборе, отсутствие статьи при пустой выдаче.

#### Scenario: Open article from sidebar

- **WHEN** пользователь выбирает статью из меню документации
- **THEN** открывается выбранная статья, её ID отражён в URL `/tsam-panel/docs?article=<id>`, меню и мобильный sidebar закрыты

#### Scenario: All articles and invalid identifier

- **WHEN** пользователь выбирает «Все разделы» или открывает документацию с неизвестным article без поискового фильтра
- **THEN** каталог остаётся работоспособным и показывается первая статья без ошибки страницы

#### Scenario: Legacy article URL

- **WHEN** пользователь открывает `/tsam-panel/documentation?article=surface-register&query=test`
- **THEN** открывается `/tsam-panel/docs?article=surface-register&query=test` с выбранной статьёй и без промежуточной записи старого адреса в истории

#### Scenario: Legacy search URL

- **WHEN** пользователь открывает `/tsam-panel/documentation?q=неоднозначности&article=skill-register`
- **THEN** открывается `/tsam-panel/docs` с теми же `q` и `article`, поиск восстановлен, промежуточной записи старого адреса в истории нет

#### Scenario: Search without results

- **WHEN** пользователь открывает документацию с запросом без совпадений и любым article
- **THEN** показано «Ничего не нашлось», статья скрыта, `article` удалён по documentation-search
