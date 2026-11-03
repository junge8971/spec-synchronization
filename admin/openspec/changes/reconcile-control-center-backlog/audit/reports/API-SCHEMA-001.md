# API-SCHEMA-001 — component schema comparison

## Result

Current snapshot independently contains **382 schemas**, historical raw and local aggregate **380 each**. Against either baseline: **3 added, 1 removed, 8 changed, 371 unchanged components**. Historical raw versus aggregate: **0 structural schema differences**. Exactly **12 operation IDs** are reachable from the affected schema set (5 domain, 4 skill, 3 surface operations). This is reference routing, not an operation-level comparison or runtime verification.

## Files Retrieved

All paths below are repository-relative. JSON pointers below disambiguate single-line snapshots.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/API-SCHEMA-001.md` (lines 1–8): scope and acceptance.
2. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/metadata.json` (lines 1–19): saved provenance and expected digest/counts.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1): current JSON, fully parsed.
4. `docs/api/contracts/openapi-2026-10-15.raw` (line 1): historical JSON, fully parsed.
5. `docs/api/contracts/openapi.json` (lines 1–22075): aggregate JSON, fully parsed.
6. `docs/api/contracts/README.md` (lines 1–33): historical digest and aggregate normalization context.

Initial metadata read incorrectly resolved `sources/` relative to the change root and returned ENOENT. Work stopped and supervisor was contacted. Supervisor explicitly clarified that these paths are relative to `audit/`, authorized continuation in this same run, and required recording the correction. No alternate input or fallback was used.

## Integrity evidence

| Input | Bytes | SHA-256 | Validation |
|---|---:|---|---|
| Current | 413007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | Matches saved metadata digest and byte count |
| Historical | 354412 | `2f3c48d3542e4486f7c1a501c4a1a4a0b813c662af26079a1e98c9f09d6ea26d` | Matches README digest |
| Aggregate | 642329 | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` | Computed fingerprint; no independent expected digest in supplied metadata/README |

Metadata records retrieval `2026-10-16T11:13:29.451Z`, source URL `https://nchat-a-tech.mos.ru/api/control/openapi.json`; no ETag/Last-Modified. These are saved provenance statements, not a new retrieval.

## Method

Three local `python3 - <<'PY'` inspection commands read inputs with `Path.read_bytes`, parsed with `json.loads`, computed SHA-256 with `hashlib`, compared `/components/schemas`, and traversed local JSON `$ref` graphs from every HTTP operation and path-level parameters. No files were written by those commands. All completed successfully. Digest equality assertions for current and historical passed.

Comparison sorts dictionary keys, ignores object ordering/whitespace, compares JSON number values (thus `1` equals `1.0`), preserves array ordering, and reports a changed array as one replacement containing complete before/after values. Added/removed objects are reported once at their root, including their full value. Missing is denoted **ABSENT**, not JSON null. Counts under this deterministic convention: **18 additions, 3 removals, 3 replacements = 24 pointer-level changes** against either baseline. These include whole-component additions/removal, not 24 changed components.

An initial diagnostic also compared Python numeric types; this is not the structural criterion. A subsequent recursive numeric-format inventory (including array contents) found **109 equivalent integer/float spellings across 38 components** between historical raw and aggregate. These serialization differences do not change JSON numbers or schema constraints and are excluded from structural counts. The complete value-level schema equality check between those two documents returned no differences.

## Complete structural delta

All before values apply to both historical and aggregate; all after values refer to current. Prefixes used only for readability:

- `S` = `/components/schemas`
- `K` = `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`

### Added components (3)

`/components/schemas/SkillCheckResponse`: ABSENT →
```json
{"properties":{"check_type":{"$ref":"#/components/schemas/SkillCheckType"},"status":{"$ref":"#/components/schemas/SkillCheckStatus"},"blocking":{"type":"boolean","title":"Blocking"},"message":{"anyOf":[{"type":"string"},{"type":"null"}],"title":"Message"},"checked_at":{"type":"string","format":"date-time","title":"Checked At"}},"type":"object","required":["check_type","status","blocking","message","checked_at"],"title":"SkillCheckResponse"}
```

`/components/schemas/SkillCheckStatus`: ABSENT →
```json
{"type":"string","enum":["passed","failed","warning","blocked"],"title":"SkillCheckStatus"}
```

