# Code Context

## Scope and result

DELTA-DIALOG-LIST-CARD-EXAMPLES: bounded documentary comparison only. Both complete historical readable bodies and all exact body-view chunks were read inertly. Findings below distinguish existing owner coverage, historical disagreements, and unresolved documentary boundaries. They do not propose endpoint/auth/DTO adoption, decide source precedence, establish runtime absence, or identify UI implementation defects.

## Files Retrieved

Paths below are relative to the project root. `A` means `openspec/changes/reconcile-control-center-backlog/audit`; `L` and `C` are exact source aliases used in findings, not additional sources.

1. `A/work-items/DELTA-DIALOG-LIST-CARD-EXAMPLES.md` (complete) — scope and restrictions.
2. `A/sources/wiki-241080643/r1/metadata.json` (lines 1–21) — historical list r1, wiki v7, version timestamp 2026-09-08T17:41:38.349+08:00.
3. `A/sources/wiki-241083649/r1/metadata.json` (lines 1–21) — historical card r1, wiki v2, version timestamp 2026-09-08T20:54:39.660+08:00.
4. `A/sources/wiki-241080643-readable/r1/metadata.json` and `A/sources/wiki-241083649-readable/r1/metadata.json` (each lines 1–14) — parent-attributed derivation/hash/roundtrip records.
5. **L:** `A/sources/wiki-241080643-readable/r1/content.txt` (lines 1–224, complete).
6. `A/sources/wiki-241080643-readable/r1/body-view-chunks.json` (lines 1–8, all six ordered chunks, zero-based indices 0–5). Chunk 0: conditions request/errors; 1: list parameters/body; 2–3: list response/errors and initial row table; 4–5: remaining row/count/pagination/selection tables.
7. **C:** `A/sources/wiki-241083649-readable/r1/content.txt` (lines 1–255, complete).
8. `A/sources/wiki-241083649-readable/r1/body-view-chunks.json` (lines 1–11, all nine ordered chunks, indices 0–8). Chunks 0–2: request/full illustrative response/errors; 2–4: message/category/participant/operator tables; 4–6: route/actions; 6–8: answers/skill/basis/rating tables. Boundaries can split words/keys; these are not independent examples.
9. `openspec/specs/dialog-registry/spec.md` (lines 1–101).
10. `openspec/specs/dialog-details/spec.md` (lines 1–82).
11. `openspec/specs/dialog-route/spec.md` (lines 1–57).
12. `openspec/specs/dialog-answer-insights/spec.md` (lines 1–68).
13. `openspec/specs/dialog-selection-builder/spec.md` (lines 1–67) — comparison limited to directly relevant conditions/phrase/application/validation clauses.

## Key Code / documentary findings

No application code was inspected. The critical structures below are documentation, not executable requests or adopted interfaces. Stable finding IDs identify this lane only.

### DLC-01 — Query and selection: covered intent, incompatible historical representation

**Evidence:** L 1–37 (Step 1 request and `selectionId` response), 58–67 (Step 2 parameter table), 164–177 and 219–224 (`selectionBuilder`). Exact list chunks 0–3,5. Current owners: `openspec/specs/dialog-registry/spec.md` 32–44,79–101; `openspec/specs/dialog-selection-builder/spec.md` 18–39,41–67.

Historical Step 1 describes creating a selection because numerous conditions may not fit a URL; Step 2 optionally applies its ID. Conditions explicitly describe `match=and|or`, phrase `contains` with a comment about occurrence/nonoccurrence, `searchMode=words|exact`, `scope=all|user|assistant|skill|operator`, and conditional `skillId`/`operatorId`. The example's `value=null` is not a rule that a missing phrase is valid, nor does the comment establish a complete operator enum. Historical `words` means words in any order; current `any_order` additionally requires every word. Do not infer equivalent matching semantics or translate automatically.

Historical query parameters are all optional: selection ID; period presets today/last7days/last30days/lastMonth/custom; custom ISO-8601 from/to; singular channel and skill IDs with `all`; full-text query over dialog text, ID and attributes; offset and limit. Current owner instead requires one versioned selection with q/period/channel_ids/skill_ids/condition_group/time_zone, AND combination, all_time default, inclusive calendar dates and server interpretation, explicit application, typed all/any conditions and validation. Existing filtering intent is covered; selection-ID lifecycle, singular/multiple filter equivalence, precise q search-domain correspondence and scoped participant-ID selection remain documentary reconciliation boundaries. The historical date examples do not establish inclusivity, timezone, preset defaults or expiry of selection IDs.

