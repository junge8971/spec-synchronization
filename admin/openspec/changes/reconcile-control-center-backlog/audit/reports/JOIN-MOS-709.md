# JOIN-MOS-709 — registration shell and historical failure reconciliation

## Result and scope

**Bounded static join established; MOS-709 completion is not established.** The current application contains a four-step registration wizard, explicit final submission, step validation and draft-preserving navigation. The fresh issue packet records an unsuccessful historical test and five separately owned defects. Neither present shell code nor accepted analysis of those children establishes full parent acceptance.

Only MOS-709 was assessed. No publication, policy selection, coverage mutation or closure is proposed as an automatic outcome.

Notation:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `F` = `app/features/surface-registration`
- `T` = `app/widgets/surface-registration/ui/tests/surface-registration.test.tsx`

## 1. Exact source and provenance

Primary source: `A/sources/jira-surface-details-d095/r1/content.json#/items/2`.

| Pointer | Evidence and interpretation |
|---|---|
| `/items/2/key` | `MOS-709` |
| `/items/2/description` | “Реализовать многостраничную форму добавления поверхности, согласно примеру”. This establishes the multi-step form obligation; the referenced image is not available for visual comparison. |
| `/items/2/status` | `Require improvement`, not CLOSED or current delivery acceptance. |
| `/items/2/updated` | `2026-10-16T19:22:15.622+0800` |
| `/items/2/retrievedAt` | `2026-10-20T16:56:26.290Z`; packet cutoff is separately `2026-10-20T16:56:26.589Z`. |
| `/items/2/attachments/0` | `818857`, `image-2026-09-07-17-27-52-150.png`, image/png, 55229 bytes. Metadata only. |
| `/items/2/comments/items/0` | Comment `1106721`: estimate “5-6”; not acceptance criteria. |
| `/items/2/comments/items/1` | Comment `1113502`: package-related MR mention; no dependency installation or merged implementation inferred. |
| `/items/2/comments/items/2` | Comment `1115295`: draft form MR mention; MR body/merge/deployment uninspected. |
| `/items/2/comments/items/3` | Comment `1123351`, updated `2026-10-02T21:27:33.896+0800`: “Протестировано неуспешно” on the historical `mobile-a-tech` contour, listing MOS-1110/1164/1165/1166/1167. This is attributed historical failure evidence, not a test executed in this audit. |

All four comments are present: `/items/2/comments/total = 4`. Collection limitations and count completeness are recorded in the adjacent `metadata.json`.

Exact module membership: `A/sources/jira-hierarchy/r1/content.json#/results/17/key = MOS-783`, `/results/17/children/2 = MOS-709`. The detail packet’s `parent:null` does not negate this saved membership.

Supporting historical scenario: `A/sources/wiki-241080065-readable/r1/content.txt:17–23` describes four steps—details, responsibles, scenarios, review—and saving a draft or sending for checking. This supports shell context, not complete current policy or screenshot parity.

## 2. Prior evidence and distinct ownership

Prior reports/reviews and parent decisions were consulted before current implementation inspection. Controlling qualifications:

- `A/decisions.md`, D-090/D-091, and `A/reviews/R-D090-EIGHT.md`, `R-D091-RECOVERY.md`: accepted child analysis is partial analytical coverage.
- `A/publication/DRAFT-SURFACE-D091.md`: unpublished text-feedback candidate, not an implemented correction.
- D-004/D-005 and `A/reviews/R-SURFACE-CONFIG.md`: configuration publication and source disagreements do not activate a configurator or authorize hidden configuration writes.
- D-093: sandbox remains deferred; ordinary transport does not establish sandbox execution.
- `A/reports/G2-JIRA-MEMBER-JOINS.md:248`: historical MOS-709 row is U and explicitly warns against substituting generic capability evidence for its five nested bugs.

| Exact member | Ownership retained; not re-audited here |
|---|---|
| MOS-1110 | Type dropdown geometry; accepted analysis leaves visual criterion unresolved. |
| MOS-1164 | Historical domain-derived identifier truncation; contemporary target unresolved. No regenerated channel ID or 200-character cap. |
| MOS-1165 | Owner-team dropdown geometry; not responsible-user selection. |
| MOS-1166 | Visual restriction of current descriptive catalog text, under `surface-skill-selection`; no `purpose = detail.description` inference. |
| MOS-1167 | First-step reflection of domain input, under `surface-registration`; not confirmed addresses, occupancy or server channel generation. |
| MOS-911 | Catalog, parameter and selection semantics. Here only its composition into the wizard is identified. |
| MOS-958 | Registration transport/field migration and dependency boundary. Here only the shell’s transport handoff is identified. |

MOS-709 remains the **parent multi-step shell and historical failure aggregation** seam. No child coverage is reassigned to it.