`/components/schemas/SkillCheckType`: ABSENT →
```json
{"type":"string","enum":["anketa","phrases","exact_conflicts","semantic_conflicts","endpoint"],"title":"SkillCheckType","description":"Порядок объявления - порядок вывода проверок."}
```

### Removed component (1)

`/components/schemas/SkillZone`:
```json
{"type":"string","enum":["authenticated","anonymous"],"title":"SkillZone"}
```
→ ABSENT.

### Changed existing components (8)

Every changed pointer is listed; no other existing components change structurally.

| Exact pointer | Before | After |
|---|---|---|
| `/components/schemas/CreateDomainRequest/properties/zones/items/$ref` | `"#/components/schemas/SkillZone"` | ABSENT |
| `/components/schemas/CreateDomainRequest/properties/zones/items/type` | ABSENT | `"string"` |
| `/components/schemas/DomainResponse/properties/zones/items/$ref` | `"#/components/schemas/SkillZone"` | ABSENT |
| `/components/schemas/DomainResponse/properties/zones/items/type` | ABSENT | `"string"` |
| `/components/schemas/UpdateDomainRequest/properties/zones/anyOf` | `[{"items":{"$ref":"#/components/schemas/SkillZone"},"type":"array"},{"type":"null"}]` | `[{"items":{"type":"string"},"type":"array"},{"type":"null"}]` |
| `/components/schemas/SurfaceCardActionRequest/properties/value/minLength` | ABSENT | `1` |
| `/components/schemas/SurfaceCardActionType/enum` | `["message","skill"]` | `["message","skill","link"]` |
| `/components/schemas/SurfaceCardRequest/properties/subtitle/maxLength` | ABSENT | `200` |
| `/components/schemas/SurfaceCardRequest/properties/subtitle/minLength` | ABSENT | `1` |
| `/components/schemas/SurfaceCardRequest/properties/title/maxLength` | ABSENT | `100` |
| `/components/schemas/SurfaceCardRequest/properties/title/minLength` | ABSENT | `1` |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/cards/maxItems` | ABSENT | `4` |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/greeting/maxLength` | ABSENT | `500` |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/greeting/minLength` | ABSENT | `1` |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/greeting_fallback/maxLength` | ABSENT | `500` |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/suggestions/items/maxLength` | ABSENT | `100` |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/suggestions/items/minLength` | ABSENT | `1` |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/suggestions/maxItems` | ABSENT | `5` |
| `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/properties/checks` | ABSENT | `{"items":{"$ref":"#/components/schemas/SkillCheckResponse"},"type":"array","title":"Checks"}` |

Final replacement pointer: `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/required`.

Before:
```json
["id","code","service_id","name","types","display_version","purpose","expected_result","description","domain","team","contact","author_user_id","limitations","comments","related_materials","connection","intents","status","training","training_eta","autotest","autotest_note","version","created_at","updated_at"]
```
After:
```json
["id","code","service_id","name","types","display_version","purpose","expected_result","description","domain","team","contact","author_user_id","limitations","comments","related_materials","connection","intents","status","training","training_eta","autotest","autotest_note","version","created_at","updated_at","checks"]
```

## Reference routing to operations

Traversal follows `$ref` recursively, resolves RFC 6901 tokens, and uses a visited set per operation to terminate cycles. All refs encountered during this operation traversal resolved locally in each of the three documents. Operation reachability, not every alternative graph path, is the unit counted. Historical and aggregate yield identical affected operation sets and chains; current adds the three check schemas and removes SkillZone reachability. The union is the same 12 IDs in every snapshot.

### Operation inventory

Labels are local report shorthand, not API identifiers.

| Label | Method/path | Exact operationId |
|---|---|---|
| D1 | GET `/api/control/api/skills/v1/domains` | `get_domain_list_api_control_api_skills_v1_domains_get` |
| D2 | POST `/api/control/api/skills/v1/domains` | `create_domain_api_control_api_skills_v1_domains_post` |
| D3 | GET `/api/control/api/skills/v1/domains/{domain_id}` | `get_domain_detail_api_control_api_skills_v1_domains__domain_id__get` |
| D4 | PUT `/api/control/api/skills/v1/domains/{domain_id}` | `update_domain_api_control_api_skills_v1_domains__domain_id__put` |
| D5 | PATCH `/api/control/api/skills/v1/domains/{domain_id}` | `update_domain_api_control_api_skills_v1_domains__domain_id__patch` |
| K1 | GET `/api/control/api/skills/v1/skills/{skill_id}` | `get_skill_detail_api_control_api_skills_v1_skills__skill_id__get` |
| K2 | PUT `/api/control/api/skills/v1/skills/{skill_id}` | `update_skill_api_control_api_skills_v1_skills__skill_id__put` |
| K3 | PATCH `/api/control/api/skills/v1/skills/{skill_id}` | `update_skill_api_control_api_skills_v1_skills__skill_id__patch` |
| K4 | POST `/api/control/api/skills/v1/skills/{skill_id}/status` | `change_skill_status_api_control_api_skills_v1_skills__skill_id__status_post` |
| U1 | POST `/api/control/api/surfaces/v1/surfaces` | `create_surface_api_control_api_surfaces_v1_surfaces_post` |
| U2 | PUT `/api/control/api/surfaces/v1/surfaces/{surface_id}/configuration` | `update_surface_configuration_api_control_api_surfaces_v1_surfaces__surface_id__configuration_put` |
| U3 | GET `/api/control/api/surfaces/v1/surfaces/{surface_id}` | `get_surface_detail_api_control_api_surfaces_v1_surfaces__surface_id__get` |

### Complete affected-component mapping

| Component | Current operations | Historical/aggregate operations |
|---|---|---|
| CreateDomainRequest | D2 | D2 |
| DomainResponse | D1,D3,D4,D5 | D1,D3,D4,D5 |
| UpdateDomainRequest | D4,D5 | D4,D5 |
| SkillZone (removed) | none | D1,D2,D3,D4,D5 |
| tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse | K1,K2,K3,K4 | K1,K2,K3,K4 |
| SkillCheckResponse (added) | K1,K2,K3,K4 | none |
| SkillCheckStatus (added) | K1,K2,K3,K4 | none |
| SkillCheckType (added) | K1,K2,K3,K4 | none |
| UpdateSurfaceConfigurationRequest | U1,U2 | U1,U2 |
| SurfaceCardRequest | U1,U2 | U1,U2 |
| SurfaceCardActionRequest | U1,U2 | U1,U2 |
| SurfaceCardActionType | U1,U2,U3 | U1,U2,U3 |

### Exact ref-edge evidence

To reconstruct each operation-root JSON pointer: `/paths/` + method/path table's path with `/` escaped as `~1` + `/` + lowercase method + suffix below. `Q` denotes `/requestBody/content/application~1json/schema/$ref`; `R` denotes `/responses/200/content/application~1json/schema/$ref`. Targets named below are exactly `#/components/schemas/` plus that name. Component source pointers are explicit.

