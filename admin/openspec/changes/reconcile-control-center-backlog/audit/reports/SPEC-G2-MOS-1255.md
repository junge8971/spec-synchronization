# Code Context

## Result

**SPEC-G2-MOS-1255 only.** Existing plan substantially covers the accepted preview behavior; no new product approval gate or real-response API work is justified. Recommend one bounded task clarification to preserve the explicit component-test obligation, plus optional scenario precision below. No implementation/API/delivery acceptance. All five owner tasks remain historically **unchecked**. Parent owns independent review and integration.

Locators: `O = openspec/changes/mos-1255-feedback-preview`; `C = openspec/changes/reconcile-control-center-backlog`; `A = C/audit`. All abbreviated paths below expand literally. `Rnn` means accepted `MOS1255-Rnn`, not a new requirement. D-064 (`A/decisions.md:3–11`) accepts the report/review, not delivery or automatic approval of every proposed refinement.

## Files Retrieved

1. `O/proposal.md:1–34`, `O/design.md:1–51`, `O/tasks.md:1–10`, `O/specs/feedback-preview/spec.md:1–28` — complete owner proposal, design, numbered checklist and sole delta capability. `O/.openspec.yaml:1–2` — schema metadata.
2. `A/reports/REQ-G2-MOS-1255.md:1–110` and `A/reviews/R-REQ-G2-MOS-1255.md:1–58` — complete accepted extraction and independent ACCEPT; report requirement rows at40–70, prototype references78–84, uncertainties98–102.
3. `A/work-items/G2-FEEDBACK-SPEC-WAVE.md:1–29` — complete common contract and units; executed only MOS-1255. `A/decisions.md:1–60` — requested bounded read returned D064 and earlier history; only D064 used for this conclusion.
4. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108` — complete governing process, not business requirement re-audit.
5. `A/sources/jira-feedback/r1/content.json:59–67`, `/items/6` — complete MOS-1255 record selectively decoded; description at66, paragraphs D1–D3 and AC1–AC6. `A/sources/wiki-247734813/r1/content.json:8`, `/text[4893:6286]` — only the accepted W.Form slice semantically read (Unicode zero-based, end-exclusive). Whole source bytes parsed/hashed, not other issue bodies/wiki sections reviewed.
6. Path discovery: all files under `O`; `find **/feedback-preview/**` under `openspec/specs` returned none. No main feedback-preview capability found; this is not nonimplementation evidence. No neighbor plans, archives, application code, API contracts or tests read; dependency seam is explicit within owner artifacts and accepted J.D3, so no neighboring expansion was necessary.

HEAD observed: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (assignment reference matches). `git diff --cached --name-only` returned empty; ignored artifacts are identified by hashes, not assumed tracked.

## Key Code — exact plan joins (documentary; no application code)

### Every owner requirement and named scenario

| Owner item / exact locator | Accepted join | Disposition / task join |
|---|---|---|
| **Isolated interactive preview**, `O/specs/feedback-preview/spec.md:7–9`: immediate draft projection | R02–R08 (`report:41–47`); R05 type changes covered jointly by seven renderers and type-change cleanup | Keep. Task1.1; description is explicit in delta although task1.1's abbreviated verification lists title/options/required/order only. |
| Same requirement: interactive seven types / ranges | R09–R15 (`report:48–54`) | Keep. Task1.1; scale and NPS are separate types despite combined spelling `scale/nps`, not one type. |
| Same requirement: separate answers / no server send | R19–R20 (`report:58–59`) | Keep. Tasks1.1,1.2,2.3. Local trial state, not draft mutation or unrelated editor-traffic prohibition. |
| Same requirement: required / valid zero and false / preview feedback | R21–R24 (`report:60–63`) | Keep. Task1.2 + design29; task verification should inherit preview-only feedback, not real saved-response success. |
| Same requirement: Skip reset | R25 (`report:64`) | Keep. Task1.2 + design29. Does not imply navigation, card discard or real skip registration. |
| Same requirement: deletion / changed type / deleted option cleanup | R16–R18 (`report:55–57`) | Keep. Task1.2; only incompatible trial answers mandated to clear. |
| Same requirement: explicit empty/unknown states | R27–R28 (`report:66–67`) | Keep. Task1.1; no substitute renderer, supported further by design41. |
| **Valid zero and negative boolean**, `O/specs/feedback-preview/spec.md:11–14` | R21–R23 + R19–R20 | Exact positive validation/isolation scenario → task1.2, verification2.1/2.3. It tests a scale and false, not explicitly NPS zero or unanswered required failure. Those remain requirement-covered, not separately named scenarios. |
| **Draft changes invalidate preview answers**, `O/specs/feedback-preview/spec.md:16–19` | R16,R18,R08 (and current projection R04–R05) | Exact removal/type-change/order scenario → tasks1.1/1.2. Deleted option R17 is in requirement9 and task1.2, not in this scenario's WHEN. No loss of obligation, no promise to preserve every other trial value. |
| **Accessible preview interactions**, `O/specs/feedback-preview/spec.md:21–23` | R29–R30 (`report:68–69`); R21 error context | Keep. Tasks1.2/2.1. Accessible names/errors and predictable focus are explicit existing local plan refinements, beyond Jira's unenumerated keyboard wording; no claim of separately evidenced product approval. Own-interface acceptance and no fake successful API align with owner scope/safety (`proposal24,30–34; design13,21,33–35`). |
| **Keyboard and narrow layout within this task**, `O/specs/feedback-preview/spec.md:25–28` | R29–R30; local explicit error/focus refinement above | Keep → tasks1.2/2.1. “Existing dialogs” focus return is conditional, not instruction to create a preview modal or audit parent-card exit. |

### Every numbered task (all `[ ]`)

| Owner task / locator | Accepted requirements or identified local rule | Coverage / action |
|---|---|---|
| **1.1**, `O/tasks.md:3` | R02–R15,R19,R26–R28; R01 only composition-context coverage (`proposal28; design23`, private editor preview) | Keep current behavior. R26's visible preview marking is explicit here although delta9 only requires preview-specific submission message. R01 “alongside constructor” is compatible with private draft-owner preview but not stated literally in owner artifacts; optional add “рядом с конструктором” without imposing fixed columns on narrow screens. |
| **1.2**, `O/tasks.md:4` | R16–R25,R29–R30; design29 supplies exact feedback meaning | Keep. Covers zero/false, no draft mutation and no answer send. Type-change cleanup and Skip are explicit behavior though examples are abbreviated. |
| **2.1**, `O/tasks.md:8` | R29–R31 partially; existing local architectural/security verification (`design23,33–35`) | **Precise correction recommended:** explicitly require component coverage of all seven types, required including unanswered and 0/false, draft changes and absence of answer-send requests. Current “targeted unit/component tests” permits unit-only evidence for most of AC6; task2.3 explicitly requires component evidence only for no requests. This is verification traceability precision, not missing runtime behavior. |
| **2.2**, `O/tasks.md:9` | Local project quality/verification rule; not a new Jira functional requirement | Keep. Honest command results, conditional API/build checks; checklist is planned work, not evidence commands ran. No command in this task was executed by this audit. |
| **2.3**, `O/tasks.md:10` | R20,R31; existing local release-evidence rule | Keep. Explicit local-preview component-evidence exception already answers generic HTTP/staging boilerplate in design47,51. Do not require nonexistent response endpoints, invent a new staging dependency, or mark the gate closed. No-requests assertion applies to trial submission, not all editor operations. |

R01–R31 are all joined above; R01 has only contextual placement coverage and R31 has under-explicit suite coverage. These are narrower than a claim that every accepted requirement has a dedicated scenario. Two requirements and all three named scenarios, plus five numbered tasks, are accounted for.

### Proposal/design coverage and existing-plan resolutions

- **Ownership/isolation:** `proposal9,14,20,28–34; design13,19–29` join R01–R25 and J.D1–D3. Draft foundation MOS-1251 and questions MOS-1254 are prerequisites; final MOS-1251 composition explicitly does not block preview. Data remain owned by draft's private editor; entities own domain/API interfaces (`design23,35`). No proposed new feature/store or independent questionnaire save mechanism is needed.
- **Feedback-copy concern is already semantically resolved:** `design29` says submit “сообщает только о проверке предпросмотра”; `delta9` makes preview-specific meaning SHALL. This exactly joins R24/J.AC4 (`J:66`) and is consistent with accepted review9–17 and report98. W.Form's thank-you toast (`W:8 /text[4893:6286]`; report84) is a prototype reference, not established mandatory final copy. **Keep/no-op; no exact-copy approval question.** This identifies explicit plan semantics, not a newly invented product approval or general source precedence.
- **Validation/isolation:** zero/false are explicitly answered in `design29; delta9,11–14; tasks4`; required-unanswered validation remains mandatory by delta9. Whitespace-only text, empty tag details, unknown-required submit policy, success-reset and double-click rules remain unspecified in this owner plan as in report99. Do not turn these into blocking product gates without a concrete implementation conflict. Trial errors need accessible names/errors and predictable focus (`delta23,28; task2.1`), partially resolving source-only accessibility uncertainty, but not prescribing exact placement or first-error focus.
- **Cleanup/reset:** `design29; delta9,16–19; tasks4` explicitly settle deletion, type-change incompatibility and Skip-reset obligations. They do not settle a compatibility matrix, stable trial-answer key algorithm, unaffected-value preservation or parent lifecycle retention (`report100`). Do not equate “incompatible” with clearing all answers; no new preservation guarantee is authorized either. “Смена … вопроса или варианта” in design29 remains qualified by incompatibility; it does not require reset on mere wording edits.
- **Empty/unknown:** explicit states already required (`delta9; task1.1`). `design41` additionally prohibits defaults replacing saved unknown/inactive values and invented renderers. This supports R28 without defining unknown-required submission behavior or proving runtime enforcement.
- **Keyboard/narrow screen:** `delta23,25–28; tasks4,8` already specify accessible errors, focus, nonoverlap and keyboard operation. No breakpoint or forced desktop columns implied. W.Form visual refs V01–V06 (`report78–83`) are not newly mandatory pixel/copy/ARIA requirements. No additional browser-test approval is sought.
- **Scope/safety:** `proposal10,14,24,34; design13,23–25,33–43,47–51` preserve existing framework/FSD/auth/API safeguards and exclude execution of display rules/real response collection. Generic optimistic-locking/DTO/CORS text is shared integration caution, not new preview response operations. The more specific local component evidence in task2.3 avoids a fabricated API-delivery requirement. Historical `design3` statement that implementation is absent was not independently verified here.

### Recommended bounded disposition

1. **Update candidate, not an integrated decision:** clarify task2.1's verification sentence to name AC6's component suite: all seven types, required unanswered versus answered including scale/NPS 0 and boolean false, live draft changes, and no answer-send requests. Source: J.AC6 (`J:66`), R31 (`report70`); existing delta9–19 and tasks1.1/1.2/2.3 supply behavior. Preserve unchecked status and no-browser restriction.
2. **Optional compatible precision, not missing-feature finding:** add named scenarios for (a) option removal cleanup, (b) Skip reset preserving draft/no request, (c) unanswered required versus 0/false with preview-only feedback, and (d) empty/unknown and visible preview mode. Put in the existing delta, not a new change; these restate existing obligations, not new validation policy. Likewise literal alongside-constructor placement in task1.1 would make R01 traceability exact. Parent may retain current compact scenarios and record these joins instead.
3. **Keep/no-op** for preview semantics, current dependencies, no real answer traffic, local evidence gate, unknown-state honesty, and keyboard/narrow layout. No genuinely necessary product question established by this comparison. Unspecified compatibility/validation details remain visible, not silently decided or declared globally resolved.

## Architecture

Requirement-level flow: MOS-1251 foundation draft → MOS-1254 question/options edits → MOS-1255 immediate rendering. Trial input lives separately; trial Submit performs required checking and preview-only feedback, Skip clears trial input, incompatible edits invalidate it. No path from trial answers to real response persistence. This is the documented ownership model, not inspected application data flow.

## Start Here

Open `openspec/changes/mos-1255-feedback-preview/tasks.md:8–10` against accepted `REQ-G2-MOS-1255.md:70`: the only recommended correction is making the component suite explicit, while retaining the already adequate local-preview evidence exception. Then use delta9–28 for scenario precision; do not reopen exact toast copy approval.

## Integrity and validation

SHA-256 locally recomputed over whole files; accepted report hash matches independent review's recorded digest. Source content digests match those in accepted report/review (metadata not freshly reread).

| Input | SHA-256 |
|---|---|
| `A/reports/REQ-G2-MOS-1255.md` | `61207d52e321907edca1799a165a3e26ead9ea9b372395cb7100ffe12e65a065` |
| `A/reviews/R-REQ-G2-MOS-1255.md` | `c76592a768b0a70167499572b97e638e803beca1583866748554e1c441b9a554` |
| `A/work-items/G2-FEEDBACK-SPEC-WAVE.md` | `e48969c1d6c09998909c400db7cb138839cf384cb3d8e6595c9e1e4e35e6419e` |
| `O/proposal.md` | `5dffd3459e0cd0958fcfedc239878faa4e06c5a1f08c55565bcce59b0268e0a1` |
| `O/design.md` | `1d2766da0fa4246267b6a42e35e503788f668eda21b496504ac7e53b66085153` |
| `O/tasks.md` | `311d06349f6bf1781845fe300af6cbb6df900c77120899a673a194c77583b12b` |
| `O/specs/feedback-preview/spec.md` | `8917ec33bc3768a3a0616a95ecd6719894e4bc3f659c87779ce1cde17a132a51` |
| `A/sources/jira-feedback/r1/content.json` | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| `A/sources/wiki-247734813/r1/content.json` | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |

Manual documentary comparison only. No tests/build/typecheck/lint/format/typegen/OpenSpec validation, network/browser, business calls, nested agents, repository edits or staging. Only this configured external artifact written. Retained source extraction limitations (flattened wiki, unread attachment, omitted Jira fields) persist; live freshness and runtime/API/test coverage are unassessed. Independent review and parent publication remain pending.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Compared complete owner artifacts; joined both requirements, all three scenarios and five unchecked tasks to accepted R01–R31; identified bounded component-test wording correction and existing-plan resolutions."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/1dbb628d-48b0-499e-8f9a-50c0b1fe5378/SPEC-G2-MOS-1255.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local file discovery, numbered reads, Python selective JSON decoding and SHA-256 inspection","result":"passed","summary":"Owner files fully read; accepted report/source digests verified against recorded values; no main feedback-preview spec found."},
    {"command":"git rev-parse HEAD; git diff --cached --name-only","result":"passed","summary":"Reference HEAD matches; no staged paths."},
    {"command":"Application tests/build/typecheck/lint/format/typegen and OpenSpec validation","result":"not-run","summary":"Read-only documentary assignment; execution prohibited/not needed for comparison."}
  ],
  "validationOutput": ["2 requirements, 3 named scenarios, 5 unchecked tasks mapped; no task closure or delivery claim."],
  "residualRisks": ["Flattened retained sources and omitted attachment/Jira fields limit completeness; live freshness unverified.","Validation edge policies and trial-state compatibility/lifecycle details remain unspecified, not automatic blockers.","No runtime/API/test coverage assessed; independent review and parent integration pending."],
  "noStagedFiles": true,
  "diffSummary": "External analytical artifact only; repository unchanged.",
  "reviewFindings": ["Recommend explicit AC6 component-suite wording in task2.1; optional scenario/placement precision; no new product gate justified."],
  "manualNotes": "Preview feedback semantics already explicit in design29/delta9; task2.3 already permits local component evidence instead of fabricated answer-API staging evidence. All owner checkbox states preserved."
}
```
