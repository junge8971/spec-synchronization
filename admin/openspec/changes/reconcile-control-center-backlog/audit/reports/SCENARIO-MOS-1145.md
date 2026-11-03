# Code Context

## SCENARIO-MOS-1145 — documentary reconciliation

**Result:** Existing MOS-1027 owns the approved disable/enable UI; MOS-1031 owns future history reading. No duplicate plan is warranted. Primary sources expose reason-dictionary and lifecycle-documentation discrepancies, plus unresolved backend guarantees. This report does not verify implementation, runtime delivery, tests or repository index state.

No direct writes, code inspection, network requests, browser/MCP use, tests, builds or product changes were performed. Report supplied for persistence solely to `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1145.md`.

## Files Retrieved

Paths below are repository-relative. JSON evidence uses pointers and named HTML sections rather than artificial line numbers.

### Primary evidence and provenance

All content hashes below were recomputed from saved bytes and matched metadata.

| ID | Exact source | Version / capture | SHA-256 |
|---|---|---|---|
| J | `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-skill-switch-details/r1/content.json` and `metadata.json` | r1; captured `2026-10-16T13:58:59.883Z` | `2f2bd86c7a59b0e8232d0e5eb4f3dd6829f3860619374835a79f287b0e2a50be` |
| W | `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json` and `metadata.json` | r1; page revision 17, changed `2026-10-09T23:32:41.029+08:00`; captured `2026-10-16T11:48:21.710Z` | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` |
| C | `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r2/content.json` and `metadata.json` | r2; page revision 6, changed `2026-10-13T17:56:19.256+08:00`; captured `2026-10-16T12:37:03.295Z` | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` |
| A | `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` and `metadata.json` | r1; OpenAPI 3.1.0, service version 0.1.0; captured `2026-10-16T11:13:29.451Z` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| D | `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-details-MOS-774/r1/content.json` and `metadata.json` | r1; captured `2026-10-16T11:49:06.782Z`; item-key inspection | `e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208` |

Evidence locators:

- J `/items/0`: MOS-776 parent scope, including concierge redirection and agreement; zero comments.
- J `/items/1/description`: complete MOS-1145 requirements, DB model, operations and acceptance criteria.
- J `/items/1/comment`: two captured comments, total two. `/comments/0/body` mentions draft MR 18; `/comments/1/body` links the test plan. Neither was followed.
- J `/items/1/attachment/0`: attachment `835759`, `TEST_PLAN_MOS_1145.md`, metadata only. **Body unread.**
- J `/items/1/status/name`: `Ready for test`; `/updated`: `2026-10-16T19:22:39.198+0800`.
- W `/bodyView`: general principles; ЖЦ-5/6, АУД-1–4, ИСТ-6; complete ОТК-1–12 / ПРТ-ОТК-1–6; model §6.4 `skill_disabling`, §7.2–7.4; task mapping T-82–87.
- C `/bodyView`: general information/security/envelope; §2.6 detail; §2.8 editing; §2.9 concurrency/idempotency; §2.10 errors; §3 version history. Body heading says **v1.0**, history includes **v1.1 dated 14.09.2026**. These are not page revision 6 or capture r2. Metadata preserves earlier r1 404 with unexplained cause.
- A `/paths` and exact schema pointers detailed below.
- D `/items`: MOS-1119 not present. Scoped saved-source search found hierarchy membership under MOS-782 and a member-index entry, but no MOS-1119 detailed body. No dependency behavior inferred from those index references.

### Owning specifications, read completely

1. `openspec/specs/skill-global-toggle/spec.md` (1–94): current UI owner and historical approval.
2. `openspec/specs/skill-lifecycle/spec.md` (1–98): separate generic lifecycle and stale disabled-status wording.
3. `openspec/changes/archive/2026-10-13-mos-1027-skill-global-toggle/proposal.md` (1–29), `design.md` (1–63), `specs/skill-global-toggle/spec.md` (1–92), `tasks.md` (1–29): complete archived owner.
4. `openspec/changes/mos-1031-skill-audit-history/proposal.md` (1–27), `design.md` (1–26), `specs/skill-audit-history/spec.md` (1–47), `tasks.md` (1–17): existing blocked history-read owner.
5. `openspec/changes/archive/2026-10-02-mos-909-skill-lifecycle-rollout/proposal.md` (1–27), `design.md` (1–68), `specs/skill-lifecycle/spec.md` (1–68), `specs/control-center-mock-server/spec.md` (1–57), `specs/skill-training-phrases/spec.md` (1–30), `tasks.md` (1–24), `verification.md` (1–22): historical eight-status scope and generic-command boundaries.
6. `openspec/changes/archive/2026-10-02-mos-909-skill-current-status/proposal.md` (1–28), `design.md` (1–27), `specs/skill-lifecycle/spec.md` (1–41), `tasks.md` (1–18): historical read-only status owner.

