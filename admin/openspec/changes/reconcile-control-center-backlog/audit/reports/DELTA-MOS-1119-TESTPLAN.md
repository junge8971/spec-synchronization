# Code Context

## DELTA-MOS-1119-TESTPLAN — documentary supplement

**Result:** newly readable attachment adds a direct dictionary-schema disagreement and more specific persistence/command expectations. It is a test plan, not test execution evidence. No source precedence, product change or task closure is selected. Independent review remains required. D-016 remains valid for its historical input set.

## Files Retrieved

Paths are repository-relative. **A** means `openspec/changes/reconcile-control-center-backlog/audit`.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/DELTA-MOS-1119-TESTPLAN.md` (1–13), complete assignment.
2. **P** = `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-attachment-833803/r1/content.md` (1–209), complete newly saved plan; adjacent `metadata.json` (1–17), complete provenance.
3. **L** = `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-lifecycle-details/r2/content.md` (1–67), complete selected description; adjacent `metadata.json` (1–16), complete provenance.
4. `openspec/changes/reconcile-control-center-backlog/audit/decisions.md` (1–100; only D-016 at 3–11 used), historical acceptance boundaries.
5. `openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-MOS-1119.md` (1–93) and `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-DELTA-MOS-1119.md` (1–73), complete accepted supplement/review.
6. **S** = `openspec/specs/skill-lifecycle/spec.md` (1–98), complete existing lifecycle specification.
7. Complete discovered active MOS-1031 artifacts: `openspec/changes/mos-1031-skill-audit-history/.openspec.yaml` (1–2), `proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–17), `specs/skill-audit-history/spec.md` (1–47).
8. **O** = `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`, only status operation and its referenced schema closure, located by JSON pointers below; adjacent `metadata.json` (1–20). No other operations inventoried. JSON parsed as data, not executed.

### Integrity / source scope

Locally recomputed SHA-256 values match supplied metadata:

- P: `36817b1ee1a9087fe418a45874ee570f32f56d63557214ab58186a8379b3a766`.
- L: `633abdc28221704babdf91d5cacfd7be46e1197d6fe8f3175e20e0af22caeb95`.
- O: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`.

P metadata records capture 2026-10-19T07:13:04.297Z, full decoded text, 7410 saved UTF-8 bytes matching attachment metadata size; no attachment version/ETag. Its hash covers persisted decoded text, not independently hashed raw HTTP bytes. L is a selected normalized Markdown extraction, not complete issue JSON. O is the saved A-environment publication captured 2026-10-16T11:13:29.451Z, not current runtime or C-environment evidence. Capture order establishes no precedence or common deployment revision.

## Key Code / Published Contract Locators

No application code inspected. Define **OP** as O JSON pointer:

`/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`.

- OP `/description`: dictionary-governed transitions; optional reason; readiness recalculation for forward transitions starting checking→training; draft→checking and returns exempt; blocked checks preserve status/version/history but persist recalculated checks. Documents 422 VALIDATION_ERROR, 409 VERSION_CONFLICT and IDEMPOTENCY_KEY_REUSED, plus other failures.
- OP `/parameters/1`: required UUID Idempotency-Key. `/requestBody/content/application~1json/schema` references `#/components/schemas/ChangeSkillStatusRequest`.
- O `/components/schemas/ChangeSkillStatusRequest/required` = `["status", "expected_version"]`; `/properties/reason/anyOf` = string or null; `/properties/expected_version/minimum` = 1.
- OP `/responses/200/content/application~1json/schema` references `TsamResponseSchema_SkillResponse_`, whose `/properties/data` references `tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`. That DTO requires status, version, created_at, updated_at and checks among its fields. Its `updated_at` is a **skill response field**, not either dictionary's column.
- OP `/responses/422/content/application~1json/schema` references `HTTPValidationError` (`detail` array of `ValidationError`), not a structurally specified VALIDATION_ERROR code envelope. OP publishes no explicit 409 response schema; its description still supplies the named 409 requirements. This is prose/schema granularity disagreement, not absence of a command contract.
- O `/components/schemas/SkillStatus/enum` includes disabled; initial dictionary seed absence and existing spec wording remain previously accepted questions, not new findings created by this plan.

## Stable Delta Candidates

### MOS1119-TP01 — direct updated_at disagreement

**Evidence:** P §«Справочники статусов и переходов», 63–68 explicitly expects `updated_at` absent in **both** dictionaries. L §«Description — skill_statuses», 19–24 and §«Description — skill_status_transitions», 34–39 explicitly include `updated_at timestamptz NOT NULL default now()` in both. P 40–60 otherwise repeats the accepted eight statuses/nine edges; 65–67 restates active/uniqueness/FK checks.

**Disposition:** material source disagreement, not inferred omission. Ask backend/document owner which versioned dictionary definition each document targets and to reconcile it through separately authorized work. Do not drop or add columns, change frontend DTOs, or select attachment precedence. Dictionary `updated_at` is distinct from skill-card `updated_at` in O. Existing MOS1119-D01 ownership suffices for unchanged seeds.

