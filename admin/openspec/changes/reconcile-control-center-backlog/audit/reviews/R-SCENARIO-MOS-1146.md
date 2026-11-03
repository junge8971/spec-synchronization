# R-SCENARIO-MOS-1146

**Verdict: ACCEPT WITH CORRECTIONS**

Designated artifact: `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-1146.md`. Returned for harness persistence; no direct writes.

## Mandatory correction

**R1146-01 — Low severity: locate percent annotations precisely.**

The report’s “Public incident read” section says the numeric alternative carries `ge`/`le`. They actually belong to the enclosing **number-or-patterned-string union**, not exclusively the number branch.

Primary evidence in `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`:

- `/components/schemas/SkillIncidentResponse/properties/affected_percent/anyOf/0`
- `/components/schemas/UpsertSkillIncidentRequest/properties/affected_percent/anyOf/0`

Both contain:
```json
{
  "anyOf": [
    {"type": "number"},
    {"type": "string", "pattern": "^(?!^[-+.]*$)[+-]?0*\\d*\\.?\\d*$"}
  ],
  "ge": 0,
  "le": 100
}
```

Replace the sentence with: **“The non-null number-or-patterned-string union carries nonstandard `ge: 0` and `le: 100`; these are not standard `minimum`/`maximum` constraints and do not establish generic JSON Schema range enforcement.”**

Preserve optionality, nullability and the report’s existing warning against claiming validator enforcement. No source/schema modification is requested.

## Independently verified findings

All thirteen candidate mappings remain usable with that correction.

- **MON1146-001/002:** MOS-1026 already owns read-only incidents. Its proposal’s blanket contract-absence wording is stale, but publication does not close its broader contract/integration gate. MOS-1025 expressly excludes incidents.
- **003–005:** Jira requests dictionary-backed lowercase strings, active-code validation during internal synchronization and preservation of used historical values. These are not permission to discard inactive historical incident rows. `SkillCatalogsResponse` names only `skill_types`, `training_states`, `autotest_states`. Managed-resource lookup permits section `skills` but returns an arbitrary map; incident lookup names and inactive inclusion are not established.
- **006:** Required/non-null, required/nullable and optional/nullable response fields are correctly distinguished. `affected_percent` alone is optional; false and zero must not become missing data.
- **007–010:** External identity is not an external URL. Jira explicitly requests status-group ordering and descending detection time, empty-list success, immutable upsert identity and backend validation/migration behavior. Requested acceptance and Ready-for-test/MR metadata do not prove delivery.
- **011:** Wiki §4.7/§7 genuinely differs: `skill_incident_*`, side `owner`, optional message, level `varchar(8)`, title `string(500)` and creation/update timestamps. Jira instead names `incident_*`, uses `team`, and requires message. No silent alias, imposed wiki cap or timestamp synthesis follows.
- **012:** МОН-13 explicitly requests a resolution deadline; the DTO supplies `postmortem_due_at`, not that deadline. `resolved_at` is an event timestamp, and `side` does not establish an assigned person. External links are also required by the existing MOS-1026 plan but absent from this DTO.
- **013:** Historical auth approval on **09.10.2026** remains recorded and closed in its original scope, not independently runtime-verified or extended to incident integration. Internal fake-incident synchronization is separate from frontend Express/demo fixtures.

### Exact contract boundaries

Verified public GET:
`/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1incidents/get`

Its 200 response references `TsamResponseSchema_list_SkillIncidentResponse__`: required `code`, `data`, `message`, with array-valued `data`. No pagination/query parameters are published.

Verified internal PUT:
`/paths/~1api~1control~1api~1internal~1incidents~1{external_id}/put`

It requires `UpsertSkillIncidentRequest` and returns `TsamResponseSchema_EntityCreatedResponse_`. It is not a frontend editor command.

Local request/response schema equality was independently checked. Saved operation security is OR; local internal and aggregate operation security is the approved AND pair. Schema equality therefore does not establish operation/security equality, deployment or working integration.

## Evidence inspected

Complete reads:

- `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1146.md` (1–198), both assigned monitoring work-items and `audit/decisions.md`.
- `openspec/changes/mos-1026-skill-operations-info/`: proposal (1–27), design (1–26), tasks (1–18), `specs/skill-operations-info/spec.md` (1–47).
- `openspec/changes/mos-1025-skill-monitoring/`: proposal (1–27), design (1–26), tasks (1–17), `specs/skill-monitoring/spec.md` (1–47).
- Main specs `skill-catalog-experience`, `control-center-api-integration`, `control-center-http`.
- Archived `2026-10-09-integrate-mpmm-auth-permissions` and `2026-10-09-add-local-session-demo`: proposals, designs, tasks and every delta specification; `docs/mpmm-auth-rollout.md` (1–58).
- `docs/api/contracts/skill-incidents-internal.openapi.json` (1–346).

Primary-source inspection:

- Jira `/items/0` and `/items/1` completely, including comment/status metadata.
- Published incident operations, DTOs, envelopes and relevant catalog lookup schemas; corresponding local aggregate fragments.
- Skills wiki `/bodyView`: МОН-13/14, ПРТ-МОН-6, §4.7, §7, T-35/T-59.
- Catalog wiki `/bodyView`: general information, skill catalog reference and version history.

All four source-content hashes were independently recomputed and matched metadata:

| Source | SHA-256 |
|---|---|
| Jira monitoring r1 | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` |
| API live r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| Skills wiki r1 | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` |
| Catalog wiki r2 | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` |

Capture timestamps match the report. API is OpenAPI 3.1.0/service 0.1.0; skills page is revision 17; catalog page is revision 6, distinct from body v1.0 and history v1.1 dated 14.09.2026. Both local contract hashes also match the report. None selects source precedence.

## Remaining limits and owner questions

Retain the report’s questions concerning incident lookup names/inactive labels, `owner` versus `team`, resolution deadline/person/URL sources, additional-status ordering, source-state errors and omitted upsert-field semantics.

No implementation, runtime, database, deployment or test coverage was inspected. No tests/builds, browser/network/MCP operations or endpoint execution occurred. Index state remains **uninspected/unverified**.

No monitoring-settings/refresh or responsible-assignment editor is activated: their explicit conditional write gates remain unchanged. Preserve originals; parent acceptance and any future documentation authorization remain separate.