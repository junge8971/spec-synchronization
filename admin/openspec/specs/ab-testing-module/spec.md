# ab-testing-module Specification

## Purpose

Предоставить изолированный удаляемый раздел настройки A/B-экспериментов, подключённый к существующей оболочке без изменения режима API и без имитации исполнения экспериментов.

## Requirements

### Requirement: Default removable section

Раздел SHALL регистрироваться при обычном dev, typegen и production build без отдельного feature flag. Новый предметный код SHALL принадлежать `app/optional/ab-testing/`, серверные fixtures/handlers — `mocks/ab-testing/`. Внешние подключения SHALL быть перечислены в инструкции удаления; основные разделы и KB MUST NOT зависеть от A/B. Production SHALL содержать runtime раздела, но MUST NOT содержать его моки. Существующие mock/real режимы SHALL сохраняться.

#### Scenario: Ordinary build

- **WHEN** приложение собрано без специальных настроек A/B
- **THEN** три маршрута раздела присутствуют в manifest и выходном графе, mock modules отсутствуют даже при dev mock setting=true

#### Scenario: Remove the section

- **WHEN** удалены A/B-папки и документированные подключения
- **THEN** основные разделы и KB собираются без правок их предметного кода; общие DTO и серверные данные сохраняются

### Requirement: Shell routes and access

Раздел SHALL предоставлять `/ab-testing`, `/ab-testing/new`, `/ab-testing/:experimentId` под существующим basename `/tsam-panel/`, пункт «A/B эксперименты» в группе «Контент», крошки и единую подсветку меню. Вкладки SHALL восстанавливаться из `tab=main|groups|surfaces|rules`, неизвестная вкладка SHALL открывать main. Существующие session/access boundaries и политика непокрытых операций SHALL сохраняться без новых permissions или собственной авторизации.

#### Scenario: Direct detail link

- **WHEN** разрешён прямой вход на карточку с tab=groups
- **THEN** карточка загружается отдельным запросом независимо от страницы реестра, открыты группы и подсвечен раздел A/B

#### Scenario: Creation or denied access

- **WHEN** открыт new либо доступ запрещён существующей политикой
- **THEN** new не используется как ID эксперимента; запрещённый экран не начинает бизнес-загрузки

### Requirement: Configuration is not execution

Раздел SHALL сохранять параметры и статусы, но MUST NOT исполнять либо имитировать распределение трафика, запуск по расписанию, сбор метрик и автостоп. Рядом с настройками расписания/автостопа и пояснением правил SHALL быть видимое объяснение границы API. Подтверждение сохранения или статуса MUST NOT утверждать фактический запуск/остановку трафика. UI MUST NOT выводить назначение контрольной группы из позиции или тега, назначать алгоритмы группам или синтезировать результаты.

#### Scenario: Save scheduled experiment

- **WHEN** настройки scheduled и auto_stop сохранены успешно
- **THEN** UI подтверждает сохранение настроек и поясняет, что их исполнение не обеспечивается этим API, без таймера запуска и вымышленных метрик

### Requirement: Unsupported functions and accessible states

Неподдержанные функции прототипа SHALL оставаться видимыми с локальными доступными пояснениями, без успешной имитации. Архив `archived` MUST NOT подменяться `disabled` или DELETE; новый выбор archived SHALL быть недоступен при текущем контракте. Неизвестные сохранённые коды SHALL отображаться без молчаливой замены. UI SHALL различать loading, empty, no matches, invalid response, 403, 404 и retryable errors; обеспечивать клавиатурную доступность, focus management и текстовый безопасный вывод данных.

#### Scenario: Archive and disabled

- **WHEN** отображаются варианты статуса
- **THEN** disabled имеет серверную подпись, archived присутствует недоступным с объяснением отсутствия поддержки и не отправляется вместо другого статуса

#### Scenario: Supported request fails

- **WHEN** поддержанный GET вернул 500
- **THEN** отображается ошибка с повтором, а не фиктивные данные или утверждение об отсутствии API
