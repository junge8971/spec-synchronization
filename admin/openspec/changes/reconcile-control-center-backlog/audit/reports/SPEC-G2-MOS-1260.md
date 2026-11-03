# Code Context

Parent correction after R-G2-LIFECYCLE-EXPORT-SPEC: R23/R26 are covered; explicit enumeration is optional, not a mandatory omission. Original reviewer REVISE and external author artifact are retained. Corrections below are parent dispositions, not a fresh independent ACCEPT.

## Files Retrieved
All paths below are repository-relative; abbreviations are exact locator aliases.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-LIFECYCLE-EXPORT-SPEC.md`: complete assignment, only SPEC-G2-MOS-1260 executed.
- P = `openspec/changes/mos-1260-feedback-export/proposal.md` (1–34, complete).
- D = `openspec/changes/mos-1260-feedback-export/design.md` (1–54, complete).
- S = `openspec/changes/mos-1260-feedback-export/specs/feedback-export/spec.md` (1–35, complete).
- T = `openspec/changes/mos-1260-feedback-export/tasks.md` (1–11, complete).
- R = `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-G2-MOS-1260.md` (complete, including attestation; mapping rows 32–73, prototype 83–90, unknowns 94–100).
- `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-G2-FEEDBACK-REQUIREMENTS-RESUME.md` (complete read; export verdict/analysis 53–73, integrity 12–29).
- A = `openspec/changes/mos-1249-feedback-api/specs/feedback-api/spec.md` (15–38), followed solely through D:37 to resolve permission/session uncertainty.
- B = `openspec/changes/mos-1249-feedback-api/design.md` (1–35; relevant precedence 5–10), followed solely through D:7 to resolve prototype scope. No referenced contracts, sources or implementation inspected.

Accepted R status comes from assignment and independent review, superseding R's historical pending heading. All hashes are parent-attributed, not independently recomputed; freshness not certified.

## Key Code — requirement-to-plan mapping (planning clauses, not code)
C = covered across owning plan; P = partial precision gap. No requirement is treated as implementation acceptance.

| Accepted rows | Exact owner clauses/scenarios/tasks | Finding |
|---|---|---|
| R01 | S:11; T:4 task 1.2 | C: real binary download. |
| R02 | S:9; D:29; T:3 task 1.1 | P: metadata field selection covered; metadata-derived **labels** not explicit anywhere in owner plan. |
| R03–R04 | S:9; T:3 task 1.1 | C: minimum one, unique fields. |
| R05 | S:9,13–16 “Export beyond current page”; T:3 | C: selected order preserved. |
| R06–R08 | S:9,13–16; D:29; T:3,11 tasks 1.1/2.4 | C: entire current applied search, not local rows/page. Unapplied conditions are excluded by “applied”; limit/offset cannot truncate an explicitly entire selection. Repeating both exclusions is optional. |
| R09–R11 | S:9,18–21 “Export saved card while editing”; D:29; T:3,11 | C: one saved record, fields only/no search, new ID gate, dirty-source disclosure; no draft substitution. |
| R12 | S:11; D:31; T:4 | C: server CSV UTF-8/BOM. |
| R13 | D:31; T:4 CSV verification | C: semicolon explicit in design; no need to duplicate in spec/task. |
| R14–R17 | S:11; D:31; T:4 | C: Content-Disposition, preserve server bytes; backend escaping/formula defense. |
| R18 | S:11; D:29; T:3,10 | C with wording precision: metadata limit and 10000 are present. D's “export_max_rows (10000)” does not literally say “default”; replacing parentheses with “default 10000” is a clarification, not grounds to invent missing/malformed-metadata fallback. |
| R19 | S:11; T:3 | C: header-only empty result. |
| R20–R22 | S:11,23–26 “Limit or malformed file”; D:31; T:4 | C: 422 limit and JSON/HTML do not download/succeed. |
| R23 | S:11 safe name; D:31 name validation; T:4 name verification/no false download | C: safe header-derived filename, filename validation and no false download collectively exclude missing/invalid filename success. Explicit negative-branch wording is optional; fabricated fallback is not authorized. |
| R24–R25 | T:4 explicitly 403/404; S:11 404; A:35–38 “Server scope denial” | C: no false download; 403 need not be repeated in S. |
| R26 | S:11,23–26; T:4 | C: existing response/error verification, actual CSV requirement and no-false-download clauses cover 422 errors. Enumerating non-limit 422 explicitly is optional, not a missing general failure path. |
| R27–R30 | S:11; D:31,35; T:4 | C: network/cancel/user-owner change no false file/success; session isolation and URL release. |
| R31–R32 | D:35–37,45; A:26–38; T:10 task 2.3 | C by explicit delegation: TSAM.ManagedResource:read plus export. A:30–33 read-only scenario requires owner UI to apply policy; not a new auth model or request ACL. |
| R33–R36 | P:9,14; D:13; S:9,18–21 | C: nested questions/options/rules and user responses excluded, regardless of shorter lists elsewhere. |
| R37 | D:31; T:4 | C: no imported dialog headers (Content-Length/Cache-Control/X-Content-Type-Options). |
| R38 | S:13–16; T:3,8,11 | C: beyond-page scenario plus unit/component/mock HTTP umbrella. |
| R39 | S:18–21; T:3,8,11 | C: saved detail/dirty integration coverage. |
| R40–R41 | S:23–26; T:4,8 | C: limit and malformed response coverage. |
| R42 | T:4,8; D:31,35; S:11 | C: session-isolation coverage; no separate test task required. |

All 42 accepted Jira IDs accounted for. One material omission (R02 metadata labels); R23 filename and R26 non-limit 422 wording are optional precision only. No contradictory main export behavior found.

### Eight prototype rows, separately classified
| Rows | Exact plan anchor | Classification |
|---|---|---|
| W01 | P:30; S:9,30–35; T:3 | Field selection covered. Exact modal presentation is prototype detail not explicitly fixed in owner clauses; adding the modal wording is optional fidelity clarification, not a missing export capability. |
| W02 | P:14,34; D:13,29,41; S:9; B:7–10 | Broader section export not adopted: stage one uses metadata columns, not tags/segments/surfaces/nested sections. Existing boundary resolves mismatch; no new precedence decision. |
| W03 | S:9,30; T:3 | Field choice covered, checkbox widget not explicit; section-choice part excluded as W02. Exact widget repetition optional. |
| W04 | S:30; T:4 | Download action covered; literal “Выгрузить” copy not specified, optional fidelity detail. |
| W05–W06 | S:11,23–26,30; D:23 | Bottom-right/two-second toast not fixed; no false success is fixed. Prototype presentation details, not evidence of a missing CSV requirement; do not mandate new toast timing. |
| W07–W08 | S:30–35; D:23; T:8 | Keyboard/focus/accessibility covered; exact Esc/backdrop dismissal is not explicit. Optional UI fidelity clarification using existing kit, not authority to equate modal dismissal with network cancellation. |

## Architecture / existing answers to source unknowns
- Ownership already decided: entity owns API/normalized selection; export feature uses public entity API; pages/widgets compose (D:19–25). No new subsystem, dialog export audit, or FSD redesign needed.
- Applied search versus filter draft and saved card versus editor draft are explicitly distinct (D:29; S:9,13–21; T:3,11). Server owns content and value serialization. Column representation, row order and detailed escaping are not frontend reconstruction choices (S:11; D:31).
- “Owner” here means shared session/owner-generation response isolation, not a newly invented survey owner: S:11 says user change; D:31 says response belongs to session; D:35 and T:4 preserve owner/generation/session isolation. Exact cleanup lifecycle timing remains implementation detail, not a new product blocker.
- Exact read/export identifiers resolved by explicit linked A:28. Backend scope and permission/CORS/real-limit evidence remain release checks (D:45,54; T:10–11); mocks cannot close them.
- Safe filename/type validation and URL cleanup are already required; detailed algorithms, error copy, metadata-malformation policy and cancel UX are not specified. This comparison does not invent those policies. R23's fail-closed outcome is covered collectively; explicit restatement is optional and does not authorize fallback algorithms.
- Prototype-only details remain distinguishable from accepted stage-one requirements. No need to reopen source precedence or inspect original HTML/PDF; B:7–10 already establishes prototype composition versus API operations and rejects demo export as production behavior.

## Start Here / minimal candidates
Open `openspec/changes/mos-1260-feedback-export/specs/feedback-export/spec.md` lines 9–11 first:
1. Supported minimal correction: explicitly include metadata-derived column labels at line 9 (R02).
2. Optional only: explicitly enumerate missing/invalid filename and generic 422 in the no-file/no-success clause (R23/R26). Existing requirements and T:4/8 verification already cover these cases; no owning-plan edit required.
3. Optional precision only: D:29 could call 10000 the default; do not turn that into a fabricated fallback for bad metadata.
4. No-op for all remaining Jira behavior and stage-one exclusions. No duplicated scenarios/tasks required for every row. Modal/widget/copy/toast/dismissal restatements are optional, not release blockers or authorization to broaden export.

No material missing input or unapproved choice was needed for these conclusions. No new extraction, API/code audit, tests/network/build/browser, repository edits or delegation. This is S-lane evidence only; no feature/global task closed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped all 42 accepted Jira rows and classified all 8 prototype rows against exact owner clauses/tasks; isolated one material metadata-label omission; parent review correction classifies two other alleged gaps as covered/optional precision."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/035012ee-f634-45c5-99f3-cbbf11cf9574/spec-1260.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"nl -ba owning-plan files; grep -n accepted report/review locators","result":"passed","summary":"Local read-only line-number inspection; no execution of project code."}],
  "validationOutput": ["Complete owning plan and accepted requirement report read; export review accepted all extracted rows; mapping includes every R01–R42 and W01–W08."],
  "residualRisks": ["Source freshness and runtime correctness not assessed; hashes parent-attributed.","Exact prototype presentation details remain non-explicit; no new scope choice made.","Release evidence for real endpoints/errors/permissions/CORS/limit remains open under task 2.3."],
  "noStagedFiles": true,
  "diffSummary": "External artifact only; no project edits or staging actions.",
  "reviewFindings": ["Mandatory candidate: metadata labels only. Filename and generic 422 behavior already covered; explicit restatement optional."],
  "manualNotes": "Bounded planning comparison, not implementation acceptance. No tests or git staging inspection performed; no staging actions taken. Shared references followed only for explicit permission/session and prototype-precedence ambiguities."
}
```
