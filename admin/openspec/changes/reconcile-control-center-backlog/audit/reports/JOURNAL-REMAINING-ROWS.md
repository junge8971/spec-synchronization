# Code Context

## Result and boundaries

Exactly **15 documentary units** assessed: row2 bullets 1–13 and rows4/5. Rows1/3 were not reassessed. This is routing evidence for independent review, not implementation authorization, a new change proposal, source precedence, or task closure.

**A** = `openspec/changes/reconcile-control-center-backlog/audit/`. All A-relative paths below resolve under that exact directory. Primary source **J** = `A/sources/wiki-250781168/r1/content.json`, `/bodyView` (line 10) and `/bodyStorage` (line 11). Saved page version **8**, updated `2026-10-08T18:31:40.254+08:00`, retrieved `2026-10-19T08:24:54.988Z`; metadata at adjacent `metadata.json:1–29`. Local SHA-256 recomputation matches `cd74e398e690d48e3da571a6c2adf02d8c755856948d98747b8d447ad628244d`. HTML inspected inertly; no navigation.

### Status and exact locator convention

J has one table. `table/tbody/tr[1]` is its header; **data row2 = tr[3]**, **row4 = tr[5]**, **row5 = tr[6]** (one-based). Content is `td[2]/div`; status is `td[3]/div/p`. Every scoped row is dated 08.10.2026.

Legend: OPEN is a new/unanswered/not-yet-asked question (macro `29045448-b493-4cd2-85c3-8d10ba302ee3`); CLOSED means question closed, answer accepted (`ab39723d-3117-478f-bf10-5a2e2229b5b6`). Waiting, counter-question, decision-awaiting-action and answered-but-needing-resolution are separate legend states. Thus OPEN does not approve every bullet, and CLOSED accepts the recorded answer, not deployed behavior.

Row2 OPEN status macro: `4d92cbf7-88a4-4836-be2f-22c298d019d5`; its introduction attributes the list to **Андрей: Учесть всё**. Row4 CLOSED macro: `309e4f36-c0e6-4979-9077-050d4bcba40a`. Row5 CLOSED macro: `eba3b48d-2e6b-47d4-a2fd-01b2810da831`.

## Files Retrieved

Selected documentary reads only; no application source opened. Line ranges describe substantive evidence consumed, not implementation verification.

1. `A/work-items/JOURNAL-REMAINING-ROWS.md:1–15`; J lines 1–11, scoped body nodes and adjacent metadata: assignment, source and legend.
2. `A/reports/DELTA-MOS-1119.md:1–93`, `A/reviews/R-DELTA-MOS-1119.md:1–74`; `A/reports/DELTA-MOS-1119-TESTPLAN.md:1–95`, `A/reviews/R-DELTA-MOS-1119-TESTPLAN.md:1–90`; `A/decisions.md:57–71`: accepted dictionary/storage evidence and qualifications.
3. `A/reports/SCENARIO-DOMAIN-ZONES.md:20–96`, `A/reviews/R-DOMAIN-ZONES.md:1–103`; `A/reports/DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md:1–92`, `A/reviews/R-DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md:1–82`: domain ownership, transport/storage distinction and unresolved questions.
4. `openspec/specs/skill-domain-management/spec.md:1–59`: current domain baseline.
5. `A/reports/LOCAL-001.md:24–108`, `A/reports/LOCAL-002.md:5–62`: existing capability/change and routing inventories, used as documentary inventories only, not reinspection of their implementation findings.
6. `A/reports/JIRA-MOS-1327.md:1–44`, `A/reports/JIRA-MOS-1403.md:1–29`, `A/reports/JIRA-MOS-624.md:1–65`: dictionary/API membership and coverage gaps. No new issue bodies traversed.
7. `openspec/specs/skill-registration/spec.md:7–25` plus targeted matching lines; `openspec/specs/surface-registration/spec.md:1–65`; targeted clauses `openspec/specs/skill-card-editing/spec.md:34` and `openspec/specs/dialog-selection-builder/spec.md:57–61`: bounded cross-form routing, not a global coverage audit.
8. `A/decisions.md:11–23`: r2 publication acknowledgment and historical API qualification, not fresh API inspection.

