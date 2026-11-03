# Code Context

Parent revision following R-SPEC-G2-MOS-1257 REVISE: mandatory scope limited to omission preservation/after-trim precision and consistent distinct-count/parsed-segment wording. Repeated existing test families, quoted-comma/no-null examples and separate scenario layout are optional throughout, not acceptance blockers. Original external report and REVISE retained; no fresh independent ACCEPT claimed.

## Result

**SPEC-G2-MOS-1257: keep the existing name-string/no-code decision; make bounded completeness corrections, not a new product gate.** All two owning requirements, two scenarios and five numbered tasks are joined below. The accepted 20 requirements are accounted for without re-extraction. The plan explicitly settles the wire/CRUD part of Q1257-01; it does **not** explicitly settle per-field versus aggregate counting or detailed normalization mechanics. Proposal/design/task wording omits the accepted **after-trim** qualifier and omitted-field preservation. These are precise documentary gaps, not evidence of absent runtime behavior.

`O` = `openspec/changes/mos-1257-feedback-labels`; `C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `C/audit`. These abbreviations expand literally throughout. `Rnn` = `REQ-G2-MOS-1257-nn`; `Wnn` = corresponding accepted wiki clause. Parent retains acceptance/publication authority; no approvals or execution inferred.

## Files Retrieved

Full semantic reads:

1. `O/proposal.md:1–34`, `O/design.md:1–53`, `O/tasks.md:1–10`, `O/specs/feedback-labels/spec.md:1–25`: complete owning plan; all discovered delta specs (one).
2. `A/reports/REQ-G2-MOS-1257.md:1–135`, `A/reviews/R-REQ-G2-MOS-1257.md:1–61`: accepted requirement extraction and complete independent review (review read to EOF).
3. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`: governing process.
4. `A/work-items/G2-FEEDBACK-SPEC-WAVE.md:1–25`; `A/decisions.md:1–9`: assignment and D-064 acceptance, not full decision history.

Bounded primary-source / dependency reads:

5. `A/sources/jira-feedback/r1/content.json:77–85`, JSON `/items/8`: complete assigned issue, read by decoded JSON extraction. Description at line84 includes all six AC.
6. `A/sources/wiki-247734813/r1/content.json#/text`: decoded zero-based half-open Unicode-character slices `[3844:4893]`, `[7848:8140]`, `[9598:11134]`, `[20813:22292]`. Prototype/code discrepancy, prototype limitations and dynamic-label model/examples only; no links followed.
7. `openspec/changes/mos-1249-feedback-api/design.md:5–30`: explicit delegated sources/precedence seam from O/design:7. Scoped grep additionally returned lines35–51 (some long lines truncated; not relied on as full clauses). Scoped label/limit search of its `specs/feedback-api/spec.md` returned no matches; not a full semantic read of that spec, nor an API audit.
8. `openspec/changes/mos-1251-feedback-editor/tasks.md:1–7`: only foundation 1.1–1.4 and downstream composition 1.5, to verify O/proposal:32 and O/design:21 dependency seam.

Path discovery: `find` under O found one delta capability; `find **/feedback-labels/*` under `openspec/specs` returned no files. Main capability absence is **not** nonimplementation. No archive, application code, runtime contracts, HTML/PDF attachment, or broader neighboring plan inspected. Hashing entire files is not a claim of semantic reading beyond these limits.

## Key Code — exact plan joins (no application-code audit)

### Owning requirements and scenarios

| Owning item / exact locator | Accepted joins | Disposition and precise evidence |
|---|---|---|
| **Free survey labels**, `O/specs/feedback-labels/spec.md:7–11` | R01, R05–07, R09–14, R16–17, R20; normalization supported by R15 | **Keep**, with precision corrections below. Line9 explicitly forbids API-code generation and separate CRUD, uses name strings, distinct-100, 150, 16000, comma separator, empty-string clear/no null and canonical result. Line11 preserves saved labels on audience change and requires nonempty segment labels. R08 omission is absent; R12 after-trim is absent. R06 quote behavior is implied by “always separator” but deserves an explicit boundary example. R14 should name parsed `segments`, not potentially any label field. |
| **Canonical labels and clearing**, `O/specs/feedback-labels/spec.md:13–16` | R04, R07, R10, R15–16 | **Keep** exact association lifecycle. The sample backend transforms casing/duplicates, then clearing sends `""` at subsequent save. It does not specify a general client canonicalization algorithm or globally delete labels. Add separate omission-vs-clear/no-null example for R08–09; do not replace this scenario. |
| **Accessible labels interactions**, `O/specs/feedback-labels/spec.md:18–20` | R02–03, R18–19 (partial: accessible errors are not themselves input retention) | **Keep**. Extra explicit existing local rules: accessible names/errors, predictable focus, narrow layout, task-local acceptance and no simulated API success. These are existing plan/project safeguards, not new Jira rows; provenance O/design:35–37, O/proposal:10,24,32 and supplied AGENTS accessibility/test policy. No new independent approval asserted. Input retention is explicit in proposal:10/tasks:3, not in this SHALL. |
| **Keyboard and narrow layout within this task**, `O/specs/feedback-labels/spec.md:22–25` | R02–03; R19 verification framework, plus preceding local accessibility rule | **Keep**. Keyboard/error access, no overlapping controls and focus return on existing-dialog close. Does not require creating a dialog or testing neighboring features. Add/remove actions are explicit in task1.1 rather than individually named here. |

