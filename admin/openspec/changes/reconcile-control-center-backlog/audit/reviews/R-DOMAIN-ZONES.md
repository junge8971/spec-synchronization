# Code Context

## Decision

**REVISE narrowly; core evidence accepted.** The report correctly separates schema widening from eligible assignment and identifies the inactive-update uncertainty. Its directory and policy gates must not hold up already-supported planning corrections. No application or baseline change is authorized by this review.

## Files Retrieved

All paths below are repository-relative. JSON pointers identify independently parsed branches, not inferred source content.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/R-DOMAIN-ZONES.md` (lines 1–8): review scope.
2. `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-DOMAIN-ZONES.md` (lines 1–120): findings and candidate deltas reviewed, not used as primary proof.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1): current domain schemas, operations, generic lookup references.
4. `docs/api/contracts/openapi-2026-10-15.raw` (line 1): historical counterparts.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/content.json` (lines 24–40, `/items/1` only): MOS-1306 description, status and attachment metadata.
6. `openspec/specs/skill-domain-management/spec.md` (lines 1–59): normative baseline.

Bounded discovery: `find` under `openspec/changes` for domain/zone paths returned no relevant non-audit active change. A local read-only scan of 85 non-archive, non-audit Markdown files for `MOS-1306`, `skill-domain-management`, `SkillZone`, `skill_zones`, `skill_domain_zones`, whole-word `zones` and Russian zone-word forms returned zero matches. An initial substring scan also matched unrelated words such as диапазон; those are not domain evidence. Archive contents and unrelated reports were not read.

## Key Code / independent evidence

### E1 — Wire representation, not eligibility

Historical → current, at identical JSON pointers:

- `/components/schemas/SkillZone`: `{"type":"string","enum":["authenticated","anonymous"],"title":"SkillZone"}` → absent.
- `/components/schemas/CreateDomainRequest/properties/zones/items`: `$ref: #/components/schemas/SkillZone` → `{"type":"string"}`.
- `/components/schemas/DomainResponse/properties/zones/items`: same change.
- `/components/schemas/UpdateDomainRequest/properties/zones/anyOf/0/items`: same change.
- `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2/schema/anyOf/0`: same change; parameter remains optional `zone`, with a null alternative.

Create and response still require zones; update `/required` remains `["expected_version"]`, and its zones remains optional/nullable. None of the three zone array branches specifies minItems/uniqueItems. These facts do not establish empty/duplicate/inactive acceptance or omission/null semantics. Domain collection GET/POST and domain-item GET/PUT/PATCH descriptions are absent in both snapshots.

### E2 — MOS-1306 business rules

Exact source: Jira `/items/1/description`, line 30, sections named below:

- Opening compatibility statement: “клиент продолжает передавать и получать список кодов зон.”
- **Валидация**: “При создании и изменении домена backend должен:” followed by “требовать хотя бы одну зону”, “запрещать повторяющиеся зоны”, “проверять существование зоны в {{skill\\_zones}}”, “разрешать назначение только активных зон”, and “отклонять неизвестные и неактивные значения”.
- Same section: “Неактивная зона, уже связанная с доменом, должна продолжать отображаться при чтении, но не должна назначаться новым доменам.”
- **Справочник зон** seeds `authenticated` / Авторизованная / 10 / true and `anonymous` / Неавторизованная / 20 / true. These are initial values, not proof of additional currently available codes.
- **Изменение persistence-модели**: “не пересоздавать неизменившиеся связи”; “Изменение домена и его зон выполнять в одной транзакции.”
- **Изменение query repository**: “Сортировать зоны по {{skill\\_zones.sort\\_order}}”; “Не допускать дублирования доменов и некорректного {{skills\\_count}} из-за JOIN со связующей таблицей.”
- **API**: “Формат запросов и ответов не изменяется”; “Изменение является внутренней нормализацией модели хранения.” These concern representation/storage, not negation of E1's schema delta.

