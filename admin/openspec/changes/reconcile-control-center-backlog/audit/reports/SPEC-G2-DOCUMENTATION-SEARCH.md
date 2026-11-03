# Code Context

## Result — baseline row 19 ownership resolved, evidence remains bounded

`documentation-search` is explicitly introduced by `openspec/changes/archive/2026-10-13-mos-906-documentation-search-url/proposal.md:3–20`, not inferred from similar navigation names. Its five requirements and twelve scenarios are the same requirement body as the current main spec (exact local text comparison passed). The archive's companion shell delta explicitly delegates search selection/fallback to this capability. **No textual correction or new product change is supported by this comparison.** Parent/fresh reviewer retain acceptance; this report does not close G2 or any feature.

MOS-906 is an accepted-inventory member of MOS-784, and its saved title independently matches documentation search plus URL persistence. This establishes identity/provenance, not complete Jira acceptance criteria: the accepted member snapshot omits descriptions/comments/custom acceptance fields. SH011 and RT009 now have an exact, explicitly declared specification join, but remain **partial static navigation/restoration evidence**, not proof of all search requirements.

## Files Retrieved

Paths below are repository-relative. Abbreviations expand literally: `C` = `openspec/changes/reconcile-control-center-backlog`; `A` = `openspec/changes/reconcile-control-center-backlog/audit`; `O` = `openspec/changes/archive/2026-10-13-mos-906-documentation-search-url`. These prefixes apply to the hash table too.

| Exact file | Actual semantic read coverage | Why |
|---|---|---|
| `C/proposal.md` | 1–30, complete | Authority/no product behavior change |
| `C/design.md` | 1–133, complete | Evidence separation and publication gates |
| `C/tasks.md` | 1–45, complete | G2–G5 remain open |
| `C/specs/control-center-backlog-reconciliation/spec.md` | 1–108, complete | Governing reconciliation requirements |
| `A/work-items/G2-OWNERSHIP-WAVE.md` | 1–19, complete | Common contract and assigned section |
| `openspec/specs/documentation-search/spec.md` | 1–87, complete | Exact current owner and all scenarios |
| `openspec/specs/control-center-shell/spec.md` | 91–124 only | Current explicit cross-capability delegation |
| `O/proposal.md` | 1–28, complete | MOS-906 and capability declaration |
| `O/design.md` | 1–57, complete | URL transitions, focus, revalidation, exclusions |
| `O/tasks.md` | 1–43, complete | Task mapping and historical receipts |
| `O/specs/documentation-search/spec.md` | 1–85, complete | Originating five requirements/twelve scenarios |
| `O/specs/control-center-shell/spec.md` | 1–30, complete | Exact bridge from SH011/RT009 |
| `A/reports/LOCAL-001.md` | 1–194, complete | Main ID at 55; exact archive inventory at 162 |
| `A/decisions.md` | 1–22 and 395–412 only | D-062, D-010, D-009 qualifications; adjacent context |
| `A/reports/G2-MAIN-CAPABILITY-JOINS.md` | 1–30 and 65–164 only | SH/RT chains, row19 at 105, N18 at 158 |
| `A/reviews/R-G2-MAIN-CAPABILITY-JOINS.md` | 110–159 only | Row19 at 124 and rationale at 155 |
| `A/reports/IMPL-MOS-904.md` | 1–105, complete | SH011 = REQ-MOS-904-011, row at 56 |
| `A/reports/IMPL-MOS-905.md` | 1–112, complete | RT009 = REQ-MOS-905-009, row at 67 |
| `A/reviews/R-IMPL-MOS-904.md` | 1–102, complete | Independent bounded acceptance; row011 at 56 |
| `A/reviews/R-IMPL-MOS-905.md` | 1–97, complete | Qualified mapping; row009 at 50 |
| `A/reports/JIRA-MOS-784.md` | 1–55, complete | Existing membership/source pointers, row at 22 |
| `A/reports/G1-INVENTORY-SOURCE-CROSSWALK.md` | 185–230 only | MOS-906 I(137), U source-detail status at 227 |
| `A/sources/jira-hierarchy/r1/content.json` | 1–35, complete; only results[18] used | Already accepted MOS-784 membership |
| `A/sources/jira-hierarchy/r1/metadata.json` | 1–11, complete | Retrieval/extraction and digest |
| `A/sources/jira-member-index/r1/content.json` | 1189–1197 only | Exact MOS-906 item, not recensus |
| `A/sources/jira-member-index/r1/metadata.json` | 1–16, complete | Selected-field limitations/digest |

