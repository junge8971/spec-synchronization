## Context

See [proposal](proposal.md) for authority and evidence links. D-084 resolves frontend scope only. REQ R01–R19 record historical backend obligations; the user explicitly excluded R15 export-limit definition and acceptance from current frontend scope. API reports absence in saved r2/local/generated contracts, not live deployment absence. Both export operations and their 19-column defaults are now published in the T OpenAPI linked in proposal.md; no export request was executed. SPEC/recovery and independent review support a new owner without changing historical owners.

Current anchors inspected: `app/widgets/skills-registry/ui/skills-registry.tsx` composes normalized URL filters, pagination and independent shown-row rollout selection; `app/entities/skill/api/skill-registry-client.ts` maps list parameters and also has `getAllSkills` pagination, neither being export. `app/widgets/skill-details/ui/skill-details-header.tsx` has metadata only. `app/shared/lib/handlers/download-attachment.ts` and its tests provide temporary anchor cleanup, not object-URL management. `app/shared/api/file-response.ts` parses UTF-8 extended filenames and sanitizes control/path characters; its exact header expectation must be checked against the future skill contract, not imposed on it. Existing React Query, HTTP transport, browser Blob/object URLs and test tooling suffice; no dependency is needed.

## Goals / Non-Goals

**Goals:** Add two thin UI entrypoints sharing request lifecycle and safe attachment handling, with independently verifiable backend integration acceptance and no change to list/edit behavior.

**Non-Goals:** Client CSV generation, fetching all pages to manufacture an export, exporting checkbox selections, importing CSV, scheduling, column-selector UI, backend implementation in this frontend repository, new authentication/permissions policy, or claims of deployed integration from mocks.

## Decisions

### 1. Implement the published contract

REQ R01/R02 identify requested `POST /api/control/api/skills/v1/skills/export` and `POST /api/control/api/skills/v1/skills/{skill_id}/export`; both are now published, but reproducible local contracts still require alignment. The user explicitly approved implementation against this publication without further backend clarification gates. Record the available evidence below and align reproducible saved aggregate, split contracts and generated types before wiring requests. Do not invent aliases or handwritten substitute DTOs. Retain existing security normalization and approved session transport; export-specific security must be established from publication. Conflicting publication returns to agreement; R15 is explicitly excluded by the confirmed scope decision, not silently waived. An unspecified export limit or limit-specific error is not a gate. No frontend cap, guessed limit error or mock limit is introduced; all returned backend errors still prevent download.

**Contract and acceptance checklist (REQ R03–R19; API evidence):**

- Both operations, JSON request schemas and `{}` defaults; exact supported filter/sort validation and default sort; behavior if pagination keys are supplied (frontend never supplies them).
- Allowed `fields` codes, default full column set, labels/order, equality across list/card, empty/unknown-field errors, duplicate-field handling. Initial UI omits `fields`; do not infer columns from the table or questionnaire.
- Existing missing/inaccessible-card errors and validation errors, including published statuses/bodies. No guessed status or DTO. Numeric export limits and limit-specific errors are outside this checklist.
- Binary file response/media type, attachment disposition and filename encoding/header exposure; generation date/timezone and exact filename convention, with card ID. Resolve compatibility with the existing filename reader without inventing a filename fallback.
- BOM/semicolon/header, quoting/newline/null conventions, one row per skill, header-only empty selection and injection mitigation; backend acceptance evidence for CSV safety; frontend failure paths never download incomplete transfers or error bodies.
- Export operation security requirements, existing `TSAM.Skill:view` mapping and server skill/team access restrictions, excluding deleted skills. No new credentials, policy, anonymous-access inference or session mechanism.

Unspecified backend details and real integration evidence remain documented acceptance unknowns, not implementation blockers. The frontend preserves server bytes and handles errors; it does not infer column labels, sort policy, CORS guarantees or undocumented error codes. Mock-only conventions are labeled as such.

### 2. Compose one feature without crossing FSD boundaries

Put typed skill export access behind `entities/skill` public API, and action/lifecycle UI in `features/skill-csv-export`, composed by registry and detail widgets. Keep named types, constants and handlers with their nearest owners and one handwritten component per file. Reuse shared HTTP and file utilities where compatible; extend a shared helper only for demonstrated common behavior. Do not import a neighboring feature's internals or copy another domain's export contract. Alternative: widget-local duplicate clients would split safety and error handling without benefit.

