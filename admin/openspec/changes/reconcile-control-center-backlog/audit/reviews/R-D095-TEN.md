# R-D095-TEN — independent read-only review

## Verdict

**Nine ACCEPT; JOIN-MOS-913 REVISE by additive correction. No escalation.**

Acceptance is limited to bounded analytical evidence. It does not establish delivery, passing tests, backend enforcement, deployment or publication approval. Parent retains acceptance, registers and queue ownership.

`A` = `openspec/changes/reconcile-control-center-backlog/audit`.

## Per-report decisions

| Report | Verdict | Independently checked basis and candidate disposition |
|---|---|---|
| JOIN-MOS-707 | **ACCEPT** | Exact `/items/0` distinguishes layout intent, historical mock implementation and historical test testimony. Current registry header, links, permission-controlled creation and table composition support the bounded join. Component assertions establish DOM/navigation expectations, not responsive geometry. **Keep evidence update; no demonstrated corrective implementation.** Missing images and current registry main spec remain limitations. |
| JOIN-MOS-708 | **ACCEPT** | `/items/1/comments/items/1` explicitly specifies two-character search and automatic upper-page correction. Current parser forwards any nonempty query; registry leaves an out-of-range request unchanged until explicit recovery. Existing component test asserts that behavior. **Keep historical/current distinction; threshold remains an owner question, not an automatic regression fix.** |
| JOIN-MOS-709 | **ACCEPT** | `/items/2` preserves unsuccessful historical testing and five separately owned defects. Current navigation handler validates forward movement and requires a marked final submitter on Review. Inspected wizard assertions cover progression, retained parameters and unmarked submission. **Keep shell evidence; no child-to-parent completion inference or redesign.** |
| API-MOS-712 | **ACCEPT** | `/items/3` supplies seven work obligations and five DoD bullets. Current client exposes the eleven surface operations but no history transport. Saved audit query explicitly uses cursor pagination without totals. **Keep obligation matrix; consolidate history pagination and error-provenance questions as below.** The r1 API attribution is valid. |
| JOIN-MOS-901 | **ACCEPT** | `/items/4` requires backend storage, ACL, transitions and tests. Actual mocks use process state, previous-status restoration and permissive transitions; they do not prove durable history or backend enforcement. **Keep backend-evidence handoff; no duplicate frontend work.** TEST_PLAN824049 remains metadata-only. |
| JOIN-MOS-910 | **ACCEPT** | Actual client reads `items`, maps server total and sends query/status/type/sort/limit/offset. Registry renders returned order. List schema deliberately accepts nullable whole `stats`; detail schema does not. **Keep current transport; preserve historical `surfaces` discrepancy and nullability question.** r1 descriptions are genuinely present. |
| JOIN-MOS-911 | **ACCEPT** | Current hook requests the prod catalog, retains draft parameters and re-fetches catalog/details before preparation. Inspected model assertions distinguish non-prod, not-found, read-error and catalog mismatch, rejecting writes on failed preparation. **Keep existing owner; contradictory successful pagination remains optional evidence strengthening, not an established backend defect.** |
| JOIN-MOS-913 | **REVISE** | Server-owned connection/checklist findings remain useful. Equal-count membership divergence is supported. However, the report overlooks an existing empty/whitespace-code regression immediately preceding its cited help test. Apply correction C1 and retain the bounded help-authority conclusion below. **No broad re-analysis required.** |
| JOIN-MOS-914 | **ACCEPT** | Both F1 and F2 survive independent tracing through the mounted coordinator and feedback controls. **Keep two narrow corrective candidates under existing lifecycle ownership**, with the static-only qualifications below. No sandbox/configurator activation. |
| JOIN-MOS-958 | **ACCEPT** | Exact source remains Hold with MOS-1336 dependency. Current request/response boundary uses business-user identifiers and server-confirmed channel data. Rejection adapter accepts only structured HTTP422 validation details. **Keep safe no-replay behavior; consolidate error integration and retain product-context/dependency questions.** r1 prose attribution is valid. |

## API provenance: the suspected revision mismatch is not present

Independent JSON comparison found **all eleven surface-operation descriptions identical between saved r1 and r2**.

| Exact saved path | Capture timestamp | SHA-256 |
|---|---|---|
| `A/sources/api-live/r1/content.json` | `2026-10-16T11:13:29.451Z` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `A/sources/api-live/r2/content.json` | `2026-10-19T08:11:44.238Z` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |

Both digests match adjacent metadata.

Therefore:

- Reports **712/910/913/958 correctly cite r1** for the inspected operation-description prose.
- Reports **901/914 correctly cite r2**.
- Do **not** “repair” the first four citations to r2 or claim these descriptions first appeared on October 19.
- “Later publication” means later than the October 15 local/raw snapshot, not necessarily r2.
- Whole-document hashes differ; equality of these eleven descriptions does **not** imply complete schema/security equality.

This also agrees with the earlier controlling `R-SURFACE-CONFIG.md`, which already attributes these descriptions to October 16 r1.

For exact pointers, use prefix:

