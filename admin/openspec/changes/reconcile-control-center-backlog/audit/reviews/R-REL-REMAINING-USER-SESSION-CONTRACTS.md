# R-REL-REMAINING-USER-SESSION-CONTRACTS

## Review

**Decision: REVISE — one narrow mandatory correction to the proposed sufficiency criterion.**

Aliases:
- **C** = `openspec/changes/reconcile-control-center-backlog`
- **A** = `C/audit`
- **R** = `A/reports/REL-REMAINING-USER-SESSION-CONTRACTS.md`
- **H** = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`
- **D** = `openspec/changes/archive/2026-10-09-add-local-session-demo`

### Correct

- **Necessity versus relevance:** R:5 correctly says neither candidate is established as mandatory and expressly avoids declaring irrelevance, redundancy, obsolescence or inaccessibility. That bounded conclusion is supported by the accepted ledger, not by inspection of unseen bodies.
- **Exact references:** R:13–14 correctly reuse:
  - user **238347672 / MOS-944** → `A/sources/jira-details-MOS-774/r1/content.json#/items/5/description`;
  - session **241079770 / MOS-904** → `A/sources/jira-shell-details/r1/content.json#/items/4/description`.
  
  These match `G1-JIRA-CONTRACT-COLLECTION-DELTA` report:26–42 and review:18–36. Historical **238329164** is not a replacement for **241079770**.
- **Policy distinctions:** Approved `/me` identity does not substitute for business-user administration or membership/contact records. Approved frontend policy cannot establish unseen document content. The report explicitly preserves these distinctions.
- **Safety boundaries:** Configuration-selected mock/real mode remains separate from credential destinations. Exact UI permissions do not grant backend object access, including for `*`. No role-name grants, transport ACL, synthetic permission403, own OIDC, global logout, role editor or automatic mutation replay is introduced. Demo fixtures remain credential-free and separate from business-user records.
- **Acceptance lineage:** R:34 correctly preserves the original historical-auth **REVISE**, D-042’s parent-applied ASR-04 qualifier correction and parent acceptance. The separate access-role review remains **ACCEPT**.
- **Authority and closure:** No collection, runtime verification or automatic task closure is authorized. D-053’s later shell captures do not establish either remaining candidate’s necessity or content.

### Finding: P1 — proposed decision test narrows task2.4 beyond its contract

**Location:** R:13–16, particularly the suggested parent question and its “Otherwise … nonmandatory exclusions” branch.

**Evidence:** `C/tasks.md:13` requires the published API snapshot and **available explanatory documents**. It does not restrict those explanations to unresolved business-user wire questions or discrepancies in the approved session integration. `C/design.md`, sections 1 and 5, includes relevant material from allowed tasks and distinguishes agreed product scope from documentary requirements/conflicts. D-045 expressly leaves broader explanatory sufficiency unresolved.

The report’s general caveats are sound, but its actionable test is narrower:

- user necessity is framed around a wire explanation and operation/field/error;
- session applicability is framed around the approved MPMM integration and a specific discrepancy;
- absent those particular questions, the suggested disposition recommends exclusion for sufficiency.

A relevant document could explain historical requirements, applicability, ownership or provenance without exposing a previously identified wire gap or contradicting approved policy. Such evidence would not authorize implementation of those historical ambitions. Conversely, settled frontend policy does not itself establish documentary sufficiency.

**Smallest mandatory correction:**

Broaden the two applicability questions and R:16’s conditional disposition to cover **a concrete in-scope explanatory need**, including historical requirement/applicability, ownership or provenance clarification—not only wire gaps or approved-session discrepancies. Make wire questions and discrepancies examples rather than exclusive conditions.

State that failure to identify those particular gaps leaves necessity **unestablished**; it does not alone justify exclusion. Any nonmandatory deferral/exclusion remains the parent’s explicit bounded documentary-sufficiency judgment, with its rationale and uncertainty recorded.

Retain the existing prohibition on reopening approved policy or implementing historical extensions. **No mandatory fetch, all-documents prerequisite or report rewrite is requested.**

### Fixed

None. Read-only review.

### Merge verdict

**BLOCK documentary acceptance pending this wording correction.** The exact-reference findings, policy safeguards and conditional nature of the recommendation otherwise stand.

## Inspection completed

Read completely, before auth/demo assessment:

- C proposal, design, reconciliation specification and tasks.
- H proposal, design and all six specifications: `mpmm-session`, `control-center-http`, `control-center-permissions`, `control-center-api-integration`, `control-center-shell`, `control-center-mock-server`.
- D proposal, design and all three specifications: `local-session-demo`, `control-center-shell`, `control-center-mock-server`.

Also read completely:

- Assigned reviewer work item, analyst assignment and target report.
- Reports and reviews for `G1-JIRA-CONTRACT-COLLECTION-DELTA`, `G1-API-COLLECTION-DELTA`, `DELTA-AUTH-SESSION-ROOT-DOC`, `DELTA-ACCESS-ROLES-ROOT-DOCS`.
- Relevant complete decision entries D-051–053, D-045 and D-042 at `A/decisions.md:3–21,59–63,81–85`.

Compared candidate locators against the accepted carrying ledger; checked the actual task2.4 wording and approved prerequisite contracts. Historical source findings remain attributed to their accepted reports/reviews rather than independently renewed.

## Actual limits

Only local reads and a scoped report-locator search were used. No candidate bodies, primary Jira packets, source graph, application code or API schemas were inspected; no absence census or semantic audit was repeated.

No browser/network, credentials/storage access, requests/downloads, execution, tests/build/E2E, nested delegation or repository edits occurred. Hashes, acquisition safeguards, external freshness and runtime behavior were not verified. No staging inspection or attestation.

**Global6/28 and tasks2.3/2.4/2.6 remain unchanged.** This review neither resolves the candidates’ necessity nor grants acquisition authority or global closure.