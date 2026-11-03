# Code Context

## Result — API-G2-FEEDBACK-SURVEY-MUTATIONS

- Saved r2 and both local contracts publish survey **POST, detail GET and PUT**, not PATCH. Existing MOS-1249 design explicitly selects published PUT. Jira PATCH remains a source discrepancy; no guessed method substitution is needed or authorized.
- All three operation subtrees match locally after excluding their separately approved security normalization; all **16 transitively reachable schemas match exactly**.
- CRUD §7.1 explicitly resolves label limits **per field**, 150 after trim, skipped empty tokens, and whitespace/comma-only clearing. These are explanatory contract semantics, not all encoded schema constraints or deployment evidence.
- **Q1 remains unresolved:** “If an existing unknown type has nonempty options, should saving preserve opaque options, omit them, or block save?” No inspected clause specifically reconciles this case. Parent confirmed retaining the question without choosing policy; no exhaustive absence of an accepted ruling elsewhere is asserted.

Only the configured external artifact was written. No repository changes, business/network/browser calls, tests, typegen, code audit, nested agents or expanded collection.

## Files Retrieved

Aliases expand literally: `C=openspec/changes/reconcile-control-center-backlog`; `A=C/audit`; `D=docs/api/contracts`; `O=openspec/changes/mos-1249-feedback-api`.

