## Why

MOS-1051 reports incorrect Russian count inflection after the training-status filter. The registry still renders a fixed `навыков` suffix, and existing assertions encode incorrect `1 навыков` and `2 навыков` labels; the accepted JOIN-SKILL-REGISTRY and R-SKILL-REMAINING-SEVEN evidence supports a narrow correction.

## What Changes

- Inflect the server-total label as `навык`, `навыка`, or `навыков` using existing/platform plural facilities.
- Preserve server filtering, URL/history, pagination, and the numeric total.
- Correct erroneous assertions and plan regression coverage for 0, 1, 2–5, 11–14, 21–24 and `status=training`.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `skill-catalog-experience`: require Russian inflection of the existing server-total count label.

## Impact

Limited to the count presentation in `app/widgets/skills-registry/ui/skills-registry.tsx`, its small formatting helper if needed, and nearby unit/component assertions. No new dependency, API/schema change, local counting, registry redesign, sorting change, notification work, or auth/permission change. This package is planning only; parent review and separate implementation authorization remain required.
