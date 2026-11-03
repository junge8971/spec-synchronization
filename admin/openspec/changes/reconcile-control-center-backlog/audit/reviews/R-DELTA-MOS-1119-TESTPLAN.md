# R-DELTA-MOS-1119-TESTPLAN — Independent documentary review

## Review

**Verdict: ACCEPT — all eight documentary candidates.**

- **Correct:** The report accurately separates test-plan expectations from executed outcomes, backend commands from approved frontend capabilities, and persistence from history-reader publication.
- **Fixed:** None; read-only review.
- **Findings:** No issues found.
- **Merge verdict:** OK with notes: documentary acceptance only; parent retains final disposition.

**Mandatory corrections: none.** The qualifications below remain binding.

## Evidence inspected

**A** = `openspec/changes/reconcile-control-center-backlog/audit/`.

Read completely:

- `A/work-items/R-DELTA-MOS-1119-TESTPLAN.md`
- `A/work-items/DELTA-MOS-1119-TESTPLAN.md`
- `A/reports/DELTA-MOS-1119-TESTPLAN.md`
- **P:** `A/sources/jira-attachment-833803/r1/content.md` and metadata
- **L:** `A/sources/jira-lifecycle-details/r2/content.md` and metadata
- `A/reports/DELTA-MOS-1119.md`
- `A/reviews/R-DELTA-MOS-1119.md`
- **S:** `openspec/specs/skill-lifecycle/spec.md`
- All active MOS-1031 artifacts: `.openspec.yaml`, `proposal.md`, `design.md`, `tasks.md`, `specs/skill-audit-history/spec.md`
- Original `A/sources/api-live/r1/metadata.json`
- Parent-provided `A/sources/api-live-status-readable/r1/content.json` and metadata, including the status POST and all 24 transitively referenced schemas.

Also read **D-016** in `A/decisions.md`, including its historical approval and evidence boundaries.

The original API JSON is a single line exceeding the read tool’s limit. After a blocking request, the parent supplied the readable local subset above. Its reference keys preserve original schema pointers; this review inspected those values rather than relying on the report’s API summary. Parent reports parsed-value equality with the original saved source. This is derived evidence, not a new API capture or complete OpenAPI inventory.

Define **OP** as the original API pointer:

`/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`

Schema pointers below refer to the original `/components/schemas/` namespace.

## Per-candidate disposition

| Candidate | Disposition and evidence | Mandatory correction / retained qualification |
|---|---|---|
| **MOS1119-TP01** | **ACCEPT.** P:63–68 explicitly requires absence of `updated_at` in both dictionaries; L:19–24 and 34–39 explicitly includes it in both. The referenced namespaced `SkillResponse` independently requires its own `updated_at`. | **None.** This is a direct documentary disagreement, not omission or a skill-response incompatibility. Retain the backend/document-owner question about targeted versions. No precedence, column change or DTO change follows. |
| **MOS1119-TP02** | **ACCEPT.** P:93–130 supplies draft→checking, checking→training and training→autotest success expectations. OP `/description` requires fresh readiness checks for the latter two, plus method permission and authentication headers. P:10–15 does not specify that complete setup. S:11,49 retains only three approved generic frontend commands. | **None.** Concrete backend requests do not authorize extra UI commands or unconditional success. Keep readiness/access/header fixture questions; team access alone does not waive the command boundary. |
| **MOS1119-TP03** | **ACCEPT.** P:70–91 specifies one creation row, NULL→draft, version 1, creation-equal timestamp, actor and NULL reason, with no additional row on creation replay. P:181–191 separately prohibits retrospective creation rows for pre-MOS-1119 skills and requires subsequent real transitions. | **None.** Creation and legacy cohorts are distinct. Preserve the migration-boundary question and prohibition on synthetic history. P:78 SQL ordering is not reader ordering/pagination. The creation operation’s transport contract was not inspected. |
| **MOS1119-TP04** | **ACCEPT.** P:95–130 covers textual reason, omitted reason and explicit null. `ChangeSkillStatusRequest/required` contains only `status` and `expected_version`; `/properties/reason/anyOf` permits string or null. L:55 permits scenario-dependent nullable history reason. | **None.** These examples establish neither absent/null equivalence for replay hashing nor empty-string/whitespace normalization. Preserve separate toggle reason requirements and existing reason-code/free-text questions. |
| **MOS1119-TP05** | **ACCEPT.** P:132–151 specifies invalid-edge/current-status 422 and stale-version 409 with a new key, without status/version/history changes. OP `/description` supplies named validation/version errors, while `/responses/422` references `HTTPValidationError`, whose `detail` items reference `ValidationError`; it does not structurally specify the asserted named-code envelope. | **None.** Retain the prose/schema distinction without selecting an envelope. A fresh same-state command is not successful-command replay. The plan does not eliminate other published errors or define precedence between simultaneous failure conditions. |
| **MOS1119-TP06** | **ACCEPT.** P:153–179 specifies replay response equality, one increment/row, changed status or reason with reused key, and two admissible concurrent requests with distinct keys yielding one success and one version conflict. OP `/description` supplies the conflict codes but not complete replay equality, retention or key-scope semantics. | **None.** These are testable expectations, not exactly-once delivery or demonstrated serialization. Retain concurrency-fixture, response-equality and key-scope/retention questions. S:49–61 still prohibits automatic POST retry and requires conservative unknown-outcome handling. |
| **MOS1119-TP07** | **ACCEPT.** P:105–109 preserves the prior history row; P:193–197 specifies coupled status/history changes and no version increment on error. OP `/description` explicitly permits recalculated checks and new `checked_at` to persist on readiness refusal while status/version/history remain unchanged. | **None.** Local invariants do not imply whole-card immutability, universal rollback, distributed audit atomicity or proven append-only enforcement. The observation instructions are not fault-injection execution evidence. Creation history remains the separately specified case. |
| **MOS1119-TP08** | **ACCEPT.** P:199–209 specifies A/C migration/startup, tables/seeds, history skill-ID index, status FKs, preservation of existing statuses and one Alembic head. P:17–21 publishes command/card endpoints; P:74–79 uses SQL observation, not a history-query API. MOS-1031 `design.md:13–17` and `tasks.md:3–5` preserve the reader gate. | **None.** No migration outcome, environment equivalence, reader publication or restoration algorithm is demonstrated. Retain MOS-1031 ownership and MOS1119-D02 restoration questions. Newly reading attachment833803 narrows the historical evidence gap without rewriting D-016 or establishing test execution. |