**Disposition:** registry/builder owner comparison; no new selection endpoint, enum conversion or relaxation of current validation.

### DLC-02 — Paging, sorting and counts: retain distinct assertions

**Evidence:** L 66–67,83–85,157–176,208–224; list chunks 1–5. Current `openspec/specs/dialog-registry/spec.md` 46–77.

Historical offset has minimum 0; limit is 1–100, with example 25, not a stated default. `pagination` defines total, shown on the current page, offset, limit and hasMore; `summary.total` is all dialogs under current filters and `summary.shown` is page display count, explicitly ≤ total. Optional `selectionBuilder.foundCount` is count under builder conditions. Current owner specifies opaque cursors, default limit 25, server total/data_updated_at, continuation identity/retry/reset and sorting by started_at/ended_at/channel/operator_rating/duration, default -started_at, server nulls-last.

No sorting parameter, default order or null placement promise is stated in the complete historical list body. This is bounded document silence, not missing backend functionality or grounds to remove current sorting. Offset and cursor models disagree; do not synthesize offset-to-cursor conversion. Example total 52 versus builder count 56 can describe different filter scopes and does not prove inconsistency. Example shown=25 with only two illustrated items is a sample/count discrepancy, not evidence of a complete 25-row response or a production counting defect. Do not derive totals from sample array length or assume all count fields are interchangeable.

### DLC-03 — List rows: substantial owner coverage with identity/auth/incident boundaries

**Evidence:** L 87–155,194–207 (`items[]` table, keys id through incidentMarkText); chunks 2–4. Current `openspec/specs/dialog-registry/spec.md` 18–30; `openspec/specs/dialog-details/spec.md` 23–40.

Historical row fields explicitly cover identifier, first user message/topic, skill/operator participants with IDs and labels, operator participation, authorization at dialog start, ISO start/end, duration in seconds, localized channel, operator rating 1–5, incident flag and conditional incident text. `endedAt=null` explicitly means active; `operatorRating=null` means no rating. `incidentMarkText` is string or null, only when hasIncidentMark=true; its omission in the false-flag examples is not a contradiction.

Current registry covers corresponding presentation concepts in six columns with chat_id, skills, independent has_operator/has_failure, channel IDs/names, nullable end/rating and authorization states unauthorized/authorized_in_dialog. Historical boolean start authorization must not collapse those states or become employee authentication. Historical incident text and hasIncidentMark cannot automatically be equated to current has_failure. Historical `id` cannot automatically be equated to chat_id: C 25–27 separately illustrates id/chatId/sessionId.

**Genuine sample/table conflict:** L 141–147 lists an operator participant but says hasOperator=false; table L 198–199 describes actual participants and whether an operator participated. Preserve both assertions as a historical inconsistency; do not choose a derived flag or diagnose current UI behavior. Current owner explicitly retains independent operator/failure flags.

### DLC-04 — Card snapshot, overview, transcript and participants

**Evidence:** C 1–8,24–82,159–196; card chunks 0–5. Current `openspec/specs/dialog-details/spec.md` 9–40,70–82.

Historical card description supplies overview, timeline and answers in one response, agreeing in intent with the current unified snapshot. Overview is example-only here: id/chatId/sessionId, authorized/ssoId, channel, start/end/duration, stepsCount, endReason/endedBy, url/deviceInfo/title; there is no separate overview field table defining nullability or the meaning of its stepsCount. Current owner covers identity, timing, categories, completion metadata, surface/url, counters, user, participants and operators. Device information/title/ssoId correspondence is not established by those clauses; do not manufacture fields or infer retained-data obligations.

Historical transcript table specifies user/assistant/operator authors, conditional nullable operator/skill identity, postedAt/text and optional-valued rating; rating is described only for rated assistant messages. Current owner explicitly includes skill/subsystem/operator/user, attachment-only nullable text, stable source order, resident authorization transitions, multiple operators, null/zero/empty distinctions and ongoing snapshot duration. These current semantics are not negated by a shorter historical example; no message ordering, equal-time tie rule, attachment absence, or completeness guarantee follows from C's ellipsis.

