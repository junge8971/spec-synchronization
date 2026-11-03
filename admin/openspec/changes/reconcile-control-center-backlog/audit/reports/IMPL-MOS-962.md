# IMPL-MOS-962 — синхронизация и перевыпуск токена

## Результат и границы

**Обнаружен implementation gap, не основание для закрытия MOS-962.** Текущий `/sandbox` отображает статическую заглушку. Реализованный клиент отправки **поверхности** в sandbox и его тесты нельзя засчитывать как синхронизацию стенда с production или подтверждённый отзыв бизнес-токена.

Проверен только IMPL-MOS-962: новое сопоставление сохранённого требования с текущими UI/client/test-файлами. Контекст MOS-960, чат/trace/history MOS-961, новая auth-модель и полный аудит песочницы не выполнялись. Исходный SCENARIO и его review использованы как карта; замечания review не считаются автоматически внесёнными исправлениями.

Ничего не опубликовано и не записано инструментами. Ниже — кандидаты для родительской очереди `pending-publication.md`.

## Первичный источник

`A` = `openspec/changes/reconcile-control-center-backlog/audit`.

- `A/sources/jira-sandbox-details/r1/content.json`: `/items/2/key`, строка 47 — **MOS-962**; `/items/2/description`, строка 50.
- Требование: реальная синхронизация с версией, временем, результатом; отсутствие постоянного «Синхронизирован» до подтверждения; новый токен **и подтверждённый отзыв старого**; актуальное предупреждение об отключённых модулях/навыках; согласование доступа.
- `/items/2/status` — Backlog; `/items/2/updated` — `2026-10-15T14:46:47.097+0800`.
- Источник получен `2026-10-16T13:18:06.195Z` согласно metadata. SHA-256 содержимого пересчитан и совпал с metadata.
- Комментариев 0, attachments пуст; custom fields и тела вложений не собраны. Это исторический срез, не актуальная проверка Jira.

## Новое implementation/test evidence

| ID / решение | Expected | Observed: точные текущие локаторы | Unknown / предел вывода |
|---|---|---|---|
| **I962-01 — update** существующего SCENARIO-01/02 | Команда синхронизации и подтверждённые версия/время/результат; не постоянный неподтверждённый успех | `app/routes/sandbox.tsx:1–5` возвращает только `PlaceholderPage`. `app/pages/placeholder/ui/placeholder-page.tsx:1–10` содержит статические «ЦАМ» / «Административная консоль», без состояния, запросов или команд. В этом render path нет ни sync, ни надписи «Синхронизирован». | Отсутствие ложного успеха здесь — следствие отсутствия сценария, а не реализация протокола подтверждения. Поведение внешнего стенда неизвестно. |
| **I962-02 — update** доказательной границы SCENARIO-01/02 | Sync стенда нельзя заменять lifecycle поверхности | `app/entities/surface/api/surface-registry-client.ts:105–109` валидирует только `surface_id/status/updated_at`; `:118–125` отображает lifecycle actions на пути; `:190–203` выполняет bodyless POST по `surfaceId`. Нет параметра синхронизированной production-ревизии или результата отзыва токена в этом ответе. | Реальная семантика backend сверх проверяемого клиентского ответа не установлена. Это положительное evidence существующего transport, а не доказательство отсутствия всех backend sync API. |
| **I962-03 — keep + update evidence** SCENARIO-07 | Сохранить запрет видимого/скрытого запуска sandbox в surface MVP | `openspec/specs/surface-lifecycle-publication/spec.md:39,65–68`; `app/widgets/surface-details/ui/surface-details/model/surface-details-action-policy.ts:14–28` не разрешает sandbox action. `app/widgets/surface-details/ui/surface-details.test.tsx:143–154` проверяет отсутствие кнопки/checklist при status sandbox; `:618–636` проверяет ответ `SANDBOX_CHECK_REQUIRED`: отправлен только `publish`, без автоматического sandbox. | Тесты прочитаны, **не запускались**. Первый названный тест использует конкретно status sandbox: его название не доказывает отдельный прогон всех статусов. Запрет запуска поверхности не отменяет требование MOS-962. |
| **I962-04 — keep** владельца MOS-1023; **update** implementation evidence | Новый бизнес-токен вместе с подтверждённым отзывом прежнего; безопасная обработка неизвестного исхода | В sandbox render path отсутствует token UI. `app/widgets/skill-details/ui/tabs/connection-tab.tsx:9–44` показывает endpoint, contract_version, auth_required и текст «Транспортный токен» по `auth_type`; этот текст не является выданным секретом, metadata контура или rotation. `openspec/changes/mos-1023-skill-environment-tokens/tasks.md:1–14` оставляет API/security gate и реализацию незавершёнными; task 1.1 прямо включает отзыв и восстановление неизвестного исхода. | В inspected UI нет реализации подтверждённого перевыпуска. Нельзя выводить готовность из transport_token или технического session refresh. Точное соответствие sandbox credential общей модели skill/environment остаётся вопросом существующего владельца. |
| **I962-05 — update** SCENARIO-05, без присвоения MOS-960 | Актуальное предупреждение о влияющих отключённых модулях **и навыках** | Статическая `PlaceholderPage` не получает выбранный стенд, module/skill metadata и не отображает предупреждение. Это точный UI gap в целевом route, независимо от наличия данных в других разделах. | Не исследована заново полнота metadata API. Область влияния, freshness и идентификация выбранного стенда остаются вопросами владельцев; глобальную сводку нельзя объявлять таким предупреждением. |

