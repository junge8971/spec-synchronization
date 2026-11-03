# REL-D031 — MPMM / assessment relevance classification

Assessment only; no scope activation, implementation finding, supersession decision, or task closure. Exactly four assigned saved pages were assessed locally. Candidate owners below are routing suggestions, not approved ownership or requirements.

## Files Retrieved

All paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

- `work-items/REL-D031-MPMM-ASSESSMENT.md` — complete assignment.
- `sources/wiki-245678373-readable/r1/content.txt` (lines 1–10), `sources/wiki-238324852-readable/r1/content.txt` (1–58), `sources/wiki-243761671-readable/r1/content.txt` (1–141), `sources/wiki-243765248-readable/r1/content.txt` (1–218): all four text bodies read fully.
- For each of those four IDs: `sources/wiki-ID/r1/metadata.json` and `sources/wiki-ID-readable/r1/metadata.json`, read fully; `sources/wiki-ID/r1/content.json`, inspected saved non-body fields, including attachment indexes only. No attachment bytes read.
- Exact `body-view-chunks.json` files were not read: text supplies sufficient evidence for the bounded classifications below; no claims about image content, destination content, or detailed visual/table layout are made.

The first combined terminal read truncated its beginning; the missing metadata and ten-line role body were reread separately. All required text bodies were therefore inspected, not inferred from titles.

## Per-page evidence and disposition

### 245678373 — Ролевая модель МПММ

**Saved revision:** r1; source v1, `2026-09-25T15:37:42.484+08:00`.

**Classification: direct admin requirement evidence (historical proposal, not current authorization).** Not an image-only container: the ten body lines state substantive behavior independently of its image.

Evidence: `sources/wiki-245678373-readable/r1/content.txt:2–6` assigns multiple roles and scopes and says role permissions govern actions in the ЦАМ panel, giving skill creation/list/deletion/edit/status examples. Lines 7–10 distinguish attribute-based visibility from action permission: “Область видимости отвечает только за доступ к просмотру данных, не регулирует функциональные действия.” Line 9 gives own/team/all skills as visibility examples.

**Candidate routing:** current Control Center permissions/UI visibility and skill/team-context scenarios; session/permissions integration owner for later semantic reconciliation. These examples do not prove existing grants, establish permission identifiers, or authorize role/scope editors. No assessment/reviewer grant can be derived from them.

**Unread / future needs:** one indexed PNG (`245678191`, `deepseek_mermaid_20260925_e80c91.png`), image bytes uninspected. An approved textual equivalent would be needed only if the diagram adds necessary semantics. Before mapping this proposal to current behavior, obtain explicit business-approved action-versus-visibility rules and the agreed current permissions contract; do not implement the historical examples as a map.

### 238324852 — Ассессмент навыков

**Saved revision:** r1; source v8, `2026-08-28T21:00:58.218+08:00`.

**Classification: direct admin requirement evidence, bounded to an operational assessment proposal.**

Evidence: `sources/wiki-238324852-readable/r1/content.txt:1–16` explicitly places the assessor in the Control Center, entering the skill catalog and reviewing skill monitoring, thresholds, dependencies, incidents, responsible parties, planned windows, and dialogs; search, filters, saved selections and export are mentioned. Lines 17–26 describe normal/abnormal judgment, disabling a skill via a switch, rationale, resident-facing text, concierge redirection, coordination, and reassessment after the skill team reports recovery. Lines 42–47 specify the same catalog-based use case and prerequisites. Lines 48–51 leave main/alternative scenarios as placeholders. Lines 53–58 explicitly leave incident-based recording and communication with the team open.

**Candidate routing:** skill catalog/monitoring, dialog investigation, operational skill-state controls; skills checking/review owner only to clarify boundaries. The document concerns operational health and temporary disablement, not evidence that the currently approved skill-check or publication-review process has these steps. “Асессор” is a source actor, not a current role assignment. Do not activate saved selections, export, concierge redirection, incident workflow or switches merely because this body mentions them.

**Unread / future needs:** saved attachment index is empty. No linked assessments, users or identities visited. Later work needs a business decision separating operational assessment from approved checking/review, completion of the placeholder flows, and resolution of the incident question. Any current scenario comparison must use separately authorized approved scenario sources; none was performed here.

### 243761671 — Аналитическая справка по существующей админке МПММ

**Saved revision:** r1; source v3, `2026-09-17T21:14:13.972+08:00`.

**Classification: mixed with bounded admin subset — historical MPMM inventory plus proposed ЦАМ integration.**

Evidence: `sources/wiki-243761671-readable/r1/content.txt:1–40` describes an existing MPMM admin and its claimed implemented/unimplemented modules, including sessions, administrators, roles, logs, security settings and unrelated mobile-product functions. Those are source assertions, not verified implementation. Lines 41–61 explicitly propose reuse for ЦАМ and changes to role cardinality, visibility and object permissions. Lines 64–71 connect session/authentication and current-user API to ЦАМ; line 71 names `GET /me`. Lines 80 and 93–95 place teams in `tsam-panel`, connected to authenticated users through API. Lines 106–115 discuss object history and place platform switches in the product panel. Lines 135–141 record unresolved business/architecture decisions. The readiness percentages at 124–134 are historical source estimates, not this assessment’s findings.

