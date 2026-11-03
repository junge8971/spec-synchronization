# D093 — восемь независимых локальных сценариев, без публикации

Authority: пользователь поручил продолжать; все публикационные предложения складывать в audit/pending-publication.md. Модель: openai-codex/gpt-6-astra / low. Root текущий проект; baseline HEAD bc0d9800f25a90989b9c73c76f91996f8300f1d3.

Повторная parent попытка прочитать разрешённый MOS-707 через browser MCP вернула `TypeError: Failed to fetch` в 2026-10-20T15:08:41.998Z, items=[]; другие семь запланированных issue не запрашивались после ошибки. Никаких новых тел поверхностей не получено. Внешнюю очередь удерживаем, не подменяем данные предположениями. Продолжаем независимые локальные сценарии с уже сохранёнными телами.

Общий контракт: проект read-only; возвращать полный непустой отчёт в final response через назначенный runtime output. Не писать файлы tools, не запускать tests/browser/network/business API, не менять git/code/contracts/specs/ledgers/checkboxes, не создавать children. Parent единолично интегрирует после свежего пакетного review. Historical source cutoff и отсутствие deployment evidence обязательны. Проверить уже принятые reports/reviews/decisions и не повторять сделанный аудит: новые точные member joins либо недостающие implementation/test сопоставления. Указать source JSON pointers, code/spec/test locators, hashes, expected/observed/unknown, только evidence-backed keep/update/new/question. Не выбирать новые auth/продуктовые политики. Candidate proposal возвращать в отчёте для очереди, не публиковать.

| Work-item / owner | Inputs / точная цель | Output относительно audit |
| --- | --- | --- |
| JOIN-MOS-672 / analyst1 | sources/jira-shell-details/r1, exact MOS672 body; современная шапка, prior REQ/IMPL-MOS904 только как карта; не присваивать соседний member | reports/JOIN-MOS-672.md |
| JOIN-MOS-673 / analyst2 | sources/jira-shell-details/r1, exact MOS673 body; современная навигация, prior MOS904/905 карта | reports/JOIN-MOS-673.md |
| JOIN-MOS-674 / analyst3 | sources/jira-shell-details/r1, exact MOS674 body; breadcrumbs и текущие owners, prior MOS905 карта | reports/JOIN-MOS-674.md |
| IMPL-MOS-960 / analyst4 | sources/jira-sandbox-details/r1, SCENARIO-MOS-960 и review; недостающее точное code/test evidence sandbox context, не новый requirement audit | reports/IMPL-MOS-960.md |
| IMPL-MOS-961 / analyst5 | тот же source, SCENARIO-MOS-961 и review; chat/trace/history actual code/test boundaries | reports/IMPL-MOS-961.md |
| IMPL-MOS-962 / analyst6 | тот же source, SCENARIO-MOS-962 и review; sync/token actual code/test boundaries, не новые auth-модели | reports/IMPL-MOS-962.md |
| IMPL-MOS-920 / analyst7 | sources/jira-operations-details/r1, SCENARIO-MOS-920 и review; global modules UI/transport/mock/tests | reports/IMPL-MOS-920.md |
| IMPL-MOS-923 / analyst8 | тот же source, SCENARIO-MOS-923 и review; maintenance windows UI/transport/mock/tests | reports/IMPL-MOS-923.md |

Статус queued. Dependencies: сохранённые G1 источники и предыдущие reports; lanes независимы. Reviewer: отдельный свежий Astra-low пакетный reviewer после восьми outputs. Acceptance: точное новое покрытие либо честный no-op/gap; P прежних sandbox/operations не выдавать за новое U→P. Stop: инфраструктурный сбой/отсутствие обязательного локального источника/решение за пределами scope — точный blocker, без замены модели или режима. Не открывать внешние links из источников.
