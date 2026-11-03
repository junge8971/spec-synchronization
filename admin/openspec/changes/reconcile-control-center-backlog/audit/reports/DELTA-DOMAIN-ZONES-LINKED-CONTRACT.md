# Code Context

## Result

**REVISE evidence inventory narrowly; ESCALATE source reconciliation; no material delta to D-002's accepted read/validation rules or unresolved activation gates.** The newly available page explicitly retains a two-value enum and proposes 1–2 unique zones. It does **not** identify a zone lookup key, inactive inclusion policy, or unchanged-inactive update exception. Its PATCH-only description does not authorize replacing the established PUT workflow. Record these differences without choosing source precedence or asserting deployment.

## Files Retrieved

All paths below share `openspec/changes/reconcile-control-center-backlog/audit/`. JSON pointers and headings identify selected content precisely.

1. `work-items/DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md` (lines 1–13): bounded assignment.
2. `sources/wiki-241097511/r2/content.json` (lines 1–49; `/bodyView` at line 39), `metadata.json` (lines 1–51), `attachments.json` (line 1): new primary source and provenance. HTML parsed inertly; only domain sections, directory reference and relevant open questions analyzed.
3. `reports/SCENARIO-DOMAIN-ZONES.md` (lines 1–115), `reviews/R-DOMAIN-ZONES.md` (lines 1–122): established findings and mandatory corrections; no repeated implementation/active-plan audit.
4. `decisions.md` (lines 21–30, D-002): accepted disposition and no activation.
5. `sources/api-live/r1/content.json` (line 1): selected domain and directory schema/operation branches below.
6. `sources/jira-api-delta-scenarios/r1/content.json` (lines 24–40, `/items/1` only): MOS-1306 validation/read rules checked directly.

### Provenance verified

Content SHA-256 independently matches both supplied digest and metadata `/sha256`: `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47`; size 73058 bytes matches `/bytes`. Content and metadata `/version/number` are **6**, with `/version/when` `2026-10-13T17:56:19.256+08:00`; saved retrieval is `2026-10-16T12:37:03.295Z`, status 200. These are page revision/capture facts, not semantic contract version or backend availability.

`/bodyView`, heading **Общая информация**, says **v1.0**. Heading **3. История версий** lists v1.1 (14.09.2026, owner model/working-zone type clarification) and v1.0 (11.09.2026). Preserve this internal labeling discrepancy; neither label automatically supersedes another source. Attachment capture digest independently matches metadata `/attachments/sha256` (`dce4311f74a29968dec10bca60a9caa34892ddc093647a099efe9a893d121812`); `/data/results` is empty, `/data/size` 0. This proves only this saved listing, not absence of attachments elsewhere. Prior r1 access failure remains preserved; successful r2 availability does not explain the earlier 404.

## Key Code / bounded evidence and dispositions

### 1. Enum and proposed bound: new reconciliation evidence, not restored wire restrictions

New wiki `/bodyView`:

- **1.1 Модель домена**: `zones` is required `array[Zone]`, “Одна или несколько рабочих зон”. It enumerates `authenticated` (authorized user) and `anonymous` (without user authorization), then states: “Zone является enum. Массив zones может содержать только перечисленные значения.” It immediately qualifies: “Термин и окончательный справочник зон требуют подтверждения в открытых вопросах.”
- **1.2 Ограничения домена**, table headed **Предлагаемое ограничение**, zones row: “От 1 до 2 уникальных значений из справочника”. This is proposed wording, not a newly approved maximum-two policy.
- **4. Открытые вопросы**: “Утвердить справочники рабочих зон, типов навыка и версий стандартного контракта.”

Current API exact pointers independently checked:

- `/components/schemas/CreateDomainRequest/properties/zones/items` and `/components/schemas/DomainResponse/properties/zones/items`: `{"type":"string"}`.
- `/components/schemas/UpdateDomainRequest/properties/zones/anyOf/0/items`: same string item, with nullable alternative; `/required` contains only `expected_version`.
- `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2`: optional `zone`; `/schema/anyOf/0` is string.