## 3. Expected / observed / unknown

| Obligation or boundary | Observed current evidence | Unknown / limitation |
|---|---|---|
| Multi-step addition form | `app/routes/surface-registration.tsx:1–5` → `app/pages/surface-registration/ui/surface-registration-page.tsx:1–5` → `app/widgets/surface-registration/ui/surface-registration.tsx:15–76` → `F/ui/surface-registration-form.tsx`. This is an actual composition chain, not filename similarity. | Historical example-image equivalence. |
| Four-step shell | `F/model/constants/surface-registration.constants.ts:25–53` defines Details, Responsibles, Scenarios, Review with labels and per-step field sets. `F/ui/surface-registration-step-content.tsx:9–45` renders each corresponding step. | Source does not require separate URL routes for every step. Current implementation uses one route with indexed steps. |
| Visible progression | `F/ui/surface-registration-progress.tsx:15–46`: ordered list, completed/active/upcoming states, `aria-current="step"` and decorative completion icon. | DOM/classes do not establish actual rendered geometry. |
| Validated navigation | `F/model/handlers/surface-registration-handlers.ts:17–30`: next validates current fields; locked attempts cannot navigate; back returns to preceding step or registry. `F/ui/surface-registration-actions.tsx` disables next when not ready. | Not executed in this audit. No independent claim of every validation edge. |
| Explicit final action | Same handlers `:32–40`: submission requires Review and a submitter carrying `data-registration-submit="true"`. Actions use ordinary `type="button"` for navigation and a marked final submit button. | Browser-specific event behavior untested here. |
| Draft continuity | `F/model/use-surface-registration.ts:34–60` keeps a single React Hook Form instance and watched draft across step changes; widget retains skill-selection controller. | No persistence across reload or duplicate prevention across tabs; the form explicitly discloses these limitations at `F/ui/surface-registration-form.tsx:40–43`. |
| Leaving safely | `use-surface-registration.ts:51–55` establishes unsaved-change blocking and before-unload handling; form mounts the leave dialog. | Not a guarantee against all browser/tab failure modes. |
| Submission/readback boundary | `F/model/use-surface-registration-attempt.ts`, `submit`, `createPreparedSurface`, `readCreatedSurface`: lock, prepare, POST, retain returned ID, then GET; failed read retries reading rather than creating again. | Backend persistence, real error-envelope fidelity and deployment are unverified; this is not a full MOS-958 audit. |
| Historical failure | Fresh comment `1123351` names exactly the five known children. | No newer success comment in the complete returned comments; absence of such a comment is not proof that no later external testing occurred elsewhere. |

The Scenarios step explicitly says greeting configuration is unavailable and server defaults apply (`surface-registration-step-content.tsx:25–32`). This is not a newly inferred MOS-709 defect: current registration specification and archived contract migration permit omission where no editor exists.

## 4. Spec, archive, API and test locators

### Specification ownership

`openspec/specs/surface-registration/spec.md` owns:

- **Responsible assignments use business user identifiers**
- **Creation supports an atomic optional configuration**
- **Rejections are distinct from unknown creation outcomes**
- **Empty production catalog explains registration blocking and recovery**

These constrain the current wizard but do **not explicitly codify the complete four-step shell/order/progress behavior**.

Relevant archived migration:

`openspec/changes/archive/2026-10-15-update-control-center-api-contracts/`

- `proposal.md`, What Changes: optional configuration; standalone configurator and single-page redesign excluded.
- `design.md`, §2–3: business-user references, optional configuration, retained creation-attempt state machine.
- `tasks.md:8–20`: registration migration tasks and the historically unchecked real-error classification task 3.2.

Archive checkbox states are historical records, not this audit’s execution evidence. No rewrite or reopening is proposed.

### API boundary

`docs/api/contracts/surfaces.openapi.json`:

- `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces/post`
- `/components/schemas/CreateSurfaceRequest`
- `/components/schemas/CreateSurfaceRequest/properties/configuration`
- `/components/schemas/CreateSurfaceRequest/properties/submit_for_check`

The request has registration fields and optional nullable configuration; `submit_for_check` defaults to false. These DTOs do not prescribe wizard layout.

`app/entities/surface/api/surface-registry-client.ts:205–212`, `createSurface`, sends POST to `/surfaces/v1/surfaces`, expects 201 and validates returned `id`.

No new endpoint is needed for the shell. No domain occupancy, employee identity, sandbox or configuration policy was selected.

### Tests inspected, not run

