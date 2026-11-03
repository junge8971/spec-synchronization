# JOIN-MOS-958 — registration transport and dependency reconciliation

## Result and scope

**Bounded static join completed for MOS-958 only.** The current frontend implements the principal registration fields, business-user selection, draft/review POST and server-confirmed channel display. It deliberately does not implement global domain-occupancy preflight or editable greeting/configuration in the wizard.

The saved Jira issue remains **Hold**, explicitly dependent on **MOS-1336**. Later local specifications resolve the responsible-user representation and permit omission of configuration from this wizard. Neither those decisions nor current code establish completion of MOS-958 or deployment of its dependency.

A substantive remaining seam is error compatibility: the saved newer API description documents domain/user/configuration rejections, whereas the current adapter recognizes only structured HTTP 422 `detail[]`. This supports a bounded follow-up to the existing error-integration gate, not automatic implementation or closure.

No files were written. This report is returned for runtime persistence at the assigned authoritative output path.

### Path abbreviations

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `F` = `app/features/surface-registration`
- `W` = `app/widgets/surface-registration/ui/tests/surface-registration.test.tsx`
- `C` = `openspec/changes/archive/2026-10-15-update-control-center-api-contracts`

## Source and prior-evidence boundaries

### Exact fresh source

`A/sources/jira-surface-details-d095/r1/content.json#/items/9`:

| Pointer | Evidence |
|---|---|
| `/key`, `/summary` | MOS-958, “[FE][Поверхности] Доработать мастер поверхности и подключить регистрацию” |
| `/description` | Surface/configuration names, type, domains, purpose, product_context, owner and two responsible assignments; channel_id from server response; scenarios and greeting in resulting configuration; draft/review POST; no defined global pre-submit occupancy check; checking an available registry page is insufficient. |
| `/status` | `Hold` |
| `/updated` | `2026-10-16T19:22:26.182+0800` |
| `/comments/items/0` | Comment `1126733`: estimate 3, not acceptance evidence. |
| `/comments/items/1` | Comment `1130748`: historical MR36 mention on branch MOS-958, not inspected implementation or merge evidence. |
| `/comments/items/2` | Comment `1130808`: API partly unimplemented; MOS-1336 created to update it; full implementation described as impossible before that update. |
| `/comments/total` | 3; all three returned. |
| `/attachments` | Empty returned array. |
| `/retrievedAt` | `2026-10-20T16:56:26.589Z` |

Adjacent `metadata.json` records parent-owned retrieval, ten exact keys, complete returned comment counts and membership verification against saved MOS-783 children. Linked issues, MRs, custom fields and attachment bodies were not collected. The linked wiki IDs **241082009** and **238347672** are source references, not evidence that their linked contents were freshly inspected here.

### Prior work consulted

Before implementation inspection, read the surface-config recovery report and independent review, D091 surface draft, D091 recovery review, D093 review and relevant decision excerpts. Their controlling boundaries are preserved:

- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md` and `A/reviews/R-SURFACE-CONFIG.md`: published configuration constraints do not activate the deferred editor or establish backend correctness.
- `A/publication/DRAFT-SURFACE-D091.md`, `A/reviews/R-D091-RECOVERY.md`, decisions D090–D091: MOS-1166 text presentation and MOS-1167 local domain reflection remain distinct owners. Domain reflection is not occupancy confirmation.
- `A/reviews/R-D093-EIGHT.md`, decision D093: no sandbox activation or runtime inference from lifecycle transport.
- Subsequently consulted `A/reports/DELTA-SURFACES-ROOT-BRIEF.md` as a documentary ownership map, not a substitute for exact MOS-958 evidence.

Owning artifacts inspected: main `surface-registration` specification; `C/proposal.md`, `design.md`, `specs/surface-registration/spec.md`, `tasks.md`; main lifecycle deferral at `openspec/specs/surface-lifecycle-publication/spec.md:179–196`.

No neighboring member is claimed covered by similarity.

## Expected / observed / unknown

| Obligation | Expected | Observed static implementation and assertions | Unknown / disposition |
|---|---|---|---|
| Registration fields and POST | Exact MOS-958 description requires listed fields and draft/review submission. | `F/model/to-create-surface-request.ts:7–26` maps names, type, normalized domains, purpose/context, owner, two IDs, team, prepared skills and `submit_for_check`. `app/entities/surface/api/surface-registry-client.ts`, `createSurface`, performs POST `/surfaces/v1/surfaces`, requires 201 and validates returned UUID ID. `F/model/tests/surface-registration.test.ts`, “maps a normalized contract request with review=%s”, covers both booleans. | Actual backend acceptance and persistence unverified. No frontend delivery claim. |
| Responsible identity | Historical source calls string-versus-employee-reference model undefined. | Main `surface-registration/spec.md:9–21` explicitly selects business-user IDs, not arbitrary names or UUID-only values. `F/ui/steps/responsible-user-field.tsx` uses public `searchBusinessUsers`, query/offset pagination and abort signal; legacy strings are cleared for explicit reselection. Mapper extracts `.id`. | Historical ambiguity is resolved in the inspected local agreement, not by inventing a new identity model. Directory deployment and old backend assignments remain unverified. |
| Server channel ID | Client must not compute channel_id. | Mapper contains no channel field. `F/ui/steps/surface-details-step.tsx:58–73` states occupancy is unverified and channel assigned after creation. Attempt controller retains POST ID then performs fresh detail read. W:623–646 asserts server channel rather than cached channel; W:704 onward includes null-channel/server-draft behavior. | Newer API prose describes a server derivation algorithm; it does **not** authorize duplicating that algorithm in the client. |
| Global occupancy boundary | A registry page cannot establish global availability; contract returns conflict on creation. | First step makes no availability claim. W:173, “uses local domain validation without searching the registry or generating a channel”, is the explicit regression locator. Main registration owns confirmed conflict handling, not a new preflight endpoint. | No occupancy API selected. Global race safety, database uniqueness and deployment are backend unknowns. MOS-1167’s separate local-input feedback candidate must not be absorbed here. |
| Scenarios and greeting | Historical description includes both in resulting configuration. | Mapper sends prepared `enabled_skills`. Main registration `:23–40` permits an editor-less wizard to omit configuration and use backend defaults. W:770–818 asserts one draft creation and absence of both `greeting` and `configuration`. Model test explicitly requires “no greeting”. | This is a scope reconciliation, not fulfillment of an editable greeting requirement. Configurator activation remains separately deferred; no hidden configuration PUT or invented defaults warranted. |
| Draft versus review | Submit according to POST schema, without inventing success status. | Mapper sends boolean `submit_for_check`. W:290–397 covers review request; W:770–818 covers draft. `F/model/use-surface-registration-attempt.ts` confirms through GET rather than assigning requested state locally. | Backend may return a state different from requested; actual returned state remains authoritative. |
| Known rejection versus unknown outcome | Main spec requires reliable field errors and preservation; unknown POST outcome must not permit blind replay. | `F/model/registration-rejection.ts:4–8` accepts only ApiError HTTP 422 matching `validationErrorSchema`. Attempt controller maps reliable `loc` fields, preserves snapshot, permits corrected explicit submission only on recognized rejection; otherwise locks unknown outcome. W:505–550 covers network/503/abort/malformed 201/invalid 422; W:552–592 covers recognized validation correction; W:594–621 covers GET-only retry. | Newer published domain/user/configuration envelope is not recognized by this adapter merely because its code exists in documentation. Do not declare the source’s domain-conflict UX complete. |
| Hold and MOS-1336 dependency | Preserve explicit historical dependency until independently resolved. | Jira source records Hold and comment 1130808. `C/design.md` identifies MOS-1336 material among migration inputs; `C/tasks.md §3` leaves 3.2 unchecked. Current local documentation explicitly preserves the error-integration gate. | No exact MOS-1336 body or linked MR was traversed. Its complete scope, current status and backend rollout are not established. Hold is not cleared by this report. |

Tests above were **read, not executed**.

## API evidence and the remaining error seam

Two snapshots must remain distinct:

1. Local contract: `docs/api/contracts/surfaces.openapi.json`.
2. Saved later publication: `A/sources/api-live/r1/content.json`, previously captured API evidence, **not a fresh API retrieval during D095**.

Exact JSON pointers in both:

- `/components/schemas/CreateSurfaceRequest`
- `/components/schemas/SurfaceResponsibleRequest`
- `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces/post/responses`

The request schema contains the mapped fields, optional nullable configuration referencing `UpdateSurfaceConfigurationRequest`, string responsible identifiers, and `submit_for_check` default false. POST response definitions retain 201 and 422 schema entries.

The later saved API additionally contains:

`/paths/~1api~1control~1api~1surfaces~1v1~1surfaces/post/description`

Its prose explicitly documents:

- Responsible IDs from the user directory.
- Server-generated channel based on the first domain.
- Case-insensitive domain ownership exclusion.
- 409 `DOMAIN_ALREADY_IN_USE`, `/domains`, and `details.domains`.
- 422 `FAILED` field errors, including `/responsible/product`.
- 422 `VALIDATION_ERROR` for request/configuration structure.
- Staged validation and defaults when configuration is omitted.

The corresponding local split-contract POST description is absent. `docs/api/contracts/surface-error-provenance.md` correctly attributes its unresolved-evidence claim to retained **15 October** inputs, but its present release-gate handoff needs reconciliation against this later published prose. The newer description is documentary progress; it is not an observed sanitized production response or proof that the published wire representation is deployed.

**Additional bounded tension:** newer prose requires nonblank `product_context`, while the mapper and its test intentionally permit trimmed `''`. Likewise, client trimming of surface fields differs from prose stating the server preserves them as sent; that server statement alone does not prohibit client normalization. Record these as contract-comparison questions, not automatic validation changes. Minimum-one selected prod skill remains an agreed UI rule even though the API allows an empty list.

## Bounded publication candidates — parent-owned queue only

| Candidate | Disposition and exact ownership |
|---|---|
| MOS958-K1 | **Keep** existing registration transport, selected business-user IDs, server-read channel, no occupancy preflight and no blind replay. Evidence update only; no duplicate implementation plan. |
| MOS958-U1 | **Update existing error-integration evidence/gate**, anchored to `C/tasks.md §3.1–3.2`, `docs/api/contracts/surface-error-provenance.md`, and main registration “Rejections are distinct from unknown creation outcomes”. Record that later publication supplies error-code/status/pointer prose while the current adapter remains detail[]-only. Preserve historical archive content; any actionable follow-up needs parent ownership, freshness and review. Do not mark 3.2 complete. |
| MOS958-Q1 | **Question:** what precise reviewed/deployed envelope should the real adapter recognize for domain/user/configuration rejection, and does it prove noncreation? No generic 409/422 acceptance or message parsing. |
| MOS958-Q2 | **Question:** reconcile later nonblank product_context prose with current optional UI/model behavior before proposing a narrowly scoped validation change. No policy chosen here. |
| MOS958-K2 | **Keep scope boundary:** scenario payload belongs to registration/skill selection; editable greeting/configuration remains deferred configurator work. Historical source tension remains visible, not silently erased. |
| MOS958-Q3 | **Question:** parent may obtain exact MOS-1336 dependency evidence and deployment confirmation if needed. This report does not infer closure from its mention in migration artifacts. |

No new standalone product capability is justified by this bounded inspection. MOS-709 shell ownership, MOS-911 selection semantics, MOS-913 saved-card behavior, MOS-914 lifecycle, MOS-959 configurator and MOS-1166/1167 presentation candidates remain distinct.

## Input fingerprints

SHA-256 recomputed locally from full file bytes; these identify inspected inputs, not remote authenticity or deployment.

| Input | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| `A/sources/jira-surface-details-d095/r1/metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `A/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `docs/api/contracts/surfaces.openapi.json` | `9d8ef7ff68e187cebb051e6ee85a9ad333f0af903537a5e181425694c48d9758` |
| `docs/api/contracts/surface-error-provenance.md` | `4c9dc8882222f9ec0e64a18d05090561d1053ce17498de4f38ab37fb92c90e0a` |
| `openspec/specs/surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| `F/model/to-create-surface-request.ts` | `102b6382781f52b006d69d020849c818759d87a034d1a02c057efc1f214df564` |
| `F/model/use-surface-registration-attempt.ts` | `dd19442e241138f477f61493cbc14ed240b6f39fc87f14d57cf02c619eea209d` |
| `F/model/registration-rejection.ts` | `b9e83a04dabfff6a18af280edc392e0201a5640cae2a26035a4d819a8075714d` |
| `app/entities/surface/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `F/model/tests/surface-registration.test.ts` | `3186703cc7c35ee464516fc8883c20576efe4361b45a1aeaa84c565505250f31` |
| `F/ui/steps/responsible-user-field.test.tsx` | `38c0b6150833faa2f33b04f815b2f63845c144e3a13450af3b1fe7116ccbbb41` |
| `W` | `c50563fcaf2ce4ea6844a38c8805675922c3169a1ecc2ebdfc0d655ea4976c53` |
| `C/tasks.md` | `6002750f35319a52ce0c9fcd50731385ada811844c6edc3499943d87051dd478` |

## Limitations and handoff

- Mandatory local packet was available and its content hash matched the work item. No source/infrastructure blocker occurred.
- Historical MR/comment/status evidence is not execution proof. Exact dependency completion and deployed API behavior remain unknown.
- No network, browser, business requests, tests, build, configuration changes, nested agents or git mutation performed.
- HEAD is the work-item-attributed baseline; git/index was not inspected and no clean-index attestation is made.
- Prior reports and archived checkboxes were read as history, not accepted anew as execution evidence.
- Parent alone decides analytical coverage, acceptance and queue integration. No coverage count, publication, product policy or issue closure changed.