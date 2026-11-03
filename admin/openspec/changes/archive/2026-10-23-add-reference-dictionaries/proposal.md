## Approved checks delta

The user approved restoring the dictionary Checks tab after publication of the backend contract in supplied `crud-api (1).md` §18.7 and live OpenAPI at `https://nchat-a-tech.mos.ru/api/control/openapi.json` (HTTP 200 in this session). This supersedes the earlier no-server-checks decision below only for dictionary diagnostics. Implement GET checks and explicit refetch, analyze and import the checks contract with its transitive schemas, and verify UI/error/session behavior. Checks concern saved data only and never gate Save or activation. System-state UI remains outside this change; its supplied delta is context, not implementation authorization. Journal remains unavailable. Publication is not evidence of authenticated operation execution or D1 completion.

## Why

Control Center has published generic catalogs APIs and a partially implemented Dictionaries section. The latest user-relayed backend decisions explicitly bound the remaining editor and lifecycle work to those APIs, replacing conflicting Wiki requirements rather than treating unsupported features as global prerequisites.

## What Changes

- Deliver the unified registry, published server filters/sorts, saved selections/share links, ordinary and attachment-rule editors, settings, creation, status persistence, physical deletion and three server exports.
- Apply the explicit decision: «физическое удаление справочника - правильное решение; По правам делаем как в апи; делаем без серверных проверок; Активация и пауза - сохраняем статус; Фильтры делаем те, которые доступны в апи; Вложения, делаем как в апи без определений правил».
- Use computed API mutation permissions, not writable allows. Restore published read-only server diagnostics under the approved checks delta; preserve immediate input validation and backend error handling without simulated checks.
- Persist activation/pause status and publication/cache/required settings only; do not promise consumer propagation, invalidation or upload enforcement. Attachment rules follow published CRUD/schema, without defining an evaluator.
- Physically delete only user dictionaries after confirmation; preserve backend errors/reference safeguards and do not fabricate soft-delete or undo behavior.
- Retain approved sequential staged Save with visible confirmed partial outcomes, remaining draft retention, no automatic retry and no fake rollback. Preserve Save/Discard/Stay, full selection URLs, first-page saved-selection Apply, duplicate-name replacement confirmation, and user/list/draft creation with lowercase code without silent transformation and default owner Команда ЦАМ.
- Keep comment-to-journal specifically unavailable/unresolved: the user did not address it and no persistence API exists. No fake editable persisted field; it does not block supported settings, editor, status or deletion work.

**Earlier stage (historical):** planning-only reconciliation of existing artifacts. Earlier bounded implementation evidence remains attributed history, not proof that revised requirements have been implemented. Subsequent implementation is already authorized; no new blanket approval or all-G1–G7 closure precondition is required. Remaining staged-save/dirty interaction details are recorded and tested with the editor work; only genuinely unsupported behavior is withheld. Deployment remains independently unverified.

## Capabilities

### New Capabilities

- `reference-dictionaries`: Isolated Dictionaries registry, staged editor, published filters/exports, stored lifecycle status and confirmed physical deletion, with truthful unsupported-capability boundaries.

### Modified Capabilities

None. Existing HTTP, session, security and optional-module requirements remain unchanged.

## Impact

Domain/UI code remains in `app/optional/reference-dictionaries/`, specialized mocks in `mocks/reference-dictionaries/`, with descriptor-only composition, native routes and portal shared UI/prototype presentation. Existing JSON/binary transport and credential-free Express composition are reused without duplicating consumer lookup storage. No invented endpoint, new auth/permission mapping, database migration, evaluator, dependency or browser/E2E work is authorized. The newly published dictionary checks endpoint and corresponding contract/type updates are authorized.

`evidence.md` retains source hashes, historical Wiki/prototype coverage and explicit revision attribution. `design.md` records exact local wire semantics and narrow residuals; `tasks.md` separates completed historical work from remaining implementation. Other owners' changes, main specs and archives remain untouched. Generated contracts may change only through the existing generation workflow for the approved contract delta. The live docs/OpenAPI were retrieved successfully; no authenticated operation or deployment acceptance is claimed.
