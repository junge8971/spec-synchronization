# Продолжение D090: review + семь аналитиков

Authority, HEAD, запреты и критерии: WAVE-D090-EIGHT.md. Model всех children: openai-codex/gpt-6-astra / medium. Parent — единственный интегратор; children read-only, возвращают только runtime-bound outputs. Эта волна не принимает предыдущую автоматически.

## Work-items

| ID / owner | Inputs / цель | Output относительно audit | Reviewer |
| --- | --- | --- | --- |
| R-D090-EIGHT / reviewer-1 | JOIN-MOS-{1411,1412,1414,1419,1422,1110,1164,1165}, исходные локаторы, текущие specs/code; проверить каждый вывод и минимальный scope | reviews/R-D090-EIGHT.md | parent acceptance |
| JOIN-MOS-1166 / analyst-2 | jira-subtasks/r1 item по key; точный дефект поверхности | reports/JOIN-MOS-1166.md | следующий независимый пакетный reviewer |
| JOIN-MOS-1167 / analyst-3 | jira-subtasks/r1 item по key; точный дефект поверхности | reports/JOIN-MOS-1167.md | следующий независимый пакетный reviewer |
| JOIN-MOS-1053 / analyst-4 | jira-subtasks/r1 item по key; прямой URL и 404 | reports/JOIN-MOS-1053.md | следующий независимый пакетный reviewer |
| JOIN-MOS-1150 / analyst-5 | jira-subtasks/r1 item по key; число возвращённых модулей | reports/JOIN-MOS-1150.md | следующий независимый пакетный reviewer |
| JOIN-MOS-1054 / analyst-6 | jira-subtasks/r1 item по key; точный дефект документации | reports/JOIN-MOS-1054.md | следующий независимый пакетный reviewer |
| JOIN-MOS-1322 / analyst-7 | jira-member-index и сохранённые sources по key; точная задача KB, не весь раздел | reports/JOIN-MOS-1322.md | следующий независимый пакетный reviewer |
| JOIN-MOS-1323 / analyst-8 | jira-member-index и сохранённые sources по key; точная задача A/B, не весь раздел | reports/JOIN-MOS-1323.md | следующий независимый пакетный reviewer |

Status: queued. Dependencies: review зависит от восьми завершённых отчётов первой волны; аналитики независимы, только сохранённый G1. Success: атомарные требования и точные source/spec/code/test joins, input hashes, явные unknown; без экстраполяции соседнего покрытия. Stop: инфраструктурный сбой либо решение за пределами scope. Отсутствующий source фиксировать как gap, не выдумывать тело задачи. Review возвращает accept/revise/escalate для каждого отчёта, точные обязательные поправки, проверку кандидатных изменений и возможность объединить четыре диалоговых исправления в один связный corrective change, избежав конфликтующих полных MODIFIED блоков. Геометрические неизвестные не превращать в утверждение о дефекте текущего кода.

Общие реестры/checkboxes не изменяются до независимой приёмки. Состояния children и IDs — в native workflow receipt; итог переносит parent.
