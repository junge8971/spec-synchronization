# Code Context

## Result

**SPEC-G2-MOS-1259: keep owning change; retain PATCH/PUT discrepancy pending authoritative API reconciliation.** Parent revision after R-SPEC-G2-MOS-1259 REVISE: no method or whole-object replacement-semantic change authorized. Expanded fixtures and repeated coverage wording below are optional precision throughout; title wording alignment is supported. Original external report/review retained; no fresh independent ACCEPT claimed. Identity, restoration, separate pagination and incompatible-search handling already have plan answers. No new product gate is warranted. This is documentary comparison, not approval, API verification or delivery acceptance. Parent integrates after independent review.

Literal path aliases:
- `C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `C/audit`.
- `O` = `openspec/changes/mos-1259-feedback-saved-filters`; `S` = `O/specs/feedback-saved-filters/spec.md`.
- `N` = `openspec/changes/mos-1250-feedback-registry`; `F` = `openspec/changes/mos-1249-feedback-api`.
- R01–R24 are the accepted IDs in `A/reports/REQ-G2-MOS-1259.md:43–66`.

## Files Retrieved — actual read set

1. `A/work-items/G2-FEEDBACK-SPEC-WAVE.md:1–25`: complete contract/assignment; only MOS-1259 executed.
2. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`: complete governing artifacts.
3. `A/reports/REQ-G2-MOS-1259.md:1–113`, `A/reviews/R-REQ-G2-MOS-1259.md:1–68`: complete accepted report/review. Report `:36–76` and review `:15–19` reinspected with line verification.
4. `O/proposal.md:1–32`, `O/design.md:1–49`, `O/tasks.md:1–10`, `S:1–28`: complete owning proposal/design/tasks and **all** delta specs (one), including numbered reinspection.
5. `A/sources/jira-feedback/r1/content.json:95–103`, `/items/10/description`: complete assigned record, all six AC and three description paragraphs directly rechecked. Full Jira/wiki content bytes hashed, not fully substantively read. Wiki evidence is attributed to accepted report `:68–74` and review `:18`; no new wiki extraction.
6. Explicit URL seam: `A/reports/REQ-MOS-1250.md:40–75`; `A/reviews/R-MOS-1250.md:20–64` (findings1/6 used; intervening findings visible, not re-audited); scoped grep of `N` for URL/1259/сохран with context1, followed by complete `N/design.md:29–33`. Relevant untruncated grep hits: `N/tasks.md:3–5`, `N/specs/feedback-registry/spec.md:37`, `N/proposal.md:9–10,22–26`. Other matching adjacent lines incidental; no complete neighboring-plan audit.
7. Explicit permission seam: `F/specs/feedback-api/spec.md:26–38`, the requirement and two scenarios linked by `O/design.md:33`.
8. `find` enumerated all paths under `O`; searching `openspec/specs` for `**/feedback-saved-filters/**` found none. Main-capability absence is **not** evidence of nonimplementation. No archive/application/DTO/API-contract inspection.

## Key Code — exhaustive owning requirement/scenario/task joins

“Local rule” means an existing owning-plan safeguard consistent with project instructions, not newly obtained approval.

