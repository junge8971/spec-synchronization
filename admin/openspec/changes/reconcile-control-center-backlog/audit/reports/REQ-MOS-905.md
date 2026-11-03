# Code Context

## Files Retrieved

All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/` (A). This is a requirements-only evidence audit, not an implementation review.

1. `work-items/REQ-MOS-905.md` (lines 1–9): bounded assignment.
2. `sources/jira-shell-details/r1/metadata.json` (lines 1–51): collection provenance, checksum, saved comment counts and collection limitations.
3. `sources/jira-shell-details/r1/content.json`: selectively parsed `/items/0` (MOS-624, key at line 14), `/items/3` (MOS-674, key at line 126), `/items/5` (MOS-905, lines 204–231), plus root provenance fields. No other issue body was examined. JSON pointers below are authoritative locators.

## Verified provenance

- Independently computed SHA256 over the exact content bytes: `30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4`; size **14311 bytes**. Both match metadata `/sha256` and `/bytes` and the assigned digest.
- Content `/sourceId` and metadata `/sourceId` are `jira-shell-details`; both `/retrievedAt` values are `2026-10-16T12:45:22.199Z`.
- Verified selected keys: `/items/0/key` = `MOS-624`, `/items/3/key` = `MOS-674`, `/items/5/key` = `MOS-905`. Per-item retrieval timestamps respectively `2026-10-16T12:45:21.394Z`, `2026-10-16T12:45:22.008Z`, `2026-10-16T12:45:22.198Z`.
- Metadata `/collection` describes a parent same-origin read-only GET from a verified Jira origin with an exact allowlist, selected fields/comments and attachment metadata only. This is a **saved provenance assertion**, not independently revalidated remote origin/authenticity.
- Metadata `/membership` asserts `jira-hierarchy/r1/content.json results[0] MOS-624; members 672/673/674/904/905`. The hierarchy source was not consulted; selected items each have `parent: null`. Do not turn the membership assertion into a direct parent-field relationship.
- Saved comments are complete by counts only: content `/items/0/comments` has startAt 0, total 0, zero items; `/items/3/comments` startAt 0, total 1, one item; `/items/5/comments` startAt 0, total 2, two items. Metadata `/comments/0`, `/comments/3`, `/comments/5` agree and mark complete. No claim about subsequent live comments is made.

## Key Code — atomic candidate requirements (no code inspected)

`C` below means `sources/jira-shell-details/r1/content.json`. Stable IDs represent extracted candidates, not completed tasks or independently approved specifications. Each clause locator includes its exact source wording because multiple clauses occupy one JSON string.

| ID | Candidate requirement | Exact locator / source clause |
|---|---|---|
| REQ-MOS-905-001 | Default home leads to skills rather than a separate overview dashboard. This is distinct from the no-skill-permission fallback. | C `/items/5/description` (line 207): `Главная нового прототипа ведёт в навыки вместо отдельного обзорного дашборда.` |
| REQ-MOS-905-002 | Add `/skills/new`. | C `/items/5/description`: `Добавить /skills/new` |
| REQ-MOS-905-003 | Add `/surfaces/new`. | C `/items/5/description`: `/surfaces/new` |
| REQ-MOS-905-004 | Add a surface card route/page; exact path is not specified. | C `/items/5/description`: `карточки поверхности` |
| REQ-MOS-905-005 | Add a dialogue card route/page; exact path is not specified. | C `/items/5/description`: `и диалога` |
| REQ-MOS-905-006 | Add `/teams`. | C `/items/5/description`: `/teams` |
| REQ-MOS-905-007 | Add `/ops`. | C `/items/5/description`: `/ops` in the add-routes sentence |
| REQ-MOS-905-008 | Support prototype `/metrics` with compatibility for existing `/dashboard`. | C `/items/5/description`: `Поддержать /metrics и /docs из прототипа с совместимостью существующих /dashboard и /documentation.` |
| REQ-MOS-905-009 | Support prototype `/docs` with compatibility for existing `/documentation`. | C `/items/5/description`: same compatibility sentence as -008 |
| REQ-MOS-905-010 | Preserve the explicit basename `/tsam-panel`. | C `/items/5/description`: `Сохранить basename /tsam-panel.` |
| REQ-MOS-905-011 | Redirect legacy `/domains` to its corresponding tab; destination is unspecified. | C `/items/5/description`: `Старые /domains, /review, /audit, /ops/stubs и /ops/maintenance перенаправлять на соответствующую вкладку` |
| REQ-MOS-905-012 | Redirect legacy `/review` to its corresponding tab; destination is unspecified. | C `/items/5/description`: same legacy-route clause as -011 |
| REQ-MOS-905-013 | Redirect legacy `/audit` to its corresponding tab; destination is unspecified. | C `/items/5/description`: same legacy-route clause as -011 |
| REQ-MOS-905-014 | Redirect legacy `/ops/stubs` to its corresponding tab; destination is unspecified. | C `/items/5/description`: same legacy-route clause as -011 |
| REQ-MOS-905-015 | Redirect legacy `/ops/maintenance` to its corresponding tab; destination is unspecified. | C `/items/5/description`: same legacy-route clause as -011 |
| REQ-MOS-905-016 | Preserve other query parameters on all five legacy-to-tab redirects above. | C `/items/5/description`: `с сохранением прочих query` |
| REQ-MOS-905-017 | For a role without skills access, use the agreed accessible entry point, not an unconditional skills landing. The destination and permission rule are not supplied here. | C `/items/5/description`: `Для роли без навыков использовать согласованную доступную точку входа.` |
| REQ-MOS-905-018 | Historical breadcrumb baseline: create breadcrumbs and display them automatically on every page. MOS-905 names breadcrumb refinement but supplies no replacement rules. | C `/items/3/description`: `Создать хлебных крошек и сделать так чтобы они автоматически отображались на каждой странице`; C `/items/5/summary`: `[FE][Общая оболочка] Доработать маршруты, вкладки и хлебные крошки` |

The ordered compatibility pairs -008/-009 preserve the wording's natural pairing; the description does not itself prescribe canonical redirect direction or status. No invented paths, tab identifiers, query keys, collision precedence, push/replace semantics, or fallback destination are included. The comment below names `/skills` explicitly; the description names the skills destination without spelling its path.

### Claims and references, not acceptance/implementation evidence

- C `/items/5/comments/items/0` (ID `1117971`, body line 220): reports `/metrics`, `/docs`, old-address redirects and home → `/skills`; skills, teams and operations tabs synchronized with URL and history; placeholder pages for new sections/cards; updated menus, breadcrumbs and documentation links. These are implementation **claims**. URL/history synchronization is a comment-derived follow-up candidate, not a description-level requirement proven implemented. It specifies neither back/forward behavior nor history replacement. Placeholders do not establish business CRUD delivery.
- C `/items/5/comments/items/1` (ID `1118004`, body line 226): a mention in MR `9` of `tsam / front / tsam-assistant-management-front`, branch `MOS-905`, with title `feat: MOS-905 дорабатывает маршруты и хлебные крошки`. No link was followed; merge, code content, correspondence to this local checkout and deployment are unverified.
- C `/items/5/status` is `Ready for test`; `/items/5/updated` is `2026-10-16T19:22:22.081+0800`. Neither is test success or completion evidence.
- C `/items/3/status` is `CLOSED`. C `/items/3/comments/items/0` (ID `1114562`) says `Протестировано успешно на контуре: [https://mobile-a-tech.mos.ru/tsam-panel]` and references an image. This is a historical test claim for MOS-674 only, not fresh testing, current deployment, or MOS-905 acceptance.
- C `/items/0` supplies provenance context: summary `[KR] Каркас административной панели`, status `Backlog`, description's generic development lifecycle and documentation links to wiki pages `223087110` and `222659162`. Its `для пользователя изменений не будет` statement is parent-context wording, not grounds to cancel MOS-905's explicit navigation changes. No atomic routing requirement is derived from that generic lifecycle.

## Architecture and boundaries

The evidence concerns shell navigation: basename → default entry or separately agreed accessible fallback → routes/compatibility addresses → tab redirects preserving other query parameters → automatic breadcrumb baseline. It does not establish current local ownership or implementation. LOCAL-001/002 and route code were not consulted; there is no implementation audit or code-change recommendation.

The permission-related sentence is retained as a requirement with an unresolved agreed destination, **not analyzed into a new auth policy**. No auth artifacts were needed/read because no auth design or implementation conclusion is made. Any subsequent auth examination must first read the approved `integrate-mpmm-auth-permissions` proposal/design/specs. Existing approved shared-session, UI-permission/backend-authorization, mock-mode and deferral boundaries remain untouched. This report does not authorize new login/session APIs, mock role enforcement, deferred business features, task closure, activation or deployment.

## Gaps, limitations and questions

1. What is the agreed default home path contract? `/skills` is explicit in comment `1117971`, whereas the description states skills semantically. Which already-agreed accessible entry point and existing permission interpretation govern the no-skills fallback? No policy/destination is invented here.
2. What exact destination route, tab identifier and query key correspond to each of `/domains`, `/review`, `/audit`, `/ops/stubs`, `/ops/maintenance`? What happens when existing query parameters collide with the target tab parameter? Preservation of *other* query is explicit; precedence is not.
3. Does compatibility require redirects from `/dashboard` and `/documentation`, or another alias mechanism? What are canonical addresses, history push/replace, and back/forward expectations? The comments alone do not settle these.
4. What are the exact surface/dialogue card paths and identifiers? What breadcrumb labels, hierarchy, clickability and dynamic-card naming are required? Are URL/history-synchronized tabs from the comment approved acceptance criteria?
5. Metadata `/limitations/0–2` and C `/limitations/0–2` state custom fields and attachment bodies were not collected, and comment pagination is as reported. No missing custom-field criteria can be inferred.
6. C `/items/3/attachments/0–2` contains metadata only: image `817144` (`image-2026-09-03-13-36-19-668.png`, 8078 bytes), image `825968` (`image-2026-09-22-16-44-42-595.png`, 3319 bytes), HTML prototype `817143` (`Прототип ЦАМ, версия MVP.html`, 1158654 bytes). Their bodies/visuals were not examined or executed. C `/items/0/attachments` and `/items/5/attachments` are empty in this saved selection; this is not a claim about live attachments.
7. C `/items/5/description` references contracts wiki `241097511` (domains/skills catalog), `241082009` (surfaces), and `241080659` (teams). No links were followed. Linked catalog/surface snapshots were not examined; business API/CRUD evidence cannot substitute for shell-routing UX. The assignment identifies teams wiki `241080659` as uncollected here.
8. No tests, browser, network, builds, source edits, plan edits or Git mutation were performed. Saved snapshots cannot establish current implementation or runtime behavior. None of the above ambiguities blocks this bounded extraction; they remain questions for reconciliation, not invitations to invent contracts.

## Start Here

Open `sources/jira-shell-details/r1/content.json` at `/items/5/description` (line 207) first: it is the new routing requirement source. Keep `/items/5/comments` (lines 214–231) separate as reported work, and `/items/3/description` as the historical breadcrumb baseline.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Extracted 18 stable atomic candidates with exact source pointers; verified content hash, byte size, selected keys and saved comment counts; separated description requirements from comments/status/MR/test claims."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-905.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python JSON selection and SHA256/byte-count verification of jira-shell-details/r1/content.json","result":"passed","summary":"Assigned digest and 14311 bytes match; selected issue keys and saved counts verified."}],
  "validationOutput": ["SHA256 30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4; selected keys MOS-624/MOS-674/MOS-905; comment counts 0/1/2 match totals."],
  "residualRisks": ["Attachment bodies/custom fields unavailable; teams contract uncollected; tab destinations, collision/history semantics, fallback and card paths unspecified; implementation and deployment not assessed."],
  "noStagedFiles": true,
  "diffSummary": "Sole authorized report written; no source/product/plan edits or staging performed.",
  "reviewFindings": ["No input blockers for bounded extraction; unresolved contract questions documented."],
  "manualNotes": "Independent local evidence reading only. No tests or external links followed. noStagedFiles describes this worker's actions, not an inspected repository-wide staging state. Independent review remains pending."
}
```
