## Purpose

Provide truthful skill registry and saved-card CSV exports using agreed server-produced files, preserving selection semantics, access boundaries and safe download behavior.

## ADDED Requirements

### Requirement: Contract-gated skill export actions

The frontend SHALL provide registry and saved-card CSV actions only through published and agreed skill export operations. Unpublished or unagreed operations MUST NOT be called, replaced by endpoint aliases, ordinary list pagination, client CSV generation or synthetic success. If shown before integration is available, an action SHALL be disabled with an accessible explanation. Existing session, permission and credential-destination rules SHALL remain unchanged; UI visibility SHALL reuse the existing skill-view permission and backend authorization SHALL remain authoritative.

Source: [D-084 and accepted evidence](../../proposal.md), REQ R01–R03/R11/R19; existing `control-center-api-integration` obligations. The user has approved the published export contract. Unspecified backend details in [design](../../design.md) SHALL remain separately reported acceptance unknowns, not implementation blockers or invented frontend guarantees.

#### Scenario: Missing publication

- **WHEN** either export operation lacks an agreed published request, file, error or security contract
- **THEN** that action sends no export request and produces no local file or success; any visible unavailable action has an explanation available without hover

#### Scenario: Existing access boundary

- **WHEN** an export is attempted with the existing permitted session context and backend denies access
- **THEN** the frontend shows no file or success, preserves existing session/error handling without automatic replay, and does not substitute local data or broaden permissions

### Requirement: Whole-selection registry export

Registry export SHALL use the normalized applied search, filters and sort at activation, matching agreed list selection semantics, and export the entire accessible selection independently of page and shown-row bulk selection. Requests MUST NOT contain pagination or selected-row IDs. Backend integration acceptance SHALL preserve deleted-skill exclusion, team restrictions and one CSV row per skill. Confirmed empty results SHALL remain exportable as headers only; loading/error/placeholder data MUST NOT be represented as a confirmed selection.

Source: REQ R04/R08/R09/R16/R17 and D-084; existing catalog and bulk-rollout ownership remain unchanged.

#### Scenario: Filtered second page with checked rows

- **WHEN** a user activates CSV export on a filtered and sorted later page with some visible rows checked for rollout
- **THEN** the export uses current agreed search/filter/sort without pagination or checked IDs and the server file represents the whole accessible selection, not just that page

#### Scenario: Empty accessible selection

- **WHEN** a confirmed selection contains no matching accessible skills
- **THEN** export can return the server-produced header-only CSV without inventing a row or reporting failure merely because the selection is empty

#### Scenario: Selection changes during export

- **WHEN** the user changes filters after activating export
- **THEN** the in-flight request retains its activation-time selection and a subsequent explicit export uses the new normalized selection

### Requirement: Saved-card export and default columns

Card export SHALL identify the saved skill and export server-saved values without submitting, saving or clearing unsaved edits. Its scope SHALL be clear to the user. Initial list/card actions SHALL omit optional `fields` and use all 19 published server-default scalar columns, not a full questionnaire export; a fields-selector UI is outside this initial scope. Backend integration acceptance SHALL retain JSON `{}` defaults, optional nonempty allowed fields, equal columns for equal fields across list/card, and validation errors for empty/unknown fields. Default columns MUST NOT be inferred from displayed table or questionnaire fields.

Source: REQ R03/R05–R07/R10/R16/R18; D-084. Defaults-only UI is confirmed by the user, not a claim of complete UI exposure of backend options.

#### Scenario: Unsaved questionnaire

- **WHEN** the saved skill is exported while unsaved questionnaire values exist
- **THEN** the request identifies only the saved skill with default export settings, the server file has a header and one saved-data row, and the draft is not submitted, overwritten or discarded

#### Scenario: Default and optional columns

- **WHEN** initial list/card actions request default exports
- **THEN** neither sends a fabricated fields list and both use agreed server defaults; integration acceptance separately verifies equal explicitly selected columns and rejection of empty/unknown fields