| Owning item / exact locator | Accepted join | Coverage/disposition |
|---|---|---|
| **Personal saved searches**, `S:7–9` | R01–R07, R10–R11, R13–R18, R21, R23; R08/R09 elaborated in scenario/tasks | Explicit server/resource/name/full search, duplicate titles, selected-ID update, apply offset0, paged list and error/no-fallback. **Retain method discrepancy pending authoritative join** (F1). Optional offset/pagination wording precision (F2); existing coverage is accepted. Backend ownership/equal foreign-missing404 are covered through design/dependency. |
| **Duplicate names**, `S:11–14` | R08, R14–R16 | New ID per creation; only explicit selected-ID action updates. **Keep identity; defer method replacement to authoritative join.** No name-based key, uniqueness or overwrite. |
| **Apply and update complete search**, `S:16–19` | R03–R07, R16–R17, R20 | Two conditions/sort/stored offset40 → all parameters restored at offset0; full update, errors preserve form. **Keep**; explicitly include query, multivalue ordinary filters and nondefault limit in acceptance fixture. |
| **Accessible saved-filters interactions**, `S:21–23` | R19 (no simulated success); local rule `O/proposal.md:10,24,32`, `O/design.md:21,31,33` | Keyboard/names/errors/focus/narrow layout; own UI acceptance; no successful unavailable stubs. **Keep**. Accessibility is not falsely attributed to a Jira row. |
| **Keyboard and narrow layout within this task**, `S:25–28` | Same local accessibility rule; R19 error visibility | Existing-dialog focus return, operable layout/errors. **Keep**; no new dialog or browser test obligation. |
| **Task1.1 `[ ]`**, `O/tasks.md:3` | R01–R13, R16, R19, R23–R24 | Clients/mocks, resource/full search, filter pagination, 201→GET, immutable resource, empty update/null, `/search/...`,404. **Record PUT/PATCH and empty-update terminology discrepancy; do not replace pending authoritative join**. Explicitly preserve limit/offset and reject whitespace-only name. 201/null remain existing contract-check refinements, not independently verified API facts. |
| **Task1.2 `[ ]`**, `O/tasks.md:4` | R08, R14–R18, R21–R24; R03–R07 restoration; R19–R20 through proposal/spec | Explicit create/apply/update/delete with permissions; distinct IDs for equal names; no cross-record update; restoration; no partial stale-schema apply. **Retain method discrepancy**; expanded input/no-false-success fixtures are optional precision. |
| **Task2.1 `[ ]`**, `O/tasks.md:8` | R24 + local FSD/accessibility/security/mock rules `O/design.md:21,31–33` | Review/unit/component, no browser/E2E. Together tasks1.1/1.2 cover all six R24 scenarios after method correction. **Keep**, optionally make six-case join explicit. |
| **Task2.2 `[ ]`**, `O/tasks.md:9` | R24 + existing project validation rule | Conditional API/build checks; honest environment failures. **Keep unchecked**; not run here. |
| **Task2.3 `[ ]`**, `O/tasks.md:10` | R01, R08–R13, R15–R16, R23 + existing release-evidence rule `O/design.md:45,49` | Ownership/pagination/CRUD evidence or stand-owner confirmation; open without evidence. **Keep existing release gate**, not a new product gate. No HTTP checks here. |

All two requirements, three scenarios and five numbered tasks are joined. All owning tasks remain unchecked; no execution inferred.

## Architecture — existing-plan resolutions and corrections

### F1 — concrete plan discrepancy: PUT versus PATCH

R15/R16/R19/R24 and directly inspected `A/sources/jira-feedback/r1/content.json:102`, `/items/10/description`, description paragraph2 and AC3/5/6 explicitly say **PATCH**. `S:9,14`, `O/tasks.md:3–4` say PUT; `O/design.md:27` mentions automatic PUT. The generic source-reference `O/design.md:7` does not resolve this mismatch.

**Conditional reconciliation only:** retain Jira PATCH versus owner PUT. Before changing any method-bearing clause, join authoritative saved-filter API evidence and accepted reconciliation rulings through the API owner. The reviewer additionally inspected F/design:5–23: authority is delegated to OpenAPI/CRUD documentation and the existing shared plan explicitly names published PUT. That is planning evidence, not this report's independent API verification. If authoritative evidence establishes PATCH, update all affected references consistently; otherwise resolve the discrepancy without silent precedence. Preserve selected-ID targeting, complete search, immutable resource and existing whole-object replacement semantics pending that join. No method or semantic rewrite is authorized by accepted Jira extraction alone.

### F2 — identity/full restoration/pagination already answered

