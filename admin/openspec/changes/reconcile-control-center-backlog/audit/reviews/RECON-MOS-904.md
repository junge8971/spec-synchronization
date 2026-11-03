# Code Context

## RECON-MOS-904 — disposition: REVISE

Independent local evidence review completed; no input/scope blocker. Accept the 14 primary-description candidates and the profile-exit conflict; revise the report's implication that documentation-menu and introductory-help behavior await fresh product decisions. Existing main shell requirements already specify those behaviors. No implementation audit, task closure, writer authorization, source-precedence ruling or runtime conclusion follows.

### Findings

1. **Revise — already-owned help/docs choices presented as missing.** `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-904.md:107,118–119` must distinguish absence in Jira/auth deltas from absence across accepted specifications. `openspec/specs/control-center-shell/spec.md:91–142` specifies dropdown placement, first-six catalog ordering, destinations, fallback, closing behavior, help trigger, versioned browser-local persistence, dismissal, reopening, keyboard focus and unavailable-storage behavior. Full article/copy bodies were not inspected; that is not grounds to reopen these behavioral decisions.
2. **Retain / escalate only the bounded owner question — profile exit.** Jira `/items/4/description` genuinely requests «с выходом». `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md:15` explicitly excludes logout endpoint/UI; its `design.md:25,98` excludes own logout and preserves MPMM ownership. `openspec/changes/archive/2026-10-09-add-local-session-demo/design.md:46` says no logout. Current shell `spec.md:284–306` accepts a confirmed profile menu but not global logout. Thus this is a real unresolved cross-document scope tension, not a missing profile specification. Neither local exit semantics nor a global logout/OIDC/new API can be inferred. Owner reconciliation is needed before adding an exit action; this review does not decide which source prevails.
3. **Revise — unsupported index attestation.** Author report `:140` asserts `noStagedFiles:true`, while `:143` states the index was not inspected. Remove the assertion, not replace it with an inferred false/empty-index claim. This review did not inspect git/index either.
4. **Narrow branding/navigation questions.** Author report `:116–117` should preserve asset/version provenance uncertainty, not reopen the accepted brand labels or `/teams`/`/ops` entry-point policy. Exact text, route availability, unfinished-content explanation and mobile closure already have owners below. No claim that these are implemented is made.

## Files Retrieved

Paths and aliases below are exact repository-relative locators. Entire required archived proposal/design/spec sets were read before auth/mock analysis; truncated combined output was retrieved in continuation reads.

- `openspec/changes/reconcile-control-center-backlog/audit/work-items/RECON-MOS-904.md` (1–9); `openspec/changes/reconcile-control-center-backlog/audit/work-items/REQ-MOS-904.md` (1–9): bounds.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-904.md` (1–145): reviewed extraction.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (1–194): bounded ownership inventory, not independently revalidated counts. Its main-capability list and archive inventory locate existing shell/auth/demo/routing owners; no missing MOS-904 plan inferred from directory naming.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-shell-details/r1/content.json`: root metadata and complete `/items/0`, `/items/1`, `/items/2`, `/items/4` only, parsed by JSON pointers rather than line citations.
- `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-shell-details/r1/metadata.json`: complete metadata, especially `/membership`, `/comments/0`, `/comments/1`, `/comments/2`, `/comments/4`, `/limitations`.

