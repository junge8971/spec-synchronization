# G1-API-COLLECTION-DELTA

## Result

**Three historical requests: (1) partial—new discovery evidenced, original provenance still independently unverified; (2) resolved for the saved Swagger entrypoint, partial for broader explanatory-source sufficiency; (3) resolved—API container captured and classified, with all six named children already captured and documentarily covered.** This is a bounded disposition, pending independent review, not task 2.4 acceptance or global closure. Progress remains **6/28**; tasks 2.3/2.4/2.6 remain open.

`A/` below expands exactly to `openspec/changes/reconcile-control-center-backlog/audit/`. Source dates, HTTP outcomes, hashes and acquisition safeguards are attributed to saved metadata and accepted chains; none was remotely observed or independently recomputed here. “Current coverage” means the saved increments through D-044, not current external freshness.

## Old request → increment → disposition

| Historical request in `A/reports/G1-API-COLLECTION.md`, “Exact remaining collector requests” | Actual increment and exact locator | Disposition / remaining boundary |
|---|---|---|
| **1. Recover original Swagger discovery receipt tied to api-live/r1, or retain uncertainty.** | `A/sources/api-live/r1/metadata.json:2–18` records 2026-10-16T11:13:29.451Z and asserted Swagger discovery. Separately, `A/sources/api-docs/r1/content.html:1–32`, especially configuration line 17, supplies `url: '/api/control/openapi.json'`. Adjacent `metadata.json:2–19` records 2026-10-19T08:10:46.142Z, full decoded inert HTML, HTTP200 and resolved URL. `A/sources/api-live/r2/metadata.json:2–21` explicitly links this receipt and records 2026-10-19T08:11:44.238Z. D-022/D-023 accept the increment and its bounded impact reviews. | **Partial overall.** The separate discovery-to-r2 chain is evidenced; the original r1 discovery remains metadata-attested only. No original receipt was supplied by these increments; this is not proof it never existed or that the collector guessed. A new read cannot repair historical provenance retroactively. Only an already-retained original receipt, if available through the parent, could supplement that question; otherwise explicitly retain it as unverified. No fresh network acquisition is required by this finding. |
| **2. Disposition explanatory documents linked from the docs entrypoint.** | Entire saved HTML inspected inertly. Exact observed spec/config/asset/callback set is enumerated below and agrees with `api-docs/r1/metadata.json#/linkedResources`. Existing explanatory packets reconciled below by exact ID, not title. D-030 supersedes unread835759; D-027/D-029 qualify registry/prototype coverage; D-044 repairs feedback index only. | **Resolved at this saved entrypoint; partial beyond it.** It exposes the OpenAPI URL, not another business explanatory-document link. Assets and callback are expressly excluded with reasons. This is positive inspection of this HTML, not an inference from absent OpenAPI `externalDocs`, nor a claim about every Jira/wiki reference. Broader source/attachment relevance and authority remain separately bounded; no exhaustive-documents certificate follows. |
| **3. Coordinate discovered wiki241085256 “API,” formerly uncollected/relevance pending.** | `A/sources/wiki-241085256/r1/content.json:1–21` and `metadata.json:1–22`: HTTP200, v2, captured 2026-10-19T09:36:52.261Z under D-031. Complete `/bodyView` at line11 is a children macro with six links; `/attachments` at lines13–20 is size0, next null. `A/reports/REL-D031-PLANNING-API.md`, section “241085256 — API”; `A/reviews/R-REL-D031-PLANNING-DATA.md`, PLANNING row/finding; D-032. | **Resolved collection/relevance request.** Link/container-only, not endpoint contract. D-032 accepts corrected classifications while retaining original REVISE: analyst-local unread must not mean globally uncollected. All six children now have saved packets and accepted documentary chains below. No automatic traversal or semantic completeness follows. Distinct registry247747363 is not a substitute for this container. |

### Publication provenance, without another semantic audit

