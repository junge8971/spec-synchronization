# AB-EDITOR — bounded implementation audit

## Result and authority

HEAD verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches assignment). Current local inputs hashed below; no historical equality asserted for Git-ignored OpenSpec.

Read complete main editor/module specs, accepted documentary report/review, and owning archive `2026-10-15-add-optional-ab-testing` proposal/design/tasks and editor/module delta specs. Reused accepted ABROOT-03/04/05/06 evidence; did not re-extract wiki or attachments. Existing editor tasks 2.1–2.4, 3.3, 5.1–5.8 already own the scenario. No new lifecycle policy or implementation work is justified by this bounded inspection. One existing documentary clarification candidate survives: minimum sample size is **per group**, whereas mounted label is generic. Do not silently rewrite archived decisions or change checked tasks.

## Scenario → implementation → transport/mock → written tests → owner

Paths below are relative to repository; A=`app/optional/ab-testing/`. Function names are exact locators. Tests are written evidence, **not executed**.

- **New/detail and four tabs:** `A/routes/{creation,details}.tsx` mount `AbTestingEditor`; `A/ui/ab-testing-editor.tsx:AbTestingEditor` distinguishes `/new`, rejects invalid UUID, keys loader by session owner/ID. `A/ui/editor/editor-loader.tsx:EditorLoader` loads lookup/detail independently and shows retry instead of fixtures. `A/model/use-ab-testing-editor.ts:useAbTestingEditor` owns one RHF draft, snapshot and URL tab fallback; `A/ui/editor/editor-form.tsx:EditorForm` wires four tabs and pending fieldset. `A/model/ab-testing-form.ts:createAbTestingDefaults` uses active lookup defaults, two 50/50 groups, null sample and empty surfaces, never first-option fallback. Written component cases `A/ui/editor/editor.test.tsx:308,338,389,400,948` cover defaults/nulls/references/fallback (test inventory; not all bodies reviewed). Owner: editor “Complete editor and initial values”, module “Shell routes and access”; archive tasks 1.3, 5.1.

- **Validation/conflict:** `A/api/ab-testing-schema.ts:abTestingGroupsSchema,abTestingSurfaceIdsSchema,validateAbTestingRules` implement 2–100 groups, integer 0–100 and total 100, unique IDs/tags, 1–100 UUID surfaces, string/int32 bounds, scheduled date, ordered dates and segment. `A/handlers/editor-save.ts:validateEditor/createEditorSaveHandler` validates before send and maps errors without accepting snapshot. `mocks/ab-testing/validation.mjs:validateExperiment/validateReferences/validateGroups/validateRules` checks generated schema, server-side name/code uniqueness, catalog/surface existence and aggregate rules before mutation. Written `A/model/ab-testing-form.test.ts:94,117,152` and `A/model/ab-testing-errors.test.ts:13,26,45` inventory these boundaries; directly read component assertions at `editor.test.tsx:615–650,770–799` preserve draft, focus nested error and deny false success. Directly read mock `aggregate.test.mjs:120–181` asserts state/timestamps unchanged across invalid aggregates/conflicts. Owner: editor “Aggregate validation”; tasks 2.4, 3.3, 5.5–5.6. No separate validation backlog needed.

- **Create/update identity and recovery:** `A/model/ab-testing-form.ts:buildAbTestingPatch` sends changed scalars and whole changed arrays, preserving server group IDs and nullable clearing; `A/handlers/editor-save.ts:persistEditor` skips empty diff. `A/api/ab-testing-client.ts:createAbTestingExperiment/getAbTestingExperiment/updateAbTestingExperiment` uses shared `apiRequest`, POST expecting 201 ID, GET and partial PUT expecting validated aggregate, under existing A/B API path. `A/model/ab-testing-mutations.ts` disables retry, guards owner and duplicate submission, retains confirmed create ID and reads it instead of POST replay; update validates response identity before cache replacement. `mocks/ab-testing/handlers.mjs:save` validates candidate before state mutation. Directly read `mocks/ab-testing/aggregate.test.mjs:61–103` checks reorder/rename IDs, whole surface replacement, GET equality and null clearing. Component `editor.test.tsx:651–669` explicitly asserts replace-navigation to confirmed ID and one POST after GET failure. Additional written mutation cases `ab-testing-mutations.test.ts:49,66,86,97,111`. Owner: “Aggregate persistence and identity”; tasks 2.2–2.3, 3.3, 5.6. Local mocks are not real persistence/deployment proof.