No app code, test body, API schema, new external source or unrelated archive was inspected. Archive metadata `.openspec.yaml` was discovered but not read or used. Initial filename listing was truncated and is not absence evidence. Hashing whole files below does not imply semantic reads beyond the ranges above.

## Key Code / exact documentary ownership

No code was inspected in this lane. Critical normative joins:

- `O/proposal.md:3`: MOS-906 requires reproducible documentation search by direct link; existing search versus local-only query is historical motivation, not a claim about today's code.
- `O/proposal.md:15–20`: new `documentation-search`; modified `control-center-shell` fallback.
- `openspec/specs/documentation-search/spec.md:11`: **search MUST NOT require server API**.
- `O/specs/control-center-shell/spec.md:5` and current shell `spec.md:93`: search fallback is determined by **documentation-search**; first matching article for invalid selection, no article for empty results.
- `O/design.md:13–35`: URL is source of state; input/clear/correction replace history, manual selection pushes, direct/reload/POP preserve a valid article. `q` is stored verbatim; only matching normalizes. Repeated q/article read first, writes collapse the changed key; unrelated repetitions remain. Legacy `query` is not an alias.
- `O/design.md:17` and main documentation `spec.md:79–82`: local q/article transitions must not retrigger root checking; initial confirmation and explicit retry/revalidate remain. This is a documentation navigation integration requirement, not authority to change auth.

### MOS-906 provenance, without source expansion

`A/sources/jira-hierarchy/r1/content.json:26`, JSON `$.results[18].children[3]`, names MOS-906 under MOS-784 (`Q key result`, not a literal Epic). Existing accepted inventory authority is inherited from the assignment/D-062 and `A/reports/JIRA-MOS-784.md:7–24`; no new hierarchy census was performed.

`A/sources/jira-member-index/r1/content.json:1189–1196`, JSON `$.items[137]`, gives `[FE][Документация] Завершить поиск по документации и сохранить результат в URL`, Development task, Ready for test, updated `2026-10-13T21:33:56.235+0800`, and empty saved subtasks. Hierarchy retrieved `2026-10-16T11:08:08.629Z`; index retrieved `2026-10-16T11:20:38.570Z`. Both current saved-file digests match their metadata. This is saved extraction consistency, not remote freshness/authenticity or status-based completion. Parent relation comes from hierarchy, not an invented REST parent field. G1 crosswalk row227 still says U for detail source availability; this report supplies a local-spec ownership join, not missing Jira body content.

## Requirement-to-task-to-existing-evidence map

Main-spec line ranges below identify every requirement and scenario. Originating documentation delta has the same body at main line minus two. All referenced archive checkboxes are historical records, not newly accepted execution results.