`api-live/r1` metadata declares SHA-256 `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`; `api-live/r2` declares `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993`; Swagger receipt declares `02aecc4a486cd3b697887ca917500e2cbd031ee9e1177dfba17c1bf588873ece`. These are **attributed values**, not this run's hash checks. r2 metadata retains OpenAPI3.1.0/info.version0.1.0; original report retains those r1 versions. Matching version labels do not mean identical publications.

Reuse `A/reports/API-R2-STATUS-DELTA.md` and `API-R2-TOKEN-DELTA.md`, their exact named `A/reviews/R-API-R2-STATUS-DELTA.md` and `R-API-R2-TOKEN-DELTA.md`, and D-023: the newer publication has accepted bounded status/token changes. Selected reviewer closures, not whole-publication reviewer verification, underpin acceptance; hash/reachability claims retain their author/parent attribution. Derived `api-token-status-readable/{r1,r2}` and `api-live-status-readable/r1` are not acquisitions. No schemas or operation semantics were re-audited here. Published security, historical auth approval, token-owner/disclosure/revocation gates, three-command scope and source-conflict gates are untouched.

## Exact saved Swagger link/config disposition

Base URL from `A/sources/api-docs/r1/metadata.json#/url`: `https://nchat-a-tech.mos.ru/api/control/docs`.

| Inert HTML locator | Exact observed target | Disposition |
|---|---|---|
| `content.html:17`, SwaggerUIBundle `url` | `/api/control/openapi.json` → `https://nchat-a-tech.mos.ru/api/control/openapi.json` | Published specification; captured separately as api-live/r2, not an additional prose document. Resolution is also recorded in metadata `/discovery`. |
| `content.html:6`, stylesheet href | `https://cdn.jsdelivr.net/npm/swagger-ui-dist@5/swagger-ui.css` | Swagger UI stylesheet, not business explanatory documentation; metadata says not fetched. |
| `content.html:7`, shortcut-icon href | `https://fastapi.tiangolo.com/img/favicon.png` | UI icon, not explanatory documentation; not fetched. The hostname does not authorize documentation-site traversal. |
| `content.html:13`, script src | `https://cdn.jsdelivr.net/npm/swagger-ui-dist@5/swagger-ui-bundle.js` | UI runtime asset, not explanatory documentation; not fetched/executed. No runtime-generated link inventory claimed. |
| `content.html:23`, oauth2RedirectUrl | `window.location.origin + '/api/control/docs/oauth2-redirect'`; metadata resolves `https://nchat-a-tech.mos.ru/api/control/docs/oauth2-redirect` | OAuth callback configuration, not business explanatory documentation; not visited. No auth-flow authority inferred. |

`#swagger-ui`, layout, presets, deepLinking and extension flags are renderer configuration, not extra explanatory-source links. The full saved HTML has no other document anchors/configured document URLs. This finding is bounded to its static saved text; no asset execution, rendering, callback access or externalDocs-based completeness inference was used.

## Reconcile the old explanatory packet table

Each row below retains the old table's exact canonical content path. Metadata was directly read; original bodies were **not** re-audited. JSON locators `/version` (or `/version/number`), `/retrievedAt`, `/attachments`, `/limitations` identify provenance. Existing captures are not new acquisitions in this run. A saved body is not whole-source semantic acceptance.

