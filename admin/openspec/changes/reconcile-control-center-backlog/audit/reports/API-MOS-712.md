# API-MOS-712 — contract-preparation obligation reconciliation

## Result

**Partial documentary coverage; not delivery or DoD closure.** The exact MOS-712 body is available and mapped below. Saved wiki241082009 documents most requested operations, but delegates history elsewhere; its contracts differ materially from local OpenAPI and subsequently captured API descriptions. History’s requested offset/total pagination is not supplied by the saved audit-service query contract.

No product publication, policy selection, implementation change, coverage promotion or task closure is proposed automatically. Parent alone accepts and queues candidates.

`A` = `openspec/changes/reconcile-control-center-backlog/audit`. All paths are repository-relative unless stated otherwise.

## Sources, authority and prior-work boundaries

### Exact assigned member

`A/sources/jira-surface-details-d095/r1/content.json#/items/3`:

- Key: **MOS-712**, “[B] Подготовить контракты регистрации и конфигурирования поверхностей”.
- Status: `Review`; updated `2026-10-16T19:22:16.063+0800`.
- Item retrieval: `2026-10-20T16:56:26.334Z`; packet retrieval: `2026-10-20T16:56:26.589Z`.
- `/description` contains seven “Что делаем” bullets and five DoD bullets.
- `/comments/total=0`, `/comments/items=[]`, `/attachments=[]`.
- These are saved observations, not acceptance or execution evidence. Custom acceptance fields and linked resources were not collected by this run.

### Documentary inputs

- **W:** `A/sources/wiki-241082009/r2/content.json#/bodyView`, complete body inspected inertly. Page revision **5**, body contract **v1.0**, dated 08.09.2026; captured `2026-10-16T12:28:15.837Z`. Section numbers below refer to this body.
- **L:** `docs/api/contracts/surfaces.openapi.json`. Its surface path objects equal those in `docs/api/contracts/openapi.json`; no surface operation descriptions are present in this local snapshot.
- **R:** `A/sources/api-live/r1/content.json`. Saved subsequent API publication, not a request to the backend during this audit. Scoped surface operation descriptions were inspected.
- **H:** `A/sources/wiki-241077434-readable/r1/content.txt:252–334`, audit-service §3.2 search contract. Used only for the history-pagination obligation, alongside the existing audit-service report.
- Supplementary local documentation: `docs/api/contracts/surfaces.md` and `surface-error-provenance.md`.

The initial guessed `wiki-241082009/r1/content.md` does not exist. This is **not a missing-source blocker**: r1 contains the retained failed collection receipt; the authoritative available body is r2, explicitly identified by D-005. No replacement source or external fallback was used.

### Prior evidence read and preserved