## Key Code / owner evidence keys

No code analysis was performed. These keys abbreviate exact documentary ownership anchors in the table:

- **DICT**: `A/reports/JIRA-MOS-1327.md:18–38`: MOS-1321 “Реализовать раздел Справочники”, MOS-1399 “Актуализировать справочники для справочников”, both observed Hold. Exact saved membership: `A/sources/jira-hierarchy/r1/content.json#/results/21/children/{0,1}`; selected index records `A/sources/jira-member-index/r1/content.json#/items/{138,139}`. Descriptions/acceptance/attachments/comments uncollected. This is a module-level routing candidate, not an assigned frontend implementer or proven requirement coverage. `LOCAL-001:34–108` supplies no dedicated active dictionary change in its historical inventory.
- **API**: `A/reports/JIRA-MOS-1403.md:6–29`: MOS-1386 “Реализовать раздел API”, observed Hold, under MOS-1403; saved hierarchy `/results/25/children/0`, member index `/items/145`. Same missing detail fields. `LOCAL-002:50–52` routes other managed resources via documentation; this does not create a dedicated UI owner or prove missing behavior.
- **STORE**: `A/decisions.md:57–71`, `DELTA-MOS-1119:36–55`, `DELTA-MOS-1119-TESTPLAN:45–91`, with reviews `R-DELTA-MOS-1119:40–66`, `R-DELTA-MOS-1119-TESTPLAN:46–53,80–86`. These concern **skill status/transition/history dictionaries**, not the generic dictionary-management UI. Explicit dictionary `updated_at` presence versus absence remains a real, separate source disagreement; table-name flexibility does not resolve it. Seeds are not UI commands; persistence is not a history-query API. MOS-1031 reader gate and disabled restoration questions stay owned there; no duplicate changes.
- **DOMAIN**: `openspec/specs/skill-domain-management/spec.md:23–44`: creation fields `name, description, owner, api_url, team_id, zones`; confirmed creation closes dialog and updates server-backed choices; field/general validation, preserved input, PUT/version/idempotency baseline. No `code` form field or code-generation policy in these clauses. This is bounded planning coverage, not an API absence assertion. Accepted domain reviews retain fixed baseline selection, inactive-code read retention, unresolved lookup/inactive-update semantics and no automatic PATCH substitution (`R-DOMAIN-ZONES:59–90`; linked review `31–61,70–77`). Zone codes are not `skill_domains.code`.
- **FORMS**: existing capability inventory `LOCAL-001:34–79` routes independently to skill-registration, surface-registration, domain management and other form owners; it supplies no global unsaved-state owner. Exact current partial coverage: `openspec/specs/skill-registration/spec.md:9–21` requires confirmation on unfinished departure and field-linked errors, preserving a **four-step** wizard and truthful local recovery. `skill-domain-management/spec.md:32–44,56–59` covers error/input retention and accessible cancellation, not every departure modal. `surface-registration/spec.md:41–59` covers rejection/unknown-outcome preservation, not a universal departure guard. `skill-card-editing/spec.md:34` preserves dirty input on refresh/error; that is not creation-screen coverage. Do not conflate these guarantees.

## Exhaustive disposition table

For JR-02-01…13, exact locator is J `/bodyStorage`, row2 `td[2]/div/ol/li[@data-uuid='<UUID>']` (also list ordinal shown). All have source status **OPEN**, regardless of definite wording. Primary disposition is bold; qualifications form part of it.