- **Saved-status tag restriction / status commands:** `A/model/ab-testing-form.ts:isAbTestingGroupTagReadonly` uses saved non-draft snapshot and existing ID, not watched draft status. Mock `validation.mjs:validateGroups` rejects changed existing tags against saved status; `aggregate.test.mjs:183–230` asserts active→draft plus changed tag fails atomically, reorder remains possible, separate saved draft then tag change succeeds. `A/ui/editor/editor-status.tsx:EditorStatus` blocks new/dirty/pending/unknown status; paused targets active, others target paused; completion requires confirmation and is disabled when already completed. `editor-save.ts:commandBlocked/persistEditor` independently guards commands and emits only `{status}` without dates. Directly read `editor.test.tsx:673–710` asserts cancel no-op, exact status-only patches, completed blocker and rejected completion retaining dates/status/no success. Saved-tag/keyboard case inventoried at :418. Owner: “Existing group tags follow saved status”, “Persisted status commands”; tasks 5.2, 5.7; accepted ABROOT-04. No inference of historical launch lock, terminal completed state, traffic control or new lifecycle transition API.

- **Draft/session safety:** `use-ab-testing-editor.ts:useAbTestingEditor` uses Router blocker for dirty pathname changes, beforeunload, independent snapshot and confirmed-ID redirect; `ab-testing-mutations.ts` checks shared session owner before/after responses. `EditorForm` exposes explicit server reconciliation and discard; refetch does not reset form automatically. Directly read component `editor.test.tsx:632–650,711–769` asserts duplicate-send prevention, uncertain result preservation, leave/stay, tabs, unload, refetch and owner replacement. Test at :736 models same-owner refresh using query invalidation, not a real auth refresh exchange. Owner: “Draft and session safety”; tasks 2.2, 5.8. Existing entity-session/shared-transport imports retained; backend authorization not replaced by UI guards.

- **Preview/reference seams (limited):** mounted `EditorForm` connects `EditorGroups`, `EditorSurfaces`, `EditorRules`; written component inventory at `editor.test.tsx:418,443,467,496,525,549` covers keyboard/DnD identity, incomplete preview, 0%, label threshold, limits, cross-tab rules and paginated references. Their full implementations/test bodies were not reviewed in this bounded pass: no exhaustive conformance finding. Existing tasks 5.2–5.5 already cover them; do not create duplicate work from inspection limits.

## Necessary correction / no-op

**ABROOT-05 wording only:** accepted report ABROOT-05 cites source S227 as minimum sample **per group**. Main editor spec “Complete editor and initial values” and “Aggregate validation” specify the scalar/bounds but omit that qualifier; `A/ui/editor/editor-main.tsx:44` renders `Минимальная выборка` without a per-group hint. Preserve this existing clarification candidate with editor owner/task 5.1, rather than manufacturing a calculator, statistics task, new DTO or execution requirement. It is a semantic wording clarification, not evidence numeric behavior is wrong. Any active planning delta should be limited to this qualifier if the parent accepts it; archived task completion remains unchanged.

Otherwise **planning no-op for inspected create/edit/status/validation scenarios**: implementation and written tests map to existing owners. This does not attest whole-editor completeness. Module execution boundary is visible beside sample/dates/auto-stop (`editor-main.tsx`), and status confirmation explicitly disclaims traffic effects (`editor-status.tsx`).

