# G1-WIKI-ROOT-REGISTRY

## Result and boundary

Root-snapshot registry reconciled: **42 entries = 42 unique page IDs**, exactly matching checkpoint r1 in order, titles and discovery pointers; symmetric difference empty. Four direct-link pages have saved bodies/extractions; **38 remain uncollected**, not proven unavailable. No direct-link status changed since checkpoint r1. Later successful packets resolve two historical failures **outside this 42-set**, and must not inflate its coverage.

This is completeness of accounting for `sources/wiki-238324523/r1/content.json#/pages` only. It is not completeness of the live root, Confluence tree, linked materials, attachments, Jira-linked sources, task 2.3 or G1. No semantic approval or task closure is recommended. All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/` unless explicitly prefixed with the change path.

## Files Retrieved

- `../proposal.md` lines 1–29; `../design.md` lines 1–143; `../tasks.md` lines 9–16: scope, ambiguity gate, source metadata requirements and task 2.3.
- `work-items/G1-WIKI-ROOT-REGISTRY.md` lines 1–9: bounded assignment.
- `sources/wiki-238324523/r1/content.json` lines 1–53: sole discovery snapshot.
- `source-checkpoint-r1.json` lines 1–366: original saved inventory and 42 discovery records.
- `source-checkpoint-r2.json` lines 1–167: supplemental successes, attachment summaries and limitations.
- `sources/wiki-241080062/r1/metadata.json`, `sources/wiki-243776365/r1/metadata.json`, `sources/wiki-245673187/r1/metadata.json` lines 1–14 each; respective `content.json` line 1: provenance, body presence, attachment index fields and hashes (no business interpretation).
- `sources/wiki-247734813/r1/metadata.json` lines 1–11; `content.json` lines 1–135, especially 10–12: flattened body extraction and observed attachment link.
- `sources/wiki-241082009/r1/access-result.json`, `sources/wiki-241097511/r1/access-result.json` lines 1–13 each; corresponding r2 `metadata.json` lines 1–50 and 1–51, `content.json` lines 1–49 each, `attachments.json` line 1 each: failures retained, later successes.
- `sources/wiki-241085439/r1/metadata.json`, `sources/wiki-241085838/r1/metadata.json`, `sources/wiki-241088180/r1/metadata.json`, `sources/wiki-241092242/r1/metadata.json` lines 1–54 each; respective `content.json` lines 1–64: additional saved IDs and their distinct membership provenance.
- `sources/wiki-241080062-readable/r1/metadata.json` lines 1–253; `sources/wiki-241097511-readable/r1/metadata.json` lines 1–79: derived packet lineage, not new external captures. Chunk bodies were not semantically reviewed.

## Key evidence and provenance

Root: observed URL `https://wiki.mos-team.ru/spaces/KR/pages/238324523/`; embedded `retrievedAt=2026-10-16T11:13:47.038Z`; method is parent browser main-content text/link extraction with normalized page IDs. Its SHA-256 recomputes to `1b7343ea0c6ba9d52cbe2dbae19a9e725efe1654dcfc188570208b15ee58d003`, matching checkpoint r1. **No root metadata.json exists**; external version, independent capture provenance and attachment index remain absent. The embedded timestamp is evidence, not an invented replacement metadata timestamp. Hash concerns the saved extraction, not the original web response. The snapshot preserves IDs/titles, not individual hrefs for its 38 uncollected destinations; this report does not construct URLs from those IDs.

All ten saved non-root canonical wiki content hashes recomputed equal their adjacent metadata SHA-256 values. Root comparison to metadata is not applicable (file absent), not a digest mismatch. These checks establish local byte consistency only, not origin authenticity, freshness, semantic completeness or external approval.

| Direct-link packet | External version; saved retrieval time (UTC) | Body / attachment evidence | Remaining need |
|---|---|---|---|
| `wiki-243776365/r1` | 13; 2026-10-16T11:51:52.439Z | bodyView + text; attachment index size 0, next null | No missing body/metadata/index for this snapshot; freshness and semantic review separate |
| `wiki-241080062/r1` | 17; 2026-10-16T11:48:21.710Z | bodyView + text; index size 1, next null; attachment 245672060, `БД-Навыки.svg` | No missing body/metadata/index; SVG body uncollected, relevance review before request |
| `wiki-245673187/r1` | 18; 2026-10-16T11:45:08.223Z | bodyView + text; index size 0, next null | No missing body/metadata/index for this snapshot |
| `wiki-247734813/r1` | 11; 2026-10-16T11:17:53.564Z | textContent + links, tables flattened; no bodyView or attachment enumeration | Attachment index; structural bodyView if table-sensitive evidence is required; linked prototype body remains uncollected |

