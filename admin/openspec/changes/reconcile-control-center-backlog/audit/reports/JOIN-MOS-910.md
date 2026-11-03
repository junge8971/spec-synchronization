# JOIN-MOS-910 — server-backed surface registry

## Result and scope

**Bounded static join completed for MOS-910 only; parent acceptance remains pending.** Current implementation supports the registry endpoint, server query parameters, Russian labels and null-versus-zero statistics. The exact Jira wording `data.surfaces` differs from the implemented and published `data.items`; the archived agreed design explicitly chose `items`, not a dual-format fallback.

No product publication, coverage transition, policy selection or feature closure is proposed as accomplished. No files were written, tests executed or external services accessed.

Paths below are repository-relative:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `R` = `openspec/changes/archive/2026-09-28-surface-registry`
- `E` = `app/entities/surface`
- `W` = `app/widgets/surfaces-registry/ui`
- `F` = `app/features/surface-registry-filter/model`

## Source and prior evidence

### Exact member source

`A/sources/jira-surface-details-d095/r1/content.json#/items/5`:

- Key: **MOS-910**.
- Summary: `[FE][Поверхности] Доработать список поверхностей и подключить серверные фильтры`.
- `/description` explicitly requests:
  - real endpoint and `data.surfaces/data.pagination` mapper;
  - headings/statuses matching the new prototype;
  - Russian labels for `portal/portal_section/mobile_application`;
  - dialogs from `stats.dialogs_30d`, with `stats=null` representing unavailable statistics;
  - `query`, `status`, `type`, `sort`, `limit/offset`.
- Linked contract: wiki page **241082009**. No external link traversal occurred.
- `/status`: `Testing`; `/updated`: `2026-10-19T14:58:33.109+0800`.
- `/retrievedAt`: `2026-10-20T16:56:26.422Z`.
- `/comments/total`: 2, matching two returned comments:
  - `/comments/items/0`, ID `1114072`: estimate, not execution evidence.
  - `/comments/items/1`, ID `1118220`: linked draft MR 10 mentioning MOS-910. MR contents were not fetched; this does not prove merge or deployment.
- `/attachments`: empty. No prototype image/body was obtained from this item.

Packet metadata records collection completion at `2026-10-20T16:56:26.589Z`. These are distinct item/packet timestamps. Membership verification against MOS-783 is parent-recorded metadata, not independently re-performed here.

### Prior evidence and ownership preserved

Before implementation inspection, read:

- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md`
- `A/reviews/R-SURFACE-CONFIG.md`
- `A/publication/DRAFT-SURFACE-D091.md`
- `A/decisions.md`, D-090–D-094.

These preserve configurator deferral, separate MOS-1166/1167 registration feedback candidates, and sandbox/lifecycle boundaries. None supplies registry delivery proof.

`A/reports/DELTA-SURFACES-ROOT-BRIEF.md` was additionally read **after** the primary registry inspection. Its DSRB-01 remains documentary list intent, not a previous implementation acceptance. This late supplemental read is disclosed rather than represented as prior-first inspection.

Ownership remains exact:

- **MOS-910:** actual server registry transport/envelope, request semantics, labels and registry statistics.
- **MOS-707:** historical table/page presentation and attachment parity.
- **MOS-708:** historical search/filter/pagination/URL expectations; current URL machinery is cited here only as MOS-910’s transport path.
- **MOS-911/913/914/958:** selection, detail/connection, lifecycle and registration transport remain separate.
- Accepted MOS-1110/1164–1167 work is neither reopened nor credited as MOS-910 completion.

## Agreed specification and historical limitations

Read `R/proposal.md`, `R/design.md`, `R/specs/surface-registry/spec.md` and `R/tasks.md`.

Relevant exact requirement locators in the archived spec:

1. **Server-backed registry**
2. **Persistent query state**
3. **Prototype labels and API values**
4. **Nullable statistics**

The archived design, **Decision 1**, expressly selects `data.items`, rejects unconfirmed automatic support for `data.surfaces`, preserves server filtering/sorting, and permits explicitly requested page size 10 despite API default 20.

**Decision 2** deliberately permits `stats:null` through a local compatibility type without rewriting generated OpenAPI types; omitted `stats` is not implicitly permitted.

A bounded search of `openspec/specs` for `Server-backed registry`, `Nullable statistics`, `data.surfaces` and `MOS-910` returned no matches. Therefore this report cites the **archived registry spec**, not an invented current main `surface-registry` capability. Main-spec synchronization is a parent-owned question, not an authorized edit.

The archival documents reference `docs/MOS-910-backend-questions.txt`. Reading that exact path returned **ENOENT**, and filename discovery under `docs` found no `*910*` file. Consequently:

- Backend answers and historical execution results allegedly recorded there cannot be verified.
- Checked archive tasks do not substitute for that missing evidence.
- This missing historical reference does not prevent the primary-source/code join, but blocks verification of that historical journal’s claims.
- No replacement journal or fallback evidence was invented.

Historical role assumptions and E2E task instructions in the archive are not current authorization. This inspection neither reopens auth policy nor runs browser tests.

## Expected / observed / unknown matrix

| Obligation | Expected | Observed locally | Unknown / boundary |
|---|---|---|---|
| Endpoint | Real surface list endpoint | `E/api/surface-registry-client.ts#getSurfaceRegistry` calls `/surfaces/v1/surfaces`; its API test asserts full path `/api/control/api/surfaces/v1/surfaces`. | No deployed request was made. |
| Envelope | Jira says `data.surfaces`; archived agreement says `data.items` | `app/shared/api/http-client.ts#unwrapEnvelope` returns envelope `data`; `getSurfaceRegistry` validates `{items,pagination}` and maps `items` directly. Published local response schema also requires `items`. | Fresh Jira wording still differs. No evidence authorizes switching to `surfaces` or accepting both. |
| Filters | `query/status/type` sent to server | `getSurfaceRegistry` sends all three; `F/registry-search-params.ts#parseSurfaceRegistrySearchParams` preserves query and recognizes contract status/type values. Filter handlers update URL through the shared parameter helper. | Actual backend matching/access-controlled result correctness unverified. |
| Sorting | Contract sort values, no local page sort | `surfaceRegistrySortValues` supplies five fields with ascending/descending forms. Sort handler updates URL; registry renders response order without a local sort. | Backend collation/tie handling and computed dialog ordering are not demonstrated by client tests. |
| Pagination | `limit/offset`, server total | Client sends `limit=pageSize`, `offset=(page-1)*pageSize`; maps `total_items` and response `limit`. Widget counts `total`; pagination computes `ceil(total/pageSize)`. | Client returns requested page, not server `current_page`; server consistency is assumed, not runtime verified. |
| URL handoff | Preserve conditions; reset page when conditions change | Parameter helper resets page for query/status/type/sort changes unless an explicit page is supplied. Query key includes the full request; AbortSignal reaches client. | Historical MOS-708 equivalence remains a distinct owner’s question. |
| Headings and type/status labels | Russian labels and canonical API values | Table shows Поверхность, Тип, Владелец, Статус, Диалогов, Обновлена. Constants map all three types and seven statuses, including `review → Проверка`. | Exact “new prototype” visual parity cannot be established from this source packet. |
| Registry statistics | `dialogs_30d`; null means unavailable; zero preserved | List schema accepts null object and null numeric field. Table uses `surface.stats?.dialogs_30d?.toLocaleString('ru-RU') ?? '—'`, preserving zero. `<abbr title="За последние 30 дней">` labels the period. | No live statistics calculation demonstrated; omission of `stats` remains invalid. |
| Frontend/server separation | Server selects/orders/pages results | `W/surfaces-registry.tsx` consumes query data directly; local filtering/sorting found in the **test response fixture**, not production table logic. | Fixture behavior is not backend implementation evidence. |

## API pointers and remaining contract distinction

For both JSON documents below, define:

`P = /paths/~1api~1control~1api~1surfaces~1v1~1surfaces/get`

### Current local contract

`docs/api/contracts/surfaces.openapi.json`:

- `P/parameters/0..5`: query, status, type, sort, limit, offset.
- Limit schema: minimum 1, maximum 100, default 20; offset minimum/default 0.
- `P/responses/200/content/application~1json/schema/$ref`:
  `#/components/schemas/TsamResponseSchema_PaginatedResponseSchema_list_SurfaceListItemResponse___`.
- That component’s `/properties/data/$ref`:
  `#/components/schemas/PaginatedResponseSchema_list_SurfaceListItemResponse__`.
- Paginated component `/properties/items` and `/properties/pagination`; both required.
- `/components/schemas/SurfaceListSort/enum`: `name`, `type`, `owner`, `dialogs`, `updated_at`, each with optional leading `-`.
- `/components/schemas/SurfaceListItemResponse/properties/stats`: non-null `$ref`.
- `/components/schemas/SurfaceStatsResponse/properties/dialogs_30d`: integer or null.

Thus **nullable fields are published, but nullable whole `stats` remains a deliberate frontend extension** in `E/model/types/surface.types.ts#Surface`.

`docs/api/contracts/surfaces.md` points to that OpenAPI and contains registration compatibility notes; it does not itself resolve whole-object list-statistics nullability or the Jira `surfaces` name.

### Saved later API publication

`A/sources/api-live/r1/content.json`, same `P/description`, additionally documents:

- case-insensitive substring search across name, configuration name, domains, channel ID and owner;
- trim/empty-query behavior and `%`/`_` wildcard semantics;
- identifier tie-breaking;
- `dialogs` sorting only by identifier because the service does not calculate dialog counts;
- empty pages beyond the end;
- statistics fields coming as null.

This is saved publication evidence, **not new live retrieval or execution**. Its structural list-item schema still references a non-null stats object. The wording “Поля `stats` приходят `null`” is not sufficient to silently collapse the object-versus-field distinction.

The test fixture’s `.includes(query)` and numeric dialog comparison do **not** establish wildcard behavior or saved API’s identifier-only dialog sorting. This is a bounded fidelity limitation, not proof of production client-side sorting or a mandate to change mocks.

