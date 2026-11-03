# R-API-001 — independent review

## Verdict: REVISE semantic handoff; ACCEPT structural evidence

Both reports' central structural counts and schema routing are correct on independent recomputation. API-SCHEMA-001 is acceptable within its explicitly limited reference-routing scope. API-OPS-001 correctly labels description excerpts and does not call them cosmetic, but its generic statement about constraints/errors omits material lifecycle, concurrency, validation and persistence semantics. Before using the pair as the backlog/scenario handoff, incorporate the description findings below (or explicitly route this review alongside them). No product decision or backend availability conclusion follows.

# Code Context

## Files Retrieved

Repository-relative paths:
1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/R-API-001.md` (lines 1–8): review objective.
2. `openspec/changes/reconcile-control-center-backlog/audit/reports/API-OPS-001.md` (lines 1–134): reviewed assertions.
3. `openspec/changes/reconcile-control-center-backlog/audit/reports/API-SCHEMA-001.md` (lines 1–224): reviewed assertions and routing.
4. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/metadata.json` (lines 1–19): recorded provenance.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1, parsed in full): current source; all 18 new descriptions read in full.
6. `docs/api/contracts/openapi-2026-10-15.raw` (line 1, parsed in full): historical source.
7. `docs/api/contracts/openapi.json` (lines 1–22075, parsed in full): local aggregate.
8. `docs/api/contracts/README.md` (lines 1–35): historical counts/digest and intentional normalization, especially lines 3–10.

## Key Code / independently recomputed evidence

Two read-only Python inspections parsed all three documents, recursively compared dictionaries (arrays compared as values), enumerated the eight OpenAPI HTTP methods, hashed bytes and traversed local `$ref` recursively with cycle protection. RFC 6901 tokens were decoded during reference resolution. No author-produced delta was used as comparison input. The first command output exceeded the display cap; its saved output's beginning was subsequently read, recovering the counts, complete schema delta and initial descriptions. No evidence was left dependent on truncated output.