Complete semantic reads:
1. `A/work-items/G2-FEEDBACK-MUTATION-CONTRACTS.md:1–15` — complete common contract and assigned unit; neighboring filter heading read incidentally, not executed.
2. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108` — authority and evidence separation.
3. `A/reports/REQ-G2-MOS-1254.md:1–133`, `REQ-G2-MOS-1257.md:1–135`, `SPEC-G2-MOS-1254.md:1–160`, `SPEC-G2-MOS-1257.md:1–144`; `A/reviews/R-REQ-G2-MOS-1254.md:1–66`, `R-REQ-G2-MOS-1257.md:1–61`, `R-SPEC-G2-MOS-1254.md:1–73`, `R-SPEC-G2-MOS-1257.md:1–82` — accepted requirements, parent-corrected classifications, original reviews.
4. `O/proposal.md:1–32`, `O/design.md:1–81`, `O/specs/feedback-api/spec.md:1–38` — full API-owner approval/contract-update boundary, not proof of wire correctness.
5. `D/README.md:1–33`, `D/managed-resources.md:1–55`, `A/sources/api-live/r2/metadata.json:1–22` — provenance, normalization and retained CRUD locator.

Bounded reads:
6. `A/decisions.md:1–24` — complete D-065 and incidental D-064/start D-063; not full decision history.
7. `D/crud-api.md:1–155,223–246,415–518,995–1145,1194–1296` — introductory contract/permissions, inactive-reference rules, survey create/labels/detail/update/system fields/errors/statuses. TOC/other-resource table rows incidental; no other operations audited. The linked raw CRUD file was **hashed only**, not semantically read; findings cite the actual Markdown hash below.
8. `A/sources/api-live/r2/content.json`, `D/openapi.json`, `D/managed-resources.openapi.json` — only exact operation roots and their full reachable schemas below, plus two referenced security definitions. Parsed whole files for extraction/hash/comparison, not a whole-contract semantic audit. No reuse of prior read-schema conclusions: the small required closure was independently read. No registry/lookup/search/answers census.

Combined shell output truncated twice; missing governing/report beginnings were reread from tool spools. No semantic claim depends on unseen truncated output. Accepted REQ reports supply Jira/wiki joins; those primary packets were not independently reread in this API unit.

## Key Code — exact JSON read set

Pointers below apply identically to all three JSON files unless security difference is stated. Define:

- `P=/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys`
- `E=/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys~1{entity_id}`
- `S=/components/schemas`

These are literal JSON-pointer prefixes, not filesystem paths. Full operation reads: `P/post`, `E/get`, `E/put`; path-item key inspection establishes only `post` at P and `get,put,delete` at E. DELETE body was not audited. PATCH is absent at both assigned path items.

| Operation | Request / success / formal error |
|---|---|
| `P/post` | Required JSON body `$ref S/FeedbackSurveyCreate`; 201 `$ref S/TsamResponseSchema_EntityCreatedResponse_`; 422 `$ref S/HTTPValidationError`; operationId `create_fb_survey_api_control_api_v1_managed_resources_feedback_surveys_post` |
| `E/get` | Required path `entity_id`, string UUID; 200 `$ref S/TsamResponseSchema_FeedbackSurveyResponse_`; 422 HTTPValidationError; operationId `get_fb_survey_api_control_api_v1_managed_resources_feedback_surveys__entity_id__get` |
| `E/put` | Same path parameter; required JSON body `$ref S/FeedbackSurveyPatch`; 200 full survey envelope; 422 HTTPValidationError; operationId `patch_fb_survey_api_control_api_v1_managed_resources_feedback_surveys__entity_id__put`, summary “Patch Fb Survey” |

Exact nested response-schema pointer pattern: `{operation}/responses/{status}/content/application~1json/schema`; request: `{operation}/requestBody/content/application~1json/schema`. DTO/operationId spelling “Patch” is not an HTTP PATCH operation. No other statuses or concurrency/idempotency headers are declared in these operation objects.

### Full schema closure and constraints

All entries below denote complete `S/<name>` reads; line ranges refer to `D/managed-resources.openapi.json` for convenient navigation. No `$ref` remained unresolved; closure is exactly these 16 schemas. No oneOf/allOf/conditional constraints are hidden beyond this closure; unions here are the described anyOf branches.

| Schema (split lines) | Complete material constraints |
|---|---|
| FeedbackSurveyCreate (5222–5345) | Object, additionalProperties=false; required name/code/type_code. name string 1–255; code string max100 pattern `^[a-z][a-z0-9_]*$`; type_code string 1–50. Optional description string/null; owner string max200/null; responsible_user_id string/null; active_since date string/null. status string1–32 default draft; audience_type string1–32 default all. tags/segments/operator_groups string max16000 default empty. surface_ids array max100 UUID strings; questions array max100 FeedbackQuestion; display_rules FeedbackDisplayRules. Those arrays/object optional but not nullable; no minItems/uniqueItems. |
| FeedbackSurveyPatch (5346–5540) | Object, additionalProperties=false; **no required fields**. All 15 fields optional and anyOf their corresponding nonnull create shape/null. No create defaults restated. questions string? **No:** array max100 FeedbackQuestion or null; display_rules object-ref or null; each label string max16000 or null. `{}` is schema-admissible, while CRUD rejects it. |
| FeedbackQuestion (5148–5185) | Object, additionalProperties=false; required title/type_code. Optional id string UUID (not null); title string1–500; type_code string1–50, no enum; required boolean default false; options optional array max100 FeedbackOption, not null. No tags-dependent minItems, no uniqueness or ID-membership rule. |
| FeedbackOption (5111–5129) | Object, additionalProperties=false; required text string1–255; optional id string UUID, not null. No other fields. |
| FeedbackDisplayRules (4692–4901) | Object, additionalProperties=false, no required fields. trigger_type string1–50 default manual, not null. Nullable integer min0: min_messages/min_duration_sec/delay_show_sec/pause_after_last_sec/cooldown_sec. Nullable integer min1: max_per_session/max_per_day/max_per_user. Nullable booleans skip_if_rated default true, quiet_hours_enabled default false, exclusive_show default false. quiet_from/quiet_to time-string/null. dialog_type/dialog_result string1–32/null default any. priority integer/null default0. No cross-field dependencies. |
| FeedbackSurveyResponse (5541–5686) | Object; additionalProperties unspecified. Required id(UUID), created_at/updated_at(date-time), name/code/type_code, questions, display_rules. Other top-level field constraints/defaults as Create. questions required nonnull array FeedbackQuestionResponse **without request max100**; display_rules required nonnull FeedbackDisplayRulesResponse. surface_ids still max100. Labels optional nonnull string max16000/default empty, not object/code arrays. |
| FeedbackQuestionResponse (5186–5221) | Object; additionalProperties unspecified. Required id UUID/title1–500/type_code1–50/options array FeedbackOptionResponse. required boolean optional default false. options has no response maxItems; no type enum or conditional options rule. |
| FeedbackOptionResponse (5130–5147) | Object; required id UUID and text1–255; additionalProperties unspecified. |
| FeedbackDisplayRulesResponse (4902–5110) | Same properties/unions/defaults as request rules, no required fields; additionalProperties unspecified rather than false. |
| TsamResponseSchema_EntityCreatedResponse_ (2953–2976) | Object; required code(ResponseCode), data(EntityCreatedResponse), message(string); optional errors array ErrorItem. No null branch for success data; additionalProperties unspecified. |
| EntityCreatedResponse (2852–2863) | Object; required id string UUID; additionalProperties unspecified. |
| TsamResponseSchema_FeedbackSurveyResponse_ (7086–7109) | Same envelope, data FeedbackSurveyResponse. Required code/data/message; errors optional array; additionalProperties unspecified. |
| ResponseCode (2950–2952) | String, no enum/constant. SUCCESS value is explanatory text, not enforced here. |
| ErrorItem (2864–2909) | Object; required message string; optional field/code string-or-null; details object additionalProperties=true or null. Outer additionalProperties unspecified; no JSON Pointer pattern, no code enum. |
| HTTPValidationError (2910–2922) | Object; optional detail array ValidationError, no required keys; additionalProperties unspecified. |
| ValidationError (2977–3012) | Object; required loc array of string-or-integer items, msg string, type string. Optional input unconstrained, ctx object; additionalProperties unspecified. No required loc prefix or minimum count. |

For field-specific proof, append `/properties/<field>` to its S pointer; `/required` and `/additionalProperties` hold object constraints. Particularly relevant: `S/FeedbackSurveyPatch/properties/questions/anyOf/0/maxItems`, `S/FeedbackQuestion/properties/options/maxItems`, `S/FeedbackOption/properties/id/format`, `S/FeedbackSurveyPatch/properties/tags/anyOf/1/type` (null), and corresponding segments/operator_groups branches. Schema omission of a constraint is not product permission.

### Security and comparison boundary

For each of the three operations, r2 `/security` is `[{"AdminToken":[]},{"AccessToken":[]}]` (OR); aggregate/split are `[{"AdminToken":[],"AccessToken":[]}]` (AND). Removing only this key yields exact Python structural equality, including operationId, parameters, messages and all response/request declarations. All 16 full schema objects equal both local versions without normalization.

`/components/securitySchemes/AdminToken` and `/components/securitySchemes/AccessToken` in r2 declare header apiKey schemes, respectively `X-Admin-Token` and `X-Access-Token`, with descriptions requiring both raw tokens. README lines7–10 records separately agreed AND normalization. No auth/permission change follows from the OR discrepancy. CRUD lines74–92 records global-scope checks and create/read/update business rights; runtime enforcement was not tested.

## Requirement joins and explanatory semantics

`Qnn=REQ-G2-MOS-1254-nn`, `Lnn=REQ-G2-MOS-1257-nn`. These join accepted requirements, not newly approved product decisions.

| Join | Evidence and bounded conclusion |
|---|---|
| Q02,Q21; L04–05; SPEC1254 method finding | Exact POST/PUT roots above; CRUD136–153,1061–1086 explicitly partial **PUT**, omitted top-level fields unchanged. O/design:23 and operation table:45–52 explicitly prescribe published PUT after contract update; O/spec:9–14 prescribes POST→GET and PUT baseline. Wire identity resolved by independent contract reading plus existing ruling, not automatic Jira precedence. Jira POST/PATCH wording retained historically. |
| Q10–13,Q24 | Request max100 questions/options and string lengths directly encoded. additionalProperties=false on all request objects excludes sort_order, FKs, local keys, root system IDs/timestamps. Optional nested UUID allows omission; schema alone does not distinguish old/new identity. CRUD465,1102–1105 explicitly backend UUID generation, preserve existing question/option IDs, new IDs not set, array order authoritative. CRUD1194–1197 excludes root system fields. |
| Q09,Q21–24,Q30–31 | CRUD1088–1105: omitted top-level questions unchanged; [] deletes all questions/options; supplied list fully replaces membership; change one question by sending full final list with options. This is not partial nested-delta semantics. POST201 returns only survey ID (CRUD479–481), then GET obtains nested IDs; PUT200 contains full current card (1083–1086). Response schema requires nested IDs/options; persistence/order round trip itself remains runtime-unverified. |
| Q14–15 | CRUD1137–1140: tags requires nonempty options; other types options absent or empty. Schema has neither this conditional nor a minimum. Known non-tags empty-vs-omitted choice is documented as both allowed, not forced by schema. Does not resolve Q1. |
| Q25–29,Q06 | CRUD223–239: new selections active-only, new inactive reference409 REFERENCE_INACTIVE; unchanged existing inactive references may be resent, existing questions matched by ID may edit/reorder. No schema active flag/enum. Unknown type string fits shape, but CRUD1222–1243 documents unknown-reference409. Shape admissibility is not successful save or opaque-option preservation semantics. Preview explanation/type-transition confirmation remains UI requirement, not inferred API behavior. |
| Q32–33; L18 | CRUD1199–1280 describes field JSON Pointer, including `/questions/0/title` and `/questions/0/type_code`, request-array indices, form-level error when field absent, optional details;409 can combine NOT_UNIQUE/REFERENCE_NOT_FOUND/REFERENCE_INACTIVE. No changes persist on error. OpenAPI only declares422 HTTPValidationError; envelope ErrorItem lacks pointer grammar and success envelopes cannot represent null error data. Thus documentary error-envelope divergence remains, not a fabricated409 schema. O/design:54 adds `/questions/0/options/0/text` as planned mapping example; CRUD does not give that exact option example or guarantee particular errors for every nested field. Index escape rules beyond named JSON Pointer, deleted/reordered-target fallback, actual422 envelope and runtime mapping unverified. Input retention is client requirement, not server guarantee. |
| L05–10,L20 | Schema string fields; CRUD483–513 explicitly comma-separated names, not catalogs, no UUID/code payload, no separate label CRUD; POST defaults empty; PUT only replaces submitted fields; omitted preserves; empty clears associations not global labels; whitespace/commas also clears; null/arrays rejected by prose. **PUT schema allows null**, so no claim formal DTO enforces prose/no-null rule. |
| L11–14; SPEC1257 limit questions | CRUD515–517 explicitly **each field** max100 distinct labels, each name max150 after trimming, input string max16000. Schema independently enforces max16000 for each individual field (including nullable PUT string branch), not a combined card budget; it does not encode count150/count100. CRUD510–513 requires at least one parsed segments label for segment audience. Blank-only/comma-only segments therefore cannot satisfy that rule. No new nonempty rule for tags/operator_groups. |
| L06,L15–17 | CRUD499–517: trim label edges, skip empty elements, case-insensitive dedupe, reuse existing names/create missing in same transaction, independent namespaces per field; canonical saved spelling sorted case-insensitively and joined with comma-space; label is_active does not restrict use; quotes do not escape comma. This resolves blank-token behavior, response order and field scope documentary questions. Exact Unicode/casefold/collation/trim character repertoire and length-count implementation remain unspecified. No client algorithm mandated; interior whitespace collapse not explicitly promised. Audience switch preservation is the accepted UI/plan rule; omitted-field semantics support it but do not specify hidden unsaved-draft behavior. |

Other reachability-only parent context: schema permits nullable PUT top-level fields; CRUD1142–1144 validates final card, rejects null clearing required fields, saves root/nested data transactionally, and has no optimistic locking. CRUD1081 rejects empty object with422 EMPTY_PATCH despite schema allowing it. Display-rules whole replacement/defaults (1099), quiet-hour conditions and surface-audience conditions (1138–1140) were read because reachable but do not constitute a full MOS-1251 audit. No schema min questions, duplicate option-text policy or nested-ID ownership error taxonomy was found; absence is not approval to invent them.

UI-only Q01,Q03–08,Q16–20,Q29,Q34 and L01–04,L16–19 are not certified by this API lane: parent draft ownership, controls, confirmation, preview, input retention and test obligations remain their accepted R/S evidence. Seven supported types are not asserted to be an API enum from this closure; lookup was not re-audited.

## Q1 and residual unknowns

**If an existing unknown type has nonempty options, should saving preserve opaque options, omit them, or block save?**

Accepted SPEC1254 report and review preserve tension between unknown-code/data retention and non-tags nonempty-options exclusion. Fresh API evidence adds only unrestricted string type shape (1–50) and unrestricted type/options combination at schema level, alongside CRUD1137–1138 tags-only semantics and CRUD1222–1243 missing-reference conflict. None expressly defines the existing-unknown-plus-nonempty-options exception. Do not select preserve, omit, block or destructive cleanup. Parent was consulted and replied to finish unresolved; no specific accepted ruling supplied in reviewed evidence, no expanded collection authorized. Parent may seek a user decision after independent verification, not a newly invented blanket release gate.

Remaining unknowns: actual deployment/current freshness; actual422 vs explanatory envelope; nested-ID invalid/foreign/duplicate behavior and index handling after concurrent draft edits; precise Unicode counting/trim/casefold; whether optional schema defaults occur exactly as documented at runtime. Schema maxLength describes per-string characters, not a tested JavaScript/Python/backend counting equivalence. No release/feature checkbox closure.

## Architecture

Planned flow: MOS-1254 nested editor and MOS-1257 label chips → MOS-1251 draft/single save → MOS-1249 entity/transport → survey POST or partial-top-level PUT → full GET/PUT card baseline. Questions/options are full nested replacement with preserved existing UUIDs; labels are named association sets. Actual frontend/mocks were not inspected. Parent owns reconciliation/publication; no application-file change proposed here.

## Start Here

Read `docs/api/contracts/crud-api.md:483–517,1088–1144` next to `docs/api/contracts/managed-resources.openapi.json:5111–5540`. These isolate resolved label precision, nested replacement and remaining Q1 without conflating schema permissiveness with business approval.

## Hashes and provenance

SHA-256 computed over complete saved bytes; hashes do not mean complete semantic reads. r2 metadata: retrieved `2026-10-19T08:11:44.238Z`, URL `https://nchat-a-tech.mos.ru/api/control/openapi.json`, discovered from retained Swagger receipt; full decoded response, 420099 bytes, OpenAPI3.1.0/info0.1.0. This is a saved documentation snapshot, **not current live freshness or deployment validation**.

