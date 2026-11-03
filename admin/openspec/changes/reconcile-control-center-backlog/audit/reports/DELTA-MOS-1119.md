# Code Context

## DELTA-MOS-1119 — supplemental storage evidence

**Result: material documentary delta; no product authorization.** The previously unavailable MOS-1119 description now supplies a requested storage model, initial dictionaries and nullable history fields. It does not resolve the restore mechanism, publish a history reader, or prove implementation. D-015 remains historically valid for its original input set. Independent review is required before accepting this supplement.

## Files Retrieved

Repository-relative paths; aliases below identify exact locators, not additional sources.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/DELTA-MOS-1119.md` (1–20): assignment boundaries.
2. **L** = `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-lifecycle-details/r2/content.md` (1–67); adjacent `metadata.json` (1–16): complete selected extraction/provenance.
3. `openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-782.md` (1–67): membership only. MOS-1119 locators are hierarchy `sources/jira-hierarchy/r1/content.json#/results/16/children/17` and member index `sources/jira-member-index/r1/content.json#/items/108`, as recorded by that report; underlying packets not re-audited.
4. `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (1–12): D-015, read without truncated lines.
5. `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1145.md` (1–178, final line unterminated) and `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-1145.md` (1–181): complete accepted baseline and independent qualifications.
6. **J** = `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-skill-switch-details/r1/content.json`, exact JSON pointer `/items/1/description`: reread complete MOS-1145 description, specifically “Изменение статусов навыка”, “Таблица истории действий”, both operation scenarios and “Хранение предыдущего статуса”. No embedded example executed.
7. `openspec/changes/mos-1031-skill-audit-history/.openspec.yaml` (1–2), `proposal.md` (1–27), `design.md` (1–26), `specs/skill-audit-history/spec.md` (1–47), `tasks.md` (1–17): all discovered active change artifacts read completely.
8. **S** = `openspec/specs/skill-lifecycle/spec.md` (1–98): complete main lifecycle spec.
9. **T** = `openspec/specs/skill-global-toggle/spec.md` (1–70): existing toggle ownership, reason requirements and historical approval; remainder not needed for this supplement.

### Integrity and provenance

`sha256sum` over L returned exactly:

`633abdc28221704babdf91d5cacfd7be46e1197d6fe8f3175e20e0af22caeb95`

This matches both assignment and metadata. Hash scope is saved UTF-8 Markdown, **not original Jira JSON/page or attachment bytes**. L is a selected normalized extraction: tables preserve description, comments preserve only selected non-personal excerpts. Capture `2026-10-19T07:06:01.008Z`; issue update `2026-10-16T19:22:39.728+0800`; Ready for test is documentary status only. Metadata preserves an earlier r1 timeout. J was used for narrow source verification, not a fresh whole-packet hash audit.

`git rev-parse HEAD` returned assigned HEAD `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Index/worktree state was not inspected and is **unverified**; matching HEAD does not establish either.

## Key Code / Requested Storage Contract

No application code inspected.

- L:19–26: status dictionary code PK, display name, unique display order, active flag and timestamps; eight initial statuses from draft to prod.
- L:34–41: transition dictionary `(from_status, to_status)` composite PK, status FKs, active flag and timestamps; nine initial edges.
- L:49–55: history UUID PK; required skill UUID FK with deletion restriction; nullable old-status FK (NULL at creation); required new-status FK; server-time default; nullable `actor_sso_id varchar(200)` (NULL for automatic change); nullable `reason text` when the scenario provides one.
- S:11,49: current frontend generic command matrix remains only `draft → checking`, `sandbox → review`, `whitelist → prod`. Storage seeds do not enlarge it.
- MOS-1031 design:13–17 and tasks:3–5: Query API acceptance, entity type+ID, ordering/pagination, redaction and consistency remain prerequisites; no fabricated local rows.

## Stable Supplemental Candidates

