# Code Context

## Result

**REVISE narrowly: substantive delta accepted; provenance attestation and D-002 locator need correction. ESCALATE only the already-unresolved product/contract questions, not known read/validation planning.** No source precedence, activation, implementation, task closure or deployment conclusion follows.

## Files Retrieved

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/` (A). Primary JSON pointers/HTML headings supplement physical lines.

1. `work-items/R-DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md` (1–7) and `work-items/DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md` (1–13): bounded assignment.
2. `reports/DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md` (1–111): report under review.
3. `sources/wiki-241097511/r2/content.json` (1–49; `/bodyView` line 39), `metadata.json` (1–51), `attachments.json` (1): independent byte/hash verification; inert extraction of domain sections, relevant directory paragraph and version/open-question sections.
4. `sources/api-live/r1/content.json` (line 1): independently parsed domain schemas/operations and the two catalog reference chains only.
5. `sources/jira-api-delta-scenarios/r1/content.json` (24–40; `/items/1/description` line 30): saved MOS-1306 validation, persistence, read and query requirements.
6. `reviews/R-DOMAIN-ZONES.md` (1–122): prior corrections, not fresh proof of historical schema or implementation.
7. `decisions.md` (21–38): D-002 begins at 25; domain-zone disposition is at 31 and downstream-use restriction at 34.

## Verified provenance

Independent local SHA-256 calculation:

- Wiki content: **710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47**, **73058 bytes**; matches assignment and metadata `/sha256`, `/bytes`.
- Attachment listing: **dce4311f74a29968dec10bca60a9caa34892ddc093647a099efe9a893d121812**, 372 bytes; matches metadata `/attachments/sha256`. Saved `/data/results` is empty and `/data/size` is 0; no universal attachment-absence claim.
- Content and metadata `/version/number` = **6**, `/version/when` = `2026-10-13T17:56:19.256+08:00`. Metadata `/retrievedAt` = `2026-10-16T12:37:03.295Z`, `/status` = 200. These are saved capture/page revision facts, not independent server observation or semantic approval.
- `/bodyView`, **Общая информация**, labels the contract **v1.0**; **3. История версий** includes **v1.1 / 14.09.2026** and **v1.0 / 11.09.2026**. Report correctly preserves the distinction. Metadata `/priorAttempt` records preserved r1 failure; r1 was not re-opened here, and the earlier 404 cause remains unverified.
- API/Jira contents were independently parsed/read, but their capture hashes were not reverified. Historical schema widening remains prior-reviewed evidence, not a newly repeated comparison.

## Key Code / independent dispositions

### Accept: enum and proposed cap are reconciliation evidence, not approved policy

Wiki `/bodyView`, **1.1 Модель домена** explicitly calls Zone an enum restricted to `authenticated` and `anonymous`, then says the final directory requires confirmation. **1.2 Ограничения домена**, column **Предлагаемое ограничение**, says zones are “От 1 до 2 уникальных значений из справочника”; **4. Открытые вопросы** asks to approve the working-zone directories. Report lines 26–42 correctly distinguish fixed-code wording from a proposed maximum-two constraint.

API `/components/schemas/CreateDomainRequest/properties/zones/items`, `/components/schemas/DomainResponse/properties/zones/items`, and `/components/schemas/UpdateDomainRequest/properties/zones/anyOf/0/items` are all `{"type":"string"}`. Their array branches declare no enum/minItems/maxItems/uniqueItems. Update `/required` is `["expected_version"]` and zones has a null alternative. `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2` is optional `zone` with string/null schema. Transport expressiveness is not assignment eligibility or omission/null semantics.

Jira `/items/1/description`, **Валидация**, requires at least one unique existing active `skill_zones` code and rejects unknown/inactive values on create/update. **Справочник зон** calls the two codes initial values. Neither source proves availability/acceptance of a third code. No arbitrary-string selector or proposed cap is authorized.

### Accept: named catalogs route does not supply a zone key

Wiki `/bodyView`, **1.3 Модель навыка**, paragraph “Получить справочники навыка” names `GET /api/control/api/skills/v1/catalogs`; its `skill_types` response-field statement is about skill types, not zones.

API `/paths/~1api~1control~1api~1skills~1v1~1catalogs/get/responses/200/content/application~1json/schema/$ref` references `TsamResponseSchema_SkillCatalogsResponse_`; `/components/schemas/TsamResponseSchema_SkillCatalogsResponse_/properties/data/$ref` references `SkillCatalogsResponse`. Its `/properties` declares only `skill_types`, `training_states`, `autotest_states`.

Generic `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get/parameters/0/schema/$ref` references `CatalogLookupSectionName` (enum includes `skills`). That operation's 200 JSON schema references `TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___`; its `/properties/data/additionalProperties/items/$ref` references `ManagedResourceCatalogItem`, with required fields only `code`, `display_name`; `sort_order` and `is_active` have defaults 0 and true.

Thus report lines 44–56 correctly identify **missing declared zone key/inclusion guarantees**, not forbidden extra response properties or an impossible zone lookup. Jira's storage table name `skill_zones` cannot be promoted to a response key. Defaults do not prove returned flags or eligibility. No new CRUD dependency follows.

### Accept: inactive reads remain known; mutation acceptance remains unknown

Wiki **2.1 Получить список доменов** and **2.2 Получить карточку домена** return both codes in examples and say nothing about linked inactive retention. Omission of that case is not a prohibition.

Jira **Валидация** explicitly retains already-linked inactive zones on read. **Изменение query repository** requires `skill_zones.sort_order`, no duplicate domains and correct `skills_count`. These facts support report lines 58–64 and D-002 without a directory key: truthful returned-code display and known validation planning must not wait for future labels/selection approval.

Jira **Изменение persistence-модели** requires adding new links, removing absent links, not recreating unchanged links, and atomicity. This persistence requirement does not establish a validation exemption for resubmitting unchanged inactive codes. Report lines 68–72 correctly retain the uncertainty and prohibit forced round trips, silent stripping, reassignment or assumed omission/null workarounds.

### Accept: PATCH documentation is not authority to replace PUT

Wiki **2.4 Изменить домен** documents PATCH, mandatory Idempotency-Key, changed fields plus required `expected_version`, full Domain response and create errors plus version conflict. **2.3 Создать домен** provides generic 422 validation, not exact zone-rejection mapping.

API `/paths/~1api~1control~1api~1skills~1v1~1domains~1{domain_id}/{put|patch}/requestBody/content/application~1json/schema/$ref` references the same `UpdateDomainRequest` for both methods; both operations require Idempotency-Key. The wiki's partial PATCH description neither forbids PUT nor approves switching the prior-reviewed PUT/concurrency/idempotency baseline. D-002 line 31 explicitly prohibits inferred PATCH substitution.

## Necessary corrections

1. **Report line 106: unverified `noStagedFiles:true`.** Lines 92 and 109 explicitly say index state was not inspected. Not staging or writing only one report does not establish an empty index, including pre-existing staged files. Remove the positive attestation or mark index state unverified in an appropriate nullable/omitted representation; do not infer it from read-only intent. This review also did not inspect the index.
2. **Report lines 14 and 88: update D-002 citation.** `decisions.md:21–30` now includes D-003 and the beginning of D-002 but omits the domain-zone rule. Cite **`decisions.md:25–34`, especially 31**. This is a locator correction, not a substantive decision change.

## Architecture

Keep separate: saved wiki design/proposals; current saved API transport; Jira's intended storage/eligibility/read rules; prior-reviewed fixed selector and PUT baseline; unknown deployed behavior. The new page adds enum/proposed-cap and catalogs/PATCH documentation differences but settles none of the lookup or inactive-update gates. Existing auth/mock agreements and normalization/uniqueness deferrals remain untouched; zone authorization terminology is business data, not permission policy. No auth or mock implementation was inspected or authorized.

## Remaining questions and limitations

- Product/contract owners: reconcile fixed enum and proposed cap with directory evolution without assuming source chronology establishes precedence.
- Backend contract: exact zone lookup endpoint/key/example, active/inactive inclusion, labels/order, unchanged-inactive submission and omission/null behavior for the intended method, and zone rejection payloads remain unresolved.
- These questions do not block recording accepted validation/read/no-loss facts. Dynamic selection remains conditional, not activated.
- No fresh implementation, active-plan inventory, historical API comparison, migrations, runtime calls or test execution. Prior ownership/no-active-plan claims remain bounded to the earlier review; no named owner inferred. No input blocker required escalation to the supervisor.
- Only this bound review was written. No network/MCP/browser/tests/build/generation, git mutation, source/product edits or nested agents. Source labels/status do not prove deployment or test completion.

## Start Here

Correct the reviewed report's index attestation and D-002 locator, then consume it with `reviews/R-DOMAIN-ZONES.md:79–101` and `decisions.md:25–34`. Carry only the bounded source-reconciliation delta forward; no task closure or active plan creation is authorized.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent wiki byte/hash and inert body verification, scoped API traversal and MOS-1306 reading support substantive acceptance with two narrow report corrections."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python SHA-256 verification and HTMLParser extraction","result":"passed","summary":"Both wiki hashes match; domain enum/proposed-cap/PATCH, catalog paragraph and version labels verified."},
    {"command":"Local Python scoped API JSON traversal and numbered report inspection","result":"passed","summary":"String schemas, dual update methods, catalog reference chains and report correction locators verified."},
    {"command":"tests / build / network / browser / git index inspection","result":"not-run","summary":"Execution checks excluded by scope; index not inspected."}
  ],
  "validationOutput": ["Substantive findings accepted; report requires index-attestation and D-002 citation corrections."],
  "residualRisks": ["Lookup key/inactive inclusion and unchanged-inactive update semantics unresolved.","API/Jira capture hashes not reverified; no runtime or deployment evidence.","Index state unverified; no noStagedFiles attestation made."],
  "diffSummary":"Sole bound independent review written; no source/product changes.",
  "reviewFindings": ["revise: report line 106 asserts uninspected index state.","revise: report lines 14 and 88 should cite decisions.md:25–34, especially 31.","accept: bounded substantive delta preserves prior read/validation and approval boundaries."],
  "manualNotes":"Fresh local primary-source inspection only. Historical/baseline findings retained as prior-reviewed evidence; no activation, precedence, task closure or deployment inference. noStagedFiles omitted deliberately because index state is unknown."
}
```
