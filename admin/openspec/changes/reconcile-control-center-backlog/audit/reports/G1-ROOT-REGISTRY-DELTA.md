# G1-ROOT-REGISTRY-DELTA

## Result and boundary

Incremental local reconciliation of the **accepted 42 direct-root IDs**, not a new inventory census or semantic audit. **18 IDs now have canonical saved body/extraction packets (14 additions to the baseline four); 24 have no canonical packet.** The 18 include three containers and one image-only overview extraction: this is not 18 substantively reconciled requirements sources. **17 of the 18 have returned attachment indexes; feedback 247734813 lacks its index.** All 17 saved indexes have `next: null`; no saved pagination continuation is indicated. The 24 absent packets also lack indexes.

All ten former holds were authorized by D-031, captured, and classified under D-032. Their old pending/held wording is historical, not a current permission blocker. No current root page is marked inaccessible: browser discovery timeout before a page request is not HTTP403/404.

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`. Only this report is written. No source, registry, decision, checkpoint, code, spec or task checkbox changes. Independent review/parent acceptance of this delta remains separate.

## Files Retrieved

- `work-items/G1-ROOT-REGISTRY-DELTA.md:1–11`: bound assignment.
- `reports/G1-WIKI-ROOT-REGISTRY.md:1–122`: accepted baseline, original gaps and collector groupings; unchanged states explicitly reused below.
- `sources/wiki-238324523/r1/content.json:1–53`, `sources/wiki-238324523/r2/links.txt:1–42`, `sources/wiki-238324523/r2/metadata.json:1–15`: established membership and observed hrefs.
- `decisions.md:3–95`: D-022–D-032 dispositions and correction histories.
- `collection-D031-held-pages.json:1–203`: ten capture receipts; pending-classification wording superseded by D032.
- `coverage-partial-r7.json` through `coverage-partial-r13.json`: complete parsed revision records, no global inventory reread.
- `sources/wiki-241077052/r1/metadata.json:1–15`, `sources/wiki-250781168/r1/metadata.json:1–24`, `sources/wiki-247751846/r1/metadata.json:1–20`, `sources/wiki-247747363/r1/metadata.json:1–20`; each of the ten D031 metadata paths explicitly listed below, lines 1–22: parsed metadata and canonical file existence. JSON envelope/index fields were inspected without semantic reinspection of HTML bodies. `sources/wiki-241077052/r1/content.md:1–25` supplies the selected image-only extraction/index.
- `reports/REL-D031-PLANNING-API.md:1–86`, `reports/REL-D031-DATA-DRAFTS.md:1–100`, `reports/REL-D031-MPMM-ASSESSMENT.md:1–100`: accepted classification reuse, not fresh adjudication.
- `reviews/R-REL-D031-PLANNING-DATA.md:1–44`, `reviews/R-REL-D031-MPMM-ASSESSMENT.md:1–44`: original REVISE/ACCEPT provenance; current acceptance taken from D032.
- `sources/wiki-attachment-250805153/r1/metadata.json:1–24`, `sources/wiki-attachment-247751845/r1/metadata.json:1–24`, `sources/wiki-attachment-250800526/r1/metadata.json:1–24`, `sources/wiki-attachment-247747361/r1/metadata.json:1–24`: parent/version attribution and saved inert text; content.txt existence checked, bodies not re-audited.
- `reports/ATTACH-DICTIONARY-PROTOTYPES.md:1–44`, `reports/ATTACH-API-PROTOTYPES.md:1–44`: selected review ranges and non-whole-attachment acceptance.

## Current 42-row ledger

`P/i` reuses baseline pointer `sources/wiki-238324523/r1/content.json#/pages/i`; observed saved href is root r2 `links.txt` line `i+1`. Titles are baseline labels, not a claim of r1/r2 title equality. Every captured canonical packet is `sources/wiki-ID/r1/`; v is external wiki version. Derivatives are not new pages.

