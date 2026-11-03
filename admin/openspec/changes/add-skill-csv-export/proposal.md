## Why

D-084 explicitly approves frontend list/card CSV export planning after D-083 accepted the bounded MOS-1409 evidence. The mounted skill registry and card have no connected export flow; both backend operations are now published in the T OpenAPI, but saved contracts still need alignment. Frontend delivery uses the server file, not a fabricated local download.

## What Changes

- Add a registry CSV action for the entire accessible selection using current normalized filters and sort, independent of pagination and shown-row bulk rollout selection.
- Add a saved-card CSV action by skill ID, never exporting unsaved form values.
- Download only the server-produced attachment, with accessible pending/error states, no partial download on failure, and safe resource cleanup.
- Preserve MOS-1409 format, validation and backend permission obligations as integration acceptance. By explicit user decision, the historical R15 export-limit requirement is outside current frontend scope and is not an implementation or acceptance gate. Do not invent a client limit; handle any returned backend error without downloading its body.
- Confirmed initial UI scope: omit optional `fields` and use all 19 published server-default scalar columns for both actions. A column selector is separate product scope; this is not a full questionnaire export.
- Preserve existing session/permission ownership, credential-destination checks and credential-free local business mocks. No new auth policy, client CSV serialization or bulk-selection export is in scope. This revision changes planning artifacts only.

## Capabilities

### New Capabilities

- `skill-csv-export`: Contract-gated frontend list and saved-card CSV actions and safe server-file delivery.

### Modified Capabilities

None. `skill-catalog-experience` retains ordinary listing/navigation, `skill-card-editing` retains editing, and `control-center-api-integration` retains shared contract/session rules. Bulk rollout remains separate; none of these owners currently specifies skill CSV export.

## Impact

Future implementation affects skill entity API/public exports, a focused `features/skill-csv-export` slice, registry/card widget composition, shared file/HTTP utilities only where needed, and contract-backed Express handlers/tests. No new dependency is planned. The user explicitly approved implementation from the published contract, without awaiting additional backend clarifications or independent review. Aggregate/split/generated alignment and existing security rules remain required. Unverified backend format/access/CORS properties are reported separately, not inferred from mocks or treated as implementation gates.

Authority and evidence (paths relative to `../reconcile-control-center-backlog/audit/`): [D-083/D-084](../reconcile-control-center-backlog/audit/decisions.md), [REQ R01–R19](../reconcile-control-center-backlog/audit/reports/REQ-MOS-1409.md), [API](../reconcile-control-center-backlog/audit/reports/API-MOS-1409.md), [SPEC](../reconcile-control-center-backlog/audit/reports/SPEC-MOS-1409.md), [SPEC recovery](../reconcile-control-center-backlog/audit/reports/SPEC-MOS-1409.recovery.md), [IMPL](../reconcile-control-center-backlog/audit/reports/IMPL-MOS-1409.md), and [independent review](../reconcile-control-center-backlog/audit/reviews/R-MOS-1409.md). MOS-1409 is a backend dependency/source, not an invented frontend Jira assignment. Saved-contract absence does not establish live backend absence; historical SPEC verification failure remains historical. The user requested implementation using available functionality and confirmed this scope revision; implementation tasks remain open. Historical source reports are retained unchanged. Publication was read at https://nchat-t-tech.mos.ru/api/control/openapi.json; https://task.mos-team.ru/browse/MOS-1409 is Ready for test and contains a developer deployment statement for A/C/T, not runtime acceptance evidence.