### Что именно доказывают существующие transport-тесты

`app/entities/surface/api/surface-registry-client.test.ts`:

- `:440–478`, `maps every lifecycle action to a bodyless POST and validates the status response`: включает sandbox в массив actions; проверяет количество вызовов, POST, отсутствие body и принадлежность URL набору lifecycle-путей. Ответ fixture имеет status **prod для всех actions**. Поэтому тест не доказывает синхронизацию, production-ревизию или даже особую семантику sandbox-ответа.
- `:480–520`, `rejects an invalid lifecycle status or timestamp and preserves HTTP errors`: проверяет неизвестный status, невалидное время и HTTP 409 через **publish**. Это свидетельство проверок общего lifecycle-клиента, не специальный тест sync/token.
- Ни один из этих прочитанных тестов не проверяет новый токен, отзыв старого, потерянный rotation-ответ или stand-sync progress.

В `mos-1023-skill-environment-tokens/specs/skill-environment-tokens/spec.md:21–33` уже заданы подтверждение перевыпуска и неизвестный исход без автоматического повторного выпуска; `:35–47` — secret-safe интеграция. Tasks 2.2–2.4 перечисляют необходимые будущие проверки. **План тестов не является существующим тестовым покрытием.**

## Минимальные кандидаты для очереди parent

1. **Update:** дополнить MOS-962/связанный audit точными I962-01…05: `/sandbox` — заглушка; surface transport существует, но не закрывает sync/token acceptance; существующие тесты имеют описанную узкую область.
2. **Keep:** существующий MOS-1023 остаётся владельцем общего бизнес-token контракта и safety gate. Не создавать второй token change; не помечать текущие checkbox выполненными.
3. **Keep:** запрет sandbox запуска в surface MVP и ранее согласованную auth-политику. Замечание review о сохранении исторически записанного auth approval не превращать в новое открытие auth gate или разрешение sync/rotation. Auth approval/deployment в этой работе заново не проверялись.
4. **Question, существующие вопросы, не новые политики:** backend/product должны определить идентичность стенда и ревизии, authoritative sync confirmation/unknown-outcome recovery; через MOS-1023 — идентичность credential и доказательство отзыва; владельцы контекста — impact/freshness предупреждения; владельцы доступа — конкретные operation permissions.
5. **New:** новая задача или новое требование **не обоснованы**. Новое здесь — локальное implementation/test evidence, а не новая публикационная поверхность и не U→P.