**U/reused** = unchanged baseline uncollected state, exact canonical directory absence locally checked; access unknown. Need **BMA**: body/extraction, provenance metadata, attachment index. **B/reused** = baseline packet retained without new semantic audit. **Δ** = addition since baseline. **I=n** = returned indexed count, exhausted saved pagination, not attachment-body review coverage.

| P/i | Exact ID | Baseline title | Current capture / disposition | Current gap or limit |
|---|---|---|---|---|
| 0 | 241082618 | Декомпозиция | Δ r1/v3, I=0; D032 PLANNING mixed subset | Classification, not full reconciliation |
| 1 | 245670575 | Декомпозиция задач: диалоги | U/reused | BMA |
| 2 | 241085260 | Системный анализ | Δ r1/v2, I=0; D032 PLANNING container | Links are not contracts/traversal authority |
| 3 | 241085256 | API | Δ r1/v2, I=0; D032 PLANNING container | Distinct from 247747363; children not thereby captured |
| 4 | 238347066 | /skills - Каталог навыков | U/reused; D032 next batch | BMA; transport blocked, no page failure |
| 5 | 238352321 | /skills/{id} - Карточка навыка, описание | U/reused; D032 next batch | BMA; transport blocked, no page failure |
| 6 | 241074633 | /skills/{id}/monitoring - Мониторинг навыка | U/reused; D032 next batch | BMA; transport blocked, no page failure |
| 7 | 241080643 | /dialogs - Список диалогов | U/reused | BMA |
| 8 | 241083649 | /dialogs/{id} - Карточка диалога | U/reused | BMA |
| 9 | 238350232 | /reports и /reports?tab=builder - Шаблон и конструктор отчётов | U/reused | BMA |
| 10 | 241102892 | RBAC - Роли, ресурсы и разрешения | U/reused | BMA; no auth implementation approval |
| 11 | 241092173 | Группы данных | Δ r1/v17, I=8; D032 DATA mixed ownership/context subset | Eight attachment bodies unread |
| 12 | 241076726 | Модель данных | Δ r1/v20, I=2; D032 DATA mixed substantive body-model subset | Two files unread; embedded ERDs saved, not fully interpreted |
| 13 | 245678373 | Ролевая модель МПММ | Δ r1/v1, I=1; D032 MPMM direct historical proposal | PNG unread; no grants/editor approval |
| 14 | 241077052 | Бизнес-анализ: Админка | Δ r1/v3, I=2; image-only structural extraction, r7 | Two images unread; not empty requirements or accepted overview semantics |
| 15 | 243776365 | Бизнес-анализ: Диалоги | B/reused r1/v13, I=0 | No snapshot BMA gap; no new semantic acceptance |
| 16 | 241080062 | Админка. Навыки | B/reused r1/v17, I=1 | SVG 245672060 uncollected/unread; readable derivative not new page |
| 17 | 245673187 | Бизнес-анализ: Поверхности | B/reused r1/v18, I=0 | No snapshot BMA gap; no new semantic acceptance |
| 18 | 247734813 | Раздел Обратная связь | B/reused r1/v11, flattened text+links | Index absent; structural body conditional; known prototype pending |
| 19 | 247737907 | Раздел База знаний | U/reused | BMA; no optional activation |
| 20 | 247747489 | Раздел Состояние системы (рубильники) | U/reused | BMA |
| 21 | 247744768 | Раздел Шаблоны ответов | U/reused | BMA |
| 22 | 247751846 | Раздел Справочники | Δ r1/v10, I=2; D027/028 corrected WD accepted | Two prototype texts saved; D029 selected findings only |
| 23 | 247747363 | Раздел API | Δ r1/v7, I=2; D027 WAR accepted | Two prototype texts saved; D029 selected API findings only |
| 24 | 247742436 | Раздел А/В Тестирование | U/reused | BMA; no optional activation |
| 25 | 250794931 | Фильтрация списков | U/reused | BMA |
| 26 | 241085263 | Черновые документы/заметки | Δ r1/v4, I=0; D032 DATA container | Twelve child labels do not establish coverage |
| 27 | 241080088 | Админка. Состояние системы | U/reused | BMA; distinct from 247747489 |
| 28 | 247728705 | Бизнес-анализ: Команды | U/reused | BMA |
| 29 | 241080065 | Админка. Поверхности | U/reused | BMA; not substituted by 245673187 |
| 30 | 241080071 | Админка. Диалоги | U/reused | BMA; not substituted by 243776365 |
| 31 | 241080068 | Админка. Песочница | U/reused | BMA |
| 32 | 241080082 | Админка. Отчеты | U/reused | BMA; distinct from 238350232 |
| 33 | 241080100 | Админка. Команды и доступ | U/reused | BMA |
| 34 | 241080097 | Админка. Заглушки | U/reused | BMA |
| 35 | 241080080 | Админка. Дашборд | U/reused | BMA |
| 36 | 238329164 | Бизнес-анализ: Аутентификация и сеанс | U/reused | BMA; approved auth boundary retained |
| 37 | 238333356 | Бизнес-анализ: Роли и права | U/reused | BMA; no new role model |
| 38 | 238324852 | Ассессмент навыков | Δ r1/v8, I=0; D032 MPMM direct operational proposal | Not checking/review activation; unfinished flows |
| 39 | 243761671 | Аналитическая справка по существующей админке МПММ | Δ r1/v3, I=0; D032 MPMM mixed historical subset | Historical estimates not verified runtime; links not covered |
| 40 | 243765248 | Бизнес-анализ. МПММ | Δ r1/v8, I=7; D032 MPMM mixed integration/historical subset | Seven PNGs unread; approved contracts first |
| 41 | 250781168 | Журнал вопросов - для админки ЦАМ | Δ r1/v8, I=0; D024/025 all five data rows dispositioned | Documentary routing only; downstream owner/implementation gaps |

