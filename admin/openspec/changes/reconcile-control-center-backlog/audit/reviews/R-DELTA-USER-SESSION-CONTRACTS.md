# R-DELTA-USER-SESSION-CONTRACTS

## Review

**Disposition: REVISE — two narrow documentary corrections.**

- **Correct:** All 18 findings preserve the distinction between historical requirements, draft proposals and approved frontend policy. No implementation or runtime acceptance follows.
- **Fixed:** None; read-only review.
- **Merge verdict: BLOCK documentary acceptance pending the two corrections below.** No policy changes or further collection requested.

## Findings and exact minimal corrections

Aliases:

- **A** = `openspec/changes/reconcile-control-center-backlog/audit`
- **R** = `A/reports/DELTA-USER-SESSION-CONTRACTS.md`
- **U/S** = `A/sources/wiki-{238347672,241079770}-readable/r1/content.txt`, respectively.
- **UC/SC** = corresponding `body-view-chunks.json`.
- **UP/SP** = corresponding `envelope-index-projection.json`.
- **H** = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`
- **D** = `openspec/changes/archive/2026-10-09-add-local-session-demo`

Chunk numbers below are **zero-based JSON indexes**; physical line = index + 2.

### Finding: P2 — restore the audit action namespace

**Location:** R:69, SES-10, “Proposed six actions”.

The report lists `authentication.succeeded/failed` and `session.logged_out/revoked/terminated/expired` without identifying these as abbreviations. The source’s actual proposed values all include the `access.` system namespace. This matters in a column labelled “Exact newly saved claim”.

**Evidence:** S:346–353; SC:16–17, especially SC:17’s action table. The source expressly defines `<система>.<объект>.<действие>`.

**Smallest mandatory correction:** replace that list with:

> Proposed six actions: `access.authentication.succeeded`, `access.authentication.failed`, `access.session.logged_out`, `access.session.revoked`, `access.session.terminated`, `access.session.expired`.

Retain their proposed/catalog-owner-confirmation status.

### Finding: P2 — add the locator supporting transport-derived source identity

**Location:** R:70, SES-11.

The statement “source_service from transport identity” is correct, but its cited S:411–445 / SC:18–21 does not contain that derivation rule. S:413 defines the composite idempotency key; S:358 / SC:18 discusses transport-level credentials and absence of `source_service` from the body, not derivation from caller identity.

**Evidence:** The explicit rule is at **S:344 / SC:16**; it is also repeated at S:240 / SC:9. SES-10 already cites the relevant broader source region, but SES-11’s own locator does not.

**Smallest mandatory correction:** change SES-11’s citations to:

> S **344,411–445**; SC **16,18–21**

No prose change is required.

## Complete inspection coverage

Read the complete reviewer assignment, analyst assignment and target report.

Before source assessment, read completely:

- H `proposal.md`, `design.md`, and all six specifications: `mpmm-session`, `control-center-http`, `control-center-permissions`, `control-center-api-integration`, `control-center-shell`, `control-center-mock-server`.
- D `proposal.md`, `design.md`, and all three specifications: `local-session-demo`, `control-center-shell`, `control-center-mock-server`.

Independently inspected:

- U:1–313 and **all seven UC chunks, indexes 0–6**.
- S:1–445 and **all 22 SC chunks, indexes 0–21**. Text read in windows 1–220 and 221–EOF; chunks in physical-line windows 1–7, 8–13, 14–19 and 20–EOF.
- Complete user canonical `A/sources/wiki-238347672/r1/content.json`, including body and returned attachment index.
- Both complete canonical metadata files and both complete readable metadata files.
- Complete UP and SP, including every non-body field and every attachment link value.

The session canonical file was **not independently read or parsed in full**. Its body was inspected through all ordered exact chunks, with its full non-body fields represented by SP. Parsing, canonical equality, hashes and chunk roundtrip remain **parent-attributed**, not independently recomputed.

Also read completely the reports/reviews for:

- `DELTA-AUTH-SESSION-ROOT-DOC`
- `DELTA-ACCESS-ROLES-ROOT-DOCS`
- corrected `REL-REMAINING-USER-SESSION-CONTRACTS` and its original review.

Read complete decision entries D-055/D-054 at A/decisions.md:3–9 and D-042 at :91–93. Prior source bodies and Jira packets were not re-audited.

## Verification of all 18 findings

| Finding | Verification |
|---|---|
| **USR-01** | U:6–7,27–37,119–139; UC:0,2–3 support cookie-authenticated administrative profiles, local UUID/subject, nullable fields, role codes and administrative state. Correctly distinct from approved `/me`, contacts and team membership. |
| **USR-02** | U:35–71,108–139,167–181; UC:0–3 support prefix search, any-of roles, date boundaries, stable sorting, pagination and card behavior. Empty success is not missing/concealed access. No deployment inference. |
| **USR-03** | U:58–68,127; UC:1,3 contain exactly **nine preliminary role codes**, with empty assignments allowed. No hierarchy or production grants are inferred; fixed demo profiles remain separate. |
| **USR-04** | U:182–215; UC:3–4 support `users.activate`, pending/suspended→active, required UUID key, positive int64 version, reason length and new-login requirement. |
| **USR-05** | U:216–247; UC:4–5 support `users.block`, active→suspended and invalidation of application sessions—not global СУДИР blocking or token changes. |
| **USR-06** | U:248–287; UC:5 preserve version increment, original status/body replay for identical commands, method/URI/body key conflicts and explicit prohibition of automatic retry after version conflict. |
| **USR-07** | U:8–26,33,288–310; UC:0,5–6 support correlation, error-envelope details, concealed404, inactive403 and authorization503. Audit Query API delegation does not grant reader access or frontend publication authority. |
| **SES-01** | S:1–10,33–41,421–445 confirms paused DRAFT status, unagreed frontend/provider parameters, backend cookie architecture and MOS-659’s contract-only scope. No replacement of approved MPMM integration follows. |
| **SES-02** | S:43–80; SC:2–3 preserve proposed302, normalized same-origin return path, transaction/browser binding, PKCE and proposed600-second duration. Example addresses are not registered endpoints. |
| **SES-03** | S:81–128; SC:3–5 support callback validation, atomic transaction consumption, OIDC identity assurance, active-profile checks and successful-browser-session replacement. Failed callback does not revoke an existing valid session. |
| **SES-04** | S:129–187,295–313; SC:5–7,13–14 support current-session fields, nullable absolute expiry, backend checks and separation of functional permissions, provider scopes and object authorization. No DTO conversion is authorized. |
| **SES-05** | S:18–32,188–201,244–273 preserve redirect-versus-JSON errors, configuration503, invalid-session401 and proposed inactive-profile403 cleanup. The report expressly prevents importing that cleanup into approved generic business403. |
| **SES-06** | S:202–243; SC:8–9 preserve own-session logout, validation/CSRF without cookie, null redirect, no fabricated audit event, store-outage behavior and unresolved key applicability. No frontend logout or automatic replay is approved. |
| **SES-07** | S:274–293; SC:11–12 support proposed cookie attributes, distinct Lax binding cookie, exact Origin/Referer rules and unresolved CORS/CSRF decisions. Browser close is not reliable logout. |
| **SES-08** | S:170,187,314–321,440 support illustrative15 minutes, preliminary15–60-minute range, unresolved defaults/activity/absolute limits and locally recorded unlimited parallel sessions. No chronology precedence or adopted timeout is asserted. |
| **SES-09** | S:295–334; SC:12–16 support secret/public-ID separation, conditional activity, concurrent mass revocation, index limitations, restart/eviction and unconfirmed external propagation. Backend requirements are not delivered SPA capabilities. |
| **SES-10** | S:109–110,215–236,335–354,409–420 support source-owned synchronous fail-open audit publication, alerts/retries, proposed catalog and observed-expiry limitation. Correct except the action-name abbreviation identified above. |
| **SES-11** | S:411–445 supports publication idempotency/conflicts, preserved auth outcome, no exactly-once guarantee and provider TBDs. Transport-derived identity is also correct but needs the additional locator above. Backend audit retry remains distinct from frontend replay. |

## Provenance, lineage and attachment boundaries

Verified saved identity:

- User **238347672**, page **v8**, captured `2026-10-19T14:43:52.961Z`.
- Session **241079770**, page **v2**, captured `2026-10-19T14:43:53.276Z`.
- Both saved envelopes report HTTP200 and zero redactions. Page versions remain distinct from body contract versions.
- Carrying references remain attributed to MOS-944/MOS-904; packet filenames and links do not assign implementation ownership.

D-042 accepts the parent-corrected ASR findings while preserving the original independent **REVISE**. ACCESS has its separate **ACCEPT**. D-054 preserves the original necessity-review **REVISE** and accepts the parent correction. D-055 grants documentary inclusion only—not applicability, owner, runtime or policy acceptance.

UP records an empty returned attachment index. SP records exactly four `image/png` entries:

| ID | Exact title |
|---|---|
| 241079265 | image-2026-9-7_16-29-13-1.png |
| 241079264 | image-2026-9-7_16-29-13.png |
| 241078912 | image-2026-9-7_16-9-47-1.png |
| 241078911 | image-2026-9-7_16-9-47.png |

Both indexes report status200, start0, limit100 and next null. SC:16 contains the two stated login/logout image references with empty `alt` values. No Mermaid diagram body or image semantics were recovered from those references.

**All four PNG bodies remain unread.** No attachment bytes or thumbnails were accessed or rendered. This local inventory is not summed with root39/Jira23, and no root42 members are added.

## Limits and retained policy

The report correctly retains configuration-selected mock/real mode, separate credential-destination safety, validated `/me`, exact UI permissions and backend object scopes even with `*`. It introduces no role-name grants, frontend request ACL, synthetic403, own OIDC, role editor, logout capability or automatic replay.

Historical explanatory value is not restricted to known wire conflicts. This review does not establish all-document sufficiency, task2.4 closure, deployed API availability or missing implementation.

Only local documentary reads/discovery and scoped locator searches were used. No report edits, browser/network access, credentials/storage inspection, downloads, rendering, code/API graph traversal, source execution, tests/build/E2E, nested delegation or staging inspection occurred. No executable checks were run because they are outside this assignment.

**Global6/28 remains unchanged.** Runtime, reader-access, common-session placement, CORS, refresh rotation, `/me` and backend-enforcement gates remain unverified.