- **Identity:** `O/proposal.md:9,14,20`, `O/design.md:27`, `S:9,11–14`, tasks1.1/1.2 distinguish creation from selected-ID update. Equal names produce distinct IDs; GET detail and ID-targeted delete client are planned. Keep R01/R08/R09/R14–R16/R23 without inventing a widget, rename policy or uniqueness rule.
- **Full search:** `S:9,18–19` restores query/ordinary filters/conditions/sort/limit and resets offset0 despite stored offset40. Task1.1 requires full schema. Explicitly name persisted **limit and offset**, plus multivalue ordinary filters, to join R03–R07; never omit stored offset just because applying resets it.
- **Separate lists:** `O/design.md:27` explicitly separates saved-filter pagination from survey pagination; tasks1.1/2.3 verify it. R11 says server pagination. Add “own server pagination, independent of result limit/offset” to `S:9` or task1.1 as precision, not a new feature.
- **Title wording:** `O/design.md:27` says “1–150 непробельных символов,” potentially banning internal spaces. Align to R02 and `S:9`: “1–150 символов и не состоять из пробелов.” Test empty/whitespace/1/150/151; do not invent trimming, Unicode counting or case policy.

### F3 — compatibility policy is an existing refinement, not a new gate

Source-only R18 prohibits unexplained partial application; accepted extraction/review correctly did not select recovery from source alone. Newly inspected plan evidence answers the narrower implementation-policy question:

- `S:9`: stale search **shows an error**, no silent partial application/fallback.
- `O/tasks.md:4`: obsolete schema **is not partially applied** (not just “not silently”).
- Explicit integration seam `N/design.md:33`: damaged saved filter **is not partially applied or automatically rewritten**.
- `O/design.md:39`: retain unknown/inactive originals, no defaults over saved values.

Together these establish existing **error/no-partial-apply** planning policy, compatible with R18; explained partial recovery is not required. This is explicit plan text, **not evidence of a separate user approval**. **Keep**, optionally align `S:9` to task wording and name unsupported parameters as well as stale schema. Do not reopen rejection-versus-recovery as an automatic blocking product question, or invent migration/version fields.

R19–R21 already join `O/proposal.md:10,14`, `S:19,23`, `O/design.md:27`, tasks1.1/1.2: honest error/no stub success, preserve input/form, no localStorage fallback. Refine existing checks so storage failure, `/search/...` validation and empty PATCH each preserve name/search and show no success; incompatible search is not applied. No invented HTTP mapping, retry/undo workflow or offline substitute. `O/design.md:38` already advises preserving baseline, explaining unknown outcome and avoiding blind retries; it does not prove backend concurrency behavior.

### F4 — permission/owner seam already specified

`O/design.md:31–33` links `F/specs/feedback-api/spec.md:26–38`: read uses `TSAM.ManagedResource:read`; personal-filter actions use create/update/delete; backend determines owner; exact action/resource/`*`, session and owner/generation isolation remain. Existing scenarios cover read-only principal and server403; `O/tasks.md:4` owns UI verification. `O/design.md:27` equates foreign/unknown404 without owner speculation, satisfying R12/R13/R22 at plan level.

**Keep mapping**; optionally name action checks/read-only/server denial in task1.2. No fresh role/wildcard decision, client owner authority, request ACL or role-enforced business mocks. Server403 does not justify distinguishing foreign filter404. Existing release task2.3 remains open.

### F5 — actual named URL integration; no ownership transfer

Accepted `REQ-1250-24–28` at `A/reports/REQ-MOS-1250.md:45–49`, ownership `:58`, and accepted review findings1/6 (`:23–31,61–63`) remain the adjacent-owner evidence.

`N/design.md:31–33` actually names **q, repeated status, repeated type, sort, limit, offset, conditions JSON via URLSearchParams**, with one URL↔validated-search conversion for history/copy/**saving**/export. `N/tasks.md:5` plans common search/URL; `N/specs/feedback-registry/spec.md:37` requires complete applied-search restoration, conditions after MOS-1258. `O/design.md:19,21` links prerequisite/public normalized-search entity and prohibits feature-to-feature imports.