## Changed-entry provenance and accepted dispositions

All fourteen retrieval dates below are **2026-10-19 UTC**; matching content files exist. Ten D031 and two dictionary/API packets save full `bodyView` strings and separate returned indexes. Journal saves `bodyView`/`bodyStorage`, with index in metadata. Overview saves selected `content.md`, not original HTML.

| ID | Exact metadata path | Retrieval time; wiki version | Disposition |
|---|---|---|---|
| 241082618 | `sources/wiki-241082618/r1/metadata.json` | 09:36:51.968Z; v3 | PLANNING/D032 |
| 241085260 | `sources/wiki-241085260/r1/metadata.json` | 09:36:52.127Z; v2 | PLANNING/D032 |
| 241085256 | `sources/wiki-241085256/r1/metadata.json` | 09:36:52.261Z; v2 | PLANNING/D032 |
| 241092173 | `sources/wiki-241092173/r1/metadata.json` | 09:37:05.459Z; v17 | DATA/D032 |
| 241076726 | `sources/wiki-241076726/r1/metadata.json` | 09:37:07.198Z; v20 | DATA/D032 |
| 241085263 | `sources/wiki-241085263/r1/metadata.json` | 09:37:07.403Z; v4 | DATA/D032 |
| 245678373 | `sources/wiki-245678373/r1/metadata.json` | 09:37:20.568Z; v1 | MPMM/D032 |
| 238324852 | `sources/wiki-238324852/r1/metadata.json` | 09:37:20.708Z; v8 | MPMM/D032 |
| 243761671 | `sources/wiki-243761671/r1/metadata.json` | 09:37:21.097Z; v3 | MPMM/D032 |
| 243765248 | `sources/wiki-243765248/r1/metadata.json` | 09:37:21.481Z; v8 | MPMM/D032 |
| 241077052 | `sources/wiki-241077052/r1/metadata.json` | 08:24:09.633Z; v3 | r7 sourceAdditions; capture, not image review |
| 250781168 | `sources/wiki-250781168/r1/metadata.json` | 08:24:54.988Z; v8 | D024/025; r7/r8 |
| 247751846 | `sources/wiki-247751846/r1/metadata.json` | 09:01:10.646Z; v10 | D027/028; r9/r10; D029 attachments |
| 247747363 | `sources/wiki-247747363/r1/metadata.json` | 09:01:11.011Z; v7 | D027; r9/r10; D029 attachments |

