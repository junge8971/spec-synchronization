# Code Context

## SCENARIO-MOS-1398 — responsible assignments

Designated artifact: `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1398.md`

Read-only evidence analysis; report returned for parent persistence. No direct writes, implementation inspection, network, browser, MCP, tests, builds, generation or Git operations. D-001–D-013 preserved. No product activation, editor approval, source precedence or completion inferred.

**Result:** MOS-1026 already owns the frontend read-only responsible/contact scenario. MOS-1398 supplies materially richer backend requirements, but the saved public OpenAPI does not publish its assignment operations or DTOs. Keep the existing API gate; propose bounded documentation enrichment, not a new duplicate plan or editor.

## Files Retrieved

Paths below are repository-relative. JSON pointers identify inspected source sections more precisely than physical lines.

### Primary evidence

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MONITORING-WAVE.md` — complete task.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` — complete routing inventory.
- `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` — complete D-001–D-013 dispositions.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-monitoring-details/r1/content.json` — `/items/0` and `/items/3`, including complete descriptions, status, updated timestamps, comments and attachments.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1) — all path keys; targeted skills/contact/catalog/lookup schemas and operation.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json` (line 1) — `/bodyView`, “Карточка навыка: мониторинг (МОН)”, §5.1 `skill_responsibles`, role dictionary rows and decomposition T-57.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r2/content.json` (lines 1–49; selected JSON fields) — `/version`, `/bodyView` contract-version label/history, §1.3 skill model, creation/update `contact_user_id` context.
- Corresponding four `metadata.json` files — complete.

### Complete relevant active plans

- `openspec/changes/mos-1026-skill-operations-info/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-operations-info/spec.md` (1–47).
- `openspec/changes/mos-1025-skill-monitoring/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–17), `specs/skill-monitoring/spec.md` (1–47).

### Main specifications

- `openspec/specs/skill-card-editing/spec.md` (1–49).
- `openspec/specs/skill-lifecycle/spec.md` (1–98).
- `openspec/specs/control-center-permissions/spec.md` (1–91).

### Mandatory auth/demo prerequisites, read completely

Under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`:

- `proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52).
- `specs/mpmm-session/spec.md` (1–138).
- `specs/control-center-permissions/spec.md` (1–89).
- `specs/control-center-http/spec.md` (1–71).
- `specs/control-center-shell/spec.md` (1–101).
- `specs/control-center-api-integration/spec.md` (1–64).
- `specs/control-center-mock-server/spec.md` (1–27).

Under `openspec/changes/archive/2026-10-09-add-local-session-demo/`:

- `proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26).
- `specs/local-session-demo/spec.md` (1–123).
- `specs/control-center-shell/spec.md` (1–55).
- `specs/control-center-mock-server/spec.md` (1–106).

Also `docs/mpmm-auth-rollout.md` (1–58), including historical approval.

## Integrity and version checks

SHA-256 recomputed from saved bytes; all four hashes and byte counts exactly match metadata.

| Source | SHA-256 | Bytes | Version/capture |
|---|---|---:|---|
| Jira monitoring r1 | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` | 44254 | Revision 1; `2026-10-16T13:48:06.559Z` |
| Public API r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | 413007 | OpenAPI `3.1.0`; service `/info/version` `0.1.0`; capture `2026-10-16T11:13:29.451Z` |
| Skills wiki r1 | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` | 481595 | Page 17; `2026-10-09T23:32:41.029+08:00`; capture `2026-10-16T11:48:21.710Z` |
| Catalog wiki r2 | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` | 73058 | Page 6; `2026-10-13T17:56:19.256+08:00`; capture `2026-10-16T12:37:03.295Z` |

Catalog page revision 6 is not its body contract version: body labels **v1.0**, while version history includes **v1.1, 14.09.2026**. No precedence selected.

Jira `/items/3/key` is exactly `MOS-1398`, status `Backlog`, updated `2026-10-16T19:24:17.680+0800`. `/items/0/key` is `MOS-775`, also `Backlog`. Both have zero captured/total comments and empty attachments. Custom fields were not collected. Parent context names monitoring, responsibles and planned windows; it does not establish delivery.

## Key Code / published contract

No application code inspected.

The saved API publishes:

- `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/get`.
- `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`: required `contact` referencing `SkillContactResponse`, not an operational-assignment collection.
- `/components/schemas/SkillContactResponse`: required string `id`, `name` reference, required string `email`. This is not MOS-1398’s nullable enrichment object.
- `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get`.
- `/components/schemas/CatalogLookupSectionName`: includes `skills`.
- `/components/schemas/TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___/properties/data`: arbitrary string keys mapped to arrays of `ManagedResourceCatalogItem`.
- `ManagedResourceCatalogItem` requires only `code` and `display_name`; the generic schema does not establish which dictionary keys are actually returned.
- `SkillCatalogsResponse` explicitly lists `skill_types`, `training_states`, `autotest_states`.

