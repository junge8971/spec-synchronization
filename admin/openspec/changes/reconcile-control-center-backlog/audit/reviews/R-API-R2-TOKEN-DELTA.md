# R-API-R2-TOKEN-DELTA — Independent review

## Review

- **Correct:** All six candidates distinguish newly published DTOs/commands from agreed business behavior, runtime verification and permission to implement. Existing MOS-1023 ownership and gates remain intact.
- **Fixed:** None; read-only review.
- **Findings:** No issues found.
- **Merge verdict: OK** for accepting these bounded documentation-update candidates only. No implementation, task closure or sandbox activation is authorized.

## Evidence and verification limits

`A` = `openspec/changes/reconcile-control-center-backlog/audit`.

Read completely:

- Assigned review work item, `A/work-items/API-R2-TOKEN-DELTA.md`, and `A/reports/API-R2-TOKEN-DELTA.md`.
- Both `A/sources/api-token-status-readable/{r1,r2}/content.json` files and metadata: selected operations, all included recursively reachable schemas, shared skill DTO and security definitions.
- Original `api-live/{r1,r2}/metadata.json`, plus `api-docs/r1/content.html` and metadata.
- Existing `mos-1023-skill-environment-tokens` proposal, design, tasks, capability spec and `.openspec.yaml`.
- Main `skill-connection-settings/spec.md`; relevant readiness and sandbox-exclusion sections.
- Prior REQ-MOS-1023/RECON-MOS-1023 and SCENARIO-MOS-962/R-SCENARIO-MOS-962 reports; D-012 at `A/decisions.md:93–103`.

The derived files explicitly preserve selected original JSON values, not the complete OpenAPI document. **Source/derived hashes and parsed-value roundtrip equality were computed by the parent, as recorded in metadata; I did not independently recompute them.** Original publication metadata records r1 retrieval on 2026-10-16 and r2 on 2026-10-19. The later Swagger discovery receipt does not retroactively verify r1 acquisition.

The selected r1 operations explicitly list both token paths as absent; r2 contains both. Six token schemas are newly present in the selected reachable set. The report’s whole-document inventory and ordinary GET linkage are supported by its original-source analysis, not independently re-extracted from full original JSON in this review. Directly inspected revoke linkage independently establishes the ordinary shared DTO’s secret-bearing potential.

## Per-candidate verdicts

| Candidate | Verdict | Independent evidence and retained limits |
|---|---|---|
| **API-R2-TOKEN-01** | **ACCEPT** | r1 derived `/absentPaths` lists reissue and revoke; r2 `/operations` publishes both POST definitions. Six token schemas appear in r2 `/references`. This corrects reuse of r1 absence as current publication inventory, not absence of agreement or deployment proof. MOS-1023 `proposal.md:21–27` expressly references the **local** `docs/api/contracts/openapi.json`; remote publication does not disprove that local-file claim. No task check-off or regeneration follows. |
| **API-R2-TOKEN-02** | **ACCEPT** | r2 token-operation parameters require path UUID7 `skill_id`, environment reference and UUID `Idempotency-Key`; JSON body references `SkillTokenMutationRequest`. Its sole declared property is required integer `expected_version >= 1` (`r2/content.json:1032–1045`). Environment enum is exactly sandbox/whitelist/prod (`:795–803`). These are shapes, not scopes, state-selection rules, version-increment semantics or replay guarantees. No request secret property or explicit additional-property rejection is declared. |
| **API-R2-TOKEN-03** | **ACCEPT** | `SkillTokenResponse` requires all seven fields, including nullable `revoked_at` and nullable `token_value` (`r2/content.json:1046–1104`). The shared namespaced skills DTO requires `tokens`; r1 lacks that property. Empty arrays are schema-valid, but history completeness and an explicit never-issued interpretation are not defined. Null value, inactive record and absent environment likewise do not establish “не выдан”. No expiry, scope or active-record uniqueness rule is supplied by these definitions. |
| **API-R2-TOKEN-04** | **ACCEPT** | `SkillTokenIssuanceResponse.issued_token` is required but nullable (`r2/content.json:987–1029`). Non-null `IssuedSkillTokenResponse.token_value` is a string without nonempty, masking or one-time-disclosure constraints (`:323–374`). Ordinary `tokens[].token_value` also permits strings. Clearing only `issued_token` therefore cannot classify the remaining response as metadata-safe. Actual disclosure, cache contamination or leakage is **not** proven by DTO definitions. |
| **API-R2-TOKEN-05** | **ACCEPT** | Reissue returns the issuance envelope; revoke returns `TsamResponseSchema_SkillResponse_`, whose data points to the namespaced skills DTO. Both declare only 200 and 422 responses and provide success-message extensions, without operation descriptions defining invalidation consequences. No explicit atomic replacement, overlap, propagation, already-revoked behavior or authoritative old-token invalidation guarantee is present. This preserves MOS-1023 task 1.1 and accepted SCENARIO-MOS-962-03 rather than duplicating them. |
| **API-R2-TOKEN-06** | **ACCEPT** | MOS-1023 `design.md:13–17`, tasks 2.1–2.4 and **Secret-safe sandbox integration** retain one shared business model, controlled secret handling and skill-ID-only navigation. Main `skill-checks-training/spec.md:63–70` forbids status-only readiness; `surface-lifecycle-publication/spec.md:65–68` excludes sandbox launch. Shared response publication changes integration considerations, not those boundaries. Status-response mapping remains the separate lane’s responsibility. |

