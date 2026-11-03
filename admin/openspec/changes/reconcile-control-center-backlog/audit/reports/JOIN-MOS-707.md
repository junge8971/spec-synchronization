# JOIN-MOS-707 — historical surface-page presentation

## Result and scope

**Bounded partial join; parent acceptance required.** Current registry code contains the page header, documentation link, creation entry, table fields, sortable headers and horizontal-overflow container described in MOS-707. This does **not** establish historical screenshot parity, responsive geometry, deployed behavior or successful execution of tests.

A material documentation gap was found: **`openspec/specs/surface-registry/spec.md` is absent.** Parent independently confirmed the absence and authorized continued bounded inspection, treating the archived registry delta as historical evidence only—not substitute current authority. No spec restoration, synchronization or policy decision is proposed automatically.

Only MOS-707 is assessed. MOS-708 owns search/filter/pagination/URL semantics; MOS-910 owns current server integration and registry refinements. Registration, selection, connection and lifecycle members retain their separate ownership.

Paths below are repository-relative:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `W` = `app/widgets/surfaces-registry/ui`
- `H` = `openspec/changes/archive/2026-09-28-surface-registry`

## Source and prior evidence

### Exact fresh source

`A/sources/jira-surface-details-d095/r1/content.json#/items/0`:

- Key: **MOS-707**, `[FE][Поверхности] Создание страницы`.
- `/description`: lay out the surfaces page similarly to the attached example.
- `/status`: `CLOSED`; `/updated`: `2026-09-24T17:18:32.529+0800`.
- Item retrieval: `2026-10-20T16:56:26.201Z`; packet cutoff: `2026-10-20T16:56:26.589Z`.
- `/comments/total = 3`; three comments returned.
- `/comments/items/0`, ID **1106722**: estimate only.
- `/comments/items/1`, ID **1112680**: claims header, documentation, connection button, registry columns, temporary mocks and sortable columns; describes narrow-window reflow and mobile horizontal scrolling checks.
- `/comments/items/2`, ID **1115954**: claims successful layout/table/sorting/mobile testing at `https://mobile-a-tech.mos.ru/tsam-panel`. This is attributed historical testimony, not execution evidence from this audit.

Attachment metadata:

| Pointer | Attachment |
|---|---|
| `/items/0/attachments/0` | **818849**, `image-2026-09-07-17-22-47-896.png`, PNG, 80,697 bytes; source URL `https://task.mos-team.ru/secure/attachment/818849/image-2026-09-07-17-22-47-896.png` |
| `/items/0/attachments/1` | **827197**, `image-2026-09-24-12-14-22-259.png`, PNG, 122,827 bytes; source URL `https://task.mos-team.ru/secure/attachment/827197/image-2026-09-24-12-14-22-259.png` |

Neither attachment body was collected. Exact visual equivalence cannot be inspected.

Historical membership map: `A/reports/JIRA-MOS-783.md`, MOS-707 row, points to `jira-member-index/r1/content.json#/items/116` and `jira-hierarchy/r1/content.json#/results/17/children`. The old report's missing-description/comments limitation is superseded **for this exact member and these fields only** by the fresh packet. Membership was not independently recomputed here.

### Prior work preserved

Read prior inventory, recovered configurator report, D090/D091/D093 decision excerpts, surface draft and D093 review before implementation inspection:

- `A/reports/SCENARIO-SURFACE-CONFIG-r2.md`: published configuration details do not activate deferred functionality.
- `A/publication/DRAFT-SURFACE-D091.md`: registration text/domain-feedback candidates remain separate and unpublished.
- `A/reviews/R-D093-EIGHT.md`: static assertions do not establish geometry, deployment or sandbox delivery.
- `A/decisions.md`: parent retains acceptance and publication ownership.

These were used as scope maps, not repeated as fresh neighboring audits. No MOS-1110/1164–1167, sandbox or lifecycle coverage is claimed.

## Expected / observed / unknown