| Stable ID / exact list locator | Source statement and qualification | Existing owner evidence and disposition |
|---|---|---|
| **JR-02-01**, li[1], `947a28d2-8e4f-41bd-b08f-c3e0d0f653da` | Sorting must exist on dictionary list. Definite expectation, not specified sort fields/default/order protocol. | **Targeted follow-up needed — DICT.** Record list sorting for existing module review; no exact current owner clause found proving this requirement covered. STORE display order/seeds do not establish registry sorting. Missing clause is a coverage gap, not a behavior defect. |
| **JR-02-02**, li[2], `05d85250-eb7b-41ab-9cb3-5bae518f5742` | Do not insert complex selection/filter conditions; mark the item for future, do not delete it. | **Targeted follow-up needed — DICT.** Preserve explicit current exclusion and future marker in the existing module's requirements reconciliation. No authority to activate complex filters or remove ordinary sorting/search. No matching local owner clause located; do not import dialog/feedback filtering requirements. |
| **JR-02-03**, li[3], `095abdf4-ec4a-4c25-9833-a39540926cd3` | Create in modal, then open card page with checking/additional filling; tabs, not steps. If page size duplicates modal, they *may* not count it as a separate page. | **Targeted follow-up needed — DICT.** Route specific dictionary create→card/tab flow; page-accounting remark is conditional, not a deletion decision. No matching plan clause identified. DOMAIN's close-dialog behavior and FORMS' approved skill wizard concern different entities and are not contradictions or candidates for replacement. |
| **JR-02-04**, li[4], `80191a78-676b-4e06-a2b1-6ed23d20f6ae` | Two distinct service-code error texts: Latin characters and uniqueness. | **Targeted follow-up needed — DICT.** Capture separate error intents, then obtain dictionary code validation/error contract. No exact rule, regex, preflight or uniqueness mechanism established here. DOMAIN explicitly defers unpublished uniqueness constraints; do not apply this dictionary statement to domain name/api_url or infer a new domain code input. |
| **JR-02-05**, li[5], `c1d3bb5e-85d2-4d35-a8ad-546430c3a05b` | Save plus separate activation toggle instead of “save and activate”; **or** dynamic button label; correction wanted for testing. | **Genuine decision question — DICT.** Which offered UI alternative is accepted? Neither alternative is selected by OPEN status or “Учесть всё”. No matching current owner clause settles it. No invented combined save/activation API or test-completion claim. |
| **JR-02-06**, li[6], `d078f531-e37c-4cd7-9004-842f33166f10` | Export selection modal and completion modal. | **Targeted follow-up needed — DICT.** Definite presentation request; payload/content selection, completion meaning and export contract remain unspecified here. Existing report/dialog exports are different modules, not proof this is covered or grounds for a duplicate export change. |
| **JR-02-07**, li[7], `5af4b7ea-0d1f-4411-8d04-7dddd7096fd0` | Top widgets (how many enabled): try adding and see whether approved; no promise it will pass. | **Genuine decision question — DICT.** Experimental proposal, not approved required widgets. Ask whether the experiment was accepted and what metric scope is intended; no result saved in inspected evidence. Do not implement or infer a count endpoint. |
| **JR-02-08**, li[8], `7d1e708d-f8dc-414b-b7c7-e11a013534d1` | Whether developer-entered data counts as storage: take to tomorrow's sync with Ruslan for final decision. | **Genuine decision question — DICT / storage-document owner routing.** Meeting outcome/accounting meaning absent; Ruslan is a named meeting participant, not proof of implementation ownership. STORE's requested schemas/test observations do not answer this accounting question. No new storage policy chosen. |
| **JR-02-09**, li[9], `92875384-d206-4204-b842-2e0432d40e5f` | Discuss dictionary concept, counting and physical storage separately; recommendations may arrive later. | **Genuine decision question — DICT, with STORE as limited comparison.** No final conceptual decision found. Accepted skill dictionary persistence details narrow their own domain only; they neither settle generic dictionary accounting nor authorize a new global storage model. Keep any later recommendations unverified. |
| **JR-02-10**, li[10], `0c3cb1c3-0ce2-4bea-a33d-d508c4b96981` | Target physical DB table names may differ from developers' adopted names. | **Historical clarification — row5 / STORE / DOMAIN.** Consistent with CLOSED JR-05-01; no new naming decision or rename task. Does not waive schema fields/FKs/behavior or resolve STORE's updated_at disagreement; does not permit API/DTO/lookup-key renaming. |
| **JR-02-11**, li[11], `e5f1e5b7-ee61-4ed7-b93c-ec4e772fcdf4` | Add unsaved-data departure modal to all creation screens, “as for dialogs”. | **Targeted follow-up needed — FORMS and DICT/API for their creation screens.** Skill registration already specifies departure confirmation: no-op for that existing requirement, not proof of modal implementation. Remaining cross-form breadth is **unverified**; retain a bounded per-owner coverage check rather than inventing a global owner/change or starting a cross-app code audit. Dialog analogy is source testimony, not fresh verification. Preserve recovery and unknown-outcome safety. |
| **JR-02-12**, li[12], `7803e7a7-db9f-45b0-8ece-46028976fec8` | Check required-field highlighting everywhere; source says stars and validation were found everywhere, but missing fields on another tab are unclear. | **Targeted follow-up needed — FORMS / DICT/API where applicable.** Historical positive observation is not current coverage proof. Route specifically cross-tab error discoverability, not a claim that all required validation is missing. Current skill/domain field-linked error clauses cover part only; no universal other-tab indication clause verified. No new mandatory-field business rules inferred. |
| **JR-02-13**, li[13], `979b7b80-e137-4c6b-82cf-0b32e289e07f` | API creation form has only Save; Disable, Suspend, Export, Save belong only in card. | **Targeted follow-up needed — API.** Definite create/card action distinction; MOS-1386 is existing inventory route, not approved frontend execution owner. Full owner description/current dedicated plan coverage unavailable. No action endpoint, lifecycle policy, permission or deployment inferred from button names. Do not mistake this for feedback API MOS-1249. |

