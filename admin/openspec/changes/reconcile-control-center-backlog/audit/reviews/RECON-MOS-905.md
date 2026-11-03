# Code Context

## Disposition

**REVISE reconciliation annotations; ACCEPT the 18-ID source extraction.** The primary snapshot supports all candidates with the description/comment/historical distinctions already recorded. Most questions in REQ-MOS-905 are omissions of that individual Jira description, **not missing combined requirements**: accepted shell routing rules already specify paths, query collision handling, history and breadcrumbs. Do not create duplicate implementation or decision tasks from those questions.

The remaining narrow semantic issue is REQ-MOS-905-017: Jira says to use an agreed accessible entry point without skills, whereas the approved auth design explicitly retains `/` → `/skills`, then an accessible domains tab or a denial page with accessible links. There is no evidence here for an automatic redirect to some other business section. Record this distinction, not a new policy. No input/scope blocker, writer authorization, delivery finding or task closure is asserted.

## Files Retrieved

Paths are repository-relative. `A` = `openspec/changes/reconcile-control-center-backlog/audit`; `R` = `openspec/changes/archive/2026-09-28-update-control-center-routing`; `H` = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`. These aliases expand to exact paths in the locators below.

1. `A/work-items/RECON-MOS-905.md` (1–9), `A/work-items/REQ-MOS-905.md` (1–9), `A/reports/REQ-MOS-905.md` (1–89): scope and extraction under review.
2. `A/sources/jira-shell-details/r1/metadata.json` (1–52); `A/sources/jira-shell-details/r1/content.json`, JSON pointers `/items/0`, `/items/3`, `/items/5` only (keys at lines 14, 126, 204; MOS-905 description line 207 and comments 214–231): selected primary requirements and claims. Whole bytes hashed, but no other issue body inspected.
3. `A/reports/LOCAL-001.md` (1–194): discovery inventory only, not semantic or index attestation.
4. `openspec/specs/control-center-shell/spec.md` (1–315): current shell requirements, especially 47–118 and 144–282.
5. `openspec/specs/control-center-permissions/spec.md` (1–91): current permission policy.
6. `R/proposal.md` (1–31), `R/design.md` (1–78), `R/specs/control-center-shell/spec.md` (1–159): bounded originating MOS-905 routing contract.
7. Complete required auth artifacts: `H/proposal.md` (1–38), `H/design.md` (1–171), `H/specs/control-center-api-integration/spec.md` (1–64), `H/specs/control-center-http/spec.md` (1–71), `H/specs/control-center-mock-server/spec.md` (1–27), `H/specs/control-center-permissions/spec.md` (1–89), `H/specs/control-center-shell/spec.md` (1–101), `H/specs/mpmm-session/spec.md` (1–138). Read before permission-fallback analysis; oversized tool output was continued from its saved inspection log.
8. `openspec/changes/archive/2026-10-06-mos-1041-dialog-details/specs/control-center-shell/spec.md` (1–67): subsequent dialog breadcrumb/detail refinement.
9. `openspec/specs/dialog-details/spec.md` (1–21), `openspec/specs/surface-overview-connection/spec.md` (1–26): bounded cross-check that shell entry points do not replace separate accepted business-card contracts. Heading searches additionally located sections, without implementation inspection.

## Primary evidence verification

Fresh SHA256: `30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4`; **14311 bytes**, matching assignment and metadata. Selected keys independently match MOS-624, MOS-674, MOS-905. Saved comments have startAt 0 and item-count/total **0/0, 1/1, 2/2**, matching metadata entries 0/3/5. Metadata retrieval timestamp is `2026-10-16T12:45:22.199Z`. This verifies local consistency, not live Jira authenticity, hierarchy or completeness beyond saved counts.

- MOS-905 `/description` supplies -001 through -017. It does not prescribe canonical alias direction, exact card IDs, tab query key, collision/history mechanics or fallback destination.
- MOS-674 `/description` supplies historical automatic breadcrumbs (-018); MOS-905 `/summary` names refinement. Do not relabel -018 as a newly detailed MOS-905 description requirement.
- MOS-905 comment `1117971` claims routing, URL/history tabs, placeholder pages and breadcrumbs work. MR mention `1118004` and `Ready for test` do not prove implementation, merge, test success or deployment.
- MOS-674 comment `1114562` is a historical successful-contour-test claim only; CLOSED is status, not fresh testing. MOS-624 generic lifecycle wording is context, not a route acceptance criterion.
- Attachment bodies/custom fields remain uncollected; teams wiki 241080659 is not supplied here. No referenced URLs or attachments were fetched. These gaps do not prevent the bounded shell reconciliation.

## Key Code — requirement-to-spec coverage (no code inspected)

`S` below is exactly `openspec/specs/control-center-shell/spec.md`. Every stable ID is preserved. “Covered” means specification coverage, never delivered behavior.

| Candidate ID | Current owner / exact locator | Reconciliation |
|---|---|---|
| REQ-MOS-905-001 | S 144–162; H/design.md 113–119 | Covered: `/` → `/skills`, no separate welcome dashboard; permission handling is separate. |
| REQ-MOS-905-002 | S 216–223 | Covered: `/skills/new`, static create path not an entity ID; current spec now requires registration wizard, not permanent MOS-905 placeholder. |
| REQ-MOS-905-003 | S 216–238 | Covered: preserve `/surfaces/new` and existing registration behavior. Jira “add” is not evidence that a duplicate page must be built. |
| REQ-MOS-905-004 | S 216–228 | Covered path `/surfaces/:surfaceId`; unfinished-content restrictions are conditional, not permission to replace accepted business cards with placeholders. |
| REQ-MOS-905-005 | S 216–233; dialog-details/spec.md 9–21 | Covered `/dialogs/:dialogId`, with accepted detail using `chat_id`; no skill UUID restriction inferred. |
| REQ-MOS-905-006 | S 47–84, 179–189, 216–218 | Covered `/teams`; section access and tabs do not prove team CRUD delivery. |
| REQ-MOS-905-007 | S 47–84, 179–194, 216–218 | Covered `/ops`; entry point does not activate unfinished operations. |
| REQ-MOS-905-008 | S 144–167 | Covered: canonical `/metrics`, legacy `/dashboard` redirects with replace and preserved other query. |
| REQ-MOS-905-009 | S 91–118, 144–157 | Covered: canonical `/docs`, legacy `/documentation` redirects; article/search query retained. |
| REQ-MOS-905-010 | S 144–167, 260–282 | Covered deployment basename `/tsam-panel/`; Jira `/tsam-panel` spelling is not a conflicting second base. |
| REQ-MOS-905-011 | S 146–177 | Covered `/domains` → `/skills?tab=domains`. |
| REQ-MOS-905-012 | S 146–177 | Covered `/review` → `/skills?tab=review`. |
| REQ-MOS-905-013 | S 146–177 | Covered `/audit` → `/teams?tab=audit`. |
| REQ-MOS-905-014 | S 146–177 | Covered `/ops/stubs` → `/ops?tab=stubs`. |
| REQ-MOS-905-015 | S 146–177 | Covered `/ops/maintenance` → `/ops?tab=maintenance`. |
| REQ-MOS-905-016 | S 146–177 | Covered all five: preserve other query including repeated values; old path overrides conflicting `tab`; replace history. |
| REQ-MOS-905-017 | S 47–89, 179–214; H/design.md 113–119; control-center-permissions/spec.md 9–65 | Policy already specified; see precise semantic qualification below. Do not invent an alternative destination or role-to-route ordering. |
| REQ-MOS-905-018 | S 260–282; R/design.md 51–59; R/specs/control-center-shell/spec.md 142–159 | Historical baseline refined: no “Главная”, no root breadcrumb before redirect; sections/tabs/detail labels and canonical parent links specified. Preserve historical provenance rather than literal universal display on the transient root. |

Origin ownership: `R/proposal.md:3–14,24` explicitly identifies MOS-905 and shell ownership. `R/specs/control-center-shell/spec.md:58–159` contains routes, tab/history, entry points and breadcrumb rules; `R/design.md:27–59` explains choices. Current auth refinements are explicit `H/specs/control-center-shell/spec.md:22–101`, not inferred from archive placement. Dialog dynamic naming refinement is in `openspec/changes/archive/2026-10-06-mos-1041-dialog-details/specs/control-center-shell/spec.md:45–67` and S 260–282. No active product-change gap was established or new change proposed.

## Architecture and already answered questions

The shell owns canonical URL and route metadata, tab selection, navigation and breadcrumbs. Business capabilities own card contents. Session/access requirements constrain what may mount or fetch; they do not redefine URL compatibility or authorize unimplemented features.

1. **Aliases and history:** agreed redirects run old → canonical, replace current history, retain repeated unrelated query and choose the tab dictated by the old path. `R/design.md:31` additionally calls for fragment preservation with framework navigation, not an HTTP redirect/status contract. There is no remaining need to choose redirect direction/status as a new product task.
2. **URL tabs:** S 179–214 explicitly requires `tab`, push for a different allowed tab, preserving other query, removing `tab` only for the original table default, back/forward access re-evaluation. Defaults/order: skills `list, domains, review`; teams `teams, audit`; ops `modules, stubs, maintenance`. `R/design.md:39` says no mandatory rewrite for empty/unknown tab and no extra history on reselecting current tab. Thus comment-derived history claims have independent spec backing, not proof of execution.
3. **Fallback:** completed auth read establishes exact action/resource/`*` permissions, not role-name inference. Absent/empty/unknown tab selects first permitted tab; an explicitly forbidden existing tab denies rather than silently falling back. Domain:view without Skill:view can enter domains under `/skills`. With no accessible skills tab, `H/design.md:119` says root still redirects to `/skills`, then denial with accessible links, not a redirect loop. With no business grants, S 86–89 requires denial plus static docs, no repeated login or business requests. These are already agreed outcomes. The Jira phrase “доступную точку входа” does **not** establish automatic landing on another business route; if someone interprets it that way, that interpretation conflicts with the explicit design and needs clarification rather than implementation by assumption.
4. **Breadcrumbs/cards:** S 260–282 fixes section hierarchy, non-default tab labels, parent registry links, current-item accessibility and detail labels. Dialog uses topic or `Диалог <chat_id>` from the same response; pending/error uses neutral `Диалог`, not stale prior topic. Skill preserves its data-source name and `Навык` fallback. No new breadcrumb decision task is needed.

## Precise corrections, tensions and residual questions

### Safe report-only correction candidates

- Keep -001 through -018 as extracted; append the spec locators above. Reclassify REQ-MOS-905 gaps 1–4 as **source-local omissions already resolved by accepted rules**, with the narrow -017 wording qualification.
- Keep comment/status/test claims separate and replace broad residual “tab destinations, collision/history semantics, fallback and card paths unspecified” with “unspecified in this Jira description; mapped in accepted shell/auth artifacts; implementation/runtime unassessed.”
- Remove unsupported `noStagedFiles:true` from REQ-MOS-905 (and do not inherit LOCAL-001's same claim). No index inspection was performed here. “No staging performed by this inspection” cannot attest an empty index. This review omits that field.
- Product/spec implementation changes: **no-op from this requirements review**. No duplicate route task, new permission fallback policy, route expansion, deferred activation or closure is warranted.

### Bounded tensions, not invented missing policy

- Historical MOS-674 “every page” versus later explicit absence of root breadcrumbs: recorded refinement, not a missing mechanism.
- Original routing archive's no-session navigation and unconditional default-tab behavior are historical, explicitly modified by the auth change/current specs. Do not reinstate them based on the older archive.
- Current shell default-breadcrumb scenario S 269–272 mentions unknown `tab` as default, while S 181/211–214 permit a first allowed non-default tab. Combined rules select the permitted actual tab and require its breadcrumb when not the table default (S 262). A documentation-only qualification of that example could remove ambiguity; it is not justification for changing fallback behavior.
- Shell unfinished-card prose must be read with its explicit “already implemented cards are not replaced” qualification (S 225–228) and separate accepted surface/dialog contracts. This audit does not establish which runtime cards are implemented.
- The only potentially unresolved product interpretation is whether Jira's -017 phrase was intended to demand a different automatic destination despite H/design.md:119. The saved source does not say that, and no such policy is proposed. Existing design answers the operational question; do not manufacture a blocker unless a contradictory intended outcome is actually asserted.

## Evidence boundaries

Observed code: **none**. Test assertions/files: **none read or executed**. Spec scenarios are normative expectations, not passing tests. Historical Jira test statement is an attributed claim. Archive/MR/Ready for test do not establish delivery. SPA fallback at the deployment host, live auth/session availability, actual route behavior, business-card readiness and backend enforcement remain runtime unknowns. Required auth artifacts were read; no auth contract source precedence or new login/logout flow was inferred.

No network/MCP/browser/tests/build/generation, nested agents, git commands/mutations, source/product/spec edits or task closure. Only this bound review is written.

## Start Here

Open `openspec/specs/control-center-shell/spec.md:144–282` for the already-agreed answers. For -017 specifically, read `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/design.md:113–119` alongside current shell 179–214 before interpreting Jira's abbreviated fallback wording.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently verified primary snapshot hash/keys/saved comments, mapped all 18 stable IDs to current shell/auth routing rules, and separated source omissions from remaining interpretation/runtime limits."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-905.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Read-only Python SHA256/byte count and selected JSON inspection; local find/read/grep/nl/wc inspection","result":"passed","summary":"14311 bytes; assigned SHA256; selected keys MOS-624/MOS-674/MOS-905 and saved comment totals 0/1/2 match."}],
  "validationOutput": ["All 18 IDs retained and mapped; complete approved auth proposal/design/specs read; no implementation or test inspection."],
  "residualRisks": ["Jira accessible-entry wording must not be expanded into an automatic alternate-route policy contrary to the explicit approved design.","Code/tests/deployment and live source completeness are unassessed; attachments/custom fields and linked teams source remain unavailable in the bounded evidence.","Index unverified; no empty-index attestation."],
  "diffSummary": "Only the bound independent review written; no product, source, spec or extraction-report edits.",
  "reviewFindings": ["Revise reconciliation annotations and unsupported index claim, not the 18-ID extraction; most routing questions already answered by accepted rules.","No actual input/scope blocker; no duplicate task, activation or closure proposed."],
  "manualNotes": "Requirements/spec reconciliation only. Normative scenarios, historical test claims and runtime unknowns are explicitly separated; no tests executed."
}
```
