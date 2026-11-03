# Code Context

## R-SCENARIO-MOS-1398 — independent review

**Verdict: ACCEPT WITH CORRECTIONS.**

The twelve-candidate mapping is substantially supported. Accept it only with the precision corrections below. Preserve the original report; no product-plan changes, editor approval, source precedence, activation or task closure follow.

Designated output: `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-1398.md`. Returned for harness persistence; no direct writes performed.

## Mandatory corrections

### R1398-01 — Medium: qualify the backup/prod tension

**Report:** `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1398.md:113`.

Replace any reading of “mandatory backup / prod coupling disagreement” as an established contradictory transition rule with this narrower conclusion:

> Wiki requires a second contact and associates assignment with bringing a skill to prod. MOS-1398 does not establish role prerequisites in this task and explicitly leaves existing prod checks unchanged. This is a scope/requirements tension requiring reconciliation, not proof that MOS-1398 removes or prohibits every existing backup prerequisite.

**Primary evidence:**

- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json`, `/bodyView`, МОН-17: “Заместитель ответственного обязателен: навык не остаётся без второго контакта.”
- Same pointer, §5.1 `skill_responsibles`: “Задаются при выводе навыка на прод”; monitoring usage includes checking mandatory backup.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-monitoring-details/r1/content.json`, `/items/3/description`, “Описание”: “Обязательность ролей перед переходом в prod этой задачей не устанавливается.”
- Same pointer, conditional assignment section: “Действующие проверки перехода в prod не менять.”
- `openspec/changes/mos-1026-skill-operations-info/specs/skill-operations-info/spec.md:11–14` defines truthful display when backup is absent, not eligibility for prod.

**Preserve:** no newly invented lifecycle gate, no automatic precedence, no silent removal of wiki requirements.

### R1398-02 — Medium: revalidation exemption belongs to assignments, not user identity globally

**Report:** `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1398.md:105`, C10.

Replace “unchanged users need no revalidation” with:

> Unchanged assignments—unchanged `(role,user_id)` pairs—need no repeated user validation. Do not infer exemption merely because the same user ID appears elsewhere in the existing list.

**Primary evidence:** Jira `/items/3/description`, “Назначение после подтверждения сценария редактирования”: “Неизменившиеся назначения не требуют повторной проверки пользователя.” The same section distinguishes unchanged pairs from user replacement and retains identity/date only for unchanged pairs.

This preserves the report’s correct inactive-role distinction: an unchanged inactive/deleted-role assignment may survive; replacing its user is prohibited. All these PUT semantics remain conditional.

### R1398-03 — Low: preserve the request upper bound

**Report:** `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1398.md:100`, C05.

Change “enrich once per unique user per read” to:

> Perform **at most one user-service request** per unique user ID within a read.

**Primary evidence:** Jira `/items/3/description`, “Сведения о пользователях”: “не более одного запроса”.

Do not turn an upper bound into a mandatory external call count. Nullable enrichment, retained assignment identity and failure provenance remain supported.

## Independently verified findings

- **C01–C04:** external nonblank string user IDs, unique role per skill, multi-role users, storage/migration boundaries, exact role seeds, lookup registration and inactive-assignment preservation match Jira.
- **C05–C08:** unavailable/missing users retain the assignment with `user=null`; provenance values are `external/mock/unavailable`. Requested GET has `items`, separate role lookup, ordering and independence from monitoring settings. An unresolved assigned backup is not an unassigned backup.
- **C09–C12:** PUT is explicitly conditional on confirming an editing scenario. Full replacement, duplicate-role rejection, atomicity, stable unchanged identities, service-failure distinction and preservation of grants/contact/team/status are supported. No editor is authorized.
- **Ownership:** MOS-1026 already owns read-only operational contacts. MOS-1025 expressly excludes responsibles. Main-spec agreement establishes intended behavior, not implementation.
- **Published contract:** all 94 saved API path keys were inspected. Exact parsed-document scans found no `responsibles`, `responsible_roles`, `skill_responsible_roles` or `user_data_source`. This establishes bounded publication absence only.
- `SkillContactResponse` requires non-null string `id`, non-null `name` reference and non-null string `email`; it is not the requested nullable enrichment DTO.
- `ManagedResourceCatalogItem` requires only `code` and `display_name`. The lookup envelope’s arbitrary-key map neither proves nor disproves actual `responsible_roles` availability.
- Historical-role labels, exact enrichment/name/error schemas, user-team presentation and the `varchar(32)` assignment versus `varchar(50)` dictionary-code tension remain legitimate questions. Generic published code length 64 does not settle table acceptance.

