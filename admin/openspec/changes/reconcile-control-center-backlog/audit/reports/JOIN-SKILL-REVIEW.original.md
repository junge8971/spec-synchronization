# Lane 6 — MOS-1020 review join

Bounded read-only candidate evidence; not feature acceptance. HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Only this configured artifact written. No tests/build/typegen/network/browser/credentials or nested agents.

## Sources and prior evidence

Aliases: **A** = `openspec/changes/reconcile-control-center-backlog/audit`; **J** = `A/sources/jira-details-MOS-774/r1/content.json`; **API** = `A/sources/api-live/r2/content.json`; **S** = `openspec/specs/skill-review/spec.md`; **C** = `openspec/changes/archive/2026-10-02-mos-1020-skill-review`; **W** = `app/widgets/skill-review`; **F** = `app/features/skill-review`; **T** = `W/ui/skill-review.test.tsx`.

Exact member is **J `/items/9`**, key MOS-1020 (not the older aggregated index 64). `/description` requests: queue with skill selection, questionnaire, phrases and check results; five criteria (scenario completion, wording variation, editorial policy, sufficient phrases, understandable error behavior); mandatory reason AND text for return. It flags undefined API queue/criteria/return reasons/decision with actor/date/final status. Status `Ready for test` and updated `2026-10-16T19:22:31.894+0800` are source metadata, not delivery proof; attachments/subtasks are empty.

Reused first: `A/reports/SCENARIO-MOS-909.md:55–61` C02 and `A/reviews/R-SCENARIO-MOS-909.md:49,65–75`: approved MVP is separate review→whitelist, not invented approved/rejected aliases. Its r1 response-linkage assertion is qualified by accepted `A/reports/API-R2-STATUS-DELTA.md:39–100` and `A/reviews/R-API-R2-STATUS-DELTA.md:5,33–45`: current status response is a full card plus issuance field, not the old envelope. No repeated lifecycle/token audit.

Linked saved catalog wiki is historical CRUD context: `A/sources/wiki-241097511-readable/r1/readable-text.txt:418–490` §§2.5–2.6 supplies list/detail but list table omits status. Saved API independently publishes status filtering. This discrepancy does not mean the queue API is absent or select a source-precedence rule.

API locators below use JSON Pointer with slash escaping:
- **L** `/paths/~1api~1control~1api~1skills~1v1~1skills/get`
- **D** `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/get`
- **P** `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`
- **DTO** `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`

## Requirement → API → owner → code → written assertions → disposition

### R1020-01 Queue, selected questionnaire and phrases

**J `/items/9/description`, sentence 1** → **L `/parameters`** publishes status, limit, offset; **D** and **DTO `/properties/intents`, `/properties/version`** supply detail materials → **S:9–26**, **C proposal:7,26**, **C tasks:5–6** → `W/model/use-review-queue.ts:5–12` fixes review/pageSize20/name sorting and clamps page; `app/entities/skill/api/skill-registry-client.ts:54–78` sends server status/limit/offset; `W/ui/skill-review.tsx:11–66` selects queue skill; `W/ui/review-panel.tsx:12–44` reads detail; `W/ui/review-material.tsx:5–38` renders questionnaire and intents/phrases from that card.

Written assertions inspected: complete `W/model/use-review-queue.test.tsx`, test “reads only the requested review page…” asserts exactly `{status:'review',sort:'name',limit:'20',offset:'0'}` and offset20, empty items/page reset and isError. **T**, “distinguishes pending, error, retry and empty queue” asserts distinct messages and two fetches; “loads questionnaire and phrases from one detail…” asserts purpose, expected result, phrase, retry count3, no `/intents` request. “returns to a valid server page…” asserts accepted skill absent and final offset0. These are mocked-fetch assertions, not backend observations.

**Disposition: no implementation plan warranted for this already-owned MVP join.** Server queue exists through filtered catalog operation, not a separate review-item protocol. Main page grep `app/pages/skills/ui/skills-page.tsx:36–38` mounts actual widget, not a review placeholder.

### R1020-02 Five named criteria

**J sentence 2** → no criteria payload in **P `/requestBody` → `/components/schemas/ChangeSkillStatusRequest`** (status, expected_version, optional nullable reason only) → **S:28–40**, **C design:17**, **C tasks:10** explicitly approve local-only checklist → `F/constants/skill-review.constants.ts:1–7` contains all five exact labels; `F/ui/skill-review-decision.tsx:20–40` renders named native checkbox inputs and local-only explanation; `F/model/use-skill-review.ts:20–39` keys assessment by id/version/status, resets and requires all criteria.

**T** “requires all five criteria…” asserts count5, local explanation, keyboard toggle, disabled action with four, dialog after five, reset on version and skill change, no non-GET. “cancels without POST…” asserts exact status/version payload and no Storage.setItem. The test counts five rather than asserting every exact label; exact labels were inspected in constants. No claim of comprehensive URL/storage persistence testing.

**Disposition: no-op for approved local assessment.** Record full persisted criteria separately deferred; do not turn local checkboxes into backend decisions or equate these editorial criteria with readiness check types.