`/items/1/status` is `Ready for test`. `/items/1/attachments/0/filename` is `TEST_PLAN_MOS_1306.md`; its body and execution results are not present in inspected evidence.

### E3 — Directory candidate, not confirmed zone directory

Current API:

- `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get/parameters/0/schema/$ref` references `CatalogLookupSectionName`; `/components/schemas/CatalogLookupSectionName/enum` includes `skills`.
- Same operation `/responses/200/content/application~1json/schema/$ref` references `TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___`.
- `/components/schemas/TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___/properties/data/additionalProperties/items/$ref` references `ManagedResourceCatalogItem`.
- `/components/schemas/ManagedResourceCatalogItem/required` is `["code","display_name"]`; `/properties/sort_order/default` is 0 and `/properties/is_active/default` is true.

The generic map has no declared zone key. No zone-named schema/path exists in the current document. Schema defaults do not prove actual zone availability, returned active flags or inclusion of linked inactive entries. Inactive codes can already be represented by DomainResponse: displaying a returned code need not await a directory containing that code. Rich labels and selection eligibility do require a concrete source contract.

### E4 — Baseline and bounded ownership

`openspec/specs/skill-domain-management/spec.md:25`: “Зоны SHALL соответствовать `authenticated` и `anonymous`.” This fixes baseline selection scope, but does not say both values must always be selected. The same paragraph defers additional normalization/uniqueness/unpublished restrictions and forbids invented preflight or demo-derived blockers.

Lines 9–21 require server-backed display/counts and error distinction; 32–35 preserve input and known-field/general error handling; 42–54 require PUT, expected_version, Idempotency-Key and safe retries; 56–59 preserve keyboard cancellation/accessibility. A PATCH route or optional update property does not supersede baseline PUT semantics.

Discovery supports only “no relevant active continuation found in these artifacts,” not universal absence of work or an assigned owner. The capability owner is a proposed routing role; MOS-1306 is a backend dependency, not a frontend task assignment.

## Finding dispositions

| Finding in reviewed report | Disposition | Reason / correction |
|---|---|---|
| Wire widening; arbitrary-string business acceptance not established (lines 22–36) | **accept** | E1/E2 independently confirm every cited branch and business limitation. Reject any free-text eligibility interpretation. |
| MOS-1306 compatibility, validation, sorting/count integrity and atomicity (38–50) | **accept** | E2 supplies explicit requirements, not runtime completion. No further product decision is needed to record these as source-backed planning facts. |
| Generic lookup exists but zone evidence missing (52–62) | **revise** | Core gap accepted. Separate unknown concrete key/response/selection behavior from already-known domain read behavior. Lookup inactive inclusion and rich labels are not prerequisites to retaining an inactive code returned by DomainResponse. Error payload confirmation gates exact mapping, not preserved-input/general-error acceptance. |
| No active continuation / owner handoff (5, 18, 79) | **accept**, bounded | E4 discovery supports no locator found; capability-owner handoff remains a proposal, not named ownership or proof no external plan exists. |
| Fixed baseline vs directory evolution (83) | **revise** | Keep fixed-code baseline and do not activate additional choices. Recording backend directory-backed eligibility and schema evolution is a safe evidence correction now; it does not require approving a frontend directory-driven selector. |
| Inactive read versus unchanged update (84) | **accept** | Read retention is explicit. Broad inactive rejection and preservation of unchanged links do not establish a grandfathered resubmission exception. Reject assumed successful round trip, silent stripping, automatic reassignment, or assumed omission/null workaround. Clarification gates only update behavior, not read planning. |
| Representation compatibility versus schema enum removal (85) | **accept** | E1/E2 describe different contracts; neither proves deployed runtime widening. |
| Preserved approved deferrals (86) | **accept** | E4: no reopening normalization/uniqueness, auth or unrelated product scope. |

## Candidate delta dispositions

These dispositions approve or revise audit/planning recommendations only, not implementation or main-spec edits.