| MOS-707 expectation | Observed local implementation and test locator | Remaining uncertainty |
|---|---|---|
| Surfaces page with header | `app/pages/surfaces/ui/surfaces-page.tsx`, `SurfacesPage`, renders `SurfacesRegistry`. `W/surfaces-registry.tsx`, header JSX, renders “Подключение” and H1 “Поверхности”. | No actual route/deployment execution. |
| Documentation and connection entry | Same header links to `/docs?article=surface-register` and `/surfaces/new`. Creation uses `PermissionButton` with `surfaceView` and `surfaceCreate`. | Historical unconditional wording does not override current permission control. No auth-policy audit or policy replacement is made. |
| Name/domains, type, owner, status, dialog count, updated date | `W/surfaces-registry-table.tsx`, `SurfacesRegistryTable`, renders all six semantic columns, plus an open indicator. Name links to detail; domains are joined; owner and channel ID displayed; date formatted with `Intl.DateTimeFormat('ru-RU')`. | Historical screenshot styling, exact sizes, typography and row content unavailable. |
| Sortable columns | Table instantiates sortable headers for `name`, `type`, `owner`, `dialogs`, `updated_at`; status is a plain header. `W/surfaces-registry-sortable-header.tsx` supplies button labels and active `aria-sort`. | Source does not require every column to sort. No unsupported status-sort defect inferred. Server sort correctness belongs to MOS-910. |
| Reflow above table at smaller widths | Registry header uses `flex flex-wrap … gap-4`; action group uses `max-sm:flex-row-reverse`; filters/count wrapper changes from column to row at `sm`. | CSS intent is not measured reflow. Narrow-screen overlap, clipping and visual fidelity remain unknown. |
| Horizontal table scrolling on mobile | Table wrapper uses `overflow-x-auto`; table uses `w-full min-w-[1000px] table-fixed`. | Presence of classes is not proof of working scroll geometry or absence of outer-page overflow. |
| Temporary mock data in historical implementation | Current widget obtains data through `useSurfacesRegistryQuery`, not an inline historical mock list. | Mock-era comment is historical, not a requirement to restore client-local data. Production and mock runtime behavior were not exercised. |
| Successful historical test comment | Exact comment and contour URL are preserved above. | Cannot verify deployed revision, credentials, data, browser dimensions, test procedure or result. `CLOSED` is not closure evidence for current code. |

### Test evidence, read only

`W/surfaces-registry.test.tsx`:

- **`shows contract fields and distinguishes a real zero from null`** asserts heading, documentation/creation hrefs, table existence, row count, zero/dash values and date-sort control.
- **`uses API sort strings when selecting a sortable column`** asserts name header changes from ascending to descending and URL `sort=-name`.
- **`opens a surface from its name link or from the free row area`** and **`keeps the surface name as a keyboard-accessible native link`** cover modern navigation behavior.

These use seeded fixtures and stubbed `fetch` responses. The sort assertion checks control state/URL; it is not a fresh demonstration of real backend row ordering. The inspected test file has no responsive-geometry or historical screenshot assertion. Tests were **not run**.

## Spec and API ownership

### Missing current main owner

Reading `openspec/specs/surface-registry/spec.md` returned `ENOENT`. Discovery under `openspec/specs` found surface lifecycle, overview/connection, registration and skill-selection directories, but no registry directory. Searching current main specs for `реестр поверхностей|Surface registry|surface-registry` returned no matches.

Parent confirmed this finding and explicitly permitted continued partial reporting. Implications for specification completeness remain unresolved; no current registry-main conformance verdict is possible.

### Historical owner, not current substitute

Read `H/proposal.md`, `design.md`, `tasks.md` and `specs/surface-registry/spec.md`.

- Proposal **Why/Non-goals** explicitly identifies MOS-910 as completing the registry after MOS-707/708 and avoids rewriting those foundations.
- Archived delta **Prototype labels and API values** names the six current columns and server-supplied fields.
- **Nullable statistics** and **Surface detail navigation** own later refinements; they are not credited as separate MOS-707 completion.
- **Persistent query state** identifies sortable fields, consistent with the current header structure.
- Historical role assumptions and archived checked tasks are not current policy or test evidence.

