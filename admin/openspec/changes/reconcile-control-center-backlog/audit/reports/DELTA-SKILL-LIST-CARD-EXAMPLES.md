# DELTA-SKILL-LIST-CARD-EXAMPLES

## Result

Two historical examples add explicit search-field, paging and questionnaire vocabulary, not approval of a current Control Center API. Five bounded evidence candidates below preserve existing catalog/card owners and unresolved gates. No accepted MOS-1018 publication revision, feature activation, implementation defect or task closure follows from these examples.

# Code Context

## Files Retrieved

Repository-relative aliases: `A = openspec/changes/reconcile-control-center-backlog/audit`; `H = openspec/changes/archive`.

1. `A/sources/wiki-238347066-readable/r1/content.txt` (1–175; **L**) and `A/sources/wiki-238352321-readable/r1/content.txt` (1–141; **C**): complete readable bodies. Their respective `body-view-chunks.json` (1–5 / 1–7, all array entries) were read completely as inert markup to verify nested parameter/response tables and example structure.
2. `A/sources/wiki-238347066/r1/metadata.json` and `A/sources/wiki-238352321/r1/metadata.json` (1–23 each), plus both readable `metadata.json` (1–14): complete provenance. Original `content.json` records inspected for top-level metadata and `$.attachments`, not executed.
3. `A/reports/REQ-MOS-1018.md` (1–62), `A/reports/DELTA-MOS-1018-LINKED-CONTRACT.md` (1–97), `A/reports/WRITE-MOS-1018.md` (1–38), `A/reviews/RECON-MOS-1018.md` (1–116), `A/reviews/R-WRITE-MOS-1018.md` (1–82), `A/reviews/R-DELTA-MOS-1018-LINKED-CONTRACT.md` (1–97): full scoped prior findings and acceptance boundary.
4. `openspec/specs/skill-catalog-experience/spec.md` (1–112), especially 37–93; `openspec/specs/skill-card-editing/spec.md` (1–49), especially 9–25: current owner requirements.
5. `H/2026-10-01-skills-prototype-alignment/design.md` (1–147 read; relevant 80–101, 134–147) and `readiness.md` (complete): explicit G1/G6 decisions and MOS-929/933 ownership; historical readiness claims not independently validated.
6. `H/2026-10-01-skills-status-and-registration-recovery/design.md` (complete; relevant 27–31): approved server status/filter and unknown-list-status qualification, rather than reverting to the earlier G1 status exclusion.
7. `H/2026-09-29-mos-944-skill-card-editing/design.md` (1–45; relevant 19–33): partial acceptance, contact and material-display constraints. Historical PATCH wording is not substituted for current spec PUT.
8. `openspec/changes/mos-1018-skill-phrase-conflicts/design.md` (1–29): retained separation of transient check, persisted save and agreed-send validation.

### Provenance

**L:** wiki 238347066, capture r1, page v8 dated `2026-09-08T17:40:36.272+08:00`, retrieved `2026-10-19T10:18:27.973Z`, title `/skills - Каталог навыков`.

**C:** wiki 238352321, capture r1, page v2 dated `2026-09-08T17:40:50.253+08:00`, retrieved `2026-10-19T10:18:28.161Z`, title `/skills/{id} - Карточка навыка, описание`.

Both original records have `$.attachments.status = 200`, `start = 0`, `limit = 100`, `size = 0`, `next = null`, `results = []`. These are empty returned indexes, not a claim about all possible attachments. Metadata attributes discovery to root wiki 238324523 r2 links 5–7; no linked documents were traversed. Parent-recorded SHA-256 and readable-body roundtrip were **not independently recomputed**. Full readable text and exact chunks were inspected, without rendering, repairing or executing examples.

## Key Code / evidence candidates

All L/C line references resolve to the exact readable paths above and versions stated above. JSON paths below denote keys inside the documentary response examples embedded in original `$.bodyView`, not executable JSON contracts. Stable IDs are local to this report, not accepted implementation tasks.

### DELTA-SKILL-LIST-CARD-EXAMPLES-01 — search/filter vocabulary; retain G1 clarification

- **Evidence:** L 6–46, `parameters` table rows `query`, `status`, `domain`, `offset`, `limit` (all optional). `query` expressly searches **name, purpose and serviceId** (L16); status and domain filter skills (L18–32). Exact markup is in chunks `$[0]`.
- **Existing coverage:** current catalog spec 37–74 already requires server selection, status plus query/domain/team, contract IDs, URL/history and page reset. Archive prototype design 84,95,99 explicitly leaves query semantics/full sort-filter allowlist gated, uses neutral «Поиск навыков», and retains `query`, `domain_id`, `team_id`, not copied demo parameters.
- **Delta/disposition:** newly available historical evidence names three search targets; it does not settle semantics of the current query operation. The example does not specify team filtering, matching/case rules, conjunction rules or domain value type. Do not remove accepted team filtering or change `domain_id` to `domain`. No sort parameter or sort order appears in this example; that is document-local silence, not evidence that current server sorting is absent.
- **Owner:** MOS-933/catalog G1 (MOS-929 for table data). Attach this evidence to the existing search/filter clarification; do not change the search promise or implement local-page search/sort.

