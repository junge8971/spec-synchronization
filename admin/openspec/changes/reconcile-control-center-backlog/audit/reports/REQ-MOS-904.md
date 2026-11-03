# REQ-MOS-904 — bounded requirements evidence audit

## Result and scope

MOS-904 contains header/navigation requirements, not proof of implementation. Its profile-with-exit wording conflicts with the approved scope excluding logout UI; retain the requirement as unresolved rather than implement or silently reinterpret it. Production-demo exclusions do not cancel approved local mocks. No task closure, deployment conclusion, source-code coverage claim, or product activation follows from this report.

Fresh local reading only: inspected Jira items 0, 1, 2 and 4, collection metadata, and both required approved changes' proposal/design/specs. No linked service, attachment body, code, tests, plan, or other issue detail was inspected. No network/browser/test/build actions were performed. Only this report was intentionally written.

## Files retrieved and provenance

All paths below are repository-relative. `J` means `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-shell-details/r1/content.json`; `M` is its sibling `metadata.json`. JSON pointers below are exact locators; quoted fragments disambiguate multiple requirements inside a description string (there are no sub-field pointers into its prose).

- Assignment: `openspec/changes/reconcile-control-center-backlog/audit/work-items/REQ-MOS-904.md`, complete, lines 1–9.
- `J`: root `/sourceId`, `/retrievedAt`, `/allowlist`, `/limitations`; selected objects `/items/0`, `/items/1`, `/items/2`, `/items/4` only. Root has six items and six allowlisted keys. Selected keys verified as MOS-624, MOS-672, MOS-673, MOS-904 respectively. Other issue bodies were not extracted or reviewed.
- `M`: complete metadata, including `/membership`, `/collection`, `/comments`, `/limitations`, `/redactions`.
- Verified local content byte length: **14311**; SHA256 **30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4**, exactly matching assignment and `M` `/sha256` and `/bytes`.
- Separately computed metadata SHA256: **ae842c6c481369e871263f49ad0c58fc9b078ea760c9bb37c20aa400a8854dcb**. The supplied expected hash is for content, not both files; no independently supplied metadata digest was available.
- `J` and `M` `/retrievedAt` agree: **2026-10-16T12:45:22.199Z**. Selected per-item timestamps: MOS-624 `12:45:21.394Z`, MOS-672 `12:45:21.471Z`, MOS-673 `12:45:21.808Z`, MOS-904 `12:45:22.111Z`, all on 2026-10-16.
- Metadata reports same-origin read-only GET from verified Jira origin, exact allowlist, selected fields/comments and attachment metadata only. This is collector-recorded provenance, not independently revalidated origin authenticity. Digest verification proves local snapshot consistency, not remote truth.
- `M` `/membership` attributes membership to `jira-hierarchy/r1/content.json results[0] MOS-624; members 672/673/674/904/905`. That upstream hierarchy was not reopened under this bounded assignment. All four selected `J` objects have `/parent: null` and empty `/subtasks`; therefore the detail snapshot does **not** independently establish parent-child relationships. MOS-624 is parent context by collection provenance, not by a populated parent field.

### Counts verified against metadata

| Issue pointer | Key | Comments startAt / maxResults / total / actual items | Attachment metadata count | Recorded status |
|---|---|---|---|---|
| `/items/0` | MOS-624 | 0 / 0 / 0 / 0 | 0 | Backlog |
| `/items/1` | MOS-672 | 0 / 1 / 1 / 1 | 3 | CLOSED |
| `/items/2` | MOS-673 | 0 / 1 / 1 / 1 | 3 | CLOSED |
| `/items/4` | MOS-904 | 0 / 2 / 2 / 2 | 0 | Ready for test |

Corresponding `M` `/comments/0`, `/comments/1`, `/comments/2`, `/comments/4` report matching counts/totals and `complete: true`. Completeness is as reported for this capture, not a claim about later comments. No custom fields or attachment bodies were collected. Comment objects contain id/body/created/updated but no author identity; author attribution cannot be verified.

### Approved local scope files read

