# Code Context

## Result and scope

MOS-960 has a primary requirement for a selected skill/surface sandbox context and a server test session bound to the tested version. The inspected publications provide reusable entity metadata, not that session contract. Surface `sandbox` is a status transition, not chat launch; skill readiness checks and integer `version` do not establish a tested snapshot. Preserve existing API/security gates and intentional MVP exclusions. This report does not activate functionality, choose source precedence, close tasks, or attest implementation.

Fresh local primary-evidence/spec analysis only. Jira content inspected semantically only at `/items/0` (MOS-960); sibling items were not analyzed. Hashing the containing file verifies bytes, not sibling requirements. HTML was parsed as inert text. No application source, network, MCP, browser, tests, builds, credential extraction or git operations. No access-policy or mock-design analysis: approved auth/demo prerequisites were located but not read or used to infer behavior; sandbox business-token references are not treated as application auth context.

## Files Retrieved

### Primary evidence and exact locators

All paths below are relative to the repository root. SHA-256 values were recomputed from saved `content.json` bytes and matched adjacent metadata. JSON pointers/section labels are used instead of misleading line citations for embedded HTML.

| ID | Exact file | SHA-256 | Inspected locators |
|---|---|---|---|
| J | `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-sandbox-details/r1/content.json` | `4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8` | `/items/0`: key, summary, description, status, updated, comments |
| C | `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r2/content.json` | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` | `/bodyView`, §§1.3–1.5 skill/connection model, §2.9 concurrent/repeated commands; bounded context/version discovery |
| S | `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241082009/r2/content.json` | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` | `/bodyView`, introduction, §§1.1–1.3, 2.4–2.7: context/configuration, sandbox and publication prerequisites |
| U | `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json` | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` | `/text`, “Песочница (ПЕС)” ПЕС-5/8/9, ПРТ-ПЕС-5/6; “Подключение” ПОД-8; tables 5.2 and 6.3; T-79 (dependency only) |
| V | `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-245673187/r1/content.json` | `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa` | `/text`, story “отправить конфигурацию в песочницу”, scenarios 1–2; process “3. Проверка в песочнице”; `surface_skills` usage; configuration/greeting portions |
| A | `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | `/paths` names for bounded discovery; five operations below and their full transitive schema references |

Read each corresponding `metadata.json`. J was retrieved 2026-10-16, issue updated 2026-10-15, status Backlog, zero collected comments; custom fields and attachment bodies were not collected. C is wiki version 6, S version 5, U version 17, V version 18. These are publication identities, not tested configuration versions or evidence of approval. A is a saved documentation capture, not a business-operation execution.

### Local requirements, fully read matching artifacts

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MOS-960.md` (lines 1–9): assignment boundary.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (lines 1–210): discovery routing only; not adopted as implementation evidence.
- `openspec/specs/skill-checks-training/spec.md` (lines 1–70): especially 63–70, status alone cannot establish readiness/current processed version or sandbox availability.
- `openspec/specs/skill-connection-settings/spec.md` (lines 1–58): connection metadata and optimistic-lock save, not a sandbox session.
- `openspec/specs/skill-catalog-experience/spec.md` (lines 1–112): especially 37–44, integer version/status display without unsupported readiness claims.
- `openspec/specs/surface-lifecycle-publication/spec.md` (lines 1–196): especially 37–68, 134–138, 179–196, explicit no sandbox workflow and no hidden calls.
- `openspec/specs/surface-overview-connection/spec.md` (lines 1–123): especially 80–94, saved greeting/scenario facts are not sandbox-check proof.
- `openspec/changes/mos-1023-skill-environment-tokens/proposal.md` (lines 1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-environment-tokens/spec.md` (1–47): whole active artifact set. Existing API/security gate, ID-only navigation, no invented token protocol, dialog implementation excluded.

Bounded local discovery of non-archive product change Markdown found sandbox/MOS-960 references only in that MOS-1023 artifact set. LOCAL-001 names no sandbox main capability; relevant main-spec matches above were read rather than inferred from names. This is not an exhaustive implementation or archival audit.

## Key Code / published contract

No application code was retrieved. Relevant saved OpenAPI operations (prefixes are literal):

1. `GET /api/control/api/skills/v1/skills/{skill_id}` → `TsamResponseSchema_SkillResponse_` → `tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`.
2. `POST /api/control/api/skills/v1/skills/{skill_id}/status` → `ChangeSkillStatusRequest`, same skill response.
3. `GET /api/control/api/surfaces/v1/surfaces/{surface_id}` → `TsamResponseSchema_SurfaceDetailResponse_` → `SurfaceDetailResponse`.
4. `POST /api/control/api/surfaces/v1/surfaces/{surface_id}/sandbox` → `TsamResponseSchema_SurfaceStatusResponse_` → `SurfaceStatusResponse` (no request body).
5. `PUT /api/control/api/surfaces/v1/surfaces/{surface_id}/configuration` → `UpdateSurfaceConfigurationRequest`, `TsamResponseSchema_UpdateSurfaceConfigurationResponse_` → `UpdateSurfaceConfigurationResponse`.

