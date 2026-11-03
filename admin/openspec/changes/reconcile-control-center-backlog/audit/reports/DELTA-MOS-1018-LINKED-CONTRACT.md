# DELTA-MOS-1018-LINKED-CONTRACT

## Recommendation: bounded no-material-delta

The newly available catalog contract supplies **no pertinent new phrase-conflict rule requiring reconsideration of the accepted MOS-1018 planning statements**. Preserve the accepted documentation publication and all existing gates; no revision, automatic reopening, integration authorization or task closure is recommended. The evidence-access limitation changes prospectively: a revision-6 body is now available locally. This does not invalidate the historical r1 404 or explain its cause.

## Code Context

### Files Retrieved

Paths are repository-relative. Let `A = openspec/changes/reconcile-control-center-backlog/audit` and `P = openspec/changes/mos-1018-skill-phrase-conflicts`. Compact JSON evidence is located by JSON pointer and rendered heading below, not invented HTML line numbers.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/DELTA-MOS-1018-LINKED-CONTRACT.md` — complete bounded assignment.
2. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r2/content.json` (lines 1–49), `metadata.json` (lines 1–51), `attachments.json` (line 1) in that same directory — new primary source, provenance and attachment coverage; complete inert body reading.
3. `openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-1018.md` and `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-WRITE-MOS-1018.md` — complete prior disposition/publication context, not substituted for primary evidence.
4. `openspec/changes/mos-1018-skill-phrase-conflicts/proposal.md` (1–27), `design.md` (1–29), `tasks.md` (1–18), `specs/skill-phrase-conflicts/spec.md` (1–52) — complete current accepted planning.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-details-MOS-774/r1/content.json` (line 1), `$.items[7].key` and `.description` — confirmed MOS-1018 and direct linked-contract membership.
6. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json` (line 1), `$.bodyView`, MAC-6, ПРТ-МАС-5/6/7 and T-19 — existing send/checking tension, selectively reread.
7. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1), three operation descriptions below — independent check of retained boundaries only.
8. `docs/api/contracts/openapi-2026-10-15.raw`, historical single-phrase operation keys — chronology verification only.
9. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r1/access-result.json` (1–13) — preserved earlier access limitation.

### Provenance and integrity

Independently computed SHA-256 over local file bytes:

| New evidence | Bytes | SHA-256 | Comparison |
| --- | ---: | --- | --- |
| `A/sources/wiki-241097511/r2/content.json` | 73058 | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` | Matches work item and metadata |
| `A/sources/wiki-241097511/r2/attachments.json` | 372 | `dce4311f74a29968dec10bca60a9caa34892ddc093647a099efe9a893d121812` | Matches metadata |

Content and metadata agree on source ID `wiki-241097511`, HTTP 200, URL `https://wiki.mos-team.ru/rest/api/content/241097511?expand=body.view,version`, capture `2026-10-16T12:37:03.295Z`, and page `$.version.number = 6` (revision timestamp `2026-10-13T17:56:19.256+08:00`). Title: **API-контракт реестра доменов и каталога навыков**. Metadata records parent same-origin collection; local verification establishes saved-record consistency, not independent remote authenticity or deployment.

Attachment record: HTTP 200, captured `2026-10-16T12:37:36.819Z`; `$.data.results = []`, size 0, and no `$.data._links.next`. Metadata agrees: count 0, next null. No attachment traversal is needed.

Direct membership is established by saved MOS-1018 `$.items[7].description`, under “Контракты”, linking `/spaces/KR/pages/241097511/API-…`. No neighboring source was followed. r1 records HTTP 404 with no collected body and no exact capture time; successful r2 collection does not distinguish deletion, wrong-ID or permission-masking explanations for the earlier result.

**Version distinction:** page revision 6 is not the contract-body version. `$.bodyView` → “Общая информация” says “Версия контракта: v1.0.”; “3. История версий” lists v1.1 dated 14.09.2026 and v1.0 dated 11.09.2026. Record this internal labeling discrepancy without choosing a winning version. Neither label proves phrase-method introduction or runtime deployment.

### Key Code / contract evidence

All new-source headings below are within `A/sources/wiki-241097511/r2/content.json`, `$.bodyView`.

| Exact heading/pointer | New source says | MOS-1018 impact |
| --- | --- | --- |
| “Общая информация”; “1. Цель задачи” | Catalog viewing, creation and card modification; protection against duplicate execution/concurrent writes. | Scope is catalog CRUD, not phrase-conflict commands. |
| “1.3 Модель навыка” → “Поля навыка”; “2.6 Получить карточку навыка” | Skill object includes integer `version`; card returns that model. | This document does not specify intents, persisted conflict readiness/checks or a phrase-check result. Its omission does not negate the saved API's checks. |
| “2.8 Изменить карточку навыка” → “Изменяемые поля” | Card PATCH fields and `expected_version`, returning incremented version. | No phrase-set editing or send/status command is defined here. Do not substitute card PATCH for PUT intents or agreed send. |
| “2.9 Обработка конкурентных и повторных команд” → “Версия объекта” | PATCH requires matching `expected_version`; successful changes increment version; mismatch gives 409 `VERSION_CONFLICT`. | Optimistic locking is not a certificate that all current unsaved phrases were checked, nor a binding of preflight output to those phrases. |
| Same heading → “Идемпотентность” | Key binds method, URI and body in current-user context; same-key/same-body repeats return original status/body; changed body rejects. | Duplicate suppression does not establish current-input certification, persisted readiness or fresh validation on send. |
| “2.5 Получить список навыков”; “2.6 Получить карточку навыка”; “2.8 Изменить карточку навыка” | Visibility/access checks are delegated to a separate authorization contract. | No approval of cross-team conflict-name disclosure, and no reason to remove neutral fallback or fetch hidden details. |
| “2.10 Формат ошибок”; “4. Открытые вопросы” | Generic format/business-validation errors; catalog questions. | No phrase normalization boundary examples, exact/semantic handling, phrase-specific blocking error or send-revalidation policy. Generic 422 is not proof of these rules. |