Prefix `AUTH` = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`; prefix `DEMO` = `openspec/changes/archive/2026-10-09-add-local-session-demo`. These aliases expand to exact paths for all citations below. Complete proposal/design/spec files were read before scope comparison:

| File | Lines read | Relevance |
|---|---:|---|
| `AUTH/proposal.md` | 1–38 | Approved real-session scope, no logout UI/new OIDC |
| `AUTH/design.md` | 1–171 | Session ownership, mode selection, unresolved deployment gates |
| `AUTH/specs/control-center-api-integration/spec.md` | 1–64 | Bootstrap/error boundaries, no fixture success inference |
| `AUTH/specs/control-center-http/spec.md` | 1–71 | Credentials and backend authorization boundaries |
| `AUTH/specs/control-center-mock-server/spec.md` | 1–27 | Preserve credential-free business mocks |
| `AUTH/specs/control-center-permissions/spec.md` | 1–89 | UI policy and documentation access |
| `AUTH/specs/control-center-shell/spec.md` | 1–101 | Navigation ownership, route availability and deferrals |
| `AUTH/specs/mpmm-session/spec.md` | 1–138 | Confirmed principal, shared-session limits |
| `DEMO/proposal.md` | 1–28 | Approved local controls and confirmed header |
| `DEMO/design.md` | 1–70 | Fixed fixtures, separate panel, no logout |
| `DEMO/specs/control-center-mock-server/spec.md` | 1–106 | Production isolation and no mock RBAC |
| `DEMO/specs/control-center-shell/spec.md` | 1–55 | Branding, profile presentation, accessibility |
| `DEMO/specs/local-session-demo/spec.md` | 1–123 | Mode configuration, profiles, response scenarios |

These are scope constraints, not evidence that their implementation or integration gates passed. Archived location is not used as deployment proof.

## Atomic candidate requirements

All IDs are stable within this report. Rows 001–014 come exclusively from primary MOS-904 description, `J` **`/items/4/description`**, not from comments or approved-scope text. All remain candidates for reconciliation, with no completion assessment.

| ID | Exact source fragment | Atomic candidate / unresolved detail |
|---|---|---|
| REQ-MOS-904-001 | «Заменить старый бренд» | Replace old branding. Jira does not specify the replacement mark or exact label here. |
| REQ-MOS-904-002 | «жёстко заданные ФИО» | Remove hardcoded personal name; approved confirmed-principal presentation constrains the replacement. |
| REQ-MOS-904-003 | «/роль» | Remove hardcoded role display; this does not authorize a role editor or grant permissions from a label. |
| REQ-MOS-904-004 | «Доработать существующие header» | Update existing header. Component name is Jira's target wording, not verified source architecture. |
| REQ-MOS-904-005 | «SidebarHeader» | Update sidebar header. Exact visual change unspecified here. |
| REQ-MOS-904-006 | «SidebarContent» | Update sidebar content. Exact visual change unspecified here. |
| REQ-MOS-904-007 | «SidebarFooter» | Update sidebar footer. Exact visual change unspecified here. |
| REQ-MOS-904-008 | «Добавить профиль» | Add profile UI; precise content/interaction comes from separately approved scope, not this phrase. |
| REQ-MOS-904-009 | «с выходом» | Requested exit action associated with profile. **Unresolved scope conflict:** no approved logout UI or global MPMM logout is authorized. Do not invent local logout semantics. |
| REQ-MOS-904-010 | «переход к командам» | Provide navigation to teams, subject to confirmed permissions and actual route availability. No team-management expansion implied. |
| REQ-MOS-904-011 | «контекстное меню статей документации» | Provide contextual article menu. Article inventory, placement and target behavior are unspecified in the description. |
| REQ-MOS-904-012 | «Доступность разделов брать из auth-контекста» | Derive section availability from confirmed access context, within the already approved UI-only permissions policy; no new auth policy/API inferred. |
| REQ-MOS-904-013 | «Демонстрационные reset, переключение произвольной роли и сценарии показа не переносить в рабочий контур» | Exclude demo reset, arbitrary-role switching and show scenarios from the working environment. The three excluded controls share one explicit boundary; approved local demo remains permitted. |
| REQ-MOS-904-014 | «Подсказки первого входа и повторное открытие справки оставить как справочную UI-функцию» | Retain first-entry hints and repeatable help as informational UI, not a demo/auth workflow. First-entry persistence and help content need decisions. |

For independent reconciliation of the compound prohibitions/help clause without changing the parent IDs: REQ-MOS-904-013 covers three separately verifiable prohibitions (reset; arbitrary role switch; show scenarios), and REQ-MOS-904-014 covers two separately verifiable behaviors (first-entry hints; reopening help). These are not extra requirements from another source.

## Source distinctions: history, claims and status

### Parent context, not header acceptance criteria

`J` `/items/0/summary` names «[KR] Каркас административной панели». `/items/0/description` lists the development cycle (product formulation, analysis, development, testing, release), says there will be no changes for the user, and links wiki pages 223087110 and 222659162. This outline does not specify the MOS-904 header or establish screenshot contents. The links were not followed.

### Historical header/navigation descriptions

- MOS-672 `J` `/items/1/description`: «Создать шапку по контенту идентичную скриншоту и примеру» plus image reference. This is historical header parity intent, **not recoverable visual requirements** without the referenced bodies.
- MOS-673 `J` `/items/2/description`: «Сделать навигацию аналогичную по наполнению согласно примеру и скриншоту» plus image reference. Same limitation; no menu inventory inferred.
- MOS-672 attachments `/items/1/attachments/0..2`: IDs 817138 (`image-2026-09-03-13-26-35-746.png`, 22057 bytes), 825952 (`image-2026-09-22-16-31-27-903.png`, 17129 bytes), 817137 (`Прототип ЦАМ, версия MVP.html`, 1158654 bytes).
- MOS-673 attachments `/items/2/attachments/0..2`: IDs 817141 (`image-2026-09-03-13-29-40-640.png`, 24010 bytes), 826497 (`image-2026-09-23-12-21-03-315.png`, 31195 bytes), 817140 (`Прототип ЦАМ, версия MVP.html`, 1158654 bytes).
- Names, MIME types, sizes and URLs are metadata only. Equal prototype filenames/sizes do not prove identical bodies, a shared version, or any UI content.

### Comments are claims, not verified tests or requirements

- MOS-672 `/items/1/comments/items/0/body`, id **1114541**, created/updated **2026-09-22T21:32:51.609+0800**: reports successful testing at `https://mobile-a-tech.mos.ru/tsam-panel` and references a screenshot. Test scope/results/artifacts were not available or verified.
- MOS-673 `/items/2/comments/items/0/body`, id **1115041**, created/updated **2026-09-23T17:21:09.555+0800**: analogous test claim and screenshot reference. Neither CLOSED status proves present implementation, acceptance of MOS-904, or deployment.
- MOS-904 `/items/4/comments/items/0/body`, id **1117112**, created/updated **2026-09-25T20:23:52.388+0800**: claims a help button with introductory walkthrough; navigation groups main menu/«Аналитика»/«Эксплуатация»; a «Состояние системы» link not yet leading to a working page; documentation at menu bottom and quick article menu. Keep as reported change commentary, not additional primary requirements or verified current behavior. Its skills/surfaces registry loading/empty/error/pagination discussion is out of this header/navigation assignment and was not expanded into candidates.
- MOS-904 `/items/4/comments/items/1/body`, id **1117939**, created/updated **2026-09-28T19:02:50.149+0800**: «И пути для апи поменял». No old/new paths, operation list or contract evidence; no API requirements extracted.
- MOS-904 `/items/4/status` is **Ready for test**, `/items/4/updated` **2026-10-16T19:22:21.694+0800**. Status is a recorded workflow label, not test success. Comments predate this update; no field history establishes which description version they assessed.

