# Code Context

## Disposition

**Evidence reconciliation only; retain all existing gates.** MOS-962 requires real stand synchronization and business-token reissue with confirmed old-token revocation. Published surface lifecycle status/time and module metadata are useful context, not those commands or proof of their completion. No implementation, activation, new plan or task closure is authorized by this report.

## Files Retrieved

Paths are repository-relative. `A` below means `openspec/changes/reconcile-control-center-backlog/audit`. Source content JSON is line 1; precise selectors/heading locators below disambiguate it.

1. `A/work-items/SCENARIO-MOS-962.md` (lines 1–9): bounded assignment.
2. `A/sources/jira-sandbox-details/r1/content.json` (line 1, **only `$.items[2]`**, verified key MOS-962) and corresponding `metadata.json`: primary issue.
3. `A/sources/api-live/r1/content.json` (line 1, selected paths/DTOs below) and `metadata.json`: saved publication evidence, not live execution.
4. `A/sources/wiki-241080062/r1/content.json`, `A/sources/wiki-245673187/r1/content.json`, `A/sources/wiki-241097511/r2/content.json`, `A/sources/wiki-241082009/r2/content.json` (each line 1, pertinent `$.bodyView` sections below) and each corresponding `metadata.json`: inert source passages and provenance.
5. `A/reports/REQ-MOS-1023.md` and `A/reviews/RECON-MOS-1023.md` (complete): prior extraction **with its corrective review**, not new requirements. `A/reports/LOCAL-001.md` (lines 65–120): bounded ownership routing only.
6. `openspec/changes/mos-1023-skill-environment-tokens/.openspec.yaml` (1–2), `proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-environment-tokens/spec.md` (1–47): complete existing token change.
7. `openspec/changes/archive/2026-10-02-mos-1019-skill-checks-training/`: complete `.openspec.yaml`, proposal, design, tasks and `specs/skill-checks-training/spec.md`; `openspec/specs/skill-checks-training/spec.md` (1–70): existing status-observation/readiness boundary, not rerun acceptance.
8. `openspec/specs/surface-lifecycle-publication/spec.md` (1–196): current surface MVP expressly excludes sandbox launch, including hidden launch.
9. Mandatory auth prerequisites, all read: `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md` (1–38), `design.md` (1–171), `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138).
10. Mandatory demo prerequisites, all read: `openspec/changes/archive/2026-10-09-add-local-session-demo/proposal.md` (1–28), `design.md` (1–70), `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123).

### Verified snapshot identities

Computed SHA-256 of each content file matches its metadata; Jira also matches the assignment digest. Version is snapshot metadata, not precedence or approval.