Full inert body reading found no phrase-conflict/preflight, whole-input result-binding, persisted readiness-recalculation or server-on-send rule. This is **absence in this catalog document**, not absence across all evidence. Catalog uniqueness proposals are not phrase normalization rules; no unrelated domain or token decision is derived.

### Material supporting/conflicting evidence retained

For saved API base `/api/control/api/skills/v1/skills/{skill_id}`, independently reread:

- `$.paths[base + '/phrase-conflicts/check'].post.description`: checks one phrase, saves nothing, changes no readiness checks. Scope/self-exclusion, exact/blocking versus semantic/warning, percentage/order and cross-team names remain published facts, not whole-set or disclosure approval.
- `$.paths[base + '/intents'].put.description`: full group replacement and transactional conflict recalculation; no-op neither recalculates nor increments version; response lacks checks. Catalog PATCH version prose does not supersede these separate operation semantics.
- `$.paths[base + '/status'].post.description`: explicitly exempts `draft -> checking` from readiness checks/recalculation. Wiki `$.bodyView` MAC-6 and T-19 block wizard send on exact conflicts; ПРТ-МАС-7 gives resulting checking state. New catalog CRUD prose neither resolves nor worsens this accepted mismatch.
- Historical `/phrase-conflicts/check` POST exists in `docs/api/contracts/openapi-2026-10-15.raw` without a `description` key. Preserve “existing method, newly documented semantics relative to snapshot,” not “new method.”

No material new supporting or conflicting phrase-specific rule was found. No source precedence is selected.

## Architecture

Keep three distinct boundaries: transient single-phrase comparison; persisted full-group save/recalculation; agreed-send server validation. Generic catalog object concurrency and idempotency are not a fourth mechanism that closes the gaps between them.

No accepted statement needs reconsideration: retain `P/proposal.md:25–27`, `P/design.md:13–18,23–25`, `P/tasks.md:3–5,11–13`, and `P/specs/skill-phrase-conflicts/spec.md:30–52`. The only prospective evidence update is that this linked source is now locally readable. Historical reports describing the earlier access state remain unchanged. Previously excluded presentation/count work is not reopened.

## Start Here

`openspec/changes/mos-1018-skill-phrase-conflicts/design.md:13–18,24` remains the operative planning boundary; no edit is recommended. Existing task 1.1 must still resolve normalization examples, safe disclosure, binding to the full current input/version, concrete blocked send and its server revalidation, including the wizard/status mismatch. This new source answers none of those questions. No new owner decision or escalation is required merely for this evidence addition.

## Validation and limitations

Local JSON parsing, byte hashing, numbered planning reads and inert HTMLParser extraction only. No scripts from HTML executed; no network/MCP/browser, nested agents, tests/build/generation, product edits, historical edits, git mutation or task closure. Only this report was written. Existing evidence was selectively reread, not re-audited globally or independently rehashed. No repository-wide integrity or staging-state claim is made. Saved documents cannot prove deployed behavior.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Bounded no-material-delta recommendation based on independent revision-6 body reading, verified content/attachment hashes, direct MOS-1018 link membership, current accepted planning and scoped primary comparison."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-MOS-1018-LINKED-CONTRACT.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python JSON parsing, SHA-256 and inert HTMLParser extraction","result":"passed","summary":"Content 73058 bytes and attachments 372 bytes match metadata hashes; revision/capture/link membership verified."},
    {"command":"Numbered current planning reads and selected saved API/wiki/historical JSON inspection","result":"passed","summary":"Accepted gates and chronology remain applicable; catalog rules do not supply missing phrase-specific decisions."},
    {"command":"Tests/build/generation/network/MCP/browser","result":"not-run","summary":"Prohibited by bounded assignment."}
  ],
  "validationOutput": ["No accepted MOS-1018 statement requires revision from this source; no task closure or implementation acceptance."],
  "residualRisks": ["Normalization examples, disclosure, whole-current-input binding and concrete send/server validation remain unresolved.","Page revision 6 differs from body v1.0 label and v1.1 history; no precedence inferred.","Saved provenance is locally consistent, not remote/runtime proof; r1 404 cause remains unknown."],
  "diffSummary":"Only authoritative delta report written; historical evidence, decisions and planning left unchanged.",
  "reviewFindings": ["No new blocker or material phrase-conflict delta in the linked catalog contract."],
  "manualNotes":"No staging actions; index state not inspected. Recommendation is bounded to new linked-source impact, not a repeat audit or task acceptance. Independent reviewer and parent retain acceptance ownership."
}
```
