# R-SCENARIO-MOS-909 — Independent documentary review

## Review

**Verdict: ACCEPT — C01–C08, bounded documentary reconciliation only.**

- **Correct:** The report distinguishes superseded read-only restrictions from approved rollout, schema fields from business guarantees, and documentary ownership from implementation evidence.
- **Fixed:** None; read-only review.
- **Findings:** No issues found.
- **Merge verdict:** OK with notes: documentary acceptance only; parent retains final disposition.

**Mandatory corrections: none.**

## Evidence inspected

Repository-relative aliases:

- **A** = `openspec/changes/reconcile-control-center-backlog/audit`
- **C** = `openspec/changes/archive/2026-10-02-mos-909-skill-current-status`
- **R** = `openspec/changes/archive/2026-10-02-mos-909-skill-lifecycle-rollout`
- **S** = `openspec/specs/skill-lifecycle/spec.md`
- **T** = `openspec/specs/skill-global-toggle/spec.md`

Read completely:

- `A/reports/SCENARIO-MOS-909.md` and both MOS-909 analyst/reviewer work-items.
- C: `.openspec.yaml`, proposal, design, tasks and lifecycle delta.
- R: `.openspec.yaml`, proposal, design, tasks, verification and all three deltas: lifecycle, mock server and training phrases.
- S and T.
- `A/sources/jira-MOS-909/r1/content.md` and metadata.
- `A/sources/api-live-status-readable/r1/content.json`: operation and all 24 referenced schemas; its metadata and original `api-live/r1/metadata.json`.
- All three cited accepted reviews: `R-SCENARIO-MOS-1145.md`, `R-DELTA-MOS-1119.md`, `R-DELTA-MOS-1119-TESTPLAN.md`.
- D-015–D-017 in `A/decisions.md`.
- Cited MOS-1019, MOS-1020 and MOS-1021 proposals; MOS-1031 design and tasks.

The original skills wiki exceeded the reader’s single-line limit. After blocking supervisor coordination, inspected parent-derived local text:

- `A/sources/wiki-241080062-readable/r1/readable-text.txt`: lines 1–40, 115–164, 290–329, 758–907, 1020–1044 and 1090–1109. These include lifecycle/ЖЦ, КАРН/ПРТ-КАРН, ОТК/ПРТ-ОТК, dictionary §§7.1–7.4 and all cited task rows.
- `A/sources/wiki-241097511-readable/r1/readable-text.txt`: complete, including §§1.3, 2.6, 2.8–2.10 and 3–4.
- Both original and derived wiki metadata packets.

These are primary-source-derived text extractions, not independent fresh captures. Neighboring-change inspection was deliberately limited to the named proposals/design/tasks; no complete neighboring implementation audit is claimed.

## Per-candidate disposition

| Candidate | Verdict and evidence | Preserved qualification |
|---|---|---|
| **MOS909-C01** | **ACCEPT.** Jira description at `content.md:10–13` requests state-dependent commands while separating prototype codes. C proposal’s “What Changes” retains historical read-only scope. R proposal:7–9 and design:17–46 explicitly replace G5 with three commands; S:11–35,49–74 retains them. | No new approval gate or duplicate plan. Preserve confirmation snapshots, pending suppression, server-derived responses and read-based uncertainty recovery. The UI matrix is not backend admissibility proof. |
| **MOS909-C02** | **ACCEPT.** Jira:10 expressly forbids treating prototype codes as API codes. Skills wiki `/bodyView`, lifecycle and §7.3, includes eleven statuses; published `SkillStatus/enum` has nine, excluding approved/rejected. R design:30 excludes prototype additions. MOS-1020 proposal:7–11,26–29 explicitly approves `review → whitelist`; MOS-1021 proposal:8–11 defers approved→whitelist. | Existing MVP mapping is settled; broader source modeling remains unresolved. No invented aliases or runtime statuses. MOS-909’s absence of a review command does not prohibit the separately approved review capability. |
| **MOS909-C03** | **ACCEPT.** S:37–40 and 78–83 retain obsolete disabled/eight-status wording. Published `SkillStatus/enum` includes disabled; T:11–27,38–46,58–64 recognizes it and requires dedicated commands. D-015 and accepted MOS-1145 C02 already own this correction. | Reuse the existing documentary candidate. Disabled is not a successful ninth progression stage or authorization for generic status disable/enable. Preserve 13.10.2026 prod→disabled→prod approval and existing non-prod restoration questions. Do not rewrite historical archives. |
| **MOS909-C04** | **ACCEPT.** Skills wiki ЖЦ-3, КАРН-3 and T-26 request completed/current/future visualization. R design:32–34 and S:30–35 deliberately keep noncurrent stages neutral. MOS-1031 design:13–17 and tasks:3–5 retain the reader gate. The inspected response DTO contains no transition-history array. | Later stage labels already exist; completed-history rendering remains consciously excluded. Neither enum order nor persisted-history requirements prove completed steps, a guaranteed future path or an available reader. |
| **MOS909-C05** | **ACCEPT.** S:30’s blanket absence rationale needs qualification against the saved namespaced response schema. Its required fields include checks, training, training_eta, autotest and autotest_note. Status-operation description explicitly provides fresh readiness checks, exceptions and persisted recalculated results on refusal. MOS-1019 proposal:7–11,21–29 owns observation, not current-input-bound run/result proof. | Narrow wording candidate only. Preserve neutral stages and current-phrase readiness limitations. No new check UI, rerun command, ETA interpretation or frontend readiness calculation. D-017 and accepted TP07 correctly preserve the checks-persistence exception. |
| **MOS909-C06** | **ACCEPT.** S:18–26,49–59,71–98 and R design:42–46 require strict validation, stale-state blocking and conscious recovery. Status-operation description names business errors; explicit response schemas list only 200/422. Catalog §2.9 specifies generic idempotency scope/replay but no retention duration. | Publication-aware recognition of disabled does not loosen unknown-state handling. Queue-busy “retry later” does not authorize automatic POST retry. No exactly-once, universal rollback, replay-retention or error-priority guarantee follows. |
| **MOS909-C07** | **ACCEPT.** Jira directly links the catalog wiki. Its §1.3 model and §2.8 mutable-field list omit status, while the independently inspected API operation publishes status POST and R explicitly selects it. | Catalog scope/version differences do not establish lifecycle API absence or require renewed approval. No PATCH status or invented endpoint. Historical auth approval remains attributed to D-015–D-017, not independently reopened or expanded. |
| **MOS909-C08** | **ACCEPT.** Jira:20–26 records MR/test assertions with explicit evidence limits. C tasks:13–18 and R verification:5–22 record historical checks and omissions. Wiki КАРН-4, ОТК/ПРТ-ОТК and T-27/T-87 request richer live-state behavior; T:13 excludes durations/metrics from the MVP. | Comments and archives do not attest current code, execution or runtime propagation. Preserve separate observation, review, bulk, toggle and history ownership. No task, feature or global closure follows. |