Historical participants.totalMessages explicitly excludes user messages (assistant plus operator). Each participant has type/id/name/message count, share 0..1 and good/bad counts; `messagesShare` says “of all messages,” requiring denominator clarification alongside that explicit exclusion. Current detail clause uses server share_percent/message_count with step_count and forbids normalizing rounding. Do not multiply fractions by 100 or equate counters without an accepted mapping. The optional singular historical operator block provides rating 1–5, maximum scale and nullable reason/comment; current owner explicitly supports multiple operators while retaining one dialog performance rating. Historical absent operator, null rating and empty operators are not interchangeable contracts.

Categories historically carry id/dialogId/name, assignedBy operator|auto and assignedAt (C 169–175). This is read metadata, not evidence of category mutation, permissions or a new category-addition requirement. Current detail already requires displaying categories; the category-addition spec and MOS-1044 membership routing were not needed or inspected.

### DLC-05 — Route, timing units and operator actions

**Evidence:** C 83–117,197–226; card chunks 1,4–6. Current `openspec/specs/dialog-route/spec.md` 9–57; `openspec/specs/dialog-details/spec.md` 79–82.

Historical timeline table defines trace stepsCount, coveredSec, totalDurationSec, notCoveredSec and steps. Step table defines id, type (reception/classification/routing/external_call/response/ethics/operator_transfer/operator_response/completion), component/title/start time, durationMs, transitionMs to next step, threshold/error booleans, and type-dependent details. Seconds versus milliseconds are explicit; illustrative timestamps do not define a global timezone policy. Threshold value/rule, transition aggregation and coverage formula are not specified. The 37 trace steps versus overview stepsCount=6 is not a proven contradiction: the overview counter lacks a definition. Nor do sample duration totals establish latency, completeness or deployment.

Current owner uses source-ordered route steps with occurred_at/kind/component/action/detail/duration_ms/failed, different kind vocabulary, server traced/untraced totals, no summing step durations, and explicit unavailable versus empty trace. Historical transitionMs/threshold/type details require owner clarification if proposed as retained requirements; they are not automatic extensions or aliases. There is no justification to generate steps/IDs, infer message links or turn missing totals into zero.

Historical actions identify each operator and event time plus action enum, action label, nullable object/result and nullable waitSec (seconds). Current action clauses preserve per-event authors/order and hide an empty array. Object/result/wait and historical action enum do not establish a DTO mapping into current details, queue latency invariants, or authorization/audit behavior. Single example author does not constrain cardinality.

### DLC-06 — Answers and ratings: material source disagreement, not a new implementation defect

**Evidence:** C 118–144,167–168,227–255; card chunks 1–3,6–8. Current `openspec/specs/dialog-answer-insights/spec.md` 9–68.

Historical dedicated answers array describes assistant-answer analysis with explicit question/answer message IDs and texts, answer time, a skill {id,name,serviceId}, basis {type,label,description,sources}, nullable rating and comment indicator. Basis enum is external_data/no_data/llm; sources examples carry endpoint/serviceId. Rating table uses good/bad, reason, nullable comment and ratedAt.

Current owner derives all non-user answers (including operator/subsystem) from messages in the shared snapshot, uses nearest preceding user message as question, allows no preceding question, and separates message good/poor from dialog operator_rating. Current basis kinds external_system/knowledge_base/model/operator_template/no_data and basis=null have explicit independent meanings; source navigation requires safe URLs and confirmed skill route identity. Thus dedicated answer pair IDs, assistant-only rating wording, bad versus poor and basis vocabularies are substantive documentary differences. Neither source is silently rewritten here. Historical sources do not establish that an endpoint is a UI navigation link, nor that serviceId is a route ID. Answer timing is documented separately from message/question timing, but no ordering/completeness rule follows from the example.

**Disposition:** answer-insights/detail ownership, preserve conflicting derivation/population/rating assertions and clarify only through the owner contract process; no copying of answers DTOs or automatic enum mapping.

### DLC-07 — Exact sample/table mismatches and errors

**Evidence:** list chunks 0,2–4; card chunks 0–8; locators below. These are source-quality observations, not runtime defects.