| Exact canonical content path under A | Metadata read / retained identity | Present collection disposition |
|---|---|---|
| `sources/wiki-241082009/r2/content.json` | adjacent `metadata.json:1–50`; v5, HTTP200, 2026-10-16; separate empty attachment index | Retained surface contract; r1 failed attempt preserved. Not the root surface brief241080065 or business page245673187. No duplicate fetch candidate. |
| `sources/wiki-241097511/r2/content.json` | adjacent `metadata.json:1–49`; v6, HTTP200, 2026-10-16; separate empty attachment index | Retained domain/skill catalog contract; earlier404 cause remains unknown. Not dictionary/API registry. No duplicate fetch candidate. |
| `sources/wiki-241085439/r1/content.json` | adjacent `metadata.json:1–56`; v15, HTTP200; 8 bearer-example redactions; index0/next null | Retained dialogue contract, linked through MOS1015 metadata. Not the later dialogue-list/card examples. Preserve redactions and publication/runtime distinction. |
| `sources/wiki-241085838/r1/content.json` | adjacent `metadata.json:1–56`; v3, HTTP200; index0/next null | Retained report contract. D-036 explicitly preserves prior v3 catalog alongside newer root examples, not a replacement or precedence decision. |
| `sources/wiki-241088180/r1/content.json` | adjacent `metadata.json:1–56`; v4, HTTP200; index0/next null | Retained global-modules contract; distinct from root system-state pages247747489/241080088 accepted under D-037. |
| `sources/wiki-241092242/r1/content.json` | adjacent `metadata.json:1–56`; v4, HTTP200; index0/next null | Retained stubs/banner/maintenance contract; not root templates247744768/admin-stubs241080097 accepted under D-038. |
| `sources/wiki-241080062/r1/content.json` | adjacent `metadata.json:1–14`; v17 | Retained Admin Skills body. Accepted final root ledger/review identifies indexed SVG245672060 still unread, not missing page body. Readable derivatives add no page or acquisition. |
| `sources/wiki-245673187/r1/content.json` | adjacent `metadata.json:1–14`; v18 | Retained surfaces business analysis. Accepted ledger/review carries empty index via parent-projected legacy packet; this run does not independently reparse it. Distinct from brief241080065. |
| `sources/wiki-243776365/r1/content.json` | adjacent `metadata.json:1–14`; v13 | Retained dialogues business analysis. Accepted ledger/review carries empty index via parent projection. Later D-035 supplements do not replace this body or certify its exhaustive semantics. |
| `sources/wiki-247734813/r1/content.json` | adjacent `metadata.json:1–11`; v11, flattened body.view textContent/links | Retained feedback extraction, not full structural body. New `sources/wiki-247734813-attachment-index/r1/{content.json,metadata.json}` is a separate 2026-10-19 selected index; D-044 and `reviews/R-FEEDBACK-INDEX-REPAIR.md` accept five entries, not attachment bodies or a body refresh. Structural repair remains conditional on a concrete table-sensitive owner question. |

Metadata can contain stale capture-time wording without being erroneous history. In particular:

- `A/sources/jira-api-delta-scenarios/r1/metadata.json:1–8` describes selected descriptions and attachment metadata, not full issues or executed examples. It remains retained evidence, not an exhaustive Jira document set.
- `A/sources/jira-lifecycle-details/r2/metadata.json:1–16` retains normalized MOS1119 description, comments excerpts, earlier failure and unread-at-capture attachment qualification. `A/sources/jira-attachment-833803/r1/metadata.json:1–17` separately binds the full decoded test plan to that issue. Its historical “835759 remains unread” is not current inventory.
- `A/sources/jira-skill-switch-details/r1/metadata.json:25–30` likewise records unread835759 historically. **Superseded for current collection:** `A/sources/jira-attachment-835759/r1/metadata.json:1–23` records exact indexed URL, HTTP200, full saved `content.md`, capture 2026-10-19T09:25:25.254Z and digest. `A/reports/DELTA-MOS-1145-TESTPLAN.md` and `A/reviews/R-DELTA-MOS-1145-TESTPLAN.md`, accepted by D-030, cover the complete 322-line text and TP01–10. No re-download or test-plan-body gap remains. Test/deploy prose is source-attributed; scenarios, SQL and HTTP were not executed. Old reports/metadata remain unchanged.

## API-container children and separate registry

Complete primary container read: `A/sources/wiki-241085256/r1/content.json:11` (`/bodyView`, six ordered `li/a` hrefs). No hidden requirement prose or additional links occur in that compact body. The following are exact target IDs, not guessed endpoints. Each child's `metadata.json:1–21` was directly read; all record HTTP200, full bodyView plus separate returned index, and **root-authorized** capture—not traversal authority granted by the container. Empty indexes are reused from the accepted ledger/review, not newly parsed here.