### Auth/demo prerequisites, read completely

Under `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`:

- `proposal.md` (1–38), `design.md` (1–171), `tasks.md` (1–52).
- `specs/control-center-api-integration/spec.md` (1–64).
- `specs/control-center-http/spec.md` (1–71).
- `specs/control-center-mock-server/spec.md` (1–27).
- `specs/control-center-permissions/spec.md` (1–89).
- `specs/control-center-shell/spec.md` (1–101).
- `specs/mpmm-session/spec.md` (1–138).

Under `openspec/changes/archive/2026-10-09-add-local-session-demo/`:

- `proposal.md` (1–28), `design.md` (1–70), `tasks.md` (1–26).
- `specs/control-center-mock-server/spec.md` (1–106).
- `specs/control-center-shell/spec.md` (1–55).
- `specs/local-session-demo/spec.md` (1–123).

Also:

- `docs/mpmm-auth-rollout.md` (1–58): final historical release confirmation.
- `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (1–121): D-001–D-014, including index/runtime and source-version corrections.
- `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (1–194): discovery only; its unsupported empty-index attestation is not adopted.

## Key Code / Published Contract

No application code inspected.

Let `P = /paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}` within A.

### Exact operation comparison

| Aspect | Jira request | Saved OpenAPI |
|---|---|---|
| Disable | `POST /api/v1/skills/{skill_id}/disable` | `POST /api/control/api/skills/v1/skills/{skill_id}/disable`, pointer `P~1disable/post` |
| Enable | `POST /api/v1/skills/{skill_id}/enable` | `POST /api/control/api/skills/v1/skills/{skill_id}/enable`, pointer `P~1enable/post` |
| Path identifier | Example UUID | Required string, `format: uuid7` |
| Mutation header | Not specified in Jira example | Required `Idempotency-Key`, string UUID |
| Disable body | `reason`, nonempty `fallback_text` | Required JSON body; required `reason`, `fallback_text`, `expected_version` |
| Enable body | `reason`; no client action | Required JSON body; required `reason`, `expected_version` |
| Version | Not in Jira example | Integer `expected_version >= 1` |
| Success | Unwrapped example containing skill/status/action | HTTP 200 `TsamResponseSchema_SkillDisablingResponse_` |
| Declared error response | No exact HTTP/error mapping | HTTP 422 `HTTPValidationError`; no operation description specifying business errors |

Schema pointers under `/components/schemas/`:

- `DisableSkillRequest`, `EnableSkillRequest`: no declared client `action`, actor or timestamp fields.
- `SkillDisablingReason-Input`: string, `minLength:1`, `maxLength:32`, **not an enum**.
- `DisableSkillRequest/properties/fallback_text`: non-null string, `minLength:1`; no maximum or trim constraint.
- `SkillDisablingResponse`: required UUID `skill_id`, `status: SkillStatus`, `action: SkillDisablingActionResponse`; **no new version**.
- `SkillDisablingActionResponse`: all six fields required:
  - `id`: UUID string;
  - `action`: enum `disable | enable`;
  - `reason`: `SkillDisablingReason-Output`, unrestricted string;
  - `fallback_text`: string or null;
  - `actor_id`: string, **not UUID-formatted in this publication**;
  - `created_at`: date-time string.
- `TsamResponseSchema_SkillDisablingResponse_`: required `code`, `data`, `message`; optional non-null array `errors`; `ResponseCode` is a string, not a success enum.
- `HTTPValidationError`: optional `detail` array of `ValidationError`; each item requires `loc`, `msg`, `type`.
- `SkillStatus`: nine values, including `disabled`; not wiki’s eleven-status model.
- `tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`: required status/version and other detail fields, but no declared previous-status, disable-history, `off_since`, `prod_since` or `off_fallback` fields.

The schemas do not declare rejection of extra properties. Absence of client action fields therefore must not be restated as published `additionalProperties:false`. The normative no-client-action rule comes explicitly from Jira.

`P/get` supplies the full detail envelope. `P~1status/post` takes `ChangeSkillStatusRequest` (`status`, `expected_version`, optional nullable reason) and returns full detail, unlike disable/enable. Its description mentions `disabled` among transitions not waiting for the phrase queue. That is a reconciliation issue with Jira’s dedicated-operation prohibition—not permission to bypass disable validation.

Generic lookup exists at:

`/paths/~1api~1control~1api~1v1~1managed-resources~1catalogs~1lookups~1{section}/get`

`CatalogLookupSectionName` includes `skills`; its result is a string-keyed map of `ManagedResourceCatalogItem[]`. This does **not** publish a concrete disabling-reason key or prove active/historical filtering. The saved publication contains no literal `disabling_reasons`, `planned_maintenance` or `team_obligation_violation`.