### DELTA-SKILL-LIST-CARD-EXAMPLES-02 — paging/count shape; no replacement of accepted navigation

- **Evidence:** L34–46 offsets/limits; L114–118 example `pagination.{total,offset,limit}` = `15,0,15`; L175 explicitly ties paging to additional requests on «Показать ещё». Response contains three illustrated rows, not fifteen (L62–113).
- **Existing coverage:** catalog spec 32–35,39,46–59 requires restored selection/page, server total and limit/offset. Prototype design 95–99 rejects local total/metric calculation and per-row card fetches.
- **Delta/disposition:** supports server-supplied pagination metadata and historical load-more presentation, not replacement of accepted page/history navigation. Sample row count cannot be used as total or proof of a malformed live response. Default/max limit, stable ordering, total scope after filters and end-of-page behavior remain unspecified here. No server-sort allowlist can be derived from this envelope.
- **Owner:** MOS-933/catalog G1, with MOS-929 list display. Existing pagination requirement substantially covers the intent; retain presentation/contract ambiguity only.

### DELTA-SKILL-LIST-CARD-EXAMPLES-03 — ambiguous conflictsCount and alerts; existing count gate, not new defect

- **Evidence:** L72–79,90–94,105–110 show `skills[*].dialogsCount30d`, `conflictsCount`, misspelled **`allerts`**. Field table L161–174 defines dialogs over 30 days, but calls `conflictsCount` **«Количество аллармов»**, and `allerts` an array of alerts. Counts do not equal alert-array lengths: first 1 versus 2; second 2 versus 0; third 0 versus 1.
- **Existing coverage:** catalog spec 39,76–93 keeps statistics/warnings source-gated and distinguishes unavailable/error from no problems. Prototype design 84,89,99,134 separates catalog G1 from card/master G6 and forbids synthetic counters. REQ-MOS-1018 R08 supports a checks-tab conflict count; RECON-MOS-1018 proposed agreeing count source/completeness. **R-WRITE-MOS-1018 explicitly accepts publication without the broader count/presentation expansion**; linked-contract delta and its accepted review retain that exclusion.
- **Delta/disposition:** the newly inspected example adds a concrete naming/meaning ambiguity to that known count issue. It cannot establish phrase-conflict cardinality, unique affected phrases, severity, completeness, alert count equivalence or readiness. Zero is not certification of no conflicts. Do not rename/repair `allerts`, count arrays locally, reopen excluded count work, or claim a newly broken implementation.
- **Owner/prior candidate:** MOS-929/933 G1 for catalog display; MOS-1018-R08 / RECON count-source proposal for phrase meaning, with existing checks owner rather than a duplicate UI. Monitoring/analytics meaning remains with existing profile owners; no broader audit performed.

### DELTA-SKILL-LIST-CARD-EXAMPLES-04 — card questionnaire semantics substantially covered; shape mapping unresolved

- **Evidence:** C31–50 and `Тело ответа → skill - Блок описания навыков`, rows 1–17 (C96–115). `description` is short purpose (row 4); `fullDescription` optional extended description (row 5); `expectedResult`, type, zone, contact and restrictions/comments (optional rows 10–11) are explicit. `relatedMaterials` example is an array of `{title,note}` (C43–45), while table row 12 shows two string-like entries (C107–110). Version is string `2.4` (C46,111), and domain/team/contact are display strings.
- **Existing coverage:** skill-card-editing spec 9–16 already lists service_id, purpose, description, expected_result, type, domain, zones, team, contact, limitations, comments, related_materials, integer version and dates, with null handling and safe materials. MOS-944 archive design 19–33 retains unresolved contact source, read-only contact in partial scope and plain-text materials. Current spec 20–25 owns contract IDs and PUT, not the historical archive's PATCH.
- **Delta/disposition:** vocabulary suggests semantic correspondences (`description` → purpose, `fullDescription` → description, restrictions → limitations), **not an authorized DTO conversion**. Optional is not a complete missing/null/empty rule; singular zone does not define current zones-array cardinality; a contact name does not identify a selectable contact ID. The material table/example mismatch does not authorize links or an object-schema migration. Dotted example versions are not accepted integer concurrency versions. No new questionnaire field obligation beyond existing coverage is established.
- **Owner:** MOS-944/skill-card-editing for any field-shape clarification; retain approved server types, null behavior and safe display. No source precedence chosen.