## Ownership and approved-scope tensions

1. **Profile versus exit:** `AUTH/proposal.md:15`, `AUTH/design.md:25,93–99`, `AUTH/specs/control-center-shell/spec.md:3–5` exclude own OIDC/logout UI and global MPMM logout. `DEMO/design.md:42–46` expressly says no logout; `DEMO/specs/control-center-shell/spec.md:24–46` authorizes confirmed FIO/email/roles and accessible profile menu, but prohibits global logout in real mode. REQ-MOS-904-009 needs explicit owner resolution; none of these sources authorizes deleting shared tokens or adding a logout endpoint.
2. **Confirmed header, not synthetic administrator:** `DEMO/specs/control-center-shell/spec.md:24–41` defines name/email fallback, empty roles, text-only rendering and hiding stale personal data during checking/error. These constrain candidates 002/003/008; they are separate approved requirements, not text present in Jira.
3. **UI availability versus authorization:** `AUTH/specs/control-center-permissions/spec.md:7–36,58–79` assigns visibility to confirmed permissions, not role names; backend authorizes requests and object scopes. Static documentation/help is available to any confirmed principal. Do not interpret Jira's “auth-context” as a new API/model, frontend request ACL or unrestricted grants.
4. **Navigation and deferrals:** `AUTH/specs/control-center-shell/spec.md:22–64` already owns grouping, `/teams`, `/ops`, `/metrics`, `/docs`, empty groups, missing-route handling and explanations for unfinished content. The older comment about the non-working system-state link neither cancels these approved constraints nor proves the feature now works. Permissions must not activate an unavailable API or turn placeholder content into completed functionality (`AUTH/specs/control-center-permissions/spec.md:23,60`).
5. **Working contour versus local mocks:** `DEMO/specs/control-center-shell/spec.md:3–20` separates production shell from the local «Моки» panel. `DEMO/specs/local-session-demo/spec.md:7–28,45–82` permits fixed none/viewer/editor/full fixtures and fixed response selection only in configured local demo, without real credentials or role editing. `yarn dev` defaults to mocks; dev opt-out and production use real session independent of hostname. T is a current backend address, not an auth switch. Do not cancel local mocks or introduce arbitrary-role production tools based on candidate 013.
6. **Help is not a backend entitlement:** Primary description keeps hints/reopening as informational UI. Approved shell preserves help on mobile (`DEMO/specs/control-center-shell/spec.md:12–15,43–46`); static help remains available with confirmed no-business-grants principal (`AUTH/specs/control-center-permissions/spec.md:34`; `AUTH/specs/control-center-shell/spec.md:61–64`). Neither source specifies complete walkthrough copy or first-visit storage semantics.
7. **No rollout inference:** `AUTH/design.md:139–141,164–171` and `DEMO/proposal.md:28` retain real integration verification gates. Local documents, test comments and archived changes do not establish shared-session origin compatibility, CORS, refresh rotation or server-side enforcement in any deployment.