Operation roots (all three documents):

- D2 + Q → CreateDomainRequest.
- D1 + R → TsamResponseSchema_DomainListResponse_.
- D3,D4,D5 + R → TsamResponseSchema_DomainResponse_.
- D4,D5 + Q → UpdateDomainRequest.
- K1,K2,K3,K4 + R → TsamResponseSchema_SkillResponse_.
- U1 + Q → CreateSurfaceRequest.
- U2 + Q → UpdateSurfaceConfigurationRequest.
- U3 + R → TsamResponseSchema_SurfaceDetailResponse_.

Common component edges (all three):

| Ref source pointer | Target component |
|---|---|
| `/components/schemas/TsamResponseSchema_DomainListResponse_/properties/data/$ref` | DomainListResponse |
| `/components/schemas/DomainListResponse/properties/items/items/$ref` | DomainResponse |
| `/components/schemas/TsamResponseSchema_DomainResponse_/properties/data/$ref` | DomainResponse |
| `/components/schemas/TsamResponseSchema_SkillResponse_/properties/data/$ref` | tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse |
| `/components/schemas/CreateSurfaceRequest/properties/configuration/anyOf/0/$ref` | UpdateSurfaceConfigurationRequest |
| `/components/schemas/UpdateSurfaceConfigurationRequest/properties/cards/items/$ref` | SurfaceCardRequest |
| `/components/schemas/SurfaceCardRequest/properties/action/$ref` | SurfaceCardActionRequest |
| `/components/schemas/SurfaceCardActionRequest/properties/type/$ref` | SurfaceCardActionType |
| `/components/schemas/TsamResponseSchema_SurfaceDetailResponse_/properties/data/$ref` | SurfaceDetailResponse |
| `/components/schemas/SurfaceDetailResponse/properties/configuration/$ref` | SurfaceConfigurationResponse |
| `/components/schemas/SurfaceConfigurationResponse/properties/cards/items/$ref` | SurfaceCardResponse |
| `/components/schemas/SurfaceCardResponse/properties/action/$ref` | SurfaceCardActionResponse |
| `/components/schemas/SurfaceCardActionResponse/properties/type/$ref` | SurfaceCardActionType |