## Local input SHA256

- Main `openspec/specs/ab-testing-editor/spec.md`: `7cffebc09d33477bc300ec9c76f2989c9e095846e2a90fc74747b3393c2d13e9`
- Main `openspec/specs/ab-testing-module/spec.md`: `0013ea05d4c913d321baae18dca1076029792bf58ffc06e6a1715d53eca60366`
- Audit `reports/DELTA-AB-TESTING-ROOT-DOC.md`: `cd8cb41cc08c0f2400a03dc842f089eec3f1c393e8db8070ffc11f65f91fea69`
- Audit `reviews/R-DELTA-AB-TESTING-ROOT-DOC.md`: `3db6568ae32989577ee8271a092d41c44abf9fd2c1bb6e3f705c10ceb2b9ce82`
- Audit `work-items/G2-OPTIONAL-DOMAINS-SEVEN.md`: `9720c147622d55b007071126202799405226f607c8935d431761f980c476e89a`
- Archive `proposal.md`: `93d219f6c749cda697f3b1dcc231e3d4dbf2ea71b99267f7d610b19ba390edfd`
- Archive `design.md`: `fba208c2d27c670ff0e981d5fa17d2121df16ff67ca66d8df0adf255fff2cee6`
- Archive `tasks.md`: `e005921905e56e00cead68fd3c58d7ae30b9ffb79d6313de3162734ec30f1073`
- Archive `specs/ab-testing-editor/spec.md`: `d6609115890ed3f2db3b2b9889dce58fd6274a323579c7bd40aa328569d76891`
- Archive `specs/ab-testing-module/spec.md`: `f2f83ebaa1bc01e27fd5cf7aa988e18c57cabb01ff114a41602322afc71eed37`

Audit prefix: `openspec/changes/reconcile-control-center-backlog/audit/`; archive prefix: `openspec/changes/archive/2026-10-15-add-optional-ab-testing/`.

## Limits

Read-only project work; only configured external report written. No network, browser, credentials, tests/build/typegen or nested agents. Registry/export implementation not audited; a broad test-name search returned adjacent test names, which were not analyzed. No fresh saved OpenAPI/CRUD-document census or real API call; transport/mock descriptions are code evidence, not deployed contract verification. No global FSD/removability or production-graph verification, nor new authorization model. Accepted attachment/source limits persist. Global/feature checkboxes unchanged.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Mapped editor creation, validation, persistence, status and draft scenarios to mounted code, mock handlers, written tests and existing spec/tasks; retained only existing per-group wording candidate."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/50982ca9-1cc4-42f9-b49b-912e0b738c81/impl-ab-editor.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"git rev-parse HEAD","result":"passed","summary":"Matches assigned HEAD."},{"command":"SHA256 current local spec/report/archive/work-item inputs","result":"passed","summary":"Recorded ten input hashes; no git-show of ignored artifacts."},{"command":"git diff --cached --name-only","result":"passed","summary":"No staged paths."},{"command":"tests/build/typecheck","result":"not-run","summary":"Prohibited by audit contract."}],
  "validationOutput": ["Static code and selected test assertions inspected; no runtime conformance claim."],
  "residualRisks": ["Tests unexecuted; real API/deployment unverified.","Reference/preview implementation only mapped at mounted seams and written-test inventory, not exhaustively reviewed.","Per-group sample wording remains an existing documentary clarification candidate, not an approved new behavior."],
  "noStagedFiles": true,
  "diffSummary": "External report only; no project edits.",
  "reviewFindings": ["No new lifecycle or duplicate implementation task justified by inspected paths.","editor-main.tsx:44 omits per-group qualifier identified by accepted ABROOT-05."],
  "manualNotes": "Complete owning specs and relevant archived planning artifacts read; accepted source extraction reused. No completion/deployment inference or task-checkbox changes."
}
```
