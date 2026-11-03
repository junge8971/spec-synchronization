# Восемь Astra-low lanes: два точных backend member, четыре источника доказательств

Authority: исходный apply, user eight-way parallel request, D091 model switch to Astra low. Root /home/user/my/work/codesrc/projects/CAM/tsam-admin-front; HEAD bc0d9800f25a90989b9c73c76f91996f8300f1d3. Model openai-codex/gpt-6-astra / low.

Общий вход: sources/jira-optional-backend-details/r1/content.json и metadata.json; source SHA256 3a135ce9c6e285f66d92263fdb995a48ddad098d4b9e4dd2324754c1cf2bb618. MOS1322=items[0], MOS1323=items[1]. Прочитать D091 и R-D091-RECOVERY: прежний gap body относится к старому пакету; текущий новый body впервые доступен. Не повторять прежний общий модульный аудит.

| ID / owner | Узкая ответственность | Output относительно audit |
| --- | --- | --- |
| REQ-MOS-1322-r2 / analyst1 | Атомарные требования точного backend issue, зависимости и вопросы | reports/REQ-MOS-1322-r2.md |
| API-MOS-1322-r2 / analyst2 | Операции/DTO/errors KB: сохранённый live r2 против local, по новому body | reports/API-MOS-1322-r2.md |
| SPEC-MOS-1322-r2 / analyst3 | Точный owner mapping main/active/archive полного набора артефактов; не подменять backend frontend | reports/SPEC-MOS-1322-r2.md |
| IMPL-MOS-1322-r2 / analyst4 | Конкретные code/mock/test evidence для тела KB, неизвестность backend/deployment | reports/IMPL-MOS-1322-r2.md |
| REQ-MOS-1323-r2 / analyst5 | Атомарные требования точного backend issue, configuration/execution граница | reports/REQ-MOS-1323-r2.md |
| API-MOS-1323-r2 / analyst6 | Операции/DTO/errors A/B: сохранённый live r2 против local по новому body | reports/API-MOS-1323-r2.md |
| SPEC-MOS-1323-r2 / analyst7 | Точный owner mapping main/active/archive полного набора артефактов | reports/SPEC-MOS-1323-r2.md |
| IMPL-MOS-1323-r2 / analyst8 | Конкретные code/mock/test evidence, включая partial PUT/group identities; backend unknown | reports/IMPL-MOS-1323-r2.md |

Status queued. Все независимы, зависят от нового evidence packet. Каждый возвращает полный русский отчёт через runtime output, не пишет tools. Parent — единственный интегратор. Reviewer: свежий пакетный reviewer после завершения. Acceptance: точные locators/хеши входов, requirement/observed/unknown, рекомендации keep/update/new/question без нового scope, неизменные исторические reports и features. Source dependencies не дают права открывать чужие задачи. Stop: недоступный обязательный input/инфраструктурный сбой/продуктовое решение; явный blocker вместо домысла.

Project read-only: никаких code/contracts/spec/ledger edits, tests, browser/network/business API, git mutations или nested subagents. В рецензиях и отчётах mock/contract/client не доказывают backend или deployment. Для SPEC читать полные относящиеся proposal/design/specs/tasks, используя принятые прежние reports как карту, не как замену. Для API не регенерировать DTO. Для IMPL не запускать тесты. Независимые результаты не заменяют последующее ревью.