## Exact schema and operation verification

Original operation pointer:

`/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`

Schema pointers below are under original `/components/schemas/`, preserved as reference keys in the readable packet.

- `ChangeSkillStatusRequest` requires `status` and integer `expected_version`, minimum 1. `reason` is optional and nullable string.
- Required operation parameters are UUIDv7 `skill_id` and UUID `Idempotency-Key`.
- The 200 envelope references `tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`, not an assumed unqualified schema.
- That DTO requires `checks`, `training`, `training_eta`, `autotest`, `autotest_note`, `status` and `version`. Training/autotest are non-null strings without enumerated values; ETA/note are required but nullable strings. ETA has no declared duration or timestamp format.
- `checks` is a required non-null array; the schema supplies no minimum count or guarantee of all five check types.
- `SkillCheckResponse` requires all five fields: check_type, status, blocking, message and checked_at. Message is nullable; checked_at is a non-null date-time string. Requiredness does not imply non-nullability.
- The operation prose requires recalculation before advancement along `checking → training → autotest → sandbox → review → whitelist → prod`. It explicitly exempts `draft → checking`, `review → draft` and `whitelist → review` from checks/recalculation.
- Missing results do not count as passed; semantic-conflict warnings do not block.
- Readiness refusal preserves status/version/history while persisting recalculated checks and a new checked_at. Queue-busy separately says nothing was saved. These statements must not be generalized into whole-card rollback for every refusal.
- Explicit responses are 200 and 422. Named business-error prose does not provide a complete corresponding structured error contract.
- The fields establish neither completed lifecycle history nor binding of an observed result to the current phrase revision.

These details support C05 without authorizing readiness activation.

## Provenance and limitations

The declared MOS-909 digest matches the assignment/report/metadata:

`b2def825eb88fa33d1e553a33d7c75fca087f4593c1c431e5daf7f68baabda72`

Its scope is saved normalized Markdown, not raw Jira bytes. **This reviewer did not independently recompute hashes.** The author’s Jira hash computation and parent’s derived-packet equality/hash checks remain attributed evidence.

The API remains the saved 2026-10-16 publication, not a deployment observation. Skills wiki revision 17 and catalog revision 6 are distinct from capture times and catalog body v1.0/v1.1 history. The catalog metadata preserves the unexplained earlier r1 failure. No chronology-based precedence is selected.

No application code, tests, builds, network, browser, SQL, endpoints, credentials, Git state or nested delegation were inspected or executed. No project edits were made. Auth/toggle approval is preserved through current specifications and accepted decisions, not re-attested through runtime testing.

**Final disposition: accept C01–C08 without mandatory corrections.** C03 remains previously accepted documentary debt; C05 is a supported narrow wording candidate. Neither grants permission to edit specifications, extend commands, reopen historical approvals or close product work.