## Gaps and questions for owners

No blocker prevents producing this bounded report; the following block requirement finalization, not this evidence audit:

- **Session/product owner:** reconcile «профиль с выходом» with the approved no-logout scope. Is the Jira wording to be corrected/deferred, or is a separately approved change needed? No new exit behavior is assumed here.
- **Contract owner:** MOS-904 `/items/4/description` links wiki **241079770** (API contract for entry/session management), not collected in this source bundle. Obtain a separately authorized snapshot/provenance before relying on it. No assumption that it matches or supersedes approved local auth scope; no link followed.
- **Design/product owner:** which branding asset and historical example version are authoritative? The approved demo shell specifies «Центр управления» / «Цифровой ассистент» (`DEMO/specs/control-center-shell/spec.md:5`), but attachment content and visual parity cannot be established here.
- **Navigation owner:** confirm present intended entry points and explanatory state for unfinished teams/system-state content under the existing approved route policy. This is not a request to activate deferred functionality.
- **Documentation owner:** supply approved article inventory/order, context-menu placement and behavior, destinations, and treatment of missing articles; the primary description supplies no inventory.
- **Help owner:** define first-entry trigger, dismissal/reopening interaction, persistence/reset and content/versioning, including mobile/keyboard behavior. Preserve approved accessibility; do not invent storage or auth dependencies.
- **Evidence owner:** historical screenshots/prototype bodies, test cases/results and comment author identity are absent. Their absence limits visual/test claims; no recovery or collection was attempted.

## Validation and residual risks

Manual evidence checks used local SHA256, byte length, JSON structure and selected-item extraction; source counts and exact pointers were compared with collection metadata. No application checks were run because this assignment prohibits them. Source hash matches; selected comment counts match; no implementation conclusion is supported. Remaining risks are the unresolved exit wording, unavailable wiki/attachment contents, unverifiable remote provenance beyond collector metadata, historical comments lacking author/version context, and absent code/deployment verification by design.

```acceptance-report
{
  "criteriaSatisfied": [
    {"id": "criterion-1", "status": "satisfied", "evidence": "Bounded report preserves primary requirements, historical/test comments and approved scope separately; includes exact JSON pointers, verified digest/counts, unresolved questions and residual risks."}
  ],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-904.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command": "sha256sum openspec/changes/reconcile-control-center-backlog/audit/sources/jira-shell-details/r1/{content,metadata}.json", "result": "passed", "summary": "Content matches supplied SHA256; metadata digest recorded separately."},
    {"command": "Local Python JSON inspection of root metadata and items 0,1,2,4", "result": "passed", "summary": "14311 bytes; six items; selected keys, comments and attachment counts verified."},
    {"command": "Application tests/build/browser checks", "result": "not-run", "summary": "Forbidden by bounded evidence-only assignment."}
  ],
  "validationOutput": ["Content SHA256 matches 30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4", "Selected comment counts 0,1,1,2 match reported totals and metadata."],
  "residualRisks": ["Profile-exit wording conflicts with approved no-logout scope.", "Wiki241079770 and attachment bodies unavailable in the inspected bundle.", "Collector provenance is recorded, not independently remotely authenticated.", "No implementation, test coverage, integration or deployment verification was performed."],
  "noStagedFiles": true,
  "diffSummary": "Only the assigned requirements evidence report was intentionally written; no source/product/plan changes.",
  "reviewFindings": ["Scope tension: MOS-904 /items/4/description requests exit; approved auth proposal line 15 excludes logout UI."],
  "manualNotes": "Read both approved changes' complete proposal/design/spec sets before scope comparison. No git staging was performed; staging state was not inspected. Task statuses and comment claims were not treated as acceptance or rollout evidence."
}
```
