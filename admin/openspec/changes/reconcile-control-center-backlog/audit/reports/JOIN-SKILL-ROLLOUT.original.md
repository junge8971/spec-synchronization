# Lane 7 — MOS-1021 bounded join

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Static local evidence only; no feature acceptance.

## Sources and prior evidence

A = `openspec/changes/reconcile-control-center-backlog/audit/`; J = `A/sources/jira-details-MOS-774/r1/content.json`; API = `A/sources/api-live/r1/content.json`; S = `openspec/specs/skill-bulk-rollout/spec.md`; R = `openspec/changes/archive/2026-10-05-mos-1021-skill-bulk-rollout/`; F = `app/features/skill-bulk-rollout/`; W = `app/widgets/skills-registry/ui/`.

Exact member read: J `/items/10`, key MOS-1021, description: checkboxes/selected panel; select-all means shown rows until API says otherwise; eligible agreed→whitelist and whitelist→prod; agreed batch OR explicitly permitted single commands with bounded parallelism and per-skill report; API mass-transition/per-object/partial-success uncertainty. Saved status Ready for test is not acceptance. Attachments array is empty.

Reused before targeted implementation inspection: `A/reviews/R-G2-MAIN-CAPABILITY-JOINS.md:131` limits existing skill-bulk join to lifecycle transition provenance, not execution; `A/reviews/R-SCENARIO-MOS-909.md:49` preserves approved-status deferral versus separately approved review capability. Initial accepted-export evidence discovery (`A/reviews/R-MOS-1409.md:22,27`) identifies shown-row selection and historical selection owner; no export audit repeated. `A/reports/G2-JIRA-MEMBER-JOINS.md:195` currently marks this member B because selection/execution was not audited.

## Requirement joins

| ID / exact member clause | Saved API / scope | Spec and historical owner | Actual implementation / written assertions | Disposition |
|---|---|---|---|---|
| RO1 `/items/10/description`, first two sentences: checkboxes, panel, shown rows | API `/paths/~1api~1control~1api~1skills~1v1~1skills` is ordinary list; no whole-filter selection contract inferred | S “Visible-row selection”; R proposal What Changes; tasks 1.1 | W `skills-registry-table.tsx:23–37,65–80` uses `items.map(id)`; `skills-registry.tsx:41–53,119–125` supplies request-keyed current items; F `model/use-skill-bulk-rollout.ts:27–33,46–49,69–74` resets view and filters selected IDs. W `skills-registry.test.tsx:24–58` asserts 10 selected rows, 11 checked boxes including header, reset on page/query/sort/status change, keyboard selection, mixed-state and cancel without POST | Concrete member join; no corrective feature owner needed |
| RO2 description “согласованные в белые списки, из белых списков в прод” | API `/components/schemas/SkillStatus/enum` has nine values including whitelist/prod, no approved; status POST description says transition dictionary controls admissibility and fresh readiness checks may block | S “Contract-backed eligible rollout”; R proposal bullets and Impact explicitly record user-approved whitelist→prod-only MVP, deferred agreed→whitelist, review not an alias; tasks opening retains boundary | F `model/rollout-validation.ts:17–29` rejects empty/non-whitelist/unavailable selection; hook `:47–49` checks snapshot equality; handler `:12–29` sends prod. W test `:41–58` blocks mixed selection. F hook test `:75–102` changes status/version and asserts no call, blocks stale reads/cancel/hidden rows | Preserve historical scope, not a new fallback authorization. Wider member clause remains consciously deferred; no new status or policy |
| RO3 description batch OR explicitly allowed bounded singles | API `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`: required UUID header, UUID7 ID, ChangeSkillStatusRequest. `/components/schemas/ChangeSkillStatusRequest` requires status/expected_version≥1, optional nullable reason. Inspected skills-path inventory contains no batch operation; this is saved-publication scope, not live absence proof | S “Sequential commands and per-item outcome”; R proposal Impact explicitly records user agreement to sequential singles; R design Decisions says no batch/fan-out and maximum one. Tasks 2.1 | F handler `:42–80` synchronous lock and awaited loop; `:12–18` fresh random UUID/confirmed version. Entity `app/entities/skill/api/skill-details-client.ts:68–87` validates ID/key/body, POSTs, validates returned identity. W test `:60–134` holds first response, double-clicks, asserts one POST before release then two, exact prod/version bodies and distinct UUID-shaped keys | No batch-policy inference. Existing explicit permission satisfies the alternative planning route; no need to reopen API gate for this MVP |
| RO4 description per-skill report / partial-success uncertainty | Same POST returns one `TsamResponseSchema_SkillResponse_`, not a group result. Description distinguishes version conflicts/readiness refusal; response schema formally lists 200/422, descriptive errors broader. No group atomicity/rollback guarantee inferred | S outcome and “Read current state before a new attempt”; R design report/no-replay decisions; tasks 2.2–2.4 | F handler `:19–29,64–99` retains per-item outcomes and continues after error, invalidates attempted details; report `ui/skill-bulk-rollout-report.tsx:6–46` lists ID/message and explicit current-read non-causality. Hook test `:104–131` asserts conflict/warning/success, three calls, targeted invalidation; `:133–198` asserts network/408/503/invalid-response unknown, no automatic POST, prod read blocks retry, whitelist read requires new version/key, failed read preserves uncertainty; `:200–226` asserts synchronous lock/unmount prevents second command | Existing frontend orchestration policy, not backend batch semantics. Evidence supports partial implementation join without executed-test or deployment claims |