`/paths/~1api~1control~1api~1surfaces~1v1~1surfaces`

and the appropriate operation `/description`, including POST creation, GET list/detail, configuration/enabled-skills PUT and six lifecycle POSTs.

## Mandatory additive corrections and integration guards

### C1 — MOS-913 test-evidence correction

Preserve the original report and append an explicit correction:

`app/widgets/surface-details/ui/surface-details.test.tsx:710–718` already contains:

```text
it.each([null, '', '   '])('disables copying for %j code', ...)
```

It asserts disabled copying and visible absence feedback.

Consequently, remove **empty/whitespace copy-button coverage** from the proposed missing-regression list when consuming the report. These tests were inspected, not executed. Reverse metric combinations, integer validation and equal-count checklist divergence remain separate questions.

The report’s opening “one concrete discrepancy” also understates its later count-only finding. Summarize the two distinct seams without conflating them: help navigation and draft-membership explanation.

**This review supplies the precise correction; parent may accept an additive overlay without rewriting the original.**

### C2 — help toast versus `/docs`: retain bounded authority findings

Current main requirement:

`openspec/specs/surface-overview-connection/spec.md:47–54`

requires `/docs` under the deployment basename.

Current component test `surface-details.test.tsx:720–740` instead requires a placeholder toast and unchanged route.

I searched archived Markdown, including ignored-file discovery, for embedding-help/instruction/toast references and inspected the later lifecycle MVP design. The October 12 design changes lifecycle/checklist permissions and removes sandbox; it does **not** supersede embedding-help navigation. The inspected October 16 contour design likewise supplies no replacement instruction behavior. Earlier lifecycle toast provisions concern copy/lifecycle feedback, not permission to replace documentation navigation.

**No later superseding approval was found in the inspected repository evidence.** Thus retain a narrow `/docs` reconciliation candidate, not a claim that no approval could exist elsewhere. A contrary test demonstrates implementation expectation, not product authorization.

No main-spec or archive synchronization is authorized.

### C3 — equal count does not establish equal membership

Actual mounted checklist receives only `selectedSkillCount` and uses:

```text
selectedSkillCount !== surface.enabled_skills.length
```

Saved `[A]` versus draft `[B]` therefore suppresses the explanation despite changed membership. The current main checklist requirement expressly requires explanation when draft and saved composition differ.

Retain this as a narrow static UI gap. Do not alter saved checklist facts, selection policy, publication eligibility or parameter defaults. No runtime reproduction was performed.

### C4 — consolidate overlapping findings

Maintain **one existing error-provenance/integration handoff** for 712-03, MOS901-E03 and MOS958-U1/Q1:

- October 15 local documentation has an explicit historical cutoff.
- October 16 r1 already supplies creation/domain/user/configuration error prose.
- Current registration adapter remains HTTP422 `detail[]`-only.
- Documentary progress does not supply an executed sanitized rejection, prove noncreation, authorize generic409/422 classification or clear task3.2.

Maintain **one history-pagination question** under contract preparation, with backend evidence linked from MOS-901:

- MOS-712 literally requests size, offset and total.
- `wiki-241077434-readable/r1/content.txt:252–334` explicitly provides limit/cursor, next_cursor/has_more, keyset rather than offset, and no total.
- No invented history endpoint, synthetic total, routing/auth policy or automatic requirement amendment follows.

## MOS-914: mounted-path verification

### F1 — command and detail confirmations

Verified chain:

`SurfaceDetails` → `SurfaceDetailsContent` → `useSurfaceDetailsOperations` → `publishSurface`

Both header `SurfaceDetailsQuickActions` and connection checklist receive the coordinator’s `onPublish`.

`useSurfaceMutationController.runAndRefresh` returns command `response` independently of refreshed `detail`. The coordinator checks refresh failure and `detail.status === 'prod'`, but not `response.status`. `SurfaceDetailsPublishAction.executePublish` treats resolved mounted `onPublish` as completion and opens success.

Thus a schema-valid **non-prod command response followed by prod detail** can statically reach success. The fallback branch has the same omission, but the finding does not depend on that fallback being mounted.

This conflicts with the main lifecycle requirement and October12 design §3 requiring both confirmations.

Existing success test at `surface-details.test.tsx:472–511` supplies prod for both responses; it does not cover the mismatch.

**Disposition:** retain F1 as a bounded corrective/regression candidate. No observed backend occurrence is claimed.

### F2 — write-oriented retry after confirmed-write refresh failure

Verified chain:

1. Coordinator confirms skills PUT and resets its server baseline.
2. Failed following GET throws a “repeat reading” operation error.
3. Publish component routes non409 errors to `retryPublish`, labelled **«Повторить»**.
4. `retryPublish` invokes mounted publication again.
5. If cached status/selection remain eligible, preparation and another PUT can occur.

After successful publish POST and failed final GET, cached prod can instead block that retry at eligibility. This is **not proof of a repeated POST**, but the retained control is still not GET-only recovery.

`SurfaceDetailsQuickActions` remains mounted when its trigger is hidden and separately exposes `mutation.retryRefresh`. The generic read-error panel also provides GET retry. Their existence does not remove the write-oriented feedback alternative.

