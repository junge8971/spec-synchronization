# Code Context

## Result

**Wire widening confirmed; business acceptance is not widened to arbitrary strings.** MOS-1306 preserves the list-of-zone-codes representation while requiring directory-backed validation and continued reading of already-linked inactive zones. The main specification still names only `authenticated`/`anonymous`. No active domain/zone product change or task owner was found in the current non-archive artifacts. Route the planning gap to the **skill-domain-management capability owner**, with MOS-1306 as backend dependency; the reconciliation change owns this evidence handoff, not product-policy approval. No named person or existing active implementation task can be identified from these inputs.

## Files Retrieved

Paths are repository-relative; single-line JSON citations use exact JSON pointers below.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-DOMAIN-ZONES.md` (lines 1–9): assignment.
2. `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-API-001.md` (lines 1–153), `openspec/changes/reconcile-control-center-backlog/audit/reports/API-SCHEMA-001.md` (lines 1–224), `openspec/changes/reconcile-control-center-backlog/audit/reports/API-OPS-001.md` (lines 1–155), `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (lines 1–185): prior routing, not substitutes for fresh source checks.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1), `metadata.json` in that directory (lines 1–19): current contract, selected domain and lookup branches independently parsed.
4. `docs/api/contracts/openapi-2026-10-15.raw` (line 1): historical domain schemas and operations independently parsed.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/content.json` (MOS-1306 object at `/items/1`, key at line 25, attachment filename at line 35), `metadata.json` in that directory (lines 1–8): only MOS-1306 analyzed. Other issue contents were not used.
6. `openspec/specs/skill-domain-management/spec.md` (lines 1–59): baseline coverage, fixed-code requirement and approved deferrals.

Targeted path discovery found no active domain/zone-named change. A non-archive, non-audit Markdown scan for `MOS-1306`, `skill-domain-management`, `SkillZone`, `skill_zones`, `skill_domain_zones`, whole-word `zones` and Russian zone forms returned no matches. Main-spec scoped search found zone requirements only in the domain capability. Archive paths were discovered but archive contents were not read. Thus there is **no active scenario/task locator to cite for a domain-zone continuation**; do not invent one or reuse unrelated skill changes.

## Key Code / exact evidence

### Published wire contract

Current-source pointers below were compared directly with historical raw:

| Exact JSON pointer | Historical → current |
|---|---|
| `/components/schemas/SkillZone` | `{"type":"string","enum":["authenticated","anonymous"],"title":"SkillZone"}` → absent |
| `/components/schemas/CreateDomainRequest/properties/zones/items` | `{"$ref":"#/components/schemas/SkillZone"}` → `{"type":"string"}` |
| `/components/schemas/DomainResponse/properties/zones/items` | same ref → inline string |
| `/components/schemas/UpdateDomainRequest/properties/zones/anyOf/0/items` | same ref → inline string |
| `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2/schema/anyOf/0` | same ref → inline string |

The query remains optional `zone`, nullable. Create still requires `zones`; response still requires `zones`; update requires only `expected_version`, with optional nullable `zones`. The three zone array branches have no `minItems` or `uniqueItems`; string items have no enum. These absences are schema expressiveness gaps, not permission to submit empty, duplicate, unknown or inactive values. Nullable/omitted update behavior must not be silently assigned a new meaning.

Affected domain roots: GET/POST `/api/control/api/skills/v1/domains`, GET/PUT/PATCH `/api/control/api/skills/v1/domains/{domain_id}`. At each corresponding `/paths/<RFC6901-escaped-path>/<method>/description`, description is **absent in both snapshots**. There is therefore no new domain-operation description to quote as validation evidence; the substantive description is Jira's, below.

### MOS-1306 business description

All following exact excerpts are from `/items/1/description` in the Jira snapshot (Jira markup preserved):

- Compatibility: “Внешний API и доменное представление {{Domain.zones}} должны остаться совместимыми: клиент продолжает передавать и получать список кодов зон.”
- Validation: “* требовать хотя бы одну зону;”, “* запрещать повторяющиеся зоны;”, “* проверять существование зоны в {{skill\\_zones}};”, “* разрешать назначение только активных зон;”, “* отклонять неизвестные и неактивные значения.”
- Existing inactive value: “Неактивная зона, уже связанная с доменом, должна продолжать отображаться при чтении, но не должна назначаться новым доменам.”
- Ordering: “* Сортировать зоны по {{skill\\_zones.sort\\_order}}.”
- Join correctness: “* Не допускать дублирования доменов и некорректного {{skills\\_count}} из-за JOIN со связующей таблицей.”
- Atomicity: “* Изменение домена и его зон выполнять в одной транзакции.”
- Scope: “Формат запросов и ответов не изменяется:” and “Изменение является внутренней нормализацией модели хранения.”

The same description seeds `authenticated` / Авторизованная / 10 / true and `anonymous` / Неавторизованная / 20 / true; requires synchronization without recreating unchanged links and zone filtering via EXISTS or JOIN. Storage migration acceptance is backend work, not frontend implementation authorization. `/items/1/status` is `Ready for test`, not test evidence or availability certification.

### Still-missing directory evidence

The current snapshot does publish a **generic lookup candidate**, so “no directory API exists” would overstate the evidence:

- `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get/parameters/0/schema/$ref` → `CatalogLookupSectionName`.
- `/components/schemas/CatalogLookupSectionName/enum` includes `skills`.
- `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get/responses/200/content/application~1json/schema/$ref` → `TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___`.
- `/components/schemas/TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___/properties/data/additionalProperties/items/$ref` → `ManagedResourceCatalogItem`.
- `/components/schemas/ManagedResourceCatalogItem/properties` includes `code`, `display_name`, `sort_order`, `is_active`; `/required` contains only `code`, `display_name`.

This generic map does **not identify a zone collection key or guarantee that skills lookups include zones or inactive linked values**. No zone-named path/schema was found. Still needed: confirmed lookup key/response example, active versus inactive inclusion/filtering, ordering and label semantics, unknown historical-code handling, directory failure behavior and documented business-error payloads. Do not infer a zone directory from a database table or fabricate an endpoint. No observed lookup/backend response was supplied.

## Architecture / coverage and minimal proposed deltas

MOS-1306 normalizes backend persistence → domain DTOs continue carrying codes → UI needs separate selection eligibility and existing-value rendering. Schema widening supports code representation, not business validation. Main-spec coverage is normative planning evidence only; application implementation and test coverage were not inspected.

All baseline locators below refer to `openspec/specs/skill-domain-management/spec.md`:

| Existing requirement/scenario locator | Coverage | Minimal proposed planning delta, not an authorized edit |
|---|---|---|
| `Server-backed domain registry`, lines 9–21; `Domain with skills beyond the loaded skill page`, lines 13–16 | Zones displayed, server total/skills_count, domain navigation, empty/error states | Add read/list scenario retaining an inactive linked code and server ordering; filtered result has one row per domain and unchanged skills_count. Do not derive counts by client joins. |
| `Domain creation form`, lines 23–25; `Successful domain creation`, lines 27–30 | Two fixed codes; server-backed success refresh | Reconcile fixed two-code wording with directory-driven active assignment **after directory evidence/approval**. Preserve both seeded codes. Add active-code assignment and reject empty/duplicate/unknown/inactive zone scenarios; no free-text “any string” interpretation. |
| `Domain validation failure`, lines 32–35 | Preserved input, known-field errors, general fallback for unknown paths, no false success | Explicit zone rejection coverage without assuming Jira business failures use exactly the schema-validation envelope. Capture actual error contract before tightening field mapping. |
| `Team directory unavailable`, lines 37–40 | Team-only directory failure | Add analogous zone-directory loading/empty/error/retry acceptance only once the actual source is agreed; do not replace missing lookup data with invented codes. |
| `Version-safe domain editing`, lines 42–44; `Concurrent modification`, lines 46–49; `Retry after network failure`, lines 51–54 | PUT, expected_version, Idempotency-Key, preserved dirty input, safe retries | Add existing inactive-value read/edit scenario and unchanged-zone round trip; specify behavior only after resolving ambiguity below. Preserve concurrency/idempotency rules and no-loss failure behavior. |
| `Keyboard cancellation`, lines 56–59 | No mutation on cancel and accessible focus/labels | Retain for any future zone-selection UI; no separate accessibility regression waiver. |

No active tasks can currently absorb these as already-approved implementation work. Proposed next artifact is an owner-reviewed domain-zone continuation plan, not creation of a change by this audit.

### Conflicts / decisions explicitly left open

1. **Baseline fixed-code constraint vs directory evolution:** line 25 says zones SHALL correspond to `authenticated`/`anonymous`; Jira supplies those as seeds and active-directory rules, while OpenAPI allows string representation. These are different scopes of evidence. Do not silently supersede the main spec or declare new codes accepted.
2. **Inactive read vs update acceptance:** Jira requires inactive linked zones remain readable, but also says create/update reject inactive values. Whether an unchanged inactive code can be re-submitted, must be omitted from an unrelated partial update, or requires explicit remediation is not settled by these inputs. Preserve display and input; owner/backend clarification must precede update-policy assertions. Do not silently strip, reactivate or reassign it.
3. **Representation compatibility vs enum removal:** list shape and original codes remain compatible; enum removal is nevertheless a schema/type change. “Internal normalization” does not justify ignoring the contract delta, nor does it prove runtime widening.
4. **Preserved approved deferrals:** main-spec line 25 explicitly defers additional name/api_url normalization/uniqueness and other unpublished restrictions to separate agreement; it prohibits invented preflight and demo-derived restrictions from blocking CRUD. Zone reconciliation does not reopen those deferrals or authorize auth/role changes.

## Start Here

Open `openspec/specs/skill-domain-management/spec.md:23–44`, alongside Jira `/items/1/description` and the current three zone schema branches. First resolve directory evidence and inactive-update semantics with the capability/backend owners; then produce minimal proposed scenario/task changes for approval, rather than editing baseline or assuming deployment readiness.

## Validation and limitations

Local read-only Python inspections independently parsed the selected source branches, compared historical/current schemas, scanned active artifact zone references and traversed the generic lookup refs. Current API and Jira content SHA-256 values matched their saved metadata. Provenance records API retrieval `2026-10-16T11:13:29.451Z`, Jira retrieval `2026-10-16T11:23:51.742Z`; these are saved captures, not fresh network observations.

Confluence, comments and attachment bodies were **not collected**. `/items/1/attachments/0/filename` is `TEST_PLAN_MOS_1306.md`; metadata/URL presence is not its contents or execution evidence. No backend implementation, migration, application/generated contract, runtime response, browser or test inspection establishes completion here. No tests, generation, network/MCP/browser, nested delegation or source/spec/archive edits were performed. No infrastructure/input blocker occurred. Only this report was written; pre-existing staging state was not inspected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Fresh source comparison confirms enum removal and four inline-string branches; MOS-1306 quotes, baseline scenario locators, absent active task ownership, lookup evidence gaps and minimal proposed deltas recorded without policy decisions."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-DOMAIN-ZONES.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python selected MOS-1306 extraction and active artifact reference inspection","result":"passed","summary":"Only MOS-1306 issue analyzed; no relevant active domain-zone plan references found."},
    {"command":"Local Python digest, historical/current domain schema and lookup reference inspections","result":"passed","summary":"Both saved digests matched; zone deltas and generic lookup limits confirmed."},
    {"command":"tests / generation / network / browser","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["SkillZone absent currently; create/read/update zones and list zone parameter use strings.","Generic skills lookup exists but zone key/inactive inclusion are not specified by inspected schema."],
  "residualRisks": ["Inactive-code re-submission semantics and concrete directory evidence remain unresolved.","No active product continuation task or named owner found; capability-level handoff only.","Confluence/comments/attachment bodies and runtime/backend/application evidence unavailable or outside scope."],
  "noStagedFiles": true,
  "diffSummary": "Only bound audit report written; no application, generated, main-spec or archive modifications.",
  "reviewFindings": ["Planning gap: fixed-code baseline requires owner-reviewed reconciliation, not automatic arbitrary-string acceptance."],
  "manualNotes": "No staging performed; index state not inspected. Preserved normalization/uniqueness deferrals. No deployment readiness or product precedence conclusion."
}
```
