# Code Context

## R-IMPL-MOS-904 — disposition: ACCEPT (bounded static evidence)

Fresh independent inspection supports the author's 14-ID mapping and bounded gaps. No material correction or escalation blocker was found. Acceptance concerns the evidence report only: not implementation acceptance, test success, deployment, source precedence, task closure or activation. D-008/D-009 gates remain unchanged. The precision notes below must accompany downstream use.

## Provenance and approved scope

Independently read `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-shell-details/r1/metadata.json` and parsed `content.json` root metadata plus `/items/1`, `/items/2`, `/items/4`. Recomputed **14311 bytes**, SHA256 **30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4**, matching metadata. Root retrieval timestamp is **2026-10-16T12:45:22.199Z**. This verifies saved-file consistency, not remote authenticity.

MOS-904 `/items/4/description` contains all 14 candidate fragments. Its two comments (1117112, 1117939; pagination 0/2/2, two actual items) describe historical changes, not current execution evidence. Both precede the issue's captured updated timestamp, **2026-10-16T19:22:21.694+0800**; no field history binds them to the captured description. `Ready for test` is not acceptance. MOS-672/673 each have one captured comment and three attachment metadata entries; successful historical-testing comments and CLOSED statuses do not prove this code revision. Same-named HTML attachments 817137/817140 are not proven identical. No HTML was executed or remote link followed. Screenshot/HTML/wiki241079770 bodies were not inspected; parity remains unverified. Membership is collector-attributed, not newly established from null parent fields.

Current shell `openspec/specs/control-center-shell/spec.md:28–142,179–218,284–306` already owns branding, navigation, docs ordering/destinations, help persistence/accessibility and confirmed profile. No duplicate policy decision is needed. Archived auth `proposal.md:15` expressly excludes logout endpoint/UI; demo `design.md:46` also says no logout. Jira «с выходом» remains a source/scope tension, not an approved implementation defect. No exit, OIDC, new API or auth bypass is authorized. Fixed local demo remains approved; production exclusion does not cancel it. Configuration chooses real/mock mode; T is a deployment address, not an auth switch. Credential-destination checks and backend authorization remain separate, unverified by this UI review.

## Files Retrieved

Paths below are exact repository-relative unless absolute. Listed ranges were read; grouped ranges refer to each named file independently.