API locator: `app/entities/surface/api/surface-registry-client.ts:21–46`, `paginationSchema` and `surfaceSchema`, contains the typed/validated presentation fields: name, domains, owner, type, status, statistics and timestamps. The historical delta identifies GET `/api/control/api/surfaces/v1/surfaces`. Full endpoint/envelope/filters/pagination reconciliation is deliberately left to **JOIN-MOS-910**; no backend contract or deployment verification is claimed here.

## Bounded publication candidates

All candidates are **queue-only**, subject to parent acceptance and applicable freshness/review gates.

1. **KEEP — historical MOS-707 presentation join.** Record current page/table locators and exact comment attribution without duplicating server-integration work.
2. **UPDATE — evidence availability.** Replace the old MOS-707 “description/comments unavailable” limitation with the fresh exact packet. Retain missing attachment bodies and uncollected custom fields.
3. **QUESTION — absent current registry main spec.** Parent may queue investigation of intended spec ownership. Do not silently copy the archive, synchronize main specs or restore historical permission assumptions.
4. **Optional verification candidate only.** If separately authorized, strengthen component assertions for exact displayed fields and sorting controls. Geometry and screenshot parity remain separate evidence needs; this report does not authorize browser/E2E work.
5. **No new implementation change established.** The inspected presentation seam contains no confirmed corrective defect against the available prose. Unknown visual parity is not evidence of either compliance or failure.

Any coverage change is parent-owned and limited to **MOS-707 analytical partial coverage**, never delivery acceptance or checkbox closure.

## Input fingerprints

SHA-256 values were freshly calculated with read-only `sha256sum`.

| Input | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| Adjacent `metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `W/surfaces-registry.tsx` | `56f3348b48ee5e0cbaf85c6533389649935f4775642826d2abb065f4cf56b779` |
| `W/surfaces-registry-table.tsx` | `00e15f25c4a3d6c52f050ddac427bdf88ac1c3f7843cc76a316d03e872150824` |
| `W/surfaces-registry-sortable-header.tsx` | `afebb1a99104d3c51c2b7ff6f82bef068639d0615f4e6fda7582e27a1b2f582a` |
| `W/surfaces-registry.test.tsx` | `dc780c80f7f731076e667d57174313d1d1242222c655e8a36d4c3ba52865015e` |
| `app/entities/surface/api/surface-registry-client.ts` | `de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05` |
| `H/proposal.md` | `9785022b4382ac10469754fc49799021684e5ff7956b23fe6a543540dd10a8de` |
| `H/design.md` | `2968bf34ebd61cc2d861b129e080512843f0718b08ba796ab3049dc714644681` |
| `H/tasks.md` | `a1ad5429920f771dc04d8a8ff218fed59f9ff7dbda244a242f22aa3a3a69d6b2` |
| `H/specs/surface-registry/spec.md` | `7895c5b5e6e66f066138b541eb16b3a1dde760c591f92e3c82f2d919dd1bccdf` |
| `A/decisions.md` | `7f2e819f00420b8de338453c8844b9138958ca44e2046740db25b004cff46e3e` |
| `A/reports/SCENARIO-SURFACE-CONFIG-r2.md` | `0f197edbb0c24ca779a05b00fe091fa909d174b5db7dd926a9aa948c217d7910` |
| `A/reports/JIRA-MOS-783.md` | `4088bb978c718cee5104e570f42ab0b99191a4035f5f9752a80e098153b56354` |
| `A/publication/DRAFT-SURFACE-D091.md` | `de98a82303e6a4ff8b673583b6c2a18a36864d90a1d91b478bfa19fd1d7da77f` |
| `A/reviews/R-D093-EIGHT.md` | `aee6c464b24662ed9e5396e382ca2e35a3add12ffe47a6c452178f847084e2bc` |

The packet hash matches its metadata and assignment. Hashes establish local byte identity, not remote authenticity or deployment freshness.

## Execution limitations

No files were written with tools. No network, browser, business API, tests, build, lint, typecheck, configuration change, git mutation or nested agent was used. HEAD/index state was not independently verified. This complete report is returned for runtime persistence at the assigned output path.