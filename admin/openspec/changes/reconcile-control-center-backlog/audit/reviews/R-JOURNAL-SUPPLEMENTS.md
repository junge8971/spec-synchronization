# R-JOURNAL-SUPPLEMENTS — independent documentary review

## Review

**No issues found.**

| Report | Verdict | Mandatory corrections |
|---|---|---|
| `reports/JOURNAL-FEEDBACK-AUDIENCE.md` | **ACCEPT** | None |
| `reports/JOURNAL-SURFACE-MVP.md` | **ACCEPT** | None |

- **Correct:** Both supplements distinguish historical documentary answers from approved scope, implementation evidence and authorization to change requirements.
- **Fixed:** None; review-only.
- **Merge verdict:** **OK** for documentary acceptance only. Parent remains the acceptance/publication owner.

`A` below means `openspec/changes/reconcile-control-center-backlog/audit`; `M` means `openspec/changes/archive/2026-10-12-mos-914-surface-lifecycle-mvp`.

## Independent verification boundary

Read both supplements and their original analyst work-items; independently compared the first and third journal data rows and legend in `A/sources/wiki-250781168/r1/content.json`, both `bodyView` and `bodyStorage`, against its metadata.

Verified source identity: page `250781168`, page version **8**, updated `2026-10-08T18:31:40.254+08:00`, captured `2026-10-19T08:24:54.988Z`. Metadata records SHA-256 `cd74e398e690d48e3da571a6c2adf02d8c755856948d98747b8d447ad628244d`. **No independent hash recomputation was performed.**

Owner evidence read:

- Complete MOS-1251 and MOS-1258 proposal/design/tasks/specs and change metadata.
- MOS-1249 design/tasks and feedback-api delta specification.
- Complete `openspec/specs/surface-lifecycle-publication/spec.md` and complete M proposal/design/tasks, both delta specifications and change metadata.
- `A/reports/SCENARIO-MOS-960.md`; scoped MOS-961/MOS-962 report passages cited by the supplement; complete `R-SCENARIO-MOS-960/961/962.md`.
- Complete `RECON-MOS-959.md` and `RECON-MOS-959-CONTRACT.md`; `SCENARIO-SURFACE-CONFIG-r2.md:70–115`.
- `R-MOS-1250.md` for documentary ownership/qualification, not independent implementation verification.
- `A/decisions.md`, including D-004/005/012/020/023; `A/sources/api-live/r2/metadata.json`.

No API schema/operation scan, linked-wiki re-audit, application-code inspection, tests, builds, browser/network access or Git/index verification occurred. API conclusions below remain attributed to accepted historical reports/reviews, not freshly verified r2 or runtime facts. Other journal rows were not assessed.

## Feedback supplement — ACCEPT

Primary locators are valid in both journal body representations: first table `tbody/tr[2]`, second physical `td`, its `div.content-wrapper`; status in the last physical `td`. The fifth and seventh pre-table paragraphs distinguish РЕШЕНИЕ from ЗАКРЫТЫЙ.

| Candidate | Independent result and evidence | Exceptions / mandatory corrections |
|---|---|---|
| **JOURNAL-FEEDBACK-AUDIENCE-01** | **Accept: already covered.** Row paragraph 2 and first `pre` attribute one `fb_survey_surface` relation to the quoted model; paragraph 4 asks about shared edits. MOS-1251 design **Implementation decisions**, spec **Linked audience and surfaces / Shared surfaces** (`:30–47`) and task **1.2** explicitly provide one `surface_ids` set and cross-tab synchronization. Tasks **1.4–1.5**, **2.3** and MOS-1249 **1.2** support the persistence/dependency mapping. | None. This is planning coverage, not verification of storage or implementation. |
| **JOURNAL-FEEDBACK-AUDIENCE-02** | **Accept: historical question only.** Paragraph 5 says «уточнить на встрече с ГК, с Русланом»; list UUIDs `5589b816-1bab-4179-a7a3-edc007048fd9` and `debb3a98-0508-4908-b2a8-b2dc304222e1` ask about removal versus synchronization. Status macro `23e504b4-1547-4275-8469-0c78d920d4b5` supplies no meeting outcome. MOS-1251 already defines the shared-set baseline and says no blocking product decisions remain in its agreed stage. | None. Missing follow-up is not a new blocker or removal approval. |
| **JOURNAL-FEEDBACK-AUDIENCE-03** | **Accept: ownership guard.** The model excerpt mentions registry audience display, not search semantics. MOS-1258 spec **Advanced conditions and reproducible selection** (`:7–24`) and tasks **1.1–1.2** place audience inside the flat conditions group. MOS-1251 spec **Display rule configuration** and task **1.3** separately own card rules, without frontend trigger execution. | None. No new registry surface filter, independent audience filter or trigger-specific relation follows. |