### DELTA-SKILL-LIST-CARD-EXAMPLES-05 — status/capability display; preserve separate list/card rules

- **Evidence:** L71,89,104 show `rejected`, `checking`, `in_review`; C51 and table row 18 (C116) show localized `Прод`. C53–77 and117–141 include a separate `metrics30d` block with ratings/steps examples. These are display examples, not allowed-action/capability declarations.
- **Existing coverage:** catalog spec 39,61–74 and status-recovery design 27–31 approve only published filter enum values, preserve unknown string status in list rows as «Неизвестный статус», and keep strict card validation. Card spec 11 forbids synthesized unsupported lifecycle statuses. Prototype G6 at design 134 distinguishes visible capability explanations from fabricated values; catalog G1 remains separate. Later accepted status display is not undone by the earlier archive's exclusion.
- **Delta/disposition:** do not add `rejected`/`in_review` to filters, equate `in_review` with `review`, or wire localized `Прод` as a card enum. The list compatibility rule is not blanket acceptance of this old response envelope or relaxed card validation. Presence of status/metrics in examples does not activate lifecycle actions, connected analytics, warnings or readiness; metrics definitions/calculations are outside this bounded card-description comparison.
- **Owner:** skill-catalog-experience/status-display owner and MOS-944 overview, with existing profile owners for capability integration. This reinforces known source/model differences; no current API-absence claim or implementation finding.

## Architecture

Keep documentary vocabulary separate from accepted wire contracts and from integration/capability state. L uses `POST /api/esk/skills` (L3), UUID-shaped sample IDs and `skills`/`pagination`; C uses `POST /api/esk/skills/{id}` (C1), sample `s-water` (C15,32) and `skill`/`metrics30d`. Errors use `error_type/error_message` (L121–133; C80–92). None authorizes changing current methods, paths, IDs, response/error envelopes or mutation protocols.

Request-body `sudir_id` and `access_token` (L48–53; C17–22) are documentary examples, including anonymous-null prose. No credentials were retrieved, transmitted or requested; no session model, permission grant or auth-policy analysis is inferred. Accepted auth approval remains untouched. Card zone/restrictions describe the business skill, not the administrator session.

The accepted MOS-1018 boundary remains `design.md:13–18,24`: transient single-phrase result, persisted full-set save checks and agreed-send server validation are distinct. A list counter or descriptive card cannot certify complete current input, resolve normalization/disclosure, or resolve the known wizard/status disagreement. The accepted linked-contract no-material-delta conclusion is not displaced. Current r2 API publication is acknowledged; no fresh operation scan or present-day absence claim was made.

## Start Here

`openspec/specs/skill-catalog-experience/spec.md:37–93`, followed by prototype archive `design.md:84–99` and status-recovery archive `design.md:27–31`: these establish which historical example semantics are already covered and which remain gated. For card vocabulary use `openspec/specs/skill-card-editing/spec.md:9–25`. Candidates above are evidence attachments to those owners, not a new plan or authority to reopen/close work.

## Validation and residual risks

Local file discovery, complete two-source readable/chunk inspection, metadata/attachment-index parsing and numbered documentary comparison only. No network/browser/MCP, example execution, application-code audit, tests/build, API scan, nested delegation or product/source/archive edits. Only this report was written. Parent hashes/roundtrip and prior validation results remain attributed, not independently attested. Saved examples cannot prove deployment or runtime behavior. Unresolved items are current search/filter mapping, count meaning/completeness and historical-to-current field/status shapes; no automatic source precedence is proposed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Five bounded stable candidates compare both complete historical examples and exact table/key/line locators against current catalog/card clauses and accepted MOS-1018 publication boundaries."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-SKILL-LIST-CARD-EXAMPLES.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read/find and Python metadata/attachment inspection; numbered documentary reads","result":"passed","summary":"Both full readable bodies and exact chunks inspected; empty returned attachment indexes confirmed; relevant accepted owner decisions located."},
    {"command":"Tests/build/browser/network/example execution","result":"not-run","summary":"Prohibited by bounded read-only assignment."}
  ],
  "validationOutput": ["Historical search/paging/card vocabulary documented; no automatic API/session adoption, feature activation, task closure or implementation defect claim."],
  "residualRisks": ["Search semantics, count meaning/completeness and field/status mappings are not resolved for current contracts by these examples.","Parent hashes/roundtrip not independently recomputed; saved documentation is not runtime evidence.","Index/staging state not inspected; no staging operations performed."],
  "diffSummary":"Only authoritative audit report written; no code, source, main-spec, archive or planning edits.",
  "reviewFindings": [],
  "manualNotes":"Read-only documentary delta apart from the designated output; count/presentation expansion excluded from accepted WRITE-MOS-1018 remains excluded. Independent review/parent acceptance remains separate."
}
```
