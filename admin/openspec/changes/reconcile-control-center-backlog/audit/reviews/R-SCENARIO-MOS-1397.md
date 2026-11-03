# Code Context

## R-SCENARIO-MOS-1397

**Verdict: ACCEPT.** All fourteen candidate mappings are supported within the inspected evidence. **Mandatory corrections: none.** Acceptance concerns evidence reconciliation only—not implementation, publication authorization, monitoring activation or feature closure.

Returned for harness persistence to:
`/home/user/my/work/codesrc/projects/CAM/tsam-admin-front/openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-1397.md`

No direct writes performed.

## Files Retrieved

All paths are repository-relative. JSON sources are cited by exact pointers and body headings.

- `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1397.md` (1–205), complete.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/R-MONITORING-WAVE.md` (1–12) and `SCENARIO-MONITORING-WAVE.md` (1–14), complete.
- `openspec/changes/mos-1025-skill-monitoring/`: `proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–17), `specs/skill-monitoring/spec.md` (1–47), complete.
- `openspec/changes/mos-1026-skill-operations-info/`: `proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-operations-info/spec.md` (1–47), complete.
- `openspec/changes/mos-1030-skill-result-analytics/`: `proposal.md` (1–28), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-result-analytics/spec.md` (1–51), complete.
- `openspec/changes/reconcile-control-center-backlog/`: `proposal.md` (1–30), `design.md` (1–133), `tasks.md` (1–45), `specs/control-center-backlog-reconciliation/spec.md` (1–108); `audit/decisions.md` (D-001–D-013), complete.
- `openspec/specs/control-center-api-integration/spec.md` (73–110) and `openspec/specs/skill-catalog-experience/spec.md` (64–99).

Fully read historical prerequisites:

- `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: `proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52); `specs/mpmm-session/spec.md` (1–138), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-http/spec.md` (1–71), `specs/control-center-shell/spec.md` (1–101), `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-mock-server/spec.md` (1–27).
- `openspec/changes/archive/2026-10-09-add-local-session-demo/`: `proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26); `specs/local-session-demo/spec.md` (1–123), `specs/control-center-shell/spec.md` (1–55), `specs/control-center-mock-server/spec.md` (1–106).
- `docs/mpmm-auth-rollout.md` (1–58).

Truncated inspection output was read in continuation chunks.

### Primary-source integrity

Under `openspec/changes/reconcile-control-center-backlog/audit/sources/`, freshly computed content hashes match metadata:

| Source | SHA-256 | Verified dimensions |
|---|---|---|
| `jira-monitoring-details/r1/content.json` | `6dc8925cbbb1cfcd3a4179db720d38a72d9436926f7df3b73e612eb528c84c73` | 44,254 bytes; captured 2026-10-16T13:48:06.559Z; complete `/items/0` and `/items/2` read |
| `api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | 413,007 bytes; captured 2026-10-16T11:13:29.451Z; OpenAPI 3.1.0, API version 0.1.0; 94 paths, 382 schemas |
| `wiki-241080062/r1/content.json` | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` | 481,595 bytes; page 17, version time 2026-10-09T23:32:41.029+08:00; captured 2026-10-16T11:48:21.710Z |
| `wiki-241097511/r2/content.json` | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` | 73,058 bytes; saved status 200; page 6, version time 2026-10-13T17:56:19.256+08:00; captured 2026-10-16T12:37:03.295Z |

Catalog body label **v1.0** and history **v1.1 / 14.09.2026** are distinct from page revision 6. Successful r2 does not explain the recorded prior failure. The report’s four MOS-1025 planning hashes also independently match.

## Key Code / Contract Evidence

No application code was inspected.

### Preserved candidate findings

