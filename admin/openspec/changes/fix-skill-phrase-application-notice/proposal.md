## Why

MOS945 reconciliation confirms that the phrase editor lacks the existing required distinction between saved skill version and unavailable application/retraining data. A save confirmation, including one followed by a failed detail read, must not be mistaken for model application.

## What Changes

- Make the existing application-data-unavailable notice explicit on the training phrases tab in viewing and editing states.
- Clarify confirmed-save and failed-follow-up-GET behavior while preserving the confirmed saved version and groups.
- Retain the deferred applied-model indicator; do not infer training started, completed, or a version became active.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `skill-training-phrases`: clarify placement and persistence of the saved-version/application-unavailable disclosure.

## Impact

Bounded UI change in `app/features/skill-training-phrases/ui/skill-training-phrases.tsx` and assertions in `app/widgets/skill-details/ui/skill-details.test.tsx`. No API, dependency, permissions, or save-protocol changes. MOS1018 preflight and persisted readiness results remain separate. This package is planning only; parent review and integration precede separately authorized implementation.