`AUTH` = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`:

| Exact suffix under AUTH | Complete lines read |
|---|---:|
| `proposal.md` | 1–38 |
| `design.md` | 1–171 |
| `specs/control-center-api-integration/spec.md` | 1–64 |
| `specs/control-center-http/spec.md` | 1–71 |
| `specs/control-center-mock-server/spec.md` | 1–27 |
| `specs/control-center-permissions/spec.md` | 1–89 |
| `specs/control-center-shell/spec.md` | 1–101 |
| `specs/mpmm-session/spec.md` | 1–138 |

`DEMO` = `openspec/changes/archive/2026-10-09-add-local-session-demo`:

| Exact suffix under DEMO | Complete lines read |
|---|---:|
| `proposal.md` | 1–28 |
| `design.md` | 1–70 |
| `specs/control-center-mock-server/spec.md` | 1–106 |
| `specs/control-center-shell/spec.md` | 1–55 |
| `specs/local-session-demo/spec.md` | 1–123 |

Additional current/route artifacts:

- `openspec/specs/control-center-shell/spec.md` (1–315), abbreviated **S** below: current accepted shell behavior.
- `openspec/specs/control-center-permissions/spec.md` (1–91), abbreviated **P**: UI-only permissions and backend authorization.
- `openspec/specs/mpmm-session/spec.md` (1–140), abbreviated **M**: confirmed principal and configured real/mock modes.
- `openspec/changes/archive/2026-09-28-update-control-center-routing/proposal.md` (1–31), `design.md` (1–78), `specs/control-center-shell/spec.md` (1–159), abbreviated **R** directory: historical route ownership, read before route reconciliation. Its historical no-session wording is not treated as the current auth policy.

## Primary-source verification

Let **J** denote the exact content.json path above. Independently computed byte length **14311** and SHA256 **30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4**, matching metadata and work-item. Root retrieval timestamp is **2026-10-16T12:45:22.199Z**, matching metadata. Collector provenance is recorded, not independently authenticated remote truth.

| J pointer | Key | Comments startAt/maxResults/total/actual | Attachments | Status |
|---|---|---|---:|---|
| `/items/0` | MOS-624 | 0/0/0/0 | 0 | Backlog |
| `/items/1` | MOS-672 | 0/1/1/1 | 3 | CLOSED |
| `/items/2` | MOS-673 | 0/1/1/1 | 3 | CLOSED |
| `/items/4` | MOS-904 | 0/2/2/2 | 0 | Ready for test |

These match corresponding metadata comment counts/totals and recorded completeness. Selected objects have null parent and empty subtasks; membership remains collector-attributed to `jira-hierarchy/r1/content.json results[0]`, not independently established by detail fields. Hierarchy reopening was unnecessary for this candidate/owner mapping; no new hierarchy assertion is made.

- **Primary requirements:** the 14 candidates all occur in J `/items/4/description`; exact fragments retained below. Parent `/items/0/description` is development-cycle context, not header acceptance criteria.
- **Historical descriptions:** `/items/1/description` and `/items/2/description` request screenshot/example parity. Metadata cannot establish those visual contents.
- **Comment/test claims:** `/items/1/comments/items/0` id 1114541 and `/items/2/comments/items/0` id 1115041 claim successful historical testing; no test assertions/artifacts were inspected. `/items/4/comments/items/0` id 1117112 reports help/navigation changes; id 1117939 at `/items/4/comments/items/1` merely claims changed API paths. Neither establishes current implementation or additional API requirements. Unrelated registry commentary was not expanded.
- **Version uncertainty:** MOS-904 comments precede `/items/4/updated` (2026-10-16T19:22:21.694+0800); no field history ties claims to the captured description. Status is not acceptance evidence.
- **Approved scope/main specifications:** normative local behavior, distinct from Jira wording and implementation evidence. Archive placement alone is not deployment proof.
- **Observed code/test assertions/runtime:** none inspected or executed; all remain unknown by assignment.

## Requirement-to-existing-owner coverage (14 stable candidates)

Every row's primary locator is **J `/items/4/description`**, disambiguated by the quoted fragment. Coverage means accepted specification ownership, not implemented coverage.

| Candidate ID | Primary fragment | Existing accepted owner and disposition |
|---|---|---|
| REQ-MOS-904-001 | «Заменить старый бренд» | **S:28–45**, DEMO `specs/control-center-shell/spec.md:3–20`: exact labels «Центр управления» / «Цифровой ассистент», prototype-aligned mark, current section title. Asset-body parity remains a collection gap, not an undecided brand label. |
| REQ-MOS-904-002 | «жёстко заданные ФИО» | **S:284–306**, DEMO shell `:24–46`: confirmed `/me` name, omitted empty parts, email fallback, stale-data hiding. Accepted. |
| REQ-MOS-904-003 | «/роль» | Same owner: confirmed roles array, «Роли не назначены» when empty; roles convey information, not grants. **P:9–21**. Accepted. |
| REQ-MOS-904-004 | «Доработать существующие header» | Shell **S:28–45,120–142,284–306** owns branding, help and confirmed profile. Component-target wording does not itself specify another feature or prove current component architecture. |
| REQ-MOS-904-005 | «SidebarHeader» | Responsive branding/active-section owner **S:28–45**. Existing scope target; exact component-level visual parity requires the historical bodies, not a fabricated new product plan. |
| REQ-MOS-904-006 | «SidebarContent» | **S:47–89,179–214** and AUTH shell `:22–101`: grouped navigation, permissions, route availability, selected tabs. Covered behavioral owner; no independent layout inferred. |
| REQ-MOS-904-007 | «SidebarFooter» | **S:91–118** owns bottom-sidebar documentation dropdown. Shell owns responsive behavior. Jira gives no separate footer behavior beyond the surrounding requirements. |
| REQ-MOS-904-008 | «Добавить профиль» | **S:284–306**, DEMO shell `:24–46`: accessible confirmed name/email/roles menu, text-only values, keyboard/mobile focus. Accepted, distinct from exit. |
| REQ-MOS-904-009 | «с выходом» | **Unresolved tension**, AUTH `proposal.md:15`, `design.md:25,98`; DEMO `design.md:46`; **S:11,286**. No accepted exit action; owner reconciliation only, no inferred local/global logout implementation. |
| REQ-MOS-904-010 | «переход к командам» | **S:47–89,179–214**, R `proposal.md:12`, `design.md:57`: `/teams` in «Эксплуатация», appropriate permissions/tabs, active highlight/mobile closure, honest unfinished content. Profile-menu placement is not required by this phrase. No team-business expansion. |
| REQ-MOS-904-011 | «контекстное меню статей документации» | **S:91–118**, R shell `:37–54`: bottom button, first six existing catalog articles in catalog order + «Все разделы», `/docs?article=<id>` and `/docs`, basename, closure, legacy redirect, unknown-article fallback; current search-aware fallback is also specified. Behavior is not awaiting a fresh owner decision. Concrete catalog bodies not audited. |
| REQ-MOS-904-012 | «Доступность разделов брать из auth-контекста» | **P:9–81**, **S:47–89**, **M:47–59**: confirmed permissions drive UI, not role names; backend authorizes requests/object scopes. No new auth context endpoint/model or frontend request ACL. Accepted. |
| REQ-MOS-904-013 | «Демонстрационные reset, переключение произвольной роли и сценарии показа не переносить в рабочий контур» | **S:28–45**, DEMO mock-server `:3–15`, local-session-demo `:7–28,45–82`: retain all three prohibitions outside configured local demo; separate fixed-profile/scenario «Моки» panel permitted locally, absent in production. No cancellation of local demo. |
| REQ-MOS-904-014 | «Подсказки первого входа и повторное открытие справки оставить как справочную UI-функцию» | **S:120–142** covers both behaviors: versioned browser-local mark, no user/profile request dependency for that mark, close/completion marks viewed, reopen at step one, accessible header button outside profile menu, focus/Escape, storage-failure fallback. **S:39–41,301–306** retains mobile help. Exact walkthrough copy not audited; persistence/interaction are already specified. |

Rows 004–007 are structural targets from Jira, not independently testable behavioral detail or proof of implementation. Preserve their IDs without inventing per-component requirements. Row 013 retains reset/role-switch/show-scenario prohibitions; row 014 retains first-entry and reopen behaviors separately within its existing ID.

## Architecture / scope constraints

Existing shell capability owns UI behavior; routing archive supplies route provenance, with current shell and permissions specs expressing confirmed-access behavior. Auth owns real-session bootstrap and principal; demo owns fixed local principal/scenarios. Inventory absence of a directory named MOS-904 does not mean there is no owner.

Approved mode rules remain: `yarn dev` defaults to mocks; dev opt-out (`CONTROL_API_MOCKS=false`) and production use configured real API/session regardless of hostname. T is the current backend deployment, not an auth switch. Credential destination validation remains separate (**M:9–26,128–140**). Local business mocks are credential-free without role enforcement; permissions are UI presentation, while backend authorizes real requests and object scopes. No own OIDC, global logout, new auth API or local-demo cancellation is authorized by this reconciliation.

The help scenario's historical «без сессии» wording (**S:126**) does not authorize bypassing real-mode session bootstrap (**S:11; M:9–26**). Its local mark semantics are already explicit. If planning requires pre-bootstrap help presentation, narrowly reconcile that scenario with the existing session boundary; do not reopen all help behavior or invent an auth exemption.

## Minimal planning correction candidates

- Cross-reference candidates 001–008 and 010–014 to existing shell/auth/demo owners rather than create a missing-shell product plan or request decisions already recorded.
- Correct author report `:118–119` to separate known behavior from uninspected article/copy bodies; narrow `:116–117` to provenance and verification rather than new navigation/branding choices.
- Keep 009 visible as unresolved source/scope tension; any proposed exit remains outside present approval pending owner reconciliation.
- Remove author `noStagedFiles:true`; preserve unknown index state. No plan or author report was edited here.

## Owner questions versus collection gaps

**Owner questions:** reconcile requested profile exit with explicit approved no-logout UI scope; if an exact historical visual version is needed, identify its authoritative artifact/version after collection. Optionally clarify the narrow pre-bootstrap help scenario wording noted above without changing its accepted local persistence contract. No blanket request for new article ordering, placement, routes, persistence, keyboard or mobile policy is justified.

**Collection/verification gaps (not globally missing requirements):** wiki241079770 linked from MOS-904 has no body in this inspected bundle; parent wiki223087110/wiki222659162 were not followed. MOS-672 attachment IDs **817138,825952,817137** and MOS-673 **817141,826497,817140** are metadata only, including screenshots and two same-named `Прототип ЦАМ, версия MVP.html` files. Equal filename/size does not prove identical content. Article catalog/copy and exact mark were not inspected. Comment authors, field history and historical test artifacts are absent. These limit provenance/parity/test claims, not accepted shell behavior. Remote origin authenticity, runtime integration/CORS/refresh rotation/server authorization and deployed SPA fallback remain unverified.

## Start Here

Open `openspec/specs/control-center-shell/spec.md:91–142` first: it directly corrects the false planning gaps for candidates 011/014. Then retain the explicit exit exclusion at AUTH `proposal.md:15` beside J `/items/4/description`, without choosing source precedence.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent bounded source verification and 14-ID existing-owner mapping; revise findings identify accepted help/docs behavior, retain exit tension and reject unsupported index attestation."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-904.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python JSON extraction of root and items 0,1,2,4 with hashlib SHA256","result":"passed","summary":"14311 bytes; expected content digest, selected keys and comment/attachment counts verified."},
    {"command":"Local find/read and numbered document inspection; wc and scoped heading lookup","result":"passed","summary":"Complete required auth/demo proposal/design/spec sets, routing artifacts, current shell/permissions/session and bounded inventory read."},
    {"command":"Tests/build/browser/network/code audit/git-index inspection","result":"not-run","summary":"Outside bounded evidence-only inspection; no application or index assertions made."}
  ],
  "validationOutput": ["SHA256 30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4 matches work-item and metadata.","Current shell lines 91–142 already specify documentation-menu and introductory-help behavior."],
  "residualRisks": ["Profile-exit wording remains an owner reconciliation question, not approved logout behavior.","Linked wiki, attachment bodies, exact article/copy contents and historical test evidence were not verified.","No implementation, runtime integration, deployment or index state was inspected."],
  "diffSummary":"Only the authoritative review artifact written; no source/product/plan edits.",
  "reviewFindings":["revise: author report lines 118–119 reopen already-specified docs/help choices.","retain: primary exit wording conflicts with explicit approved logout-UI exclusion.","revise: author report line 140 attests an uninspected index."],
  "manualNotes":"Fresh local document inspection only. No actual input blocker; no task closure, source-precedence decision, product activation or writer authorization. Index attestation intentionally omitted."
}
```