### Closed units

| Stable ID / exact paragraph locator | Attribution / source status | Existing owner evidence and disposition |
|---|---|---|
| **JR-04-01**, J `/bodyStorage`, row4 `td[2]/div/p[2],p[4],p[6]` (speaker paragraphs p[1],p[3],p[5]) | **CLOSED.** Gleb asks whether backend generates required `skill_domains.code` from domain name because prototype lacks input. Andrey says independently generated codes will not match integration, so populate later through integration. Gleb compares `skills.service_id`/UI linking, then says **temporarily generate ourselves while absent from prototype**. | **Historical clarification — DOMAIN, with targeted contract follow-up if this field is pursued.** Preserve both target integration and attributed temporary workaround; CLOSED does not establish an agreed generation algorithm, current backend implementation, permanent auto-generation, or approved new UI field. Current main spec 23–35 lists other fields; accepted zone reports address `zones`, not this domain identifier. No exact current owner artifact covering code provisioning was found: explicit gap. Route to skill-domain-management capability/backend contract roles, not a newly invented task. Do not reopen approved normalization deferrals or use this as evidence that domain APIs lack all code support. |
| **JR-05-01**, J `/bodyStorage`, row5 `td[2]/div/p[2],p[3]` | **CLOSED.** Gleb asks if DB tables must match target model 1:1. Andrey: checked; not necessary, do as convenient, leave as is. | **No-op — accepted physical-name latitude**, corroborating JR-02-10. Existing persistence/document owners retain physical naming decisions; no rename task. STORE's field-level disagreement and DOMAIN's external code/zone contracts remain separate. No API path/property/schema/lookup-key naming change authorized, and no implementation consistency attested. |

## Architecture / preserved approvals and gaps

The journal's generic dictionary UI requests, MOS-1119's skill process dictionaries, domain integration identifier and domain-zone directory are **four different contexts**. Similar words (`code`, activation, dictionary, storage) are not evidence of shared ownership or contract identity. Compare same-layer requirements before alleging disagreement.