Exact accepted artifact chains:

- **PLANNING:** `reports/REL-D031-PLANNING-API.md` → `reviews/R-REL-D031-PLANNING-DATA.md` → D032 / `coverage-partial-r13.json`. Original **REVISE** concerned lane-local unread versus global collection wording, not classifications. Parent corrected wording, verified three captured children against the receipt, and accepted corrected report. No fresh reviewer ACCEPT invented.
- **DATA:** `reports/REL-D031-DATA-DRAFTS.md` → same review (**ACCEPT**) → D032/r13.
- **MPMM:** `reports/REL-D031-MPMM-ASSESSMENT.md` → `reviews/R-REL-D031-MPMM-ASSESSMENT.md` (**ACCEPT**) → D032/r13. Consult existing approved session/permissions/mock artifacts before genuinely new policy questions; no repeat D031 permission question.
- **Journal:** `reports/JOURNAL-FEEDBACK-AUDIENCE.md` and `reports/JOURNAL-SURFACE-MVP.md` → `reviews/R-JOURNAL-SUPPLEMENTS.md` → D024; `reports/JOURNAL-REMAINING-ROWS.md` → `reviews/R-JOURNAL-REMAINING-ROWS.md` → D025. All five rows dispositioned, not downstream reconciliation complete.
- **Dictionary:** `reports/WIKI-DICTIONARY-DETAIL.md` → original `reviews/R-WIKI-DICTIONARY-DETAIL.md` REVISE → `reviews/R-WIKI-DICTIONARY-CORRECTIONS.md` → D028. Preserve 29/10 partition and 26-chunk correction provenance; no repeat audit.
- **API section:** `reports/WIKI-API-REGISTRY.md` → `reviews/R-WIKI-API-REGISTRY.md` → D027. Distinct from generic API container and api-live publication.

## Root provenance: historical versus current

D022 accepted root r2 separately from r1. `sources/wiki-238324523/r2/metadata.json` records **2026-10-19T08:12:59.945Z**, external **v3**, 42 observed hrefs and empty exhausted index. Reuse accepted same-ordered-ID comparison; do not rederive membership. r1 still lacks metadata; r2 does not repair/backdate it. r2 is link extraction, not fresh full root body or whole tree. Loaded DOM and separately fetched version/index may differ in revision. Its then-held/uncollected-child wording is historical after D032.

## Attachment indexes, saved bodies and review coverage

The 17 indexed captured root children contain **25 returned entries**: four saved prototype texts and **21 unread bodies** (18 D031, two overview, one skills SVG). This is a subtotal over known indexes, not the whole root/global attachment population: feedback lacks an index and 24 pages lack packets. Feedback's prototype is a separate pending discovery edge, not an exhaustive attachment inventory.

| Parent | Exact indexed attachment IDs | Body/review state |
|---|---|---|
| 241092173 | 241105744, 241105743, 243764790, 243764789, 243764775, 243764773, 243764772, 243764759 | Eight unread: previews/mxfile/drafts not interpreted from names |
| 241076726 | 241078199, 241078198 | Two unread ERD files; embedded page SVG/viewer payload not equivalent to full ERD review |
| 245678373 | 245678191 | PNG unread; role prose substantive independently |
| 243765248 | 245678564, 245678561, 245678560, 245678554, 245678553, 245678547, 245678536 | Seven PNGs unread |
| 241077052 | 241080074, 241080073 | Two PNGs unread; first observed in body; not proof of absent requirements |
| 241080062 | 245672060 | SVG uncollected/unread; baseline retained |
| 247751846 | 250805153 v1, 247751845 v1 | Saved inert decoded text; D029 ADP01–10 selected findings |
| 247747363 | 250800526 v2, 247747361 v1 | Saved inert decoded text; D029 AAP01–11 selected API findings |
| 247734813 | No index; prototype at `content.json#/links/0/href` | Prototype body pending; no complete index/table assurance |

