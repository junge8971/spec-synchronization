# REL-D031-DATA-DRAFTS — relevance classification

## Scope and evidence

Only the three assigned saved pages were classified. No contracts, implementation, other saved page bodies, remote links, attachment bytes, tests, or application code were inspected. Local JSON/HTML inspection was inert: no saved scripts, diagram viewers, or source content were executed or rendered. This report is the sole output mutation. Classification does not establish source precedence, implementation gaps, or completion of task 2.3/G1.

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`. Text line numbers are 1-based convenience locators; chunk numbers are 1-based JSON array entries, not rendered evidence. Tables/section names disambiguate chunk boundaries.

### Files retrieved

- `work-items/REL-D031-DATA-DRAFTS.md`: complete assignment.
- `sources/wiki-241092173/r1/metadata.json`: complete; saved revision r1, wiki v17 (2026-09-23T16:42:09.540+08:00).
- `sources/wiki-241092173-readable/r1/content.txt`: complete lines 1–39; `body-view-chunks.json`: complete chunks 1–4 inspected as inert HTML.
- `sources/wiki-241076726/r1/metadata.json`: complete; saved revision r1, wiki v20 (2026-09-09T19:42:42.531+08:00).
- `sources/wiki-241076726-readable/r1/content.txt`: complete lines 1–516; `body-view-chunks.json`: parsed for headings, links, image context and selectively inspected chunks, especially 1–3, 8, 10–12, 28–29. Not a complete graphical ERD interpretation.
- `sources/wiki-241085263/r1/metadata.json`: complete; saved revision r1, wiki v4 (2026-09-09T13:18:42.839+08:00).
- `sources/wiki-241085263-readable/r1/content.txt`: complete lines 1–12; `body-view-chunks.json`: complete chunk 1.
- Each corresponding `sources/wiki-ID/r1/content.json`: envelope and complete `attachments` index inspected through local JSON parsing. All three saved page/index statuses are 200; attachment counts 8/2/0 respectively, each `next: null`.

Saved metadata records retrieval on 2026-10-19 and existing SHA-256 values. Hash integrity and parent roundtrip computations were not independently verified here; no such verification is claimed.

## 241092173 — Группы данных

**Classification: mixed scoped subset, chiefly supporting ownership/context evidence.** This is not merely a diagram/file container: two actual HTML tables assign entities to named modules and systems. It does not independently specify complete UI workflows.

| Body locator (v17/r1) | Relevance and candidate scenario owner |
| --- | --- |
| Lines 1–9; first table “Административный интерфейс”, chunk 1 | User → Аутентификация и сеанс; Role/Permission/UserRole/RolePermission → Роли и права; SecurityAudit/ActionAudit → respective audit journals. All explicitly marked МПММ. Supporting integration boundary, not authorization to implement local role administration or audit MPMM. |
| Lines 12–19; second table “Центр управления”, chunks 1–2 | Skill → Каталог навыков; SkillIntent and MonitoringDependency → Подключение навыков; SkillConflict/SkillMonitoring/SkillMetric → Мониторинг навыков; SkillDisable → Отключение навыка. These are explicitly ЦУ-owned. Incident is monitoring-related but marked ЕСК. |
| Lines 20–27; second table, chunks 2–3 | Dialog, Message, MessageRating, RouteStep, OperatorAction, Participant, Category, Operator → Диалоги, marked ЕСК. Relevant supporting data for the named admin scenario, not ownership of an operator application or permission to audit ЕСК. |
| Lines 28–37; second table, chunk 3 | Channel/Surface/SurfaceConfig → Поверхности; ReportTemplate/Report/Export → Отчёты; DocumentationArticle → Оболочка и документация; Module → Модули платформы; Team → Команды. Explicit ЦУ ownership supports routing future questions to these scenarios. |
| Lines 38–39; drawio macros, chunks 3–4 | Hidden diagram names and viewer configuration, not readable diagram model contents. No relationships or coverage inferred from those names. |

### Uninspected attachment inventory and bounded collection rationale

All eight attachment bodies remain unread. Names below are index evidence only:

- `241105744` — `Диаграмма без названия-1789392199936.png`, version 12; `241105743` — same basename without suffix, mxfile, version 12.
- `243764790` — `Диаграмма без названия-1789642341384.png`, version 2; `243764789` — same basename without suffix, mxfile, version 2.
- `243764773` — `Диаграмма без названия-1789642220950.png`, version 1; `243764772` — same basename without suffix, mxfile, version 1.
- `243764775` — `~Диаграмма без названия-1789642220950.tmp`, drawio draft, version 1.
- `243764759` — `~Диаграмма без названия-1789642127849.tmp`, drawio draft, version 1.

If a later approved question requires diagram-only ownership/relationship evidence, first bound collection to the two diagram names actually embedded in chunks 3–4 and their indexed previews/source files. The other diagram and temporary drafts have no established normative role; collect only if an explicit provenance/version question requires them. No filenames prove full model coverage. No ordinary outgoing page hyperlinks were found in this body's anchor scan.

## 241076726 — Модель данных

**Classification: mixed scoped subset containing directly relevant body-model statements and supporting cross-system material.** The page has extensive embedded entity descriptions, field/type/requiredness tables, and relationship prose. It must not be classified as attachment-only or excluded wholesale because of the administrative-panel heading.

| Body locator (v20/r1) | Relevance and candidate scenario owner |
| --- | --- |
| Lines 2–13 and 14–39; entity-list tables, chunks 9–10 and 29–30 | Administrative and ЦУ entity inventories. These are body tables, not conclusions drawn from ERD attachment names. |
| Lines 42–98, 110–135; User/Role/Permission/UserRole/RolePermission/SecurityAudit/ActionAudit sections, chunks 30–35 | Supporting identity, access and audit context. Cross-system references do not expand local auth scope. Detailed role assignments/audit structures are not approval for new local administration. |
| Lines 99–109 and 136–148; Team and Module field tables, chunks 33–36 | Team describes owners of skills/surfaces; Module explicitly describes an enable/disable switch. Candidate owners: Команды and Модули платформы, supported by the groups page. Their placement under “Административная панель” does not negate this relevance or resolve architectural ownership precedence. |
| Lines 150–289; Skill through SkillMetric, chunks 36–44 | Direct model support for skill registration/catalogue, connection/intents, conflict and metric monitoring, dependencies, incidents, and disablement. Candidate owners are the corresponding named skill scenarios above. Incident remains cross-system context per the groups table. |
| Lines 290–416; Dialog through Operator, chunks 44–52 | Direct body-model support for Диалоги: messages, ratings, timeline, operator actions and participants. This does not authorize audit of ЕСК internals or implementation of all operator actions as local UI commands. |
| Lines 417–456; Channel/Surface/SurfaceConfig, chunks 52–54 | Direct model support for Поверхности, ownership and configuration. |
| Lines 457–506; ReportTemplate/Report/Export, chunks 54–57 | Direct model support for Отчёты and dialogue CSV export. Scheduling/field descriptions are candidate source statements, not a finding that approved APIs/UI must change. |
| Lines 507–516; DocumentationArticle, chunks 57–58 | Direct body-model support for Оболочка и документация. No inference of a separately approved knowledge-base module. |

Examples establishing substantive body relevance include Module's `is_enabled`/`lockable`/`fallback_text` (lines 136–148), Skill's registration/status fields (150–173), and SurfaceConfig's configuration object (449–456). These are cited as model statements only, without reconciling values, requiredness, or names to a wire contract.

### Embedded ERDs versus unread files

The original body contains two `plantumlcloud` viewer blocks: administrative ERD (chunks 1–9; encoded SVG passed to `createViewer` starts in chunk 3) and ЦУ ERD (chunks 10–29; encoded SVG begins in chunk 11 and continues through 29). Selective inert inspection confirms embedded SVG entity/link markup (e.g. User and Permission–RolePermission; Skill and Surface–Channel). Thus diagram payload exists in the saved body, even though the text convenience export omits it. Viewer JavaScript was not executed, SVG was not rendered, compressed markup was not unpacked, and complete ERD relationship interpretation is not claimed.

Separately, the attachment index lists `241078199` (`erd.png`, version 5) and `241078198` (`erd.svg`, version 5). Both attachment bodies remain unread. Their identity/equivalence to either embedded ERD and completeness are unverified. Future collection should be bounded to these exact files only if a specific unresolved visual/model relationship cannot be answered from the saved body; do not describe this task as full model coverage.

The body also contains anchors `http://Permission.id` and `http://Skill.id` in relationship context. They were not followed and are not credible authority for remote system collection; model identifiers should remain identifiers unless independently clarified.