| Alias / source under `A/sources/` | Version / retrieval | SHA-256 |
|---|---|---|
| J `jira-sandbox-details/r1` | MOS-962 updated 2026-10-15T14:46:47.097+0800; retrieved 2026-10-16T13:18:06.195Z | `4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8` |
| API `api-live/r1` | info.version 0.1.0; retrieved 2026-10-16T11:13:29.451Z | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| W `wiki-241080062/r1` | v17, 2026-10-09T23:32:41.029+08:00 | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` |
| S `wiki-245673187/r1` | v18, 2026-10-09T23:34:11.543+08:00 | `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa` |
| C `wiki-241097511/r2` | v6, 2026-10-13T17:56:19.256+08:00; contract text v1.0 | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` |
| SC `wiki-241082009/r2` | v5, 2026-09-08T18:24:09.893+08:00; contract text v1.0 | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` |

J status is Backlog, saved comments total 0, attachments empty; custom fields/attachment bodies are not collected. API was captured from the documented A deployment, not evidence of T runtime equivalence. Wiki HTML was treated as inert text; links/embedded examples were never invoked. No actual credentials were inspected.

## Key Code / Evidence

### Stable candidate register

These are factual correction/no-op candidates for independent review, **not approved requirements additions**. J locators all mean `$.items[2].description`; W/S/C/SC mean `$.bodyView`, named heading and numbered requirement/table row.

| Candidate | Primary evidence | Disposition and exact existing owner/boundary |
|---|---|---|
| **SCENARIO-MOS-962-01 — sync command versus lifecycle send** | J: «реальную команду синхронизации с версией, временем и результатом» and missing «синхронизация стенда с продом, её прогресс». W `Песочница (ПЕС)` ПРТ-ПЕС-5 names sync; `K. Песочница` T-79 says the button updates stand skill composition/settings, with backend→verification-contour sync and FE button/toast. | Correct any blanket assertion that no sandbox-related API exists: a surface send operation does exist. Conversely do not relabel it stand sync. No bounded local product change establishes ownership of the complete sync protocol; preserve that ownership question rather than creating a parallel token/sandbox plan. |
| **SCENARIO-MOS-962-02 — truthful synchronization status** | J: «До подтверждения не показывать постоянное “Синхронизирован”». API `SurfaceStatusResponse` has only surface_id/status/updated_at. C `1.3 Модель навыка` / `Поля навыка`, `1.5 Подключение навыка`, and `2.9 Обработка конкурентных и повторных команд` distinguish object version and contract_version. | Safe factual boundary: lifecycle updated_at is not synchronization completion time; skill version/contract_version is not synchronized stand version. Required sync result/progress, version identity and authoritative confirmation are unspecified. Do not invent percentages, permanent success, polling, SSE, interval or invalidation rules. MOS-1019 status polling is not a reusable approved sync protocol. |
| **SCENARIO-MOS-962-03 — new token AND confirmed old revocation** | J: «новый токен и подтверждённый отзыв старого». W ПРТ-ПЕС-5; `Карточка навыка: подключение (ПОД)` ПОД-7; `G. Карточка навыка: подключение` T-52; `5.2. skill_tokens` describes issuance/revocation history. | **No-op on existing gate.** `mos-1023-skill-environment-tokens/tasks.md` 1.1 explicitly includes old-token revocation and unknown-outcome recovery; design Decisions and spec `Controlled disclosure and rotation` already require consequence confirmation, no optimistic success and no automatic repeat after lost response. Add only MOS-962 source traceability if approved later. A changed/new token does not prove old-token invalidation; neither a stored revoked_at model field nor admin refresh supplies the required business operation. |
| **SCENARIO-MOS-962-04 — shared metadata/security** | W `5.2. skill_tokens` usage includes verification-environment token; W ПРТ-ПЕС-5 requires sandbox reissue. J supplies no disclosure policy. | **No-op:** retain complete MOS-1023 metadata/disclosure/lifetime/scope/rotation gate, single shared entities/skill business model, skill-ID navigation, secret cleanup, no persistent cache/URL/log secrets, and current input/unknown-outcome safety. Its spec `Server token metadata` and `Secret-safe sandbox integration`, tasks 2.1–2.4 already cover these. RECON copy/environment/audit refinements remain recommendations, not adopted new requirements. Do not reopen answered storage/session boundaries. |
| **SCENARIO-MOS-962-05 — current disabled-state warning** | J: disabled modules **and skills** affect the test stand; UI must show current warning. W ПРТ-ПЕС-6 / K T-81 mention surface configuration and disabled modules; S `2.1. surface_skills` usage repeats that context. | Narrow correction: relevant disabled metadata is published, so “all warning data absent” is too broad. ModuleResponse.status and summary.disabled_modules/banner, SkillStatus.disabled and surface enabled_skills can supply context. They do not establish which disabled objects affect a selected stand or when changes propagate. Warning freshness/scope remains a backend/product question; do not add a polling protocol or assume global summary equals selected sandbox impact. Coordinate only context960 on identity/configuration; chat961 must not infer readiness from this warning. |
| **SCENARIO-MOS-962-06 — access decision** | J: «Согласовать доступ к этой операции по ролям». W ПРТ-ПЕС-6 says «Владелец поверхности» for configuration/warning. API surface-send operation explicitly names TSAM.Surface:send_to_sandbox. | Existing auth policy is **not reopened**. Archived auth spec `control-center-permissions`, `Exact permission matching` / `Explicit feature policy`: sandbox currently explicit `*` for UI until mapping agreed, role names grant nothing; backend authorizes requests. Surface-send permission is not a stand-sync/token-rotation grant. Ask owners for the missing operation mapping, not a new role engine or wildcard grant. Demo full does not implement absent APIs. |
| **SCENARIO-MOS-962-07 — readiness and approved scope** | W ПЕС-8 requires completed classifier additional training; ПЕС-9 requires isolated environment. S `Общие для всех вкладок`, row 9 explicitly asks whose configuration the send replaces. SC `2.6 Отправить конфигурацию в песочницу` publishes status/time, not execution readiness. | **No-op** on `openspec/specs/skill-checks-training/spec.md`, `Status observation does not establish readiness` and `surface-lifecycle-publication/spec.md`, `No sandbox workflow in MVP`. Neither status sandbox nor command HTTP success proves chat readiness, version readiness or successful checks. Preserve the existing surface MVP prohibition on sandbox launch and hidden launch; publication is not authorization to activate it. |

### Exact published contract pointers

All API pointers below start at `A/sources/api-live/r1/content.json` line 1:

- `$.paths['/api/control/api/surfaces/v1/surfaces/{surface_id}/sandbox'].post`: bodyless surface lifecycle send; description says transition to sandbox, returns new status/time, external-service error prevents status persistence. Its declared permission is `TSAM.Surface:send_to_sandbox`. The operation describes allowing any source status, including prod/archived; this is publication prose, not an instruction to override current UI approval.
- Response `responses['200'].content['application/json'].schema` → `#/components/schemas/TsamResponseSchema_SurfaceStatusResponse_` → `SurfaceStatusResponse`. Required business fields: `surface_id: uuid`, `status: SurfaceStatus`, `updated_at: date-time`. **No sync version, progress, job identifier, completion result or revocation receipt.** Generic envelope code/message does not establish these semantics.
- `$.components.schemas.SurfaceDetailResponse.properties`: configuration, enabled_skills, connection, status, updated_at are published context. `SurfaceSkillResponse` contains skill_id/parameters, not an effective disabled-impact/readiness verdict.
- `$.paths['/api/control/api/assistant-modules/v1/modules'].get` and `.../modules/summary.get` publish module metadata: `ModuleResponse` has status/version/updated_at/disable_impact_message; `ModuleStatus` is enabled/disabled; `ModuleSummaryResponse` contains banner and disabled_modules, whose items carry id/name. None is a sandbox synchronization receipt.
- Skill detail GET `/api/control/api/skills/v1/skills/{skill_id}` points to SkillResponse through its envelope; `SkillStatus` includes disabled and sandbox. `SkillListItemResponse` includes status/version/updated_at. `SkillConnectionSchema` contains endpoint/contract_version/auth_required/auth_type/parameters; `SkillAuthType` enum is transport_token. These are not issued sandbox-token metadata.
- Targeted path-name inspection found the surface send as the only sandbox/sync/token-named path. Schema-name and schema-text inspection found no sync/sandbox command schema or token lifecycle schema; token text in schemas is SkillAuthType.transport_token. No relevant saved operation/DTO supplies stand-sync progress or issue/reveal/revoke/rotate semantics. This is a bounded snapshot finding, not proof of backend nonexistence.