| Exact aliased input | SHA-256 |
|---|---|
| A/sources/api-live/r2/content.json | ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993 |
| D/openapi.json | c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7 |
| D/managed-resources.openapi.json | cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf |
| A/sources/api-live/r2/metadata.json | 444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba |
| D/crud-api.md | 4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058 |
| D/crud-api-2026-10-15.raw (hash only) | 91c8dc68fc1b602a64428d1d6f1d9c44a0e6a89eced226e4773853badf13954a |
| D/README.md | cb452cf8caf22245c7a62af5f16880e7b5c1b5aa6d591c5aa3e88261632929b3 |
| D/managed-resources.md | 529780f69c4451793d8a2af3cfb89cda9cc9c908d9a48c207de5ff21fb33435d |
| A/work-items/G2-FEEDBACK-MUTATION-CONTRACTS.md | dfefccdc3e4538ee4e4dbcd984885ec5b329b6e38abf46209cc7ed5ba8f45db4 |
| A/decisions.md (partial read) | 312d45d2eb7d465cf6819b143a1af79cba81ee3956c2785b370019ca2ab63acb |
| A/reports/REQ-G2-MOS-1254.md | 764084c9fed0d395911e5ee57198d5a1dc125d667f9f54d98ed9491a11032f92 |
| A/reports/REQ-G2-MOS-1257.md | bab215846ec9451dfe979865097509f2b5adce9cfd683d454bf63047e8d9979d |
| A/reports/SPEC-G2-MOS-1254.md | d63bd8618ea0f4ac2aaff2f18676cdb80a51c8f47c1b7b0d06f346361ba262ac |
| A/reports/SPEC-G2-MOS-1257.md | 2fc5d7be701420778b67cbff6e65df7731b22fc6c38da6e13c6f53b06a8d0e85 |
| A/reviews/R-REQ-G2-MOS-1254.md | cd771780ba1b02e458088bbe5cdef5b1560649f26946b100b0c45dc69947db3d |
| A/reviews/R-REQ-G2-MOS-1257.md | 229921653804c9db48f6dd8b67a034252402adaf2546fe07df6789b2187a05fe |
| A/reviews/R-SPEC-G2-MOS-1254.md | aaff5baae42713916c6a2df20417c4d9e31bf4dbaf5a7781369999c78ee1da89 |
| A/reviews/R-SPEC-G2-MOS-1257.md | 8d963bc8fc071e9a12f7f2bed8ac8685d80239184c92959d503d33da3b2527b9 |
| O/proposal.md | 5cc397bd1aab8722961df260fbc16216069816d3fe02d2a82eab09b9e41506ac |
| O/design.md | 0b15bcebfea15e35aca35a90c835a00efd892bb9a962fc16401892ca6017d91d |
| O/specs/feedback-api/spec.md | a783836ee1f191457d5331e87e2befaf809740fe39125ab302457645b9a591a3 |