## 241085263 — Черновые документы/заметки

**Classification: container-only.** Complete chunk 1 is a `children` macro containing twelve links; complete text lines 1–12 are their labels. There are no embedded requirements or model tables and no indexed attachments. Child-page relevance/status is unresolved, not inherited from this title or from link labels. No child body was inspected in this run.

Exact unvisited link targets are `/spaces/KR/pages/<ID>/…` in chunk 1, in the following text-line order. Candidate routes below are provisional collection subjects, not established requirement owners:

| Line / target | Label | Concrete reason for possible future bounded collection |
| --- | --- | --- |
| 1 / 241080088 | Админка. Состояние системы | Determine whether system-state material supports existing monitoring/module scenarios or is merely draft context. |
| 2 / 247728705 | Бизнес-анализ: Команды | Clarify team ownership/management narrative beyond Team model rows. |
| 3 / 241080065 | Админка. Поверхности | Establish whether it contains surface workflows rather than only draft navigation. |
| 4 / 241080071 | Админка. Диалоги | Establish the admin dialogue-view boundary versus external ЕСК operations. |
| 5 / 241080068 | Админка. Песочница | Determine sandbox relevance; this container itself provides no scenario requirements. |
| 6 / 241080082 | Админка. Отчеты | Clarify report/export scenario narrative beyond entity descriptions. |
| 7 / 241080100 | Админка. Команды и доступ | Separate team business ownership from access administration without reopening agreed auth policy. |
| 8 / 241080097 | Админка. Заглушки | Determine whether fallback text relates to existing skill/module/surface scenarios; owner otherwise unknown. |
| 9 / 241080080 | Админка. Дашборд | Determine whether a distinct approved dashboard scenario exists; label alone is insufficient. |
| 10 / 238329164 | Бизнес-анализ: Аутентификация и сеанс | Only if needed to resolve provenance within the already agreed MPMM session boundary, not to design new auth. |
| 11 / 238333356 | Бизнес-анализ: Роли и права | Only if needed to distinguish UI permission visibility from MPMM role administration; no editor approval inferred. |
| 12 / 238324852 | Ассессмент навыков | Determine whether the material belongs to a skill-review scenario or remains deferred; no scope inferred. |

