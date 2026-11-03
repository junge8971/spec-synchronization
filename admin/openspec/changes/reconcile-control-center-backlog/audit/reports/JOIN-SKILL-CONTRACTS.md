# MOS-701 — bounded backend-contract join

## Result
MOS-701 is attributable to concrete existing domain/catalog/card/connection contracts and frontend consumers, but its complete backend DoD is **not established**. Recommend **U→P for planning attribution only**, retaining explicit contract-completeness questions below; not feature acceptance, backend completion or deployment evidence. No new frontend corrective owner is warranted from this lane. D087's domain read correction is already owned and must not be duplicated.

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Sources are current local saved bytes, not externally refreshed.

Aliases: A=`openspec/changes/reconcile-control-center-backlog/audit`; W=`A/sources/wiki-241097511-readable/r1/readable-text.txt`; S=`A/sources/api-live/r1/content.json`; L=`docs/api/contracts/openapi.json`; E=`app/entities/skill/api`. JSON locators below use object-key notation (path keys literal), avoiding ambiguous flattened line numbers.

## Exact member and evidence reuse
`A/sources/jira-details-MOS-774/r1/content.json:/items/4` is MOS-701, backend task, Review, updated 2026-10-16T19:22:14.826+0800. Its description requires domain model and CRUD/uniqueness or explicit questions; skill search/filter/sort/paging; draft/card questionnaire; connection/auth/parameters; all methods with schemas, requiredness, constraints, request/response/error examples; uniqueness/version/concurrency/idempotency; visibility/permissions/audit-event schemas. Attachments are empty. “Provided prototype” and agreed contract format have no precise locator in this member; do not identify them by inference (accepted `G1-JIRA-DETAIL-DOCUMENT-EDGES.md:110`).

Reused before targeted inspection: `reports/IMPL-SKILL-DOMAINS.md` (complete), `reviews/R-OPTIONAL-DOMAINS-SEVEN.md:1–65`, checkpoint D087; `reports/DELTA-SKILL-LIST-CARD-EXAMPLES.md:1–100`. Reused history report `reports/IMPL-SKILL-AUDIT-HISTORY.md:1–45` for the already-owned audit integration boundary, not another audit-service inspection. Earlier examples are documentary vocabulary, not current wire authority. No reopening of completed optional/domain/token/history/monitoring/export audits.

## Requirement joins