Exact schema locators are `/components/schemas/<name>`. All transitive DTOs of these operations were inspected, including `SkillConnectionSchema`, `SkillCheckResponse`, `SkillStatus`, `SurfaceConfigurationResponse`, `SurfaceSkillResponse`, `SurfaceConnectionResponse`, `SurfaceStatus`, their child models/enums, and common validation/error envelopes. No unrelated API operation was re-audited.

Critical shapes:

```text
Skill connection: endpoint?, contract_version?, auth_required, auth_type?, parameters?
Skill detail: id, version (integer), display_version (string), status,
              training, training_eta, autotest, autotest_note, checks, intents, connection
Skill check: check_type, status, blocking, message, checked_at
Change skill status: status, expected_version; optional reason; Idempotency-Key header
Surface detail: id, status, configuration, enabled_skills, connection, updated_at, ...
Surface configuration: greeting, greeting_fallback, suggestions, cards, appearance
Surface sandbox response: surface_id, status, updated_at
```

A publishes checks on detail and rechecks on skill lifecycle advancement; it does not publish a checked configuration revision or test-session identifier in these models. A explicitly describes surface sandbox as forwarding a transition to an external surfaces service, returning the new status/time; failure does not save status. This is published behavior, not observed runtime behavior. A says surface `updated_at` records creation/last status change and is unchanged by configuration/selected-skill saves: it cannot be promoted to tested-configuration version.

## Atomic candidates and coverage

Stable report-local IDs below are evidence candidates, not approved new requirements. J `/items/0/description` grounds C01–C09.

| Candidate | Requirement and supporting publication | Spec coverage / remaining boundary | Ownership and narrow question |
|---|---|---|---|
| MOS-960-C01 | Page for a **chosen skill**. C §1.3 and A skill detail identify the entity; U ПОД-8 describes entry from connection. | MOS-1023 delta lines 35–42 already requires skill-ID-only navigation after its gate. No inspected spec defines a server test context. | MOS-960 product/backend: confirm how chosen skill identifies the server context; do not duplicate the existing safe-navigation rule. |
| MOS-960-C02 | Page for a **chosen surface**. S §§1.2/2.4 and A surface detail provide identity/current saved configuration. U ПРТ-ПЕС-6 and V `surface_skills` usage add surface configuration/disabled-module warnings. | Surface overview covers saved entity data, not sandbox execution context. | MOS-960 + surface owner: distinguish current saved surface from configuration actually loaded on the stand; no inference from status. |
| MOS-960-C03 | Display **endpoint**. U ПЕС-5 and C §1.5/A `SkillConnectionSchema.endpoint` publish skill implementation address. | Existing connection-settings requirement covers this field; it does not identify the sandbox/chat endpoint, especially for a surface. | Backend/product: does MOS-960 mean service address, stand address, or both? No transport destination is invented. |
| MOS-960-C04 | Display **available environment/contour**. U ПЕС-9 requires an isolated test contour. | MOS-1023 metadata is conditional on an agreed API. Catalog working zones are not interchangeable with sandbox/prod environments. | Backend/security/product: identify authoritative available-contour metadata. Keep token gate unchanged; token presence is not readiness. |
| MOS-960-C05 | Display **scenario composition**. S §1.3 and A `SurfaceDetailResponse.enabled_skills`/`SurfaceSkillResponse` publish saved IDs/parameters. | Surface overview distinguishes persisted data from draft. Skill `intents` and surface enabled skills are not automatically the effective test-stand composition. | MOS-960 backend/product: clarify meaning in skill versus surface context and how effective composition is identified. |
| MOS-960-C06 | Display **greeting**. S §1.3 and A `SurfaceConfigurationResponse.greeting/greeting_fallback` supply surface content. | Saved greeting covered by overview; not proof that this content is loaded in a test session. No skill-specific greeting source found in inspected models. | Product/backend: define skill-only applicability and saved-versus-effective greeting. Preserve unknown/not-applicable distinction. |
| MOS-960-C07 | Display **synchronization state**. U ПРТ-ПЕС-5/T-79 mention synchronization action, not a state DTO. | No synchronization state in scoped context/status DTOs or matching main specs. | MOS-962 dependency owner supplies state semantics; MOS-960 displays it only after agreement. No sync implementation analyzed. |
| MOS-960-C08 | **Server test-session model**. J explicitly requires it; S §2.6/A surface sandbox returns status only. | No test-session schema/operation found in scoped publications; no inspected local capability covers it. | MOS-960 backend/product: obtain authoritative session identity/context/lifecycle contract. Do not reuse administrative session or invent endpoint/body. |
| MOS-960-C09 | **Binding to tested version**. J explicitly requires it. C §2.9 publishes integer object concurrency version; A also has business `display_version` and connection contract version. | None of these is a declared test-session binding. Skill checks have time but no tested revision; surface DTO has no configuration version. Main checks-training deliberately prohibits readiness inference. | MOS-960 backend/product: which immutable/reproducible revision is tested, what objects it covers, and how correspondence is confirmed after edits? No versioning mechanism prescribed. |