| Child / saved canonical content | External version / capture | Accepted documentary chain reused |
|---|---|---|
| `/skills` → `A/sources/wiki-238347066/r1/content.json` | v8; 2026-10-19T10:18:27.973Z | `A/reports/DELTA-SKILL-LIST-CARD-EXAMPLES.md` → `A/reviews/R-DELTA-SKILL-EXAMPLES.md` → D-034 |
| `/skills/{id}` → `A/sources/wiki-238352321/r1/content.json` | v2; 10:18:28.161Z same day | Same chain; no current API adoption |
| `/skills/{id}/monitoring` → `A/sources/wiki-241074633/r1/content.json` | v4; 10:18:28.344Z | `A/reports/DELTA-SKILL-MONITORING-EXAMPLE.md` → same review → D-034 |
| `/dialogs` → `A/sources/wiki-241080643/r1/content.json` | v7; 10:35:01.626Z | `A/reports/DELTA-DIALOG-LIST-CARD-EXAMPLES.md` → `A/reviews/R-DELTA-DIALOG-SUPPLEMENTS.md` → D-035 |
| `/dialogs/{id}` → `A/sources/wiki-241083649/r1/content.json` | v2; 10:35:01.839Z | Same chain; source differences preserved |
| `/reports` and builder → `A/sources/wiki-238350232/r1/content.json` | v33; 10:44:36.785Z | `A/reports/DELTA-REPORTS-ROOT-DOCS.md` → `A/reviews/R-DELTA-REPORTS-ROOT-DOCS.md` → D-036 |

These chains are reused from D-034–D-036 and accepted `A/reports/G1-ROOT-REGISTRY-FINAL-INCREMENT.md`, “Accepted chains and correction provenance,” with `A/reviews/R-G1-ROOT-REGISTRY-FINAL-INCREMENT.md`; their individual source semantics were not reread. Historical PLANNING “unvisited” rows are lane-local, not six outstanding acquisition requests.

**Distinct registry:** `A/sources/wiki-247747363/r1/metadata.json:1–20` records “Раздел API,” v7, 2026-10-19T09:01:11.011Z. `A/reports/WIKI-API-REGISTRY.md`, WAR01–12/Versions and evidence coverage, plus `A/reviews/R-WIKI-API-REGISTRY.md` and D-027 accept registry documentary coverage, not published service API conformance. Its two HTML attachments250800526/247747361, initially unread in that chain, are subsequently saved and **selectively** reviewed under D-029 (`reports/ATTACH-API-PROTOTYPES.md` → `reviews/R-ATTACH-API-PROTOTYPES.md`, as carried by accepted root ledger). No whole-prototype acceptance, execution, or inferred PDF acquisition. Registry PDF-model conformance assertions and embedded-image coverage remain unverified; neither title nor PDF mention supplies an authorized new URL.

## Bounded remaining questions/candidates

1. **Historical r1 provenance only:** can the parent supply an already-retained original discovery receipt bound to the 2026-10-16 capture? The consulted increments supply none. If unrecoverable, preserve “independently unverified,” not “guessed.” No network visit or new acquisition is needed to state this limitation.
2. **Task2.4 sufficiency decision after independent review:** determine whether these entrypoint dispositions and retained explanatory packets satisfy its bounded “available explanatory documents” requirement with explicit residual exclusions. Do not require all42 root semantics/all code as an invented prerequisite; equally, do not infer sufficiency from absence of externalDocs or root-count completion. No additional uncollected business-document URL was found in the saved Swagger HTML.
3. **Only owner-question-driven attachment work:** skills SVG245672060 remains a discovered candidate at the accepted ledger's parent241080062 attachment row. Feedback IDs250790182/247746709/247739129/247737143/247734812 are now indexed (`A/sources/wiki-247734813-attachment-index/r1/content.json:2–24`, reviewed in R-FEEDBACK-INDEX-REPAIR), but relevance and body authority remain unresolved; filenames do not establish API explanatory necessity. Ask which precise owner question requires any body before proposing collection. No blanket download authority exists. Reuse already-saved registry prototypes first; referenced PDF/image requires an exact relevant locator and authorization, not guessed navigation.
4. **Conditional feedback structural repair:** only if a named table-sensitive question cannot be answered from retained extraction/accepted evidence; D-044 does not authorize an automatic page refresh. The index gap itself is resolved.