The final-refresh test at `:553–596` clicks **«Повторить чтение»**; it does not exercise **«Повторить»** or prove that alternative absent.

**Disposition:** retain phase-aware recovery candidate; preserve full preparation for genuinely rejected publication. Counterexamples are static only.

## Hash verification

All **156 input-hash table entries** were independently verified against their **resolved exact paths**, including aliases and adjacent-directory references. No mismatch or unresolved path remained. A preliminary digest-presence scan was followed by exact-path verification; digest presence alone was not treated as sufficient.

Reviewed report fingerprints:

| Path under `A/reports/` | SHA-256 |
|---|---|
| `JOIN-MOS-707.md` | `58a58eacb369a4b3861756fa99bad849a56eff6c3df5732e07654d1b15c53855` |
| `JOIN-MOS-708.md` | `9dce0c6d99267d6eb5e3a4e6c72c4fbb6ff097a4500065f2e6ff44d603b34ae5` |
| `JOIN-MOS-709.md` | `34ad57f6f1ec628efc5bc246e101e46ce2055b957d25b9dc70b4711a6bd33c34` |
| `API-MOS-712.md` | `5afb79611e85f3ff51fca4cfabaf1596e253cab1b76ec0a1e5e1b262ada8fabf` |
| `JOIN-MOS-901.md` | `d35e786a94a2e051d6613b1634235e7d5a228f129099204fe64d30909b26c5e3` |
| `JOIN-MOS-910.md` | `e592172aea918051fed84be4c07cb671810ee8ea5d6a2f3514715e7c6c78c176` |
| `JOIN-MOS-911.md` | `bde8b93fe2245b7d60837035fc635db859e59cd2316fd60b54bdedfe9f69ee52` |
| `JOIN-MOS-913.md` | `aca62e683447f9a561e6390923022c9d5bd36978b4dcbb318a9133c972c3dd88` |
| `JOIN-MOS-914.md` | `46446f254f4eac7d5596ebeeca9b8c5e62dc064757fc84de6c21afcb61ed9d7f` |
| `JOIN-MOS-958.md` | `41db6d50ea3d22f2aff1aae14a895df3731e48a47e9a0307039914c91fbbdddf` |

Additional mounted-path evidence:

`app/widgets/surface-details/ui/surface-details/surface-details-quick-actions.tsx`  
SHA-256: `37cecc524545764fd4e39e3af95f525dd260183b0b723b86412a17d3bbfac343`.

## Exact coverage eligibility

Independently verified:

- Hierarchy `sources/jira-hierarchy/r1/content.json#/results/17` identifies MOS-783 and contains all ten exact members.
- Historical ledger `reports/G2-JIRA-MEMBER-JOINS.md:246–255` records all ten as **U**.
- Current `coverage.json` is accepted through D-094; D090–D094 do not promote these ten.
- Current baseline remains **89P/1B/83U**, total173; global11/28 unchanged.

Eligibility:

- **Nine accepted reports:** MOS707/708/709/712/901/910/911/914/958 are eligible for individual U→P after parent acceptance.
- **MOS913:** eligible only after parent accepts the additive correction and qualifications above.
- Nine promotions would produce **98P/1B/74U**.
- All ten, after correction and acceptance, would produce **99P/1B/73U**.
- **No transition is performed by this review.**

P means substantive partial analytical coverage, not passed tests or completion. Nested registration defects, sandbox members and configurator work receive no additional coverage.

Current coverage file SHA-256:  
`4f14e07033cca801961ae3083bf9529e5bf0fb8b831ca1f36232c47eed2b75da`.

## Limits and process record

- Jira packet cutoff: **2026-10-20T16:56:26.589Z**. Exact item timestamps remain distinct. Returned comment counts match totals for all ten.
- Primary Jira packet SHA-256 verified: `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a`.
- Missing current registry main spec is a confirmed limit; archived registry material is historical, not a substitute current authority.
- Missing MOS910 journal, layout images and TEST_PLAN824049 body remain unavailable evidence. No reconstruction or retrieval occurred.
- Approved sandbox/configurator exclusions, auth integration and mock boundaries remain controlling. Historical no-auth wording is not grounds to remove approved session/permission behavior.
- Historical statuses, comments and checked archive tasks do not establish deployed revision, storage, ACL, actual transitions, statistics or propagation.
- Hash verification covered every recorded input entry; semantic review used decisive source/code/spec/test sections, not exhaustive re-audit of every neighboring file.
- Prior controlling reviews/decisions were read, but some were read after initial report/source inspection. This does not satisfy a strict prior-first sequence retroactively.
- One initial API-description output exceeded display capacity. A subsequent bounded comparison verified capture dates, hashes and equality of all eleven descriptions.
- No model/mode fallback or infrastructure blocker occurred.
- No tests/build/typecheck/lint/format, network/browser/business API, children, configuration changes or Git mutations. Git/index and baseline HEAD were not independently attested.
- No files were written with tools. This Markdown is returned for runtime persistence at the authoritative output path.