| ID | Delta and exact evidence | Bounded disposition / owner question |
|---|---|---|
| **MOS1119-D01 — initial dictionaries are not UI commands** | L:26,41 requests eight initial statuses and nine transitions: draft→checking; checking→training; training→autotest; autotest→sandbox; sandbox→review; review→draft; review→whitelist; whitelist→review; whitelist→prod. All three currently approved generic UI transitions occur in that seed set (S:11,49). Other edges concern a broader process; L supplies no frontend caller policy. | Documentary compatibility for the three edges, **not backend acceptance proof**. No new buttons, review decisions, automatic progression or dictionary-driven UI authorization. Ask lifecycle owner how active flags and process-only edges are exposed/enforced if a future contract needs them. S:30 still forbids treating ordered stages as completed history. |
| **MOS1119-D02 — disabled integration remains underspecified** | L:26,41 contains no initial disabled row or disabled edge; L:51–52 requests FKs to the status dictionary. J `/items/1/description`, “Изменение статусов навыка” and “Хранение предыдущего статуса”, requires disabled via dedicated commands and delegates previous-status storage/restoration to MOS-1119. L provides old/new history fields but no explicit selection/restore algorithm or disabled seed extension. Supplements MOS1145-C02/C03. | Ask backend owner where disabled dictionary support and restoration integration are specified, including identifying the immediately preceding state under repeated/concurrent operations. Absence from initial seeds is **not proof of forbidden toggle or deployed incompatibility**. Do not infer “read latest row” algorithm or expose generic disabled transitions. Preserve T:64 approved prod→disabled→prod and D-015; no reopening or expansion to all-status UI. |
| **MOS1119-D03 — history persistence is not history-query publication** | L:43–55 now specifies requested transition-history storage keyed by skill ID. It supplies no endpoint, wire entity type, query/filter protocol, ordering, pagination, redaction, consistency or relationship to broader audit events. MOS-1031 proposal:7–10,20–27; design:13–17; spec:9,23,32–47; tasks:3–5 retain these gates. Supplements MOS1145-C12. | **No-op for existing ownership/gate.** Keep MOS-1031, not a duplicate plan; do not substitute this table or a command receipt for Query API. Ask existing owner whether the eventual audit reader includes/project these events and under which contract. No fresh global API inventory was performed; the prior publication-absence result remains attributed to accepted SCENARIO-MOS-1145, not re-attested here. |
| **MOS1119-D04 — nullable storage fields do not loosen UI requirements** | L:51,54–55 permits null old status at creation, null actor for automatic changes and scenario-dependent null reason. J “Таблица истории действий” separately requires `skill_disabling.reason` as a code FK and non-null UUID `actor_id`; T:34–51 requires reason for both UI commands. Different tables/contexts do not by themselves contradict each other. Supplements MOS1145-C04/C08. | Do not make toggle reason optional, replace its codes with arbitrary history text, require UUID formatting for `actor_sso_id`, or substitute current user for missing actor. Ask owner for projection/identity mapping and future automatic-actor presentation; no UI label policy follows from storage nullability. Creation `old_status = NULL` is not an unknown-current-status fallback. Existing reason-dictionary/free-text tension remains unresolved. |
| **MOS1119-D05 — immutability and referential guarantees are requests** | L:13,45 requests immutable history; L:49–53 provides UUID/time defaults and deletion-restricting FKs. These establish intended storage shape, not mechanisms preventing UPDATE/DELETE, actual event completeness, chronological tie-breaking, replay deduplication or successful migrations. J operation scenarios separately require atomic status/history changes; MOS1145-C09 already preserves that distinction. | Ask backend owner for implementation/acceptance evidence and precise integration transaction boundaries when separately authorized. Do not claim a distributed audit transaction, delivery SLA or proven append-only persistence from schema prose, defaults or Ready-for-test. No implementation audit performed. |
| **MOS1119-D06 — missing-description gap narrowed, test evidence unchanged** | L:9,59–67 and metadata now supply selected MOS-1119 description, empty returned subtasks, metadata for attachment **833803**, and excerpts from both returned comments (1122856: draft MR16; 1125304: test-plan reference). Supplements MOS1145-C15 and D-015:11. | Record newly available description **without rewriting historical “unavailable” findings**. Attachment `TEST_PLAN_MOS_1119.md` is known only by ID/name/MIME/7410-byte metadata; its body is unread. MR, custom fields and changelog remain uninspected. MOS-1145 attachment **835759** is distinct and remains unread here. Neither attachment metadata nor comments prove test execution or delivery. |

