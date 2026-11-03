# JOIN-MOS-1053 — прямой вход в навыки

## Границы и итог

Read-only сверка конкретного MOS-1053, не всего MOS-624/оболочки. HEAD по контракту WAVE-D090-EIGHT: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (самостоятельно Git не проверялся). Записан только этот отчёт; тесты, серверы, браузер, сеть, git mutations и fanout не запускались. Исторические ledgers/checkboxes не изменены.

**Вывод: keep существующий owner; question — фактическое обслуживание URL на указанном контуре.** Тело требования доступно. Локально есть и маршрут навыков, и SPA fallback двух способов обслуживания; текущий дефект приложения не доказан. Ни CLOSED, ни статическая конфигурация не подтверждают исправление на внешнем хосте. Минимальное update-кандидат — точный положительный серверный regression case `/tsam-panel/skills` с HTML Accept в уже существующем тесте; новый продуктовый change не обоснован.

## Первичный источник и атомарный join

Пути ниже относительно корня репозитория; `A` = `openspec/changes/reconcile-control-center-backlog/audit`.

- `A/sources/jira-subtasks/r1/content.json:7–23`, JSON `/items/0`: key MOS-1053, parent MOS-666, CLOSED, updated `2026-10-09T15:05:26.189+0800`.
- **Точное тело** `/items/0/description`, строка 14: «Воспроизводится на контуре: https://mobile-a-tech.mos.ru/tsam-panel», шаг «Перейти по ссылке: https://mobile-a-tech.mos.ru/tsam-panel/skills», ФР «Ошибка 404», ОР «Открывается раздел навыков».
- `A/sources/jira-member-index/r1/content.json:47–59`, `/items/5/key` = MOS-666, `/items/5/subtasks/0/key` = MOS-1053. Это вложенная задача, не дополнительный прямой член модуля.
- `/items/0/attachments/0` (строки 16–22): 826713, `404.png`, image/png, 9096 bytes. Сохранены метаданные/URL, не изображение; адрес не посещался. `jira-subtasks/r1/metadata.json` явно ограничивает пакет: без скачивания вложений, comments/custom acceptance fields.

| Атом | Expected из тела | Observed локально | Unknown |
|---|---|---|---|
| MOS-1053-01 | Прямой переход по точному `/tsam-panel/skills` открывает раздел навыков вместо 404 | React Router SPA basename `/tsam-panel/`; `/skills` зарегистрирован и ведёт к SkillsPage; Nginx и локальный Express имеют index fallback | Ответ фактически развёрнутого `mobile-a-tech.mos.ru`, используемые ingress/config/build и состояние сессии; воспроизведение/устранение исходного 404 |

Это один пользовательский исход с двумя техническими швами: выдача HTML сервером и выбор экрана Router. Заголовок во множественном числе не расширяет тело до требования проверить каждый раздел. Refresh — дополнительная гарантия текущего main, не отдельный явно описанный шаг MOS-1053. Скриншот не требуется для чтения доступного тела, но детали первоначального 404 по нему неизвестны.

## OpenSpec owner и исторические доказательства

- **Main:** `openspec/specs/control-center-shell/spec.md:144–163`, `Canonical routes and compatible redirects`: basename, `/` → `/skills`, прямой вход/повторное открытие того же экрана при SPA fallback. Покрывает предмет MOS-1053 без нового requirement.
- **Archived delta:** `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md:58–76` — та же гарантия; `design.md:63–73` отделяет memory-router проверки от production fallback. `tasks.md:19–40` сохраняет незакрытый 4.1 и оговорку об отсутствии проверки внешнего хоста. Не переносить исторические результаты в результаты этой сессии.
- Отдельный действующий corrective delta для MOS-1053 в просмотренных coverage/локаторах не установлен; owner уже main shell + архив routing, инфраструктурная привязка родителя MOS-666 согласуется с конфигурацией `.maki`, но не доказывает root cause.
- Переиспользованы `A/reports/JIRA-MOS-624.md:50–65` (точный вложенный источник и пределы вложений), `A/reports/IMPL-MOS-905.md`, строка таблицы REQ-MOS-905-010 (basename/локальный fallback); принятые ограничения shell-аудита отражены в `A/decisions.md:605,615`. Эти отчёты не заменяют приведённое выше member body.
- `A/coverage.json` `/acceptedEvidenceThrough` = D-089; `/members/source` ведёт в `reports/G2-JIRA-MEMBER-JOINS.md`, строка 296: MOS-1053, MOS-666, `I(5)/subtasks/0 → S(0)`, исторический U/UN. В `/members/overlays` MOS-1053 отсутствует. Настоящий отчёт — кандидат узкого substantive partial join для независимого review, не самостоятельный переход population и не закрытие задачи.

## Code / tests / API

