# IMPL-MOS-1027 — bounded local implementation evidence

## Result and scope

**MOS-1027 remains P; zero new U-to-P transitions.** Static implementation and test assertions support the existing skill-card confirmation, reason/message validation, dedicated commands and read-based recovery. Duration and affected-surface details remain outside the approved MVP, although requested by the saved Jira item. The `/ops` page is a separate placeholder, not a second implementation of this skill-card control.

No publication, acceptance, feature closure or implementation change is proposed by this report. Parent disposition and independent review remain pending.

Only local read-only inspection and SHA-256 computation were performed. No writes, network, browser, tests, build, lint, typecheck, Git operations or nested agents occurred. No mandatory input was missing and no infrastructure failure occurred.

## Prior evidence read first

Before inspecting current implementation, read:

- `audit/reports/SCENARIO-MOS-1145.md`
- `audit/reviews/R-SCENARIO-MOS-1145.md`
- `audit/reports/DELTA-MOS-1145-TESTPLAN.md`
- `audit/reviews/R-DELTA-MOS-1145-TESTPLAN.md`
- Relevant `audit/decisions.md` entries **D-015, D-016–023 and D-030**.

Here and below, `audit/` means `openspec/changes/reconcile-control-center-backlog/audit/`.

Controlling qualifications retained:

- D-015 distinguishes specification coverage from implementation evidence.
- The **13.10.2026 prod→disabled→prod approval remains intact**, without implying an integration run or universal restoration guarantee.
- Reason-dictionary/free-text compatibility remains an existing owner question.
- D-020’s separate generic lifecycle scope is unchanged.
- D-030 accepts the attachment’s execution-integration and process-memory limitations only within its described task/version context.
- Historical unread-attachment statements are supplemented by the accepted test-plan report, not repeated as current missing-input claims.
- Historical auth approval and credential-free business mocks remain unchanged; no role mapping or new permission policy is selected.

The prior requirement audit was not rerun.

## Primary source and owning scope

**Exact assigned source:**  
`audit/sources/jira-details-MOS-774/r1/content.json#/items/15`

Inspected the complete selected item and adjacent `metadata.json`.

- Key: `MOS-1027`
- Summary: `[FE][Навыки] Добавить глобальное отключение и включение навыка`
- Status: `Ready for test`
- Updated: `2026-10-16T19:22:35.619+0800`
- Capture: `2026-10-16T11:49:06.782Z`
- `attachments`: empty; `subtasks`: empty.
- Metadata explicitly excludes comments, custom fields and attachment bodies.

`/items/15/description` requests:

1. Confirmation of consequences for all surfaces.
2. Mandatory reason and resident-facing message.
3. Work/disabled duration and affected surfaces from server data.
4. No equivalence between saving `substitute_response_text` and disabling a skill.
5. Reconciliation of platform-administrator versus `/ops` superadmin wording.

Its “API not defined” paragraph is historical source wording, not a current API-absence finding.

**Owning documents inspected:**

- `openspec/specs/skill-global-toggle/spec.md`, complete: “Server skill state”, “Confirm global disable and enable”, “Consistent global action outcome”.
- `openspec/changes/archive/2026-10-13-mos-1027-skill-global-toggle/design.md`, complete: UI/forms, contract ownership, recovery, approval and non-goals.
- Same archive’s `tasks.md`, complete: historical implementation/check records.
- Archived `2026-10-09-add-local-session-demo/{proposal.md,design.md,specs/control-center-mock-server/spec.md}`: credential-free mock and non-production-guarantee boundaries. Historical planning gate wording does not supersede accepted later approval.

## New evidence delta: expected / observed / unknown

Paths and named functions/test cases are exact locators.