| Requirement / all scenarios | Exact task ownership in `O/tasks.md` | Existing qualified evidence | Actual remainder |
|---|---|---|---|
| Local documentation search, main 9–21: block text; short query | 1.1 (line3) short-query/fallback; 3.2 (line16) title/summary/paragraph/note/list/steps and threshold preservation | SH011 establishes catalog-derived menu order and selected/fallback destination, **not** normalized all-block search. Archive design describes reused search; archive spec fully owns it. | SH011/RT009 do not establish all block headings/list/step matching, case/trim threshold, full article/group order or hiding empty groups. Current static conformance unassessed, not missing behavior. |
| Query/article restored from URL, main 23–35: valid manually selected second result; missing/unknown/mismatched article fallback | 1.1–1.2 (3–4), 3.1 (15) | SH011 requested/first/null selection and separately mounted selected/unknown article assertions. RT009 actual route-module legacy redirect with article/search restoration and Back/Forward. | Evidence supports restoration seam; does not independently establish entire valid-second-result/reload/POP matrix, every missing/mismatched correction branch, empty-result removal, or parameter-free ordinary entry. Browser reload/deployment remains unverified. |
| Query changes select first result, main 37–54: change after manual selection; clear; history/unrelated repeats | 1.2 (4), 2.1 (8), 3.1 (15) | RT009 covers preserved q/article/repeated filters and history for legacy navigation. SH011 covers article links/basename. | Alias REPLACE is not proof of input REPLACE/manual PUSH, atomic q/article updates, clear selecting catalog first, or manual selection persistence until next input. All those remain unassessed in reused static reports. |
| Empty results hide article, main 56–68: typing/direct-link no results; recovery | 1.1–1.2 (3–4), 2.2 (9) | SH011 observes requested/first/null selector; shell explicitly delegates no-results behavior. | Null selection alone does not prove accessible status, hidden article, article removal while q remains, both entry modes, or recovery. No defect/absence conclusion. |
| Accessible interaction, main 70–87: mobile typing; application-shell typing; manual mobile selection | 2.3 (10), 4.1–4.2 (22–23); 3.1 supports history | SH011 menu keyboard/focus/mobile sidebar closure is adjacent UI evidence, not documentation input focus. Historical archive 4.1 and receipts 36–43 specifically record root/clientLoader regression work. | Neither reused static lane establishes continuous typing DOM identity/focus/no scroll/no repeated checking or /me, manual article focus/scroll, desktop/first-entry no-scroll, status/selection assistive semantics, or preserved explicit session retry. Historical regression receipt is not fresh proof. |

### Exact bridge to SH011 and RT009

- **SH011:** `A/reports/IMPL-MOS-904.md:56` → `A/reviews/R-IMPL-MOS-904.md:56,73` → D-010 (`A/decisions.md:395–397`). Join to shell `spec.md:91–103` and originating shell delta `:3–15`: first six catalog entries, canonical article/all-sections links, basename, closure, unknown article fallback. The explicit delegation at current shell `:93` then connects the requested/first/null destination evidence to documentation main `:23–35,56–68`. Reused underlying locators are `app/widgets/documentation/model/documentation-search-params.ts:6–21` and `app/widgets/documentation/ui/documentation.test.tsx:166–190,384–390`, **not reopened here**. Reviewer qualification: destination is mounted alone; quick-menu → actual root → article integration is not established.
- **RT009:** `A/reports/IMPL-MOS-905.md:67` → `A/reviews/R-IMPL-MOS-905.md:50` → D-009 (`A/decisions.md:401–403`). Join to shell `spec.md:105–113` and originating shell delta `:17–25`: legacy article/search URLs redirect without intermediate legacy history entry. Reused `app/routes/documentation-navigation.test.tsx:8–51` uses actual route modules and asserts article/search/repeated-filter restoration and history, **not reopened here**. This is partial support for documentation main `:23–35,51–54`, not search-input or full application-root verification.
- D-009 accepts RT with review corrections, not an unqualified ACCEPT: competing surface stub coverage exists and approved home fallback is already settled. Those unrelated corrections are preserved and not re-audited. Neither correction invalidates RT009.

## Architecture and applicability

Normative flow: built-in article catalog → existing local substring search → URL q/article selection → documentation widget rendering/focus; shell owns menu and legacy route entry, explicitly delegates search semantics. Archive design keeps URL parsing in `widgets/documentation/model`, UI operations in its handlers, and catalog search behind public `entities/documentation` API. These are documentary ownership statements, not freshly verified source wiring.

**API lane:** no business/article/search backend operation is applicable to these five requirements: main line11 forbids requiring one, archive proposal 26/design 11 exclude new API/search service. Do not create an article-service gap or inspect schemas to satisfy a synthetic lane. Existing session confirmation remains an applicable integration prerequisite for the shell-typing scenario; absence of repeated /me is a negative navigation-side-effect obligation, not a new endpoint or cancellation of auth checks. Existing initial confirmation and explicit revalidation remain required.

**Runtime/implementation lanes:** applicable (URL/history/filter/accessible focus behavior is real user-facing behavior), with accepted static evidence only at the limited SH011/RT009 seams. No blanket N/A, full capability acceptance or missing-implementation claim follows.

