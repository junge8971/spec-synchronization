# Code Context

## SCENARIO-MOS-1397 — monitoring evidence reconciliation

Designated artifact: `/home/user/my/work/codesrc/projects/CAM/tsam-admin-front/openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1397.md`

Returned for parent persistence; no direct writes performed.

**Result:** Existing frontend owners are MOS-1025 for metrics and MOS-1026 for dependencies/maintenance. MOS-1397 supplies detailed **requested backend semantics**, but the inspected published OpenAPI contains no monitoring operation or DTO. Preserve both plans’ API gates and read-only scope. Conditional settings/refresh operations are neither approved frontend work nor evidence of implementation.

## Files Retrieved

Paths below are repository-relative. JSON evidence uses pointers/headings rather than artificial line-number citations.

### Planning and current requirements

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MONITORING-WAVE.md` (1–14).
- `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (1–194), routing only; its index attestation is not adopted.
- `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (1–109), D-001–D-013.
- `openspec/changes/reconcile-control-center-backlog/proposal.md` (1–30), `design.md` (1–133), `tasks.md` (1–45), and `specs/control-center-backlog-reconciliation/spec.md` (1–108), complete.
- `openspec/changes/mos-1025-skill-monitoring/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–17), `specs/skill-monitoring/spec.md` (1–47), complete.
- `openspec/changes/mos-1026-skill-operations-info/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-operations-info/spec.md` (1–47), complete.
- `openspec/changes/mos-1030-skill-result-analytics/proposal.md` (1–28), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-result-analytics/spec.md` (1–51), complete; preserves separate 30-day analytics ownership.
- `openspec/specs/control-center-api-integration/spec.md` (73–110): truthful fields, visible unavailable monitoring, no synthetic measurements.
- `openspec/specs/skill-catalog-experience/spec.md` (64–99): warnings remain source-dependent.

### Mandatory auth/demo prerequisites — completely read

Under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`:

- `proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52).
- `specs/control-center-api-integration/spec.md` (1–64).
- `specs/control-center-http/spec.md` (1–71).
- `specs/control-center-mock-server/spec.md` (1–27).
- `specs/control-center-permissions/spec.md` (1–89).
- `specs/control-center-shell/spec.md` (1–101).
- `specs/mpmm-session/spec.md` (1–138).

Under `openspec/changes/archive/2026-10-09-add-local-session-demo/`:

- `proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26).
- `specs/control-center-mock-server/spec.md` (1–106).
- `specs/control-center-shell/spec.md` (1–55).
- `specs/local-session-demo/spec.md` (1–123).

Also `docs/mpmm-auth-rollout.md` (1–58), including historical approval and its evidentiary limits. Truncated command output was subsequently read in continuation chunks.

## Evidence integrity and locators

Let `S = openspec/changes/reconcile-control-center-backlog/audit/sources/`.

All four content hashes were freshly recomputed and match their metadata.

| Source | SHA-256 | Version dimensions and inspected locators |
|---|---|---|
| `S/jira-monitoring-details/r1/content.json` | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` | 44,254 bytes; packet revision 1; captured `2026-10-16T13:48:06.559Z`. Complete `/items/2` MOS-1397 and `/items/0` MOS-775 context. |
| `S/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | 413,007 bytes; captured `2026-10-16T11:13:29.451Z`; OpenAPI `3.1.0`, `/info/version` `0.1.0`; 94 paths, 382 schemas. |
| `S/wiki-241080062/r1/content.json` | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` | 481,595 bytes; page version 17, version time `2026-10-09T23:32:41.029+08:00`; captured `2026-10-16T11:48:21.710Z`. `/bodyView`: monitoring requirements, КАРН-17, ПРТ-НАВ-4, model §§4.5–4.6, dictionary §§7.2–7.3, decomposition H/T-54–T-62. |
| `S/wiki-241097511/r2/content.json` | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` | 73,058 bytes; successful saved response 200; page revision 6, time `2026-10-13T17:56:19.256+08:00`; captured `2026-10-16T12:37:03.295Z`. `/bodyView` general information, scope, version history and open questions. Body label v1.0 differs from history’s v1.1 dated 14.09.2026. |