SC corroboration: heading `2.6 Отправить конфигурацию в песочницу` (HTML id `APIконтрактуправленияповерхностями-2.6Отправитьконфигурациювпесочницу`), subordinate `Успешный ответ` (`...-Успешныйответ.5`) returns surface_id/status/updated_at. SC `1.1 Статусы поверхности` defines sandbox as configuration sent. C `1.5 Подключение навыка` (`APIконтрактреестрадоменовикаталоганавыков-1.5Подключениенавыка`) calls contract_version the skill standard-contract version and auth_type the proposed transport_token; C `2.9` defines object optimistic locking, not sandbox synchronization. Wiki task T-52's suggested rotate route and T-81's sandbox-view route are design proposals, not saved API publication evidence.

## Architecture / Existing ownership

The existing MOS-1023 change owns common skill/environment business-token metadata and eventual gated secret operations used by connection and sandbox; no second token model is justified. MOS-1019's archived delivered scope is observation of skill status only and expressly does not establish sandbox availability. LOCAL-001 was used only to locate these owners, not to attest inventory completeness or implementation correctness.

Admin-session refresh belongs to approved MPMM technical session lifecycle, not sandbox token rotation. Auth/demo prerequisites separate UI permission presentation from backend authorization; mock principal/HTTP scenarios remain local and credential-free and cannot stand in for missing production APIs. No transport headers, revocation timing or role grants are synthesized here. The approved real-integration release gate remains open/unchanged.

