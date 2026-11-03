# Code Context

## Decision: REVISE — classification only

Core findings are supported. Minimal report correction: clearly mark the serialization/identity restatements in `A/reports/SPEC-G2-MOS-1254.md:42,54,92–94` as **optional verification/traceability refinements**, not missing owner requirements or mandatory planning corrections. `O/design.md:31` already excludes FK/local keys and preserves existing question/option UUID without restricting preservation to reorder; `O/specs/feedback-questions/spec.md:11` independently preserves existing UUID. No requirement must be repeated in every artifact. Keep these behaviors; no mandatory duplication in spec/tasks is warranted.

Also classify the particular post-reorder/deletion fixture (`A/reports/SPEC-G2-MOS-1254.md:98`) as a compatible test refinement, not a separately sourced acceptance obligation. The mandatory missing behavior is nested 409/422 placement and input retention, not a prescribed fixture or error-addressing algorithm. No further inventory or new product decision is needed to revise these classifications.

Aliases expand literally: `C=openspec/changes/reconcile-control-center-backlog`; `A=C/audit`; `O=openspec/changes/mos-1254-feedback-questions`; `E=openspec/changes/mos-1251-feedback-editor`.

## Key Code — independently verified findings

- **Unknown options: ACCEPT unresolved.** Jira `A/sources/jira-feedback/r1/content.json:57`, `/items/5/description`, AC2 excludes nonempty options for other types; AC5 preserves unknown type. `O/design.md:29,43` and `O/specs/feedback-questions/spec.md:9,11` do not reconcile opaque nonempty options. “Preserve original data” is not an explicit wire exception, omit rule or save-block rule. `O/design.md:53` does not resolve this case. Retain Q1; parent owns any authoritative ruling, not a newly imposed global gate.
- **Inactive selection: ACCEPT narrow clarification.** Jira AC5 says every new selection is active-only. Owner design:29/spec:11 explicitly restrict only new-question creation, while preserving saved inactive values. `E/design.md:37` and `E/specs/feedback-editor/spec.md:33` already specify active-only new references/selections. Clarify that switching an existing question to an inactive code is also disallowed; do not prohibit unchanged saved inactive editing/reorder or claim this rule is absent across the parent integration.
- **Nested errors: ACCEPT genuine local specificity gap.** Jira AC6 explicitly requires nested 409/422 at the appropriate question/option with input retained. `O/proposal.md:10`, owner spec:21,25, and `E/design.md:35`/tasks:6 cover retention and accessible parent errors, but not both statuses mapped to the correct nested item. Add that bounded owner scenario and verification; do not duplicate submit ownership or invent index/ID grammar or deleted-target fallback.
- **Cancellation: ACCEPT distinction.** Jira AC3 and owner design:29/spec:9 require confirmation. Owner spec:30 restores focus only. `E/tasks.md:6` and editor spec:13,27–28 concern disabled status, not question types. Rejecting an unconfirmed destructive mutation is a compatible test refinement; restoration after confirmed loss/undo is not approved by these clauses.
- **ID/edit/reorder and wire exclusions: behavior already covered.** Jira AC4 matches owner design:31, spec:11,13–16 and tasks:4,10. Preserve full-array replacement, existing IDs on edits/reorder, backend IDs for new elements, no outbound sort_order/FK/local keys. Optional explicit edit-only assertions are useful, not a newly missing semantic rule.
- **PATCH/PUT: ACCEPT discrepancy, no rewrite.** Jira description/API paragraph and AC4 name POST/PATCH; owner design:31, spec:11,16 and tasks:10 name PUT. Owner design:7 delegates contract provenance. Accepted requirements extraction is not API authority. Leave method resolution to parent/authoritative API join.

Optional only: explicit endpoint spelling, dependency staging annotation, repeated exclusion lists, edit-only/reorder-deletion fixtures and cancel-retention assertions. Existing ownership and scoped acceptance remain unchanged. I checked both requirements, all three owner scenarios and all five unchecked numbered tasks against the report; no omitted owner item or reason for a second matrix found.

## Files Retrieved / actual read limits

Complete reads:
- `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`.
- `A/work-items/G2-FEEDBACK-SPEC-WAVE.md:1–25`; `A/work-items/R-G2-FEEDBACK-SPEC-WAVE.md:1–21`. Other unit headings incidentally returned, not executed.
- `A/reports/SPEC-G2-MOS-1254.md:1–158`, `A/reports/REQ-G2-MOS-1254.md:1–133`, `A/reviews/R-REQ-G2-MOS-1254.md:1–66`.
- `O/proposal.md:1–34`, `O/design.md:1–53`, `O/tasks.md:1–10`, `O/specs/feedback-questions/spec.md:1–30`, `O/.openspec.yaml:1–2` (all owner artifacts).