These branches do not impose enum/minItems/maxItems/uniqueItems. Existing reviewed historical widening remains accepted, not re-audited here. Wiki fixed enum differs from present transport expressiveness; it echoes the already-recorded fixed-code baseline rather than proving rollback. MOS-1306 `/items/1/description`, **Валидация**, independently requires nonempty, unique, existing `skill_zones` codes, active-only assignment and unknown/inactive rejection. Its **Справочник зон** names the two codes as initial values, not the only possible future directory values. Thus there is a fixed-enum/proposed-cap versus directory-evolution reconciliation issue, **not proof that a third code is currently accepted**. Do not import the proposed maximum-two bound or arbitrary-string assignment into UI policy.

**Disposition: REVISE inventory / ESCALATE reconciliation.** Known backend validation can still be recorded now under D-002. Dynamic selection/additional codes remain unapproved.

### 2. Directory discovery: a named catalog route, but no zone collection

Wiki `/bodyView`, **1.3 Модель навыка**, only the directory-reference paragraph: “Получить справочники навыка: GET /api/control/api/skills/v1/catalogs”; the following sentence identifies `skill_types` as the type directory's response field. This is **not** a zone key. No broader skill behavior was analyzed.

Relevant API reference traversal:

- `/paths/~1api~1control~1api~1skills~1v1~1catalogs/get/responses/200/content/application~1json/schema/$ref` → `TsamResponseSchema_SkillCatalogsResponse_`.
- `/components/schemas/TsamResponseSchema_SkillCatalogsResponse_/properties/data/$ref` → `SkillCatalogsResponse`.
- `/components/schemas/SkillCatalogsResponse/properties` declares only `skill_types`, `training_states`, `autotest_states`; no declared zone field. This is not a claim that undeclared runtime fields are impossible.
- Previously identified generic route `/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get/parameters/0/schema/$ref` → `CatalogLookupSectionName`, whose `/enum` includes `skills`.
- That GET's `/responses/200/content/application~1json/schema/$ref` → `TsamResponseSchema_dict_str__list_ManagedResourceCatalogItem___`; its `/properties/data/additionalProperties/items/$ref` → `ManagedResourceCatalogItem`. `/properties` includes `code`, `display_name`, `sort_order`, `is_active`, but `/required` contains only `code`, `display_name`.

**Disposition: REVISE directory inventory only; no material resolution.** Neither route supplies a declared zone key/inactive-inclusion guarantee in these inputs. `skill_zones` in Jira is a storage directory, not proof of a response key. Generic defaults do not establish runtime eligibility. No invented endpoint/key or new CRUD dependency follows from the linked page.

### 3. Read/list and inactive retention: accepted rules unchanged

Wiki `/bodyView`, **2.1 Получить список доменов** and **2.2 Получить карточку домена**, examples return both known codes; list query table types `zone` as `Zone`. These examples neither discuss nor exclude linked inactive values. They supply no inactive lookup-inclusion or historical-code behavior.

MOS-1306 `/items/1/description`, **Валидация**, explicitly retains already-linked inactive zones on read. **Изменение query repository** requires sorting by `skill_zones.sort_order`, no duplicate domains and correct `skills_count`. New wiki examples do not contradict those rules merely by omitting the inactive case.

**Disposition: NO MATERIAL DELTA.** Preserve returned codes truthfully, including known codes that are inactive; unknown directory key/label availability must not block display. Directory-backed labels/selection and runtime compliance remain separate questions. Do not filter inactive links from read/list or derive counts through client joins.

### 4. Create/update: partial PATCH description does not resolve inactive acceptance

Wiki `/bodyView`, **2.3 Создать домен**, supplies both codes and says all fields are required; **2.4 Изменить домен** documents `PATCH /api/control/api/skills/v1/domains/{domain_id}` and “Тело запроса содержит только изменяемые поля и обязательный expected_version”, with a one-code zones example. It describes a full Domain response and reuses create errors, including 422 validation. There is no inactive exception, null policy or zone-specific business-error mapping.

