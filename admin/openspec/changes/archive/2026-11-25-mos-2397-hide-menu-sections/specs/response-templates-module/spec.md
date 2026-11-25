# Spec Delta

## MODIFIED Requirements

### Requirement: Default registration and direct navigation

Раздел SHALL подключаться без отдельного feature flag в mock и real режимах. Реестр `/response-templates`, создание `/response-templates/new` и карточка `/response-templates/:templateId` SHALL работать под действующим basename; пункт «Шаблоны ответов» SHALL оставаться скрытым в sidebar по требованию Menu-only section visibility из control-center-shell. Крошки и заголовок раздела SHALL соответствовать маршруту, а прямой вход MUST NOT возвращать скрытый пункт или подсвечивать другой пункт вместо него. Карточка SHALL загружаться отдельно от списка. Вкладки main/links SHALL восстанавливаться из URL; неизвестная вкладка SHALL открывать «Основное».

#### Scenario: Direct card link

- **WHEN** пользователь открывает разрешённую прямую ссылку карточки с `tab=links`, отсутствующей на текущей странице реестра
- **THEN** карточка загружается по ID, открываются «Связи», крошки ведут в реестр, заголовок раздела — «Шаблоны ответов», пункт меню остаётся скрытым

#### Scenario: Creation route

- **WHEN** пользователь открывает `/response-templates/new`
- **THEN** открывается форма создания и строка new не передаётся как ID API
