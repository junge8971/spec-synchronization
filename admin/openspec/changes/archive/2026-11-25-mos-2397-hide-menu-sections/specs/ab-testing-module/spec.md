# Spec Delta

## MODIFIED Requirements

### Requirement: Shell routes and access

Раздел SHALL предоставлять `/ab-testing`, `/ab-testing/new`, `/ab-testing/:experimentId` под существующим basename `/tsam-panel/`, крошки и заголовок раздела. Пункт «A/B эксперименты» SHALL оставаться скрытым в sidebar по требованию Menu-only section visibility из control-center-shell, в том числе при прямом входе; другой пункт MUST NOT подсвечиваться вместо него. Вкладки SHALL восстанавливаться из `tab=main|groups|surfaces|rules`, неизвестная вкладка SHALL открывать main. Существующие session/access boundaries и политика непокрытых операций SHALL сохраняться без новых permissions или собственной авторизации.

#### Scenario: Direct detail link

- **WHEN** разрешён прямой вход на карточку с tab=groups
- **THEN** карточка загружается отдельным запросом независимо от страницы реестра, открыты группы, сохранены заголовок «A/B эксперименты» и крошки, а пункт A/B в sidebar остаётся скрытым

#### Scenario: Creation or denied access

- **WHEN** открыт new либо доступ запрещён существующей политикой
- **THEN** new не используется как ID эксперимента; запрещённый экран не начинает бизнес-загрузки