### Security distinction

Both command operations publish:

```json
[{"AdminToken":[]},{"AccessToken":[]}]
```

This is formal **OR**. `/components/securitySchemes` descriptions explicitly require both raw `X-Admin-Token` and `X-Access-Token`. Archived approved auth specifies the paired **AND** model; C instead describes HttpOnly-cookie authentication. Preserve all three source descriptions without switching transport or choosing chronology as precedence.

The 09.10.2026 user-confirmed auth gate remains closed within its recorded scope. It is neither a new runtime attestation nor blanket approval of new functionality.

## Architecture

- **Backend request:** MOS-1145 owns dedicated operations, previous-status integration with MOS-1119, active-reason validation, atomic status/history changes and audit recording.
- **Approved frontend specification:** MOS-1027 owns prod/disabled presentation, confirmations, required input, request identity/version, response validation and read-based recovery.
- **Separate lifecycle:** MOS-909’s POST status matrix does not own global toggle.
- **History reader:** MOS-1031 remains the existing owner for type+skill-ID-filtered audit reading. A command’s action receipt is not a history-query API.
- **Session/presentation:** approved auth/demo determines real/mock mode and UI visibility. Backend authorizes requests; role prose, demo profiles and wildcard UI access do not establish server grants.

## Stable Candidate Findings