The first three attachment indexes report exhausted pagination in their saved normalized envelopes; this does not independently verify the live server. Feedback's observed prototype URL is at `sources/wiki-247734813/r1/content.json#/links/0/href` (line 12). It is a discovery edge, not an attachment inventory. No executable HTML was opened. The skills SVG download locator is `sources/wiki-241080062/r1/content.json#/attachments/results/0/links/download`.

## Per-page registry (all 42 direct links)

Locator convention: **P/i** means the exact pointer `sources/wiki-238324523/r1/content.json#/pages/i` (line `8+i`). Every row is included because it occurs there; reason column is only provisional title-based relevance unless saved metadata supports it. **U** = no saved body/access-result/metadata/index under that page ID, historically and currently uncollected; access unknown. **BMA** = need body extraction, metadata (observed URL, actual retrieval time, external version if available, digest/method/limitations) and attachment index with pagination/exact zero or explicit failure. All U rows need BMA, conditional on supervisor scope confirmation. **H** adds a hold for ambiguity, not permission to traverse.

| P/i | Stable ID | Snapshot title | Revision/current state | Inclusion relevance / ambiguity | Exact remaining packet need |
|---|---|---|---|---|---|
| P/0 | 241082618 | Декомпозиция | U | Generic planning; admin relevance needs confirmation | H: BMA |
| P/1 | 245670575 | Декомпозиция задач: диалоги | U | Dialog planning | BMA |
| P/2 | 241085260 | Системный анализ | U | Generic analysis; boundary unknown | H: BMA |
| P/3 | 241085256 | API | U | Generic API; boundary unknown | H: BMA |
| P/4 | 238347066 | /skills - Каталог навыков | U | Skills listing | BMA |
| P/5 | 238352321 | /skills/{id} - Карточка навыка, описание | U | Skills detail | BMA |
| P/6 | 241074633 | /skills/{id}/monitoring - Мониторинг навыка | U | Skills monitoring | BMA |
| P/7 | 241080643 | /dialogs - Список диалогов | U | Dialog listing | BMA |
| P/8 | 241083649 | /dialogs/{id} - Карточка диалога | U | Dialog detail | BMA |
| P/9 | 238350232 | /reports и /reports?tab=builder - Шаблон и конструктор отчётов | U | Reports | BMA |
| P/10 | 241102892 | RBAC - Роли, ресурсы и разрешения | U | Auth/permissions retained, not implementation approval | BMA |
| P/11 | 241092173 | Группы данных | U | Cross-cutting data; boundary unknown | H: BMA |
| P/12 | 241076726 | Модель данных | U | Cross-cutting data; boundary unknown | H: BMA |
| P/13 | 245678373 | Ролевая модель МПММ | U | Broad MPMM roles; establish admin relevance first | H: BMA |
| P/14 | 241077052 | Бизнес-анализ: Админка | U | Admin overview | BMA |
| P/15 | 243776365 | Бизнес-анализ: Диалоги | r1 saved, v13 | Metadata ties to MOS-773 | None for body/metadata/index; review separate |
| P/16 | 241080062 | Админка. Навыки | r1 saved, v17; readable derivative | Metadata ties to MOS-774/MOS-782 | None for body/metadata/index; SVG body uncollected |
| P/17 | 245673187 | Бизнес-анализ: Поверхности | r1 saved, v18 | Metadata ties to MOS-783 | None for body/metadata/index; review separate |
| P/18 | 247734813 | Раздел Обратная связь | r1 text extraction, v11 | Explicit feedback section | Attachment index; conditional structural body; prototype body pending |
| P/19 | 247737907 | Раздел База знаний | U | Optional knowledge base retained | BMA |
| P/20 | 247747489 | Раздел Состояние системы (рубильники) | U | System controls | BMA |
| P/21 | 247744768 | Раздел Шаблоны ответов | U | Response templates | BMA |
| P/22 | 247751846 | Раздел Справочники | U | Dictionaries | BMA |
| P/23 | 247747363 | Раздел API | U | Admin API section; not necessarily wire contract | BMA |
| P/24 | 247742436 | Раздел А/В Тестирование | U | Optional A/B testing retained | BMA |
| P/25 | 250794931 | Фильтрация списков | U | Cross-cutting list filters | BMA |
| P/26 | 241085263 | Черновые документы/заметки | U | Draft/container relevance unresolved | H: BMA |
| P/27 | 241080088 | Админка. Состояние системы | U | System state; not interchangeable with P/20 | BMA |
| P/28 | 247728705 | Бизнес-анализ: Команды | U | Teams | BMA |
| P/29 | 241080065 | Админка. Поверхности | U | Surfaces; distinct from saved P/17 | BMA |
| P/30 | 241080071 | Админка. Диалоги | U | Dialogs; distinct from saved P/15 | BMA |
| P/31 | 241080068 | Админка. Песочница | U | Sandbox | BMA |
| P/32 | 241080082 | Админка. Отчеты | U | Reports; distinct from P/9 | BMA |
| P/33 | 241080100 | Админка. Команды и доступ | U | Teams/access | BMA |
| P/34 | 241080097 | Админка. Заглушки | U | Stub/fallback section | BMA |
| P/35 | 241080080 | Админка. Дашборд | U | Dashboard | BMA |
| P/36 | 238329164 | Бизнес-анализ: Аутентификация и сеанс | U | Auth/session retained, not new auth authorization | BMA |
| P/37 | 238333356 | Бизнес-анализ: Роли и права | U | Roles/permissions retained | BMA |
| P/38 | 238324852 | Ассессмент навыков | U | Assessment boundary explicitly ambiguous | H: BMA |
| P/39 | 243761671 | Аналитическая справка по существующей админке МПММ | U | Historical/broad MPMM; relevance needed | H: BMA |
| P/40 | 243765248 | Бизнес-анализ. МПММ | U | Broad MPMM; relevance needed | H: BMA |
| P/41 | 250781168 | Журнал вопросов - для админки ЦАМ | U | Admin decision/question context | BMA |

