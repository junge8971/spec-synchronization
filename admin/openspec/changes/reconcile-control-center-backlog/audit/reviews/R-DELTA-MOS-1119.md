# R-DELTA-MOS-1119 — Independent review

## Review

**Verdict: ACCEPT — bounded supplemental documentary evidence only.**

- **Correct:** All six candidates distinguish requested backend storage from approved UI commands, published query contracts and delivered guarantees.
- **Fixed:** None; read-only review.
- **Findings:** No issues found.
- **Merge verdict:** OK with notes: acceptance applies to the documentary supplement, not implementation, product activation or task closure.

**Mandatory per-candidate corrections: none.** The qualifications below remain part of acceptance.

## Evidence inspected

Paths prefixed **A/** are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

Read completely:

- `A/work-items/R-DELTA-MOS-1119.md`
- `A/work-items/DELTA-MOS-1119.md`
- `A/reports/DELTA-MOS-1119.md`
- **L:** `A/sources/jira-lifecycle-details/r2/content.md` and adjacent `metadata.json`
- `A/sources/jira-lifecycle-details/r1/access-result.json`
- `A/decisions.md`, particularly **D-015**
- `A/reports/SCENARIO-MOS-1145.md`
- `A/reviews/R-SCENARIO-MOS-1145.md`
- **J:** `A/sources/jira-skill-switch-details/r1/content.json`, including the complete MOS-1145 description, attachment metadata and comments
- `A/reports/JIRA-MOS-782.md`, for attributed membership evidence only
- All discovered active `openspec/changes/mos-1031-skill-audit-history/` artifacts: `.openspec.yaml`, `proposal.md`, `design.md`, `tasks.md`, and `specs/skill-audit-history/spec.md`
- **S:** `openspec/specs/skill-lifecycle/spec.md`
- **T:** `openspec/specs/skill-global-toggle/spec.md`

Primary L and J evidence—not merely the author’s summary—supports the dispositions below. No fresh global API inventory or application implementation inspection was performed.

## Per-candidate disposition

| Candidate | Verdict and exact evidence | Corrections / retained boundaries |
|---|---|---|
| **MOS1119-D01** | **ACCEPT.** L:19–26 supplies the status dictionary and eight initial statuses; L:34–41 supplies the transition dictionary and nine initial edges. S:11,49 limits generic UI commands to `draft → checking`, `sandbox → review`, `whitelist → prod`, all present in those seeds. | **No correction.** Seed compatibility is not backend acceptance proof or authority for additional buttons. The remaining edges do not establish frontend caller policy. Ordered statuses do not prove completed history; retain S:30. |
| **MOS1119-D02** | **ACCEPT.** L:26,41 omits disabled from initial rows/edges; L:51–52 requires status FKs. J `/items/1/description`, “Изменение статусов навыка”, requires disabled and dedicated commands; “Хранение предыдущего статуса” delegates storage/restoration to MOS-1119 and prohibits duplicating it in `skill_disabling`. L provides old/new fields but no restoration-selection algorithm. | **No correction.** Initial-seed omission is not a prohibition of disabled or proof of deployed incompatibility. Preserve the owner question about dictionary support and restoration integration, including repeated/concurrent operations. Do not prescribe “read latest row.” T:64 preserves the approved prod → disabled → prod UI; neither revoke nor expand it. |
| **MOS1119-D03** | **ACCEPT.** L:43–55 requests transition-history persistence with skill identity. It publishes no reader operation or query protocol. MOS-1031 `design.md:13–17`, `tasks.md:3–5`, and history spec requirements retain Query API, type+ID, ordering/pagination, redaction and consistency gates. | **No correction.** Retain MOS-1031 ownership and unavailable-before-contract behavior. Neither the storage table nor a command receipt supplies the required reader. Prior publication-absence findings remain attributed to the accepted MOS-1145 packet, not newly verified here. No duplicate plan is warranted. |
| **MOS1119-D04** | **ACCEPT.** L:51,54–55 explicitly permits creation-time null old status, automatic-change null actor, and scenario-dependent nullable reason. J `/items/1/description`, “Таблица истории действий”, separately requires a reason-code FK and non-null UUID actor in `skill_disabling`. T:34–51 requires reason for both UI commands. | **No correction.** Distinct table contexts do not establish contradiction or permission to weaken UI validation. Do not UUID-constrain `actor_sso_id`, substitute the current user, invent automatic-actor labels, or treat creation NULL as an unknown-current-status fallback. Existing reason-code/free-text reconciliation remains unresolved. |
| **MOS1119-D05** | **ACCEPT.** L:13,45 requests immutable history; L:49–53 specifies UUID/time defaults and deletion-restricting FKs. J’s disable/enable scenarios separately require atomic status/history writes and prohibit an extra history row for repeated disable. | **No correction.** These are requirements, not demonstrated append-only enforcement, migration success, event completeness, ordering guarantees or deduplication. Defaults and FKs do not independently prevent history UPDATE/DELETE. Preserve the distinction between status/history atomicity and an unproven distributed audit transaction. |
| **MOS1119-D06** | **ACCEPT.** L:9,59–67 and metadata establish a newly available selected extraction, empty returned subtasks, attachment **833803**, and excerpts from both returned comments. J `/items/1/attachment/0` independently identifies attachment **835759** for MOS-1145. D-015 explicitly permits supplementation without rewriting its original evidence limits. | **No correction.** Record the narrowed description gap while preserving historical unavailable findings. Both attachment bodies remain unread. Draft MR mentions, test-plan references and Ready-for-test status do not prove execution or delivery. Custom fields, changelog and linked MR remain uninspected. |

## Provenance and integrity limits

The assignment, report and L’s metadata consistently declare:

`633abdc28221704babdf91d5cacfd7be46e1197d6fe8f3175e20e0af22caeb95`

Its stated scope is **saved UTF-8 Markdown extraction**, not original Jira response/page or attachment bytes. This correctly matches L’s explicit selected-normalized-extraction limitation. Description tables are normalized; saved comments contain selected non-personal excerpts, not complete original comment bodies.

The saved r1 access result confirms a collection timeout with no saved payload; it does not establish an HTTP failure or any remote content. The r2 supplement does not overwrite that history.

**Independent digest recomputation was not performed:** the available review tools provide file reads/searches, not byte-hash execution. The author’s reported successful hash command remains attributed evidence; this review verifies digest consistency and scope, not a fresh cryptographic attestation. Likewise, the author’s reported HEAD command is not independently re-attested.

## Preserved approvals and ownership

- **D-015 remains historically valid** for its original input set.
- **13.10.2026 toggle approval remains intact**, as explicitly recorded in T:64. It is not an integration-test result or an all-status restoration guarantee.
- **09.10.2026 auth approval remains intact** under D-015’s accepted disposition; this storage supplement neither reopens nor extends it.
- MOS-1027 retains approved toggle ownership; MOS-909/main lifecycle retains the narrow generic-command matrix; MOS-1031 retains future history-reader ownership.
- Newer collection time establishes no source precedence.
- No additional UI commands, grants, transport changes, restoration algorithm or product policy are authorized.

## Execution and final disposition

Only local discovery and document reads were performed. No direct edits, tests/builds, network/browser/MCP access, endpoint/example execution, attachment execution, Git operations or nested delegation occurred.

Implementation, deployment, runtime behavior, tests, repository index/worktree state and actual backend enforcement remain **unverified**. Attachment bodies **833803** and **835759** remain unread and distinct.

**Accept all six supplemental candidates without mandatory corrections.** This independent acceptance is evidence for parent disposition only. It closes neither MOS-1119, MOS-1031, any feature, global tasks 3.2/3.4 nor G2.