**Archive validation versus present evidence:** `O/tasks.md:25–43` records historical typecheck/lint/format success, split Node retry success, a post-fix whole-suite surface timeout and passing isolated retry, and targeted documentation 5-file/40-test success. The whole post-fix run was not uniformly green. Those receipts and eleven checked tasks establish historical recording only. Tests/build/api:check were not run here; the archive itself says build/api:check/E2E were not run. Reading archives cannot verify current source freshness, runtime, browser history or deployed host behavior.

## Concrete disposition for parent integration

1. Replace row19's **unknown exact identity/ownership** explanation with the explicit MOS-906 archive + current shell delegation chain above, subject to fresh review. Main/delta requirement ownership and task traceability are resolved; no orphan or duplicate owner was found in the inspected scope.
2. Keep external requirement extraction **partial**: saved Jira membership/title plus complete local normative requirements, but no MOS-906 description acceptance-body parity. Keep static implementation **partial** at SH011/RT009 only, all runtime unknown. API disposition is **no documentation business API required**, with existing session dependency separately retained. Do not represent this as five fully covered lanes.
3. Planning artifact action: **keep/no-op**. Current and originating documentation requirement bodies match exactly, and current shell carries the intended delegation. No contradictory approved scope or material missing input prevents this bounded answer; no product choice is needed.
4. Remaining evidence gaps are exactly the unassessed clauses in the matrix, not new product requirements. Parent may retain them as bounded coverage limitations; neither a full docs re-audit nor new reports/tests are automatically commissioned. Missing external body freshness is a source limitation, not a reason to infer no search implementation.

## Start Here

Open `openspec/specs/documentation-search/spec.md:9–87` with `openspec/changes/archive/2026-10-13-mos-906-documentation-search-url/proposal.md:15–20` and shell delta `specs/control-center-shell/spec.md:3–5`. These resolve the precise ownership seam without repeating navigation code inspection.

## Actual input hashes

SHA-256 computed locally after reads; partial-read files hashed whole. No Git HEAD/index verification or baseline equality claim. Reference HEAD from assignment remains `bc0d9800f25a90989b9c73c76f91996f8300f1d3`, not independently checked.