### Every numbered owning task (all historically `[ ]`, unchanged)

| Task / exact locator | Accepted joins / local safeguard | Disposition |
|---|---|---|
| **1.1**, `O/tasks.md:3` | R01–03, R05–07, R11–13, R18; R19 length/empty/keyboard verification | **Keep + precise correction:** add R08 omitted-field preservation, R09 no-null case, explicit quote-not-escape case R06, “100 distinct” and “150 after trim”, and parsed nonempty `segments` check R14. Do not silently pick per-field/aggregate scope. Foundation task1.1 is a start prerequisite; whole-change foundation1.1–1.4 remains as proposal/design states. |
| **1.2**, `O/tasks.md:4` | R07, R10, R15–17, R19–20 | **Keep** canonical response, duplicate/case response normalization, audience preservation, association-only clearing and no global requests. Together with design:29 this is save-time association editing, not independent persistence. Do not upgrade “исходные связи” into a new promise about all unsaved pending edits. |
| **2.1**, `O/tasks.md:8` | R02–03, R19 plus FSD/public API/declaration placement/accessibility/security/mock safeguards | **Keep:** tasks1.1–1.2 already distribute all J-AC6 checks. Repeating their list or adding a cross-reference in2.1 is optional. Add bounded omission/trim verification with substantive corrections; quoted-comma/no-null examples and standalone scenarios are optional precision. |
| **2.2**, `O/tasks.md:9` | R19 indirectly; locally required honest verification commands and conditional API/build checks | **Keep**. No application commands run in this documentary assignment. Checkbox is planning evidence only. |
| **2.3**, `O/tasks.md:10` | R07, R10, R15–16; existing release-evidence safeguard O/design:49,53 | **Keep open**. API canonicalization/clear evidence is explicitly a pre-release condition, not proof of implementation and not a newly imposed product approval. No HTTP verification performed. |

### Proposal/design completeness and ownership

- `O/proposal.md:9–14,20` covers R01/R05/R16/R18/R20 and defers separate registries/general dictionary editor. `:24,34` preserves auth boundaries and excludes targeting execution/real-response collection. **Keep**, no scope expansion.
- `O/design.md:29` is the exact name-string/no-code, association-save, empty/no-null, backend trim/case-insensitive dedupe/canonical response decision (R04–07/R09–13/R15–16/R20). **Correct only omissions:** “100 distinct” (already explicit in delta), “150 after trim” (J-AC4), omitted field preserves prior associations (J-AC3). Numeric count unit/scope remains unproven.
- `O/design.md:21–25,35–37` owns private chip inputs with the editor draft, entity boundary and existing framework/security/verification conventions. Generic question-order and dictionary guidance at `:25,31,43` does not assign label ordering, renderer or dictionary management to MOS-1257. **Keep ownership**; no new label catalog work.
- R04 single save has an **existing exact cross-plan join**, not a gap needing new label persistence: O/design:29 says association changes at survey save; O/proposal:32 assigns composition after MOS-1257 to MOS-1251. `openspec/changes/mos-1251-feedback-editor/tasks.md:7` task1.5 explicitly integrates labels into one card payload/GET. Its foundation1.2 (`:4`) already preserves hidden links and requires segments; foundation1.4 (`:6`) handles submit/baseline/errors without input loss. Do not move those shared responsibilities or demand closure of all MOS-1251 before this task starts.
- `O/design.md:41–53` retains HTML/API boundary, concurrency/error/provenance risks and release verification. Its “no blocking product decisions” statement is not evidence settling every count/Unicode/blank-token detail, nor assurance of deployed API.

Coverage check: R01–07 and R09–20 have explicit owning or foundation/composition plan joins above, with noted precision/test gaps. **R08 has no explicit owning-plan clause**; foundation generic save does not prove omission semantics. No accepted row is silently dropped.

## Existing-plan resolutions, not a second requirement inventory

### Q1257-01: name strings versus prototype codes — resolved in existing plan for the contract

Accepted source anchors: Jira `/items/8/description` J-D and J-AC2 (`content.json:84`); wiki W-UI `/text[3844:4893]`, W-PROT `[7848:8140]`, W-DRAFT `[9598:10514]` retain code display/generation/code-array examples. These remain documented conflicting source presentations.