Вопросы не блокировали read-only сопоставление: обязательные локальные материалы доступны; выбирать продуктовую политику для отчёта не потребовалось.

## SHA-256 входов

Все значения ниже получены локально `sha256sum`; пути относительно корня проекта, `A` раскрывается выше.

| Файл | SHA-256 |
|---|---|
| `A/work-items/WAVE-D093-LOCAL-EIGHT.md` | `bfed26db7f9865a85e19e0cdfbeb0b92fc7b2b16999be3dac4d1cb92bd5eaf4e` |
| `A/sources/jira-sandbox-details/r1/content.json` | `4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8` |
| `A/sources/jira-sandbox-details/r1/metadata.json` | `685bd0e3937a50ba0ace7e9b810f5ac9a12a67e7d67e9b61b47f8e6fbe51daaf` |
| `A/reports/SCENARIO-MOS-962.md` | `ce8e5834495bfa1888794ea7383480073a4f9a358785e2dd83298aeb926c8320` |
| `A/reviews/R-SCENARIO-MOS-962.md` | `83edb6bcdf01fb628277c70bf6b8fa104b90102c21d660e54367ab08464b9879` |
| `app/routes/sandbox.tsx` | `c756d932bb442ad34cda9636ba6917e12e3fab57d949dd904432debe993332b3` |
| `app/pages/placeholder/ui/placeholder-page.tsx` | `e39b58ae268a8ef3eb906326cba5cb4e7fc21dba97589fec52090b6b745c5e69` |
| `app/widgets/skill-details/ui/tabs/connection-tab.tsx` | `63a321baf7ccb4c80fae4baf293b1e9f6a7eb1690b2c7dfcc720c00e089c2b58` |
| `app/entities/surface/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `app/entities/surface/api/surface-registry-client.test.ts` | `4d5f93269521aedb76ce4dd722390c92dfa06e86b63af622f952146ef105c886` |
| `app/widgets/surface-details/ui/surface-details.test.tsx` | `5ff98d3c6e74786075c2060fb207171f56be28a70a9802e13d0fb6e50b9def3c` |
| `app/widgets/surface-details/ui/surface-details/model/surface-details-action-policy.ts` | `712c2a86c8c6cb2aa0b34b23d775596a4ae6bce3a3ec8d73b7e0e183a64ea9c4` |
| `openspec/changes/mos-1023-skill-environment-tokens/tasks.md` | `aeab5150dd4c94fbaab8f83777ddbe26d7a7b09b9b94373976d00b45e3883342` |
| `openspec/changes/mos-1023-skill-environment-tokens/specs/skill-environment-tokens/spec.md` | `7bf408fb93f75fb5ce4381c58feca5fdc50f697170aaacbb08b9423ed5eeaf1f` |
| `openspec/specs/surface-lifecycle-publication/spec.md` | `675265a0ba98b45f1d659f6048fe97f2e590a0597d7eda304cdcfe9854ebdd91` |

## Ограничения

- Только локальное чтение, поиск и хеширование. Tests/typecheck/lint/build/format, network/browser/API не запускались.
- Текущие файлы идентифицированы хешами; указанный в work-item baseline HEAD независимо не проверялся. Git/index не исследовались и не изменялись.
- Исторический Jira snapshot не подтверждает последующие изменения задачи. Предыдущие API/wiki выводы использованы как discovery map, не как заново проверенная публикация.
- Локальный transport и тестовые fixtures не доказывают deployment на A/T, доступность сервиса, выполненную синхронизацию, отзыв credential или готовность стенда.
- Отсутствие найденной реализации ограничено указанными render/client/test boundaries, а не всем backend.
- Отчёт предназначен для runtime-сохранения в `A/reports/IMPL-MOS-962.md`; публикационные кандидаты передаются исключительно parent.