# SKILL-DOMAINS — bounded implementation audit

## Result
HEAD verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches assignment). Existing domain CRUD has mounted implementation and written tests; this is not feature completion, executed-test or deployment evidence. **Necessary correction: attach the concrete read-adapter/label discrepancy below to the existing domain-zone reconciliation handoff, not a duplicate CRUD plan.** Keep fixed selection, uniqueness/address deferrals and PUT/session boundaries unchanged.

## Scenario → implementation → mock/tests → planning
Paths below are repository-relative; named functions/test titles are exact locators.

- **Server registry/count/navigation; main spec `Server-backed domain registry` and its two scenarios:** `app/pages/skills/ui/skills-page.tsx:31–34` mounts `SkillDomainsRegistry`; `app/application/constants/route-access.constants.ts:17` requires domain-view for the tab. `app/widgets/skill-domains-registry/ui/skill-domains-registry.tsx` uses `domain_page`, server pagination/skills_count, separate error/retry and empty display, and clean `/skills?domain_id=<id>` links. `getSkillDomains` in `app/entities/skill-domain/api/skill-domain-client.ts` requests limit 10/offset and validates response; `mocks/domains-skills.mjs#get_domain_list_api_control_api_skills_v1_domains_get` filters before server-style paging. Written `skill-domains-registry.test.tsx` tests “shows server totals, both zones and full long data; links to a clean skills filter”, page/back navigation, error→retry→empty; client tests cover empty pages, detail and invalid counts. Existing archive `2026-10-01-skills-prototype-alignment/tasks.md` 9.1–9.3 already owns these requirements: **no new baseline task**.
- **Create/team/error; main spec `Domain creation form`:** `features/skill-domain-editing/ui/skill-domain-editing.tsx` provides labelled dialog; `skill-domain-form.tsx#SkillDomainForm` submits all six fields, gates on server team options and permissions, checks session owner, guards concurrent submit and closes only after mutation success. `skill-domain-team.tsx` provides unavailable/empty and retry; `model/skill-domain-form-schema.ts` deliberately adds no name/address normalization, URL restriction or uniqueness preflight. `entities/skill-domain/model/use-skill-domains.ts#useSaveSkillDomainMutation` invalidates domain and skill keys. Client POST expects created ID. Mock create validates team, writes domain and updates team relation; it is not backend eligibility evidence. Written editor tests cover required team, POST fields/key, invalidation, team empty/error, double submit and keyboard cancel. Existing archive tasks 10.1–10.2 cover this; 10.3 explicitly remains deferred for additional normalization/uniqueness. **No-op on that deferral; do not reinterpret zones as auth permissions.**
- **Published 422/no-loss:** `handlers/skill-domain-errors.ts#setSkillDomainValidationErrors` maps known body fields and valid zone indices; all loc/msg details remain in summary, unknown paths do not become fields. `skill-domain-form.tsx` preserves values and general fallback. Written `skill-domain-editing.test.tsx` create/edit 422 cases include zones and unknown expected_version, accessible descriptions and stable-key retry; `handlers/skill-domain-errors.test.ts` covers malformed, nested, negative/out-of-range/string zone locations and fallback. This already maps to main `Domain validation failure` and archive task 10.3's explicit intermediate result, not completion of its deferred policy.
- **Version/retry/cancel; main `Version-safe domain editing`:** `skill-domain-editor.tsx#SkillDomainEditor` waits for a detail fetched after mount and snapshots it. Form snapshots draft/version, retains dirty input on refetch, uses stable key for serialized unchanged body/new key after change, and instructs cancel/reopen on conflict rather than automatically changing version. Client `saveSkillDomain` uses PUT, expected_version supplied by form and mandatory key; no PATCH fallback. Mock update checks version before mutation, validates team, increments version; bottom-of-file PUT alias reuses PATCH handler. `mocks/app.mjs:87–89` includes both update methods/create in idempotency dispatch. Written client retry/method tests and editor fresh-version/dirty-refetch/conflict/focus tests cover this. `mocks/put-aliases.test.mjs` domain branch covers missing key, invalid version, replay, changed-body conflict, stale version, GET and preserved PATCH; `mocks/skill-contract-delta.test.mjs:95–113` covers domain update, replay and unknown-team atomic rejection. Archive `2026-10-13-update-control-center-contracts-put` proposal/design/tasks 2.1–2.2, 3.1 and complete domain delta explain PUT superseding older archive tasks 11.1–11.2's PATCH wording. **No archive rewrite or PUT reversal.**