### MOS1119-TP02 — concrete process requests do not expand UI; success has unstated prerequisites

**Evidence:** P §«Смена статуса с причиной», 93–109 shows draft→checking; §«Смена статуса без причины», 111–130 explicitly sends checking→training then training→autotest and expects 200. S 11,49 only approves draft→checking, sandbox→review, whitelist→prod for generic frontend commands. OP `/description` documents broader dictionary-driven command behavior but requires fresh readiness checks for the latter two examples; P preparation 10–15 does not specify readiness fixtures (nor fully spell out method permissions/headers).

**Disposition:** strengthened backend scenario evidence beyond seed-only MOS1119-D01, **not** new UI authorization. No extra buttons or client automatic progression. Owner question: what readiness/access/header setup makes those unconditional-looking 200 expectations valid for the intended revision? Preserve the omission rather than declare all seeded edges unconditionally successful or the sources irreconcilable. No new auth policy; team access shorthand does not waive the published command boundary. No-op for the approved three-command frontend matrix.

### MOS1119-TP03 — creation boundary and legacy no-backfill become explicit

**Evidence:** P §«История нового навыка», 70–91 expects draft/version 1, exactly one NULL→draft row, creation-equal timestamp, user SSO ID, NULL reason, no duplicate row on idempotent creation replay. L 51 previously explained NULL old status at creation but did not specify these cardinality/replay/time assertions. P §«Навык, созданный до MOS-1119», 181–191 explicitly preserves migrated current state, prohibits retrospective initial creation row, then records actual old/new status, author/time/reason and returns updated card state/version.

**Disposition:** new backend persistence acceptance detail. Creation row and legacy no-backfill apply to different cohorts, not contradictory rules. No synthetic history to fill the legacy gap, and a missing initial row cannot prove a skill was never created or never traversed earlier stages. SQL `ORDER BY changed_at, id` (P 78) is a test observation order, not published reader pagination/order semantics. Creation command itself was not inspected; this does not establish its transport/replay contract. Ask owner for migration boundary/fixture definition and creation timestamp/replay evidence when execution is separately authorized. Existing MOS-1031 remains owner of any eventual presentation implications.

### MOS1119-TP04 — absent and explicit-null reason are concrete, compatible status-command cases

**Evidence:** P 95–109 supplies a text reason and expects it persisted; P 115–130 separately omits reason for training and supplies explicit null for autotest, expecting NULL history values in both. L 55 permits nullable, scenario-dependent reason. O `/components/schemas/ChangeSkillStatusRequest/{required,properties/reason}` agrees on optional nullable reason.

**Disposition:** narrows MOS1119-D04 from storage nullability to a supplied generic status-command expectation; no schema mismatch for these two cases. No new reason UI required and no weakening of separate toggle reason requirements accepted in D-016. Empty/whitespace values, limits and whether absent versus null are equivalent for idempotency hashing are **not specified by these examples**; do not infer normalization or toggle reason-code mapping. Existing ownership suffices; no duplicate change.

### MOS1119-TP05 — precise failure expectations, not exhaustive error coverage

**Evidence:** P §«Ошибочный переход», 132–142 expects draft→prod and same-current-status requests to fail with 422 VALIDATION_ERROR without status/version/history effects. P §«Конфликт версии», 144–151 uses stale expected_version with a **new** key and expects 409 VERSION_CONFLICT with no such effects. OP `/description` supports disallowed-edge and stale-version errors, while OP `/responses/422` specifies HTTPValidationError and does not structurally publish the asserted code envelope (see above).

**Disposition:** new explicit same-state/no-history test expectation plus refinement of accepted failure behavior. Distinguish a fresh same-state command from exact replay of a successful prior command (TP06); do not apply 422 to all replays. Preserve named-code prose versus response-schema difference without selecting an error envelope or changing transport. Readiness-blocked, queue-busy, access, missing-header and other OP errors are outside this plan's covered scenarios, not removed requirements. Error-priority ordering when several preconditions fail remains unspecified. S 49–61 already owns safe frontend refusal/re-read behavior: no-op there.

### MOS1119-TP06 — idempotency and concurrency cardinality become testable expectations

**Evidence:** P §«Идемпотентность», 153–168 expects same key/body to reproduce the first response with one version increment and one history row; changing status **or reason** with reused key expects 409 IDEMPOTENCY_KEY_REUSED and no state/history effects. P §«Конкурентное изменение», 170–179 expects two admissible requests with equal expected_version and distinct keys to produce one 200, one 409 VERSION_CONFLICT, one mutation and one row. OP `/description` supplies the two conflict codes but not full replay equality/scope/retention semantics.

**Disposition:** supplements MOS1119-D05 with precise backend expectations, not proof of exactly-once delivery or runtime serialization. Ask owner which admissible fixture isolates concurrency from readiness/queue failures, what response equality covers, and what key scope/retention applies. Do not infer omitted-versus-null reason equivalence, error caching, replay after key expiry or an expected_version-only body change result. S 49–61 prohibits automatic POST retry and treats unknown outcomes conservatively; the test-plan replay expectation does not authorize changing that frontend policy.