However `O/design.md:29` explicitly says **“Wire — строка имён через запятую, не массив codes/UUID”** and the delta `:9` expressly forbids generating API codes. Tasks1.1–1.2 implement that choice. The linked API design `:7–10` records the user-agreed boundary “UI by prototype, operations by API, unsupported deferred” and identifies HTML as composition/scenario guidance, not API contract. This is an existing documented local decision, not a new inferred Jira-over-wiki precedence rule. **Keep/no new approval question for name-string/no-generated-code/no-CRUD behavior.** We did not independently audit the underlying approval conversation or published wire contract.

Prototype selected/unselected chips, suggestions and example names are separate **presentation possibilities**. W08 explicitly calls values prototype examples (`/text[21401:22292]`); no owning SHALL/task requires catalog lookup, suggestion service, defaults, code display or code generation. Optional suggestions using already available names could be a compatible UI refinement, **not** an approved new capability. Do not make suggestions mandatory, create a catalog/API, or require a new product gate merely because the freeform UI does not reproduce every prototype chip. If a future proposal depends on those added behaviors, decide only that bounded addition then.

### Q1257-02: model identifiers — retained documentary inconsistency, not a MOS-1257 blocker

Accepted report W05–06/Q1257-02 retains UUID/code-PK and dictionary terminology inconsistency. Name-only transport and association-only editing are already explicit in O/design:29/spec:9. **Keep boundary/no model repair**, no invented UUID payload or global lifecycle operations. Detailed model source slices were not re-read in this unit; accepted report/review carry that finding.

### Q1257-03: normalization limit scopes — partially explicit, not fully resolved

J-AC4 gives 100 **distinct** labels, 150 name characters **after trim**, 16000 **input** characters and nonempty parsed segments. Delta:9 explicitly preserves distinct count and input-string domain; design:29 assigns trim/dedupe to backend. These are not a combined card budget stated anywhere in the owning plan, but neither is per-field counting explicitly stated. **Do not label either interpretation approved.**

Safe documentary corrections now: retain distinct qualifier throughout; add after-trim qualifier; keep 16000 described as input-string length (not normalized output length); add parsed `segments` nonempty case and explicit quote separator boundary. Do not implement truncation, silent token dropping or client dedupe to “make limits fit.”

Remaining bounded contract precision: whether 100/16000 apply independently per field, when input length is measured, character-count convention, and blank-token treatment. No explicit answer in the fully read owner or the bounded foundation seams. Recommend carrying these as **contract-verification details before implementation of their boundary tests**, using the already planned MOS-1249 contract/runtime-validation seam (O/design:7,23,44,53), not reopening the whole product scope. This unit does not declare API sources missing or exhausted; no new source collection was authorized. If that later contract check still cannot settle an implementation-dependent branch, ask only that bounded question then. No blocking decision was needed to complete this comparison.

### Q1257-04/05: canonical state and evidence limits

Backend trim/case-insensitive dedupe and replacement by canonical response are explicit (design:29; spec:9,13–16; task1.2). **Keep** backend as normalization authority; do not infer Unicode algorithm, spelling selection/order or client normalization equality. Spec:11/task1.2 explicitly preserve saved associations on audience switching, while proposal:10/task1.1 preserve failed input. Foundation tasks1.2/1.4 confirm hidden-link and error-state handling, not every unsaved-draft restoration policy. Do not invent destructive hidden-field cleanup or a blanket new draft-state promise.

Omitted-field preservation is different from audience preservation: add an explicit omission-versus-empty/no-null scenario from J-AC3. Partial success/concurrency/retry precision is not answered by label examples; owner already retains baseline/unknown-outcome/no-blind-retry at design:42 and delegates shared submit to MOS-1251. Flattened wiki and missing comments/attachments remain unavailable evidence, not requirements gaps. Prototype in-memory limitation W09 must not replace the existing backend/persistence plan.

## Recommended bounded publication package (subject to review)

1. **Keep** proposal, scopes, canonical-response scenario, accessibility scenario, ownership and all unchecked statuses. No new change/capability needed.
2. **Correct** O/design:29 and O/specs/feedback-labels/spec.md:9 with omitted-field preservation and “150 after trim”; align design/task count wording to “100 distinct.” Explicit quote wording is optional precision: the existing always-separator rule already covers it. No per-field assumption.
3. **Clarify** spec:11 to require at least one parsed segment label for `audience_type=segment`; add bounded omission/trim verification without prescribing a standalone scenario. Separate quoted-comma/no-null scenarios are optional; do not specify unknown blank-token/Unicode behavior.
4. **Align** task1.1 with substantive omission/trim corrections. Existing tasks already cover all five J-AC6 families; repeating them in2.1 is optional. Leave tasks1.2/2.2/2.3 intact except optional exact source joins. No commands or tasks marked complete.
5. Preserve the limit-scope/algorithm questions as narrow unresolved contract details; do not claim they are existing approved answers, demand mandatory catalogs, or erect an automatic new product gate.