All three expected contract hashes match. Original SPEC reviews describe pre-correction hashes; current corrected reports are separately identified above, consistent with D-065; no fresh independent ACCEPT invented.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently read three exact survey operations and complete 16-schema closure; compared both local contracts, joined accepted requirements, resolved documented label precision and retained Q1 without policy choice."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/c4b6be31-55d1-4433-871d-e24706064a72/API-G2-FEEDBACK-SURVEY-MUTATIONS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"read/find/scoped grep and read-only Python JSON extraction, transitive-ref comparison and SHA-256","result":"passed","summary":"Three operations and 16 schemas inspected; expected contract hashes matched; only approved operation-security delta observed."},
    {"command":"git status --porcelain=v1 --untracked-files=no; git diff --cached --name-only","result":"passed","summary":"Both empty; no repository writes or staging by this agent. Ignored files not certified by git status."},
    {"command":"tests/typegen/build/network/browser/business calls","result":"not-run","summary":"Forbidden by bounded read-only assignment."}
  ],
  "validationOutput": ["POST/GET/PUT confirmed; PATCH absent at assigned path items.","CRUD7.1 explicitly states independent per-field limits and blank-token handling.","Q1 unresolved; supervisor instructed no policy choice or expanded collection."],
  "residualRisks": ["Existing unknown-type nonempty-options policy remains unresolved in inspected evidence.","Formal nullable PUT labels and HTTPValidationError differ from explanatory business validation/envelope.","Saved documentation is not current live freshness or deployment evidence; no runtime verification."],
  "noStagedFiles": true,
  "diffSummary": "Configured external findings artifact only; repository unchanged by this agent.",
  "reviewFindings": ["Independent review pending; no feature closure or publication approval claimed."],
  "manualNotes": "Full common contract and API-owner proposal/design/spec read; accepted R/S joins reused with explicit provenance. Parent retains product and publication decisions; exact Q1 preserved after consultation. No saved-filter or registry-read audit performed."
}
```
