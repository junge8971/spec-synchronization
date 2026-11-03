# R-API-R2-STATUS-DELTA — independent review

## Review

**Verdict: ACCEPT — STATUS-01–04 as bounded documentary evidence.**

- **Correct:** Response linkage, requiredness/nullability, preserved command semantics and targeted historical-claim qualifications agree with the inspected primary-derived values.
- **Correct:** D-020’s explicit three-command restoration scope remains intact.
- **Fixed:** None; read-only review.
- **Findings:** No issues found.
- **Mandatory corrections:** None.
- **Merge verdict:** OK with notes — documentary acceptance only, subject to the coverage limits below.

## Evidence inspected

**A** = `openspec/changes/reconcile-control-center-backlog/audit`.

Read:

- Complete assigned reviewer and analyst work-items and `A/reports/API-R2-STATUS-DELTA.md`.
- Complete `A/sources/api-token-status-readable/r1/content.json` and `r2/content.json`, including every supplied transitive reference and security definition; both adjacent metadata files.
- Original `api-live/r1` and `r2` metadata and complete `api-docs/r1` HTML/metadata.
- D-015–D-021 in `A/decisions.md:11–67`.
- Cited claim ranges of SCENARIO-MOS-909 and IMPL-MOS-909; complete DELTA-MOS-1119 and DELTA-MOS-1119-TESTPLAN reports.
- Complete five cited reviews: R-SCENARIO-MOS-909, R-IMPL-MOS-909, R-DELTA-MOS-1119, R-DELTA-MOS-1119-TESTPLAN and R-WRITE-MOS-909-RESTORE.
- Complete restoration proposal, design, tasks and lifecycle delta under `openspec/changes/mos-909-restore-approved-lifecycle-actions/`.

## Exact response-contract verification

Pointers below refer to original OpenAPI locations preserved in the readable extracts.

**OP** = `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`  
**S** = `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`  
**I** = `/components/schemas/SkillTokenIssuanceResponse`

| ID | Independent disposition |
|---|---|
| **STATUS-01** | **ACCEPT.** OP `/responses/200/content/application~1json/schema/$ref` changes from `#/components/schemas/TsamResponseSchema_SkillResponse_` to `#/components/schemas/TsamResponseSchema_SkillTokenIssuanceResponse_`. The old envelope still resolves to S; the new envelope resolves to I. Both require code/data/message and retain optional ErrorItem-array errors. |
| **STATUS-02** | **ACCEPT.** S adds `tokens`, an array referencing SkillTokenResponse, and inserts it at required index 18. The previous 27 required members remain, giving 28. No null branch, default or minimum count is supplied: empty array is permitted, omission/null is not. Other card properties are preserved. |
| **STATUS-03** | **ACCEPT.** I reproduces all 28 S properties and adds `issued_token`, required at index 28, with `IssuedSkillTokenResponse` or null. This is a card response, not token-only data. SkillTokenResponse requires all seven declared members, including nullable `token_value`; IssuedSkillTokenResponse requires non-null string `token_value`. Required issuance-field presence does not mean every transition issues a token. |
| **STATUS-04** | **ACCEPT within inspected closure.** The status operation’s remaining members and supplied pre-existing references retain their values: description, request, parameters, security, operation ID, 422 schema and success message. Readiness, queue and concurrency prose do not change. |

The unchanged request requires status and integer expected_version ≥1, optional nullable reason, required UUID Idempotency-Key and UUIDv7 skill ID. Explicit response schemas remain only 200/422; named 409 failures remain description-level mappings.

The retained prose still requires fresh applicable readiness checks, exempts the named draft/return transitions, preserves recalculated checks on readiness refusal, and distinguishes queue-busy “nothing saved.” It does not establish whole-card rollback, exactly-once delivery, replay disclosure policy, automatic retry or new frontend authority.

Checks remain a required array without a minimum/all-five structural guarantee. Process values remain unconstrained strings; ETA/note remain required-nullable strings. Neither history nor current-phrase revision binding is added.

## Prior-claim mapping

- **SCENARIO-MOS-909:41–44 and R-SCENARIO-MOS-909:67–75 / D-018:** The old status-response chain is historical-valid but stale when reused as r2 linkage. C05’s checks/process-metadata conclusions survive because those properties remain in I. No whole-report invalidation is warranted.
- **DELTA-MOS-1119-TESTPLAN:39 and its review:61–65 / D-017:** The same narrow linkage qualification is necessary. Skill-card updated_at remains distinct from dictionary columns; readiness, optional reason, error-schema and persisted-check qualifications remain supported.
- **MOS1119-TP06, report:75–79 and review:51:** Replay equality remains an expectation, not demonstrated behavior. Applying it to r2 must account for tokens, nullable issued_token and its non-null branch; unchanged status prose supplies no disclosure/redaction rule.
- **DELTA-MOS-1119 D01–D06 / D-016:** Storage, nullable history, immutability, reader and restoration questions are not invalidated by these response changes. Historical unread-body statements must remain dated rather than treated as current inventory.
- **IMPL909-05/06/10 and R-IMPL-MOS-909:29–34 / D-019:** Historical validator/cache observations are not current r2 compatibility or safe-token-handling certification. A separately authorized response-validation/cache-consumer inspection is justified; neither a guaranteed break nor safe retention follows.
- **Corrected IMPL909-07 and its review:36–46:** The unchanged published 409 SKILL_CHECKS_BLOCKED mapping preserves the previously identified conflict-reread path. No missing-readiness-reread remediation follows. Historical reviewer REVISE and parent-qualified acceptance remain distinct.
- **D-015:** Dedicated toggle/auth approvals and restoration questions remain outside this delta’s authority. The report correctly avoids claiming whole-toggle-response freshness.

## D-020 scope preservation

`A/decisions.md:19–23` explicitly approves planning to retain only:

- draft → checking
- sandbox → review
- whitelist → prod

The restoration proposal’s Impact, design Decisions 1–5, tasks 1.1–3.2 and lifecycle delta retain that boundary, remove precisely four extra generic actions, and preserve separate review/toggle/shared transport ownership.

All six implementation tasks remain unchecked. The two-file matrix/regression plan remains coherent; its “no shared API/DTO changes needed” statement concerns that narrow correction, not certification of all r2 response consumers. New response fields do not automatically expand, revoke or reopen this approval.

## Provenance and coverage limits

Original metadata and supplied parent verification consistently identify:

- r1: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`, captured `2026-10-16T11:13:29.451Z`.
- r2: `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993`, captured `2026-10-19T08:11:44.238Z`.

**This reviewer did not recompute hashes or parsed-value roundtrip equality.** Those checks remain attributed to the parent/author. The readable packets are local selected-value derivations, not new publications.

The saved HTML literally supplies `/api/control/openapi.json`; its receipt supports r2 discovery, not retroactive r1 acquisition proof or deployment equivalence.

**Whole-publication uniqueness and exhaustive consumer reachability were not independently re-established.** The supplied subset verifies the status and revoke response chains and shared DTO changes, but omits GET/PUT/PATCH operations and the remainder of OpenAPI. The report’s exhaustive comparison and GET/PUT/PATCH reachability therefore remain attributed analyst/parent evidence, not this reviewer’s independent attestation. Their stated transitive impact is consistent with the verified S delta.

No application code, runtime compatibility, token endpoint business policy, deployment, replay behavior or actual cache handling was independently audited. No edits, tests/builds, network/browser activity, endpoint execution, credentials access, Git operations or nested delegation occurred.

**Final disposition: ACCEPT without mandatory corrections, with these coverage qualifications.** No implementation authority, task closure, product activation, API regeneration or source precedence follows.