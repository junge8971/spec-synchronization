# Code Context

## Result — ACCEPT

Fresh independent documentary review of **R-API-G2-FEEDBACK-SURVEY-MUTATIONS only**. The report’s substantive conclusions are supported. **Mandatory corrections: none.** Parent retains acceptance/publication authority; this is not feature or deployment acceptance.

Minor locator cleanup (non-blocking): in the report’s requirement-joins table, MOS-1249 design’s explicit PUT ruling is at line **23**, operation table **45–52**, and nested option-pointer example **54**, not 24/38–50/50. These are citation offsets, not substantive errors.

## Key Code / verified findings

- Independently extracted complete `POST /api/control/api/v1/managed-resources/feedback/surveys`, detail `GET` and `PUT` at `/{entity_id}` from saved r2. Exact JSON pointers are `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys/post` and `/paths/~1api~1control~1api~1v1~1managed-resources~1feedback~1surveys~1{entity_id}/{get,put}`. Path-item keys are `post` and `get,put,delete`; no PATCH. `FeedbackSurveyPatch` and `patch_fb_survey…put` do not change the HTTP method. MOS-1249 design:23 explicitly selects published PUT. Saved Jira `/items/5/description` and `/items/8/description` really say PATCH: historical discrepancy, not authority for substitution or new product approval.
- Independently traversed and read all **16** reachable `/components/schemas/` objects: `FeedbackSurveyCreate`, `FeedbackSurveyPatch`, `FeedbackSurveyResponse`, `FeedbackQuestion`, `FeedbackQuestionResponse`, `FeedbackOption`, `FeedbackOptionResponse`, `FeedbackDisplayRules`, `FeedbackDisplayRulesResponse`, `TsamResponseSchema_EntityCreatedResponse_`, `TsamResponseSchema_FeedbackSurveyResponse_`, `EntityCreatedResponse`, `ResponseCode`, `ErrorItem`, `HTTPValidationError`, `ValidationError`. No unresolved refs. All complete objects equal both local contracts. All three operation objects equal both local versions after removing **only** operation `security`; saved OR versus approved local AND remains separately identified, not overturned.
- Request schema constraints/nullability/additionalProperties and response asymmetries are accurately summarized. POST returns 201 ID envelope; GET/PUT return 200 full-card envelope; all three formally declare only 422 besides success. CRUD:1081 rejects `{}` despite optional Patch fields. Label null branches are schema-admissible but CRUD:510–517 rejects null/arrays; do not generalize that rejection to legitimately nullable fields.
- CRUD:1088–1105 explicitly makes PUT partial **top-level**, replaces supplied questions/options with the full final nested collection, preserves existing IDs, omits IDs for new entries and uses array order. Empty questions deletes their options too. These behaviors are explanatory semantics, not consequences of optional schema fields alone.
- CRUD §7.1:483–517 explicitly confirms **per-field** 100 distinct labels, 150 characters **after edge trimming**, and 16000 characters in input string. It skips empty tokens, deduplicates case-insensitively, reuses saved spelling, sorts case-insensitively and joins with comma-space. Each field has an independent label namespace. Omission preserves; empty or spaces/commas-only clears associations, not global labels. Parsed segment audience requires at least one segment. Exact Unicode/casefold/collation/counting and interior-whitespace collapse are not specified. Report correctly resolves the bounded label questions without inventing a client algorithm.
- CRUD:1199–1296 describes error envelope, named JSON Pointer paths and request-array indices, combined conflict codes and no persisted changes on error. Formal `ErrorItem.field` has no pointer pattern; formal 422 is `HTTPValidationError`, not that envelope. No fabricated 409 schema, per-field error guarantee or runtime index-remapping guarantee appears in the report.
- **Q1 remains unanswered:** “If an existing unknown type has nonempty options, should saving preserve opaque options, omit them, or block save?” CRUD:1137–1138 says tags require nonempty options and other types omit/empty; CRUD:1222–1243 gives generic unknown-reference409. Neither states the existing-unknown/nonempty-options exception. Unrestricted type strings in the schema establish shape only. D-065 explicitly forbids choosing preserve/omit/block without evidence or user decision; accepted SPEC1254:70–82 retains the same tension. No-policy conclusion is justified within inspected evidence; no exhaustive absence ruling or new release gate follows.

## Files Retrieved / actual read limits

Exact roots: `C=openspec/changes/reconcile-control-center-backlog`, `A=C/audit`, `D=docs/api/contracts`, `O=openspec/changes/mos-1249-feedback-api`.