Four prototype packets: `sources/wiki-attachment-ID/r1/{metadata.json,content.txt}` for the explicit IDs above. HTTP200 times respectively 09:15:21.883Z, 09:15:21.941Z, 09:15:22.006Z, 09:15:22.071Z on 2026-10-19. Browser-decoded UTF-8 text, not independently verified original wire bytes. Metadata's “analysis pending” is historical after D029.

Inherited review limits: `reports/ATTACH-DICTIONARY-PROTOTYPES.md:18–23` lists main ranges 350–1219/1301–2253 and 285–754/829–1436, search-only intervening sections and unassessed styling. `reports/ATTACH-API-PROTOTYPES.md:12–17` records selected API ranges, excluding unrelated modules/styles/initialization. D029 accepts bounded findings via `reviews/R-ATTACH-DICTIONARY-PROTOTYPES.md` and `reviews/R-ATTACH-API-PROTOTYPES.md`, not whole-attachment semantics, rendering, execution, reachability or precedence. No repeat semantic review here.

## Historical receipts do not override current state

- Baseline 4 saved/38 missing → 18 saved extractions/24 missing via fourteen exact-ID additions, not aliases/off-root additions.
- D030/r12 pending holds → D031 permission/capture → D032/r13 classifications. Immutable receipt/metadata “pending” remains historical.
- r7 journal rows 2/4/5 pending → D025/r8 accepted documentary dispositions. No duplicate journal request.
- r9 prototypes unread → r10 saved → D029/r11 selected review. Neither “all four unread” nor “fully reviewed” is current.
- r8 outage affected managed-resource collection; r9 records recovery and MOS1321/1399/1386 plus dictionary/API captures. Not current missing packets. r13 is the new twice-timed-out skills discovery; no page request/access result.
- Baseline off-root 241082009 r1 Failed to fetch and 241097511 r1 HTTP404 already had successful r2 packets. Preserve history without reopening or counting them in 42. Other off-root Jira/API sources, attachments and readable derivatives add zero to root-page coverage.

## Next existing-authorized batches — not executed

Transport remains blocked **for this run**. This is a resume queue, not alternate-transport permission. A later authorized collector must rediscover/origin-guard through restored authorized browser transport and reconfirm observed hrefs; no synthesized URL, stale browser ID, fallback credentials or automatic child traversal. Recheck exact-ID packet presence before each batch to avoid duplicate/concurrent captures.

Each batch requests BMA only: body/extraction, actual provenance/version metadata and returned attachment index, with explicit zero/pagination or actual failure. Max four pages. Index permission is not attachment download permission. Remaining direct-root authority is retained by the work item and D030/D032, not new auth/feature implementation scope.

| Batch | Exact IDs | Root r2 links.txt lines | Existing gap |
|---|---|---|---|
| Skills first | 238347066, 238352321, 241074633 | 5, 6, 7 | D032 explicit next batch; all three canonical directories locally absent |
| Dialogs | 245670575, 241080643, 241083649, 241080071 | 2, 8, 9, 31 | Four BMA gaps |
| Auth/access | 241102892, 238329164, 238333356, 241080100 | 11, 37, 38, 34 | Documentary only, no auth model/editor approval |
| Optional | 247737907, 247742436 | 20, 25 | BMA, no activation |
| Reports | 238350232, 241080082 | 10, 33 | Distinct IDs |
| System state | 247747489, 241080088 | 21, 28 | Distinct IDs |
| Templates/stubs | 247744768, 241080097 | 22, 35 | Baseline batch minus captured dictionary 247751846 |
| Teams/surfaces | 247728705, 241080065 | 29, 30 | BMA |
| Admin tools | 250794931, 241080068, 241080080 | 26, 32, 36 | Baseline batch minus captured API 247747363 |
| Separate feedback repair | 247734813 | 19 | Index; structural body only if table-sensitive need; retain r1 |