Current-only edges:

- `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/properties/checks/items/$ref` → SkillCheckResponse.
- `/components/schemas/SkillCheckResponse/properties/check_type/$ref` → SkillCheckType.
- `/components/schemas/SkillCheckResponse/properties/status/$ref` → SkillCheckStatus.

Historical/aggregate-only edges to SkillZone:

- `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2/schema/anyOf/0/$ref` (direct D1 parameter ref; handed off as routing evidence only).
- `/components/schemas/CreateDomainRequest/properties/zones/items/$ref`.
- `/components/schemas/DomainResponse/properties/zones/items/$ref`.
- `/components/schemas/UpdateDomainRequest/properties/zones/anyOf/0/items/$ref`.

This also captures the less obvious surface-detail response impact of the shared action enum, not just configuration request impacts.

## Architecture / Start Here

Start with current `/components/schemas` and the complete delta above. Domain DTO zone arrays cease referring to the removed enum. Skill detail response wrappers reach the qualified SkillResponse, whose newly required checks array reaches the three new schemas. Surface create optionally embeds UpdateSurfaceConfigurationRequest; its cards/action chain shares SurfaceCardActionType with the surface-detail response chain. No application source was inspected or changed; this report identifies contract routing only.

## Uncertainty and boundaries

- Published snapshots establish schema structure, not deployment status, runtime acceptance, UI coverage, business priority, or completion of any feature.
- No independent aggregate expected digest was supplied; its digest is a reproducibility fingerprint, not an authenticity attestation.
- Numeric spelling changes are deliberately excluded using JSON number equality; byte equality is not claimed.
- Reference mapping covers operations under `paths` and inherited parameters, following actual `$ref` edges. It is not a semantic compatibility proof or a full operation delta; another agent owns that comparison.
- No network, MCP, tests, generation, nested agents, source/spec edits, or product decisions occurred. Only the configured report artifact was written. Tests and generation were intentionally not run under task restrictions.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"382/380/380 independently counted; 3 additions, 1 removal, 8 changed components fully enumerated with 24 pointer-level deltas; 12 operation IDs traced; provenance hashes and uncertainty documented."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/API-SCHEMA-001.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"python3 inline SHA-256/schema comparison inspection","result":"passed","summary":"Current and historical digest assertions passed; all three JSON inputs parsed."},
    {"command":"python3 inline operation-to-schema reference traversal","result":"passed","summary":"12 impacted operation IDs in each document; encountered refs resolved locally."},
    {"command":"python3 inline line-count, structural-count and numeric-format inspection","result":"passed","summary":"18 additions, 3 removals, 3 replacements; baseline schema value equality; 109 numeric spelling differences across 38 components."},
    {"command":"tests / generation / network","result":"not-run","summary":"Explicitly prohibited by task."}
  ],
  "validationOutput": ["Current 382; historical 380; aggregate 380 schemas.","Historical-to-current and aggregate-to-current structural deltas identical."],
  "residualRisks": ["Aggregate digest lacks an independent expected value in supplied metadata.","Snapshot structure and reference reachability do not establish runtime behavior."],
  "diffSummary":"Only requested report artifact written; no project source/spec changes.",
  "reviewFindings": ["No unresolved input blocker after supervisor corrected the relative metadata path."],
  "manualNotes":"Initial ENOENT stopped work until explicit supervisor path correction. Read-only local analysis thereafter; no full operation comparison performed. No staging commands executed; repository staging state not inspected."
}
```
