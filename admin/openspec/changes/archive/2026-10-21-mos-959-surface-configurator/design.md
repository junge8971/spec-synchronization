## Context

See proposal.md for motivation and exact approval. D-096 authorizes lifting only configurator deferral and selects published API as wire authority. The subsequent user «Подтверждаю» approves presets plus arbitrary #RRGGBB; local demonstration preview without requests or card execution, with separate fallback preview; explicit configuration save, dirty-publication blocking, fresh GET and GET-only recovery. It does **not** approve the earlier author's combined-save/publish recommendation, navigation prompts, editable personas, stricter creation integrity or a sandbox workflow.

The supervisor clarified the conservative compatibility interpretation: retain existing clean enabled-skills PUT during confirmed Publish. Blocking dirty publication removes the promise to publish unsaved drafts, not that established preparation write. Readback recovery never replays it or implicitly continues publication.

### Evidence and freshness

`A` below means `openspec/changes/reconcile-control-center-backlog/audit/`.

- `A/work-items/WRITE-MOS-959.md`, `A/decisions.md` D-096; follow-up user approval recorded above pending parent register update.
- `A/reports/REQ-MOS-959.md` candidates 001–039 and `A/reviews/RECON-MOS-959.md`, `RECON-MOS-959-CONTRACT.md` are reused analysis, not new authority over primary sources.
- `A/sources/api-live/r2/content.json`, saved 2026-10-19T08:11:44.238Z, SHA-256 `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993`: `/paths` operations POST `/api/control/api/surfaces/v1/surfaces`, GET `/{surface_id}`, PUT `/{surface_id}/configuration`, PUT `/{surface_id}/enabled-skills`; `/components/schemas/UpdateSurfaceConfigurationRequest`, `SurfaceCardRequest`, `SurfaceCardActionRequest`, `SurfaceConfigurationShape`, `SurfaceConfigurationFont`.
- `A/sources/wiki-245673187/r1/content.json`, SHA-256 `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa`: `/bodyView`, headings `id-Бизнесанализ:Поверхности-Вкладка"Конфигуратор"` rows 0–26, `id-Бизнесанализ:Поверхности-Общиедлявсехвкладок.1` rows 7,12–14, dictionaries 4.3 and configuration/card fields 5.1–5.2. Use nonconflicting UI text only; row 26 is resolved by user approval, row 12's dirty autosave promise is superseded by it.
- `A/sources/wiki-241082009/r2/content.json`, SHA-256 `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b`: `/bodyView` sections 1.3, 2.3–2.5. Page revision 5/body contract v1.0 has older shape/font vocabulary, nullable fallback, different defaults and combined enabled_skills PUT. Do not alias its codes or use its payload in place of published API. Immediate Prod application is a publication claim, not verified latency.
- `A/sources/jira-api-delta-scenarios/r1/content.json`, SHA-256 `b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed`: `/items/3/description` MOS-959; `/items/2/description` MOS-1237 blank-validation concern. Test-plan attachment body unavailable; issue status is not delivery proof.

No network/freshness/deployment check occurred. API publication constrains this plan, not claims about deployed validation or widget timing.

## Goals / Non-Goals

**Goals:** expose existing configuration transport safely, keep local draft/preview separate from saved facts, make explicit save/readback and dirty publication guards testable using unit/component/mock HTTP tests.

**Non-Goals:** runtime implementation in this delivery; registration redesign; new backend endpoints; combined skills/configuration transaction; history, sandbox, resident widget execution or propagation SLA; new permissions, auth/session models, role enforcement in mocks; automatic stale-card removal; reorder UI, accent-card editor, persistent configurator drafts or new navigation/discard policy.

## Decisions

### 1. Source-aligned transport, not Wiki compatibility aliases

`docs/api/contracts/openapi.json` has the same seven required configuration fields and shape/font enums as r2, but lacks published greeting/item/card length and list-count bounds. All four selected operation descriptions differ; do not wholesale replace operations/security from r2. The local `SurfaceCardActionType` also lacks the published `link` member; the user approved adding it during apply. The user subsequently approved synchronizing `docs/api/contracts/surfaces.openapi.json` and the contract provenance tests: raw snapshots/hashes remain unchanged, tests assert the exact MOS-959 delta before comparing all remaining fields with the original snapshot. Narrowly update configuration request constraints, this action enum and directly relevant documentation, regenerate via `scripts/generate-api-types.mjs` (never hand-edit `app/shared/api/schema.d.ts`). Preserve agreed envelope/security normalization.

Full replacement contains accent_color, shape, font, greeting, greeting_fallback, suggestions, cards; no enabled_skills or invented card IDs. Preserve saved card accent (default false for new cards) even without an accent editor. API creation omission/null defaults are #B3121B, round, moscow_sans, both greetings «Здравствуйте! Чем помочь?», empty lists: retain registration omission, never initialize an existing editor by overwriting GET with those defaults. GET response is the baseline.

API provides trimming, UUID canonical lowercase, duplicate rejection and action-specific rules. Do not invent parser escaping/case aliases, duplicate-equivalence algorithms, Unicode counting semantics or local deduplication. Implement unambiguous structural bounds/format checks and map server validation paths; server remains authoritative for unspecified edges. Reject unsupported tokens/unpaired braces without creating new token syntax. A stale skill action stays visible and repairable; server rejection must not delete it or silently re-enable the skill.

### 2. Ownership and reuse