## Mandatory corrections and preservation rules

**No additional correction to the reviewed report is required.** Its following qualifications must survive any later authorized documentation update:

1. **Publication versus agreement:** Replace only present-tense blanket absence claims. Preserve historical r1 evidence and unresolved task-1.1 business/security decisions.
2. **Local versus remote contract:** Annotate the dated r2 publication separately; do not mark the proposal’s local-contract assertion false without inspecting that file.
3. **Potential secrets:** Treat both `issued_token.token_value` and ordinary `tokens[].token_value` as potentially secret-bearing. The latter is not automatically safe for ordinary metadata caching merely because the former is cleared. Preserve temporary-state, cleanup, storage and diagnostic restrictions.
4. **Schema-valid versus guaranteed:** Nullable issuance, empty lists, inactive records and unconstrained string values are permitted shapes—not promises about actual runtime outcomes or UI state mappings.
5. **Revocation and recovery:** Keep atomicity, affected prior token, propagation/overlap, confirmation, partial/lost response and audit responsibility unresolved. Do not synthesize revoke-then-reissue or automatic retry after timeout.
6. **Errors and replay:** Required idempotency input does not establish retention, key scope, repeat-secret delivery or unknown-outcome reconciliation. Token operations explicitly declare 200/422 only; do not import status-operation 409 codes or recovery behavior. Open error fields do not prove leakage.
7. **Authorization boundaries:** Published security declarations do not supply token-operation permission names or authorize new transport behavior. Preserve existing agreed transport constraints. D-012’s recorded historical approval remains distinct from sandbox approval and deployment verification.
8. **Existing owner:** Retain `mos-1023-skill-environment-tokens`, all unchecked tasks, independent acceptance and surface MVP exclusion. Prior RECON recommendations remain recommendations, not silently adopted requirements.

## Remaining gates

Within the existing owner: initial issuance trigger; current-state/environment selection; explicit unissued mapping; history completeness; scopes/lifetime; reveal/copy authorization and repeat disclosure; permission-name mapping; version/concurrency behavior; replay retention and secret replay; authoritative revocation evidence; audit/redaction; sandbox target identity and readiness.

These are unresolved owner decisions, not missing inputs blocking this review.

## Validation

Local file reads and targeted file discovery/search only. No edits, shell commands, tests/builds, network/browser/MCP, actual tokens, business-operation execution, code generation, nested delegation, git mutations, sync or archive. No implementation-compliance, deployment or index-state attestation.