1. `A/work-items/R-G2-FEEDBACK-MUTATION-CONTRACTS.md` (complete), `A/work-items/G2-FEEDBACK-MUTATION-CONTRACTS.md` (complete); adjacent filter instructions incidental, not executed.
2. `A/reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md:1–162` (complete reviewed artifact).
3. `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`; governing authority. Initial combined output was truncated; missing proposal/design beginnings were reread directly.
4. `A/decisions.md:1–16` (D-065 and D-064 only).
5. `O/proposal.md:1–32`, `O/design.md:1–81`, `O/specs/feedback-api/spec.md:1–38` (complete); explicit ruling and approval boundary.
6. `D/crud-api.md:74–153,223–246,415–518,995–1144,1194–1296`; assigned explanatory semantics, with incidental surrounding resource rows only. `D/README.md:1–33`, `D/managed-resources.md:1–55`, `A/sources/api-live/r2/metadata.json:1–22` (complete).
7. `A/sources/api-live/r2/content.json`, `D/openapi.json`, `D/managed-resources.openapi.json`: parsed complete saved files, semantically read only the three full operations, their path-item keys, complete 16-schema closure above and r2 AdminToken/AccessToken security definitions. Local equivalence checked structurally; no whole-contract inventory or DELETE audit.
8. Targeted, sometimes 500-character-truncated keyword excerpts in `A/reports/{REQ,SPEC}-G2-MOS-{1254,1257}.md` were navigation/joins only, not full reads. Material passages reread untruncated: `SPEC-G2-MOS-1254.md:70–83`, `REQ-G2-MOS-1254.md:119–126`, `REQ-G2-MOS-1257.md:55–72`. Original requirement/spec reviews were **hashed only**, not independently re-reviewed. D-065 supplies their disposition.
9. `A/sources/jira-feedback/r1/content.json`: parsed saved packet; semantic read restricted to full `/items/5/description` (MOS-1254), and PATCH/limit matching lines of `/items/8/description` (MOS-1257). No wiki/attachments/source acquisition or broader editor audit.

## Hashes and provenance

SHA-256 over complete bytes is not full semantic reading. All **21** hashes listed in the reviewed report were independently recomputed and matched, including the raw CRUD file and prior reports/reviews that were hash-only here. Key reproducibility anchors:

| File | SHA-256 |
|---|---|
| A/reports/API-G2-FEEDBACK-SURVEY-MUTATIONS.md | e869082c9e4438c40923871a87707b815cab8d919e56ba05ab0e2598f2c3718f |
| A/sources/api-live/r2/content.json | ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993 |
| D/openapi.json | c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7 |
| D/managed-resources.openapi.json | cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf |
| D/crud-api.md | 4dde67125d36692cb05fcbb9b9b6e842f95717118f999c471cb5e2b393907058 |
| A/sources/api-live/r2/metadata.json | 444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba |
| A/decisions.md | 312d45d2eb7d465cf6819b143a1af79cba81ee3956c2785b370019ca2ab63acb |
| O/design.md | 0b15bcebfea15e35aca35a90c835a00efd892bb9a962fc16401892ca6017d91d |
| A/sources/jira-feedback/r1/content.json | 890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685 |

r2 metadata identifies a saved decoded documentation response from `https://nchat-a-tech.mos.ru/api/control/openapi.json`, retrieved `2026-10-19T08:11:44.238Z`, 420099 bytes, OpenAPI3.1.0/info0.1.0. This review verifies saved bytes and bounded documentary consistency, **not current live freshness, acquisition authenticity beyond the retained receipt, or deployment**.

## Architecture / Start Here

Nested editor and labels feed the parent survey draft; MOS-1249 owns transport; POST→GET and partial-top-level PUT yield the full baseline. Open `docs/api/contracts/crud-api.md:483–517,1088–1144` alongside the exact schemas before publication. No implementation was inspected. Residual questions remain Q1, actual error envelopes/index handling, nested-ID edge cases, Unicode precision and runtime behavior.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent three-operation/16-schema verification, direct CRUD7.1 and mutation/error clauses, existing PUT ruling and Q1 checked; ACCEPT with no mandatory corrections."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/fb27129a-c036-47f2-b4b6-6f8dbd5a0b32/R-API-G2-FEEDBACK-SURVEY-MUTATIONS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"read/find/scoped grep; read-only Python JSON/ref traversal, equality and SHA-256","result":"passed","summary":"Three operations and 16 schemas verified; all 21 reported hashes matched."},
    {"command":"git diff --cached --name-only","result":"passed","summary":"Empty staged-file list."},
    {"command":"tests/build/typegen/network/browser/business calls","result":"not-run","summary":"Forbidden by documentary-only assignment."}
  ],
  "validationOutput": ["ACCEPT; no mandatory corrections; minor non-blocking MOS-1249 line-reference cleanup noted."],
  "residualRisks": ["Q1 remains unresolved; no preserve/omit/block policy selected.","Saved documentation does not verify deployment/current freshness or actual 422/index behavior.","Exact Unicode/whitespace/counting and nested-ID edge behavior remain unspecified."],
  "noStagedFiles": true,
  "diffSummary": "Only configured external review artifact written; no project edits.",
  "reviewFindings": ["No blockers; optional locator cleanup only."],
  "manualNotes": "Fresh bounded primary-source review, not a new inventory. Parent accepts and publishes; no feature completion or expanded product policy authorized. Hash-only inputs and truncated navigation excerpts are explicitly distinguished from semantic reads."
}
```