Exhaustive inspection of saved path keys and exact-literal scans of that parsed API found no `responsibles`, `responsible_roles`, `skill_responsible_roles` or `user_data_source`. Thus neither requested GET/PUT nor their DTOs are published in **this snapshot**. This does not prove backend nonexistence or that generic lookup cannot return the proposed key.

## Stable candidate mapping

All `J` locators below mean Jira packet `/items/3/description`, with the named heading. These are evidence candidates, not activated requirements.

| Candidate | Exact source locator and semantics | Existing coverage / bounded recommendation |
|---|---|---|
| **MOS-1398-C01** | J “Хранение”: UUID assignment/skill IDs; external nonblank string `user_id`; one assignment per `(skill_id, role)`; one user may hold multiple roles; UTC dates, no local user FK or stored contacts. | MOS-1026 covers responsible display generically, not identity/cardinality details. Record proposed DTO semantics; do not UUID-validate external user IDs or deduplicate assignments by user. |
| **MOS-1398-C02** | J “Хранение”, “Миграция и реализация”: hard-delete cascade; soft-deleted skill retains assignments but excludes public reads; no automatic assignments to existing skills; demo assignments are separate fixtures. | Backend storage/migration acceptance, not frontend implementation tasks or evidence of execution. |
| **MOS-1398-C03** | J “Справочник ролей”: seed `owner/tech/backup` with order `10/20/30`; active, nondefault, not deleted; default uniqueness/activity constraints; managed registry registration and `SKILLS.responsible_roles` mapping. | Existing generic lookup publication is infrastructure evidence only. Proposed registration specifies `public_api=false`, `cache_seconds=0`, `managed_catalog=true`; do not infer a separate public dictionary endpoint. |
| **MOS-1398-C04** | J “Справочник ролей”: lookup active/nondeleted values ordered by `sort_order`, then code; assignments using inactive/soft-deleted roles remain readable; FK protects used roles from physical deletion. | Add a read-preservation candidate to MOS-1026. Missing role in active lookup must not delete/hide its returned assignment. Historical label retrieval remains unspecified. |
| **MOS-1398-C05** | J “Сведения о пользователях”: enrich once per unique user per read; name plus nullable email/position/phone/messenger; absent user or unavailable service yields `user=null`, retaining assignment and `user_id`. | MOS-1026’s general partial-source handling is compatible but lacks this explicit case. An assigned-but-unresolved backup is not “Не назначен”. |
| **MOS-1398-C06** | Same heading: `user_data_source=external/mock/unavailable`; demo fake adapter uses reproducible profiles and `example.invalid`. | Preserve provenance independently of assignment existence. Requested backend fake adapter is not frontend session-demo selection or proof of implementation. |
| **MOS-1398-C07** | J “API чтения”: GET `/api/control/api/skills/v1/skills/{skill_id}/responsibles`; payload `items`; fields `id, role, user_id, created_at, user, user_data_source`; role order; empty `items=[]`; dictionary separate; reads create nothing and do not depend on monitoring settings. | Existing MOS-1026 owns read-only independently loaded blocks. Keep its API gate; add exact request/response traceability only through a later approved document change. |
| **MOS-1398-C08** | Same heading: `TSAM.Skill:view`, object/team access, existing missing/soft-deleted skill handling. | Compatible with existing skill UI policy and server-owned scope. Business role codes are not grants. No new auth model or role-based frontend request ACL. |
| **MOS-1398-C09** | J “Назначение после подтверждения сценария редактирования”: **conditional** PUT, full list of `(role,user_id)`, empty list removes all; duplicate roles rejected. | MOS-1026 explicitly excludes contact editors. Preserve confirmation gate; no editor, mutation wiring or automatic task activation authorized. |
| **MOS-1398-C10** | Same heading: new assignments require active/nondeleted roles; unchanged inactive/deleted-role pairs may persist; replacing their user prohibited. New/replaced users require service validation; unchanged users need no revalidation. | Conditional backend write semantics. Distinguish unchanged pair from merely unchanged role; do not impose stricter read filtering. |
| **MOS-1398-C11** | Same heading: atomic replacement under skill lock; unchanged pair retains `id/created_at`; replaced user gets new assignment identity/date; omitted role deleted; identical list preserves identities/dates. | Stable identity/idempotent effect is specified, not delivery or an approved transport-level Idempotency-Key/version protocol. Do not import questionnaire mutation protocol by analogy. |
| **MOS-1398-C12** | Same heading: conditional update permission/access; field/index `422 VALIDATION_ERROR`; user-service failure must not masquerade as missing user; existing `401/403/404`. Assignments change no grants, team, `contact_user_id`, status or prod transition checks. | Keep existing lifecycle/contact/auth boundaries. Exact unavailable-service write status/code still needs publication; no prod prerequisite introduced. |