Saved linked wiki reuse: `A/sources/wiki-241097511-readable/r1/readable-text.txt:609–623` (§2.9) describes version conflicts and idempotency scoping, explicitly leaves retention undefined. It does not authorize a batch fallback or exactly-once guarantee; no replay added here. Original saved wiki bytes hashed, not fully reread.

## Minimal planning disposition

Recommend member-level **B→P** for MOS-1021 in `A/reports/G2-JIRA-MEMBER-JOINS.md:195`, subject to parent/package review, based on RO1–RO4 exact-member joins—not feature closure. Suggested replacement evidence wording:

> “MOS-1021 exact saved description joined to shown-row selection, whitelist→prod-only eligibility, explicitly approved concurrency-one single status commands, and per-ID partial/unknown outcomes. Main skill-bulk-rollout spec and archived 2026-10-05 owner already govern this MVP; static code and written assertion bodies inspected, not executed. Agreed→whitelist remains outside bulk MVP; no batch contract, backend admissibility or deployment acceptance inferred.”

For the capability row currently transition-only, append this bounded member provenance; do not turn whole-capability coverage green. **No-op on product/spec/task artifacts:** no new corrective owner warranted by inspected evidence; retain historical checkboxes. **Unresolved owner decision only for expanding the deferred agreed→whitelist scope or adopting a future batch contract.** Such expansion needs separate product/contract agreement; this audit does not request or supply it. Existing MOS-1020 review approval is not bulk rollout authorization.

## Actual reads / limits

Read common contract fully; exact J member via JSON extraction; API exact status operation, request/wrapper/status schemas and skills path inventory; relevant accepted-review excerpts above; full current S, full R proposal/design/tasks (not archive delta spec); full rollout hook/validation/handler/report and hook test; complete registry test (only rollout assertions used); registry table 1–100, registry 30–134, entity client 60–94; wiki readable §2.9. Initial broad audit-directory search was capped by `head`; it is discovery only, not exhaustive evidence. One filename glob for entity status client found no match; corrected via targeted symbol search and read actual client.

No tests/build/typecheck/browser/network/credentials/nested agents, production backend, mock-server enforcement, permissions/session policy, or deployment checked. No auth approval reopened or extended. Tab-return persistence, full confirmation UI and entity error-classifier internals were not independently audited; cited written tests do not establish passing. Index/staging state uninspected. Only this configured artifact written.

## Current-local SHA256 inputs

All hashes computed from current working bytes, not git-show baselines:

| Input | SHA256 |
|---|---|
| J | e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208 |
| API | 549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06 |
| A/sources/wiki-241097511/r2/content.json | 710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47 |
| wiki readable-text.txt above | c6dd8857060fa4e87a7170fb604486d12d03a8e74d1ac24c4704554eba67b2df |
| S | 38a5f4996a9d8e1506aa8094ef313383b29d1b113219eff6435028bc6eeaae11 |
| R/proposal.md | 08f9c221ef90f2b32300390b2878ac9b0ff15b3f317fbecc2b55fd89fb1044f9 |
| R/design.md | 5384537a03c86c5ef048b7c5d4176a1ede413dc68439ac4208f93faf820af8b4 |
| R/tasks.md | 451f02b8059a30b3eb742bb9e23dfeb416d20f695340255b85d32b885554fb9c |
| F/handlers/skill-bulk-rollout.handlers.ts | d36c0feba3c0acb47730f0132ef7a6ddc837c022ce822494905c0902cbd84b04 |
| F/model/use-skill-bulk-rollout.ts | 9572d67e82bcc29eb0b019f574cc1fcfb8ba99ad308ecb2d79109b7c92e5c07f |
| F/model/rollout-validation.ts | 623760e554e919e2a5364935ad5990f9cb5dd518924fa9464485811009b383a9 |
| F/model/use-skill-bulk-rollout.test.tsx | 361fc07544273d8f4e0207ef5e06cfbea4f8c347ff820c7724442173c881d0a0 |
| F/ui/skill-bulk-rollout-report.tsx | e9bf845122a8c6b3e04d2917032f376595c8aaea9baf655629d2a276a3d143f9 |
| W/skills-registry.tsx | b6a8eebad1f95a3691f1a9c99a550c897edbcbf90060a4e977e1eca025a64eff |
| W/skills-registry-table.tsx | ccf6d6eefcdcdfd195af8cd52eb2bf4da11578d14c1d32d6bf32bd4e94ba9a4a |
| W/skills-registry.test.tsx | 63977dd1e46c05dc90d83d6593a53fbacceabcacfd942993b6534e5167843270 |
| app/entities/skill/api/skill-details-client.ts | de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6 |

Final: bounded MOS-1021 join supplied; recommend planning-coverage promotion only, no new implementation plan or feature acceptance.
