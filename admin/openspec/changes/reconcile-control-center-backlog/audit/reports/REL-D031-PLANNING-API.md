# REL-D031-PLANNING-API — relevance classification

## Scope and result

Only the three assigned saved pages were inspected. Result: **241082618 mixed with bounded relevant subset; 241085260 and 241085256 link/container-only**. This is relevance inspection, not requirement reconciliation, feature acceptance, implementation verification, scope approval, or G1 closure. No child-page traversal was performed.

All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`. Source `content.json.bodyView` is authoritative; extracted text is a locator aid, not rendered UI. Versions/dates do not establish precedence. Throughout this report, “unvisited/uninspected” means not read by this analyst, not globally absent or uncollected. Before any child follow-up, check the current saved-source inventory and existing evidence owner; new collection requires an established remaining gap and a bounded authorized question.

## Files retrieved and coverage

- `work-items/REL-D031-PLANNING-API.md`: entire assignment.
- `sources/wiki-241082618/r1/metadata.json`, `sources/wiki-241085260/r1/metadata.json`, `sources/wiki-241085256/r1/metadata.json`: lines 1–26, all metadata. Each records HTTP 200, zero redactions, D-031 authorization, nonrecursive collection and inert HTML.
- `sources/wiki-241082618-readable/r1/content.txt`: lines 1–339, entire derivative body; `sources/wiki-241085260-readable/r1/content.txt`: lines 1–5, entire body; `sources/wiki-241085256-readable/r1/content.txt`: lines 1–6, entire body.
- `sources/wiki-241085260-readable/r1/body-view-chunks.json` and `sources/wiki-241085256-readable/r1/body-view-chunks.json`: lines 1–3, entire exact body chunks, establishing children-macro structure and href targets.
- `sources/wiki-241085260/r1/content.json` and `sources/wiki-241085256/r1/content.json`: lines 1–21, entire packets including body and attachment index.
- `sources/wiki-241082618/r1/content.json`: lines 12–21, redaction/index tail. Attachment indexes for all three: status 200, start 0, limit 100, size 0, next null, results empty. No attachment bytes read; no index pagination gap is indicated in these saved responses.
- `sources/wiki-241082618-readable/r1/metadata.json`: lines 1–15, derivation provenance. Hashes and exact-chunk roundtrip are parent-computed, not independently recomputed here.
- `sources/wiki-241082618-readable/r1/body-view-chunks.json`: lines 1–11 returned before the 50 KB read limit (first ten chunks), selectively corroborating headings and numbered tables through the beginning of module 2.1. Remaining exact markup was not inspected; the entire 339-line text body was inspected. No claim of full markup/link inventory for this long page.

## 241082618 — Декомпозиция

**Classification: mixed with bounded relevant subset.** Version 3, dated `2026-09-11T18:09:42.166+08:00`, retrieved `2026-10-19T09:36:51.968Z`.

This is substantive FE/BE planning, not a container. The direct Control Center subset is section **“2. Центр управления ассистентом”**, text lines 119–322, modules 2.1–2.10. Section 1, lines 1–118, contains related administrative/cross-cutting requirements but also distinct authentication, user/role administration and backend planning. Modules 3.1–3.2, lines 323–339, concern demo scenarios/documentation and provide supporting context; their acceptance as Control Center deliverables is not established here. These bounds are relevance categories, not approval or exclusion of individual backlog items.

### Exact evidence and candidate capability routing

Routing below uses names and product-scenario references **in the body**, not an application inventory or a verified implementation owner. Repository capability/spec ownership remains unverified.

| Body locator | Evidence | Candidate scenario/capability |
|---|---|---|
| Lines 120–159, module 2.1, rows 2.1.22–2.1.25, 2.1.27, 2.1.29–2.1.31, 2.1.35 | “Страница списка диалогов”; “Переписка с авторством”; “UI-конструктор с «И»/«ИЛИ» и группировкой”; “Признак сбоя, фильтр по проблеме” | Dialog registry/card/conversation/timeline, filtering, saved selections and export; body names product scenarios 26–35, 44–45, 48–52 |
| Lines 160–186, module 2.2, rows 2.2.13–2.2.19 | “Таблица с фильтрами, только свои для team”; overview, intents, checks, connection, monitoring, history | Skill catalog/card; scenarios 23, 24 and 39 explicitly referenced |
| Lines 187–219, modules 2.3–2.4, rows 2.3.12–2.3.16, 2.4.6–2.4.7 | “Показатели, зависимости, инциденты”; disable/enable modal with reason/text | Skill monitoring, incidents, maintenance windows and skill disablement |
| Lines 220–251, modules 2.5–2.6, rows 2.5.8–2.5.11, 2.6.7–2.6.11 | Reports templates/builder, preview and aggregates; dashboard grid, editing and widgets | Reports and dashboard; export mappings marked “по аналогии” in BE rows remain analogies, not proven equivalence |
| Lines 252–284, modules 2.7–2.8, rows 2.7.7–2.7.9, 2.8.11–2.8.14 | Stub/maintenance tabs; four-step skill wizard, sandbox, review and tokens | Stubs/maintenance and skill onboarding |
| Lines 285–322, modules 2.9–2.10, rows 2.9.12–2.9.19, 2.10.7–2.10.9 | Surface registry, registration wizard/configurator/connection/history; domain registry/create/edit/card | Surfaces and domains; indirect product mappings remain explicitly indirect |
| Lines 49–64, module 1.4, rows 1.4.8–1.4.11 | Team registry/card, membership and object links | Teams, product scenarios 4–13 |
| Lines 65–118, modules 1.5–1.8 | Security and object-action journals; “Состояние системы”; parameters and dictionaries | Audit/security journals, platform-module state, settings/dictionaries; body references 14–19 and 39–47 |
| Lines 2–48, modules 1.1–1.3, rows 1.1.8, 1.1.10, 1.3.9 | User header, access-denied route, “Использование прав для показа/скрытия элементов” | Current profile and permission-aware navigation, scenarios 21, 22, 38; auth/role-management ownership needs separate semantic review |
| Lines 323–339, modules 3.1–3.2 | `POST /api/v1/demo/reset`; “Страница «Сценарии показа»”; documentation two-column page, scenario 20 “косвенно” | Demo/documentation context; existing owner unknown |

Exact-markup corroboration includes anchors `id-Декомпозиция-1.Административныйинтерфейс(Аттестуемаячасть)` and `id-Декомпозиция-2.Центруправленияассистентом`, table headers “№ / Наименование задачи / Описание / Задача продуктолога”, and stable numbered row identifiers above.

**Limits and follow-up:** row 1.1.1 proposes OIDC, 1.1.9 says “Logout в СУДИР”, and 1.3.8 proposes a roles/permissions editor. Relevance does not authorize these or supersede agreed MPMM session/permission boundaries. Any future reconciliation must separately resolve authority/scope against agreed changes without choosing the newer date. BE tables, API paths and technology suggestions are planning evidence, not verified API contracts or frontend implementation obligations. Product references such as “(Д-6)”, “(Д-14)”, “(Д-15)” and “ответ к п.48” are unresolved textual references, not Jira identifiers or permission to collect additional sources. No arbitrary keys were added to an allowlist. No linked sources were visited; full long-page markup/link completeness is not claimed.

## 241085260 — Системный анализ

**Classification: link/container-only.** Version 2, dated `2026-09-09T12:51:49.608+08:00`, retrieved `2026-10-19T09:36:52.127Z`.

Entire body is a `ul.childpages-macro` with `data-macro-name="children"`, `data-hasbody="false"`, `data-content-id="241085260"`. It has exactly five list-item links, no requirement prose, schema or policy rules. Exact locator: `sources/wiki-241085260/r1/content.json:11`, also exact chunk JSON line 2; text lines 1–5 correspond in order:

1. `241085256` — API, `/spaces/KR/pages/241085256/API`. Independently assigned and read in this report; its children were not read.
2. `241102892` — RBAC - Роли, ресурсы и разрешения — **unvisited**.
3. `241092173` — Группы данных — **not read by this analyst; already captured under D-031**, classified in `reports/REL-D031-DATA-DRAFTS.md`.
4. `241076726` — Модель данных — **not read by this analyst; already captured under D-031**, classified in `reports/REL-D031-DATA-DRAFTS.md`.
5. `245678373` — Ролевая модель МПММ — **not read by this analyst; already captured under D-031**, classified in `reports/REL-D031-MPMM-ASSESSMENT.md`.

Candidate routing: API/navigation index and system-analysis context. No substantive owner established for this container; link labels suggest access-control/data-model subjects only. Follow-up first consults `collection-D031-held-pages.json`, the named companion reports and current global inventory. Reuse the three already captured bodies and their existing classification owners rather than recollecting them. The remaining child's global status must be checked separately, not inferred from absence in this narrow receipt. Only an established remaining evidence gap warrants a new bounded authorized collection/inspection. Neither RBAC rules nor MPMM role semantics can be inferred from this container.

## 241085256 — API

**Classification: link/container-only.** Version 2, dated `2026-09-09T12:45:48.652+08:00`, retrieved `2026-10-19T09:36:52.261Z`.

Entire body is a `ul.childpages-macro` with `data-macro-name="children"`, `data-hasbody="false"`, `data-content-id="241085256"`. Exact locator: `sources/wiki-241085256/r1/content.json:11`, also exact chunk JSON line 2. Text lines 1–6 are six child-link labels, not endpoint contracts:

| Line / child ID | Exact label / candidate capability | Coverage |
|---|---|---|
| 1 / 238347066 | `/skills - Каталог навыков` / skill catalog | Unvisited reference |
| 2 / 238352321 | `/skills/{id} - Карточка навыка, описание` / skill card | Unvisited reference |
| 3 / 241074633 | `/skills/{id}/monitoring - Мониторинг навыка` / skill monitoring | Unvisited reference |
| 4 / 241080643 | `/dialogs - Список диалогов` / dialog registry | Unvisited reference |
| 5 / 241083649 | `/dialogs/{id} - Карточка диалога (общая информация, таймлайн, ответы)` / dialog card | Unvisited reference |
| 6 / 238350232 | `/reports и /reports?tab=builder - Шаблон и конструктор отчётов` / reports | Unvisited reference |

Href targets are the corresponding `/spaces/KR/pages/<ID>/...` links in the exact chunk, not live requests. These labels permit candidate scenario routing but establish no request/response schema, method, permission, validation or error semantics. Existing repository owner remains unverified. Any API-semantic work first checks the global saved-source inventory and existing evidence owners, reusing available bodies/reports. Only established remaining gaps warrant separately bounded authorized child-body collection/inspection; this analyst's unread status does not prove global absence. No source or implementation gap follows merely from absent mappings here.

## Parent correction after independent review

R-REL-D031-PLANNING-DATA accepted the three classifications but required clarifying lane-local versus global collection status. Parent checked `collection-D031-held-pages.json`, added the three known captured children and companion-report routes, and made all child follow-up conditional on current inventory/ownership and an established authorized gap. Original REVISE review retained; no sources revisited or classifications changed.

## Validation and residual risks

Manual inspection covered all three full readable bodies, all primary metadata, both complete container bodies and all three saved attachment indexes. Only the specified report was written. No application-source traversal, network/browser/MCP, tests/build/E2E, API calls, credentials, source execution, nested delegation, spec/archive edits or policy changes occurred.

Residual risks: derivative text loses markup; long-page exact markup was only selectively inspected; hashes/roundtrip rely on parent provenance; linked-child semantics and referenced product decisions remain uninspected by this analyst, with known captured children routed to companion reports above; capability routing is document-derived and not implementation verification. Empty attachment indexes describe these saved responses only. Independent classification review and any later semantic reconciliation remain separate work.
