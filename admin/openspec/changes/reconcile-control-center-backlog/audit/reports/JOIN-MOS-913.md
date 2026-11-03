# JOIN-MOS-913 — overview and connection evidence join

## Disposition

**Bounded static join completed; parent review and acceptance required.** Current implementation and inspected assertions substantially support server-owned connection data, unchanged embed-code copying, nullable metrics and preservation after read errors. One concrete discrepancy remains: embedding help opens a placeholder toast rather than the agreed documentation route.

No feature closure, population transition, publication or product-policy decision is made.

Paths below are repository-relative:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `W` = `app/widgets/surface-details/ui`
- `E` = `app/entities/surface`
- `O` = `openspec/changes/archive/2026-10-07-mos-913-surface-overview-connection`

## 1. Exact source and ownership

Primary source: `A/sources/jira-surface-details-d095/r1/content.json#/items/7`.

| Pointer | Evidence |
|---|---|
| `/key` | `MOS-913` |
| `/status` | `Ready for test`; not acceptance evidence |
| `/updated` | `2026-10-19T17:47:47.953+0800` |
| `/retrievedAt` | `2026-10-20T16:56:26.509Z` |
| `/description` | Overview/connection tabs; server embed_code, channel_id, domains and authorization; saved descriptive fields, responsible people, status/dates and metrics; no fabricated data-token; truthful checklist; read errors must not clear configuration |
| `/comments/items/1` | Comment `1124934`, updated `2026-10-06T15:57:49.248+0800`: older request for code generation, copying/modal and publication modal |
| `/comments/items/3` | Comment `1126400`, updated `2026-10-07T21:27:44.116+0800`: implementation claim and proposed checks for unchanged copy, documentation, null/zero and refresh recovery |
| `/comments/items/2` | MR reference only; linked MR not traversed |
| `/attachments` | Empty |
| `/comments/total` | Four; all four returned |

Packet metadata records collection cutoff `2026-10-20T16:56:26.589Z`, distinct from the item timestamp. It records parent verification against saved MOS-783 membership. This analyst did not independently re-audit the hierarchy.

**Conflict treatment:** comment `1124934` does not authorize client-side code generation. The exact issue description and current owning specification require the original server string. Publication-modal behavior belongs to lifecycle orchestration, not a new MOS-913 generator or independent publication policy.

**Distinct ownership preserved:**

- MOS-913: detail overview, connection text/copy/help, checklist truthfulness and detail-read preservation.
- MOS-910: registry metrics and list transport; its nullable `stats` object is not automatically a detail contract.
- MOS-911: skill selection and parameters; consulted here only at the saved-data/draft preservation boundary.
- MOS-914: commands, publication sequencing, archive/restore and success modal.
- MOS-958/709 and MOS-1164–1167: registration and existing presentation candidates; not reaccepted through this join.
- MOS-959/1237: configurator/validation; published configuration details do not activate the editor.

## 2. Prior evidence and controlling artifacts

Before implementation inspection, read:

