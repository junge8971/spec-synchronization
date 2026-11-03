## Why

MOS-959's surface configurator remains a placeholder despite existing configuration transport. D-096 authorizes a separate configurator plan with published API wire authority; subsequent explicit user confirmation resolves the material color, preview and save-policy gates.

## What Changes

- Replace the configurator placeholder with saved appearance/content editing and local Greeting/Dialog previews, including separate fallback preview; make Configurator the default card tab.
- Offer color presets plus arbitrary `#RRGGBB`; use published shape/font codes, placeholders, field bounds and separate configuration/skills writes.
- Provide explicit configuration saving. Block both publication entry points while configuration or skills are dirty. Follow successful saves with fresh GET; failed readback retries GET only, never replays the successful write or implicitly publishes.
- Preserve existing clean enabled-skills PUT during confirmed publication preparation. Publication never implicitly writes configuration.
- Narrowly supersede configurator deferral, not history/sandbox exclusions, server-owned lifecycle state, registration behavior or current permissions.

## Capabilities

### New Capabilities

- `surface-configurator`: contract-backed appearance/content editor, inert demonstration previews, explicit configuration save and readback recovery.

### Modified Capabilities

- `surface-lifecycle-publication`: replace the full configurator-deferral requirement and add dirty guards/read-only recovery to existing confirmed publication preparation without removing its clean skills write.
- `surface-overview-connection`: replace checklist's unsaved-draft autosave promise with explicit-save guidance; preserve saved facts and all unrelated protections.

## Impact

Reuse surface entity transport/mutation hooks, surface-details composition/operation lock, existing skill draft controller, session presentation policy, shared form/UI primitives and Express mocks. Detailed file seams and source references are in design.md. Local configuration schema bounds, the missing published `link` action enum member (approved during apply), and mock configuration behavior require narrowly scoped alignment during later implementation, not a wholesale contract refresh. No dependencies, new endpoints, auth model, sandbox activation or runtime implementation are part of this planning delivery.

Authority: D-096 plus the user's subsequent «Подтверждаю» to (1) presets plus arbitrary #RRGGBB, (2) local demonstration preview with no requests/action execution and separate fallback preview, (3) explicit configuration save, publication blocked by either dirty draft, fresh GET after save and GET-only readback recovery. Earlier author recommendations beyond these statements are not approved. Saved API r2 is historical evidence, not external freshness or deployment verification.
