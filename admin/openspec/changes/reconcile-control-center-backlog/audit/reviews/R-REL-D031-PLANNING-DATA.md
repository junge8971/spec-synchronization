# R-REL-D031-PLANNING-DATA — independent relevance review

## Scope and evidence

Reviewed both assigned reports against their work-items and all six assigned saved pages. This is a relevance/coverage review only, not requirement reconciliation, API conformance, implementation verification, policy selection, or G1 closure.

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

Independent inspection covered:

- Both reports and both analyst work-items completely.
- All six primary `sources/wiki-ID/r1/metadata.json` files.
- All six complete readable text bodies: **339 / 5 / 6 / 39 / 516 / 12 lines**, respectively.
- Complete container chunks for 241085260, 241085256 and 241085263.
- All four exact body chunks for 241092173.
- Selected exact chunks for 241082618 (1, 10) and 241076726 (1–3, 9–11, 28–30, 32, 44), corroborating headings, tables, embedded viewer/SVG payload and identifier-shaped hyperlinks.
- All six primary attachment-index tails: **0 / 0 / 0 / 8 / 2 / 0**, status 200 and `next: null`.
- `collection-D031-held-pages.json`, solely for capture status and collection boundaries.

Chunk numbers denote JSON array entries, not rendered views. Full long-page markup, graphical ERDs and attachment bytes were not inspected. Hashes and chunk roundtrips were not independently recomputed.

## Review

### Report: REL-D031-PLANNING-API — REVISE

**Correct:** All three relevance classifications are body-backed. The decomposition is substantive mixed planning; both index pages are containers rather than API contracts. Scenario routing is explicitly provisional and does not authorize OIDC, logout, role editors, backend work or UI activation.

| Page | Assessment and exact evidence | Exception |
|---|---|---|
| **241082618 — Декомпозиция**, v3 | Mixed classification supported. `content.txt:119–322` contains modules 2.1–2.10; `:49–118` supports teams, journals, platform modules and settings; `:323–339` supports demo/documentation context. Exact chunks 1 and 10 establish numbered FE/BE tables and the administrative/Control Center headings. | None. Full readable-text coverage is correctly distinguished from selective markup inspection. |
| **241085260 — Системный анализ**, v2 | Container-only supported by complete exact chunk 1: five children links, no requirement prose. Targets are **241085256, 241102892, 241092173, 241076726, 245678373**, in the reported order. | Collection-status qualification required; see finding below. |
| **241085256 — API**, v2 | Container-only supported by complete exact chunk 1 and `content.txt:1–6`. Targets are **238347066, 238352321, 241074633, 241080643, 241083649, 238350232**. Labels support candidate skill/dialog/report routing, not method/schema/error semantics. | Future collection must first consult existing inventory; see finding below. |

**Finding — P1: Lane-local unread status is not adequately separated from global capture status in follow-up instructions.**

- **Location:** `reports/REL-D031-PLANNING-API.md`, sections “241085260 — Системный анализ,” “241085256 — API,” and final residual risks.
- **Evidence:** The system-analysis section labels four linked pages “unvisited” and recommends “separate bounded collection/inspection of the four unvisited linked bodies.” However, `collection-D031-held-pages.json`, `pages` entries for **241092173, 241076726 and 245678373**, already records successful saved body capture. The first two also have substantive classifications in the companion DATA report reviewed here. The API section similarly makes future work depend on child-body “collection/inspection” without an existing-inventory prerequisite.
- **Impact:** A lane-local reading limitation can be consumed as a global evidence gap and trigger duplicate collection or inspection.
- **Minimum mandatory correction:** Define “unvisited/uninspected” throughout as **not read by this analyst**. Explicitly record the three known captured system-analysis children and route the two data pages to the companion report. Make all child follow-up conditional on checking the global saved-source inventory and existing evidence owner first; authorize new collection only for an established remaining gap and bounded approved question. Do not infer the other children are globally absent merely because this receipt does not list them.

No classification change or additional source traversal is required.

### Report: REL-D031-DATA-DRAFTS — ACCEPT

No issues found.

**Correct:** The report distinguishes substantive model/ownership tables from diagrams and navigation containers, preserves cross-system boundaries, and does not equate complete readable text with full ERD or API coverage.

| Page | Assessment and exact evidence | Exceptions |
|---|---|---|
| **241092173 — Группы данных**, v17 | Mixed, chiefly supporting ownership/context classification supported by `content.txt:1–37` and complete chunks 1–3. The tables explicitly mark identity/audit entities МПММ, incidents/dialogue entities ЕСК, and named skill/surface/report/team/module entities Центр управления. Chunks 3–4 contain two drawio macro names/configurations, not readable diagram relationships. | None. All eight attachment entries are correctly identified as unread; their indexed names/types/version parameters match the report. |
| **241076726 — Модель данных**, v20 | Mixed direct model support and cross-system context supported by complete `content.txt:1–516`. Team (`:99–109`) and Module (`:136–148`) remain relevant despite administrative placement; skill, dialogue, surface, report/export and documentation sections support the reported routing. Exact chunks 1–3, 9–11 and 28–30 corroborate two viewer blocks, embedded SVG payload, entity inventories and detailed field-table structure. | None. Text coverage is not graphical ERD interpretation. Separate `erd.png`/`erd.svg` entries are unread and not assumed equivalent to embedded payloads. |
| **241085263 — Черновые документы/заметки**, v4 | Container-only supported by complete chunk 1 and `content.txt:1–12`. All twelve IDs and labels match the report, including final target **238324852**. | None. The report explicitly limits “unvisited” to this run and requires checking existing evidence ownership before collection. The receipt confirms 238324852 is already captured, without establishing its semantic conclusions. |

Additional verified safeguards:

- Model chunks 32 and 44 contain literal `http://Permission.id` and `http://Skill.id` anchors in relationship prose. They remain inert identifiers, not collection authority.
- Attachment-index counts and unread-byte limitations are accurately reported.
- The DATA report documents removal of unsupported `noStagedFiles: true`; no empty-index verification remains asserted. Repository staging state was not inspected by this reviewer.
- Dates, section placements and system labels do not become precedence decisions, external-system audit authorization, schema changes, or feature approval.

## Required disposition

- **PLANNING-API:** Apply the single coverage/follow-up qualification above, then re-check the edited wording.
- **DATA-DRAFTS:** Accept unchanged.
- **Fixed:** None by this reviewer.
- **Merge verdict: BLOCK** on accepting the PLANNING-API report as final until its collection-status wording is corrected; the six relevance classifications themselves are supported.

## Validation limits

Only bounded local reads and targeted local searches were used. No child or attachment links were followed; no source scripts/viewers were executed or rendered. No network, application-code inspection, tests/build/browser activity, direct edits, staging inspection, nested delegation, Jira membership changes or global closure occurred. The receipt establishes captured-versus-unread distinctions, not semantic truth or global collection completeness.