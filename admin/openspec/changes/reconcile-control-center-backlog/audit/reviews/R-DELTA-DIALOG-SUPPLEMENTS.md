# R-DELTA-DIALOG-SUPPLEMENTS — independent bounded review

## Review

- **DELTA-DIALOG-BUSINESS-PLAN: ACCEPT**
- **DELTA-DIALOG-LIST-CARD-EXAMPLES: ACCEPT**
- **Correct:** All 17 candidates preserve the distinction between documentary evidence, scoped current specifications and unresolved owner questions.
- **Fixed:** None; review was read-only.
- **Mandatory corrections:** None.
- **Merge verdict: OK** for these two documentary reports only.

No issues found.

Acceptance does not adopt historical contracts, select source precedence, authorize implementation, verify deployment, close owner gates or change global **6/28**.

## Evidence read

`A` = `openspec/changes/reconcile-control-center-backlog/audit/`.

Read completely:
- This review’s work item, both matching report work items and both reports.
- Four saved readable bodies and their complete exact markup chunk arrays:

| Alias | Saved readable source | Recorded wiki version | Body lines | Exact chunks |
|---|---|---:|---:|---|
| D | `A/sources/wiki-245670575-readable/r1/content.txt` | v4 | 1–88 | `$[0]–$[3]` |
| B | `A/sources/wiki-241080071-readable/r1/content.txt` | v2 | 1–81 | `$[0]–$[3]` |
| L | `A/sources/wiki-241080643-readable/r1/content.txt` | v7 | 1–224 | `$[0]–$[5]` |
| C | `A/sources/wiki-241083649-readable/r1/content.txt` | v2 | 1–255 | `$[0]–$[8]` |

Chunk locators refer to each corresponding `body-view-chunks.json`. All four original-source metadata files and all four readable metadata files were read completely. Recorded versions and timestamps agree with the reports.

Also read:
- Complete `openspec/specs/{dialog-registry,dialog-details,dialog-export,dialog-route,dialog-answer-insights,dialog-selection-builder,dialog-saved-filters}/spec.md`.
- Complete `A/reports/JIRA-MOS-773.md`, used only as the supplied accepted membership reference.
- Targeted `A/inventory.json:898–975,1042–1061`, used only for the claimed documentary owner associations.

## Candidate verification — business/decomposition report

| Candidate | Decision | Verified evidence and boundary |
|---|---|---|
| DBP-01 | ACCEPT | B:23–31,45 explicitly names message text/chatId/sessionId/ssoId and input/filter triggers. D task 21 names debounce. `dialog-registry/spec.md:32–44,79–101` specifies versioned selection and explicit submission. Neither source settles calendar/rolling equivalence or makes debounce proof of automatic submission. |
| DBP-02 | ACCEPT | B:45 requires type/date/topic/channel/rating/duration and sorting all columns. Registry:18–30,46–63 instead specifies six presentation columns, independent flags and bounded sorts. The report preserves the disagreement without inventing supported sorts or an exclusive type enum. |
| DBP-03 | ACCEPT | B:35,47,49,53,56 supports the additional metadata, highlighting and preview questions. Highlighting occurs in both MUST and SHOULD. Details:23–40 and answer-insights:28–40 do not establish the proposed identity/metadata mappings or owner-skill highlighting. Absence is scoped to requirements, not runtime. |
| DBP-04 | ACCEPT | B:48 explicitly requests delays between messages; D task 8 concerns processing route. Details:23–40 and route:9–48 support distinguishing transcript timing from processing durations and coverage. No new endpoint, synthesized events or inferred links are authorized. |
| DBP-05 | ACCEPT | D tasks 6,9,11,13,17,22 support selection, answers and saved-filter intent. Builder:9–67 preserves typed all/any conditions, fixed catalog, validation and the 30-condition bound; saved-filters:9–67 preserves applied-selection persistence/link limits. Answer-insights:9–26 includes non-user answers, including operators. “Arbitrary” does not remove these limits. |
| DBP-06 | ACCEPT | B:50 explicitly allows field choice for marked dialogs; export:33–35 fixes marked export to all 24 columns. B:55,74 places XLSX in SHOULD/stage 3. The report correctly distinguishes file format proposals from current CSV shapes and does not claim successful downloads. |
| DBP-07 | ACCEPT | D tasks 1–11, especially task 4, propose backend integration/projection and asynchronous report assembly/storage. Export:9–31,75–96 specifies synchronous external delivery without invented jobs. Internal asynchronous work is not necessarily incompatible; the report retains the unevidenced relationship as an architectural question. Blank issue cells establish no missing owner or service. |
| DBP-08 | ACCEPT | B:57–62,74 excludes manual tagging while placing ML/Writer in future scope. D:87 and inventory:966–975 support routing MOS-1044 to category-addition, not determining its behavior. The report explicitly leaves that owner’s uninspected semantics unresolved. |
| DBP-09 | ACCEPT | B:44–56 versus 71–81 supports the MUST/SHOULD/stage distinctions: skill filters, timeline and bulk export span full requirements and stage 2; highlight appears twice; preview has no explicit stage. No priority/date precedence or delivery commitment is selected. |
| DBP-10 | ACCEPT | B:63–70 states latency, access, audit and compliance requirements, not measurements or approvals. Details:23–25 separates resident authorization from employee session; route:50–57 prohibits manufacturing audit; export:9–11,75–77 references shared session handling. The report does not harmonize or expand auth contracts. |

