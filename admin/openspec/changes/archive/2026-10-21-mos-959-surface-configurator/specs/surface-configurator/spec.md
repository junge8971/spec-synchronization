## Purpose

Provide a surface appearance and content editor with safe local previews, explicit contract-backed persistence and truthful recovery without activating sandbox or changing session permissions.

## ADDED Requirements

### Requirement: Saved configuration editor

The surface card SHALL open Configurator by default and initialize its editor from the saved detail configuration, not prototype or creation defaults. It SHALL offer appearance controls, greeting and fallback fields, quick suggestions and greeting cards. Existing Surface view/update presentation policy, session ownership and archived read-only restrictions SHALL remain in force. Tab switching and background reads SHALL preserve unsaved input for the same surface; another surface or owner MUST NOT inherit it. Dirty state SHALL reflect changes to editable saved values, including ordered list contents, not updated_at or list counts alone. Reverting all changes SHALL restore clean state.

#### Scenario: Existing saved configuration

- **WHEN** a surface with nondefault configuration is opened
- **THEN** Configurator is selected, saved fields and card accent values are retained, and no write occurs

#### Scenario: Dirty draft survives tab switching

- **WHEN** a user changes one suggestion and switches tabs while detail refreshes
- **THEN** unsaved input remains, saved overview facts remain server-derived, and publication is blocked even if the list length is unchanged

#### Scenario: Read-only or different context

- **WHEN** the surface is archived, editing is not permitted by existing presentation policy, or the surface/session owner changes
- **THEN** no unauthorized editor action is exposed, archived writes are blocked, and the previous context's draft is not applied to the new context

### Requirement: Contract-backed appearance and content controls

The editor SHALL offer presets #B3121B, #0B6B3A, #1E4FA3, #7A3E9D, #B5651D plus arbitrary manual `#RRGGBB` values matching `^#[0-9a-fA-F]{6}$`. It SHALL offer shapes round/moderate/strict and fonts moscow_sans/system/golos_text with dictionary labels. It SHALL provide insertion controls for `{имя}`, `{отчество}`, `{время суток}` and a separate fallback field with conditional validation guidance.

Suggestions SHALL have add/delete controls, the hint «Например: Когда отключат воду», empty text «Саджестов нет» and disabled Add at five. Cards SHALL have add/delete controls, title/subtitle fields with «Заголовок»/«Подзаголовок» hints, action type/value controls and disabled Add at four. Empty cards SHALL show «Карточек нет: пользователь увидит только приветствие и саджесты». Actions SHALL be message/skill/link with hints «Текст сообщения»/«Навык»/«Адрес страницы». Hints MUST NOT become saved content. Controls, errors and limits SHALL have accessible names and keyboard operation.

#### Scenario: Custom color and invalid format

- **WHEN** a user enters a valid nonpreset #RRGGBB color or an invalid bare/short HEX value
- **THEN** the valid custom color is accepted while the invalid format shows a field error without silently restricting to presets or converting the input

#### Scenario: Collection boundaries

- **WHEN** the fifth suggestion or fourth card is added, then one item is deleted
- **THEN** the corresponding add control becomes disabled at the cap and available after deletion; empty lists are permitted and placeholders are never serialized as values

### Requirement: Published configuration validation and payload

Explicit configuration save SHALL send the complete seven-field published configuration DTO to PUT `/api/control/api/surfaces/v1/surfaces/{surface_id}/configuration`. It MUST NOT contain enabled_skills, invented card IDs, null fallback or Wiki-only shape/font aliases. Existing card accent SHALL be retained; new cards use the published false default without inventing an accent-control requirement.

Greeting SHALL be nonempty, at most 500 characters, with only the three published tokens and no unpaired braces. Fallback SHALL be a string of at most 500 characters, nonempty when greeting contains name or patronymic, and allow only the time token. Suggestions SHALL contain at most five nonempty strings of at most 100 characters without duplicates; cards at most four, with nonempty title up to 100 and subtitle up to 200. Message actions SHALL be nonempty up to 500 characters; skill actions SHALL use UUID, with connected/nondeleted validity enforced by the server at save; link actions SHALL be absolute HTTPS up to 2000 characters, allowing query but not credentials/fragments. Empty collections SHALL be valid. Whitespace-only required text MUST NOT be treated as valid content. The UI SHALL retain input on rejection and associate reliable server field paths with controls; unrecognized errors SHALL remain visible without parsing message text into invented rules.