These are collection candidates, not a recursive collection instruction. First check whether an authorized existing evidence owner already covers the exact target; nothing here establishes that these pages are globally uncollected.

## Boundaries and residual risks

- Retain current agreed UI/business-API scope and security/deferred boundaries. Permissions govern UI visibility; backend authorizes requests. No local role editor, new auth model, own OIDC entry, global MPMM logout, or external-system audit follows from these pages.
- Business fields such as Skill.auth_zone, Dialog.authorized and actor references are not automatically application auth context. Model physical names, logical links, and mixed snake_case/camelCase relationship prose are not wire-name requirements. No field rename, schema discrepancy, contract change, or implementation gap is asserted.
- Team/Module appear under different section groupings across the two model pages; this is supporting relevance evidence, not a resolved ownership/precedence conflict.
- Attachment bytes, rendered diagrams, child pages, contracts and implementation remain outside inspection. Existing inventory routes, if later consulted, can route questions but cannot prove missing functionality. LOCAL001 was not consulted here.
- Start with the cited body rows for an already authorized scenario-specific question; do not begin with filenames or recursively follow the draft container. Further collection requires a bounded question and the applicable authorization.

## Validation

Parent removed the unsupported `noStagedFiles: true` attestation before independent review: this run did not inspect repository staging state. No-staging activity is not an empty-index verification. Source classifications are unchanged.

Manual review covered all three complete metadata files and text bodies, source table/link/macro context as described above, and all three complete attachment indexes. Only local reads and inert parsing were used. No tests/build/browser/network or contract/code audit was run or needed for this classification.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Three assigned pages classified with revision, body locators, scenario ownership qualifications, unread inventories and bounded collection reasons."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REL-D031-DATA-DRAFTS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local Python JSON/HTML inspection of the three assigned saved sources","result":"passed","summary":"Read attachment indexes and inspected body headings, macro payload context and outgoing anchors without executing saved content."}],
  "validationOutput": ["Complete text bodies: 39, 516 and 12 lines; saved wiki versions 17, 20 and 4; indexed attachment counts 8, 2 and 0, all next=null."],
  "residualRisks": ["Attachment bytes and child pages remain unread; diagrams were not rendered or completely interpreted.","No source precedence, contract consistency, implementation completeness or task 2.3/G1 closure established."],
  "diffSummary": "Created only the bound relevance-classification report; no staging operation performed.",
  "reviewFindings": ["No blockers to the bounded classification; full-model coverage is not claimed."],
  "manualNotes": "All three text bodies and metadata files were read completely. Hash/roundtrip verification was not independently performed. No tests or application inspection performed. Repository staging state was not inspected; no files were staged by this run."
}
```