### Membership and ownership

D contains **22 proposed task rows** and **10 distinct keys in its concluding list**, not 22 verified Jira tasks. Exact markup confirms:
- Task 15 associates both MOS-1041 and MOS-1042.
- Task 17 associates MOS-1042 again.
- Tasks 1–11 and 18–21 have blank issue cells.
- Loading text and `СТАТУС` are embedded placeholders, not fetched statuses.

The ten listed keys are included in `JIRA-MOS-773.md:13–29`; that reference additionally lists MOS-1211, producing **11 accepted direct members**. The report correctly preserves MOS-1211 and does not treat duplicate associations as duplicate membership. Inventory archive names support the eight claimed owner routes; cross-references within inventory rows are not reassigned as primary owners.

## Candidate verification — list/card examples report

| Candidate | Decision | Verified evidence and boundary |
|---|---|---|
| DLC-01 | ACCEPT | L:1–37,58–67,219–224 documents selection-ID creation/use, and/or terminology, phrase scope and singular filters. Registry:32–44,79–101 and builder:18–67 specify a different versioned selection/application model. Historical `words` does not explicitly supply current `any_order`’s every-word rule. No automatic mapping or missing-value permission is inferred. |
| DLC-02 | ACCEPT | L:66–67,157–176,208–224 defines offset/limit and distinct summary, pagination and builder counts. Registry:46–77 specifies cursors, sorting and server counts. Complete L contains no sorting promise. The 52/56 counts may have different scopes; shown=25 versus two illustrated rows remains a sample discrepancy, not a runtime counting defect. |
| DLC-03 | ACCEPT | L:194–207 explicitly defines start authorization, null end/rating and conditional incident text. L:141–147 genuinely combines an operator participant with `hasOperator=false`, conflicting with the participation descriptions at 198–199. C:25–27 separately illustrates id/chatId/sessionId. Registry:18–30 and details:23–40 do not justify collapsing these identities or authorization/incident meanings. |
| DLC-04 | ACCEPT | C:24–82,159–196 supports unified card intent, example-only overview, transcript vocabulary, participant counts/shares and optional singular operator block. C:178 excludes user messages from totalMessages while 186 says share of all messages: clarification remains appropriate. Details:23–40 uses server percentages/step_count and multiple operators. Category metadata at C:169–175 is not mutation authorization. |
| DLC-05 | ACCEPT | C:197–226 explicitly distinguishes second-based totals/wait from millisecond step/transition durations. Overview stepsCount at C:34 lacks a defining table, so it is not automatically comparable to trace stepsCount. Route:9–57 preserves source order, server totals, unavailable/empty distinctions and per-event operator identity. No formula, threshold, DTO conversion or audit meaning is invented. |
| DLC-06 | ACCEPT | C:167,227–255 documents assistant-oriented dedicated answers, explicit question/answer IDs, good/bad ratings and external_data/no_data/llm basis kinds. Answer-insights:9–68 instead derives non-user answers and nearest preceding user questions from messages, with good/poor and different basis semantics. The report preserves these differences without converting endpoints/service IDs into navigation identities. |
| DLC-07 | ACCEPT | Exact chunks confirm C:49’s trailing nonbreaking space in `skillId ` versus table `skill` at 164. Listed sample omissions, ratingLabel/table discrepancy, missing list separators and ellipses are present. L:29–51,180–192 and C:147–158 supply sparse historical errors, not exhaustive current statuses or envelopes. Examples remain illustrative and inert. |

## Verification limits

- This independently checks the supplied reports against saved bodies, exact chunks, metadata and scoped specifications—not the original remote pages.
- Raw `content.json` envelopes and attachment indexes were not read. Hashes were not recomputed; decoded-body roundtrip and empty-index claims remain **parent-attributed**.
- Complete saved-body reading does not establish linked-resource completeness. No links, attachments, additional Jira records or archives were traversed.
- Membership is checked against the supplied accepted report, not independently rebuilt from Jira packets. Its staging-state language is not adopted.
- Category-addition semantics, application code, generated schema, API-r1/r2 operations and runtime behavior were not inspected. Current API r2’s existence is acknowledged from the work item; historical silence is not current backend absence.
- Business brief, decomposition and endpoint examples remain distinct evidence. No chronology-based precedence, source consensus or current-contract amendment is inferred.
- No network/browser, credentials, example execution/rendering, tests/build, nested delegation or repository edits were performed. Git index state was not inspected or attested.
- Existing auth/session boundaries, owner scopes and global **6/28** remain unchanged.