## Concrete zone discrepancy / minimal handoff

Accepted documentary inputs plus their reviews establish string wire representation, known backend nonempty/unique/existing/active assignment rules and retained linked inactive reads, but NOT arbitrary-code selection, directory key, inactive resubmission exception, proposed max-two policy or deployment. No source extraction was repeated.

1. **Read boundary remains closed enum:** `app/entities/skill-domain/api/skill-domain-client.ts:18` validates `zones` as `z.array(z.enum(['authenticated', 'anonymous']))` for both list and detail (and PUT result). Therefore a returned other code causes the entire response to fail validation, rather than truthfully displaying that code. This is a concrete compatibility discrepancy against accepted read/transport reconciliation, conditional on such returned data—not evidence that a third code is currently deployed. Existing client tests cover the two seeded codes and malformed count, not another returned code/inactive history.
2. **Display fallback would mislabel wider reads:** `app/widgets/skill-domains-registry/ui/skill-domains-registry.tsx` zone badge expression `zone === 'authenticated' ? 'Авторизованная' : 'Открытая'` maps every other code to anonymous/open. Currently the enum parser prevents such values reaching it; widening the parser alone would expose this latent misrepresentation. Preserve server ordering and counts; do not invent labels or filter inactive links. Known seeded codes remain displayable regardless of inactivity, but DTO/UI has no inactivity metadata to prove eligibility.
3. **Write/selection is separately fixed:** form schema and `domainZones` selection remain two-code; zones array has no minimum/uniqueness refinement. Mock domain create/update handlers have no directory-backed active/existing/nonempty/duplicate business checks. Do not equate this with approved arbitrary-string acceptance or backend validation completion. Current written editor 422 tests already prove generic rejection presentation only; inspected tests do not establish specific empty/duplicate/inactive/unknown business rejection scenarios. Record these known rejection/no-loss acceptance gaps in the same existing handoff, without choosing frontend enforcement or inventing exact error envelopes.
4. **Unresolved update policy remains unresolved:** form submits full draft including initial zones. Do not silently strip/omit inactive codes, force successful round trip, substitute PATCH or add directory loading as a current CRUD dependency. Confirm intended update semantics and actual directory/error contract before dynamic selector work.

Recommended planning delta is only this implementation/test mapping and read-boundary regression candidate attached to the accepted domain-zone continuation candidate. Prior accepted report's no-active-owner finding remains bounded to its inventory; this audit does not claim universal task absence. Capability-owner/backend clarification remains required for selector expansion and inactive updates; known read/validation/no-loss planning need not wait for it. Main/archived specs and all checkboxes unchanged.

## Authority and current local input hashes
Current local SHA256 only; OpenSpec is Git-ignored, no git-show or historical byte-equality claim. Complete main spec, both relevant archive proposal/design/tasks/domain deltas read; broader archive material was not used for decisions.

`openspec/specs/skill-domain-management/spec.md`: `b5f3ffc7329e9315b94484b0ce0333711634708779cd3b07fba734fdbbb66f25`