## Architecture

Private chip controls → MOS-1251-owned draft/single card save → name strings through entity contract boundary → backend normalization → canonical saved representation. Removal affects survey associations only. This is planned architecture, not runtime verification. Start prerequisites and final editor composition are separate; permissions/transport remain shared existing mechanisms.

## Start Here

Open `openspec/changes/mos-1257-feedback-labels/specs/feedback-labels/spec.md:7–16`, then compare `design.md:29` and `tasks.md:3–4` with Jira J-AC3/4 at the saved source line84. This gives the smallest actionable omission/trim correction while preserving the already explicit name-string decision.

## SHA-256 — complete file bytes

| Input | SHA-256 |
|---|---|
| A/reports/REQ-G2-MOS-1257.md | `bab215846ec9451dfe979865097509f2b5adce9cfd683d454bf63047e8d9979d` |
| A/reviews/R-REQ-G2-MOS-1257.md | `229921653804c9db48f6dd8b67a034252402adaf2546fe07df6789b2187a05fe` |
| A/sources/jira-feedback/r1/content.json | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| A/sources/wiki-247734813/r1/content.json | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |
| O/proposal.md | `00fef67d22a0c465537f081c16948042d0980641198736d52f3e855780a60846` |
| O/design.md | `696819963b5df1695641c2fdf0ee6849591ca103b97eeb23e0375aaae062a585` |
| O/tasks.md | `173a3d33a3242cd2a4cf1540f3fd6f89c027182359f46045f909966955925899` |
| O/specs/feedback-labels/spec.md | `7b3704e24f3f64ac9d5d08e20a152bfd245c3b02585c87a5a91e5b641060e24c` |
| C/proposal.md | `1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879` |
| C/design.md | `632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828` |
| C/tasks.md | `a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83` |
| C/specs/control-center-backlog-reconciliation/spec.md | `a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36` |
| A/work-items/G2-FEEDBACK-SPEC-WAVE.md | `e48969c1d6c09998909c400db7cb138839cf384cb3d8e6595c9e1e4e35e6419e` |
| A/decisions.md | `759351a44478a4e1874d75acb71c8efccd753c388e3fe5d363fc9aaccb488ff7` |
| openspec/changes/mos-1249-feedback-api/design.md | `0b15bcebfea15e35aca35a90c835a00efd892bb9a962fc16401892ca6017d91d` |
| openspec/changes/mos-1249-feedback-api/specs/feedback-api/spec.md (search only) | `a783836ee1f191457d5331e87e2befaf809740fe39125ab302457645b9a591a3` |
| openspec/changes/mos-1251-feedback-editor/tasks.md | `67f76db911e4bd852d2dfa4d24d5bcd64e57aacb8693a586210c340c803f1906` |

Report hash matches accepted review; source hashes match values recorded in accepted report/review. Metadata was not independently re-read in this unit. Full-byte hashes establish the inspected revision, not live freshness.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Compared full owner proposal/design/tasks/delta; joined both requirements, both scenarios and all five unchecked tasks to accepted requirements and existing safeguards; isolated exact omission/trim corrections and unresolved limit precision."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/1dbb628d-48b0-499e-8f9a-50c0b1fe5378/SPEC-G2-MOS-1257.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only find/read/grep, nl -ba and Python JSON slicing/SHA-256","result":"passed","summary":"Full owning plan and accepted report/review compared; exact primary slices and bounded dependency seams inspected; hashes recorded."},
    {"command":"Tests/build/typegen/browser/network","result":"not-run","summary":"Forbidden for this read-only documentary assignment."}
  ],
  "validationOutput": ["Two requirements, two scenarios, five tasks joined; all 20 accepted requirement IDs accounted for.","Name-string/no-code decision explicit; per-field versus aggregate limits not explicitly settled; omission and after-trim wording need correction."],
  "residualRisks": ["Limit scope, character counting, raw-input measurement and blank-token mechanics remain unresolved by inspected plan; no independent API conclusion.","Flattened wiki and uninspected attachments/comments limit source fidelity.","Independent review and parent publication acceptance pending; no runtime, API delivery or feature closure claimed."],
  "noStagedFiles": true,
  "diffSummary": "External analytical artifact only; no repository writes or staging operations.",
  "reviewFindings": ["Keep existing name-string/no-generated-code/no-CRUD contract.","Correct omission preservation and after-trim precision; retain bounded contract questions without inventing product approval."],
  "manualNotes": "Read-only documentary comparison only. Existing plan decisions distinguished from compatible UI refinements and unknown contract mechanics; all owner checkboxes remain historical unchecked evidence. Parent integrates after independent review."
}
```