Current API `/paths/~1api~1control~1api~1skills~1v1~1domains~1{domain_id}/put/requestBody/content/application~1json/schema/$ref` and corresponding `/patch/...` both reference `UpdateDomainRequest`. Optional/nullable zones do not prove mutation semantics. MOS-1306 **Валидация** rejects inactive assignments on create/update, while **Изменение persistence-модели** preserves unchanged links; neither establishes successful resubmission of an unchanged inactive code.

**Disposition: NO MATERIAL DELTA to unresolved acceptance; record PATCH documentation difference.** The wiki proves that it describes partial PATCH, not that PUT is absent or replaceable. Keep D-002/review's established PUT/concurrency/idempotency and no-loss constraints. No forced round trip, silent removal, reassignment, assumed omission/null workaround or PATCH substitution. Generic 422 wording does not settle exact inactive-rejection payloads.

## Architecture

Separate five layers: current transport carries code strings; Jira specifies eligible active directory-backed assignment and retained inactive reads; baseline selection remains fixed per accepted review; directory discovery still lacks a zone key; deployed behavior is unobserved. The newly accessible design page adds fixed-enum/proposed-limit and partial-PATCH documentation to reconcile, not precedence or implementation authority.

## Remaining questions and routing

**Product/planning:** reconcile fixed two-value wording/proposed maximum two with future active-directory selection; decide any selector expansion only through approved continuation. Candidate routing remains the previously established `skill-domain-management` capability-owner role, with MOS-1306 as backend dependency. No named owner or implementation task is established here. Prior no-active-plan finding remains bounded to that audit's inspected artifacts; no rediscovery or universal absence claim.

**Contract/backend:** confirm exact zone lookup endpoint/key/example, active/inactive inclusion and label/order semantics; settle unchanged-inactive submission and omission/null behavior for the intended update method; document zone business-error payloads. Unknown historical values and directory-failure behavior remain open. None of these blocks recording known validation, preserved-input/general-error handling or truthful existing-value display.

**Runtime:** no response observation, migration/test execution or deployment evidence; source chronology/status cannot establish them.

## Start Here

Read `reviews/R-DOMAIN-ZONES.md:79–101` with `decisions.md:21–30`, then new wiki `/bodyView` **1.1**, **1.2**, **2.4**, **4**. Add only this source-reconciliation/directory-inventory delta to the existing candidate handoff. **No activation, implementation, main-spec change, plan creation or task closure is authorized.** Independent review remains pending.

## Validation

Local Python JSON parsing/hash verification and inert HTML extraction only. Initial parser assumed `/body/view/value` and failed with `KeyError: body`; inspecting saved root keys corrected it to `/bodyView`, after which scoped extraction succeeded. No missing-input blocker. No network/browser/MCP, tests/build/generation, code audit, nested delegation, staging or other mutations; sole write is this report. Index state was not inspected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Bounded linked-contract delta with verified hashes, exact headings/pointers, retained D-002 corrections and separated policy/contract/runtime unknowns."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python hash verification and initial HTML extraction","result":"failed","summary":"Both hashes matched; extraction assumed wrong body key and raised KeyError."},
    {"command":"Local Python scoped /bodyView extraction and domain/directory JSON traversal","result":"passed","summary":"Verified enum/proposed limit/PATCH wording; catalogs schema has no declared zone key; MOS-1306 rules preserved."},
    {"command":"tests / build / network / browser","result":"not-run","summary":"Prohibited by bounded assignment."}
  ],
  "validationOutput": ["Content and attachment-list hashes match saved metadata.","New page does not resolve zone lookup or unchanged-inactive update acceptance."],
  "residualRisks": ["Source enum/proposed-limit reconciliation remains undecided; no automatic precedence.","Zone directory payload, inactive update semantics and deployed behavior remain unknown.","Fresh independent review pending; previous active-plan absence remains bounded."],
  "noStagedFiles": true,
  "diffSummary": "Sole bound report written; no product/source edits or activation.",
  "reviewFindings": ["revise: add fixed-enum/proposed-limit and catalog-route evidence without changing accepted read/validation rules."],
  "manualNotes": "Local primary-source inspection only; initial parser failure corrected. No staging performed; index state uninspected. No implementation or task closure."
}
```
