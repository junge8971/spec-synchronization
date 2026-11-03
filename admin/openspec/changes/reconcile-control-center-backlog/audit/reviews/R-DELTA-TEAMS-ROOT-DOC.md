# R-DELTA-TEAMS-ROOT-DOC — independent documentary review

## Review

**Decision: REVISE — one locator correction only.** All eight candidates are substantively supported. No change to their business conclusions, owner-question routing or evidence boundaries is required.

- **Correct:** The report distinguishes source requirements from implementation, storage proposals from wire contracts, business membership from authenticated principal, and observed issue membership from detailed ownership or delivery.
- **Fixed:** None; review was read-only.
- **Finding: P2 — incorrect exact line locator.** `audit/reports/DELTA-TEAMS-ROOT-DOC.md:29`, TEAMS-ROOT-04, cites “Общие элементы” #9 as `S 220`. In `sources/wiki-247728705-readable/r1/content.txt`, line **220 is #8**, describing Next-button placement; line **221 is #9**, requiring current-step validation.
  - **Exact minimal mandatory fix:** Replace `“Общие элементы” #9, S 220` with `“Общие элементы” #9, S 221`.
  - This is documentary precision only; the validation ambiguity remains supported.
- **Merge verdict: OK with notes.** Documentary acceptance awaits that single correction; no substantive blocker identified.

## Verification performed

`A` = `openspec/changes/reconcile-control-center-backlog/audit`; `S` = `A/sources/wiki-247728705-readable/r1/content.txt`.

Read completely:

- Assigned review work-item and analyst work-item, including supervisor clarification.
- `A/reports/DELTA-TEAMS-ROOT-DOC.md` and `A/reports/JIRA-MOS-768.md`.
- Wiki 247728705 version 9 readable body, S 1–302, both metadata files, and all 19 ordered HTML chunks, array entries 0–18. Chunks were read as inert text, without rendering or execution.
- Approved `2026-10-09-integrate-mpmm-auth-permissions` proposal, design and all six specs.
- Approved `2026-10-09-add-local-session-demo` proposal, design and all three specs.

Auth/demo prerequisites were read before evaluating permission and demo comparisons.

### All-eight disposition

| Candidate | Result and verified evidence |
|---|---|
| **TEAMS-ROOT-01** | **ACCEPT.** S 179–209 supports card fields, membership ordering, domain/surface display and summary counts; S 284–302 supports proposed storage fields. Organization/department mapping remains a question, not an inferred DTO. Surface/skill labels are correctly not promoted to team lifecycle states. |
| **TEAMS-ROOT-02** | **ACCEPT.** S 4, 236, 243, 270–272 and 300–302 support owner/editor/view versus lead/member, selected/default versus employee-derived role, and SUDIR versus Control Center user selection. The report requests clarification without asserting these directories are necessarily distinct systems or coercing identities. |
| **TEAMS-ROOT-03** | **ACCEPT.** S 98–101, step 3 #5–6 at 250–251 and step 4 #2 at 255 establish domain-gating versus mandatory surface/surface-only ambiguity. S 64–67 and 198 concern existing empty-domain display, not permission to create without domains. No precedence is selected. |
| **TEAMS-ROOT-04** | **REVISE locator only.** Correct #9 to S 221. S 228–229, 239–242, 259 and 275 otherwise support the finding. Exactly one lead remains scoped to creation. Email uniqueness and the composite team_id/user_id key at S 296–297 are not assumed equivalent. Final atomic validation is an owner question, not an invented source guarantee. |
| **TEAMS-ROOT-05** | **ACCEPT.** S 114–123, 222–223, 149–160 and 276–282 support create/add outcomes, warning, cancellation and member-add audit intent. Timestamps at 288–290 and 299 do not establish concurrency controls or edit/delete/restore endpoints. The complete body supplies no explicit version/ETag, idempotency, retry or concurrent-add resolution rule; this remains a body-specific limit. |
| **TEAMS-ROOT-06** | **ACCEPT.** S 25–45, 167, 172–175 and 265 support the business role prose. Approved auth **Exact permission matching**, **Explicit feature policy**, **Server owned resource scope** and shell **URL-driven section tabs** support exact Team permissions, explicit wildcard audit access and backend-owned data scope. Role labels cannot grant manage-members UI or global data access. |
| **TEAMS-ROOT-07** | **ACCEPT.** S 168/175 is appropriately compared with approved auth switching exclusions and demo fixed-profile/panel/reload requirements. Approved demo **Business users are not session principals** supports separating contacts/members from principal. No production switching or new mock implementation lane is authorized. |
| **TEAMS-ROOT-08** | **ACCEPT.** S 20–23 versus 165/171, S 114 versus 257–258, and S 254 versus 226–229 substantiate naming, save-label and purpose-field inconsistencies. The report does not invent a purpose field or missing frontend implementation. |

Broader cited ranges include their supporting cells; the isolated #9 line mismatch above is the required correction.

## Membership and owner-evidence boundary

Targeted saved records agree with JIRA-MOS-768:

- `sources/jira-hierarchy/r1/content.json:11`, `/results/3/children/0–3`, lists MOS-836, MOS-931, MOS-1032 and MOS-1033 under MOS-768.
- `sources/jira-member-index/r1/content.json:316–347` confirms the four summaries and snapshot statuses: backend teams/users **Ready for test**, frontend overview/creation-membership **Backlog**.

These support routing questions to existing observed scopes, not detailed acceptance ownership or completion. The report correctly preserves that limitation.

The supervisor’s ignore-independent exact-key search remains **attributed bounded evidence**. It was not rerun, and no new full census was undertaken. Neither that search nor these records establishes global absence, absence of unkeyed plans, missing frontend ownership, completed implementation or current backend/API absence. Detailed issue acceptance and contract/implementation comparison remain unavailable in this review.

## Verified limits

- Metadata confirms the recorded version and collection/update timestamps; hashes and chunk roundtrip were **not independently recomputed**.
- Original `content.json` and the separately returned attachment index were not independently inspected. Empty-index claims remain parent-attributed, not global attachment-absence evidence.
- No linked resources, attachments, application code, live contracts or runtime behavior were inspected.
- No browser/network, source execution, business calls, credentials, tests/build, nested delegation or repository edits occurred. Staging state was not inspected or attested.
- No source precedence, identity coercion, grants, new plan or auth/demo policy reopening is proposed.
- Global **6/28** and historical approvals remain unchanged.