Under `openspec/changes/reconcile-control-center-backlog/audit/`:
- `work-items/G2-OPTIONAL-DOMAINS-SEVEN.md`: `9720c147622d55b007071126202799405226f607c8935d431761f980c476e89a`
- `reports/SCENARIO-DOMAIN-ZONES.md`: `69fa428e5903a3412f51effc093537edf17f73f5457882f73c58c8144ecf7b77`
- `reviews/R-DOMAIN-ZONES.md`: `88926fed85c6104f0f865cb672f1a0f609db3c98146d307d7c3edcad369552db`
- `reports/DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md`: `a0aadd6fa2ddf0ef18ab9d53b314a23c397d8dc0ec5e9c812826218d478e9288`
- `reviews/R-DELTA-DOMAIN-ZONES-LINKED-CONTRACT.md`: `82f601ab7de1ecfa165c522ecbe77bb844a1394904be95f89ccd63bb92f0e2b3`

Under `openspec/changes/archive/2026-10-01-skills-prototype-alignment/`:
- `proposal.md`: `f7b33ba61bdc76155bbc19b27b5d2dc9038444839e432939f868a77e841bbe10`
- `design.md`: `f7d7a35a618667b3e1945022610cd3d95e3ae341d84ef889f351ad861aa9e29f`
- `tasks.md`: `fca3825b59ad64394fc0714e8cb22cc3934eb8e2c7ec73bd9c587d393295e1b2`
- `specs/skill-domain-management/spec.md`: `1bd93c7d9f69e900e93c075c4f000ab23eed8229255491065c532cf254e08f2e`

Under `openspec/changes/archive/2026-10-13-update-control-center-contracts-put/`:
- `proposal.md`: `513e4dada738d4fe889144aad9b4f06c796279a0dae251f5b283a47a199f0a3d`
- `design.md`: `1fc1af4a37931abb995788bdb4509d4e1b252b9ba84315f96fe9eb3e729aa4e2`
- `tasks.md`: `98c6c15e913ab1c221493ec8969c76360e65db3189c71e250570bbc2ab2e1c1f`
- `specs/skill-domain-management/spec.md`: `3612df6bbcd87fa8bf802be3935a7b422ac61da1669f6700ac1d66b5767424be`

Reviews' corrections retained: do not block known read/validation planning on lookup approval; linked-report D-002 locator is corrected by its review to decisions.md:25–34, especially 31 (not independently re-read here). No uninspected index attestation: `git diff --cached --name-only` returned empty in this audit.

## Limits
Only mounted domain CRUD and connected tests/mock portions assessed. No skill registry-wide or optional KB/AB audit, no global FSD/session review. Shared transport internals, actual backend responses, migration/inactive fixtures, zone directory contents and deployment unverified. Tests are written and read, never run; archive pass claims are historical documentary statements only. No network/browser/build/typegen/tests/credentials/commits/nested agents or project edits. Only this external report written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped mounted domain CRUD, clients, mocks and written tests to main scenarios and two archived owners; isolated enum-read/label discrepancy and conditional zone gaps with current input hashes."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/50982ca9-1cc4-42f9-b49b-912e0b738c81/impl-skill-domains.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD","result":"passed","summary":"Matches bc0d9800f25a90989b9c73c76f91996f8300f1d3."},
    {"command":"Local read/find/grep and Python SHA256","result":"passed","summary":"Bounded implementation/plan inspection and current local input hashes recorded."},
    {"command":"git diff --cached --name-only","result":"passed","summary":"No staged paths at inspection."},
    {"command":"tests/build/typegen/browser/network","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Two-code runtime read validator and binary zone label differ from accepted wider read reconciliation; no deployed third-code inference."],
  "residualRisks": ["Directory contract and inactive update semantics unresolved.","No execution or deployment verification; coverage absence claims limited to inspected tests."],
  "noStagedFiles": true,
  "diffSummary": "External report only; no project edits or task changes.",
  "reviewFindings": ["Correction: attach read-enum/label and focused regression evidence to existing domain-zone handoff; preserve baseline selection and deferred uniqueness/address policy."],
  "manualNotes": "Read-only bounded lane; historical archive task status is not completion evidence for current runtime. No source re-extraction or other-lane audit."
}
```