| Exact member clause (`/items/4/description`) | Saved API evidence | Existing owner / actual consumption / written assertions | Disposition |
|---|---|---|---|
| What 1: domain identifier, name, description, owner, API address, work zone | W §§1.1–1.2, lines44–90; S `/components/schemas/DomainResponse` has all these plus team/count/version/dates; saved zones are string arrays, unlike L's SkillZone enum reference | Accepted domain report maps main `skill-domain-management` to archived `2026-10-01-skills-prototype-alignment` tasks9–11 and CRUD client/editor tests. Current `fix-skill-domain-zone-read-compatibility/tasks.md:3–9` explicitly owns response widening, truthful labels and no-loss rejection cases | Covered planning attribution. Reuse D087; no second correction. Fixed selector/directory/inactive-update policy remains separate |
| What 2: domain list/card/create/edit; uniqueness rules or explicit questions | W §§2.1–2.4 defines methods/examples/errors; §1.2 says normalization and system uniqueness are proposed, unconfirmed; §4 repeats questions. S paths `/api/control/api/skills/v1/domains` GET/POST and `…/{domain_id}` GET/PUT/PATCH; CreateDomainRequest required six fields, UpdateDomainRequest requires expected_version≥1 | Same accepted domain implementation report: POST/PUT, stable key, version/422/conflict/no-loss tests; prior PATCH archive wording superseded by PUT archive. D087 explicitly preserves uniqueness/address deferral | Existing owner no-op; MOS701 permits explicit questions for uniqueness, so do not invent constraints or treat all open questions as missing UI |
| What 3: name/identifier search; domain/team/state/attention filters; sort/page | W §2.5 lines431–487 specifies name/id/service_id search, domain/team, sorting and paging, but not status/attention. S `/paths/…/skills/get/parameters` additionally includes status and type_code, limit1–100/offset≥0, free-string sort; no attention-filter parameter in this exact operation | `openspec/specs/skill-catalog-experience/spec.md:37–93` owns supported server selection and gated warning sources. E/skill-registry-client.ts:54–78 sends query/domain/team/type/status/sort/limit/offset and preserves server totals. Test file :27–110 asserts string-status preservation, malformed rejection and mixed-page totals; :113 onward tests request serialization (read through line150 only, so full serialization assertion is not attested here) | Substantial support, not complete MOS701 attention-filter DoD. Preserve existing G1 search/sort/warning clarification; do not locally filter loaded rows or promise undocumented attention semantics |
| What 4: draft/read/edit all questionnaire fields, including zone | W §§1.3,2.6–2.8 documents questionnaire and zones; S CreateSkillRequest/UpdateSkillRequest include code/types/display_version and questionnaire/contact/materials but no zones property; S skill POST description explicitly creates draft and returns ID only, not W's full Skill example | Main `skill-card-editing/spec.md:9–45` owns questionnaire and safe PUT lifecycle. E/skill-creation-client.ts:7–16 POSTs with key and validates ID-only result, matching saved POST description. E/skill-details-client.ts:15–51 validates current detail fields, :53–66 PUTs supplied body with key, :89–94 GETs detail. Its loose schema has no explicit zones validation: not proof zones are rejected or available. E/skill-details-client.test.ts:46–75 asserts PUT body/key retained across manual retry; :113–127 rejects empty success/invalid version/422 | Existing card/registration ownership; retain historical zone wording versus current schema as an explicit contract reconciliation question, not authority to add a new skill-zone write field. No draft-creation runtime test claim from this lane |
| What 5: implementation connection, authorization need, surface-configurable parameters | W §1.5 lines198–213; S and L SkillConnectionSchema and SkillConnectionParameterSchema are structurally equal; auth_required required, parameters carry key/title/type/required/default/options; schema supports select | Main connection owner is already identified by accepted list/card evidence and separate lane MOS1022. E/skill-details-client.ts uses skillConnectionSchema and PUT; test :77–111 asserts connection-only/version body and key, rejects 409/422 and malformed auth_required success DTO | Existing owner no-op here. Do not expand types or confuse business auth_required with administrator session/token issuance. Detailed connection UI belongs to lane4 |
| DoD 1: agreed-format contract, all method schemas/requiredness/constraints/examples/errors | W provides substantial request/response/error examples and requiredness, but §1.2/1.4 constraints expressly proposed. S schemas supply concrete requiredness/types and some bounds; checked paths' structured responses are only success and422, although skill POST/PUT/detail descriptions enumerate additional401/403/404/409/503 semantics. L lacks those richer descriptions | Clients consume typed/runtime-validated subset; above tests assert transport/error handling, not publication completeness. Main catalog/card specs already require contract-backed behavior | **Not demonstrated complete.** Do not report “no error contract”: prose errors exist. Agreed-format provenance, proposed-vs-approved constraints and prose/schema completeness need backend owner confirmation, not a new UI implementation task |
| DoD 2: uniqueness, object version, concurrent conflict, creation idempotency | W §§2.9–2.10 describes version increment,409, same method/URI/body/user replay and changed-body conflict; key-retention duration explicitly delegated. S Update* requires expected_version≥1 and write header UUID; skill PUT description gives atomic409 VERSION_CONFLICT and IDEMPOTENCY_KEY_REUSED | Main card safe lifecycle and accepted domain report already cover this planning. Directly inspected detail tests prove outgoing version/key and preserved retry payload, not backend deduplication. No backend idempotency execution | Substantial documentary support, not backend acceptance. Preserve explicit uniqueness questions rather than invent normalization or replay TTL |
| DoD 3: visibility, permissions, audit-event schemas | W repeatedly delegates visibility/permissions to separate authorization contract and contains no audit-event schema. S skill POST/detail/PUT descriptions explicitly name TSAM.Skill:create/view/update and team visibility/error behavior. Domain methods inspected have security declarations but no descriptions supplying a complete domain visibility/permission matrix. No Audit-named schema found in S; this bounded check is not absence of external audit service | Existing `mos-1031-skill-audit-history` ownership is established by accepted IMPL history report: separate documentary Query API exists, frontend reader gated, no browser event ingestion. UI transport tests cannot prove audit emission or visibility enforcement | **Partial, unresolved cross-contract join.** Need exact backend event codes/payload/actor/entity/version and permission/scope references for these methods; retain history owner and approved session integration, do not invent policy or reopen history audit |

## Minimal planning disposition
1. Parent may replace MOS701's current detail-only U join with P attribution to existing domain/catalog/card/registration/connection owners and this contract-gap note. This is one member attribution, not task checkbox closure or a global progress claim.
2. Suggested exact evidence-register wording (no project edit performed): **“MOS-701: saved wiki and OpenAPI describe domain CRUD, skill list/draft/card and connection schemas; current clients consume the supported subset. Backend DoD remains unverified for agreed-format provenance, approved constraints/uniqueness, attention-filter semantics, skill-zone schema reconciliation, complete method visibility/permission references and audit-event mapping. Reuse D087 domain read owner; retain existing catalog/card/connection/history/auth owners; no frontend feature or deployment acceptance.”**
3. Owner decision, not new feature: ask backend contract owner to identify authoritative publication/approved constraint set and exact cross-contract references. Existing main/archive requirements are not rewritten. No new corrective change proposed: inspected discrepancies either have existing ownership or need source/owner clarification. Separate lanes retain registry UI and connection implementation details.

