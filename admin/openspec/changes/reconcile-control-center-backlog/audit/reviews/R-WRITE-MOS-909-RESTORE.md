# R-WRITE-MOS-909-RESTORE — independent planning review

## Review

**Disposition: ACCEPT — planning artifacts only.**

- **Correct:** The proposal, design and six unchecked tasks implement D-020’s explicitly selected planning scope: preserve draft → checking, sandbox → review and whitelist → prod; remove four additional generic actions.
- **Correct:** The proposed two-file implementation boundary is sufficient based on the actual action-selection, rendering and confirmation chain.
- **Correct:** The existing-requirement delta preserves safety scenarios and separates generic lifecycle policy from review, toggle and shared API ownership.
- **Fixed:** None; read-only review.
- **Required corrections:** None.
- **Merge verdict: OK with notes** for planning publication, not implementation acceptance.

No issues found.

## Evidence and assessment

Repository-relative aliases:

- **C** = `openspec/changes/mos-909-restore-approved-lifecycle-actions`
- **A** = `openspec/changes/reconcile-control-center-backlog/audit`
- **F** = `app/features/skill-lifecycle`
- **W** = `app/widgets/skill-details/ui`
- **E** = `app/entities/skill`

### Authority and scope

Read all five C artifacts, including `.openspec.yaml`, the complete writer report, D-018–D-020, corrected IMPL-MOS-909 and its independent review.

`A/decisions.md:3–15` distinguishes the explicit three-command planning authorization from the earlier scope escalation. C’s proposal Impact, design Non-Goals and tasks preserve that distinction. They do not authorize application edits during planning, checks UI, DTO regeneration, unrelated copy repair, main-spec synchronization, archive changes or task closure.

The historical R-IMPL-MOS-909 verdict remains REVISE; D-019 accepts its specifically corrected evidence rather than retroactively declaring that review unconditional acceptance. C correctly avoids a missing-readiness-reread remediation: `E/model/skill-status-error.ts:5–10` classifies 409 as conflict and `F/handlers/skill-lifecycle-handlers.ts:42` attempts GET recovery.

### Two-file correction is supported by current code

`F/constants/skill-lifecycle.constants.ts:9–17` contains all seven connected actions. The four proposed removals are precisely checking → training, training → autotest, autotest → sandbox and review → whitelist.

The map’s only consumer found under `app` is `F/model/use-skill-lifecycle.ts:28`. The UI conditionally renders its trigger at `F/ui/skill-lifecycle.tsx:62–84`; opening confirmation requires an action at `F/handlers/skill-lifecycle-handlers.ts:10–16`. Removing entries therefore removes both triggers and new confirmations without a second allowlist or handler rewrite.

Existing snapshot equality checks cover ID, version and status (`F/model/use-skill-lifecycle.ts:29–35`). Existing confirmation submission retains its synchronous pending lock and snapshot payload (`F/handlers/skill-lifecycle-handlers.ts:19–30`). These support the proposed status-only stale-confirmation regression without requiring broader implementation changes.

### Meaningful regressions, not merely deleted expectations

Read the complete `W/skill-lifecycle.test.tsx:1–309`.

Design Decision 3 and tasks 2.1–2.3 correctly replace the seven-action expectations at `:48–136` with:

- Three explicit allowed commands, independent of the production action map.
- Explicit absence of all four removed labels across all nine recognized states.
- Six no-generic-command states, with GET-only observation and no newly opened lifecycle confirmation.
- A server-refresh transition from an actionable state to a no-command state.
- An open confirmation invalidated by a **status-only change to review with unchanged version**, including no POST and no review transition after closure.

The status-only case adds meaningful coverage beyond the existing version-change test at `:205–226`. The refresh case tests removal of a previously rendered trigger, not merely initial-state absence.

The plan expressly retains the existing assertions for exact transport/version/key, duplicate-click suppression, prod warning and actual cache data (`:87–136`), older-read cancellation (`:138–170`), uncertain outcome/new key (`:172–203`), cancellation/focus and stale version (`:205–226`), recovery and 409/422 behavior (`:228–294`), and mismatched server status (`:296–307`). These assertions were inspected, not executed.

### Safety and separate owners remain intact

Design Decisions 2 and 4 correctly leave broader entity validation and mutation behavior unchanged:

- `E/api/skill-details-client.ts:68–86` validates the published enum, version, key and returned identity.
- `E/model/use-change-skill-status-mutation.ts:9–21` preserves no retry, older-read cancellation, session-ownership checking, actual DTO commit and registry invalidation.
- `app/features/skill-review/model/use-skill-review.ts:16–40` uses the shared mutation with its own checklist and confirmation guards. The archived review design’s “Переиспользовать статусную команду” decision expressly prohibits expanding generic lifecycle.
- `W/skill-details.tsx:38–54` composes toggle and lifecycle separately. Toggle visibility remains prod/disabled-only, with dedicated command paths in `E/api/skill-global-toggle-client.ts:13–36`.
- `E/model/use-skill-details-query.ts:7–20` owns processing-state polling independently of the generic action map.

Permission wrappers, neutral eight-stage rendering and recognized disabled behavior remain outside the proposed edits. No independent auth/session or full neighboring-feature certification is claimed.

### Complete existing-requirement delta

Compared C’s entire `specs/skill-lifecycle/spec.md` with the complete main lifecycle specification and read the separate review/toggle specifications.

The delta modifies only **Contract-gated lifecycle**. It preserves all three original scenarios—Current skill API, Unknown server state and Background refresh fails—and retains the original safeguards against synthetic results/endpoints, questionnaire mutation misuse and unknown-status fallback.

Added scenarios clarify the approved three commands, six no-command states and separate owners. They do not narrow shared transport or introduce a duplicate capability. **Safe single-skill transitions** remains unchanged. Known obsolete disabled/eight-status and results wording elsewhere is explicitly deferred, not silently repaired or treated as authority to reject disabled.

## Checks and provenance

- **Strict OpenSpec validation: passed**, attributed to the writer report and parent’s reported independent validation, **1/1 with no issues**. This reviewer did not execute validation.
- **Repository `yarn format:check`: failed.** Independently read `/tmp/mos909-planning-format-check.log`: 149 audit-file warnings, including `A/reports/WRITE-MOS-909-RESTORE.md` and evidence/derived JSON. No C artifact appears in the warnings. This is **not a fully green repository check**; baseline separation for all 149 files is unestablished.
- Artifact/source digest recomputation is attributed to writer and parent, not independently performed here.
- Read-only working-tree inspection reported no changes against reviewer-launch HEAD; it does not inventory ignored planning artifacts or attest committed ranges.
- No edits, tests, builds, browser/network activity or implementation execution occurred. Future typecheck, lint, test and formatting checks remain unchecked implementation obligations.

## Publication boundary

Accept the planning package without mandatory corrections. Formatting failure remains explicitly recorded; hashed evidence was not rewritten.

This acceptance does **not** authorize implementation, close any of the six tasks, establish backend admissibility/runtime propagation, or approve main-spec synchronization/archive. A later explicit implementation request remains required.