| Locator | Actual assertion scope |
|---|---|
| `T:123–157` | Clean/dirty before-unload and internal-navigation confirmation, including cancel then leave. |
| `T:190–212` | Initial active/upcoming states and progression to completed/active after moving forward. |
| `T:214–240` | Review navigation and back preserve parameter value; unmarked form submission leaves the user in the wizard. This test does not itself explicitly assert zero POST calls. |
| `T:242–263` | Unmarked submission before Review leaves Scenarios visible and route unchanged. |
| `T:265–288` | Empty skill selection and empty normalized domain list block next. |
| `app/entities/surface/api/surface-registry-client.test.ts:242–289` | Configuration variants use one POST, correct path/body and no idempotency header. This is client-test source, not backend proof. |

No tests were added, modified or executed.

## 5. Bounded publication candidates

All items below are **queue-only recommendations for parent review**, not publication authorization.

1. **Keep:** existing four-step implementation, validated forward navigation, explicit final submit, draft continuity and safe creation/readback boundaries. No shell implementation defect requiring a new corrective feature was established.
2. **Update evidence only:** attach this exact-body/comment join to MOS-709’s audit evidence. Preserve the historical unsuccessful test, status, child ownership and original ledgers. Parent alone determines any analytical population transition.
3. **Question:** if shell-level normative traceability is desired, should `surface-registration` explicitly document the existing four-step order, backward draft preservation and explicit final submission? This is a bounded documentation candidate, not justification for a new redesign or compulsory corrective change.
4. **Keep existing candidate owners:** MOS-1166/1167 remain solely in unpublished `DRAFT-SURFACE-D091`; MOS-1110/1164/1165 remain question-gated. Do not duplicate them under MOS-709.
5. **Historical parity question:** validating “according to example” requires locally supplied image `818857` or an agreed contemporary visual criterion. This audit authorizes neither attachment retrieval nor browser testing.

## 6. Recomputed input fingerprints

SHA-256 values were computed from local bytes.

| Input | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| Adjacent `metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `A/sources/jira-hierarchy/r1/content.json` | `4d1881959ecbe13e4c2d4c27903b63a4ba71e1cba38e349dc33855a7e605fb77` |
| `A/work-items/WAVE-D095-SURFACE-TEN.md` | `046950ae1d91be8202c0e645057b66a58f19243a929f1af676df779441a04af0` |
| `A/decisions.md` | `7f2e819f00420b8de338453c8844b9138958ca44e2046740db25b004cff46e3e` |
| `A/reviews/R-D090-EIGHT.md` | `2df7b2655f9fb3ffac901f2b8a946e336579e0ab72a50be49a0223a6d8342a6f` |
| `A/reviews/R-D091-RECOVERY.md` | `f6fb801733ee223979debb0277de15e8f97448a3a69db6a2fb0f42f35c03e45d` |
| `A/publication/DRAFT-SURFACE-D091.md` | `de98a82303e6a4ff8b673583b6c2a18a36864d90a1d91b478bfa19fd1d7da77f` |
| `openspec/specs/surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| `F/model/constants/surface-registration.constants.ts` | `9c130aea6ebf5646f219b03a80ef6ec5f06c18f27c15d0f80fbb4cceb5f6924f` |
| `F/model/handlers/surface-registration-handlers.ts` | `d794c8792ab8d20ce957eaa9a305b4a97785743b726fc7709c0fe5217c45f1ac` |
| `F/model/use-surface-registration.ts` | `4a5ee2fcb09f6cbcdbc063653d1dbaad10956a8a54fa7944a61865857adaa8c4` |
| `F/ui/surface-registration-form.tsx` | `59d2afa4fd1c14e4d6441f883818a52514e5e2551ff0852a79e9e389bfa922a4` |
| `T` | `c50563fcaf2ce4ea6844a38c8805675922c3169a1ecc2ebdfc0d655ea4976c53` |
| `docs/api/contracts/surfaces.openapi.json` | `9d8ef7ff68e187cebb051e6ee85a9ad333f0af903537a5e181425694c48d9758` |
| `app/entities/surface/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `app/entities/surface/api/surface-registry-client.test.ts` | `4d5f93269521aedb76ce4dd722390c92dfa06e86b63af622f952146ef105c886` |

## 7. Limitations and procedural notes

- No mandatory source was missing. The known unavailable image prevents historical visual acceptance, not this bounded textual join.
- Historical contour, MR state, runtime tests, backend persistence and deployment were not inspected.
- Packet freshness does not clear other pending-publication freshness gates.
- A guessed client filename returned ENOENT; discovery identified the existing `surface-registry-client.ts`. A hierarchy extraction initially assumed object children, failed, then was corrected to the actual string-array structure. Neither involved a missing mandatory source or alternate runtime/model.
- Initial bulk prior-report reading used a read-only Python command and produced truncated output; decisive reviews were subsequently read with the read tool. No completeness claim is made for that truncated output.
- No intentional files were written; this Markdown is returned for runtime persistence at the assigned output path. No Git commands or index-state inspection were performed.