1. `react-router.config.ts:3–6`: `ssr: false`, `prerender: false`, basename `/tsam-panel/`. `app/routes.ts:6–14` реально регистрирует descriptors. `app/application/constants/application-routes.constants.ts:1–6` включает базовые маршруты; `app/shared/config/constants/application-routes.constants.ts:23–32` связывает `/skills` с `./routes/skills.tsx`.
2. `app/routes/skills.tsx:1–5` монтирует SkillsPage; `app/pages/skills/ui/skills-page.tsx:14–40` выбирает URL-вкладку и монтирует SkillsRegistry/домены/review. Это не заглушка маршрута. Успешный доступ остаётся под существующей session/access policy, а не обходится ради прямой ссылки; новые auth требования не выводятся.
3. **Production-конфигурация, не deployment:** `.maki/nginx/nginx-frontend-prod.conf:7–10`: `location ^~ /tsam-panel`, alias `/app/build/client`, `try_files $uri $uri/ /tsam-panel/index.html`. `docker-compose.prod.yml:27–29` монтирует эту конфигурацию, entrypoint и build/client. Наличие этих строк показывает предусмотренный fallback, но не загрузку этого config внешним Nginx и не валидность текущего deployment.
4. **Другой способ обслуживания:** `package.json:9` запускает `scripts/serve-spa.mjs`; строки 6–17 скрипта обслуживают `/tsam-panel`, возвращают index для HTML deep links, сохраняют 404 для путей с точками/non-HTML и внешних путей. Этот Express не подменяет доказательство Nginx.
5. `scripts/serve-spa.test.mjs:9–45`: положительные HTML случаи `/tsam-panel/` и `/tsam-panel/skills/123` с проверкой 200 и тела; ассет; отрицательные missing asset, business API, внешний URL и **точный `/tsam-panel/skills` с Accept application/json → 404**. Положительного HTML случая точного URL MOS-1053 в этом тесте нет. Соседний deep-link проверяет общий механизм, но не выдаётся за точное member assertion. Тест не запускался, Nginx не проверяет.
6. `app/routes/skills-navigation.test.tsx:12–14,67–78` подменяет SkillsRegistry и вручную монтирует memory route `/skills?tab=domains`; это не прямой HTTP-вход на требуемый host/path и не проверка полного production root. Использовать как вспомогательное свидетельство route wiring, не доказательство устранения 404.
7. **API:** тело MOS-1053 не содержит business API-запроса/схемы. Здесь проверяется document GET `/tsam-panel/skills`, не endpoint навыков. Сохранённый `docs/api/contracts/openapi.json`, JSON `/paths/~1api~1control~1api~1skills~1v1~1skills` (начало строки 796), описывает отдельный business resource. Изменение API/generated типов не требуется; бизнес-404 нельзя лечить возвратом SPA HTML. Отрицательный API case в `scripts/serve-spa.test.mjs:29–35` сохраняется. Данные, авторизация backend и полнота реестра вне данного атома.

## Минимальные рекомендации

- **keep:** main `control-center-shell` и archived routing как существующий owner; сохранить basename, framework routing, серверный fallback и отрицательные API/assets/non-HTML случаи. Не создавать дублирующий модуль или новый API.
- **update (кандидат после review, не выполнен):** в `scripts/serve-spa.test.mjs:21` добавить `/tsam-panel/skills` в положительную HTML-матрицу. Это малый regression gap точного URL, а не доказательство отсутствия реализации; Nginx/deployment этим тестом всё равно не покрываются.
- **new:** не требуется на имеющихся данных; нет установленного противоречия текущему main или подтверждённого нового frontend-дефекта.
- **question:** при отдельной разрешённой проверке среды установить, какой артефакт/config обслуживает указанный host и возвращает ли точный document GET приложение. Сейчас это явный deployment-evidence gap, не blocker чтения источника и не утверждение о дефекте. Получение отсутствующего 404.png/comments допустимо только отдельным решением; текущая узкая семантика тела от них не зависит.

## SHA256 ключевых входов

Вычислены локально Python hashlib без запуска приложения/тестов. SHA исходного body совпал с metadata.

| Вход | SHA256 |
|---|---|
| `A/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `A/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `A/sources/jira-member-index/r1/content.json` | `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` |
| `A/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `openspec/specs/control-center-shell/spec.md` | `4274bde7ecdf7e18bdcf73cb1755886f3e61bc2cbea3728da0a382006dd0276f` |
| `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md` | `9d51ba0735a20bb12c80618f6ec5aad6eb73e401e133e60af3bb7d11d5808ee5` |
| `react-router.config.ts` | `5612fb77145e37f599a5fa7194a3715f2cab135afadc93669778d18f0b2f07d5` |
| `app/routes.ts` | `3b7d7a026d0f73baa121d33407f155cadf9a18ffe5f0a618ad74bc02481594c4` |
| `.maki/nginx/nginx-frontend-prod.conf` | `a4375f659271f969128082a0304e235c50bc0594a656bb3c04a180228cfe6454` |
| `docker-compose.prod.yml` | `af0a010301c71b8ef7b3b1fc8f39c1e10d51cc2720beb11607a30df58bf8ec9b` |
| `scripts/serve-spa.mjs` | `f38b702764e49e37d6dee93f40462b6a1712ea3772d39fe762c13fbe3e4c3bfa` |
| `scripts/serve-spa.test.mjs` | `27c8da089e6812226fac135f28bdfb98f17f4e12927ed7fb57dd7ae1da368468` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Прочитано /items/0/description MOS-1053; атом прямого входа сопоставлен с main/archive, Router, Nginx, Express и точными ограничениями тестов/API."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-1053.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"python3: hashlib SHA256 ключевых входов и чтение coverage.json","result":"passed","summary":"Хеш body совпал с metadata; member overlay MOS-1053 отсутствует."},{"command":"tests/build/browser/network","result":"not-run","summary":"Запрещены контрактом задания."}],
  "validationOutput": ["Тело требования доступно; локальные источники и код прочитаны статически."],
  "residualRisks": ["Внешний SPA fallback и устранение исходного 404 не проверены.","Тело вложения 826713, comments/custom acceptance fields не сохранены.","Точный положительный HTML URL не перечислен в существующем Express-тесте; Nginx этим тестом не покрывается."],
  "noStagedFiles": true,
  "diffSummary": "Только аналитический отчёт; приложение, specs и исторические реестры не изменены.",
  "reviewFindings": ["Нет подтверждённого текущего frontend-дефекта; keep owner, узкий test update-кандидат и deployment question."],
  "manualNotes": "Git index не инспектировался; noStagedFiles означает отсутствие staging действий агента. Требуется независимое пакетное review, population и checkbox не менялись."
}
```
