# Code Context

Parent revision following R-SPEC-G2-MOS-1254 REVISE: classification corrections only; original review and external author artifact retained. Serialization/identity restatements, endpoint/dependency annotations, edit-only/reorder-deletion and cancellation fixtures are optional refinements throughout this report, not publication prerequisites. Required narrow findings remain active-only new selection and nested409/422 specificity; Q1/method authority stay unresolved. No fresh independent ACCEPT claimed.

## Result — SPEC-G2-MOS-1254

**Keep the existing owner and most behavior; recommend narrow planning corrections, not a new change or checklist closure. Q1 remains unresolved even after full owning-plan inspection.** The plan explicitly preserves nested identity/order, confirms option-losing type changes, retains inactive/unknown codes and separates preview ownership. It does not explicitly decide what happens to nonempty options attached to an unknown type. It also narrows active-only selection to new-question creation and lacks an explicit nested 409/422 question/option scenario. PATCH in accepted Jira requirements versus PUT in plans is a recorded contract discrepancy, not permission to replace either method.

All five owner tasks remain `[ ]`. This is documentary coverage only: no runtime, API correctness, implementation absence, deployment, product approval or delivery conclusion. Independent review and parent integration remain outstanding.

## Files Retrieved

Exact path aliases used throughout (suffixes expand literally):
- `C` = `openspec/changes/reconcile-control-center-backlog`
- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `O` = `openspec/changes/mos-1254-feedback-questions`
- `E` = `openspec/changes/mos-1251-feedback-editor`
- `R` = `A/reports/REQ-G2-MOS-1254.md`; numeric IDs below mean `REQ-G2-MOS-1254-NN`.