There are 10 H rows and 28 other U rows. H is a proposed prioritization hold, not a claim of irrelevance; all 42 remain in the registry. Similar titles do not establish duplicates, supersession or semantic equivalence. Distinct IDs retain independent dispositions, especially surfaces, dialogs, reports, API, system state and auth families.

## Later packets and preserved failure history

| ID outside root 42 | Historical → current saved state | Provenance / effect on this registry |
|---|---|---|
| 241082009 | r1 collection-failed, `Failed to fetch`, HTTP and retrievedAt null → r2 HTTP 200, v5, 2026-10-16T12:28:15.837Z; body/metadata and zero-item attachment index | MOS-959 description link in metadata. Keep failed record. Later success does not explain failure; zero addition to root coverage |
| 241097511 | r1 HTTP 404, retrievedAt null → r2 HTTP 200, v6, 2026-10-16T12:37:03.295Z; body/metadata and zero-item attachment index | MOS-1018 description evidence in r1; r2 retains priorAttempt. Keep 404 without inferring deletion/permissions/business API absence; zero addition to root coverage |
| 241088180 | r1 HTTP 200, v4, 2026-10-16T13:03:14.658Z | Operations Jira comment membership; saved body and zero-item index; outside 42 |
| 241092242 | r1 HTTP 200, v4, 2026-10-16T13:03:14.883Z | Operations Jira descriptions; saved body and zero-item index; outside 42 |
| 241085838 | r1 HTTP 200, v3, 2026-10-16T13:31:51.607Z | Reports Jira descriptions; saved body and zero-item index; outside 42 and not in checkpoint r2 |
| 241085439 | r1 HTTP 200, v15, 2026-10-16T13:31:52.139Z | MOS-1015 description; saved body and zero-item index; outside 42 and not in checkpoint r2 |