## Actual inspection and limits
Read exact member via locally saved single-line JSON; complete W readable body (669 lines); parsed only the named S/L operations/schemas and compared their bodies. S is materially different from L (notably domain strings and skill prose); do not call L the current saved backend contract. Full S was not broadly audited. Read two main specs, D087 tasks and the code/test ranges stated above. Tests were read, never run; only request construction/error assertions are directly attested. Domain and history test findings are explicitly reused accepted evidence, not independently rerun/re-read here. Wiki source linkage is documentary reuse, not proof MOS701's unnamed agreed deliverable is that page. No network/browser/tests/build/typegen/credentials/nested agents, source edits or commits. Staged file listing was empty. No external freshness, deployment, authorization enforcement or event-emission guarantee.

## Current-local SHA256
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-SKILL-REMAINING-SEVEN.md`: `0d1083ea677d8b380789a33f5e56cd30357132ee476bd3362dc31243fc89fd59`
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-details-MOS-774/r1/content.json`: `e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208`
- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511-readable/r1/readable-text.txt`: `c6dd8857060fa4e87a7170fb604486d12d03a8e74d1ac24c4704554eba67b2df`
- `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`
- `openspec/changes/reconcile-control-center-backlog/audit/reports/IMPL-SKILL-DOMAINS.md`: `449d1b9b531da58b888483fc3b45f5487f06601b3e0064b2dc1e85d5f78e47a2`
- `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-OPTIONAL-DOMAINS-SEVEN.md`: `89358bd6009f0ca666439097083ff6aa24cd9acb858b7f09a3dc35e47b53a494`
- `openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-SKILL-LIST-CARD-EXAMPLES.md`: `83526a48a1170b1a618e9663f22061164a7ecee08fa0b7faaa45423a3990f8fc`
- `openspec/changes/reconcile-control-center-backlog/audit/reports/IMPL-SKILL-AUDIT-HISTORY.md`: `239467ed1798fe7f63e117f6c5c7ac4b1fbce371216300e562c35d5893601c2d`
- `openspec/changes/reconcile-control-center-backlog/audit/review-checkpoint.md`: `047ee209762a65fcdd675e269b512370594abc279ef83846bb407bb7b4838bd5`
- `docs/api/contracts/openapi.json`: `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7`
- `openspec/specs/skill-card-editing/spec.md`: `4901cf34abc8fd2b196f26f4017805a9281bc3b82a3e5b080942b9abe56c7229`
- `openspec/specs/skill-catalog-experience/spec.md`: `21bff8f61b30215d95b59b0adbb1059ac3b64e80be358fa6bfa64b3e7cbed942`
- `openspec/changes/fix-skill-domain-zone-read-compatibility/tasks.md`: `5d00d6e69c1d754139b1e12bec759dede78c034c643f129f8a4bc12138f93404`
- `app/entities/skill/api/skill-details-client.ts`: `de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6`
- `app/entities/skill/api/skill-registry-client.ts`: `fe22d8076a52c22ea245853b2bbe3f7103a1f515776920a6ecf76b6a6fcd5969`
- `app/entities/skill/api/skill-creation-client.ts`: `11de2641658df55f0dfb519d19c6c7c7f668c7a87c3a52c342159cf5b4953402`
- `app/entities/skill/api/skill-details-client.test.ts`: `4a0f96da35d60b0a958b27b0ebcafd140ab052d1de1078ec629546f154823762`
- `app/entities/skill/api/skill-registry-client.test.ts`: `afafe2c26cee8843d47040e99a701acaf0899d44dc9a662b3417aba8caf5e398`

```acceptance-report
{
  "criteriaSatisfied": [
    {
      "id": "criterion-1",
      "status": "satisfied",
      "evidence": "Exact MOS701 clauses joined to saved wiki/OpenAPI, existing owners, current clients and inspected written assertions; completeness gaps separated from feature acceptance."
    }
  ],
  "changedFiles": [
    "/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/d6423b11-4674-417a-a7c8-0db499c5efc6/join-skill-contracts.md"
  ],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {
      "command": "git rev-parse HEAD; local read/search/JSON comparison/SHA256; git diff --cached --name-only",
      "result": "passed",
      "summary": "Static inspection only; current hashes recorded and staged listing empty."
    },
    {
      "command": "tests/build/browser/network/typegen",
      "result": "not-run",
      "summary": "Prohibited by assignment."
    }
  ],
  "validationOutput": [
    "Existing owner attribution supported; full backend contract DoD not established."
  ],
  "residualRisks": [
    "No runtime/deployment/external freshness evidence.",
    "Agreed deliverable provenance, attention filters, skill-zone reconciliation and cross-contract permissions/audit mappings remain unresolved."
  ],
  "noStagedFiles": true,
  "diffSummary": "Only authoritative external audit artifact written.",
  "reviewFindings": [
    "No duplicate D087 correction; retain backend contract completeness questions without inventing frontend policy."
  ],
  "manualNotes": "Lane2 MOS701 only; parent package review/integration pending. Domain/history assertions explicitly reused rather than independently revalidated."
}
```