## Architecture

MOS-1119 requests backend dictionaries and transition-history persistence. MOS-1145 requests dedicated toggle operations that integrate previous-state restoration with MOS-1119, plus separate action history/audit. Existing MOS-1027 owns approved frontend toggle behavior; MOS-909/main lifecycle owns the narrower generic command matrix. MOS-1031 owns future server audit reading and remains contract-blocked. Shared skill identity is useful evidence, not proof that all storage tables are a published unified audit stream.

No source precedence was selected. Newer collection time does not supersede approved UI, accepted D-015, or the historical auth approval. No new auth inspection or policy is needed for this storage-only supplement.

## Start Here

Read `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-lifecycle-details/r2/content.md:26–55` alongside J `/items/1/description` section “Хранение предыдущего статуса”. D02 is the first bounded owner question: the new model narrows the missing-evidence gap but still does not specify the promised disabled restoration integration. Then retain the gate in `openspec/changes/mos-1031-skill-audit-history/design.md:13–17`.

## Blockers, Limits and Disposition

- No required local input was unavailable; no execution-mode substitution was needed.
- Independent review remains required before accepting this report. Product activation remains unauthorized; MOS-1031 Query API remains blocked by its existing plan.
- Storage/index/runtime/implementation/test results are unverified. No tests, builds, network/browser/MCP, examples, test plans, generation, sync/archive, credentials access, git mutation or delegation were performed.
- Only this designated report artifact was written. No source, product, spec, task, decision or existing report was edited. No stage/index cleanliness assertion is made.
- This bounded supplement closes neither global tasks 3.2/3.4 nor G2. It does not close MOS-1119 or any feature.

```acceptance-report
{
  "criteriaSatisfied": [
    {
      "id": "criterion-1",
      "status": "satisfied",
      "evidence": "Verified exact assigned extraction hash; read required baseline and all active MOS-1031 artifacts; recorded six stable, precisely located supplemental candidates and preserved authorization boundaries. Independent review pending."
    }
  ],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-MOS-1119.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command": "sha256sum openspec/changes/reconcile-control-center-backlog/audit/sources/jira-lifecycle-details/r2/content.md", "result": "passed", "summary": "Exact assignment and metadata digest matched."},
    {"command": "git rev-parse HEAD", "result": "passed", "summary": "Matched assigned bc0d9800f25a90989b9c73c76f91996f8300f1d3; index uninspected."},
    {"command": "Local file discovery, numbered reads and selected JSON description inspection", "result": "passed", "summary": "All required local inputs available; complete active MOS-1031 artifacts and main lifecycle specification read."},
    {"command": "Tests, builds, network/browser and endpoint execution", "result": "not-run", "summary": "Outside read-only documentary assignment; prohibited."}
  ],
  "validationOutput": ["633abdc28221704babdf91d5cacfd7be46e1197d6fe8f3175e20e0af22caeb95", "Material storage-documentation delta; no product activation or gate closure."],
  "residualRisks": ["Independent review pending.", "Disabled restoration mechanism and storage/audit projection remain owner questions.", "Attachments 833803 and 835759 unread; MR, implementation, runtime and tests unverified.", "Index/worktree state uninspected; no empty-index attestation."],
  "diffSummary": "Designated supplemental report only; no project source or product changes.",
  "reviewFindings": ["No missing-input blocker to bounded analysis; existing history API gate remains blocked."],
  "manualNotes": "D-015 remains historically valid. Candidate findings are supplemental documentary evidence, not source precedence, UI policy, implementation acceptance or authorization to close global tasks 3.2/3.4 or G2."
}
```