| Candidate / baseline locator | Disposition | Safe planning correction versus remaining decision |
|---|---|---|
| Read/list inactive retention, ordering, unique domains and unchanged skills_count; spec 9–21 / report 72 | **accept** | Record now from E2; directory discovery is not a prerequisite. Preserve server counts/order, not client joins. Runtime compliance remains unverified. |
| Replace fixed choices with active directory assignment; spec 23–30 / report 73 | **revise** | Record nonempty/unique/existing/active backend rules now. Dynamic selection, additional codes and replacement of baseline wording require owner-approved continuation and concrete lookup contract. “Preserve seeded codes” means compatibility, not forcing future inactive values to remain selectable. |
| Explicit zone rejection / input preservation; spec 32–35 / report 74 | **accept** | No product blocker to drafting known rejection cases with preserved input/general errors. Do not prescribe exact business-error envelope or frontend-only enforcement without evidence. |
| Zone-directory loading/empty/error/retry; spec 37–40 / report 75 | **revise** | Valid conditional candidate for a future directory selector, not an existing CRUD dependency. Do not block current fixed-code CRUD merely because a new lookup is unconfirmed. Source-specific behavior remains unresolved. |
| Existing inactive edit and unchanged-zone round trip; spec 42–54 / report 76 | **revise** | Split accepted read/visible-value/no-loss failure cases from unresolved mutation acceptance. Reject a successful unchanged-inactive round-trip assertion until backend semantics are confirmed. Preserve PUT/concurrency/idempotency baseline; do not substitute PATCH or omission by inference. |
| Retain keyboard/accessibility guarantees; spec 56–59 / report 77 | **accept** | Existing baseline obligation, not new scope or a decision blocker. |

## Architecture

Backend normalization preserves a list-of-codes DTO while separating stored links from active assignment eligibility. Current schemas can carry broader codes; the baseline still fixes selection to two values. A possible generic lookup is a separate dependency for future selection/labels, not proof of a zone endpoint and not a prerequisite for truthful display of returned codes.

## Start Here

Use `openspec/specs/skill-domain-management/spec.md:23–44` with E2's validation/read statements. First split the continuation backlog into (a) source-backed read/validation/no-loss planning corrections and (b) conditional directory selection and inactive-update decisions. Do not defer all corrections behind a new product approval and do not activate new scope through this audit.

## Validation and residual risks

Local read-only JSON parsing compared both contracts and traversed lookup references; targeted filesystem discovery verified the bounded active-plan claim. No network, MCP, browser, tests, generation, application inspection, nested agents or source/spec edits. Only this review was written. Saved source status does not prove deployment or successful migration. Directory payload, inactive-update acceptance and actual business errors remain unverified; metadata digests were not independently checked in this review.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent primary-source comparison with exact pointers/quotes, bounded discovery, and accept/revise/reject treatment of findings and all six candidate deltas."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-DOMAIN-ZONES.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read-only Python JSON comparison and lookup traversal","result":"passed","summary":"Confirmed four string branches, removed enum, unchanged required/null structure and untyped zone lookup key."},
    {"command":"Targeted find and Python active Markdown scan","result":"passed","summary":"85 non-archive/non-audit Markdown files; zero relevant zone references with word-bounded Russian search."},
    {"command":"tests / generation / network / browser","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Core scenario evidence accepted; directory/read and planning/activation gates require narrow revision."],
  "residualRisks": ["Concrete zone lookup payload and inactive-update semantics unresolved.","Saved contract/Jira are not deployment or test-completion evidence.","Active-plan absence is bounded to inspected local artifacts; no named owner established."],
  "noStagedFiles": true,
  "diffSummary": "Only authoritative review report written; no source/spec modifications or staging performed.",
  "reviewFindings": ["revise: avoid blocking established read and validation planning on future directory decisions.","reject: arbitrary-string selection, guaranteed inactive round trip, or automatic scope activation."],
  "manualNotes": "Read-only independent review; index state not inspected. No infrastructure/input blocker. Product decisions separated from safe evidence corrections."
}
```