U ПЕС-8 (classifier retraining complete before testing) and ПЕС-9 (separate contour without user impact) remain explicit contextual requirements. Published skill `training`, status or checks alone are not proof that the current tested version has completed processing or that isolation works. These requirements need server-backed confirmation; this audit does not relax them.

## Contradictions, missing details and runtime unknowns

1. **Intentional product deferral, not missing implementation proof:** U/V describe sandbox entry; main surface lifecycle lines 39/65–68 explicitly exclude it. Do not turn the source story or newly seen endpoint into approval to remove that boundary. S §2.7's sandbox publication prerequisite also differs from the local MVP policy. Preserve policy and existing handling of `SANDBOX_CHECK_REQUIRED` pending an explicit owner decision.
2. **Published eligibility difference:** V sandbox-button scenario applies when surface is not Prod; its process lists configured/review/sandbox input states. A sandbox description says it accepts any original status, including prod/archived. These statements differ; no runtime request was made and neither is silently selected as precedence. No UI eligibility expansion follows.
3. **Metadata-shape difference relevant to context:** S nests enabled skills in configuration and its detail example under `data.surface`; A exposes `SurfaceDetailResponse` directly and `enabled_skills` alongside `configuration`. Do not construct a mixed DTO from the two publications. Scope does not authorize changing existing API types.
4. **Readiness publication gap has narrowed, session gap has not:** main checks-training says individual results are unavailable; A now publishes `checks` and advancement checks. Report that publication delta, not an absence of all checks. It still does not supply the MOS-960 session/tested-version binding. Broader checks reconciliation is outside this assignment.
5. **Absent in inspected scope:** server test-session identity/context contract, tested surface configuration revision, effective stand composition/greeting, and synchronization-state model were not found. Full relevant DTO traversal and bounded path/schema-name discovery support this limited statement. It does not prove absence from every backend/service, external document or future contract.
6. **Runtime unknown:** actual endpoint availability, readiness, isolation, correspondence to loaded configuration, synchronization success and behavior of the external service remain untested. Publication is not execution or approval evidence.

## Architecture and ownership

Saved entity read models can supply selected IDs and current metadata. They do not connect those values to a server test session or a tested snapshot. MOS-960 owns that context/binding question; MOS-961 chat depends on an agreed context but its transport/implementation was not analyzed; MOS-962 owns the separate synchronization-state dependency. MOS-1023 retains token API/security ownership and its conditional shared-model/ID-only navigation rules. Neither secret availability nor lifecycle status is substituted for chat readiness.

No code-change plan is proposed. Narrow correction candidates for owner review are: qualify any blanket “no API data” statement with the now-published metadata/checks; explicitly retain the session/version gap; preserve sandbox exclusion and token gates as a no-op unless separately approved. Do not alter task completion or source precedence based on this report.

## Start Here

Open `openspec/specs/skill-checks-training/spec.md:63–70` and `openspec/specs/surface-lifecycle-publication/spec.md:37–68` first: they prevent metadata publication from being mistaken for sandbox activation. Then use J `/items/0/description` and the nine candidates above to obtain the narrowly missing session/version decisions.

## Validation and residual risks

Saved primary hashes verified locally; semantic review completed for the scoped operations, transitive DTOs and listed full local artifacts. No blocking missing input prevented this bounded report. Independent review remains required. No test/build/browser or runtime validation was attempted, and no index/staging assertion is made. Only this report was intentionally written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Nine stable MOS-960 context/version candidates mapped to primary source hashes and exact JSON/section locators, scoped publication coverage, local gates, owner questions and runtime limitations."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-960.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find/grep and read-only Python JSON, inert HTML, SHA-256 and scoped DTO traversal","result":"passed","summary":"Verified six primary content digests; inspected only assigned Jira item and relevant saved contract/context operations and transitive schemas."},{"command":"Tests, build, browser, network and git operations","result":"not-run","summary":"Forbidden or outside bounded evidence/spec assignment."}],
  "validationOutput": ["Primary MOS-960 digest matches assignment and metadata.","Surface sandbox response contains surface_id/status/updated_at, not a test-session binding.","Existing no-activation and token API/security gates retained."],
  "residualRisks": ["No runtime or implementation validation; saved publication does not establish readiness or approval.","Session/version and effective stand-state gaps are limited to inspected sources, not all backend contracts.","Publication eligibility/shape differences and intentional local deferrals require owner review; no source precedence chosen."],
  "diffSummary": "Sole bounded report; no product, source, code, spec or task edits.",
  "reviewFindings": ["No audit-input blocker; retain backend/product session-version questions and independent review."],
  "manualNotes": "Fresh local evidence analysis. Auth/mock policy and sibling MOS-961/MOS-962 implementations excluded. No credentials extracted, embedded HTML executed, tasks closed or features activated. Git index not inspected or attested."
}
```
