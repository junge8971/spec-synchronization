## Context

See proposal.md for motivation. `skill-details-client.ts` uses a loose detail schema without a declared checks decoder (unknown checks need not be stripped); `checks-tab.tsx` accepts only status. `use-skill-details-query.ts` already owns processing-only polling and pauses on read failure. Reuse the complete accepted SCENARIO-SKILL-CHECKS / R-SKILL-CHECKS and JOIN-SKILL-CHECKS evidence, bounded by R-SKILL-REMAINING-SEVEN §4.

## Goals / Non-Goals

**Goals:** Typed persisted results integrated into the existing observation path, preserving record identity, drafts and truthful last-read semantics.

**Non-Goals:** Backend computation/backfill, new mutation/retry flows, lifecycle MOS-909 changes, review results expansion, MOS1018 preflight, token/security changes, or claims about applied phrase versions. Run IDs, input correlation, technical process-error interpretation, rerun permissions and sandbox availability require separate agreement.

## Decisions

- Extend existing detail types and decoder with the published required checks array and required `check_type`, `status`, `blocking`, nullable `message`, date-time `checked_at`. Actual enums: types `anketa`, `phrases`, `exact_conflicts`, `semantic_conflicts`, `endpoint`; statuses `passed`, `failed`, `warning`, `blocked`. Use existing contract-error handling for malformed responses rather than synthesizing success. Do not treat an absent field as the documented empty array.
- Render in published type declaration/display order, not severity/rank order. Show textual status, blocking indication, corrective message and timestamp using existing UI formatting; never HTML-interpret server messages. Published invariants are passed/false/null, only blocked/true, and failed/warning nonblocking with corrective messages. Do not map technical failures to failed or implement client calculation. An aggregate readiness score would invent semantics and is rejected.
- Use the existing detail query and shared response path, not a second polling loop. Accept changed checks/checked_at from a successful read even with unchanged version/updated_at; neither field is a checks freshness token. Keep data keyed to skill ID and cancellation behavior. Update observation without resetting dirty fields or their expected_version. Preserve existing polling interval, visible processing-only activation and manual reads for other statuses.
- A failed read retains last-loaded results with a stale/read-error indication and pauses polling. Recovery retries GET only; it neither recalculates checks nor repeats a mutation. No event feed or real-time freshness promise is introduced. Existing mutation/lifecycle recovery ownership remains unchanged.

## Risks / Trade-offs

- Saved publication is not runtime or backfill proof → retain empty/uncomputed display and distinguish contract/read failure; future authorized integration acceptance must verify the agreed response without inventing compatibility fallbacks.
- Peer recalculation can change results silently → accept every fresh detail response; label last-read data without expanding polling.
- Check completeness could be confused with process success → retain explicit current-input/training/sandbox disclaimer, including endpoint completeness not service health.
- Questionnaire zones, threshold configuration and normalization remain source-owner issues → display server results only; no local policies or payload expansion.

## Migration Plan

No data migration or new dependency. After separate implementation authorization, update decoder/types, props/rendering and bounded assertions together; include valid persisted-check fixtures. Rollback is the display/decoder change, not backend checks or historical specifications. Parent review and integration precede any apply; no runtime work is authorized here.