**Keep MOS-1250 ownership.** Linking saved-filter restoration acceptance to that shared conversion is a compatible integration clarification, not moving copy-link/URL delivery to MOS-1259. Save/apply consume complete shared search, with apply offset0. Selected-ID URL encoding/restoration, push-versus-replace, version/migration/concurrency, deletion of active selection remain unspecified. Leave bounded unknowns unless concrete implementation needs a decision; no invented fields or current gates.

### Proposal/design disposition

`O/proposal.md:9–14,20,24,28–32` matches personal-server operations, retained safety, dependencies and exclusions: **keep**. First-stage automatic name overwrite is explicitly excluded by saved Jira description paragraph3, not a generic Jira-over-wiki preference. Keep localStorage fallback excluded. `O/design.md:3` contains a historical implementation assertion; not adopted/validated here. Shared/template text `:21–23` about question movement is not new saved-filter functionality. Risks/release statements `:37–49` remain plan constraints, not proof of API/runtime or separately approved product decisions. No new change or feature-task closure is justified.

## Provenance — computed SHA-256

| Input | SHA-256 |
|---|---|
| `A/reports/REQ-G2-MOS-1259.md` | `b928122009f79f48b4789fadcd476bbd1a8bdf669fc438b4cceacd7b3197bd25` |
| `A/reviews/R-REQ-G2-MOS-1259.md` | `b0287c540b7222d1860f90a72e396960f645d184a12a3f82e8b6cc76d01bbbc2` |
| `O/proposal.md` | `c955adf218151450f06e1260040fd65dff6cf8905ca49eb2720b8d5908da983b` |
| `O/design.md` | `ffd8b183f81be81aee20d199b76cc7ad73ad196b604a41ead9d56019778b8e08` |
| `O/tasks.md` | `029e84d2fb5fad51da26bf567325709055405101a5c91cebddbf9159f04b3b5a` |
| `S` | `4e9aee0264a677b7dd13a6d4a3bb2eb2bd648b52be1b877a19e86bc33e36655f` |
| `A/sources/jira-feedback/r1/content.json` | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| `A/sources/wiki-247734813/r1/content.json` | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |

Source/report hashes match accepted review records; metadata not independently reread. Hashing packets is not full substantive reading/live freshness. Omitted Jira comments/attachments/custom fields, flattened wiki and unread prototype limitations remain.

## Start Here

Open `O/tasks.md:3–4` with `S:9–19` and saved Jira `/items/10/description`. Resolve method authority before any PUT/PATCH edit; preserve selected-ID identity, whole-object semantics, complete search and no-partial-apply policy. Expanded acceptance fixtures are optional, not missing requirements. No repository edits made.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Complete owner compared against accepted 24-row report/review; exact joins for both requirements, all three scenarios and five unchecked tasks; corrections and existing-plan resolutions documented."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/1dbb628d-48b0-499e-8f9a-50c0b1fe5378/SPEC-G2-MOS-1259.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find/scoped grep; nl/wc; sha256sum","result":"passed","summary":"Owner/governing artifacts and bounded seams read; line ranges and input hashes inspected."},{"command":"Tests/build/typegen/network/browser/business calls","result":"not-run","summary":"Prohibited by read-only documentary scope."}],
  "validationOutput": ["All owning scenarios/tasks joined; main feedback-saved-filters capability not found in scoped path discovery.","PUT/PATCH discrepancy confirmed; existing compatibility policy and named common URL conversion found."],
  "residualRisks": ["Independent review/parent integration pending; no API/runtime delivery or new approval inferred.","Source completeness/live freshness limited; selected-ID URL mechanics and concurrency remain unspecified, not new gates."],
  "noStagedFiles": false,
  "diffSummary": "Only configured external findings artifact written; no repository edits.",
  "reviewFindings": ["Retain method discrepancy; replacement conditional on authoritative API/accepted-ruling join, not authorized now.","Keep identity/restoration, compatibility and permission policy, URL ownership and first-stage overwrite exclusion."],
  "manualNotes": "No tests or nested agents. All feature tasks remain unchecked. Index state not inspected; noStagedFiles=false does not assert staged changes. Recommendations await independent review."
}
```