### R1020-03 Check results alongside materials

**J sentence 1** → **D `/description`**, **DTO `/properties/checks`**, `/components/schemas/SkillCheckResponse` publish stored check_type/status/blocking/message/checked_at. Detail prose allows empty checks and says GET does not run checks; it names anketa/phrases/exact_conflicts/semantic_conflicts/endpoint, NOT the manual review criteria → **S:11,84–89**, **C proposal:11,27**, **C design:16,21,28** defer displaying automatic results → `W/ui/skill-review.tsx:18–21` explicitly says results unavailable in MVP; `W/ui/review-material.tsx` renders questionnaire/phrases only; `app/entities/skill/api/skill-details-client.ts:15–51` is loose detail validation without checks validation.

**T** material assertions cover questionnaire/phrases, not rendered check results. No assertion inspected proves automatic check display, five readiness outcomes, or current-input correlation. This is explicit deferred UI, not fake successful results.

**Disposition: narrow planning clarification under existing skill-review deferred requirement**, not a fresh check engine or reopening MOS1019. Proposed exact current-planning wording: “MOS-1020: saved API publishes stored readiness checks in GET detail; review rendering remains deferred under the approved MVP. Coordinate any separately approved display with MOS-1019; do not describe published results as absent, infer readiness of current phrase revision, or substitute the five manual criteria for backend checks.” Preserve archived proposal/tasks. No newly authorized implementation or separate corrective owner needed here.

### R1020-04 Return requires reason AND text

**J sentence 3 and API-gap sentence** → `/components/schemas/ChangeSkillStatusRequest/properties/reason` is optional nullable string; **P `/description`** mentions review→draft as a return exempt from checks. Neither establishes mandatory reason dictionary plus free text nor a saved review decision → **S:82–89**, **C proposal:11,29**, **C design:11,21**, **C tasks:3,22** intentionally defer return → `F/handlers/skill-review.handlers.ts:39–68` only sends whitelist/version; `F/ui/skill-review-decision.tsx` offers approve and refresh, no return form; `W/ui/skill-review.tsx:18–21` communicates limitation.

**T** exact-payload assertion proves no reason/text/checklist in approval payload; no written return validation or persistence assertion was found in the fully read review tests. This is not an enabled placeholder action claiming success.

**Disposition: unresolved full-workflow owner decision, already attributed to skill-review**, not missing approved-MVP implementation. Exact proposed backlog wording: “MOS-1020 full return remains deferred: agree a return decision contract carrying required reason and text, validation and final-status semantics before exposing the action. Generic optional status.reason and documented review→draft do not satisfy that requirement or authorize a frontend fallback.” Do not invent codes or mapping rejected=draft; no duplicate corrective change.

### R1020-05 Decision actor/date/final status

**J API-gap sentence** → **DTO** includes skill author_user_id, created_at/updated_at/status/version; none is a review-decision actor/date. **P** returns through `/components/schemas/TsamResponseSchema_SkillTokenIssuanceResponse_/properties/data` to `SkillTokenIssuanceResponse`, whose unchanged card fields include status/version; accepted STATUS-01–04 retain issuance/security seam ownership. These fields establish status response, not a saved checklist/decision audit → **S:42–80,84**, **C design:5,19–20,26**, **C tasks:11–13,22** → `F/handlers/skill-review.handlers.ts:39–68` confirms only returned whitelist, warns on other status, blocks uncertain retry; `app/entities/skill/api/skill-details-client.ts:68–86` validates status request/skill id and consumes card; `W/ui/review-material.tsx:8–15` displays actual status and warns material is not immutable review snapshot.

**T** “cancels without POST…” asserts detail version7 despite queue version1, UUID idempotency key, single POST, whitelist success, cache/result and queue invalidation. “warns about a different server status…” asserts sandbox and absence of success. Refusal422/409, uncertain408/503/204/invalid200 and lost-response whitelist/review/read-error assertions distinguish refusal, read-before-new-command and no automatic replay. No inspected test proves review author/date persistence or retrieval.

Mock boundary: `mocks/domains-skills.mjs:270–290` checks expected_version, then assigns requested status and increments version; on change appends status history using `state.users[0]`, now(), optional reason. That is local status-history fixture behavior, not review-decision authorship or actual backend transition enforcement. Mocked success is not contract/deployment acceptance.

**Disposition: retain approved status-only action and deferred decision audit.** Proposed existing-owner wording: “MOS-1020 acceptance evidence covers local assessment and server-returned status only; actor/date and persisted decision remain unverified/deferred. Do not render skill author/updated_at, mock history, or token issued_by as review decision metadata.” No new policy, no additional states, no token-response fix duplicated here.

## Minimal planning / coverage result

Recommend parent-reviewed **MOS-1020 B→P** in `A/reports/G2-JIRA-MEMBER-JOINS.md` (current row found at line194: boundary only). Exact member requirements now join queue, five criteria, return and decision metadata to current implementation, assertions and explicit deferred owner. **P means partial requirement-level evidence, not feature completion**: automatic-results UI, return reason/text and persisted actor/date decision are not delivered by these joins. No independent claim for another member, no task checkbox changes and no new change proposed. Existing historical tasks remain as recorded, including their explicitly accepted test/format limitations (`C/tasks.md:23–27`); not current execution results.