No remaining container-child acquisition request is justified for the six listed IDs. No repeat Swagger/API fetch, callback/asset visit, registry recollection or test-plan835759 download is proposed. Other root attachment/diagram boundaries remain with accepted owners, not newly demanded for task2.4 by this report.

D-043's historical42/41/34 accounting remains intact. D-044 adds the feedback index to yield42 page packets/42 returned indexes/**39 entries = 4 saved texts +35 unread bodies**. These are accepted accounting facts reused here—not a fresh census, explanatory-document completeness, review of all four texts in full, or automatic authority to read35 bodies.

## Code Context

### Files Retrieved

Primary reads and exact ranges are recorded in the tables above. Additional complete assigned/accepted-chain reads: `A/work-items/G1-API-COLLECTION-DELTA.md:1–15`, `A/work-items/G1-API-COLLECTION.md:1–9`, `A/reports/G1-API-COLLECTION.md` (complete, including acceptance block); `openspec/changes/reconcile-control-center-backlog/tasks.md:1–32` (task2.4 at line13). `A/decisions.md:1–180` supplies D-022–D-044 and stable heading-based dispositions. Earlier decision context was returned but not re-audited. API-R2 reports/reviews, PLANNING report/review, final root review, feedback repair review and MOS1145 test-plan report/review were read completely. Root report was read through line180 (all substantive sections); registry report through line65 (all substantive sections), with complete registry review. No claim to inspect their remaining acceptance-block tails.

### Key Evidence / Architecture

Saved inert source → separately dated metadata → local derivatives → scoped report → independent review → parent decision. These are different evidence layers. Discovery receipts bind only their own capture; derivatives do not create acquisitions; index entries do not supply bodies; body collection does not certify semantics, authority or deployment. No application code was inspected.

### Start Here

Open `A/sources/api-docs/r1/content.html:1–32` and its metadata, then this report's three-request table. Review the remaining historical-provenance qualification separately from present explanatory-source coverage before any task2.4 decision.

## Validation and limits

Only local read/find/targeted grep tools and the sole report write were used. One scoped metadata grep returned no matches; direct exact-path reads superseded it, and no absence conclusion relies on that search. No source execution, schema parsing, hash computation, root census, browser/network/storage/credentials access, requests, downloads, code/tests/build/E2E, nested delegation or other edits occurred. Staging state was not inspected or attested. Independent review follows; global6/28 is unchanged.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Three historical collector requests dispositioned separately; exact inert Swagger target set, ten prior packets, six already-covered container children and superseded835759 gap reconciled with accepted decisions."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/G1-API-COLLECTION-DELTA.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read/find and scoped metadata grep","result":"passed","summary":"Exact-path reads supplied evidence; empty grep result was not used as absence proof."},
    {"command":"Network/browser/source execution/code/tests/build/hash recomputation","result":"not-run","summary":"Excluded from this bounded documentary disposition."}
  ],
  "validationOutput": ["Gap1 partial; gap2 resolved for saved Swagger entrypoint but broader sufficiency remains qualified; gap3 resolved as collection/relevance request.","Historical r1 uncertainty retained; no repeated API semantics or42-root census; global6/28 unchanged."],
  "residualRisks": ["Original r1 discovery remains independently unverified.","Broader explanatory-source relevance, permission-gated attachments and conditional structural questions remain; accepted counts do not establish completeness.","Acquisition/hashes and reused semantic chains remain attributed; external freshness/runtime unverified; independent review pending."],
  "diffSummary":"Sole assigned report written; sources, decisions, tasks, specs and owner plans untouched.",
  "reviewFindings": ["No automatic task2.4 or G1 closure; no new collection authority inferred."],
  "manualNotes":"This is an incremental collection disposition, not API product analysis or test execution. No staging-state attestation. Preserve all historical reports and original REVISE/parent-correction lineage."
}
```