| Input | Bytes | SHA-256 | Paths / operations / unique IDs / schemas |
|---|---:|---|---|
| historical | 354412 | `2f3c48d3542e4486f7c1a501c4a1a4a0b813c662af26079a1e98c9f09d6ea26d` | 94 / 128 / 128 / 380 |
| aggregate | 642329 | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` | 94 / 128 / 128 / 380 |
| current | 413007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | 94 / 128 / 128 / 382 |

Current digest/bytes agree with metadata; historical digest agrees with README. Aggregate digest is only a fingerprint.

### Operation comparison — accepted

- Historical → current: zero added/removed operations, exactly 19 changed: 18 newly present descriptions (7 skills, 11 surfaces) and one parameter-array change. All operationIds and requestBody/response objects remain equal. Unchanged operations: 109.
- Historical → aggregate: exactly 128 security changes, no other operation differences. Aggregate → current: 128 changed operations, 147 changed operation fields, or 19 operations after removing security normalization.
- At `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2/schema/anyOf/0`, `{"$ref":"#/components/schemas/SkillZone"}` becomes `{"type":"string"}`. Parameter remains optional query `zone`, nullable; no enum remains at that branch.
- Each published operation's `/security` is `[{"AdminToken":[]},{"AccessToken":[]}]`; each aggregate operation's is `[{"AdminToken":[],"AccessToken":[]}]`. These encode OR and AND respectively. README explicitly documents intentional AND normalization. Security schemes and top-level metadata compare equal; path metadata outside operations also compares equal. This is not new upstream security drift or proof of deployed enforcement.

### Schema comparison — accepted

Independently found 3 additions (`SkillCheckResponse`, `SkillCheckStatus`, `SkillCheckType`), 1 removal (`SkillZone`), 8 changed and 371 unchanged components. Historical and aggregate schemas compare structurally equal, using JSON numeric value equality. The complete 24 pointer-level differences printed independently match API-SCHEMA-001's table: 18 additions, 3 removals, 3 replacements under its array-as-value convention.

Exact changed component roots under `/components/schemas/`:
- `CreateDomainRequest`, `DomainResponse`: `/properties/zones/items/$ref` removed and `/type` set to `string`.
- `UpdateDomainRequest`: `/properties/zones/anyOf/0/items` changes from SkillZone ref to inline string.
- `SurfaceCardActionRequest`: `/properties/value/minLength` added as 1.
- `SurfaceCardActionType`: `/enum` gains `link` after `message`, `skill`.
- `SurfaceCardRequest`: title min/max 1/100 and subtitle min/max 1/200 at `/properties/{title,subtitle}/{minLength,maxLength}`.
- `UpdateSurfaceConfigurationRequest`: cards maxItems 4; greeting min/maxLength 1/500; greeting_fallback maxLength 500; suggestions maxItems 5 and items min/maxLength 1/100.
- `tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`: adds `/properties/checks` array referencing SkillCheckResponse and appends `checks` to `/required`.

New checks schema requires check_type/status/blocking/message/checked_at; message nullable, timestamp date-time. CheckType enum is anketa/phrases/exact_conflicts/semantic_conflicts/endpoint; CheckStatus enum passed/failed/warning/blocked. Removed SkillZone enum was authenticated/anonymous. These values and all report delta pointers match source; no missing schema delta found.

### Reachability — accepted, not total semantic impact

Independent traversal resolved all encountered local refs in each document and found the same 12 affected operation roots:
- Domains: GET/POST `/api/control/api/skills/v1/domains`; GET/PUT/PATCH `/api/control/api/skills/v1/domains/{domain_id}`.
- Skills: GET/PUT/PATCH `/api/control/api/skills/v1/skills/{skill_id}`; POST its `/status`.
- Surfaces: POST `/api/control/api/surfaces/v1/surfaces`; PUT `/api/control/api/surfaces/v1/surfaces/{surface_id}/configuration`; GET `/api/control/api/surfaces/v1/surfaces/{surface_id}`.

Mapping agrees with every affected-component row in API-SCHEMA-001. In particular surface-detail response reaches the shared action enum via SurfaceDetailResponse → SurfaceConfigurationResponse → SurfaceCardResponse → SurfaceCardActionResponse → SurfaceCardActionType. CreateSurfaceRequest reaches UpdateSurfaceConfigurationRequest through `/properties/configuration/anyOf/0/$ref`. Skills detail/update/status reach the qualified SkillResponse via TsamResponseSchema_SkillResponse_; creation and intent updates do NOT reach checks schemas in their response contracts. Therefore 12 is a schema-reference count, not a bound on affected scenarios.

## Material description findings and required scenario follow-ups

All evidence below is in current `content.json` line 1. To make each citation exact without repeating long prefixes, define these JSON pointer prefixes:

- `K` = `/paths/~1api~1control~1api~1skills~1v1~1skills`
- `S` = `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces`

Append each listed suffix literally to obtain its RFC 6901 pointer. Every description was absent historically and in aggregate: this proves newly published documentation, not newly deployed behavior.

| Exact pointer(s) using prefixes above | Material semantics omitted from report excerpts; required scenario follow-up |
|---|---|
| K + `/post/description` | Creation persists five checks despite blocking results; initial phrases blocked, conflict checks passed, endpoint blocked until endpoint/contract_version populated. Request checks ignored; response only ID. Route creation → detail refresh and initial blocking states for review. |
| K + `~1{skill_id}/get/description` | Read does not calculate checks; order fixed, blocking true only for blocked, passed message null; legacy/uncomputed checks may be empty. Review empty/stale/check ordering presentation rather than assuming five populated results. |
| K + `~1{skill_id}/put/description` and `~1{skill_id}/patch/description` | Partial update; connection:null removes connection. Submitted fields recalculate dependent checks even unchanged; name/domain changes affect conflict partners. Data/checks transactional; other skills' version and updated_at do not change. Name/domain updates serialize with phrase changes with 10-second wait and PHRASE_REGISTRY_BUSY; VERSION_CONFLICT saves neither data nor checks. Review stale cross-skill displays, retry and optimistic concurrency flows. |
| K + `~1{skill_id}~1intents/put/description` | Whole-group replacement, omitted groups removed; no-op does not recalculate or increment version. Global active-group conflicts cross domain/team/status; exact blocks, semantic warns, threshold default 0.75. Both prior and new peers recalculated; last conflict removal unblocks both; concurrent identical phrases block both; 10-second queue limit. Response lacks checks. Review post-save card refresh and peer invalidation/concurrency scenarios. |
| K + `~1{skill_id}~1status/post/description` | Recomputes all five checks before forward promotion checking→training→autotest→sandbox→review→whitelist→prod. Draft→checking and specified backward transitions skip checks. Semantic warning does not block. On SKILL_CHECKS_BLOCKED, status/version/history unchanged BUT recalculated checks persist with new checked_at; errors use `/checks/{check_type}`, code BLOCKED, display order. Queue applies training onward, not draft/checking/disabled. Review rejected-transition refresh, structured errors and retries separately from success. |
| K + `~1{skill_id}~1phrase-conflicts~1check/post/description` | Read-only preflight does not persist readiness; excludes self, compares active groups of nondeleted skills globally, exposes other-team skill/domain names. Similarity returned in percent, exact first then semantic descending. Route cross-team visibility to approved permission/security scenario review, without inventing approval or changing auth policy. |
| S + `/post/description` | Create draft or review; default configuration and new widget token; channel from first domain label. Surface strings preserved while config trimmed. Skill-card references checked only as UUID on creation; existence/connection checked on first config save. Domain uniqueness case-insensitive; staged first-failure validation; duplicate enabled skill documented as 500. Review create-versus-edit asymmetry, duplicate handling, defaults and error routing; do not treat documented 500 as desired behavior. |
| S + `/get/description` | Stats null, dialogs sort only ID; search `%`/`_` act as wildcards; team-scoped results; offset beyond end empty; invalid query returns 400 INVALID_ARGUMENT. Review list/search/sort/empty-page expectations. |
| S + `~1{surface_id}/get/description` | Directory failure/missing user yields null full_name/email; embed code conditional on channel/token; stats null; updated_at unchanged by config or enabled-skill saves. Review nullable display and freshness indicators. |
| S + `~1{surface_id}~1configuration/put/description` | Whole replacement, trim strings, preserve widget token/embed code. Placeholder rules and conditional fallback requirement; unique suggestions; action message ≤500, skill connected/not deleted, link absolute HTTPS ≤2000 with no fragment/credentials. Body validation precedes lookup; all body errors returned with field pointers; save does not change updated_at. Route these description-only constraints alongside schema limits, including invalid body + missing resource and link safety scenarios. |
| S + `~1{surface_id}~1enabled-skills/put/description` | Whole replacement; empty clears all, status/updated_at unchanged. Skills validated before surface lookup; existing cards not revalidated after disconnect; duplicates documented as 500. Review stale card references and error precedence. |
| S + `~1{surface_id}~1sandbox/post/description` | Any source status, explicitly including prod/archived; creation field/domain validation. External service failure prevents status persistence. Review lifecycle assumptions; do not silently impose a stricter graph as a contract claim. |
| S + `~1{surface_id}~1publish/post/description` | Only draft forbidden; other statuses permitted, bypassing sandbox and including repeated prod. Requires greeting and ≥1 enabled skill; external service failure prevents persistence. Review publication prerequisites, repeated/bypass transitions and error distinctions (draft 400 FAILED versus prerequisite 422 FAILED). |
| S + `~1{surface_id}~1disable/post/description`, `~1{surface_id}~1enable/post/description`, `~1{surface_id}~1archive/post/description`, `~1{surface_id}~1restore/post/description` | Exact transitions prod→disabled, disabled→configured, disabled→archived, archived→configured; wrong source status 409 FAILED. Each delegates externally and does not save status on external error. Review these separately from permissive sandbox/publish. |

Descriptions also explicitly name per-operation permissions and authentication/error behavior; their publication neither approves a new permission model nor supplies observed response samples. Response maps remaining unchanged must not be summarized as unchanged business behavior.

## Architecture

Historical published snapshot → intentionally security-normalized aggregate is a separate comparison from historical → newer published snapshot. Schema `$ref` reachability routes structural DTO changes; operation descriptions independently expand behavioral evidence. Combining only the 12 schema-reachable operations would miss creation, phrase updates/preflight, surface listing and lifecycle semantics.

## Start Here

Open current `content.json` at K + `~1{skill_id}~1status/post/description` and S + `~1{surface_id}~1publish/post/description`: persisted checks after rejected promotion and permissive publication are high-impact omissions in excerpt-only routing. Then route the full table to the appropriate scenario audits. Required follow-up is evidence reconciliation, not automatic implementation or a product choice.

## Limits

No application source, split contracts, generated types, approved scenario specs or backend implementation was inspected. Therefore no claim of UI mismatch, missing implementation, approved lifecycle, runtime response fidelity or backend availability is made. The reports' numeric-format inventory (109 spellings across 38 components) was not separately recounted; structural equality was independently established. Saved provenance was checked locally, not re-observed over network. Tests, generation, network/MCP/browser and nested agents were not run, as prohibited. No infrastructure blocker or ambiguous path occurred. Only this bound artifact was written; staging state was not inspected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent comparison confirmed 19 operation deltas, 3 added/1 removed/8 changed schemas and 12 reachable operations; full descriptions reviewed with precise pointer-based follow-ups and limitations."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-API-001.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"python3 inline snapshot hash, structural delta and full-description inspection","result":"passed","summary":"Recomputed digests, operation/schema changes; recovered truncated output by selective read."},
    {"command":"python3 inline recursive reference routing and parameter inspection","result":"passed","summary":"12 impacted operations per document; all encountered refs resolved; schema counts and zone parameter confirmed."},
    {"command":"tests / generation / network","result":"not-run","summary":"Prohibited by work item."}
  ],
  "validationOutput": ["94 paths / 128 operations in all inputs; schemas 380/380/382.","19 upstream changed operations; aggregate-only security normalization on all 128.","Schema delta and affected-component mapping agree with author report."],
  "residualRisks": ["Descriptions are published claims, not runtime verification.","Scenario/spec/UI reconciliation remains required; aggregate fingerprint lacks independent authenticity baseline.","Numeric-format inventory not separately recounted; staging state not inspected."],
  "diffSummary":"Only requested independent review artifact written.",
  "reviewFindings": ["REVISE semantic handoff: material description-only behavior must accompany structural routing.","ACCEPT independently verified structural counts, pointers, schema routing and intentional security normalization."],
  "manualNotes":"No product decisions or backend availability claims. Both author reports were checked against actual parsed snapshots rather than endorsed from summaries. No source/spec edits or staging commands executed."
}
```