- `A/reports/JIRA-MOS-783.md`: exact member inventory, previously missing MOS-712 description.
- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md`, `A/reviews/RECON-MOS-959-CONTRACT.md`, `A/decisions.md` D-004/D-005: preserve established configuration differences and deferral; do not re-credit MOS-959/1237.
- D-090/D-091 decisions and `A/publication/DRAFT-SURFACE-D091.md`: text presentation/domain-input feedback remain separate, unpublished candidates; no ownership transferred here.
- `A/reviews/R-D093-EIGHT.md`: sandbox session, chat and synchronization members remain distinct from surface lifecycle endpoints.
- `A/reports/DELTA-SURFACES-ROOT-BRIEF.md` and `DELTA-AUDIT-SERVICE-CONTRACT.md`: contextual maps, not substitutes for the exact MOS-712 body.

MOS-712 owns **contract preparation/completeness**. MOS-901 owns backend implementation; MOS-910 registry integration; MOS-911 skill selection; MOS-913 overview/connection; MOS-914 lifecycle; MOS-958 registration transport. This report does not award those members coverage.

## Exact pointer notation

For L and R:

- `S = /paths/~1api~1control~1api~1surfaces~1v1~1surfaces`
- `C = /components/schemas`
- List/create: `S/get`, `S/post`
- Detail: `S~1{surface_id}/get`
- Configuration: `S~1{surface_id}~1configuration/put`
- Skills: `S~1{surface_id}~1enabled-skills/put`
- Commands: `S~1{surface_id}~1{command}/post`, substituting the literal command name.

For R, append `/description` for prose claims. W references identify `/bodyView` by numbered heading and named subsection; examples are documentary, not observed responses.

## All-obligation matrix

“Documented” below means available text/schema, **not agreed authority, deployed behavior or task completion**.

| MOS-712 obligation | Expected | Observed, exact evidence | Unknown / bounded disposition |
|---|---|---|---|
| Work 1: registry, search/filter/sort/pagination, draft creation, card and editing | Contracts for all listed operations | W §§2.1,2.3–2.5; L list/create/detail/configuration paths. List parameters include query/status/type/sort, limit 1–100 default20, offset≥0 default0. | No general surface-metadata update operation among inspected surface paths. “Editing” is covered for configuration/skills, not established for every registration field. Ask owner to delimit the intended editing obligation. |
| Work 2: surface/configuration model, identifiers, names, type, purpose/context, domains, team/responsibles | Explicit schemas | W §§1.1–1.3; L `C/CreateSurfaceRequest`, `SurfaceDetailResponse`, `SurfaceResponsibleRequest/Response`, `SurfaceResponsibleUserResponse`. | W uses `type`, server-derived team, name strings and `checking`; local create uses `surface_type`, required `team_id`, business-user IDs, and `review`. W optional context differs from required local string. Historical schema is not a payload recipe. |
| Work 3: skill domains, individual skills, parameters and stored per-skill values | Catalog/schema, persistence and validation | W §§1.3,2.2,2.5 describes grouped `/available-skills`, select parameters, per-skill values and save validation. L `C/SurfaceSkillRequest` stores `skill_id` plus string-valued parameters; separate enabled-skills PUT exists. R create/skills descriptions specify required/unknown/options validation. | Local aggregate has no `available-skills` path. Main `surface-skill-selection` instead requires paginated skills list with `status=prod` and skill detail. W combined configuration/skills save is a known D-005 divergence, not a new frontend defect. |
| Work 4: widget colors, greeting/fallback, suggestions, cards/actions | Widget contract | W §1.3/§2.5; L `C/UpdateSurfaceConfigurationRequest`, `SurfaceCardRequest`, `SurfaceCardActionType`; R configuration description adds exact placeholders, conditional fallback, limits and link rules. | Local action enum has only `message,skill`; saved R adds `link` and bounds absent locally. W font/shape/nullability/default differences remain D-005-owned reconciliation. No configurator activation. |
| Work 5: save, sandbox, publish, connection code; immediate Prod changes without republication/re-embedding | Operations plus application semantics | W §§1,2.4–2.7 explicitly states immediate Prod application and unchanged code/status. L contains configuration, sandbox, publish and detail connection schemas. R configuration says full replacement and unchanged widget token/embed code. | Immediacy is a wiki claim, not measured propagation. W sandbox prerequisite conflicts with R publish description permitting non-draft publication without sandbox. Approved MVP excludes sandbox workflow; do not choose policy from this discrepancy. |
| Work 6: disable, enable, archive disabled, restore, action history | Lifecycle and history contracts | W §§2.8–2.11 and L corresponding commands cover lifecycle. R describes prod→disabled, disabled→configured/archived, archived→configured. W §1 explicitly delegates history to audit Query API with object type `surface` and `surface_id`. | History is **delegated**, not implemented by a surface endpoint. No surface-history/audit path exists in local aggregate. Saved H is a separate service contract, not accepted surface integration or evidence of emitted events. |
| Work 7: network-domain occupancy and channel formation from primary address | Explicit rules | W §2.3 prohibits occupied domains and says channel derives from first domain. R create description adds case-insensitive occupancy and first label + `-web`, e.g. `portal.example.org → portal-web`. | No deployed uniqueness, concurrency or channel-collision behavior verified. UI must not generate channel IDs or infer domain availability from these descriptions. |
| DoD 1: agreed-format contract for registry/registration/card/configuration/sandbox/publication/state/history/code | Complete contract package and agreement | OpenAPI covers 11 surface operations; W provides examples, narrative and history delegation; code is returned in detail, not a separate code endpoint. | Format acceptance/sign-off not present in exact MOS-712 comments. History integration and broad editing scope remain qualified. Operation existence is not whole-DoD completion. |
| DoD 2: registry **and history** pagination with size, offset, total | All three pagination properties for both | W §2.1 and L `C/PaginationDto` supply registry limit/offset/total_items plus page fields. H §3.2 supplies limit/cursor, `next_cursor`, `has_more`. | **Explicit documentary mismatch:** H says keyset, not offset, and no total count. Do not synthesize totals, reuse registry pagination or silently amend MOS-712. Owner reconciliation required. |
| DoD 3: schemas for surface/configuration/widget/settings/states | Explicit model definitions | W §§1.1–1.3 and L named Surface schemas provide these. | Versioned differences remain: `checking/review`, configuration enums/nullability, defaults, write responsibilities and statistics shape. Existence does not mean cross-source consistency. |
| DoD 4: skill parameter schema, per-skill values, save validation | Definitions and validation contract | W §2.2 parameter table, §2.5 unknown/required/out-of-range rejection; local string dictionary; R create/skills descriptions give parameter pointer and codes. Main skill-selection spec supplies UI ownership/default rules. | Actual backend validation untested. R documents duplicate skill IDs ending in 500; this is documented defect behavior, not desired validation or permission to weaken deduplication. |
| DoD 5: examples for incomplete configuration, occupied domain, invalid parameter, publication before sandbox, successful publication | Five distinguishable examples | W §2.13 contains full missing-greeting envelope; §2.3 “Занятый адрес” full409 envelope; §2.5 supplies invalid-parameter conditions/path; §2.7 supplies sandbox prerequisite409 and full successful publication200. | Invalid-parameter and pre-sandbox cases are prose/code examples, not full serialized envelopes. Whether that satisfies “examples” needs owner judgment. Pre-sandbox failure is contradicted by R’s no-sandbox-required description. None is execution proof. |

## Important current-document distinctions

1. **Local snapshot versus saved later publication.** L surface descriptions are absent; local card actions lack `link` and configuration schemas lack later text/list bounds. R supplies those facts. Do not describe them as globally undocumented merely because they were not imported locally.

2. **Error provenance has a historical cutoff.** `surface-error-provenance.md`, “Backend evidence (unresolved)”, explicitly relies on 15.10 raw inputs and holds archived task3.2. R create description now documents domain409 with `/domains` and `details.domains`, unknown-user422 with `/responsible/product`, and configuration validation pointers. W’s older domain example uses `/domains/0`. This supports a narrowly attributed documentary update candidate, **not automatic release-gate clearance or adapter implementation**.

3. **Do not flatten contracts.** W registry response uses `data.surfaces`, create uses `data.surface`, detail wraps `data.surface`; local contracts use `data.items`, create `data.id`, and direct detail data. Current client follows the latter. No compatibility aliases are selected here.

4. **History availability is not acceptance.** H documents a query API, so “no history document exists” would be inaccurate. Its pagination explicitly fails to match MOS-712’s literal offset/total wording. Service routing, credential destination, surface event projection, retention and authorization remain outside this row’s authority.

## Code, specification and test locators

### Static code boundaries

`app/entities/surface/api/surface-registry-client.ts`:

- `getSurfaceRegistry`: transmits query/status/type/sort, page size and calculated offset; reads `items` and `pagination.total_items`.
- `getSurfaceDetails`: detail endpoint, runtime schema and requested-ID consistency.
- `updateSurfaceEnabledSkills` versus `updateSurfaceConfiguration`: separate PUT operations.
- `runSurfaceLifecycleAction`: command-specific bodyless POST.
- `createSurface`: POST expecting201 and `data.id`.

These establish frontend transport ownership, not backend implementation or all model semantics.

### Existing assertions inspected

`app/entities/surface/api/surface-registry-client.test.ts`:

- `:83` filters/sort/offset and nullable/zero statistics assertion.
- `:123` null-object/null-field/zero/number statistics cases.
- `:389–417` exact enabled-skills payload and response.
- `:418–438` preservation of validation refusal.
- `:441–478` bodyless lifecycle POST mapping.
- `:480–520` invalid status/timestamp and HTTP error handling.
- `:522–555` generated configuration request and parsed response.

The lifecycle test uses `prod` fixtures across commands: it is **not** proof of the correct transition matrix or sandbox testing. No tests were run.

### Specification and change ownership

- `openspec/specs/surface-registration/spec.md`: **Responsible assignments use business user identifiers**, **Creation supports an atomic optional configuration**, **Rejections are distinct from unknown creation outcomes**.
- `openspec/specs/surface-skill-selection/spec.md`: **Contract-backed skill catalog**, **Schema-driven parameters**, **Parameter ownership and draft preservation**, **Registration and existing surface persistence**.
- `openspec/specs/surface-lifecycle-publication/spec.md:179–196`: explicit deferred configurator/history boundaries; no hidden configuration PUT, sandbox or invented audit call.
- Registry requirement locator is archived: `openspec/changes/archive/2026-09-28-surface-registry/specs/surface-registry/spec.md`, **Server-backed registry**, **Persistent query state**, **Nullable statistics**. The guessed main path `openspec/specs/surface-registry/spec.md` is absent; no main-spec existence or sync is inferred. Historical role clauses are not adopted as current auth policy.
- `openspec/changes/archive/2026-10-15-update-control-center-api-contracts/{proposal,design,tasks}.md`: read for migration/default/error boundaries. Tasks3.1/3.2 distinguish recorded missing evidence from unfinished real-error classification; checked tasks are historical records, not fresh verification.

## Bounded publication candidates — parent queue only

| Candidate | Disposition | Exact ownership and limit |
|---|---|---|
| **712-01** | **KEEP / evidence update** | Attach this all-obligation matrix to exact MOS-712. Replace its old description-unavailable classification only after parent acceptance. No neighboring member promotion or feature closure. |
| **712-02** | **QUESTION** | Reconcile MOS-712 history offset/total requirement with W’s delegated audit ownership and H’s explicit cursor/no-total contract. Do not create an endpoint or choose pagination policy. |
| **712-03** | **UPDATE candidate** | Qualify local surface error/documentation-absence wording with its 15.10 cutoff and R’s later published descriptions. Existing contract/error owners retain implementation and release-gate decisions. |
| **712-04** | **KEEP existing question, no duplicate plan** | Preserve D-005 configuration vocabulary/nullability/default/combined-write differences and deferred activation. Preserve D093 sandbox/session ownership. |
| **712-05** | **QUESTION** | Confirm whether “editing” includes registration-field updates and whether prose-only invalid-parameter/pre-sandbox examples satisfy MOS-712 DoD. No missing-feature verdict solely from ambiguous wording. |

**No new product implementation change is proposed by this row.**

## Independently computed input hashes

| Input | SHA-256 |
|---|---|
| `A/work-items/WAVE-D095-SURFACE-TEN.md` | `046950ae1d91be8202c0e645057b66a58f19243a929f1af676df779441a04af0` |
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| Same packet `metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `A/sources/wiki-241082009/r2/content.json` | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` |
| Same wiki `metadata.json` | `93ef4e0e138e69b76c1810b86596b8668a49bac448ff15f9bd9c987499b8d183` |
| `A/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `A/sources/wiki-241077434-readable/r1/content.txt` | `0ec8881c582231ef07e566b51e4120e6602876c090e353177265775fec583a83` |
| `docs/api/contracts/surfaces.openapi.json` | `9d8ef7ff68e187cebb051e6ee85a9ad333f0af903537a5e181425694c48d9758` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `docs/api/contracts/surfaces.md` | `04b31f1bbf9a8359f2a8d455080855c006736d11b3628b4666dbb624020b9257` |
| `docs/api/contracts/surface-error-provenance.md` | `4c9dc8882222f9ec0e64a18d05090561d1053ce17498de4f38ab37fb92c90e0a` |
| `app/entities/surface/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| Same directory `surface-registry-client.test.ts` | `4d5f93269521aedb76ce4dd722390c92dfa06e86b63af622f952146ef105c886` |
| `openspec/specs/surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| `openspec/specs/surface-skill-selection/spec.md` | `e27eb8b354e4370da3519b5387cff5369a2f083e6c3be05f82d8631746c19ee0` |
| `openspec/specs/surface-lifecycle-publication/spec.md` | `675265a0ba98b45f1d659f6048fe97f2e590a0597d7eda304cdcfe9854ebdd91` |
| Archived registry delta cited above | `7895c5b5e6e66f066138b541eb16b3a1dde760c591f92e3c82f2d919dd1bccdf` |
| `A/reviews/RECON-MOS-959-CONTRACT.md` | `ef2e754d63a4cccd7f807b60009c14381d2099f9f608db87ed75c63e82a35713` |
| `A/reviews/R-D093-EIGHT.md` | `aee6c464b24662ed9e5396e382ca2e35a3add12ffe47a6c452178f847084e2bc` |

## Limitations and execution record

- Fresh Jira collection does not refresh the saved wiki/API sources or clear publication gates.
- No backend storage, domain uniqueness, parameter enforcement, external surface-service application, audit emission, ACL, production availability or propagation latency verified.
- Source versions and dates do not select authority. Existing approved frontend boundaries remain intact.
- No network/browser/business API, tests/build/typecheck/lint/format, writes, Git mutation, configuration change or nested agents.
- Local reads and read-only Python JSON/HTML parsing/hash comparison only. Exploratory absent paths were distinguished from available mandatory r2 evidence.
- Git/index state was not inspected; no clean-tree or staged-files attestation.
- This complete Markdown is returned for runtime persistence at the assigned output path; the analyst did not write it.