| ID | Expected and source | Newly observed local evidence | Unknown / bounded disposition |
|---|---|---|---|
| **MOS1027-I01 — mounted owner and state** | Main spec “Server skill state”: prod/disabled strip; other statuses hidden; stale read blocks action. | `app/widgets/skill-details/ui/skill-details.tsx`, `SkillDetails`, mounts `SkillGlobalToggle` with read-error/fetching flags and GET refresh. Feature `ui/skill-global-toggle-content.tsx` returns null outside prod/disabled and renders textual status. `model/use-skill-global-toggle.ts` blocks action during read error, refresh, pending or required reread. Feature tests explicitly cover seven hidden statuses and read-error blocking. | **Update** existing implementation evidence, not product scope. Responsive classes are present; actual viewport rendering and keyboard/browser behavior were not executed. |
| **MOS1027-I02 — confirmation and fields** | Jira description; main spec “Confirm global disable and enable”. | Feature `ui/skill-global-toggle-dialog.tsx` names the skill and says the action affects all surfaces where connected. Disable is destructive. `ui/skill-global-toggle-fields.tsx` renders reason for both actions and message only for disable, with labels/error associations. Constants initialize empty drafts. `model/toggle-form.ts`, `validateToggleDraft`, trims and enforces reason 1–32 and nonblank disable message. | **Update** C07’s earlier specification-only coverage with actual code/assertions. UI wording is not proof that downstream surfaces apply the command. |
| **MOS1027-I03 — dedicated command, not substitute text** | Jira explicitly rejects equating substitute-response saving with disabling. Spec requires dedicated POST and forbids surface/status mutation as the toggle. | `handlers/skill-global-toggle-handlers.ts`, `buildToggleOperation`, builds reason/version/key and disable-only fallback. `app/entities/skill/api/skill-global-toggle-client.ts`, `toggleSkill`, sends only the dedicated `/skills/v1/skills/{id}/{disable|enable}` request. No `substitute_response_text`, generic status call or surface update occurs in this inspected path. Widget tests assert exactly one POST to the dedicated endpoint and exact body. | **Keep/update** existing owner; no duplicate implementation plan. This is bounded call-path evidence, not an audit of every editor or backend side effect. |
| **MOS1027-I04 — confirmation identity and uncertain outcome** | Main spec “Consistent global action outcome”. | `toggle-form.ts`, `isToggleSnapshotCurrent`, compares ID/status/version. `confirmToggle` uses synchronous locking, preserves draft on refusal and records only returned status. `refreshAfterToggle` separates command success from failed GET; `refreshToggle` closes confirmation and requires fresh confirmation. `ui/skill-global-toggle.tsx` keys content by skill/session owner/generation. Mutation hook has `retry:false` and invalidates the affected detail plus non-detail skill queries. | **Update** existing recovery evidence. No client version increment observed. Server transactionality, durable deduplication and execution integration remain unverified. |
| **MOS1027-I05 — receipt validation** | Main spec requires matching skill/action, valid server data and no fabricated target. | `skill-global-toggle-schema.ts` validates UUID identity, known status, required action fields and date-time; input validates UUIDv7 skill ID, UUID key, positive integer version and trimmed fields. Client checks matching skill ID/action and exact success status 200. It does not constrain returned status to an assumed action target. | **Keep** approved server-derived behavior. This does not solve the existing externally-disabled non-prod restoration question. Do not add a hardcoded prod result. |
| **MOS1027-I06 — impact and duration boundary** | Jira requests server-derived duration and affected surfaces; main spec expressly excludes durations/statistics/surface lists; archived design excludes impact/replay APIs. | Complete inspected toggle UI renders state, generic global-effect explanation, fields, notices and refresh—not duration, affected-surface enumeration, impact counts or preview. Inspected command response schema has status/action receipt, not these display inputs. | **Keep/question**, enriching existing C13 rather than declaring a regression. Broader Jira demand remains unresolved scope/contract work with existing owners. No timer, guessed preview endpoint or activation candidate is authorized. Absence is bounded to this UI/schema, not all backend APIs. |
| **MOS1027-I07 — mock semantics** | Demo contract permits coherent credential-free business fixtures, explicitly not production guarantees. | `mocks/skill-operations.mjs`, `toggleSkill`, checks existence/version/state, stores previous status in a map, restores it or defaults to draft, increments version/time and appends action/status-history records. Actor is `state.users[0]`, not the visitor. `mocks/api-update.test.mjs`, named toggle test, asserts replay, version/history counts, restored original status, stale-version refusal and reset isolation. | **Update** local evidence only. Mock fallback-to-draft, 409 conventions, fixed actor and in-memory state are not backend restoration/auth/persistence guarantees. The test’s original fixture status does not establish an eight-state matrix. |
| **MOS1027-I08 — global operations comparison** | Jira mentions differing card versus `/ops` role prose; existing owners must remain distinct. | `app/routes/operations.tsx` exports `OperationsPage`. `app/pages/operations/ui/operations-page.tsx` renders “Состояние системы” tabs whose contents say “Раздел в разработке”. It does not mount the inspected toggle feature. Actual feature invocation is in the skill card. Feature controls use explicit `*`, not platform-admin/superadmin role strings. | **Keep existing ownership / justified no-op.** This limited composition comparison is not MOS-1145/backend delivery acceptance or a neighbor-page audit. Existing permission policy is preserved, not newly approved or reassessed. |

## Actual assertions inspected — not executed

### Feature component tests

