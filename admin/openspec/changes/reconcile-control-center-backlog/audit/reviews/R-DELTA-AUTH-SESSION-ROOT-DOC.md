# R-DELTA-AUTH-SESSION-ROOT-DOC

## Review

**Disposition: REVISE — one narrow documentary correction.** Approved auth remains unchanged; this is not an implementation or new-auth approval.

### Inspection completed

Repository-relative aliases:

- **B** = `openspec/changes/reconcile-control-center-backlog/audit`
- **A** = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`
- **R** = `B/reports/DELTA-AUTH-SESSION-ROOT-DOC.md`
- **S** = `B/sources/wiki-238329164-readable/r1/content.txt`
- **C** = `B/sources/wiki-238329164-readable/r1/body-view-chunks.json`
- **J** = `B/sources/wiki-238329164/r1/content.json`

Read completely:

- Assigned reviewer work item, analyst work item and analyst report.
- Before source comparison: `A/proposal.md`, `A/design.md` and all six specs: `mpmm-session`, `control-center-http`, `control-center-permissions`, `control-center-api-integration`, `control-center-shell`, `control-center-mock-server`.
- Complete readable source, all nine exact markup chunks, original JSON including body and returned attachment index, and both original/derived metadata files.
- Attributed decision excerpts `B/decisions.md:57–61,219`; their underlying historical evidence was not freshly audited.

Verified identity: page **238329164**, capture **r1**, version **13**, version timestamp **2026-09-01T20:03:36.508+08:00**. The returned attachment index in `J:13–20` has `size: 0`, `next: null`, and empty `results`; this is not an exhaustive export/attachment-absence guarantee.

### Correct: candidate verification

| Candidate | Verification |
|---|---|
| **ASR-01** | `R:31`, `S:3–10,39–54`, `C:2–3` correctly distinguish historical СУДИР exchange, profile/session storage and idle exit from approved MPMM navigation and validated principal. No OAuth example occurs in this body. |
| **ASR-02** | `R:32` correctly assigns §§1–3, 8–8.3, 13, 17 and relevant §19 password controls to СУДИР, retaining §19.4’s alternative ППО wording. `S:60–91,125–128,155–157,164,169–173,178–182` supports those locators. Password lifetimes are not JWT expiry; the approved finite admin-token `exp`/30-second refresh scheduling remains separate. |
| **ASR-03** | `R:33`, `S:149–154,174–177`, `C:7–8` correctly distinguish user inactivity, unused-account blocking and refresh timing. The source gives 5–15 minutes as practice, expressly no prescribed ГИС К3 value, and 90 days as password-policy wording for unused accounts—not verified runtime enforcement. |
| **ASR-04** | `R:34` correctly preserves the broad ППО definition (`S:18`), excludes frontend role administration/global session termination, and does not turn a security-administrator label into permissions. Its row-level desirability wording needs the correction below. |
| **ASR-05** | `R:35`, `S:94–148,160–161,183–184,191–192` support event type/time/result/subject, attempted identifier, role-change actor/target/role, and object-access details. §8 separately supplies account-action time, target identifier and acting identifier under СУДИР (`S:125–128`). The report correctly retains the §5.2 ППО versus §8 СУДИР responsibility tension. Retention is ППО-side, minimum three months, preferably one year—not frontend telemetry authority or permission to log credentials. |
| **ASR-06** | `R:36`, `S:162–163`, `C:7` accurately retain **«Желательно (Требование ДИТ)»**. This is historical desired dual entry, not actual login endpoints, a CORS contract or permission to replace configured MPMM entry. |
| **ASR-07** | `R:37` is supported by the complete body and all chunks: no token/header examples, `/me` DTO, refresh protocol, 401/403 handling, permission-string matrix, cache-invalidation or CORS contract is supplied. These are body-local omissions, not backend-absence findings. The User Story expander is empty (`C:3`); the use-case expanders and terminal template/approval sections are empty (`C:9–10`, `S:193–212`). “Smoke: да” is not execution or acceptance evidence. |

### Finding: P2 — preserve exact row-level qualifiers

**Location:** `R:34`, ASR-04.

The phrase “desired event selection/filtering, active-user/session counts, arbitrary blocking/session termination, event viewing” applies “desired” across §§19.8–19.9.3 without preserving their differing third-column entries.

Evidence:

- §§18–19: **«Желательно со стороны ППО»**, `S:165–168`, `C:7`.
- §19.8: **«Желательно Со стороны ППО»**, `S:183–184`, spanning `C:8–9`.
- §§19.9–19.9.3: **«Со стороны ППО»**, without their own “Желательно”, `S:185–192`, `C:9`; §19.9 says the capabilities **«должны быть доступны»**.

**Smallest mandatory correction:** replace that portion of ASR-04 with:

> §19.8 marks event selection/filtering “Желательно Со стороны ППО”; §§19.9–19.9.3 require available console capabilities and mark active-user/session counts, arbitrary blocking/session termination and event viewing “Со стороны ППО”, without repeating “Желательно”. The parent console/settings rows §§18–19 are marked desirable.

Do not resolve this parent/child qualification by declaring new current obligations or importing these capabilities into the SPA.

### Chunk ordinals and locators

`C` contains nine strings on lines **2–10**:

- Human ordinals: **1–9**.
- Zero-based JSON indexes: **0–8**.
- Ordinal *n* is on line *n + 1* and has JSON index *n − 1*.

The report’s candidate chunk references consistently use human ordinals and match their cited physical lines. **No actual off-by-one source selection was found.**

`R:17` says “array entries 1–9”, not “JSON indexes 1–9”; this is defensible ordinal wording. A small clarity improvement is:

> nine ordered chunks, ordinal entries 1–9 (zero-based JSON indexes 0–8), on lines 2–10; all subsequent chunk numbers are ordinals.

This is clarification, not evidence that a tenth element exists or a chunk was skipped.

### Correct: approved boundaries retained

The report preserves the approved contracts:

- Configuration selects real mode; credential-destination validation is a separate boundary.
- Validated `/me` precedes business access.
- Exact action/resource/`*` controls UI; roles and assignment scopes do not grant frontend object authorization.
- Backend authorization remains authoritative; no frontend method/path ACL or synthetic permission 403.
- Shared refresh, distinct 401/403/temporary-error handling, no automatic replay, same-user draft/operation preservation and generation-based stale-data isolation remain.
- No own login/OIDC, global logout, role editor, cross-origin token bridge or newly approved auth model.
- Existing deployment/session availability, CORS, rotation, `/me` and server-enforcement gates remain unverified rather than waived.

No dedicated `add-local-session-demo` comparison was performed or implied.

### Limits and verdict

- **Fixed:** none; read-only review.
- Hashes, character counts and exact concatenation roundtrip were **not independently recomputed**. Metadata assertions remain parent-attributed.
- No source rendering/execution, network/browser access, credential/storage access, auth/business requests, code audit, tests/build/E2E or nested delegation.
- No Git index/staging inspection or attestation.
- No chronology precedence, regulatory applicability determination, runtime verification or global closure. Global **6/28** remains unchanged.

**Merge verdict: BLOCK documentary acceptance pending the single ASR-04 wording correction; no policy or runtime change requested.**