Bounded reads: Jira content:50–58, full assigned description/all seven AC; `E/design.md:29–37`, `E/tasks.md:3–7`, `E/specs/feedback-editor/spec.md:8–14,26–33,58–66` (last range incidental, no rule-display conclusion). Targeted find found no main `feedback-questions` capability; no main-spec inventory repeated. No wiki reread/hash, API audit, archive/approval-history expansion, application reads, network/browser/tests/build/typegen or nested agents. Wiki references remain accepted-extraction evidence, not fresh primary verification. Initial combined shell output hit 50KB; omitted governing proposal and design:1–100 were reread separately, so no claimed full read relies on truncation. Targeted grep results had 500-character truncation; report had already been read fully.

## Architecture / Start Here

Start with owner design:29–43 and delta spec:9–21. Parent draft owns saving; MOS-1254 owns nested editing/error targets; MOS-1255 owns preview. Parent owns acceptance/publication, Q1 decision and authoritative method/error-contract join. This review authorizes neither feature closure nor implementation claims.

## SHA-256

Computed locally over full saved files (partial reads above remain partial). All corresponding hashes match the reviewed report; hashes certify bytes, not live freshness.

| File | SHA-256 |
|---|---|
| A/reports/SPEC-G2-MOS-1254.md | 09a258d74f546ff12b1c886077473a3d20936b155f4b06b8a969274c4a8f302e |
| A/reports/REQ-G2-MOS-1254.md | 764084c9fed0d395911e5ee57198d5a1dc125d667f9f54d98ed9491a11032f92 |
| A/reviews/R-REQ-G2-MOS-1254.md | cd771780ba1b02e458088bbe5cdef5b1560649f26946b100b0c45dc69947db3d |
| A/work-items/G2-FEEDBACK-SPEC-WAVE.md | e48969c1d6c09998909c400db7cb138839cf384cb3d8e6595c9e1e4e35e6419e |
| A/work-items/R-G2-FEEDBACK-SPEC-WAVE.md | 1194ceddd98f926755ba5995273b6f9c7abba7aee5d7194fbe70782ac53abfc2 |
| A/sources/jira-feedback/r1/content.json | 890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685 |
| O/proposal.md | 87cfa93c0aee962cdc7371784a6e22f37c3d8413f1c9904f05c051112e196e41 |
| O/design.md | 181f2800f8e8f359147ef9c9d3a6eb4f3d4daafa20324dd3b8e1cf0c23d54e10 |
| O/tasks.md | 2920f54aba3994e856679db78d4706c553e7a97be0c17d420643b7f3d72fba65 |
| O/specs/feedback-questions/spec.md | eeb2d92c74667f09a97d933390176b2771d39a1596a4f0c21cf0e23e39c9d27c |
| O/.openspec.yaml | 1dfdca412094f24473d8b842866201ec26f200b29b17064b03f1e4982c35a7b9 |
| C/proposal.md | 1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879 |
| C/design.md | 632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828 |
| C/tasks.md | a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83 |
| C/specs/control-center-backlog-reconciliation/spec.md | a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36 |
| E/design.md | dfd986336cf1b687206752fb8d436c162dd2c38e8ba87b807809c1b5fbd9c028 |
| E/tasks.md | 67f76db911e4bd852d2dfa4d24d5bcd64e57aacb8693a586210c340c803f1906 |
| E/specs/feedback-editor/spec.md | 03e584e4c9d6d1d99f9e0949949dce92b1fd1cc83a5378afaf67fe86ba4b31ee |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent full-owner review completed; REVISE limited to separating existing coverage/optional fixtures from mandatory corrections."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/4c8350f6-00b1-4897-abcc-c15158018af4/R-SPEC-G2-MOS-1254.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"read/find/targeted grep/wc/nl/sed","result":"passed","summary":"Full owner and governing documents; exact Jira and bounded parent seams; truncated governing output recovered."},{"command":"sha256sum 18 inputs","result":"passed","summary":"Hashes recorded."},{"command":"tests/build/typegen/network/browser","result":"not-run","summary":"Prohibited by documentary assignment."}],
  "validationOutput": ["Both owner requirements, three scenarios and five unchecked tasks accounted for; no new inventory."],
  "residualRisks": ["Unknown-type nonempty options remain unresolved; method/error grammar need authoritative evidence.","Saved-source freshness, omitted Jira fields and external approval provenance are not established; wiki not independently reread."],
  "diffSummary": "Only configured external review artifact written; project and staging untouched by this reviewer.",
  "reviewFindings": ["REVISE: mark already-covered wire/identity restatements and particular boundary fixtures optional; core Q1/inactive/nested-error/method findings accepted."],
  "manualNotes": "No product ruling or publication performed. Existing git staging state was not inspected; author supervisor conversation not independently attested. Parent owns decisions."
}
```