### MOS1119-TP07 — local atomicity expectation is narrower than whole-card immutability

**Evidence:** P 105–109 expects a new row without changing the previous one; 193–197 requires status/history changes together and no version increase on errors, with card/table observations. L 13,45 already requests immutable history. OP `/description` says readiness refusal leaves status/version/history unchanged **but stores recalculated checks with new checked_at**.

**Disposition:** concrete status/version/history invariants refine MOS1119-D05; no contradiction with checks changing, because P does not require every card field to remain identical. Do not claim a total database rollback for every error, a distributed audit transaction, proven append-only enforcement, or a fault-injection test: the written observation strategy is not evidence that every failure window is exercised. Initial creation row in TP03 is separately defined, not invalidated by shorthand change-status atomicity prose. Backend owner should supply transaction/failure evidence under separate authority; no project edit here.

### MOS1119-TP08 — migration acceptance scope and newly read body; reader/restore gates unchanged

**Evidence:** P §«Миграция», 199–209 adds explicit A/C startup, three tables/seeds, `skill_status_history.skill_id` index, status FKs, preservation of existing skill statuses and one current Alembic head. P 17–21 supplies command/current-card endpoints and 74–79 uses direct SQL to observe history; it supplies no history-query API. Full P has no disabled-restoration algorithm. MOS-1031 design 13–17 and tasks 3–5 still require type+ID Query API, ordering/pagination, redaction and consistency.

**Disposition:** index/single-head/startup/environment assertions are newly visible migration expectations, not observed migration outcomes. **No-op** for existing MOS-1031 reader gate and MOS1119-D02 restoration owner question; do not create duplicate plans or derive “latest row” restore logic from SQL ordering. A supplied status-command contract must not be mislabeled as “no API”; a SQL history read is not a published frontend history API. D-016/MOS1119-D06 unread-833803 statements stay historically accurate; this revision narrows that evidence gap only. Attachment835759, linked MR, implementation and deployment remain uninspected. No claim that A and C passed, match one another or match O's capture.

## Architecture

MOS-1119 covers backend dictionaries/history persistence; the attachment now states acceptance observations via status command, card read and test DB. Main skill-lifecycle owns the narrower approved UI command policy and honest current-state display. MOS-1031 owns future server history presentation, still contract-gated. Persistence assertions do not supply reader publication, audit projection, restoration selection, or new frontend capabilities. D-016's separate toggle/auth approvals remain untouched.

## Start Here

Read P 63–68 against L 19–24 and 34–39: **TP01** is the direct new source disagreement. Next compare P 111–130 with OP `/description` for the missing success prerequisites in **TP02**. Preserve both versions pending owner clarification; do not edit specifications or implementation from this report.

## Limits and Disposition

All required local inputs were available. Only local file discovery, reads, JSON inspection, line numbering and digest computation were performed. Embedded SQL, HTTP snippets and test instructions were treated as untrusted documentary data and never executed. No tests/builds, endpoints, DB, network/browser/MCP, git operations, credentials, code edits or nested delegation. Only this designated report was written. Repository index/worktree state was not inspected and is not attested. No global/product task or G2 closure. Independent review and parent disposition remain outstanding.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Complete required documentary inputs read; eight stable delta candidates mapped to exact sections/JSON pointers; source disagreement and existing ownership preserved."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-MOS-1119-TESTPLAN.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local discovery, complete required document reads and numbered attachment inspection","result":"passed","summary":"All required inputs available; main lifecycle and all discovered active MOS-1031 artifacts read."},
    {"command":"sha256sum on attachment833803/r1 and lifecycle-details/r2 saved content","result":"passed","summary":"Both exact supplied digests matched."},
    {"command":"Read-only Python JSON extraction of saved status operation and referenced DTOs; SHA-256 of api-live/r1","result":"passed","summary":"Inspected supplied command contract and schema differences; digest matched saved metadata."},
    {"command":"SQL, tests/builds, endpoints, network/browser and migration checks","result":"not-run","summary":"Prohibited by bounded documentary assignment."}
  ],
  "validationOutput": ["Direct updated_at disagreement retained for both dictionaries.","Status-command contract distinguished from absent reader in this source; replay expectations do not authorize frontend retries."],
  "residualRisks": ["Independent review and parent acceptance pending.","Dictionary version disagreement and unstated readiness/concurrency fixtures remain owner questions.","Implementation, migration, runtime, tests and repository index/worktree state unverified.","No fresh global history-API inventory; attachment835759 and linked MR remain uninspected."],
  "diffSummary":"Designated documentary report only; no source, specification, decision or product edits.",
  "reviewFindings":["No missing-input blocker; direct source disagreement preserved without precedence selection."],
  "manualNotes":"D-016 remains historical for its original input set. Test-plan assertions are requirements, never executed results; no product authorization or task closure follows. Unsupported noStagedFiles attestation intentionally omitted."
}
```