Checkpoint r2 is supplemental, not replacement inventory: its four wiki entries have **zero intersection** with the root 42. Current canonical wiki directories contain root + four root-linked IDs + six additional IDs = 11 unique page IDs. Two `-readable` directories are derivatives, not pages or external revisions. `wiki-241080062-readable/r1` derives from canonical r1/v17; `wiki-241097511-readable/r1` derives from canonical **r2/v6**, not its failed r1. Their 2026-10-19 derivedAt values are not new retrieval dates. Original hash references match the recomputed canonical hashes; chunk/readable integrity was not independently rechecked here.

## Bounded requests for supervisor validation (not executed)

Every request stops at the named page(s) and their attachment **index**; no recursive page traversal or automatic attachment downloads. An access failure must retain observed URL, exact result, actual timestamp if returned, and explicit body/index gaps. Resolve observed destination URLs from saved evidence or a separately approved root reread; do not synthesize page/API URLs from IDs.

1. **P0 — Root provenance, one page (238324523).** First recover legitimate existing capture metadata if available; do not backdate it. If unavailable, retain r1 gap and ask collector for a new separately versioned root snapshot with observed hrefs, actual timestamp, available external version, method/hash and attachment index. Reconcile against—not overwrite—the 42-set. No child traversal is authorized by this request.
2. **P0 — Feedback packet, one page (247734813).** Using its saved metadata URL, collect attachment index including pagination; request bodyView only for structural/table evidence lost by textContent. Preserve r1 extraction. Inventory the already linked prototype without executing/downloading it under this request.
3. **P1 — One compact admin context batch (241077052, 250781168).** BMA for overview and question journal after supervisor confirms relevance; stop at these two pages. Their answers may guide subsequent bounded requests, not authorize all linked material.
4. **P1 — Skills batch (238347066, 238352321, 241074633), then dialogs batch (245670575, 241080643, 241083649, 241080071).** Separate collector units of three and four pages; BMA, no substitution from already saved similarly titled pages.
5. **P1 — Auth/access batch (241102892, 238329164, 238333356, 241080100).** Four BMA packets after confirmation; preserve deferred implementation boundaries. Hold broad MPMM role page 245678373 for scope decision rather than bundling it automatically.
6. **P2 — Remaining explicit admin candidates, separate batches:** optional (247737907, 247742436); reports (238350232, 241080082); system state (247747489, 241080088); templates/dictionaries (247744768, 247751846, 241080097); teams/surfaces (247728705, 241080065); admin tools (247747363, 250794931, 241080068, 241080080). Each batch ≤4 pages, BMA only. Together requests 3–6 cover exactly the 28 non-H uncollected rows, without omission or duplicate IDs.
7. **Scope decision first, zero collector navigation yet:** 241082618, 241085260, 241085256, 241092173, 241076726, 245678373, 241085263, 238324852, 243761671, 243765248. Ask supervisor to bind each to a named admin scenario or retain unresolved status. Assessment and historical/general MPMM are explicitly not authorized by title alone. If approved, split into individually bounded BMA requests.
8. **Conditional attachment body requests, not part of index closure:** only skills SVG 245672060 and feedback's observed prototype are presently identified here. First establish scenario need; use saved exact locators; save inert bytes/metadata if separately approved. Do not execute prototype HTML or enumerate arbitrary related attachments. Empty saved indexes for dialogs/surfaces do not require blanket recollection solely to make counts look complete.

## Architecture / Start Here

Evidence flow: one root extraction → checkpoint r1 discovery pointers → canonical packet directory by stable page ID → supplemental checkpoints/current filesystem → derivatives retaining original provenance. Status resolution is ID-based, never title-based. Start with `sources/wiki-238324523/r1/content.json` lines 7–50 and the table above, then inspect each canonical metadata/index packet; do not start from a global saved-source count.

## Validation and residual risks

Read-only local JSON parsing, directory discovery and SHA-256 inspection performed; no network, tests, builds, browser activity or delegation. Only this requested report was written; no shared registry/checkpoint/spec/source was edited. Tests/builds intentionally not run (inventory-only task and explicit prohibition).

Residual risks: missing root metadata/version/individual hrefs; 38 missing bodies/metadata/indexes; 10 provisional scope holds; flattened feedback tables and absent attachment index; attachment bodies not collected; live freshness and origin not independently verified; derivative chunk integrity not checked; current directories can exceed historical checkpoint coverage. These limit evidence readiness, not the verified 42-entry accounting. No global completeness or G1 acceptance claim.