| ID | Evidence and reconciliation | Bounded disposition |
|---|---|---|
| **MOS1145-C01 — dedicated operations** | J `/items/1/description`, “Изменение статусов” / “API”, forbids generic status changes for disable/enable. Main toggle spec 38–46 already requires separate commands. A’s generic status description nevertheless mentions disabled. | Keep UI behavior unchanged. API owner should clarify whether generic disabled transitions are prohibited and how that is expressed. Do not infer runtime bypass or introduce one. |
| **MOS1145-C02 — stale lifecycle documentation** | Main `skill-lifecycle/spec.md:37–40` calls disabled absent from the enum; 78–83 still enumerates eight statuses. A includes disabled and main toggle spec 11–23 requires reading it. Historical MOS-909 documents explain the older snapshot. | Concrete documentation-correction candidate: reconcile current disabled read/display wording and qualify generic-command exclusions without adding transitions. Preserve historical archive evidence. Requires separate edit approval. |
| **MOS1145-C03 — previous-status recovery** | J requires saving/restoring the immediately preceding status through MOS-1119, not duplicating it in `skill_disabling`. MOS-1027 approval explicitly fixes prod → disabled → prod for current UI; A does not expose previous status. | Preserve approval dated **13.10.2026**. It does not establish all-status restoration or permission to enable to hardcoded prod. Ask owner for authoritative MOS-1119 mechanism and behavior for externally disabled non-prod skills. Missing dependency body remains a limit. |
| **MOS1145-C04 — dictionary versus free text** | J requires active `disabling_reasons` codes `incident`, `planned_maintenance`, `team_obligation_violation`. W §7.3 instead uses `skill_disabling_reasons`: `incident`, `maintenance`, `obligations`. Main toggle 34–51 and archived design use free text 1–32 because the wire schema is string-based. | Material requirements/UI tension. Schema-valid arbitrary text is not proven business-valid. Resolve dictionary source, exact lookup key, authoritative codes and active selection with existing MOS-1027 owner. No hardcoded selector, aliases, automatic coercion or new plan authorized. |
| **MOS1145-C05 — active new actions versus retained history** | J explicitly disallows inactive reasons for new disable **and** enable, while retaining existing historical reasons. A has bounded input string versus unrestricted output string; generic lookup shape does not prove inactive inclusion. | Record backend rule now; leave consumer lookup behavior unresolved. Do not delete historical codes or apply current-input restrictions retroactively to response/history. |
| **MOS1145-C06 — action dictionary/model differences** | J specifies fixed domain enum, no action dictionary, required reason FK to `disabling_reasons`; W §6.4/7.3 specifies action FK to `skill_disabling_actions`, optional reason FK to `skill_disabling_reasons`. W general dictionary widths also differ from J’s code32/display100. | Genuine source-model discrepancy for backend/documentation owner. No database migration inferred from OpenAPI or approved by this audit. |
| **MOS1145-C07 — fallback semantics** | J requires nonempty disable text and enable history `fallback_text = NULL`. A requires nonempty disable string but allows string/null for action output without action-conditioned nullability. Main toggle requires trimmed nonempty input and omits fallback from enable request. | Existing form coverage is adequate for agreed UI. Null-on-enable remains a backend guarantee to reconcile; schema alone does not enforce it. Do not synthesize null receipt fields or assert whitespace rejection from `minLength` alone. |
| **MOS1145-C08 — action identity and provenance** | J derives action from endpoint and requires action UUID, actor UUID and server time; W uses `actor_user_id` (external SUDIR UUID), A uses unformatted `actor_id` string. Main toggle 60–64 binds skill/action and avoids fabricated success. | Preserve exact wire names/types; no UUID tightening, current-user substitution or locally invented event/time. Ask identity owner to reconcile actor identifiers. Command receipt does not prove append-only storage or delivery to audit. |
| **MOS1145-C09 — atomicity and repeats** | J requires status change plus history insertion in one transaction; repeated disable must not insert a new record. Successful enable requires disabled state and its own history row. Audit emission is required, but Jira’s explicit transaction sentence names status/history—not a distributed audit transaction. | Backend acceptance evidence remains missing. Pending UI suppression is not transactional deduplication. Distinguish repeated business action, same-key replay, concurrent requests and enable outside disabled; no exact error/success response for repeats is established. |
| **MOS1145-C10 — versions, replay and uncertain outcome** | A adds mandatory version/key beyond J examples. C §2.9 documents generic POST/PATCH replay and PATCH version conflicts, not an explicit toggle operation protocol. Main toggle 58–94 already prevents automatic repeats/reversals, validates receipt, rereads version, and separates command success from failed GET. | **No-op for existing recovery requirements.** Do not transplant catalog `409 VERSION_CONFLICT` or generic replay wording into command-specific guarantees. Same-user auth recovery preserves logical parameters but does not authorize automatic replay or bypass toggle recovery rules. |
| **MOS1145-C11 — errors and namespaces** | Jira short path differs from A’s namespaced path. A command responses enumerate 200/422 only; GET/status descriptions contain additional errors, but those are operation-specific. C’s CRUD errors use their own envelope/code descriptions. | Endpoint traceability/documentation candidate only. Existing UI owner already uses published namespaced paths and generic transport error handling. Obtain exact business errors for inactive reason, repeat, transition, stale version and audit failure before claiming them. |
| **MOS1145-C12 — history ownership** | J and W require history/audit recording. A action receipt supplies one action; inspected `/paths` contains no audit/history read path. MOS-1031 already requires stable type+ID, pagination, redaction and honest delayed-event handling. | Retain MOS-1031 gate; no duplicate history plan or fabricated local journal. Absence is bounded to inspected publication, not proof backend history does not exist. |
| **MOS1145-C13 — broader parent effect** | J parent lists concierge redirection/agreement. W ОТК-6–8 and T-83–86 add core propagation, common-answer routing and notifications; ОТК-3/T-82 adds 30-day impact and preview; ОТК-12/T-87 adds timestamps/duration. MOS-1027 explicitly excludes rich impact/history and does not promise instantaneous application. | Preserve these as broader requested scope, not effects proven by status. Parent agreement workflow is not replaced by a confirmation dialog. No guessed preview endpoint, SLA, timer or routing implementation; owner/scope questions remain. |
| **MOS1145-C14 — roles and mock boundaries** | J/W product/operations roles are requirement prose. Approved auth grants only mapped UI permissions; unmapped toggle retains explicit wildcard policy, not invented `TSAM.Skill:disable/enable` or inherited change_status. W’s disabled-button role example also differs from approved permission-based hiding. | No new grants or auth changes. Real mode uses approved paired credentials; mocks remain credential-free without role enforcement. Demo/full or fixed 403 is not backend authorization evidence. |
| **MOS1145-C15 — evidence completeness** | J comments fully captured, but attachment body unread; Ready-for-test and draft MR mention are documentary status only. Archived MOS-1027 tasks record prior local checks and user/backend consultation, explicitly without real POST execution. | Preserve historical approval and recorded results without re-attesting them. No feature closure, deployment claim or inferred test-plan contents. Independent review remains required. |

## Start Here

Open `openspec/specs/skill-global-toggle/spec.md:30–94`, then the complete archived MOS-1027 design. These establish the existing owner, approved UI and recovery boundaries.

Recommended next documentary disposition, **not authorization to edit**:

1. Review C02 as a narrow current-spec consistency correction.
2. Route C03–C08 and C11 to the existing backend/UI owners for source reconciliation.
3. Preserve C09/C12 as backend evidence and existing history-gate questions.
4. Keep C13’s broader parent scope visible without activating it.
5. Leave current confirmation/recovery/security behavior unchanged pending separate approval.

## Residual Risks and Limits

- Attachment `835759` body and detailed MOS-1119 contract remain unavailable in inspected saved evidence.
- Conflicting reason codes/models and generic-status wording remain unresolved; no source precedence selected.
- Historical approvals on 09.10.2026 and 13.10.2026 are preserved, not extended.
- Backend execution, transaction boundaries, propagation, audit persistence, tests and implementation were not verified.
- Git/index state was not inspected; no empty-index attestation is made.
- No product changes or task closures are authorized by this report.