## Exact contract checks

The inspected status-operation subset confirms:

- OP `/parameters/1` requires UUID `Idempotency-Key`.
- OP `/requestBody/content/application~1json/schema` references `ChangeSkillStatusRequest`; its `expected_version` minimum is 1.
- OP `/responses/200/content/application~1json/schema` references `TsamResponseSchema_SkillResponse_`; its `data` references `tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`.
- That DTO requires `status`, `version`, `created_at`, `updated_at` and `checks`, among other fields. These are skill-card fields, not dictionary-column definitions.
- OP publishes explicit response schemas for 200 and 422, not 409; named 409 requirements remain present in its description.
- `SkillStatus/enum` includes `disabled`. This preserves the previously accepted seed/spec reconciliation question; it does not authorize generic disabled commands.
- Readiness refusal can persist checks without status/version/history mutation. Queue-busy and other published failures remain outside the plan’s selected coverage, not removed requirements.

## Integrity and provenance

Declared digests are consistent between the assignment, report and saved metadata:

- P: `36817b1ee1a9087fe418a45874ee570f32f56d63557214ab58186a8379b3a766`
- L: `633abdc28221704babdf91d5cacfd7be46e1197d6fe8f3175e20e0af22caeb95`
- Original API: `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`
- Readable API subset: `1346f28284551b1b7924132525730e76023fc9ffea7c2a92a60a51c53fb474ef`

**No independent hash recomputation was possible with the reviewer’s tools.** Author-reported computations remain attributed to the author; original/derived API digest and parsed-value verification supplied during review remain attributed to the parent.

P metadata describes full saved decoded text, 7410 UTF-8 bytes, without attachment version/ETag; its digest is not an independently verified raw-response-byte digest. L remains a selected normalized extraction. The API remains the saved A-environment publication captured on 2026-10-16, not current runtime or C-environment evidence. Capture chronology establishes neither precedence nor a shared deployment revision.

## Preserved gates and final disposition

- Preserve **13.10.2026 prod→disabled→prod UI approval** and **09.10.2026 auth approval**, as carried by the accepted baseline and D-016; neither is reopened, expanded or independently runtime-verified here.
- Retain the three-command frontend lifecycle matrix, MOS-1031 Query API gate, and disabled dictionary/restoration owner questions.
- Do not infer “latest history row” restoration from test SQL.
- Attachment **833803** is now read; attachment **835759**, linked MR, implementation and deployment remain uninspected.
- D-016 and the earlier unread-body statements remain historically accurate for their original input sets.

Only local reads/searches and the blocking evidence-access coordination were performed. No direct edits, tests/builds, SQL, endpoints, network, credentials, Git operations or nested delegation occurred. Embedded instructions remained documentary data.

**Accept TP01–TP08 without mandatory corrections.** This review supplies evidence for parent disposition only; it authorizes no product changes, activation, feature/global task closure or G2 acceptance.