| Exact expanded-prefix path | SHA-256 |
|---|---|
| `C/proposal.md` | `1a97715e2566329143febbb509e934a88b4ecc478628fac559da690fa59bd879` |
| `C/design.md` | `632fe7775d650f2bf2d9b337d82e29058075966c3154571be8cffeeb8e690828` |
| `C/tasks.md` | `a60c535a26bf41d42930b1a33c3f2062ff2430e9eb6d51a66435fe93772c9f83` |
| `C/specs/control-center-backlog-reconciliation/spec.md` | `a4dbe5d2ca48741281d27b96eb0405edac04d071e37924ec18de7a60d6d23f36` |
| `A/work-items/G2-OWNERSHIP-WAVE.md` | `9dd958ad5d13a2bca16b60a66c02d73431b1aad5edae3a8e368bea689e1987e3` |
| `openspec/specs/documentation-search/spec.md` | `f9b88a2c524c152a4817b5e05861bb6c6e2ef3a9debf548e5b7a852135bb0c6f` |
| `openspec/specs/control-center-shell/spec.md` | `4274bde7ecdf7e18bdcf73cb1755886f3e61bc2cbea3728da0a382006dd0276f` |
| `O/proposal.md` | `627e6be0e705936eefac14a04ed790a87ae72e6c5f9a950177071f30a0c86cba` |
| `O/design.md` | `849aca071ad4123c133979fbbec0c721fe3f7a71e31dd5954bc2fad0ebb5619b` |
| `O/tasks.md` | `04bd8c2fce3c1a797e7ddf972380a5b15b94e44e461f8f58c9f67c8b487ba415` |
| `O/specs/documentation-search/spec.md` | `e34f3afe30cd6d357d07254072e168baa40c2a11308e8e81d014a57c6d0c57c8` |
| `O/specs/control-center-shell/spec.md` | `f058e30128fea38343ea491b4cf3512c2e1dbc591f276ac1022750aab09aebf3` |
| `A/decisions.md` | `0b875b2a5504480e29a0c99671614d1e65bbfc7d4173e3e3496a5dea89999798` |
| `A/reports/LOCAL-001.md` | `0ab83e87351849500a625c2d7efea2b3142d5b1b473924dc2160e03f511e010d` |
| `A/reports/G2-MAIN-CAPABILITY-JOINS.md` | `58912cbe79aeaa7b72273215dc84f26c9a1fcd86366de04b189893ec87f036b0` |
| `A/reviews/R-G2-MAIN-CAPABILITY-JOINS.md` | `2f11435ee6da92bab528ae413704e6fd2a7c6481405c86c3373ad760b58cdb95` |
| `A/reports/IMPL-MOS-904.md` | `9258bdc25e35134edcfa0d7e484c242be694d9df0c8e1f4988be20f5ab10ee1c` |
| `A/reports/IMPL-MOS-905.md` | `392d18a12350147f7023bf87eeca8d3c244bb29e3592e7d744061a196ba5fdef` |
| `A/reviews/R-IMPL-MOS-904.md` | `a00671361147dd7ce992d2d32343c26b78743a39f7036d424f5a785b554b8c17` |
| `A/reviews/R-IMPL-MOS-905.md` | `c6702fe75bf0802cc7b181093c7664bb6b00f6878d7ffcc267fae32d082d312e` |
| `A/reports/JIRA-MOS-784.md` | `5ce6b6eed5e0c9590a7b6c9e738d0bf8a2626651e91a95a54a4c9525257b1120` |
| `A/reports/G1-INVENTORY-SOURCE-CROSSWALK.md` | `c22b131adb9c14abf626a925304b75b31495ff6193f4f97fa975a65741c254a7` |
| `A/sources/jira-hierarchy/r1/content.json` | `4d1881959ecbe13e4c2d4c27903b63a4ba71e1cba38e349dc33855a7e605fb77` |
| `A/sources/jira-hierarchy/r1/metadata.json` | `1cea4dbade645b29f9af43753bf737745bd2af3592f51c2201ddbcb3ec472c91` |
| `A/sources/jira-member-index/r1/content.json` | `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` |
| `A/sources/jira-member-index/r1/metadata.json` | `6c93c19217dacdc18fbdffc95ecc2eaa326494a49eeab99559eca3b04647c89d` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Resolved baseline row19 via explicit MOS-906 capability declaration, saved membership/title and shell delegation; mapped all five requirements/twelve scenarios to originating tasks and qualified SH011/RT009 evidence, retaining exact gaps."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SPEC-G2-DOCUMENTATION-SEARCH.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local find/read/scoped grep","result":"passed","summary":"Complete governing and originating planning artifacts read; accepted source locators and bounded report/review passages inspected."},
    {"command":"Read-only Python SHA-256/line-count inspection and exact requirement-body comparison","result":"passed","summary":"26 input digests recorded; both saved Jira content digests match metadata; main/archive documentation requirement bodies identical."},
    {"command":"Tests/build/lint/typecheck/format/API checks/browser/network","result":"not-run","summary":"Excluded by read-only documentation-analysis assignment; no application/API/build changes."}
  ],
  "validationOutput": ["Five requirements and twelve scenarios have exact originating ownership; no planning contradiction found.","No documentation backend service required; existing session integration remains a distinct obligation.","Only configured report written; no source/spec/archive/shared-register changes."],
  "residualRisks": ["MOS-906 full Jira description/acceptance-body parity and remote freshness remain unverified.","SH011/RT009 are bounded static evidence, not full search/focus/history implementation or runtime acceptance.","Archive checkboxes/receipts are historical, including a recorded whole-suite timeout and separate passing retry.","Git HEAD/index state not inspected; parent and independent reviewer retain acceptance."],
  "diffSummary": "One requested report artifact; planning action recommended keep/no-op, ownership join resolved without feature closure.",
  "reviewFindings": ["No material input blocker or product decision needed for the assigned ownership join.","Do not promote shell navigation evidence to complete documentation-search coverage."],
  "manualNotes": "Read-only local analysis only; no code inspection, new source collection, browser/network/tests or delegation. Whole-file hashing is separate from semantic read coverage. No staging performed and no index-state attestation supplied. Parent acceptance remains pending."
}
```