Security normalization differences in saved versus local API are outside MOS-910 and remain under already accepted auth/API ownership.

## Test evidence read, not executed

| Locator | Assertions inspected |
|---|---|
| `E/api/surface-registry-client.test.ts`, **uses API filters/sort/offset and preserves nullable fields and zero statistics** | Exact full endpoint, combined six parameters, page 3 → offset 20, total 25, null channel and numeric zero. |
| Same file, **accepts missing statistics as a null object, a null field, zero, or a number** | Four fixtures produce null/null/0/42. Despite its title, this does not test omitted `stats`. |
| Same file, **rejects invalid UUIDs and timestamps in the API response** | Boundary validation rejects malformed response fields. |
| Same file, **forwards cancellation to fetch** | Signal forwarding. |
| `W/surfaces-registry.test.tsx`, **shows contract fields and distinguishes a real zero from null** | Total count, table row count, visible zero/dash and dialogs heading. Null-object/null-field fixtures exist, but dash assertions are aggregate rather than row-specific. |
| Same file, **uses canonical status and surface type values**, **offers the contract statuses in the filter** | Review/mobile labels and all seven statuses. |
| Same file, **navigates between API pages**, **resets pagination after changing a filter**, **uses API sort strings when selecting a sortable column** | URL and display consequences of paging/filter/sort actions. |
| Same file, **restores all registry conditions from a direct URL and browser history** | In-memory-router URL restoration; not browser execution. |
| `F/registry-search-params.test.ts` | Canonical parameters, legacy-value removal, invalid page boundaries, preservation of unrelated params, page reset and sort toggling. |

No test execution or historical pass attestation is made. Existing null/zero assertions could be strengthened with row-specific checks; that is an optional bounded evidence improvement, not a proven rendering defect.

## Bounded publication candidates — queue only

1. **KEEP — existing MOS-910 registry owner.** Preserve server transport, `items` mapping, canonical values, total-based paging and null/zero rendering. No duplicate implementation change is justified by the static inspection.
2. **UPDATE — reconciliation evidence only.** Record the exact Jira `surfaces` versus agreed/OpenAPI `items` discrepancy and whole-object-null compatibility separately. Do not rewrite historical Jira wording or add a fallback mapper.
3. **QUESTION — contract/documentation owner.** Confirm the intended whole-object-null shape and whether the missing historical backend-question journal has a preserved authoritative location. Do not select the answer here.
4. **QUESTION — specification stewardship.** Parent may examine why the registry agreement exists in archive but was not found under main specs. No main-spec sync or new capability publication is performed.
5. **OPTIONAL TEST CANDIDATE — existing registry owner.** Row-specific null-object/null-field/zero assertions and explicit distinction between fixture sort/search behavior and published backend semantics. No new product policy or mandatory defect claim follows.

No new product change is proposed for historical prototype parity, auth, lifecycle, configurator or neighboring registration work.

## Input fingerprints

SHA-256 computed from complete local file bytes:

| Input | SHA-256 |
|---|---|
| `A/work-items/WAVE-D095-SURFACE-TEN.md` | `046950ae1d91be8202c0e645057b66a58f19243a929f1af676df779441a04af0` |
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| Same directory `metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `A/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `docs/api/contracts/surfaces.openapi.json` | `9d8ef7ff68e187cebb051e6ee85a9ad333f0af903537a5e181425694c48d9758` |
| `R/specs/surface-registry/spec.md` | `7895c5b5e6e66f066138b541eb16b3a1dde760c591f92e3c82f2d919dd1bccdf` |
| `E/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `E/api/surface-registry-client.test.ts` | `4d5f93269521aedb76ce4dd722390c92dfa06e86b63af622f952146ef105c886` |
| `W/surfaces-registry-table.tsx` | `00e15f25c4a3d6c52f050ddac427bdf88ac1c3f7843cc76a316d03e872150824` |
| `W/surfaces-registry.test.tsx` | `dc780c80f7f731076e667d57174313d1d1242222c655e8a36d4c3ba52865015e` |
| `F/registry-search-params.ts` | `265318604d7244312ff78c752f6eef4cc174c098deab34764d73142783ed9fce` |
| `F/registry-search-params.test.ts` | `7fa0e55072a08957bc628d080efc51b4b40f4aaa1399f85f2bd09da2aaa03671` |
| `app/shared/api/http-client.ts` | `e3ca2dbf67139ed26e86220a44dc18503068835d390f659c0eb2577fed5f1514` |

## Limitations

No network/browser/business API, tests/build/typecheck/lint/format, git mutation, nested agents or configuration changes. Mandatory exact task packet was available and matched its recorded digest. Missing archival journal is explicitly excluded from verified evidence.

Historical status, draft MR mention, archived checked tasks and test source cannot establish release, backend filtering correctness, permissions enforcement, statistics calculation or deployment. Prototype parity remains unknown. Fresh collection of this Jira packet does not clear other publication freshness gates. Git/index state was not inspected.