`app/features/skill-global-toggle/ui/skill-global-toggle.test.tsx`, complete:

- Hidden strip for seven non-actionable statuses.
- Explicit wildcard visibility and read-error blocking.
- Empty defaults, whitespace rejection, 33-character rejection, trimmed 32-character acceptance.
- Cancel sends no mutation and restores trigger focus.
- Enable requires reason and omits fallback.
- Double submit produces one mutation; late other-skill response is ignored.
- Changed version blocks old confirmation until reread and fresh confirmation.
- Network/malformed-success recovery reads without automatic resend.
- Known 422 rejection preserves draft without claiming success.
- Confirmed status survives failed GET while further command is blocked.
- Session replacement prevents application of pending response.

These tests mock the entity mutation; they do not independently establish wire/schema behavior.

### Client tests

`app/entities/skill/api/skill-global-toggle-client.test.ts`, complete:

- Exact dedicated paths, body, key header and one request.
- Invalid identifier/key/version/reason/fallback rejected before HTTP.
- 32-character boundary accepted.
- Mismatched skill/action, malformed status/required fields/time/null rejected without retry.
- 204/202/403/409/422/503 not accepted as success.
- Raw validation error preserved; business-error envelope rejected.
- Lost response remains unknown with one attempt.

The “published request” fixture deliberately permits a known returned status without an action-target invariant; it does not prove production transition semantics.

### Mounted skill-card tests

`app/widgets/skill-details/ui/skill-global-toggle.test.tsx`, complete:

- Both actions reread full card, use server version `old + 7`, invalidate registry and send exactly one dedicated POST.
- Changed cached version blocks confirmation.
- Late response does not affect another skill.
- Returning to the original card still receives invalidation from its old completed command.
- Failed refresh retains old version, reports confirmed command separately and recovers by GET without another POST.

These are component tests with stubbed fetch, not live integration or browser execution.

### Mock test

`mocks/api-update.test.mjs`, selected named test **“skill toggle keeps versions, previous status, history and idempotency coherent”** (lines 66–117), plus setup:

- Missing key/empty fallback refusal before state change.
- Disable increments version; identical-key replay returns identical response.
- Changed reason with reused key conflicts.
- Stale-version enable conflicts.
- Disabled filtering includes the skill.
- Enable restores fixture predecessor and yields two history/action records.
- Repeated enable is refused without another action; new mock state has no prior action records.

The surrounding unrelated test cases were not audited. No test server was started.

## Candidate disposition summary

- **Update:** MOS1027-I01–I05 and I07 provide the previously missing static implementation/assertion layer.
- **Keep:** Existing MOS-1027 ownership, historical approval, confirmation/recovery rules, existing MOS-1031 reader gate and separate lifecycle boundaries.
- **Question retained:** I06 impact/duration/surface data; prior C04/TP02 reason compatibility; C03 restoration and C13/TP10 effective integration. No new policy answer inferred.
- **No-op:** I08 does not authorize `/ops` implementation or a duplicate toggle plan.
- **New product/remediation candidate:** none established by this bounded inspection.
- **Population:** all selected members already P; **zero new U-to-P**, no global gate closure.

Only the parent may accept or queue these dispositions.

## Input integrity

SHA-256 values below were computed from current local bytes. Source content matched its metadata. Hashes establish byte identity, not external freshness, deployment revision or correctness.

Abbreviations:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `G` = `openspec/changes/archive/2026-10-13-mos-1027-skill-global-toggle`
- `F` = `app/features/skill-global-toggle`
- `E` = `app/entities/skill`
- `W` = `app/widgets/skill-details/ui`