- C 49 uses `skillId` followed by a trailing nonbreaking space in the quoted key; C 164 table names `skill`. Exact chunks confirm the spelling difference; do not silently normalize it into an adopted field.
- C 41–50 omits table `messages[].hasComment` (168); categories sample 53–59 omits table dialogId (172); route sample 83–103 omits notCoveredSec (202) and step id (206); answer sample 118–143 omits hasComment (238). These are sample/table coverage differences, not proof of optionality or missing real response fields.
- C 237's rating object example includes ratingLabel, whereas the detailed rating table 250–255 has no ratingLabel row (numbering skips 2). Retain ambiguity; no field requirement or removal follows merely from row numbering.
- L 90 lacks a comma before participants; L 22–24 lacks separators between example scope/identity properties. Comments and C 51/102 ellipses further demonstrate illustrative, non-executable syntax. Nothing was parsed as a live business request or repaired/executed.
- Historical responses explicitly show 200, 422 validation and 500 internal error with error_type/error_message: L 29–51,76–80,180–192; C 17–21,147–158. Current registry 60–77 preserves status/code/field errors, cursor recovery, unavailable versus empty and retry; current details 70–82 distinguishes NOT_FOUND/503/route unavailable. Historical sparse errors do not define exhaustive statuses, retry rules or current envelopes. No auth behavior is adopted from either historical request body (L 12–13,72–73; C 13–14).

## Architecture

This is an owner-document comparison, not a code dependency audit. The current registry's applied selection and cursor chain own list identity/counts. The current detail snapshot owns transcript and metadata, and route and answer-insights project that snapshot. Historical list instead illustrates a two-step selection-ID/offset exchange; historical card puts explicit routeTimeline/operatorActions/answers beside transcript. Shared business intent does not make these representations interchangeable.

## Start Here

Open `openspec/specs/dialog-registry/spec.md` lines 32–77 first for query/paging/count ownership, then this report's DLC-01–03. For the card, open `openspec/specs/dialog-details/spec.md` lines 9–40 and `openspec/specs/dialog-answer-insights/spec.md` lines 9–44 before evaluating DLC-04–06. These are review entry points, not instructions to edit accepted requirements.

## Evidence limits and residual risks

- Raw `r1/content.json` envelopes and attachment indexes were not independently read; both empty returned attachment indexes are work-item/parent-attributed. All readable bodies and exact chunk files were read. Metadata hashes were not recomputed; decoded bodyView roundtrip equality remains parent-attributed.
- Current API publication r2 is acknowledged by the work item but was not inspected; neither API-r1 nor r2 operations were scanned. No historical omission is a claim of current backend absence.
- No application code, generated schema, tests, runtime, credentials, links/assets, external resources, network/browser/MCP or source examples were executed. Example identities and auth fields remain documentary, not current citizen records or employee-session data.
- No JIRA membership report/inventory, new graph/links, business/decomposition lane (245670575/241080071), export spec or category-addition spec was inspected; no direct export operation is described by these bodies. Existing owner names here come from the inspected specs, not independently verified issue membership.
- Only this bound report was written. No owner plans/specs/tasks/archive were edited. No tests/build/lint were run: this is the explicitly restricted documentary lane. Git index was not inspected, so no staging-state attestation is made.
- Residual risks are unresolved historical semantics/mappings and parent-attributed source integrity, not established UI/backend defects. Source precedence and any contract changes remain undecided.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Both complete historical readable bodies and all exact chunks compared against scoped current owner clauses; DLC-01 through DLC-07 record coverage, discrepancies and unresolved boundaries with source/version/key/line locators."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-DIALOG-LIST-CARD-EXAMPLES.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find/ls plus scoped numbered-line and line-count inspection","result":"passed","summary":"Read both complete bodies, six/nine exact chunks, metadata and five current specs; verified line locators."},{"command":"tests/build/browser/example execution","result":"not-run","summary":"Prohibited by the documentary work item."}],
  "validationOutput": ["List body 224 lines; card body 255 lines; all exact chunks read without truncation."],
  "residualRisks": ["Hashes and raw-envelope roundtrip not independently verified; attachment emptiness parent-attributed.","Historical identity, selection, timing, ratings and enum disagreements remain unresolved; current API/runtime not inspected."],
  "diffSummary": "Sole bound documentary report; no implementation or owner-document changes.",
  "reviewFindings": ["No implementation verdict: code audit excluded. Historical discrepancies retained in DLC-03 and DLC-07; material owner differences in DLC-01/02/04/05/06."],
  "manualNotes": "All examples remained inert. No source precedence, endpoint/auth/DTO adoption or runtime-absence claims. Git index not inspected; staging state not attested."
}
```