| Candidates | Independent verification |
|---|---|
| **C01–C03** | Jira `/items/2/description`, “Хранение” and “API чтения”, supports settings/dependency storage, normalization, uniqueness and read sorting. MOS-1025 owns metrics; MOS-1026 owns dependencies and maintenance. Their complete plans retain contract gates and independent failure handling. |
| **C04–C05** | Jira “Mock-провайдер и показатели” explicitly requests reproducible backend fixtures, `source="mock"` and fixture observation time. Availability/rating violations use **below**, response/data age use **above**; equality is not a violation. Difference units are percentage points, seconds and days respectively. This is requested backend evaluation, not a frontend calculator requirement. |
| **C06** | Jira evaluation order is absent settings → `not_configured`; active maintenance → `maintenance`; absent metrics → `no_data`; otherwise `evaluated`. Maintenance includes start and excludes end; other statuses have empty deviations. Wiki `/bodyView`, МОН-16, ПРТ-МОН-7 and T-60 instead require exclusion from metric calculation. The report correctly preserves the unresolved aggregate-window distinction. |
| **C07–C08** | Jira “API чтения” distinguishes null settings, null metrics and empty dependencies; GET creates nothing and does not synchronize dependencies. Conditional refresh uses one snapshot and aligns dependency `checked_at` with `observed_at`. Neither establishes the external-data update or last-invocation timestamps required by MOS-1025. |
| **C09** | Jira dictionary section explicitly requests `SKILLS` mapping `"dependency_statuses": "skill_dependency_statuses"`, active/undeleted sorted lookup, rejection of new invalid assignments and preservation of saved references. Lookup availability does not establish historical-label recovery. |
| **C10–C11** | The heading “Операции записи после подтверждения сценария подключения” explicitly conditions both PUT settings and POST refresh. Full replacement, stable identity, atomic full-snapshot synchronization, unchanged dates for identical snapshots, locking and rollback are requested semantics—not approved UI actions or implemented guarantees. |
| **C12** | Jira requests `TSAM.Skill:view`, object/team checks and existing skill modification rights for conditional writes. Approved auth specs distinguish UI permissions from backend authorization and prohibit inferred grants/request ACL. |
| **C13–C14** | Wiki `/bodyView`, T-58 specifies separate dependency GET; T-61 specifies PATCH thresholds and owner/product-team editing; T-62 specifies external deviation signalling. КАРН-17 says production-only visibility, while ПРТ-НАВ-4 includes disabled skills. These conflicts are accurately preserved without selecting precedence. |

### Published API boundary

Exact-string inspection of the complete saved API returns zero occurrences of `monitoring`, `threshold_availability`, `evaluation_status` and `dependency_statuses`. This supports the bounded publication gap, not backend nonexistence.

Verified operation pointer:

`/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get`

Verified schema pointers:

- `/components/schemas/CatalogLookupSectionName`: includes `skills`.
- `/components/schemas/TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___/properties/data`: arbitrary string-keyed arrays, not an explicitly published `dependency_statuses` member.
- `/components/schemas/ManagedResourceCatalogItem/required`: only `code`, `display_name`.
- `/components/schemas/ManagedResourceCatalogItem/properties/code`: length 1–64.
- Boolean `is_active` and `is_default` are optional, non-null and defaulted.

The operation publishes 200/422 and separate AdminToken/AccessToken security alternatives. This does not overturn the approved paired-header normalization or prove runtime enforcement.

The storage-width finding is valid: Jira dependency `status` is varchar(32), dictionary `code` varchar(50); wiki §§4.6/7.2 corroborate those widths, while generic published code permits 64.

### Precision retained for downstream use

These are clarifications, not mandatory report corrections:

- “Publish error responses” must not become “Jira specifies no errors”: its conditional-write section already names `422 VALIDATION_ERROR` and existing 401/403/404 responses. Exact monitoring schemas/envelopes remain unpublished.
- Catalog wiki `/bodyView`, “Общая информация”, describes HttpOnly-cookie authentication; §1.3 advertises `GET /api/control/api/skills/v1/catalogs`. Neither supplies monitoring DTOs, replaces the inspected generic lookup contract or overrides approved auth.
- Main-spec agreement establishes required behavior—not inspected implementation.

## Architecture

The report correctly preserves:

`requested backend monitoring → future agreed contract → MOS-1025 metrics + MOS-1026 operational blocks → skill-details composition`

A combined GET does not itself resolve partial failure or require duplicate queries. MOS-1030 remains separate 30-day analytics.

Historical auth approval remains **closed on 09.10.2026**, as recorded in archived auth `tasks.md:52` and `docs/mpmm-auth-rollout.md:5,24–33`. Earlier open-gate language in demo planning does not reopen that approval. It also does not authorize new monitoring integration or conditional writes.

Configured frontend real/mock mode, credential-destination validation and backend mock-provider provenance remain separate.

## Start Here

For any subsequently authorized planning refinement, open `openspec/changes/mos-1025-skill-monitoring/design.md:13–16` alongside MOS-1026’s complete design and Jira `/items/2/description`.

Remaining owner questions are correctly bounded: DTO/nullability/sample/period semantics, external freshness and last invocation, provider failure isolation, aggregate maintenance treatment, historical dictionary labels, refresh reassignment rules, visibility and explicit connection/write approval. They are not execution blockers or newly approved product deferrals.

No tests, builds, browser/network/MCP, endpoint execution, nested delegation, source/product edits or Git inspection occurred. Index state remains uninspected/unverified.