### Assignment and prerequisites

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/R-IMPL-MOS-904.md:1–6`, `work-items/IMPL-MOS-904.md:1–9`, `reports/IMPL-MOS-904.md:1–114`, `reviews/RECON-MOS-904.md:1–151` (the last three share the same audit prefix): bounds, author findings and prior corrections. `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` read, especially headings D-008/D-009; no other disposition changed.
- `openspec/specs/control-center-shell/spec.md:1–315`: existing normative owner.
- Complete required sets read **before auth/demo code analysis**, including continuation reads after output truncation. Prefix `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`: `proposal.md:1–38`, `design.md:1–171`, `specs/control-center-api-integration/spec.md:1–64`, `specs/control-center-http/spec.md:1–71`, `specs/control-center-mock-server/spec.md:1–27`, `specs/control-center-permissions/spec.md:1–89`, `specs/control-center-shell/spec.md:1–101`, `specs/mpmm-session/spec.md:1–138`.
- Prefix `openspec/changes/archive/2026-10-09-add-local-session-demo/`: `proposal.md:1–28`, `design.md:1–70`, `specs/control-center-mock-server/spec.md:1–106`, `specs/control-center-shell/spec.md:1–55`, `specs/local-session-demo/spec.md:1–123`.
- `/home/user/.agents/skills/shadcn/SKILL.md:1–260`, `.agents/skills/react-router/SKILL.md:1–119`, `.agents/skills/react-router/references/framework-mode.md:1–213`, `node_modules/react-router/docs/start/framework/navigating.md:1–182`, `react-router.config.ts:1–7`. No CLI/network documentation retrieval under this assignment; actual local wrappers inspected.

### Mounted code and assertions

- `app/root.tsx:1–25`; `app/application/ui/application-root.tsx:1–24`, `application-layout.tsx:1–47`, `session-boundary.tsx:1–26`, `session-status.tsx:1–30`, `application-hydrate-fallback.tsx:1–12`, `application-mock-tools.tsx:1–21` (each latter filename under `app/application/ui/`).
- `app/application/ui/application-layout.test.tsx:1–57`, `session-boundary.test.tsx:1–134`, `application-mock-tools.test.tsx:1–37`, `route-access.test.tsx:1–177` (same UI prefix).
- `app/widgets/header/ui/application-header.tsx:1–49`, `current-user.tsx:1–28`, `application-header.test.tsx:1–125`, `current-user.test.tsx:1–47`, `handlers/application-header.handlers.ts:1–13` (same header UI prefix).
- `app/widgets/header/ui/introductory-help/use-introductory-help.ts:1–53`, `model/introductory-help-storage.ts:1–24`, `introductory-help-dialog.tsx:1–23`, `introductory-help-content.tsx:1–62`, `constants/introductory-help.constants.ts:1–22` (same introductory-help prefix).
- `app/widgets/navigation/ui/application-navigation.tsx:1–75`, `navigation-brand.tsx:1–15`, `application-navigation.test.tsx:1–149`, `application-navigation/documentation-menu.tsx:1–56`, `application-navigation/navigation-entry.tsx:1–48` (same navigation UI prefix); `app/widgets/navigation/model/get-navigation-item-state.ts:1–14`.
- `app/shared/config/application-routes.ts:1–95`, `app/shared/config/constants/application-routes.constants.ts:120–144`, `app/shared/config/session-mode.ts:1–24`; `app/application/constants/application-routes.constants.ts:1–6`, `route-access.constants.ts:1–22` (same constants prefix); `app/application/model/route-access.ts:1–32`, `use-route-access.ts:1–39` (same model prefix); `app/routes.ts:1–15`, `app/routes/teams.tsx:1`, `app/pages/teams/ui/teams-page.tsx:1–29`.
- `app/entities/session/model/permissions.ts:1–54`, `permissions.test.ts:1–139`, `session-state.ts:1–26`, `use-session.ts:1–7` (same session model prefix): display-policy and owner-state composition only, not transport audit.
- `vite.config.ts:16–32`; `app/application/ui/local-mock-controls/local-mock-controls.tsx:1–134`, `handlers/profile-change.ts:1–6`, `local-mock-controls.test.tsx:1–97` (same local-controls prefix).
- `app/shared/ui/popover.tsx:1–75`, `app/shared/ui/dialog.tsx:1–119`, `app/shared/ui/sidebar.tsx:170–194`: primitive/portal composition.
- `app/pages/documentation/ui/documentation-page.tsx:1–5`, `app/widgets/documentation/ui/documentation.tsx:1–109`, `app/widgets/documentation/model/documentation-search-params.ts:1–50`, `app/entities/documentation/model/documentation-articles.test.ts:1–86`; `app/widgets/documentation/ui/documentation.test.tsx:166–210,384–390` and scoped harness lookup. No article-body/attachment parity audit.

## Key Code / independent 14-ID check

Every ID below retains prefix **REQ-MOS-904-** and originates in Jira `/items/4/description`. “Assertion” means inspected test source, never an executed result.

| ID | Independently verified evidence and limits |
| --- | --- |
| 001 | `app/widgets/navigation/ui/navigation-brand.tsx:1–12` imports the mark and renders both accepted labels; mounted in `application-navigation.tsx:34–36`. `app/application/ui/application-layout.test.tsx:27–29` asserts labels/no demo badge. No image parity proof. |
| 002 | `app/widgets/header/ui/current-user.tsx:6–11` requires ready principal, filters name parts and falls back to email. `current-user.test.tsx:10–19,22–45` asserts identity, empty-name fallback and checking removal; no composed replacement assertion. |
| 003 | Same component `:24` joins confirmed roles or explains empty roles. `app/entities/session/model/permissions.ts:11–28` reads grants, not role names/assignments; `permissions.test.ts:12–64` explicitly rejects implicit grants. |
| 004 | `app/application/ui/application-layout.tsx:33–36` mounts actual header; `app/widgets/header/ui/application-header.tsx:22–46` composes title/mobile trigger/profile/help. Structural target, not a separate feature. |
| 005 | `app/widgets/navigation/ui/application-navigation.tsx:33–36` mounts brand in SidebarHeader. Structural target; no historical screenshot equivalence inferred. |
| 006 | Same file `:37–60` maps groups; `app/application/ui/application-layout.tsx:24–29` supplies permission-filtered nonempty groups. `app/application/ui/route-access.test.tsx:77–113,154–168` inspects composed filtering. Standalone defaults are not policy enforcement. |
| 007 | `app/widgets/navigation/ui/application-navigation.tsx:61–72` mounts documentation in SidebarFooter. Structural target, owned docs behavior below. |
| 008 | `app/widgets/header/ui/current-user.tsx:14–25` has named trigger, constrained/truncated name and text email/roles. `current-user.test.tsx:10–45` asserts keyboard focus and open-profile text removal on checking; root-boundary portal transitions remain unestablished. |
| 009 | Inspected complete header/profile/navigation trees have no exit action. Explicit approved exclusions above prevail as scope constraints for this review, without choosing precedence between documents. Absence is not a confirmed defect. |
| 010 | `app/shared/config/constants/application-routes.constants.ts:131–140`, `app/routes.ts:6–9`, `app/routes/teams.tsx:1` connect teams in «Эксплуатация» to `app/pages/teams/ui/teams-page.tsx:12–24`, which honestly shows development placeholder. `app/application/constants/route-access.constants.ts:20` gives Team:view versus wildcard audit. Navigation assertions `app/widgets/navigation/ui/application-navigation.test.tsx:30,36–54,103–148` cover links/active/mobile; positive Team:view-only real teams composition remains a bounded follow-up. |
| 011 | `app/widgets/navigation/ui/application-navigation/documentation-menu.tsx:35–52` uses `documentationArticles.slice(0, 6)`, article URLs and all-sections URL; navigation assertions `:75–101` check basename, seven entries and catalog-derived order. `app/entities/documentation/model/documentation-articles.test.ts:9–58` independently specifies first IDs purpose/scenario/roles/testing/publish/limits. Destination source `app/widgets/documentation/model/documentation-search-params.ts:6–21` selects requested/first/null. Destination assertions `app/widgets/documentation/ui/documentation.test.tsx:166–190,384–390` include basename but mount Documentation alone, not root/menu integration. |
| 012 | `app/application/model/route-access.ts:8–31` and `app/entities/session/model/permissions.ts:21–28` require confirmed grants even for empty required list `/docs`. `app/application/ui/route-access.test.tsx:94–113,154–177` asserts denied content/no fetch, filtering and docs with no grants. Unknown-route return preserves router handling; disabled missing-route helper is not proof teams is missing. Backend request authorization remains outside this UI evidence. |
| 013 | `vite.config.ts:16–26` and `app/application/ui/application-mock-tools.tsx:3–12` guard the lazy controls import. `application-root.tsx:15–20` puts tools outside the session boundary. `application-mock-tools.test.tsx:14–35` asserts render gating/hydrate recovery, not bundle absence. `app/application/ui/local-mock-controls/local-mock-controls.tsx:58–116` uses catalog selections; `handlers/profile-change.ts:3–5` saves then reloads. Test `local-mock-controls.test.tsx:75–95` mocks that handler: it proves intended UI error/lock assertions, not successful actual reload or storage persistence. |
| 014 | `app/widgets/header/ui/application-header.tsx:30–46` exposes help outside profile. `introductory-help/use-introductory-help.ts:14–50` maintains version/ref state and reset identity; storage helper `:6–23` catches failures. `application-header.test.tsx:38–106` asserts completion/remount, new version, Escape/focus, first-step reopening and same-mount unavailable-storage suppression. It does not establish composed bootstrap reachability, Tab cycle or alternate-dismiss persistence. |

## Architecture and precision notes

1. **Session boundary versus isolated header.** `app/root.tsx:21–25` exports loader/fallback; `app/application/ui/application-root.tsx:15–19` places the whole layout/header inside SessionBoundary. `app/shared/config/session-mode.ts:9–10` identifies browser context by `location`; the boundary's non-browser branch is not a runtime auth exemption. `app/application/ui/session-boundary.tsx:14–23` withholds children without an owner and hides/inerts the retained owner subtree while not ready. `app/entities/session/model/session-state.ts:9–18` retains owner during checking/error, keys replacement by ready user ID and clears owner on redirect. `app/application/model/use-route-access.ts:14–39` deliberately retains access during temporary checks inside that hidden boundary. None authorizes stale interactive UI.

   `app/widgets/header/ui/application-header.test.tsx:23–35,113–125` mounts the header without boundary; `app/application/ui/application-layout.test.tsx:49–57` likewise bypasses root bootstrap. Their titles must not establish pre-session help availability. Generic Editor assertions in `session-boundary.test.tsx:62–118` do establish the intended withholding/hiding/replacement test scenarios, not an open profile/help portal scenario. The author's distinction is correct.

2. **Profile portals and stale state.** CurrentUser independently returns null for non-ready/missing principal (`app/widgets/header/ui/current-user.tsx:7`). Its second test opens a profile then checks portal text disappearance via global `screen` (`current-user.test.tsx:33–45`): do not incorrectly describe all open-popover transition coverage as absent. What remains unestablished is that transition **through the actual Activity/root composition**, including error/retained principal and owner replacement. Local wrappers portal their popup (`app/shared/ui/popover.tsx:24–41`, `app/shared/ui/dialog.tsx:44–65`); wrapper delegation and an inert layout wrapper alone do not prove every portal's composed visibility/focus behavior. The script-node absence assertion uses `view.container` (`current-user.test.tsx:38`), not the portal container; JSX text rendering plus the literal-text assertion support the limited claim, not a comprehensive XSS test.

3. **Help storage lifetime.** Key is browser-local `control-center-help-seen:<version>`, not user ID (`app/widgets/header/ui/introductory-help/constants/introductory-help.constants.ts:3–4`; storage `:6–20`). Failure fallback is a hook-instance `useRef(Set)` (`use-introductory-help.ts:16–28`). The failure test rerenders, not unmounts (`application-header.test.tsx:89–105`); it does not exercise a changed key/effect while storage fails or owner-driven remount. A new mounted instance loses that fallback. Whether an owner replacement counts as the same “сеанс оболочки” is not settled by that assertion; do not label it a proven defect or promise document-wide persistence. Existing shell `spec.md:120–142` owns semantics. Its `:126` pre-session wording requires only narrow reconciliation with approved bootstrap, never a bypass.

4. **Docs and responsive proof limits.** Menu order assertions are catalog-relative; catalog tests pin IDs. Menu href/basename and separately mounted destination assertions both exist, but no inspected assertion clicks the quick menu through actual root into rendered article. Mobile tests simulate width and assert closure; they are not physical-layout/browser proof. Profile/help bounds, title/finalFocus and primitive delegation do not prove long-name mobile coexistence or Tab trapping in every composed state.

5. **Production and recovery.** Guard source and stubbed rendering assertions support separation intent, not production build-artifact exclusion. Recovery controls sit outside boundary by actual composition; isolated controls tests use mocked catalogs/bootstrap/profile handler. No server fixture inventory, credential-free transport, real refresh/CORS/RBAC, build or runtime validation was performed. Approved real-integration release gates remain open.

These qualifications reinforce rather than overturn the author report. Missing assertions are gaps only in the inspected files, not whole-repository absence or actual bugs. No new tasks are activated; no source changes are proposed solely for structural IDs 004–007.

## Start Here

Open `app/application/ui/application-root.tsx:11–21` and `app/application/ui/session-boundary.tsx:11–23` first, then `app/widgets/header/ui/current-user.test.tsx:22–45`. They distinguish actual mounting, isolated portal removal assertions and the remaining composed-transition gap.

## Validation and residual risks

Only local read/find/scoped grep, numbered reads and read-only JSON/hash inspection were used. One initial numbered-read command used the wrong handler path; the correct `app/widgets/header/ui/handlers/application-header.handlers.ts:1–13` was subsequently read. No missing-input blocker. No tests/build/generation/browser/network/MCP/dev server/git/index inspection or product/source edits. Sole intentional write is this report; no index attestation.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent primary-source hash verification and mounted-code/assertion review confirm all 14 candidates with bounded precision notes and preserved approval gates."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-IMPL-MOS-904.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local find/read/scoped grep and nl/sed inspection","result":"passed","summary":"Required archived prerequisites, mounted shell composition and cited focused assertions read without execution."},
    {"command":"Initial numbered header-handler lookup","result":"failed","summary":"Wrong path omitted ui/; corrected path subsequently read successfully."},
    {"command":"Read-only Python JSON/hash inspection","result":"passed","summary":"14311 bytes and SHA256 match metadata; selected Jira objects and historical claims inspected."},
    {"command":"Tests/build/generation/browser/network/MCP/git-index inspection","result":"not-run","summary":"Prohibited or outside bounded review."}
  ],
  "validationOutput": ["ACCEPT bounded static evidence; all 14 IDs retained.","Isolated open-profile checking assertion exists; actual root/Activity portal composition remains unverified.","Production render guard is not build proof; no runtime/test-pass assertion."],
  "residualRisks": ["Jira exit request remains in tension with explicit approved no-logout scope.","Pre-session help wording must not authorize bypass; unavailable-storage remount lifetime remains unestablished by inspected tests.","Composed portal transitions, long mobile identity, Tab trap and root menu-to-article integration remain unverified in the inspected assertions.","Historical attachment/wiki parity, production artifact isolation and real deployment/session/backend guarantees remain unverified."],
  "diffSummary":"Only bound independent review report written; author evidence and product/source/plan artifacts unchanged.",
  "reviewFindings":["No material blocker to accepting the author's static evidence mapping.","Preserve precise test-harness and storage-lifetime limitations in downstream use."],
  "manualNotes":"Fresh local read-only analysis after complete mandatory auth/demo proposal/design/spec reads. No nested agents, source precedence, activation, task closure or index-state attestation. Acceptance is of the bounded report only."
}
```