### 3. Capture current selection, not current rows

At activation, snapshot the registry's normalized applied filter/sort state and map only agreed `query`, `domain_id`, `team_id`, `status`, `type_code`, `sort` semantics into the export body. Exclude page/page size, `limit`, `offset`, selected IDs and data rows. A later filter change does not mutate an in-flight request; the next activation uses the new state. Place the action with registry controls, outside rollout. A confirmed empty selection remains exportable (server header-only file). Do not export from a loading/error/placeholder view as if it confirmed current data. Card action uses the saved skill identity, with a label/explanation that unsaved edits are not included; never submits draft data or implicitly saves. REQ R04/R08–R10/R16–R18 justify these boundaries.

### 4. Use server default columns for the initial actions

Confirmed user scope choice: both actions omit `fields`, using all 19 published server-default scalar columns (card sends `{}`). Intents, phrases, readiness checks, connection parameters and related materials are not part of this file. Backend optional-field equality and validation remain integration acceptance, even though no selector is exposed. A richer UI needs separate scope approval; omission avoids inventing enums or turning a simple action into an unrequested editor. This choice follows REQ R03/R05–R07, not an assertion that all backend options are exposed.

### 5. Receive and dispose of a server file safely

Use the existing approved request/session lifecycle, not direct credential-bearing fetch or arbitrary remote download URLs. Check the agreed successful file response and safe server filename before triggering download; never download an error body or partially received response. Preserve returned bytes (no parsing/reserialization or client formula mitigation). Use a Blob URL only for the validated complete response, revoke it after handoff at a safe lifecycle point and on abandoned/error paths, and remove temporary anchors even if triggering download fails. Cancel on unmount/context invalidation and suppress late results even if abort is ignored; do not replay the export after session recovery. Do not retain sensitive bytes/URLs in long-lived caches. Pending disables duplicate activation. Accessible status/error text and explicit retry must not claim the file was saved to disk merely because download was initiated. REQ R12–R14 and existing API/session isolation obligations supply the safety baseline; generic failure safety remains required independently of the excluded limit policy.

### 6. Preserve existing security and verification ownership

Reuse current `TSAM.Skill:view` UI visibility through existing permission APIs; backend still authorizes both actions and team/skill access. Do not require edit/rollout permissions. Before any future session/mock integration work, reread approved `integrate-mpmm-auth-permissions` and `add-local-session-demo` artifacts; this change does not revise them. Express business mocks remain credential-free without role enforcement, selected by existing launch configuration and excluded from production. Mock file responses must be served by handlers after agreement, never synthesized by runtime client fallback. Unit/component tests cover request mapping, pending/errors, drafts, cleanup and accessibility; mock HTTP tests cover agreed fixtures/validation, not backend security proof. Backend format/injection/access evidence is separately required; export-limit acceptance is excluded from this delivery.

## Risks / Trade-offs

- Missing publication → keep dependent tasks blocked and export unavailable, with accessible explanation if an action is shown; no fake success.
- Default columns may not suit every user → initial defaults-only scope is confirmed; richer selection is separate work.
- Whole-selection files consume browser memory → the accepted scope has no frontend cap or limit gate. Retain cancellation, cleanup and error handling, avoid client pagination, and record large-file memory risk rather than claiming unlimited safe capacity.
- Unsafe filename or malformed file response → reject rather than manufacture successful output; unavailable headers produce an explicit error, not a guessed filename.
- Late response after context replacement → abort plus stale-result suppression and resource cleanup under existing session ownership.
- Bounded saved evidence → no live/deployment or historical SPEC hash-equality claim; user acceptance permits implementation; no independent review or runtime verification is claimed.

## Migration Plan

This revision changes planning only. The user requested implementation and confirmed the defaults-only/no-limit scope. With the user's explicit acceptance of implementation from the published contract, align contracts/types, implement the feature and composition, add explicit mock coverage and focused tests, then perform project checks. Enable real requests only after agreement; record real integration evidence separately from local tests. Rollback removes/disables export composition and connected handlers without changing registry pagination, rollout, editing or session behavior. No data migration is needed.