MOS-1397 `/updated` within `/items/2` is `2026-10-16T19:24:19.539+0800`; `/status/name` is `Development`. MOS-775 is `Backlog`. Neither establishes delivery. Both inspected items have zero comments with total zero and empty attachments. Custom fields were not collected. Other issue descriptions were not interpreted.

Catalog r2 metadata records earlier r1 failure; successful r2 does not explain it. Attachment bodies were not inspected. Wiki skills attachment enumeration is explicitly limited in metadata.

Fresh MOS-1025 planning hashes:

```text
proposal.md
1056c3c2d4d63e86828856b43113d8d121e42275c77ee2c6fbb10daf8de5ef37
design.md
705131c4ba33d553c2dbae6edb90afea8da28208bb50398a09e602175ce24c81
tasks.md
069e9a4f274aa0355b063502338bdf90a04e6d10639d012feaa97f2b4745c9c1
specs/skill-monitoring/spec.md
07d874d8fe439797c8a0b7d0efe6db455f970a73f4fd574929ba0426b631cdee
```

These are inspected-file identities, not a publication baseline acceptance or external freshness guarantee.

## Key Code / Contract Evidence

No application code was inspected.

### Published API

Exhaustive exact-string inspection of saved API JSON found zero occurrences of:

```text
monitoring
threshold_availability
evaluation_status
dependency_statuses
```

No monitoring-named schema or monitoring path exists in that snapshot. This establishes a **publication gap**, not backend nonexistence.

The published lookup operation is:

```text
GET /api/control/api/v1/managed-resources/catalogs/lookups/{section}
```

Exact JSON pointer:

```text
/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get
```

Its `section` references `/components/schemas/CatalogLookupSectionName`, whose enum includes `skills`. The response references:

```text
/components/schemas/TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___
```

`data` is a dictionary of arrays, not a schema declaring a `dependency_statuses` member. `/components/schemas/ManagedResourceCatalogItem` requires `code` and `display_name`; code is a string of length 1–64. Optional fields include nullable description/timestamps and non-null boolean `is_active`/`is_default` with defaults. This is not proof that the requested dictionary has been registered or returned.

The operation publishes 200 and 422 responses and separate security alternatives for AdminToken/AccessToken. Do not undo approved paired-header normalization or infer runtime enforcement from that metadata.

### Requested monitoring semantics

Source: Jira `/items/2/description`, headings “Mock-провайдер и показатели” and “API чтения”.

```text
priority:
  settings absent       -> not_configured
  active maintenance    -> maintenance
  metrics absent        -> no_data
  otherwise             -> evaluated

maintenance interval: [start, end)
non-evaluated states: deviations = []
threshold equality: no violation
```

This is backend-requested evaluation, **not authorization to implement a client status calculator**.

## Stable Candidate Mapping

IDs below are report-local stable candidates, pending independent review.