| Input | SHA-256 |
|---|---|
| A/work-items/WAVE-D094-LOCAL-EIGHT.md | `da5e3681c7b882ef8fc6a44a50e7dd8562068f43ac4a74c71a8f5b82e61fd0e0` |
| A/sources/jira-details-MOS-774/r1/content.json | `e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208` |
| A/sources/jira-details-MOS-774/r1/metadata.json | `a76eb6f93c564b94c6c627e4209a449361ef0da69415b49033c584e16fcca1ec` |
| A/reports/SCENARIO-MOS-1145.md | `dd8d4dd21e05142991f0b7d32492b5018ac16fd3aca1aeced36b796e079749d9` |
| A/reviews/R-SCENARIO-MOS-1145.md | `30e9edd2e84c7e3a89e2eea8fea3daac1c757069df931c303adb40820e774e40` |
| A/reports/DELTA-MOS-1145-TESTPLAN.md | `0986b8b33a5bf7e4f40e787e35bd6c62ab6733e0852766cbdd9f44f51b310597` |
| A/reviews/R-DELTA-MOS-1145-TESTPLAN.md | `b202dc19f8e9775feaa30dc4d5bdd2517c7a58f047495a5c30d68a475002e27a` |
| A/decisions.md | `dbf814a620a9ee1ff1435e912db50efb4672c3e40712f684855a14cc91df796e` |
| openspec/specs/skill-global-toggle/spec.md | `80dc6e3d1bdb7db54f74171f9cc8dae9e68494e9de158795f59ff2b72c07b2e9` |
| G/design.md | `dee80a6d387f4e8558e3e028506982a8008a89e82c3bc449207db477e9e9763e` |
| G/tasks.md | `a124742e156ac4982d06f9e26fe8e4b5c8d5889fb72e77c553e24b3fd12b769c` |
| F/constants/skill-global-toggle.constants.ts | `e692567e5a99ed9f1a4a08632a2d64f4a876a896bc3099def36eebb909114de0` |
| F/handlers/skill-global-toggle-handlers.ts | `ca5c2a2ade05b0c1f3399b97fdf0ca1411a261ccf4fa4292800007b231319c5f` |
| F/model/toggle-form.ts | `430d799232d501466e48e347d254275aaa22c5fd5af919018589034200211f3e` |
| F/model/use-skill-global-toggle.ts | `64ae804d9cc41862a406eee27cb425a24a1bf0246749540456dad8c16fd47542` |
| F/ui/skill-global-toggle.tsx | `0135987036621f6bfff8aa2d594ff27d7f4f011d0d3a4a6c2e7afc122a50d5fb` |
| F/ui/skill-global-toggle-content.tsx | `72874149a4504fe82d03c8fa62f82679381b8f5f47c67b0b45cc5f41facd59a0` |
| F/ui/skill-global-toggle-dialog.tsx | `dcc21285a49274410195dbd77068ca4a0c1b9a220aa9b525eb61d54571aa9596` |
| F/ui/skill-global-toggle-fields.tsx | `73ffc953cd04a7642744a04d8bb4a9f108ca171dd3d6ae2a33814c244437cc8d` |
| F/ui/skill-global-toggle.test.tsx | `f9d4ea6f3fec55417c199022e73079bf36da718ab41d3aeb51e88f56db4360f4` |
| E/api/skill-global-toggle-client.ts | `9cc929d9399ce51e62a7575c486cc43dd09fa07add0793a54c2377ba197459a9` |
| E/api/skill-global-toggle-schema.ts | `4e48f7549a702753a69abd08d417a3c7b6e57a853fe37041c86ec34dce029786` |
| E/api/skill-global-toggle-client.test.ts | `b4309ea5fe6d1d1a6795b1ede8e69a418b9c01db3eb5af964493ccb3c5d9abce` |
| E/model/use-toggle-skill-mutation.ts | `99343431062ebc28f2b4dff9b69a0ca5d1a58837268e8533352fff9280d3db03` |
| W/skill-details.tsx | `d7a1b1c2f751f4a00170637ae0b5f997be2448d4254b1ea8f5440d899101e067` |
| W/skill-global-toggle.test.tsx | `4fa1b2a80e1dc2f9671d96daccc43e51a6b30f07d7460ea7885ee26bf9cd768e` |
| app/pages/operations/ui/operations-page.tsx | `6100902a8833602c9d6fcc461429b9185079b7cdb6893829f30d588ee74753e9` |
| mocks/skill-operations.mjs | `da6e06c335b4949672f2e0176135a4030493e5e00d8195a30ebae02c5f911eda` |
| mocks/api-update.test.mjs | `793fb807cae6203c3d1336c15be1fd0b09d785b949e601a7dca75ee9c1e74ddb` |

## Historical and deployment limits

- Saved Jira status and archive checked tasks are historical records, not fresh test or delivery evidence.
- Archived reported passing commands were not rerun or re-attested.
- Current remote API publication, deployments, backend authorization, reason acceptance, restoration selection, persistence, audit delivery, actual answer suppression, fallback delivery and propagation latency remain unverified.
- Test-plan limits remain attributed to the accepted document’s task/version, not projected onto every deployment.
- No current API-wide absence claim was made. Local schema inspection does not replace a full contract audit.
- Tests were read only. No visual responsiveness or real keyboard interaction was verified.
- Git HEAD/index/staging state was not inspected. The wave’s baseline identifier is assignment context, not a fresh Git attestation.
- No direct output file was written; this complete report is returned for runtime persistence at the authoritative assigned path.