#### Scenario: Missing or inaccessible saved skill

- **WHEN** the card export is rejected because the skill is missing or inaccessible
- **THEN** the agreed existing skills API error behavior is presented without a file, unsaved-data fallback or fabricated error status

### Requirement: Server CSV integrity and atomic failure

Downloads SHALL preserve the complete server-produced file bytes without client reserialization. Integration acceptance SHALL require UTF-8 BOM, semicolon delimiter, header row, CSV-injection protection, attachment disposition, and a filename containing generation date and additionally skill ID for card export. Export-limit definition and limit-specific acceptance are outside current scope by explicit user decision; their absence MUST NOT block frontend implementation or acceptance. The frontend MUST NOT invent a numeric cap or a limit-specific error contract. Any returned backend error SHALL use existing error handling without downloading the error body. Exact columns, media/header conventions, filename formatting and error wire values SHALL come from publication/agreement, not frontend invention.

Source: REQ R12–R14/R16–R17/R19; historical R15 is retained in source evidence but excluded from current scope by the user-confirmed proposal revision.

#### Scenario: Valid server attachment

- **WHEN** an agreed successful response delivers a complete valid CSV attachment
- **THEN** the frontend initiates download of those bytes using its safely handled server filename; backend acceptance verifies the required format, row shape and injection safety independently of frontend download tests

#### Scenario: Backend or file-response failure

- **WHEN** the response is a backend error, transfer fails, or file metadata is malformed
- **THEN** no partial file or error body is downloaded, no success is claimed and an accessible error allows an explicit retry where permitted

#### Scenario: No published export limit

- **WHEN** the agreed export operations are available but no numeric export limit or limit-specific error is published
- **THEN** the frontend permits export without a fabricated cap or limit prerequisite, while preserving pending, cancellation, cleanup and generic error handling

### Requirement: Accessible and context-safe download lifecycle

Actions SHALL have accessible names and keyboard operation, expose pending/error state without hover, prevent duplicate activation while pending and offer explicit retry without erasing the user's selection or draft. Download initiation MUST NOT be described as proof that a file was saved to disk. Temporary download resources SHALL be released after use and on failure or abandonment. Navigation/unmount and session-context invalidation SHALL neutralize late responses so a stale file cannot download into a replacement context. Existing session recovery MUST NOT automatically replay export.

Source: D-084 frontend scope and user-confirmed revision; existing API integration/session isolation and accessibility constraints; IMPL helper limits. Generic failure safety remains required independently of export-limit policy.

#### Scenario: Pending and retry

- **WHEN** a keyboard user activates export twice while the request is pending and then receives a recoverable failure
- **THEN** only one request is submitted, pending and error are accessible, focus remains usable, and explicit retry preserves selection/draft without claiming success

#### Scenario: Stale response or failed download trigger

- **WHEN** the view unmounts or session context changes before response completion, or triggering a valid download throws
- **THEN** stale completion cannot initiate a download, temporary links and file URLs are released and no sensitive file result remains reusable by the new context

### Requirement: Separate frontend and backend acceptance

Acceptance SHALL include focused unit/component checks for selection mapping, saved-card behavior, defaults, pending/errors, access integration, stale-result suppression, resource cleanup and keyboard/status accessibility. Contract-backed local business mocks SHALL remain credential-free without role enforcement and excluded from production. Mock checks MUST NOT be presented as proof of backend authorization, CSV safety or deployed integration. E2E/browser tests MUST NOT be created, edited or run without separate explicit authorization.

Source: D-084 planning boundary, REQ R09/R11–R19 and existing API integration verification rules.

#### Scenario: Local checks pass

- **WHEN** unit/component and agreed mock HTTP checks pass
- **THEN** their scope is reported separately from backend format/injection/access evidence and real deployment verification; unresolved integration prerequisites remain open