| ID | Primary evidence | Coverage, discrepancy and narrow recommendation |
|---|---|---|
| **MOS1397-C01** | Jira `/items/2/description`, “Описание”, “API чтения”; MOS-1025 proposal 7–10, 25–27; design 13–16 | Existing metrics owner found. Record the requested per-skill GET and semantics as new evidence under MOS-1025; retain task 1.1 and no synthetic data. No duplicate monitoring plan justified. |
| **MOS1397-C02** | Jira “Хранение”; wiki `/bodyView` §4.5 | One settings row per skill; availability/rating 0–100, response seconds >0, data age integer ≥0. Window requires both dates, nonempty reason and start < end; absent window means all three null. These are backend storage/validation obligations, not frontend editor approval. |
| **MOS1397-C03** | Jira “Хранение” dependency table; “API чтения”; wiki §4.6 | Dependency fields: id/name/owner/status/checked_at; trimmed nonempty name/owner; case-sensitive normalized name unique per skill; read sort name then ID. MOS-1026 already owns dependencies (proposal 3–8; spec 21–23). Add traceability there only after review; do not assign all operational UI to MOS-1025. |
| **MOS1397-C04** | Jira “Mock-провайдер и показатели”; wiki monitoring МОН-1 and model §4.5 | Requested backend provider produces reproducible `source="mock"`, fixed observed_at, metrics and full dependency snapshot. Normal/deviating/no-data fixtures and ok/degraded/down dependencies are requested. Wiki describes dialog-vitrine metrics/external monitoring: preserve this source difference. Backend fixture provenance is not frontend Express/demo and is not real telemetry. |
| **MOS1397-C05** | Jira deviation table; MOS-1025 design 15 and spec 7–19 | Availability/rating violate below threshold; difference threshold−actual in percentage points. Response/data-age violate above threshold; difference actual−threshold in seconds/days. Equality does not violate. Requested response includes metric code, actual, threshold, difference, unit. Record this specificity; existing “agree comparisons” gate is partly informed, not fully closed. Exact DTO field names for deviation members remain unpublished. |
| **MOS1397-C06** | Jira evaluation paragraph; wiki МОН-16, ПРТ-МОН-7, T-60 | Priority and `[start,end)` are explicit; deviations empty unless evaluated; expired dates retained. Wiki says maintenance is excluded from metric calculation, whereas Jira explicitly suppresses evaluation during an active window. These are not proven equivalent for an aggregate spanning maintenance. Obtain metric-provider/window semantics before claiming complete agreement. |
| **MOS1397-C07** | Jira “API чтения”; MOS-1025 spec 30–47 | `settings=null`, `metrics=null`, `dependencies=[]` have different meanings. GET creates no rows and does not synchronize dependencies. Preserve unavailable API, transport error, not configured and no data separately. Do not equate `not_configured` with every form of “not connected” or empty deviations with healthy service. Individual metric nullability and insufficient-sample representation remain unspecified here. |
| **MOS1397-C08** | Jira “API чтения”, provider/refresh paragraphs; MOS-1025 spec 21–28 and tasks 11 | Metrics observed_at and saved dependency checked_at are distinct. Request says refresh uses one snapshot and checked_at equals observed_at for its dependencies; ordinary GET does not refresh saved dependencies. Neither timestamp establishes external-data last update or last skill invocation, both required by the frontend plan. Do not substitute settings updated_at, observation time or current time. |
| **MOS1397-C09** | Jira “Справочник состояний зависимостей”; published lookup/schema pointers above | Requested `SKILLS` key `dependency_statuses` maps to `skill_dependency_statuses`; active undeleted values sorted sort_order/code; new unknown/inactive/deleted assignments rejected; saved references remain readable; FK prevents physical deletion in use. Preserve inactive returned codes even if absent from active lookup. Published generic lookup permits dictionary-shaped data but does not prove this key or historical-label resolution. No hard-coded closed enum or silent dropping. |
| **MOS1397-C10** | Jira “Операции записи после подтверждения сценария подключения”; MOS-1025 proposal 10, design 7–9 | PUT settings is explicitly conditional. Requested full replacement requires all four thresholds; omitted optional fields become null; first save creates, later saves retain id/created_at; decimals limited to two places and SQL range, timezone-bearing input, empty fallback→null, clearing window requires three nulls. Keep read-only frontend exclusion. No editor or write activation authorized. |
| **MOS1397-C11** | Same Jira conditional heading, POST refresh paragraphs | Requested bodyless refresh atomically replaces the full dependency set, retaining existing IDs; identical snapshot leaves dates unchanged; reject normalized duplicates/unknown statuses before writing; serialize on skill lock; rollback failures; successful empty snapshot clears. Same-snapshot metrics returned. This is semantic idempotence, not proof of implementation or an Idempotency-Key protocol. Preserved inactive references versus future refresh reassignment requires precise owner clarification. |
| **MOS1397-C12** | Jira read/write access paragraphs; archived auth permissions spec 21–36, 58–89 | Jira requests Skill:view, object/team checks and current skill modification right for conditional writes. Backend authorizes requests; UI permissions do not establish API availability. Do not invent monitoring grants, method/path ACL, role-based mock enforcement or translate wiki owner/product-role prose into grants. Future UI integration must use the agreed matrix or separately reconcile an uncovered action. |
| **MOS1397-C13** | Wiki monitoring МОН-3/15, T-58/T-61/T-62; Jira conditional writes and combined GET | Wiki includes editable thresholds, separate dependency GET, PATCH thresholds, external deviation notification; Jira requests combined read and conditional PUT/POST. Existing plans explicitly remain read-only. Preserve versioned differences; no hidden endpoint substitution, notification implementation or scope extension. |
| **MOS1397-C14** | Wiki КАРН-17 versus ПРТ-НАВ-4; MOS-1025 spec 9; main API integration spec 79–104 | Wiki itself differs on production-only versus production-or-disabled monitoring visibility. Main spec preserves a visible unavailable monitoring explanation. Retain current agreed unavailable behavior; future active visibility needs reconciliation rather than choosing wiki wording by recency. |

