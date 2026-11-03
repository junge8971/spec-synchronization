# R-D090-EIGHT — independent read-only review

## Decision

**Accept all eight reports as bounded analytical joins, not delivery.** Four dialog discrepancies are established by saved requirements and executable source structure; MOS-1422 supports a static implementation/spec no-op with incomplete test evidence; three surface reports establish specific ownership/evidence gaps, not reproduced geometric defects. No report requires factual rework before analytical acceptance. The integration constraints below are mandatory; acceptance does not authorize creating every individually suggested change.

HEAD independently checked: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Scope authority: `audit/work-items/WAVE-D090-REVIEW-NEXT.md` and `WAVE-D090-EIGHT.md`. Here `A` means `openspec/changes/reconcile-control-center-backlog/audit`.

Only this review output was written. No tests, browser, network, business requests, delegation, application/spec/ledger edits or git mutations. Git working/staging diff was empty before writing; ignored OpenSpec is not covered by that observation.

## Independent evidence verification

- Read all eight reports completely. Independently read `A/sources/jira-subtasks/r1/content.json:52–266`: `/items/2,3,4,5,6,10,11,12` match the eight keys, parents, descriptions and attachment IDs claimed. Description locators are substantive, not summary-only joins.
- Recomputed **all 101 SHA256 table entries across the reports: 101 match, zero missing files or mismatches**. This includes repeated inputs. Verified saved Jira/Wiki/API content hashes against the corresponding r1 metadata fields. Metadata explicitly limits attachment evidence to enumeration and excludes comments/custom acceptance fields; Wiki publication is not runtime/approval evidence.
- Independently extracted relevant inert `bodyView` text from saved wiki-241085439 (§2.3, §2.5.1, §2.7, §3.1.3 and failure provenance caveat), wiki-243776365 (СПС-25 and reset scenarios), and wiki-245673187 (registration type choices). Read wiki-241080065-readable:17–23,70 for wizard/server channel assignment. No attachment body was used.
- Compared saved API search operation r1/r2 and r2 schema fields `DialogListItemResponse.operator_rating`, `CreateSurfaceRequest.domains`, `SurfaceDetailResponse.channel_id`; read local `dialogs.openapi.json:1013–1028`, runtime dialog response schema and query hook. Existing contracts suffice; no new API is warranted by these eight issues.
- Read main `dialog-registry`, relevant `dialog-selection-builder` and `surface-registration` requirements, and original/contour archived deltas for both capabilities. Filesystem search found only archived deltas for these two capabilities, no current active corrective delta.
- Read actual component implementations and relevant test bodies identified below. Test assertions were inspected, never executed. Read historical nested rows `G2-JIRA-MEMBER-JOINS.md:298–302,306–308`; all eight are U. Current `coverage.json` is `complete:false`, through D-089, with no overlay for these eight IDs.

## Per-report disposition and required integration corrections