Nine missing-page batches cover all 24 absent IDs once each. They are existing direct-root batches reduced by captures, not new traversal from D031 containers. No duplicate root provenance, journal, overview, dictionary/API or held-page capture is proposed. Similar titles never substitute for exact IDs.

**Not authorized here as downloads:** D031's 18 attachment bodies (D031 explicitly excluded downloads), two overview images, skills SVG and feedback prototype. Bind necessary bodies to a specific owner question and appropriate attachment-body authorization; do not blanket download based on names/indexes. Reuse four saved D029 prototype texts locally.

## Architecture / Start Here

Start with skills rows and D032 (`decisions.md:3–9`), then root r2 hrefs lines 5–7. Evidence flow: established root ID → canonical packet → separate index/body evidence → report/review/decision chain. Readable chunks retain parent lineage, not new external revisions. Capture, classification and attachment review are separate axes, never a single “complete” flag.

## Global gates, validation and residual risks

**This narrow ledger does not suffice for tasks 2.3, 2.4 or 2.6.** It does not settle Jira-linked source bodies/attachments, explanatory-document dispositions, broader semantic reconciliation, owner decisions or implementation mapping. D022/023 API publication increments, D026 off-root descriptions and D030 MOS1145 testplan acceptance do not close global gates. No invented global source count, inventory census or global checkbox recommendation. Latest accepted progress remains **6/28** (r13).

Residual risks: 24 missing packets; feedback index/conditional structural gap; 21 known indexed unread bodies plus unindexed prototype edge; image-only overview semantics unknown; partial prototype/diagram review; r1 root metadata absent and r2 DOM/version alignment unproved; local freshness/origin unverified; transport blocked; historical formatting failure unresolved. No source precedence/auth/product activation inferred.

Local inert JSON parsing and exact-ID file checks only. No digest recomputation; saved digest/roundtrip/acquisition claims remain attributed to metadata and accepted reports. No network/browser/MCP, credentials, source execution, code audit, tests/build/E2E, nested delegation or global census. Initial inspection assumed object-shaped root rows and failed read-only; reading actual two-element-array shape enabled corrected successful inspection. A subsequent broad report-row regex also included two batch rows; that was a validation-selector issue, not extra ledger membership. Only this report was written; source packets untouched.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "Current 42-row exact-ID ledger, fourteen changed metadata references, D032 correction history, separate body/index/review gaps and <=4-page existing-authorized batches provided."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/G1-ROOT-REGISTRY-DELTA.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command": "Initial local Python root-row inspection", "result": "failed", "summary": "Read-only AttributeError from object assumption; corrected after reading array-shaped source."},
    {"command": "Corrected local Python JSON/path inspection of established IDs and selected metadata/indexes", "result": "passed", "summary": "18 canonical extractions, 24 absent directories; next three skills IDs absent; packet and acceptance deltas reconciled."},
    {"command": "Tests/build/browser/network", "result": "not-run", "summary": "Explicitly prohibited for this task."}
  ],
  "validationOutput": ["Four baseline captures reused; fourteen additions; ten D031 classifications accepted under D032, original PLANNING REVISE retained.", "17 captured-page indexes, 25 indexed attachments: four saved selectively reviewed texts and 21 unread bodies; feedback index absent."],
  "residualRisks": ["Transport blocked; 24 canonical packet gaps and feedback index gap.", "Attachment/diagram/global Jira/explanatory-document coverage incomplete; no global closure.", "Hashes, freshness and origin not independently verified; prior formatting failure unresolved."],
  "diffSummary": "Only bound delta report written; no registries, sources, code, specs or tasks edited.",
  "reviewFindings": ["Independent acceptance of this delta pending; no fresh reviewer ACCEPT claimed."],
  "manualNotes": "Exact-ID local reconciliation, not semantic reaudit or census. Parent removed unsupported noStagedFiles attestation before independent review: this run staged nothing, but repository-wide staging was not inspected. Accepted classifications and selected prototype findings reused. Global progress remains 6/28."
}
```
