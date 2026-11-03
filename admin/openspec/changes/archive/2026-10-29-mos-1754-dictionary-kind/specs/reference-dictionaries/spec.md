## MODIFIED Requirements

### Requirement: User dictionary creation

Creation SHALL expose required name/code, optional description/owner and a labelled «Тип справочника» selector. The selector SHALL offer «Список значений» (`list`) and «Правила вложений» (`rules-attachments`), with `list` selected by default. This selection represents the value format `kind`, not the system/informational/user `group`. Only user dictionaries SHALL be created, with the selected kind and explicit draft status; the returned dictionary SHALL be opened without demo IDs or timestamps. The UI SHALL allow selection of `rules-attachments` even when another dictionary of that kind exists; backend rejection SHALL remain an error, not simulated success. The kind SHALL NOT be editable after creation in this UI.

Required/format feedback SHALL be immediate; available advisory uniqueness feedback SHALL not be represented as race-safe approval. Server conflicts SHALL preserve input and identify the code conflict. Owner SHALL default to Команда ЦАМ. Code SHALL obey the lowercase wire constraints without silent transformation; no unsupported uppercase request or guessed uniqueness endpoint is allowed. Dismissal with dirty input, including a changed kind, SHALL preserve input on cancellation and require confirmation before discard. The selector SHALL be keyboard accessible and disabled during a pending creation request. Errors and late responses SHALL retain existing session ownership and cancellation safeguards.

The created card SHALL display its returned server data and use the editor for the returned kind; it SHALL NOT fabricate the selected kind if the subsequent read fails or returns a different kind. Creating either kind SHALL NOT automatically attach it to other resource fields or claim that attachment rules are enforced on uploads.

#### Scenario: Default list creation

- **WHEN** the user opens the form and creates a dictionary without changing its kind
- **THEN** the selector displays «Список значений» and the request carries `group: user`, `kind: list` and `status: draft`

#### Scenario: Create additional attachment rules

- **WHEN** another rules dictionary already exists and the user selects «Правила вложений» and submits valid data
- **THEN** the request carries `group: user`, `kind: rules-attachments` and `status: draft`, and a confirmed creation opens the returned ID for the server-backed card

#### Scenario: Returned card is authoritative

- **WHEN** creation returns an ID but the subsequent card read fails or reports a kind different from the selection
- **THEN** the UI preserves the read error or displays the returned kind instead of fabricating a matching card, and does not repeat the creation request automatically

#### Scenario: Concurrent duplicate code

- **WHEN** advisory feedback found no collision but creation returns a uniqueness conflict
- **THEN** creation is not reported successful and the dialog retains the user's values, selected kind and server error

#### Scenario: Reject an unsupported kind

- **WHEN** an unsupported kind is submitted
- **THEN** no creation request is sent and the form does not report success

#### Scenario: Backend rejects a supported kind

- **WHEN** the backend rejects a selected supported kind
- **THEN** the error is shown and the selection and other input are retained without a false success

#### Scenario: Dismiss a changed kind

- **WHEN** the user changes the kind and tries to close the form, then cancels the discard confirmation
- **THEN** the form and the chosen kind remain available without creating a dictionary

#### Scenario: Pending creation

- **WHEN** creation is pending
- **THEN** the kind cannot be changed and a duplicate submission is not sent

#### Scenario: Stale creation response

- **WHEN** a creation response arrives after dismissal or session replacement
- **THEN** it cannot navigate or update the new context