- `A/decisions.md`, D-090–D-094.
- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md`.
- `A/reviews/R-SURFACE-CONFIG.md`.
- `A/publication/DRAFT-SURFACE-D091.md`.

These preserve the corrected configurator handoff, unpublished registration-only candidates, and sandbox/lifecycle boundaries. They are maps and acceptance history, not substitutes for current implementation evidence.

Controlling specification: `openspec/specs/surface-overview-connection/spec.md`, particularly:

- lines 9–45: server values and exact copy;
- lines 47–54: documentation navigation;
- lines 56–78: persisted overview and independent nullable metrics;
- lines 80–99: saved facts versus unconfirmed checks;
- lines 101–123: read recovery and cross-surface isolation.

Also inspected `O/proposal.md`, design and tasks, plus proposal/design/tasks of `archive/2026-10-12-mos-914-surface-lifecycle-mvp`. Historical checked tasks are not present execution proof. The later MVP removes the sandbox checklist item and permits controlled lifecycle actions while retaining read-only information fields.

## 3. Expected / observed / unknown

| Seam | Expected | Observed static evidence | Unknown / qualification |
|---|---|---|---|
| Detail source | Read saved detail by ID; do not synthesize connection fields | `E/api/surface-registry-client.ts:55–90,151–161`: required detail fields, nullable connection values, ID-match refinement; `W/surface-details.tsx` owns the query and keyed editor snapshot | No live response or deployment checked |
| Connection display | Server embed code as text, all domains, channel and authorization; null is absence of information | `W/surface-details/surface-details-connection.tsx`: React `pre/code` text, server props, null labels; no HTML execution or generation | Does not establish production token issuance or authorization behavior |
| Exact copying | Copy original string, including whitespace and genuine server attributes; truthful success/failure | Same component uses trim only to determine availability; `handlers/surface-details.handlers.ts:13–19` forwards the original string to `navigator.clipboard.writeText`; success follows resolution, failure keeps manual copy available | Actual browser clipboard permissions not exercised |
| Overview | Saved configuration name, purpose/context, owner, responsible people, status/dates and metrics | `surface-details-overview.tsx`: fields read from `surface`, localized dates/numbers, React text; responsible formatting through entity public API | Not proof of historical screenshot parity or backend normalization |
| Null versus zero | Each metric independently distinguishes null from 0 | `formatMetric`: `value === null ? 'Нет данных' : ...`; zero retained, including `0%` | Inspected component regression explicitly covers dialogs=null/share=0, not the reverse combination |
| Checklist | Facts from saved fields, no permanent green validation | `surface-details-publication-checklist.tsx`: saved domains/skills and trimmed greeting; mandatory parameters and uniqueness remain unconfirmed; no sandbox item | No server readiness results inferred; lifecycle policy remains MOS-914 |
| Read failure | Preserve last successful information/configuration and draft; separate successful write from failed read | `E/model/use-update-surface-enabled-skills-mutation.ts`: spread merge updates only enabled_skills/status/updated_at and tracks refresh error separately. `W/surface-details.tsx` keys state by surface ID | Static assertions, not an executed outage experiment |
| Embedding help | Open `/docs`, respecting basename, even with no code | **Mismatch:** `surface-details-connection/instruction-toast.tsx` opens a five-second placeholder toast; no navigation. Existing test explicitly requires unchanged route | Parent must determine whether an uninspected later approval exists before corrective publication |

### Detail statistics boundary

`docs/api/contracts/surfaces.openapi.json`:

- `/components/schemas/SurfaceDetailResponse/properties/stats` directly references `SurfaceStatsResponse`.
- `/components/schemas/SurfaceStatsResponse/properties/{dialogs_30d,share_percent}` permit integer or null.
- Detail `stats` itself is required and is not nullable.
- `E/api/surface-registry-client.ts` correctly distinguishes this required detail object from the registry’s nullable object.

Do not import MOS-910’s `stats=null` handling into MOS-913 automatically. Detail schema uses `z.number().nullable()` for each metric, which is broader than the local integer schema; no fractional response was observed. This is a bounded validation-strengthening question, not evidence of deployed failure.

### Checklist limitation

The explanatory sentence about saving current selections is conditioned on a difference in **counts**:

```text
selectedSkillCount !== surface.enabled_skills.length
```

This does not detect equal-count replacement of one skill with another. Main spec requires an explanation when draft and saved composition differ. This is a narrow static limitation at the MOS-913 checklist boundary, not permission to alter MOS-911 selection policy or MOS-914 sequencing. No runtime reproduction was performed.

## 4. API locators and limits

Local contract: `docs/api/contracts/surfaces.openapi.json`.

Exact operation pointer:

`/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}/get`

Relevant schemas:

- `/components/schemas/SurfaceDetailResponse`
- `/components/schemas/SurfaceConnectionResponse`
- `/components/schemas/SurfaceStatsResponse`

Saved API publication: `A/sources/api-live/r1/content.json`, same operation pointer plus `/description`.

That saved description says configuration is returned as saved, server embed text contains channel/token attributes when available, metrics are not calculated, and `updated_at` reflects creation/latest status change rather than every configuration/skill save. These statements support treating code and timestamps as server-owned; they do not prove backend execution.

The description’s phrase about null statistics does not override the structurally nonnullable detail object. Its responsible-user wording is also not grounds to reinterpret the top-level connection object. No auth/security model is selected here.

The issue links wiki page `241082009`; this report does not claim a complete wiki-contract reconciliation. That all-obligation comparison belongs to API-MOS-712.

## 5. Inspected tests — not executed

`W/surface-details.test.tsx`:

- `233–274`: persisted overview, neutral checks and nullable responsible details.
- `276–287`: independent dialogs=null/share=0 rendering.
- `289–310`: saved checklist facts versus unsaved selection; prod does not imply passed checks.
- `312–342`: server connection text, no executed script, nullable fields without inferred authorization state.
- `344–374`: exact multiline string and delayed copy success.
- `376–393`: rejected/unavailable Clipboard API, code retained.
- `720–740`: **asserts placeholder toast and unchanged route**, contradicting documentation-navigation requirement.
- `1085–1111`: route-ID reinitialization and no previous-surface display after next-surface failure.
- `1113–1141`: unsaved parameter preservation across refetch and rejected update.
- `1143–1230`: successful PUT followed by failed GET; retained configuration/connection/overview cache, retry, fresh readback and keyboard tab activation.

`E/api/surface-registry-client.test.ts:291–387`:

- UUID endpoint/cancellation.
- Nullable responsible details with retained IDs.
- Rejection of invalid used fields, legacy responsible strings, missing stats and string metrics.
- Distinct forbidden/not-found/network failures.

These are assertion locators, not claims that tests currently pass. The inspected set does not establish every edge in the main specification, including reverse metric null/zero, equal-count checklist divergence or current empty/whitespace copy-button coverage.

## 6. Bounded publication candidates — queue only

1. **KEEP — MOS-913 server-data guarantees.** Retain exact server-code copying, null/zero distinction, saved checklist facts, read-only information and read-error preservation. No broad replacement feature is justified.

2. **UPDATE candidate — embedding help.** Parent may queue a narrow reconciliation of `Embedding help opens documentation` against the placeholder toast and contrary test. Expected destination is already agreed `/docs` with basename; no new article, endpoint or generation policy. Before implementation/publication, confirm no later explicit approval superseded that agreement.

3. **UPDATE candidate — checklist explanation.** Parent may queue a narrowly scoped comparison of actual saved/draft skill membership instead of count-only divergence, preserving server facts and existing publish policy. Keep MOS-913 explanation ownership distinct from MOS-911 selection and MOS-914 command ownership.

4. **QUESTION / optional regression strengthening.** Reverse null/zero metrics, integer validation, empty/whitespace copy code and equal-count checklist divergence can be evaluated under this existing owner. No separate speculative feature or automatic defect closure.

5. **NO new generator or sandbox work.** Older generation/modal prose must not activate client-generated credentials, sandbox checks or configurator development.

## 7. Input SHA-256 fingerprints

Computed from complete local bytes during this inspection.

| Input | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| Same directory `metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `A/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `openspec/specs/surface-overview-connection/spec.md` | `51f9dc1a1d7b92ccdb059b7fda0117bf6c898378fa9a9fe185c7e2045044d193` |
| `docs/api/contracts/surfaces.openapi.json` | `9d8ef7ff68e187cebb051e6ee85a9ad333f0af903537a5e181425694c48d9758` |
| `E/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `E/api/surface-registry-client.test.ts` | `4d5f93269521aedb76ce4dd722390c92dfa06e86b63af622f952146ef105c886` |
| `W/surface-details.test.tsx` | `5ff98d3c6e74786075c2060fb207171f56be28a70a9802e13d0fb6e50b9def3c` |
| `W/surface-details/surface-details-connection.tsx` | `142a62351c26c9b17be609ecef9db5024a7a0b245c8af04530728ce7a820e85c` |
| `W/surface-details/surface-details-overview.tsx` | `b99e696ca0ef79d943bd719ac9b402d784a547be2c4ee3d2a1901d2a05e55f56` |
| `W/surface-details/surface-details-publication-checklist.tsx` | `b816776a78093e295b1282653ab63b91bd1d6d8d0c33c7ac623893cf10fe48e6` |
| `W/surface-details/surface-details-connection/instruction-toast.tsx` | `23304d552033c8442773ef94104ef484ab54a2afc30c70dbe4f3e80ff884991a` |
| `E/model/use-update-surface-enabled-skills-mutation.ts` | `3ea725ae29d746a428e5dcc816ed8a08a846b27c77bcfa62be34ed2762812b9c` |

## 8. Historical and deployment limitations

No mandatory-input or infrastructure blocker occurred. No network, browser, business API, tests, builds, configuration changes, git mutations or nested agents were performed. No repository/report files were written by the analyst.

The exact packet restores evidence for this member; it does not clear other publication freshness gates. Historical statuses, implementation comments, MR references and archived checked tasks do not establish delivery. Backend persistence, actual metrics, authorization behavior, real clipboard operation and deployed UI remain unverified.

A combined archive-read command exceeded displayed-output capacity; the directly relied-on overview proposal was subsequently read separately. This does not justify a claim that every historical artifact or later approval was exhaustively reviewed.

The parent alone accepts findings, checks eligibility and queues any publication. This report does not change historical ledger coverage or feature checkboxes.