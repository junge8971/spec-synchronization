# Spec Delta

## MODIFIED Requirements

### Requirement: Default routes and shell integration

Раздел SHALL подключаться без отдельного feature flag в mock и real режимах. Маршруты `/api-registry`, `/api-registry/new`, `/api-registry/:endpointId` SHALL работать под действующим basename; пункт «API» SHALL оставаться скрытым в sidebar по требованию Menu-only section visibility из control-center-shell. Крошки SHALL вести к реестру, а прямой вход во вложенный маршрут SHALL сохранять заголовок раздела без появления скрытого пункта или подсветки другого пункта. Карточка SHALL загружаться независимо от текущей страницы реестра. Вкладки карточки main/request/responses SHALL восстанавливаться из URL, неизвестная вкладка SHALL выбирать «Основное».

#### Scenario: Direct card entry

- **WHEN** пользователь открывает разрешённую ссылку карточки вне загруженной страницы с `tab=request`
- **THEN** загружается именно эта карточка, выбрана вкладка «Запрос», реестр доступен через крошки, заголовок раздела — «API», а его пункт меню остаётся скрытым

#### Scenario: Static new route

- **WHEN** пользователь открывает `/api-registry/new`
- **THEN** показана форма создания, строка `new` не передаётся как идентификатор карточки