Additional backend-boundary precision: requested dependency status storage is varchar(32), dictionary code varchar(50), and published generic catalog code allows up to 64. Seed values fit all three; future longer codes require contract/storage clarification, not a frontend-invented restriction.

## Architecture and Remaining Questions

The evidence supports this ownership flow:

```text
MOS-1397 requested backend provider + persisted settings/dependencies
    -> future agreed per-skill contract
    -> MOS-1025 metrics/evaluation presentation
    -> MOS-1026 dependency/maintenance presentation
    -> skill-details widget composition
```

MOS-1030 remains independent 30-day result analytics. No inspected plan requires duplicating a query merely to preserve feature ownership; MOS-1397’s combined response needs a future composition decision that preserves partial failure and honest source states.

Future questions belong to the monitoring API/product and frontend-plan owners; accountable individuals were not established:

1. Publish agreed DTOs/envelope/error responses, metric nullability, period/timezone, sufficient-sample semantics and freshness/last-call fields.
2. Clarify how provider failure affects combined reads, and whether preserved settings/dependencies remain obtainable independently.
3. Reconcile maintenance evaluation suppression with exclusion from aggregate calculation, including the time basis for evaluation.
4. Define inactive-reference label recovery and exact unchanged-versus-new assignment behavior during conditional refresh.
5. Confirm or reject the connection/write scenario explicitly before assigning editor/refresh work.
6. Reconcile backend mock provenance with the frontend ban on presenting fixture metrics as real measurements.
7. Resolve visibility and endpoint differences without granting any source automatic precedence.

These are bounded publication/product questions, not missing-input blockers to this analysis.

### Auth and mock boundaries

Archived auth `tasks.md:52` and `docs/mpmm-auth-rollout.md:5,24–33` record user confirmation **09.10.2026**. That approval remains closed in its historical scope; it is neither fresh runtime verification nor approval of monitoring integration/writes.

Configured dev/build mode selects frontend real/mock operation. Credential destination validation is separate. Backend `source="mock"` does not switch frontend mode, bypass session bootstrap or justify shipping local demo fixtures in production. Local business mocks remain credential-free without role enforcement; fixed mock 403 is not evidence of backend authorization.

## Start Here

Open `openspec/changes/mos-1025-skill-monitoring/design.md:13–16`, alongside the MOS-1397 description and MOS-1026 design 13–21.

Recommended next action is **independent evidence review**, then—only with bounded publication authorization—a documentation-only refinement of existing plan traceability and remaining contract questions. No task checkbox, API gate, main spec, runtime behavior or product scope should change from this report alone.

## Limits

- No application/backend implementation, tests, deployment or runtime behavior inspected.
- No network, browser/MCP, endpoint execution, nested delegation, code/product writes, build or generation.
- No tests or validation suites run, as expressly excluded.
- No Git commands; HEAD, diff and index state remain uninspected/unverified.
- Source hashes verify saved bytes, not current external documents.
- Related-plan discovery is bounded; no universal absence of other owners is asserted.
- No direct report write; parent owns persistence and acceptance.