## Actual reads and limits

Read exact J member via local JSON parsing; no sibling requirements audited. Read complete S and C proposal/design/tasks; C deltas were not separately read. Reused SCENARIO-MOS-909 C02 and its accepted review; targeted API-R2-STATUS report/review ranges above, not a new token audit. Parsed current saved API only for list/detail/status, request/detail/check schemas and review-named schema scan; not a full API completeness search. Read linked wiki excerpt §§2.5–2.6 only. Read complete review widget/hook/feature files and both review tests listed below, registry/detail clients and tabs explanatory component; inspected mock status-handler excerpt only. Page composition, other audit/member reports were grep locators, not complete reads. An initial combined documentary command exceeded display limit; C/S and accepted review sections were visible, and C02 was separately reread; no claim that unseen report lines were inspected.

All API statements concern saved publication, not live backend behavior. No current runtime/test pass, credentials, authorization, deployment, token retention or full return API absence certification. No browser/screenshots or missing attachment inference (this member has no saved attachments). No git index inspection; no clean-index claim. Parent package review remains required.

## Current-local SHA256 inputs

Hashes computed from current file bytes, not git-show; includes complete files even where only bounded portions were inspected. Alias expansion as above.

```text
0d1083ea677d8b380789a33f5e56cd30357132ee476bd3362dc31243fc89fd59 A/work-items/G2-SKILL-REMAINING-SEVEN.md
e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208 J
ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993 API
c6dd8857060fa4e87a7170fb604486d12d03a8e74d1ac24c4704554eba67b2df A/sources/wiki-241097511-readable/r1/readable-text.txt
51fdde74c8221ebec090d90cfe86bfe9b0df596afc12866d2312595d379582e1 S
059e40ef69d5460386ea14e3ae27c0e76a5adc2e97758b605f69f88eed72f7bb A/reports/SCENARIO-MOS-909.md
8c930323b3a2d6644d8ea4613ae490a5237c11ab55b1d67e0d0de56c5e67cb5c A/reviews/R-SCENARIO-MOS-909.md
feccf80cd07fdf235fb0200e4b16ffffc0153fac814bf1f8927ec6351960c474 A/reports/API-R2-STATUS-DELTA.md
2b505ed332f8a2c928e23111903688943092c50da18b57f7288fc49006739374 A/reviews/R-API-R2-STATUS-DELTA.md
e2fa76c3ed5d0b6eacd01a5661d44d024d84f58723f53d9543d8bba9a4d32d0d C/proposal.md
80a076f93f4e9802ba03d932e6b0340c12ed9dd00954b279b9652253fee364fa C/design.md
8f133d43d360664d73d350e9d5f960de3ff1980fdb5f9e111d2fe15d1fdd82d6 C/tasks.md
f7f21f46e732dcc2f0362c7edb23a6dee71852eb7fff94f7cc24d3dbf8ea34cc T
e4ebef5c6e6872b2450041f7c6028adc98d20d2a9bbe586d68b3401b43645884 W/model/use-review-queue.test.tsx
6cb41cb6759b323199ae47e98af3128c68a9ea303016bbe03f5119563cc1b8c9 W/model/use-review-queue.ts
2fc4d4483856f19e96f4a0892422817b31db54cb4bc06d681bd78eccd8be59df W/ui/skill-review.tsx
cb82afcc7cf192664d99b23512f720ff2d55a7b0e882599e5e94285ca41ff9b7 W/ui/review-material.tsx
be7de6f7a733198785bc5364d3c8311ba218d399508d9c601376b877ac58298f W/ui/review-panel.tsx
6716072a93cb3d04ff645c03134990ad74ffbf45340c52ef57c5a26bdf892c04 F/model/use-skill-review.ts
10d5abffa137a3ee763c9f5a474eda6be0cd94d00d34626158652e88ceb258a1 F/handlers/skill-review.handlers.ts
b662d6f942ee672f810879fc6d091eaf72f08e235433c2f442ec619ed574193b F/constants/skill-review.constants.ts
81e8de7f451e416852341af20504ca23c62e3c958077ac7d9b89a05a3e6c83fc F/ui/skill-review-decision.tsx
de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6 app/entities/skill/api/skill-details-client.ts
fe22d8076a52c22ea245853b2bbe3f7103a1f515776920a6ecf76b6a6fcd5969 app/entities/skill/api/skill-registry-client.ts
8b07da94425ce28c867b314ab972ec5ae1b58586ddaa821c82a6d49ec47774c8 app/pages/skills/ui/skills-page/skills-page-tabs.tsx
fc9e67e11fbbfde4412524de8901e659f929f7360c9e1e85ac8b36152e0b868c mocks/domains-skills.mjs
```

**Final:** five source-backed partial joins; existing MVP ownership retained; full return/decision and check-results rendering remain deferred. Only narrow planning qualifications and candidate B→P, no feature acceptance.