Published trimming and canonical skill UUID readback SHALL be respected. The UI MUST NOT invent token aliases, silently deduplicate suggestions, auto-remove stale cards or alter connected skills to make configuration save pass.

#### Scenario: Conditional fallback

- **WHEN** greeting uses `{отчество}` and fallback is empty, or fallback contains `{имя}`
- **THEN** saving is blocked with the relevant field error; a greeting without name/patronymic permits an empty fallback string, never null

#### Scenario: Action boundaries

- **WHEN** a card contains a non-UUID skill, a credential-bearing HTTPS URL, or an overlong message
- **THEN** the relevant action value is invalid and no successful-save feedback is shown

#### Scenario: Stale connected skill

- **WHEN** a previously saved card references a skill disconnected since editing and the server rejects configuration save
- **THEN** the card and entered values remain visible for explicit correction; no card deletion, skill reconnect or combined payload occurs

### Requirement: Inert demonstration previews

Greeting and Dialog previews SHALL update locally from unsaved editor values and selected appearance. Greeting SHALL show substituted greeting, suggestions and cards; Dialog SHALL show message bubbles with an assistant greeting first and suggestions after it. A separate fallback preview SHALL display fallback content with its supported substitution. Substitutions SHALL use explicitly demonstrated sample data, not resident/session identity or inferred real time. Preview MUST NOT issue requests, execute widget code, send messages, run skills or navigate card links. User content SHALL render as text, never executable HTML. Preview MUST NOT imply saved configuration, sandbox success or real widget parity.

#### Scenario: Unsaved preview

- **WHEN** greeting or appearance changes without saving
- **THEN** both local preview tabs reflect the change and explicit sample substitutions without any mutation or preview request

#### Scenario: Fallback and action safety

- **WHEN** fallback preview is selected or a displayed card action is activated
- **THEN** fallback is shown separately with demonstration data, and no network request, link navigation, message or skill execution occurs

### Requirement: Explicit save and readback recovery

The configurator SHALL provide an explicit configuration save action for dirty input and MUST NOT autosave on tab change, preview, publication or skill saving. Saving SHALL lock competing card writes and submitted editing, use existing mutation/session guards, and start a fresh detail GET after a successful PUT. An earlier in-flight GET MUST NOT confirm the write. Only fresh readback SHALL establish the normalized saved configuration baseline; status, timestamp, token and connection values remain server-owned. Saving MUST NOT fabricate draft-to-configured transitions or re-embedding requirements.

A confirmed write followed by failed readback SHALL be shown as saved with unconfirmed refreshed data, not a failed write. Last-known facts and entered values SHALL remain available; publication SHALL remain blocked until successful readback. Recovery SHALL retry GET only and MUST NOT repeat the successful PUT or implicitly publish. Failed writes SHALL preserve drafts and distinguish validation, conflict, permission and transport failures; 409 SHALL use existing manual-refresh behavior, and no automatic mutation replay is allowed. Successful configuration readback MUST NOT discard a separately dirty skills draft.

#### Scenario: Explicit configuration save

- **WHEN** a user saves valid dirty configuration
- **THEN** one complete configuration PUT is sent without skills, a new GET reads saved configuration, and the normalized result becomes the clean baseline without client-generated status or timestamp

#### Scenario: Successful write but failed readback

- **WHEN** PUT succeeds and the following GET fails, then the user retries recovery
- **THEN** the successful write is distinguished from the read failure, only GET is retried, no PUT/POST is sent, and publication remains unavailable until confirmation

#### Scenario: Independent drafts

- **WHEN** configuration is saved successfully while skills have unsaved edits
- **THEN** configuration becomes clean after fresh GET, skills edits remain unsaved, and both publication entry points remain blocked

#### Scenario: Rejected save

- **WHEN** configuration save receives 422, 403, 409 or a transport failure
- **THEN** input is preserved, no success is fabricated, no automatic write replay occurs, and conflict recovery follows the existing manual GET-only policy