## Actual discrepancies and remaining publication questions

1. **External user type disagreement.** Skills wiki `/bodyView` §5.1 and its prototype mapping describe `user_id` as UUID. MOS-1398 explicitly requests text matching existing string `UserId`; saved `SkillContactResponse.id` is string. Record the disagreement; do not select precedence from chronology.

2. **Mandatory backup / prod coupling disagreement.** Wiki МОН-17 requires a deputy; §5.1 says assignments are set when bringing a skill to prod and describes a mandatory-backup check. MOS-1398 expressly establishes no pre-prod role requirement and preserves existing prod checks. MOS-1026 spec lines 11–14 already supports genuinely unassigned backup. Do not add a lifecycle gate or silently erase the wiki requirement: product reconciliation remains necessary.

3. **Contact presentation is not fully contracted.** Wiki МОН-11 requests position, team and contacts; ПРТ-МОН-4/T-57 specify contact popover. MOS-1398 lists position/email/phone/messenger but no user-team field or exact name object shape. Existing MOS-1026 specifies contacts broadly. Do not synthesize team from the skill team or invent a user-card route.

4. **Inactive-role label resolution remains open.** Assignment response lists `role` but not its label; active-only lookup excludes some legitimately returned assignments. Preservation is explicit; a mechanism for obtaining historical labels is not. Truthful code/identity preservation can be planned without assuming expanded lookup permissions or APIs.

5. **Requested contract versus saved publication.** GET/PUT schemas, enrichment types, provenance, dictionary-key presence and precise errors remain absent from the inspected public snapshot. The generic lookup schema neither proves nor disproves deployment of `responsible_roles`.

6. **Backend schema alignment deserves owner confirmation.** Requested assignment `role` is `varchar(32)`, while dictionary `code` is `varchar(50)`. Seed codes fit both; acceptable future code lengths need alignment. Generic published catalog-item code permits up to 64 characters, but that is not proof this specific table accepts them.

## Architecture and ownership

- **MOS-1026** is the existing frontend owner: proposal lines 7–10, design lines 7–16, tasks 5–13, spec lines 7–14 and 35–47.
- **MOS-1025** explicitly excludes responsibles: proposal line 10. It supplies neighboring metric UI, not ownership of assignments.
- `skill-card-editing` owns questionnaire contact; `skill-lifecycle` owns existing transitions. Neither grants an operational-assignment editor.
- Future agreed data flow: skill ID → separate responsible read → assignment identities and nullable enrichment → read-only MOS-1026 block; independent role lookup supplies available labels/options. Monitoring settings must not gate this read.
- MOS-1398’s database, adapter, locking and migration requirements remain backend scope. No backend code audit occurred.

Owner discovery is bounded to the inspected inventory, matching plans and main specs; no universal missing-owner claim is made.

## Auth, mock and historical approval constraints

The archived auth task’s final paragraph (`tasks.md:52`) and `docs/mpmm-auth-rollout.md:5,24–33` record user approval on **09.10.2026**. That gate is historically closed by user confirmation, not agent runtime testing. Older demo planning language about an open gate does not reopen it. Approval is not extended to MOS-1398.

Configured mock/real mode is distinct from credential-destination validation: production and dev with mocks disabled use real integration regardless of hostname. Permissions govern UI; backend owns request authorization and object/team scope. Responsible role codes never confer permissions.

MOS-1398’s requested backend fake user provider is separate from frontend credential-free Express business mocks and fixed session-demo profiles. Neither proves the other exists or validates production authorization.

## Start Here

Open `openspec/changes/mos-1026-skill-operations-info/design.md:11–26`.

Recommended later, separately approved correction: enrich its existing blocked read-only scope with C01–C08 and C12’s preservation boundaries, then corresponding narrow spec/task acceptance cases. Keep C09–C11 explicitly conditional and outside the existing editor exclusion. Do not remove the API gate, create a duplicate owner, alter main specs, or close any feature task.

Future owner questions: reconcile UUID/string prose and mandatory-backup/prod requirements; publish exact enrichment/name/error schemas and historical-role labeling; decide whether an editor scenario is approved at all. These are ordinary publication/product findings, not missing-input blockers for this audit.