Exact API locators under `sources/api-live/r1/content.json`:

- `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/get`
- `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`
- `/components/schemas/SkillContactResponse`
- `/components/schemas/SkillUserNameResponse`
- `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get`
- `/components/schemas/TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___/properties/data`
- `/components/schemas/ManagedResourceCatalogItem/required`
- `/components/schemas/SkillCatalogsResponse`

## Integrity and version verification

Recomputed saved-byte hashes and sizes match all four metadata files:

| Source | Bytes | SHA-256 |
|---|---:|---|
| Jira monitoring r1 | 44254 | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` |
| API r1 | 413007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| Skills wiki r1 | 481595 | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` |
| Catalog wiki r2 | 73058 | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` |

Capture timestamps respectively: `2026-10-16T13:48:06.559Z`, `2026-10-16T11:13:29.451Z`, `2026-10-16T11:48:21.710Z`, `2026-10-16T12:37:03.295Z`.

Skills page revision 17/date `2026-10-09T23:32:41.029+08:00` and catalog page revision 6/date `2026-10-13T17:56:19.256+08:00` match. Catalog `/bodyView` says contract v1.0 while history includes v1.1 dated 14.09.2026. API is OpenAPI 3.1.0/service 0.1.0. These dimensions do not establish precedence or deployment.

## Files Retrieved

Complete report and both monitoring work-items were read, plus `audit/reports/LOCAL-001.md` and `audit/decisions.md`. Primary JSON sections and complete metadata were independently inspected as identified above.

Complete relevant plans:

- `openspec/changes/mos-1026-skill-operations-info/`: `proposal.md:1–27`, `design.md:1–26`, `tasks.md:1–18`, `specs/skill-operations-info/spec.md:1–47`.
- `openspec/changes/mos-1025-skill-monitoring/`: `proposal.md:1–27`, `design.md:1–26`, `tasks.md:1–17`, `specs/skill-monitoring/spec.md:1–47`.
- `openspec/specs/skill-card-editing/spec.md:1–49`, `openspec/specs/skill-lifecycle/spec.md:1–98`, `openspec/specs/control-center-permissions/spec.md:1–91`.

Complete historical prerequisites:

- `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: proposal 1–38, design 1–171, tasks 1–52; all six specs: mpmm-session 1–138, permissions 1–89, HTTP 1–71, shell 1–101, API integration 1–64, mock server 1–27.
- `openspec/changes/archive/2026-10-09-add-local-session-demo/`: proposal 1–28, design 1–70, tasks 1–26; all three specs: local-session-demo 1–123, shell 1–55, mock server 1–106.
- `docs/mpmm-auth-rollout.md:1–58`.

## Architecture and preserved boundaries

Historical auth approval remains closed by user confirmation on **09.10.2026** (`auth tasks.md:52`; rollout document’s “Статус” and confirmation sections), not by agent runtime verification. It neither reopens through older demo prose nor extends to MOS-1398.

Configured real/mock mode remains separate from credential-destination validation. Business role codes confer no grants; permissions govern UI and backend owns authorization. Requested backend fake enrichment remains separate from frontend Express/session-demo fixtures.

## Start Here

Read the report with R1398-01–03 above, then `openspec/changes/mos-1026-skill-operations-info/design.md:11–26`. Any later enrichment requires separate approval and retains the existing API gate and editor exclusion.

Remaining owner questions are ordinary contract/product gaps, not execution blockers. No runtime, implementation, index state or feature completeness was verified.