| Report | Verdict | Verified basis and exact safe decision |
|---|---|---|
| JOIN-MOS-1411 | **accept** | Jira `/items/2/description` and Wiki СПС-25 require hidden reset when nothing can be reset. `app/pages/dialogs/ui/dialog-filters.tsx:82–94` renders it unconditionally. Existing reset sets all five selection parts to defaults and remounts the condition editor (`dialog-registry.tsx:38–49`). `dialogs-page.test.tsx:203–247,366–455` does not assert initial/post-reset absence; the latter clears the condition group before total reset. **Required planning correction:** replace the independent candidate owner with the combined dialog change below. Preserve pending quick-draft reset and applied conditions; `quickFilterKey` alone excludes conditions and `hasPendingChanges` alone excludes already-applied filters. Keep complex-condition-only unapplied draft visibility an explicit design question, not a Jira-derived fact. |
| JOIN-MOS-1412 | **accept** | Jira `/items/3/description` and wiki-241085439 §2.3/2.7 explicitly require a red dot before the first message. `dialog-table-row.tsx:23–38` has no such dot and renders a destructive badge beneath the link. Response schema validates boolean `has_failure`; flags are independent. Tests at `dialogs-page.test.tsx:143–171,311–340` check text presence/absence, not the required dot. **Required planning correction:** one shared full-block MODIFIED delta, not the proposed separate change. Preserve accessible failure naming; no invented size/hex color/offset; no backend inference from route steps. |
| JOIN-MOS-1414 | **accept** | Jira `/items/4/description` and saved API §2.3 require server snapshot duration plus «и идёт» when `ended_at=null`. `dialog-table-row.tsx:60–62` formats only `duration_sec`; completion is shown separately. `dialogs-page.test.tsx:143–166` explicitly expects `0 мин 48 с`. **Required planning correction:** combined owner and shared full-block delta. Add unfinished/finished and zero-duration boundaries without client timer/polling or card changes. Existing card semantics cannot stand in for registry coverage. |
| JOIN-MOS-1419 | **accept** | Jira `/items/5/description` and API §2.7 require a dash for null rating. Registry passes null to `DialogOperatorRating`; that component line 8 returns «Нет оценки». Registry test line 162 and shared component test lines 19–24 expect that text. **Required planning correction:** combined owner; implement registry-specific presentation. The shared test is not globally an invalid contract: other consumers use the component in the card. Do not alter their null presentation or weaken numeric-rating/accessibility assertions merely to satisfy this registry issue. Do not infer a specific Unicode dash or gate the placeholder on `has_operator`. |
| JOIN-MOS-1422 | **accept** | Jira `/items/6/description` asks for five sort buttons. `dialogs.constants.ts:19–25` defines all five; `dialog-table.tsx:49–68` generates actual buttons, both directions and `aria-sort`; query key includes sort and starts with null cursor. Main `Cursor pagination preserves request identity` and local API enum agree. Tests exercise Start/Surface and hook continuation, not all five UI controls/directions. **Required decision:** keep functional spec/API/implementation; no new corrective feature owner and no deployment claim. Optional future parameterized regression is evidence strengthening, not proof of a current defect. Empty/loading table absence is not a new Jira criterion. |
| JOIN-MOS-1110 | **accept** | Jira `/items/10/description` targets Type on the addition form, not registry filters. `surface-details-step.tsx:40–57` uses anchored shared Select; `select.tsx:55–95` has the reported defaults. Existing registration test lines 159–171 checks adjacent grid/width classes, not opened-popup geometry. **Required decision:** question-gated planning only, capability `surface-registration`; retain the report's missing acceptance geometry explicitly. No change of `alignItemWithTrigger`, offsets, side or global defaults is justified merely by props. Do not present the proposed generic anchoring requirement as a resolved, measurable visual criterion. |
| JOIN-MOS-1164 | **accept** | Jira `/items/11/description` explicitly couples roughly 200-character domain input to an untruncated channel identifier and page scroll; its terminology is ambiguous. Current `surface-details-step.tsx:58–72` displays a fixed server-assignment message, not a domain-derived ID. `summary-item.tsx:7` wraps, not truncates; confirmed result line 21 is a different stage. API does not authorize recreating a client channel ID or imposing a 200-character cap. **Required decision:** keep current server semantics; any proposed long-domain layout plan remains conditional and cannot replace the unresolved literal truncation requirement. First identify the contemporary target element if literal clipping is pursued; do not silently retarget the issue to result/card/other text. Structural input-preservation tests are not geometric proof. |
| JOIN-MOS-1165 | **accept** | Jira `/items/12/description` targets Owner on Responsibles. `owner-team-field.tsx:14–35` uses team selection and shared positioning, not business-user responsible fields. Registration test helper opens/selects the owner but does not assert coordinates. **Required decision:** question-gated planning only, scoped to this control; no shared-default fix without cause/consumer analysis. Missing screenshot/criterion blocks visual resolution, not this analytical join. |

These are integration corrections/guards, not requests to rewrite historical reports. Preserve original reports and record this review/parent decision additively.

## ONE coherent corrective dialog change

**Recommended and scope-safe:** `fix-dialog-registry-presentation-and-reset` (candidate name, not created). Include **only MOS-1411, MOS-1412, MOS-1414, MOS-1419**. They share the registry UI, tests, and accepted API; three currently propose overlapping replacements of the same requirement. Four separate changes would risk later full-block sync overwriting another correction.

Plan exactly `proposal.md`, `design.md`, `tasks.md`, `specs/dialog-registry/spec.md` under that owner:

1. One complete `MODIFIED Requirements` block for **Registry represents server rows faithfully** containing all three row corrections: accessible red failure dot before the first message, snapshot duration with conditional «и идёт», and registry null-rating dash. Preserve every existing clause and scenario (six columns, required fields, two skills/remainder, independent flags, authorization marker, safe text, basename-aware link). Keep «не завершён» in its separate completion column.
2. Reset visibility can be one **ADDED** requirement with initial-empty, each active selection part, post-reset, and pending quick-draft scenarios, explicitly preserving existing `Quick filter application is visibly explicit` and `Draft changes require explicit application`. If instead modifying the quick-filter requirement, carry its entire current block once without dropping its scenarios. Do not modify both owners redundantly.
3. Design records exact predicate boundaries, invalid/unapplied quick-draft preservation, the complex-only draft question, and registry-local rating rendering. No API/schema/auth changes, timers, routing redesign, card presentation changes, or surface geometry work.
4. Tasks remain unchecked: implementation plus positive/boundary unit/component regressions and later project checks. Include combined all-five reset (not the present group-precleared test), failure true/false and independent operator state, finished/unfinished including zero duration, null rating at both completion states, and preservation of ratings 1–5/accessibility. Existing safe text/link, request error and cursor behavior must survive.
5. Keep MOS-1422 as no-op evidence; sorting checks may protect neighboring behavior but are not a fifth corrective requirement. No browser/E2E authority is implied. Main specs and archives remain untouched until the ordinary accepted change lifecycle.