Retain D-016/017 unchanged: three approved generic skill transitions, separate dedicated toggle, **13.10.2026 prod→disabled→prod UI** and **09.10.2026 auth approval** are neither reopened nor expanded. Attachment833803 is read as of D-017, not executed; D-016's earlier unread statement stays historical. MOS-1031 Query API gate and unresolved restoration remain intact. The existing direct updated_at disagreement remains an owner question, not resolved by physical naming flexibility.

Retain domain review qualifications: truthful inactive reads and known backend validation planning need not wait for a future directory selector; lookup key/inactive-update semantics remain unresolved; fixed-code baseline and PUT/version/idempotency rules remain. New arbitrary-string selection, proposed maximum-two policy, automatic PATCH replacement and unpublished uniqueness restrictions remain unauthorized.

**Historical API boundary:** reports inspected above refer to saved r1-era publications and their then-current schema chains. `A/decisions.md:11–23` records r2 and accepted targeted status/token deltas. No fresh API scan occurred; this report does not recertify r1 absence claims as current, assert universal absence of dictionary/API endpoints, or equate publication with runtime. Journal naming latitude is not wire-contract authority.

Coverage gaps: dedicated dictionary/API owner requirement bodies and named frontend implementers; accepted choice for save/activation; widget experiment result; storage/accounting meeting/recommendation outcomes; domain code integration/provisioning contract; all-creation departure guards and cross-tab error discoverability. Missing matches are **not proof of missing behavior**. Independent review remains pending. No global task, source status or implementation readiness is closed.

## Start Here

Open `A/reports/JIRA-MOS-1327.md:18–38` alongside the thirteen exact journal UUIDs: it establishes the existing dictionary route and missing detailed coverage without misrouting to MOS-1119. For cross-form follow-up, begin at `openspec/specs/skill-registration/spec.md:9–21` to avoid duplicating already-owned departure confirmation. For domain code, use `openspec/specs/skill-domain-management/spec.md:23–44` with JR-04-01, not the unrelated zone-code selector.

## Validation and limits

Local reads, scoped find/grep, numbered documentary excerpts, inert JSON/HTML parsing and source hash verification only. One broad combined document output was truncated; substantive dictionary documents and relevant domain sections were subsequently retrieved separately. No implementation inspection, network/browser/MCP, tests/builds/generation, nested delegation or product/spec/source edits. Only this bound report was written. No staging performed; repository index state not inspected and no empty-index attestation made.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Exactly fifteen stable documentary units routed with UUID/paragraph locators, OPEN/CLOSED qualifications, accepted dictionary/domain comparisons, existing owner anchors and explicit coverage gaps."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOURNAL-REMAINING-ROWS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Scoped local documentary find/grep/read and numbered excerpts","result":"passed","summary":"Retrieved required accepted evidence, current bounded owner clauses and inventory routing without opening implementation."},
    {"command":"Local Python inert journal JSON/HTML extraction and SHA-256 comparison","result":"passed","summary":"Thirteen list UUIDs plus two closed-row paragraph locators confirmed; saved content hash matches metadata."},
    {"command":"Tests/build/network/browser/implementation audit","result":"not-run","summary":"Excluded by assignment."}
  ],
  "validationOutput": ["15/15 scoped units assessed; rows1/3 not reassessed.","Only designated report artifact written."],
  "residualRisks": ["Independent review pending; no policy or implementation authorization.","Dictionary/API detailed owner requirements and several meeting/experiment outcomes unavailable in inspected evidence.","Cross-form behavior, runtime, current API completeness and index state unverified."],
  "diffSummary":"Bound documentary report only; no source/spec/task changes.",
  "reviewFindings":["No missing-input blocker; unmatched owner clauses explicitly retained as coverage gaps, not defects."],
  "manualNotes":"Historical API evidence remains historical because r2 exists. OPEN alternatives and CLOSED attributed answers preserved. noStagedFiles omitted because index state is unverified. No global completion or new implementation owner inferred."
}
```