For the bounded sibling dependency only: context960 owns selected context/configuration interpretation; chat961 owns chat/readiness behavior. They may reuse the facts that published metadata exists but sync completion/revocation/readiness semantics do not follow from it. No whole-sandbox audit or dependency completion claim is made.

## Genuine owner questions (not blockers to this report)

1. **Sync backend/product owner:** What entity identifies the stand and synchronized production revision; what command/read model confirms time, result and progress? How is an unknown outcome recovered and when does previously confirmed state cease to describe current inputs? No polling or retry design follows from a timestamp.
2. **Token backend/security owner, through existing MOS-1023 gate:** Is the MOS-962 sandbox token the same skill/environment verification token or a distinct stand-level credential? What server evidence confirms old-token revocation together with new issuance, including partial/lost response? Preserve already-agreed confirmation/disclosure/cleanup rules; do not assume immediate revocation or overlap.
3. **Context/configuration owner:** Which disabled module/skill records affect the selected stand, how fresh must the warning be, and whose configuration is replaced? S row 9 explicitly leaves the replacement scope open. Published global metadata alone does not answer this.
4. **Access/backend owner:** What approved granular UI permissions and server authorization apply to sync and token reissue? Role labels in Jira/wiki and surface-send permission do not answer that. Existing explicit-wildcard-only UI policy remains in force pending separate agreement; do not request wildcard to bypass the question.

No new delivery deferral is attributed to Jira: it states missing semantics. Retaining the implementation gate is the existing plan decision. No automatic Jira/wiki/API precedence is assigned. Comments/custom fields not present in these snapshots and actual runtime behavior remain unverified.

## Start Here

Open `openspec/changes/mos-1023-skill-environment-tokens/design.md` (11–17) and tasks (1–12), alongside J `items[2]`: the old-token confirmation/unknown-outcome requirement is already gated there. Independent review should attach the new source traceability and distinguish surface metadata from stand synchronization, not duplicate the token analysis or activate the surface sandbox command.

## Validation and residual risks

Read-only local JSON selection, inert HTML parsing, hash calculation and spec inspection were performed. The first discovery command looked for auth/demo at active paths and reported them absent; both were then found and fully read under their archive paths. Large output was read in continued chunks. No source/runtime/code audit, network, MCP, browser, tests, builds, credential extraction, embedded-command execution, index/staging verification or task/status edits occurred. Only this designated report was written. Source absence claims are snapshot-bounded; runtime availability and outstanding product/contract questions require separate owner evidence.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Verified assigned MOS-962 digest and six source snapshots; supplied seven stable correction/no-op candidates with exact source/contract/spec locators and preserved existing gates."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-962.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read-only Python JSON/hash and inert HTMLParser inspection","result":"passed","summary":"MOS-962 items[2] selected; six content digests matched metadata; pertinent publication and source passages inspected."},
    {"command":"Local file discovery and spec reads","result":"passed","summary":"Complete MOS-1023 and mandatory archived auth/demo prerequisites read; relevant readiness/MVP ownership inspected."},
    {"command":"Initial find of active auth/demo prerequisite directories","result":"failed","summary":"Directories were archived; corrected discovery and subsequent complete reads succeeded."},
    {"command":"Tests/build/browser/network","result":"not-run","summary":"Prohibited by bounded assignment."}
  ],
  "validationOutput": ["No synchronization/revocation protocol inferred from metadata, session refresh, status or changed token.","Report only; no activation, task closure or index attestation."],
  "residualRisks": ["Stand sync command/progress/result/version and unknown-outcome semantics remain unpublished in the inspected snapshot.","Token target identity, confirmed old revocation, warning impact/freshness and operation permission mapping require owner agreement under existing gates.","Saved publication is not runtime evidence; no automatic source precedence or backend absence conclusion."],
  "diffSummary": "Sole bound report created; no source/product/code/spec edits.",
  "reviewFindings": ["Retain MOS-1023 gates and current surface no-sandbox MVP; distinguish published lifecycle/module metadata from missing stand sync and token lifecycle semantics."],
  "manualNotes": "Fresh bounded primary-evidence/spec analysis only. Prior extraction reviewed together with RECON; recommendations not promoted to requirements. No actual tokens inspected or index state attested."
}
```