The supplement correctly preserves MOS-1249’s existing policy and source-precedence boundary rather than reviving the rejected registry policy blocker.

## Surface supplement — ACCEPT

Primary locators are valid: first table `tbody/tr[4]`, second physical `td`, identified independently by MOS-914; first ordered list contains questions, second contains Андрей’s answers. The reported question/answer UUIDs match. Status macro `5479af4b-21b9-4391-8313-091671d458e4` and legend macro `ab39723d-3117-478f-bf10-5a2e2229b5b6` establish accepted-answer status, not delivery.

| Candidate | Independent result and evidence | Exceptions / mandatory corrections |
|---|---|---|
| **JOURNAL-SURFACE-MVP-01** | **Accept: no-op.** The paragraph immediately before the answer list explicitly excludes sandbox from MVP. Main lifecycle spec **Lifecycle status and actions / No sandbox workflow in MVP** (`:37–68`), M proposal and task **1.2** already establish that boundary. | None. CLOSED does not prove execution or close the original feature. |
| **JOURNAL-SURFACE-MVP-02** | **Accept: historical checking intent.** Answer 1 distinguishes send from a system-recorded result with author/date/trace, rejects separate manual confirmation, and calls for rechecking after edits and completed training. Accepted R-MOS-960 evidence distinguishes saved checks/history from session identity and tested-version binding. | None. No new operation, completed check, surface result model or revision binding is established. |
| **JOURNAL-SURFACE-MVP-03** | **Accept: qualified publication wording.** Answer 1’s “only” scenarios/draft claim is not promoted into the complete MVP policy. Main spec **Publish requires confirmation and truthful success**, **Preparation refresh changes eligibility**, and M overview delta **Publication checklist distinguishes facts from confirmations** preserve status, current/saved composition, validation and fresh-read requirements. | None. No greeting blocker, retained failed sandbox checklist item or hidden sandbox call is introduced. MOS961-A04 remains unresolved historical contract tension. |
| **JOURNAL-SURFACE-MVP-04** | **Accept: future entry-state question retained.** Answer 2 explicitly favors «Настроена», «Проверка», «Песочница» while acknowledging conflicting prototype visibility. The supplement preserves literal Russian labels versus wiki `checking` versus historical OpenAPI `review`, as required by R-MOS-960. Main spec and M design preserve actual enable/restore responses without forced `configured`. | None. No alias, source precedence or sandbox activation follows. |
| **JOURNAL-SURFACE-MVP-05** | **Accept: audience/session question remains open.** Answer 3 explicitly leaves all-users/sender/status-only recipients unresolved while attributing an isolated test-session UI to the prototype. MOS-960 context/session candidates, MOS961-C01/C03/C05/C07 and MOS-962 owner question 3 are appropriate existing destinations. | None. Prototype intent is not proof of production isolation, effective snapshot or conversation transport. |
| **JOURNAL-SURFACE-MVP-06** | **Accept: attributed role contradiction only.** Answer 3 lists dialogue/history roles and explicitly contrasts surface-owner matrix restrictions with prototype dialogue access. D-012 and accepted scenario reviews preserve historical auth approval without extending it to sandbox. | None. No grants, permission mapping, new role model or reopened general auth gate is inferred. |
| **JOURNAL-SURFACE-MVP-07** | **Accept: full-card intent versus approved partial sequence.** Answer 4 explicitly includes greeting, suggestions, cards, appearance and scenario parameters, with save-before-command ordering. Main spec **MVP editing and deferred functionality boundaries** (`:179–196`), M design §§2–3 and tasks **2.2–2.5** deliberately limit current persistence to editable skills/parameters and preserve partial success. D-004/005 retain future configurator reconciliation. | None. “One action” does not establish atomicity, rollback, a combined PUT or authorization to simulate missing configuration editing. |

## Preserved dispositions and gates

- **D-004/005:** Configurator deferral and versioned enum/nullability/default/persistence disagreements remain intact. Historical evidence is supplemented, not overwritten.
- **D-012:** Saved checks are not session/version/readiness proof; existing token, conversation and synchronization gates remain. Historical auth approval is neither reopened nor extended.
- **D-020:** The separately approved three-command planning scope is untouched.
- **D-023:** New r2 publication does not invalidate historical evidence wholesale or establish compatibility, token revocation semantics, disclosure policy or activation authority.
- Journal status, chronology and source-attributed implementation claims do not override explicit approvals.
- No mandatory product-document update, task closure, implementation acceptance or new publication precedence is inferred.

**Mandatory corrections: none.** Acceptance is limited to these ten documentary candidate dispositions and their stated qualifications.