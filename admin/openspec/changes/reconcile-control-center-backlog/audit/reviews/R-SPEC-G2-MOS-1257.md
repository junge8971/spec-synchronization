# R-SPEC-G2-MOS-1257 — REVISE

Core omission/trim findings accepted. Minimal revision: distinguish genuinely missing semantics from optional repetition in the publication package. Parent owns decisions/publication; no feature acceptance.

# Code Context

`C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `C/audit`; `O` = `openspec/changes/mos-1257-feedback-labels`. Paths below expand literally.

## Required correction to the reviewed report

At `A/reports/SPEC-G2-MOS-1257.md:42–44,76,89–91`, downgrade mandatory repetition of all five J-AC6 test families in task2.1 and mandatory separate quoted-comma/no-null scenarios to **optional traceability/precision**. The report itself recognizes that tasks1.1–1.2 distribute these checks. `O/tasks.md:3–4,8` already combines length/empty/normalization/audience/no-global-request verification with targeted unit/component acceptance; `O/specs/feedback-labels/spec.md:9` expressly prohibits null and says comma is *always* a separator. No missing behavior is established merely because task2.1 does not repeat the list or quotes lack a named scenario. A short cross-reference is sufficient if desired; do not require duplicate lists or a particular scenario layout.

Preserve these minimal substantive corrections:
- **Omission:** explicitly distinguish omitted field → previous associations retained from `""` → associations cleared. Missing throughout the complete owner. Jira `A/sources/jira-feedback/r1/content.json:84`, `/items/8/description`, AC3 is exact evidence. Audience preservation is not equivalent. Add a bounded verification case without requiring a new standalone scenario.
- **Trim:** add “after trim” to the 150-character limit in `O/design.md:29`, delta `:9`, and task1.1 (`O/tasks.md:3`). AC4 explicitly supplies it; assigning trim to backend does not specify when the length limit applies.
- **Consistency/precision:** align design/task “100 labels” with delta's existing “100 distinct”; clarify delta `:11` as at least one parsed **segment** label for segment audience (AC4). This is not a new generic nonempty constraint on tags/operator groups. No choice of blank-token mechanics is authorized.

The proposal may remain unchanged. Explicit quote wording, a separate omission scenario, and repetition of no-null or existing test families are optional, not acceptance blockers.

## Key evidence / accepted conclusions

- `O/design.md:29`, delta `:9`, tasks `:3–4` explicitly settle name strings/no generated API codes/no separate CRUD and association-only deletion. Retain this existing decision, not invented Jira-over-wiki precedence. API owner design `openspec/changes/mos-1249-feedback-api/design.md:7–10` confirms prototype composition versus API-operation authority; published API itself was not audited.
- Jira AC5 and owner design `:29`, delta `:13–16`, task1.2 assign normalization to backend and canonical names to UI. No client normalization algorithm, Unicode equality, canonical ordering or unsaved-draft restoration promise follows.
- AC4 and the complete owner do not establish per-field versus aggregate limits, character-count convention, measurement timing or blank-token handling. Keep these as bounded contract-verification details, not new automatic product gates.
- Wiki `/text[3844:4893]`, `[7848:8140]`, `[9598:11134]` confirms prototype generated codes/code arrays and in-memory limitations; `[20813:22292]` identifies dynamic labels outside dictionary catalogs and example values. No mandatory suggestions, catalog lookup, defaults or code display should be added.
- All two owning requirements, two scenarios and five numbered unchecked tasks are accounted for in the reviewed report. Accessibility, release evidence, saved-association retention and input retention already exist; none should be repackaged as newly missing scope.

## Files Retrieved / actual read limits

Full semantic reads:
- `A/reports/SPEC-G2-MOS-1257.md:1–142`; `A/reports/REQ-G2-MOS-1257.md:1–135`; `A/reviews/R-REQ-G2-MOS-1257.md:1–61` (actual EOF is 61, not the reviewed report's stated 64).
- `O/proposal.md:1–34`, `O/design.md:1–53`, `O/tasks.md:1–10`, `O/specs/feedback-labels/spec.md:1–25`. Path discovery found exactly one delta; no matching main feedback-labels capability.
- `C/proposal.md:1–30`, `C/design.md:1–133`, `C/tasks.md:1–45`, `C/specs/control-center-backlog-reconciliation/spec.md:1–108`.
- `A/work-items/G2-FEEDBACK-SPEC-WAVE.md:1–25`, `A/work-items/R-G2-FEEDBACK-SPEC-WAVE.md:1–21`.

Bounded reads: `A/decisions.md:1–9` (D-064); complete Jira `/items/8` (file lines77–85); decoded wiki `/text` zero-based half-open Unicode-character slices `[3844:4893]`, `[7848:8140]`, `[9598:11134]`, `[20813:22292]`; API-owner design `:5–30`; `openspec/changes/mos-1251-feedback-editor/tasks.md:1–7` for draft/single-save seam. One combined command exceeded output limits; its omitted beginning was reread from the tool's saved output (lines1–138), completing the governing reads. No reliance on truncated clauses.

No metadata, full wiki, attachments, approval history, archive, application code or published API inspection. Detailed UUID/model inconsistency remains inherited accepted extraction evidence, not freshly re-audited here. Hashing full files is not full semantic reading.

## Architecture / Start Here

Private chips → MOS-1251 draft/single save → name strings → backend normalization → canonical saved UI. Start with `O/specs/feedback-labels/spec.md:9–16` and Jira AC3–4; these isolate the real omissions without reopening settled scope.

## SHA-256 (complete bytes, independently recomputed)

All corresponding input hashes match the reviewed report. These establish saved revisions, not live freshness.

| Input | SHA-256 |
|---|---|
| A/reports/SPEC-G2-MOS-1257.md | `d9d10a5adf32a291dad088d9755d540ec384db68a2b39ea46932d9c1b3ca31ff` |
| A/reports/REQ-G2-MOS-1257.md | `bab215846ec9451dfe979865097509f2b5adce9cfd683d454bf63047e8d9979d` |
| A/reviews/R-REQ-G2-MOS-1257.md | `229921653804c9db48f6dd8b67a034252402adaf2546fe07df6789b2187a05fe` |
| O/proposal.md | `00fef67d22a0c465537f081c16948042d0980641198736d52f3e855780a60846` |
| O/design.md | `696819963b5df1695641c2fdf0ee6849591ca103b97eeb23e0375aaae062a585` |
| O/tasks.md | `173a3d33a3242cd2a4cf1540f3fd6f89c027182359f46045f909966955925899` |
| O/specs/feedback-labels/spec.md | `7b3704e24f3f64ac9d5d08e20a152bfd245c3b02585c87a5a91e5b641060e24c` |
| A/sources/jira-feedback/r1/content.json | `890f70f0df89675433906751b98ee6c30df9130784550ff83d306a7dd316a685` |
| A/sources/wiki-247734813/r1/content.json | `d47db6bfc15f5f4a881c777ec78892161ed6be000c6cdf1c5c61ab4c7030c7d7` |
| C/proposal.md | `1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879` |
| C/design.md | `632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828` |
| C/tasks.md | `a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83` |
| C/specs/control-center-backlog-reconciliation/spec.md | `a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36` |
| A/work-items/G2-FEEDBACK-SPEC-WAVE.md | `e48969c1d6c09998909c400db7cb138839cf384cb3d8e6595c9e1e4e35e6419e` |
| A/work-items/R-G2-FEEDBACK-SPEC-WAVE.md | `1194ceddd98f926755ba5995273b6f9c7abba7aee5d7194fbe70782ac53abfc2` |
| A/decisions.md | `759351a44478a4e1874d75acb71c8efccd753c388e3fe5d363fc9aaccb488ff7` |
| openspec/changes/mos-1249-feedback-api/design.md | `0b15bcebfea15e35aca35a90c835a00efd892bb9a962fc16401892ca6017d91d` |
| openspec/changes/mos-1251-feedback-editor/tasks.md | `67f76db911e4bd852d2dfa4d24d5bcd64e57aacb8693a586210c340c803f1906` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent full-owner and exact source review completed; REVISE limited to separating optional repetition from required omission/trim corrections."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/4c8350f6-00b1-4897-abcc-c15158018af4/R-SPEC-G2-MOS-1257.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read/find, numbered selective reads, Python JSON slices and SHA-256","result":"passed","summary":"Owner and governing documents read completely; primary clauses and dependency seams checked; input hashes reproduced."},{"command":"Tests/build/network/browser","result":"not-run","summary":"Prohibited documentary assignment."}],
  "validationOutput": ["Two requirements, two scenarios and five tasks accounted for; omission and after-trim absent; existing decisions retained."],
  "residualRisks": ["Saved flattened sources only; live freshness, omitted evidence and deployed API unverified.","Count scope and normalization mechanics remain bounded contract unknowns."],
  "noStagedFiles": true,
  "diffSummary": "Configured external review only; no project edits or staging operations.",
  "reviewFindings": ["REVISE: remove mandatory duplicate test-list/scenario wording; preserve substantive omission/trim corrections."],
  "manualNotes": "Read-only independent documentary review, not implementation or API acceptance. Parent owns final decisions and publication. No nested agents or prohibited checks."
}
```