**Candidate routing:** session/current-user/permissions integration; teams; separately, object audit/history and platform-state scenario owners if later approved. The bounded relevance is reuse/integration and separation of product responsibilities, not wholesale import of administrator CRUD, security management, mobile-app features, or database/schema changes.

**Unread / future needs:** no indexed attachments. Referenced architecture/security documents and linked material were not opened. Later semantic work needs the approved integration contract and explicit business decisions on visibility, permission composition and owner boundaries. The source’s localStorage reuse, OIDC flow, role names and proposed permission names are historical claims/proposals only: they neither audit nor change current auth policy. No custom login/logout, new grants, permission map or role editor is authorized.

### 243765248 — Бизнес-анализ. МПММ

**Saved revision:** r1; source v8, `2026-09-25T16:20:43.504+08:00`.

**Classification: mixed with bounded admin subset — product/integration boundary evidence plus historical MPMM administration backlog.**

Evidence: `sources/wiki-243765248-readable/r1/content.txt:1–16` separates product functions from the certified MPMM admin while proposing session/security reuse. Lines 18–34 propose multiple roles, visibility and reference object lists; the role list is followed by the explicit need to fill the permission matrix with business. Lines 43–55 place integration, teams and product switches on distinct sides of the boundary. Lines 63–67 name skills, surfaces, teams, dialogs, monitoring, publication and platform state as product concerns. Lines 77–139 describe audit ingestion, permission/profile integration and current-user data. In particular, lines 123–124 state: “Frontend ЦАМ должен получать профиль текущего пользователя и его разрешения с областями видимости” for menus and visible sections. Lines 141–218 instead describe scope-list/card/edit/create and user-role administration UI; their presence in this MPMM analysis does not make them Control Center UI requirements.

**Candidate routing:** current-user/session/permissions UI visibility integration and confirmed-user display context; teams/product boundary owner. Backend integration/audit proposals remain backend-owner candidates, not frontend API implementation instructions. The historical roles, local user projection, object-list synchronization and scope editor are not imported into current auth or mock models.

**Unread / future needs:** seven indexed PNGs, IDs `245678564`, `245678561`, `245678560`, `245678554`, `245678553`, `245678547`, `245678536`, all uninspected. Linked issues were not expanded; issue labels and placeholder status text do not establish delivery or approval. Future work needs an approved current-user/permissions contract and explicit placement/approval of any proposed management UI. If images become necessary, request authorized textual requirements first; no image/prototype inspection was undertaken.

## Key evidence / architecture boundaries

These bodies establish relevance, not a migration plan. They describe a proposed split between MPMM identity/session/access administration and ЦАМ product work, with permissions/profile data informing product UI. They do not demonstrate current API or implementation behavior.

A specific semantic question remains for later authorized reconciliation: role-model lines 7–10 separate visibility from actions and reject explicit object-ID lists, whereas business-analysis lines 20–23 describe choosing concrete objects for visibility; analytical-reference lines 55–57 and 86–89 speak of role-level visibility and permission union. Record this as differing formulations, not a resolved contradiction or automatic supersession by version/date. None authorizes frontend enforcement or changes to backend authorization.

Current project guardrails remain unchanged: agreed session/refresh/current-user/permissions work and mock work retain their own approved sources; backend authorizes requests, permissions govern UI visibility. No new roles, permission maps, OIDC/logout flow, editor, auth model or mock principal is approved here. No current code/API/spec comparison was attempted.

## Start Here / later semantic work

For operational assessment, start with `sources/wiki-238324852-readable/r1/content.txt:17–26,53–58` to resolve the checking/review boundary and open incident question. For integration routing, start with `sources/wiki-243765248-readable/r1/content.txt:105–139`, especially 123–124. These are starting points for later approved reconciliation, not implementation instructions.

## Inspected/unread scope and residual risks

- Exactly four saved page text bodies, their metadata, and their saved attachment metadata inspected. Source and attachment indexes report HTTP 200; each index records `next: null`, with counts 1/0/0/7. These are local saved observations, not fresh HTTP results.
- Saved metadata attributes body-view roundtrip verification to the parent. Hashes and integrity claims were not recomputed or independently endorsed.
- No network, source execution, browser, linked-page/issue expansion, identity lookup, attachment bodies, prototypes, tests/build/E2E, application-code or current-spec inspection. Only this report was written.
- Residual risks: image-only detail remains unknown; historical proposals may differ from approved contracts; linked issue completion is unknown; operational assessment has unfinished flows. None prevents the bounded relevance classification, but all prevent treating it as scope approval or implementation verification.
- No whole-system audit, capability-by-capability reconciliation, task closure, or main-spec/archive changes.
