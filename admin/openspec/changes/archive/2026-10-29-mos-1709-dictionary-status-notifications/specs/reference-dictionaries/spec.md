## ADDED Requirements

### Requirement: Action-specific dictionary status success notifications

The dictionary card SHALL show one nonblocking success toast for each explicitly requested and server-confirmed lifecycle transition: «Справочник активирован» for draft to active, «Справочник приостановлен» for active to paused, and «Работа справочника возобновлена» for paused to active. The message SHALL distinguish activation from resumption using the status before the operation. A matching dictionary identifier and requested status SHALL be confirmed before announcing success. Feedback SHALL describe stored status only, not propagation to external consumers.

Status actions MUST NOT introduce a pre-request confirmation dialog or a modal success result. Existing dirty Save/Discard/Stay handling, deletion confirmation, mutation restrictions and unknown-outcome safeguards SHALL remain unchanged. Success feedback SHALL follow the existing operation-feedback accessibility and lifecycle rules: no focus stealing, no duplicate inline success, keyboard dismissal, and no replay on rerender, refetch or reopening the card.

#### Scenario: Activate a draft dictionary

- **WHEN** activation of a clean draft informational or user dictionary is requested and the server confirms its identifier and active status
- **THEN** «Справочник активирован» appears once as a toast, the returned status is displayed, and no confirmation dialog or modal result is added

#### Scenario: Pause and resume

- **WHEN** a confirmed active dictionary is successfully paused and subsequently explicitly resumed with matching responses
- **THEN** pause shows «Справочник приостановлен» and resume shows «Работа справочника возобновлена», each once for its operation and without downstream-effect claims

#### Scenario: Pending or unsuccessful transition

- **WHEN** a status request is pending, rejected, has an unknown outcome, or returns a mismatched identifier or status
- **THEN** no success toast for that transition appears, and existing pending, error and reconciliation behavior remains available without automatic mutation replay

#### Scenario: Dirty edits precede the transition

- **WHEN** a status action is requested with unsaved edits
- **THEN** Save/Discard/Stay remains available, Stay or failed/unconfirmed Save sends no status mutation and produces no status-success toast, and successful continuation announces the transition only after its own confirmed result

#### Scenario: Stale completion or refreshed card

- **WHEN** a completion belongs to a replaced session or another card, or the current card is rerendered, refetched or reopened after success
- **THEN** no stale or replayed status-success notification is shown

#### Scenario: Accessible notification

- **WHEN** a keyboard user completes a supported status action and focuses the toast dismissal control
- **THEN** the success is politely announced without stealing focus, remains available during interaction, and can be dismissed using the keyboard without closing the card
