# D090 — восемь узких заданий продолжения

Authority: пользователь явно поручил упрощённую процедуру и восемь параллельных агентов Astra medium. Используем компактные сценарные отчёты и одно независимое пакетное ревью; не отменяем доказательства, границы записи и критерии полноты. Исторические отчёты и ledger не переписываются.

Root: /home/user/my/work/codesrc/projects/CAM/tsam-admin-front
HEAD: bc0d9800f25a90989b9c73c76f91996f8300f1d3; git status clean (не учитывает ignored OpenSpec).
Model: openai-codex/gpt-6-astra, medium, registry checked this session.

## Общий контракт

Inputs: sources/jira-subtasks/r1/content.json (точный элемент по key), metadata той же revision; текущие coverage.json и соответствующие локальные main/delta/archive specs, code/tests. Дополнительные источники только из сохранённого audit/sources. Автор записывает в отчёте SHA256 прочитанных ключевых входов, JSON/line locators и HEAD. Предыдущие положительные результаты повторно не выдаются за новое покрытие.

Authority: read-only project; только runtime-bound уникальный output отчёта. Нет браузера, сети, business API, runtime/browser/E2E tests, edits приложения/контрактов/main specs/archive, feature-checkbox updates, git mutations или child fanout.

Acceptance: точные атомарные требования, сравнение API (либо обоснованная неприменимость), OpenSpec owner и текущий code/test путь; отдельные expected/observed/unknown, рекомендация keep/update/new/question с точными артефактами. Отсутствие источника — явный ограниченный gap, не выдуманное требование. Deployment не подтверждается статикой. Не пересматривать согласованные политики.

Reviewer: отдельный свежий Astra medium пакетный reviewer после восьми outputs; parent принимает решения и единолично интегрирует. Dependencies: сохранённый G1, независимые друг от друга. Stop: недоступный локальный источник, противоречие scope или инфраструктурный сбой — точный blocker; без замены модели/инструментов. Status: queued; run IDs сохраняются native workflow receipt и follow-up acceptance.

## Отдельные work-items

| ID / owner | Цель | Output относительно audit |
| --- | --- | --- |
| JOIN-MOS-1411 / analyst-1 | Видимость и семантика сброса фильтров диалогов | reports/JOIN-MOS-1411.md |
| JOIN-MOS-1412 / analyst-2 | Индикатор сбоя обработки диалога | reports/JOIN-MOS-1412.md |
| JOIN-MOS-1414 / analyst-3 | Время незавершённого диалога | reports/JOIN-MOS-1414.md |
| JOIN-MOS-1419 / analyst-4 | Точный дефект MOS-1419 из сохранённого описания | reports/JOIN-MOS-1419.md |
| JOIN-MOS-1422 / analyst-5 | Точный дефект MOS-1422 из сохранённого описания | reports/JOIN-MOS-1422.md |
| JOIN-MOS-1110 / analyst-6 | Точный дефект поверхности MOS-1110 | reports/JOIN-MOS-1110.md |
| JOIN-MOS-1164 / analyst-7 | Точный дефект поверхности MOS-1164 | reports/JOIN-MOS-1164.md |
| JOIN-MOS-1165 / analyst-8 | Точный дефект поверхности MOS-1165 | reports/JOIN-MOS-1165.md |

Это одна волна, не объявление завершения глобальных 3.1–3.5. Следующие независимые U/P gaps продолжаются после приёмки, пока нет блокировки.