- Compose a new `features/surface-configurator/` public editor/controller API in `app/widgets/surface-details/ui/surface-details/surface-details-content.tsx`; do not import another feature's internals. Widget owns coordination with the existing skill controller and shared operations.
- Reuse `app/entities/surface/api/surface-registry-client.ts`, `model/use-update-surface-configuration-mutation.ts`, `model/use-surface-mutation-controller.ts`, detail query/refresh helpers and public entity types. Extend `app/widgets/surface-details/ui/surface-details/model/use-surface-details-operations.ts` and action policy for the common lock and both dirty guards.
- Reuse installed form/schema tools and shared labelled inputs/tabs/buttons rather than adding dependencies. Place named types/constants/handlers in owning technical directories; one handwritten component per file.
- New draft belongs to surface ID and current session owner; keep it in the mounted card controller across tabs, no new storage. Existing session owner guard protects async results. Background reads update saved facts but do not overwrite dirty input. Compare ordered editable fields against the saved baseline; changed-then-restored values are clean, array ordering is retained, no timestamp-based equality or speculative normalization.

### 3. Local preview and editor

Default card tab becomes Configurator. Show the Wiki appearance and content controls, exact list empty states/hints and limits. HEX input accepts the approved full #RRGGBB domain; no bare-HEX conversion or preset-only restriction. Always expose fallback beside greeting with API conditional help.

Use a pure local renderer for Greeting/Dialog plus separate fallback view. Fixed visibly demonstrative substitutions (for example Иван, Иванович, Добрый день) are presentation fixtures, not resident identity or a time-of-day service; exact sample wording is a minor implementation detail, not another product policy. Render all content as text, style only validated appearance values. Preview does not mount a widget, fetch fonts/resources, navigate links, start a skill or send a message. Use existing/local font assets or CSS fallbacks, not remote font requests. Invalid partial input remains editable with errors; preview is never validation or save confirmation.

### 4. Explicit save and compatible publication preparation

Configuration has its own explicit save button; skills retain their existing save action. Saving configuration never writes skills. Both publish entry points require both drafts clean, existing status/permission eligibility, no operation/readback/conflict block, and nonempty skills. Guard again after confirmation and immediately before writes. Preserve the established confirmed-publication sequence: skill validation → clean skills PUT → fresh detail GET → eligible bodyless POST publish → detail confirmation. Do not add configuration PUT to it.

Configuration save locks competing edits/writes, sends the complete edited DTO, records confirmed response fields, and starts a new GET after PUT. A prior in-flight GET cannot confirm it. GET establishes normalized saved configuration/baseline; updated_at is not a configuration revision. On confirmed write plus failed GET retain input and last-known facts, distinguish saved/readback-unconfirmed from write failure, block publication pending fresh confirmation, offer GET-only recovery. That recovery never PUTs or implicitly publishes, including after publication preparation skills PUT. New explicit publication still requires confirmation/preparation. Preserve dirty input across unrelated skill readback; freeze submitted config during its save/readback so normalization can be adopted without losing later edits.

422 paths map to fields when reliable; general errors stay visible with draft intact. Existing 409 manual refresh/conflict lock, server-owned status and session handling remain. No automatic write replay on transport uncertainty or auth refusal. Keep navigation behavior unchanged: this approval did not add route blockers/discard dialogs.

### 5. Existing permissions and mock isolation

Use current Surface:view/update presentation policy for configuration viewing/editing and existing lifecycle permission requirements; retain current skill-view requirements for skill UI and existing publish preparation. Do not derive new grants from role names or preview data, and do not add permission checks to transport/handlers. Backend authorizes requests. Existing real session/owner guards and credential destination checks remain.

Read historical approved auth/mock proposal/design/specs at `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/` and `2026-10-09-add-local-session-demo/` for these constraints, not as new work. Dev defaults to credential-free Express mocks; production/dev opt-out uses real integration by launch config, never hostname. No new mock profiles or role enforcement.

`mocks/surfaces.mjs` configuration handler currently assigns configured and changes updated_at; do not use that as production evidence. Align the selected configuration handler/validation with published save/readback rules, including unchanged timestamp/token/embed code and preserving server status rather than synthetic readiness. Keep unrelated lifecycle mock conventions unchanged. `mocks/surfaces.test.mjs` already covers creation defaults/atomic configuration; retain those tests and add save-specific ones.

## Risks / Trade-offs

- [Versioned sources disagree] → r2 wire authority plus explicit approval; no aliases or combined PUT, no external freshness claim.
- [Dirty guard conflicts with legacy autosave copy] → full lifecycle publish/deferral and overview checklist deltas, preserving clean skills preparation; test both entry points.
- [Successful write/read failure repeats a write] → explicit recovery phase with GET-only action and request-count tests; no automatic publication continuation.
- [Stale card skill or normalization edge] → preserve input/server error, explicit repair, no speculative mutation of adjacent resources.
- [Mock behavior differs from deployment] → bounded mock alignment and contract tests are local evidence only; no claim of real backend acceptance.

## Migration Plan

After separate apply authorization: align selected configuration contract constraints; add editor/preview and save controller; integrate publication dirty/readback guards; add focused tests and mock alignment; run quality gates. No database migration or new endpoint. Rollback the UI integration to placeholder without sending compensating writes or resetting saved server configuration. Main-spec synchronization/archive remains a later explicit workflow; rebase complete modified requirements against any intervening main-spec changes before sync.