## Surface blockers and planning boundaries

There is **no blocker to accepting the eight static joins**, but there are precise blockers to declaring the surface issues corrected:

- MOS-1110: saved attachment `829292` is metadata-only; displacement direction/magnitude, state, viewport and accepted geometry are unavailable.
- MOS-1165: same limitation for attachment `832288`; selected-item alignment versus unwanted displacement cannot be distinguished from defaults alone.
- MOS-1164: attachment `832277` is metadata-only and the original dynamic-ID chain is absent in this HEAD. The current target of literal truncation is unresolved. Wrapping, absence of a generated ID, and class assertions do not establish literal clipping or no horizontal page scroll.

Allow narrow gap/clarification plans, not speculative CSS fixes. Before implementation acceptance, obtain an agreed local criterion or permitted evidence; this review authorizes neither attachment retrieval nor browser testing. Do not invent zero offsets, fixed popup side/width, collision restrictions, ellipsis policy, or a 200-character validation maximum. Keep the three surface IDs separate in evidence even if a future explicitly approved layout plan shares investigation.

## Population decision

**Eight U→P additive overlays are justified after parent acceptance**, one for each reviewed report, with this review as evidence. P means substantive but partial analysis: exact saved requirement → owner → present code/tests → explicit gap/decision. It does not mean fixed, accepted feature, delivered, deployed, or full runtime/test coverage. MOS-1422's no-op is substantive code/spec evidence; surface uncertainty does not erase the concrete joins.

Preserve historical U rows, population membership and feature checkboxes. Record the four confirmed static corrections, one no-op/test gap, and three unresolved geometry/target gaps distinctly. Keep `complete:false`; do not close global 3.1–3.5. This review performs no overlay mutation and assigns no new parent decision ID.

## Reviewed report fingerprints

| Report | SHA256 |
|---|---|
| JOIN-MOS-1411.md | `a5641af49c067fb64358ea1a23b8f39405aaa2268946bb328f2bf9e1eb7879f9` |
| JOIN-MOS-1412.md | `b037676ea37fbcd839a2a5e776b4bf038a2011996af1c369723fd98d2f61bc9e` |
| JOIN-MOS-1414.md | `325aaae186c680ced84f29d7b96ad957e234aa717895105c2751b5a6a9db7cd4` |
| JOIN-MOS-1419.md | `c99a68e4e50e9241ba6fe795d34c6e6f2a21dd643e15b8467a9db728faa08745` |
| JOIN-MOS-1422.md | `e22c48cc6211300777fa2e74a2e373558cf10258fbb76f4389ebc8384650e302` |
| JOIN-MOS-1110.md | `bcec29d6b24f2b5eb60dc97783aa5ca533d772491286420e75f5a6572b9874b8` |
| JOIN-MOS-1164.md | `8fb7c861245f10a70f54f38204d14db760443423de3e69eee9c1d41805c148c9` |
| JOIN-MOS-1165.md | `ab8eba5685b40edec8fdacbf7a9fbef63a0abe93260263708e94bbb8ba6c2aab` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Eight independent dispositions, exact source/code/spec/test joins, 101 matching input hash entries, consolidated planning and bounded overlay decisions recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-D090-EIGHT.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD; git status --porcelain; git diff --stat; git diff --cached --name-only","result":"passed","summary":"Expected HEAD; no tracked or staged changes observed before output."},
    {"command":"Read-only Python SHA256 verification of all eight report input tables","result":"passed","summary":"101 entries matched; eight report fingerprints recorded."},
    {"command":"Read-only saved JSON extraction and filesystem search for capability deltas","result":"passed","summary":"Exact Jira/wiki/API joins confirmed; only archived deltas found for the two capabilities."},
    {"command":"tests, lint, typecheck, build, browser/E2E, network","result":"not-run","summary":"Prohibited/outside this read-only review."}
  ],
  "validationOutput": ["Accept 8 bounded reports; four confirmed static dialog gaps; one functional no-op; three unresolved surface geometry/target gaps."],
  "residualRisks": ["Surface screenshots and measurable historical geometry unavailable; MOS-1164 current clipping target unresolved.","No runtime, test execution, deployment or external freshness evidence.","Future publication must combine overlapping full-block dialog deltas without loss."],
  "noStagedFiles": true,
  "diffSummary": "Only the configured independent review report written; no project or ledger changes.",
  "reviewFindings": ["No blocker to bounded analytical acceptance; surface correction acceptance remains blocked by the specific evidence gaps above."],
  "manualNotes": "All eight U-to-P overlays are justified as partial analysis only and require parent integration; no delivery or feature completion approved."
}
```