Complete reads:
1. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108` — governing process, evidence/authority separation.
2. `A/work-items/G2-FEEDBACK-SPEC-WAVE.md:1–25` — common contract and assigned unit; other unit headings incidentally returned, not executed.
3. `R:1–133`, `A/reviews/R-REQ-G2-MOS-1254.md:1–66` — accepted extraction and ACCEPT recommendation; complete 34-row baseline and Q1.
4. `O/proposal.md:1–34`, `O/design.md:1–53`, `O/tasks.md:1–10`, `O/specs/feedback-questions/spec.md:1–30`, `O/.openspec.yaml:1–2` — entire owning change, including its only delta spec.

Bounded source/seam reads:
5. `A/sources/jira-feedback/r1/content.json:50–58`, especially line 57 `/items/5/description` — all seven AC and dependency/API description. `J.ACn` below is the nth saved ordered acceptance bullet; `J.D2` is the API paragraph.
6. `E/design.md:29–37`, `E/tasks.md:3–7` — full lines for parent draft, shared serialization, errors, active lookup selection and composition dependency.
7. Targeted grep in `E/*.md` (recursive matching included its delta) for `отмен|409|422|неизвест|options|потер|PUT|PATCH`, context 1, limit 35: returned excerpts from `E/tasks.md:3–8,11–14`, `E/design.md:28–38,44–46,50–56,65–69`, `E/specs/feedback-editor/spec.md:8–14,26–33,50–52,58–66,73–76`. Some long lines truncated; no conclusion depends on omitted text. This was a dependency-seam check, not an adjacent-plan audit. In particular, disabled-status cancellation at `E/specs/feedback-editor/spec.md:13,27–28` is not question-type cancellation.
8. `find` of `openspec/specs/**/spec.md` returned 40 main capability paths, none `feedback-questions`; no corresponding main spec to read. This absence is not nonimplementation. Owner discovery returned the four Markdown documents and metadata above.

Wiki content was **hashed only**, not independently reread; W references below are to accepted report rows/locators, not fresh source extraction. No MOS-1249 plan, API contract, archive, application source or tests were read. Project instructions were supplied in context.

## Key Code — exact owning scenario/task joins

This is a planning-artifact matrix, not application code. `S` = `O/specs/feedback-questions/spec.md`, `D` = `O/design.md`, `T` = `O/tasks.md`, `P` = `O/proposal.md`. “Existing local rule” means explicit plan/project text; it does **not** manufacture a separate approval receipt. Common safety/FSD/testing rules also appear in supplied `AGENTS.md`.

### Every owning requirement and scenario

| Owning locator / exact item | Accepted joins | Disposition and task join |
|---|---|---|
| S:7–9, **Stable questions and options**, editing/types/collections | 04–14, 16–20; R:54–70; W02–W04 at R:95–97 | Keep: all seven codes, editable title/type/required, question/option add/delete, both reorder methods and exact caps/string ranges are explicit. T:3 (1.1) covers editing/limits; T:4 (1.2) reorder. Editable option text is supported by “constructor questions/options” plus option text validation and accepted W02; a clearer task assertion is compatible, not a new approval gate. |
| S:9, same requirement, non-tags options and destructive confirmation | 15,18; R:65,68; J.AC2–3 | Keep outbound exclusion and confirmation; D:29 states other types contain no options, stronger than merely not sending them. No explicit unknown-options exception or cancel/restore policy. Q1 and compatible cancel refinement below; T:3 (1.1). |
| S:11, same requirement, final array/UUID/no new ID/no sort_order | 21–24; R:71–74; J.AC4 | Structural coverage good; D:31 also excludes FK/local keys and timestamps, says new IDs come from backend and array order is authoritative. Spec itself omits FK/local keys. Optional traceability only: those exclusions may be repeated in S:11/T:4; existing design already covers them and duplication is not required. Method mismatch unresolved; T:4 (1.2), T:10 (2.3). |
| S:11, same requirement, inactive/unknown type and preview limit | 25–29; R:75–79; J.AC5 | Keep existing inactive edit/reorder, unknown code retention and preview explanation (D:29 explicitly warning/no interactive preview). **Narrowed 27:** forbidding inactive only when creating questions does not explicitly forbid switching an existing question to another inactive code. E:design:37 already says new references active-only; propagate precisely, no new product gate. T:3 (1.1). Q1 is not resolved by preserving the code. |
| S:13–16, **Reorder without identity loss** | 09,16–17,19–24,30–31,34; R:59,66–74,80–84 | Keep combined existing/new/deleted fixture for both nested collections and GET result. This scenario covers reorder identity, deletion/new-element serialization and returned composition/order; keyboard is requirement-level, not a specified trigger here. D:31 also preserves UUID on edit. T:4 (1.2), T:8–10 (2.1–2.3). Recommend explicit edit-without-reorder identity assertion in 1.2 test description, not new semantics. PUT discrepancy retained. |
| S:18–21, **Empty tag options** | 14,34; related 33, R:64,83–84 | Keep local validation, nearby error and input retention; T:3 (1.1), T:8 (2.1). This is **not** full coverage of nested server 409/422 (32–33): no response status or option-level address appears. Add separate server-error scenario rather than mislabel this one. |
| S:23–25, **Accessible questions interactions** | 19–20,32–34 partially; R:69–70,82–84; existing local safety/accessibility rules P:10, D:23–25,35–37 | Keep keyboard, names/errors/focus, narrow layout, own-scope acceptance and no successful unavailable-API stubs. General accessible errors do not specify nested 409/422 placement. Narrow layout/focus are existing local plan commitments consistent with supplied accessibility rules, not new Jira requirements. T:8 (2.1). |
| S:27–30, **Keyboard and narrow layout within this task** | 19–20; supporting 34; existing local rule S:25 | Keep actions/errors accessible, no control overlap, dialog close returns focus. T:4 (1.2), T:8 (2.1). Focus return does **not** define whether cancelling destructive type change preserves type/options. |

### Every numbered task (historical status preserved)

| Task and exact locator | Accepted joins / local rule | Disposition |
|---|---|---|
| **[ ] 1.1**, T:3 | 01,03–15,18,25–29,34; W02–W04; no unsafe HTML D:23 and supplied safety rules | Keep scope and tests. Type edit is explicit in S:9 even though task shorthand says “seven types/title/required.” Clarify active-only **any new selection**, non-tags outbound policy and Q1 boundary. It names foundation task 1.1 while P:32/D:21 name foundation 1.1–1.4: this is staging shorthand, not evidence of a cycle; annotate UI construction uses 1.1 and save/error integration uses 1.4, without requiring all MOS-1251 closed. |
| **[ ] 1.2**, T:4 | 02,09,16–17,19–24,30–31,34 | Keep array/order/UUID/new/deleted and GET checks; optionally make existing question **and option** edit/exclusion assertions explicit; these semantics are already covered, not missing obligations. Method is disputed, no method replacement authorized. |
| **[ ] 2.1**, T:8 | 19–20,32–34 partly; D:23,25,35–37 and supplied project FSD/safety rules | Keep unit/component/diff review and browser prohibition. Name nested 409/422 mapping/input tests explicitly, including post-reorder/deletion boundary, instead of relying on generic “errors.” |
| **[ ] 2.2**, T:9 | 34 through test command; remaining typecheck/lint/format/conditional API/build checks are existing project verification rules, not extra Jira product requirements | Keep/no-op; no checks executed here and no checkbox closure. |
| **[ ] 2.3**, T:10 | 02,21–24,30–31; D:49 existing release evidence rule | Keep existing pre-release save→GET/UUID gate open. Record POST/PUT vs accepted POST/PATCH discrepancy for API lane. Do not add a new gate or infer real API delivery from this task. |

### Remaining proposal/design joins (no requirement left orphaned)

- **01–03:** P:28–32 and D:19–23 explicitly place private nested editor with parent draft and MOS-1249/MOS-1251; E:tasks:7 (1.5) composes one save after MOS-1254. D:31 and T:10 describe parent serialization/save. The owner does not spell out `/catalogs/lookups/feedback` or the survey path; accepted J.D2 / R:52–53 do. Minimal traceability improvement: name the existing lookup/parent API seam in D:19–23, referencing MOS-1249, without creating question transport. No new endpoint is inferred.
- **32–33:** P:10 already preserves input on errors; S:21 preserves local input and S:25 gives general accessible errors. D:44 mentions checking actual error envelope at integration. E:design:35 and E:tasks:6 (1.4) explicitly preserve draft and focus errors across tabs. These settle general retention/parent ownership, **not** mapping both nested statuses to the appropriate question/option. Add the local scenario/1.2 or 2.1 assertions below; do not duplicate parent submit.
- **34:** T:3–4 and T:8–9 cover unit/component reorder, new/deleted element, empty tags, limits and general errors. The required nested-error specificity remains underdescribed; no claim tests exist or passed.
- P:14,20,24,34; D:11–13,23–25,35–37,41–49 preserve existing scope, ownership, security, framework reuse, no real responses/unknown renderer, no false deployment evidence and release/rollback policy. These are existing local boundaries/technical rules, not newly extracted Jira obligations. W01/W05–W07 examples do not mandate contenteditable, exact colors, toast duration or append controls. W09/W10 persisted columns do not override outbound exclusions. W12–W14 remain preview/parent-flow context, not real-answer scope expansion.

## Existing-plan resolutions and precise recommendations

### 1. Q1: unknown type with nonempty options — genuinely unresolved

Accepted question: **If an existing unknown type has nonempty options, should saving preserve opaque options, omit them, or block save?** R:119–125; review confirms this bounded uncertainty (`A/reviews/R-REQ-G2-MOS-1254.md:23–25`). Direct source: J.AC2 versus J.AC5 at saved Jira line 57.

Owning clauses do not explicitly settle it:
- D:29: “другие типы не содержат вариантов”; unknown backend type “сохраняется без подмены”.
- S:9: other types “MUST NOT отправлять непустые options”; S:11 preserves unknown type without substitution.
- D:43: unknown/inactive codes → “сохранить исходные данные”, no defaults over saved values.
- D:31/S:11 require full nested replacement with stable existing IDs; they do not define opaque-option serialization exceptions.

These are competing constraints for this corner case, not explicit permission to silently discard options, preserve them on wire, or block save. Neither code retention nor renderer deferral answers nested-data handling. D:53's general “no blocking product decisions” assertion is not a case-specific resolution. Recommend parent retain this exception in that assertion/open-questions section pending an actual accepted ruling. Do not rewrite known non-tags policy or invent a preservation exception.

Supervisor was consulted in this run and directed completion with Q1 unresolved, no expanded collection; parent will check accepted rulings/API evidence and seek explicit user semantics only if still needed. This is coordination, **not product approval** and not a blanket implementation/release block added by this report.

### 2. Inactive selection — existing parent plan already answers the broader rule

25–26 are explicit and unchanged. For 27, D:29/S:11 only prohibit creation with inactive type; J.AC5 restricts every new choice. E:design:37 explicitly allows only `is_active=true` for new references and retains old inactive values. Minimal correction: in D:29/S:11 state “new type selection, including changing type on an existing question, is limited to active entries; unchanged saved inactive type remains editable/reorderable.” T:3 should check both existing-retained and existing-switched cases. This carries an already explicit source/parent-plan rule, not a new approval request.

### 3. Confirmation/cancel — distinguish requirement, plan and compatible refinement

18, D:29/S:9/T:3 explicitly require confirmation for option-losing changes. Neither owning scenario/task describes cancel or restoration; S:30 only restores dialog focus. The parent's disabled-status cancel rule (E:tasks:6, E:spec:13,27–28) is a different transition and cannot be silently imported as approved question behavior.

A precise **compatible refinement for review**, not an already approved decision: test that rejection does not commit the destructive type/options mutation and that retained options keep IDs/text/order. Confirmation commits only the agreed transition. Do not require recovery after a confirmed destructive change, a new undo feature, or confirmation on every deletion; none is sourced. Exact transition classification, restoration after acceptance and unknown-options treatment remain unspecified. Q1 needs the bounded semantic decision above; lack of specific cancel copy/key bindings is not automatically another product gate.

### 4. Nested identity/order — keep, tighten verification rather than redesign

D:31 explicitly settles backend-generated IDs for new elements, array-defined order, full nested replacement and forbidden fields. S:13–16 and T:4/T:10 cover reorder/new/deleted/reload. Optional verification/traceability refinement, not a mandatory correction: repeat FK/local-key exclusions and edit-only UUID assertions in S:11/T:4 if useful. D:31 and S:11 already establish the relevant behavior; no requirement must be repeated in every artifact. Keep local UI keys possible internally but excluded from wire; no key algorithm is mandated. Do not add minimum question count, duplicate-text rules, normalization or an omitted-vs-empty policy: none is decided by the inspected owner. These are not automatically blocking questions.

### 5. Nested errors — add exact missing scenario, retain parent submit seam

Add to the owner delta and T:8 (or T:4 verification) a bounded scenario tied to 32–34: **when parent saving returns a nested 409 or 422 for a question or option, show the error at that item, keep all entered draft values, and make it keyboard-accessible through the parent tab/focus mechanism.** Optional compatible test refinement: a reorder/deletion fixture can check that errors are not attached to a different surviving item; this particular fixture is not a separately sourced obligation. Exact backend path grammar, index-vs-ID mapping and missing/deleted-target fallback require API evidence; do not invent a DTO format or addressing algorithm. This is stronger test specification of J.AC6, not proof a runtime error mapper is missing. E:design:35/E:tasks:6 already settle parent retention/focus ownership.

### 6. PATCH versus PUT — preserve discrepancy for authoritative API comparison

J.D2/J.AC4 and 02/21 name POST/PATCH; D:31, S:11,16 and T:10 name PUT/POST→PUT. E:design:33 repeats PUT. The owner D:7 refers source precedence to MOS-1249 but is not itself API evidence establishing an authorized reconciliation. Keep full-array semantics (consistent across both), record the method discrepancy at those exact locators and let the separate authoritative API lane/parent resolve. No plan method replacement is authorized by this report. Do not promote D:3's historical implementation assertion into a current implementation finding.

## Architecture

Documentary flow: MOS-1249 catalog/entity contract → MOS-1251 foundation draft (tasks 1.1–1.4) → private MOS-1254 nested constructor → MOS-1251 composition (1.5) → parent save/GET. Preview remains MOS-1255; unknown-code warning/limited-preview explanation stays a constructor obligation. No new question endpoint, independent persistence, neighbor feature import or response-collection owner is introduced. Identity is nested, array order is authoritative in the plan, and parent errors must reach the correct local item without replacing the draft.

## Start Here

Open `openspec/changes/mos-1254-feedback-questions/specs/feedback-questions/spec.md:7–21` beside `openspec/changes/mos-1254-feedback-questions/design.md:29–43`. Review Q1 without inferring data loss; then apply the inactive-selection/error/serialization recommendations only after independent review. Parent owns publication and approval checks.

## Input SHA-256

Computed locally with `sha256sum`; hashes identify saved bytes, not live freshness or approval. Report hash matches the independently reviewed report hash. Wiki was hash-only as noted above.

| Exact aliased file | SHA-256 |
|---|---|
| R | `764084c9fed0d395911e5ee57198d5a1dc125d667f9f54d98ed9491a11032f92` |
| A/reviews/R-REQ-G2-MOS-1254.md | `cd771780ba1b02e458088bbe5cdef5b1560649f26946b100b0c45dc69947db3d` |
| A/work-items/G2-FEEDBACK-SPEC-WAVE.md | `e48969c1d6c09998909c400db7cb138839cf384cb3d8e6595c9e1e4e35e6419e` |
| O/proposal.md | `87cfa93c0aee962cdc7371784a6e22f37c3d8413f1c9904f05c051112e196e41` |
| O/design.md | `181f2800f8e8f359147ef9c9d3a6eb4f3d4daafa20324dd3b8e1cf0c23d54e10` |
| O/tasks.md | `2920f54aba3994e856679db78d4706c553e7a97be0c17d420643b7f3d72fba65` |
| O/specs/feedback-questions/spec.md | `eeb2d92c74667f09a97d933390176b2771d39a1596a4f0c21cf0e23e39c9d27c` |
| O/.openspec.yaml | `1dfdca412094f24473d8b842866201ec26f200b29b17064b03f1e4982c35a7b9` |
| C/proposal.md | `1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879` |
| C/design.md | `632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828` |
| C/tasks.md | `a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83` |
| C/specs/control-center-backlog-reconciliation/spec.md | `a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36` |
| A/sources/jira-feedback/r1/content.json | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| A/sources/wiki-247734813/r1/content.json | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |
| E/design.md | `dfd986336cf1b687206752fb8d436c162dd2c38e8ba87b807809c1b5fbd9c028` |
| E/tasks.md | `67f76db911e4bd852d2dfa4d24d5bcd64e57aacb8693a586210c340c803f1906` |
| E/specs/feedback-editor/spec.md | `03e584e4c9d6d1d99f9e0949949dce92b1fd1cc83a5378afaf67fe86ba4b31ee` |

## Validation and residual risks

Manual full-owner comparison covers both requirements, all three scenarios, all five numbered tasks and all 34 accepted IDs via grouped joins. No repeated requirement inventory, code/planning edits, source collection, network/browser/business calls, tests/build/typegen or nested agents. Inspection commands succeeded; git tracked status and cached diff were empty at inspection, but ignored OpenSpec files are not certified by git status. Only this external artifact is written. Full source freshness, omitted Jira fields/flattened wiki limits, external approval provenance and authoritative API method/error grammar remain outside scope. Q1 stays unresolved; no automatic product gate or feature-task completion is asserted.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Full owner read; exact joins for both requirements, three scenarios and five unchecked tasks to all 34 accepted IDs; bounded corrections and Q1 retained."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/1dbb628d-48b0-499e-8f9a-50c0b1fe5378/SPEC-G2-MOS-1254.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"find/read/targeted grep and nl/wc inspection","result":"passed","summary":"Complete owner, accepted report/review, governing inputs; bounded parent seam and no feedback-questions main spec."},
    {"command":"sha256sum listed inputs","result":"passed","summary":"17 input hashes recorded; accepted report hash matches review."},
    {"command":"git status --porcelain=v1 --untracked-files=no; git diff --cached --name-only","result":"passed","summary":"No output; no staging or repository writes performed."},
    {"command":"tests/build/typecheck/lint/typegen/browser/network","result":"not-run","summary":"Prohibited or outside this read-only documentary assignment."}
  ],
  "validationOutput": ["Every owner scenario and numbered task mapped; all owner tasks remain unchecked.","Q1 not explicitly settled by existing owner clauses; no preserve/omit/block selection made."],
  "residualRisks": ["Q1 needs parent accepted-ruling check and possibly bounded user decision.","PATCH/PUT and nested error-path grammar require separate authoritative API evidence.","Saved source freshness and approval provenance not independently established; no runtime verification."],
  "noStagedFiles": true,
  "diffSummary": "External findings artifact only; repository unchanged by this agent.",
  "reviewFindings": ["Review recommendations: broaden active-only new selection wording; explicitly specify nested 409/422 placement; optional repetition of already-covered FK/local-key exclusions in verification, not a missing requirement.","Cancel retention is a compatible refinement, not an already approved question-specific decision."],
  "manualNotes": "Supervisor authorized finishing with Q1 unresolved and no expanded collection. Parent owns independent review, authoritative API/approval checks and publication. No implementation or delivery acceptance claimed."
}
```
