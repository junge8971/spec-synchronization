# Independent lifecycle/export plan review

## Verdicts

- **SPEC-G2-MOS-1256: ACCEPT**
- **SPEC-G2-MOS-1260: REVISE**
- **Escalation: none.**

These verdicts concern the candidate planning analyses only. Parent retains acceptance authority. No implementation, release gate, feature task or global G2 acceptance is implied.

## Evidence and scope

Read completely: both assignments, both candidate reports including attestations, all eight owning proposal/design/spec/tasks files, both accepted REQ reports, and `R-G2-FEEDBACK-REQUIREMENTS-RESUME.md`.

Shared reading was limited to `mos-1249-feedback-api/specs/feedback-api/spec.md:1–38` and `mos-1249-feedback-api/design.md:5–10`, for transport/error handling, permissions, isolation and source precedence. Accepted requirement quotations sufficed; no primary-source re-extraction was necessary.

**Parent-verified, not independently computed:**

| Candidate | SHA-256 |
|---|---|
| `spec-1256.md` | `196b0b282fb81a6b367c2308af3ba95189394e29ba514bd05da6aac637b2be0c` |
| `spec-1260.md` | `bb36155e95097c6b3dca5feeebf899056bb4c6dc2bc7d7ec56a009e6ab425814` |

The unchanged eight-plan baseline is likewise parent-attributed. Candidate historical command attestations were not replayed.

Paths below are relative to `openspec/changes/`. `L` means `mos-1256-feedback-lifecycle`; `E` means `mos-1260-feedback-export`; `F` means `mos-1249-feedback-api`.

## Review — MOS-1256

**Correct:** The candidate accounts for all 36 accepted rows. Its sole mandatory clarification is supported.

| Rows | Verified coverage |
|---|---|
| R01–R08 | `L/design.md:27`, `L/specs/feedback-lifecycle/spec.md:9–16`, `L/tasks.md:3–4`: lookup statuses, pause/resume, disabled versus soft deletion, confirmations and no restore. No transition matrix inferred. |
| R09–R11 | Spec lines 9, 18–21 and task 1.1 preserve explicit save/cancel and input on failure. |
| R12 | Partial: task 1.2 names separate pending and prevents double deletion; status pending re-entry is not expressly excluded. |
| R13–R18 | Design lines 27, 35, 42; spec lines 9–16; tasks 1.2/2.3; `F/specs/feedback-api/spec.md:9,21–24`: confirmed-result refresh, no automatic retries, unknown outcomes, occupied code and deletion-related 404 boundaries. |
| R19–R24 | `L/design.md:31`, spec lines 11, 23–31 and task 1.1 cover both entry paths, cancellation, combined PUT, preliminary-save deduplication and unchanged disabled. |
| R25–R26 | Design lines 35–37 incorporates `F/specs/feedback-api/spec.md:26–38`, including exact update/delete permissions and owner UI responsibility. |
| R27–R36 | Tasks 1.1/1.2 and 2.1, corresponding scenarios, and shared error/unknown-outcome clauses provide the verification obligations. Separate tasks per assertion are unnecessary. |

### Correction disposition: status pending re-entry — APPROVE

`L/tasks.md:4` explicitly couples pending with **DELETE** and “отсутствие … двойного удаления.” Task 1.1’s one-PUT confirmation requirement addresses a confirmed action, while design line 31 addresses preliminary-save deduplication. Neither expressly prohibits a second status submission while the first remains pending.

The accepted R12 obligation is broader than those two deduplication cases.

**Smallest material plan fix:** append to existing task 1.1 verification that pending status submission excludes repeat submission. No new scenario, task, state machine or duplicated spec wording is required.

The candidate appropriately treats local 409 wording as optional: shared error preservation, local input retention and component verification already apply.

**Merge verdict: OK** for this candidate report; its proposed plan correction remains for parent disposition and subsequent authoring.

## Review — MOS-1260

**Correct:** All 42 Jira rows and eight prototype rows are accounted for. The principal scope and architecture mappings are sound.

| Rows | Verified coverage |
|---|---|
| R01, R03–R11 | `E/specs/feedback-export/spec.md:9–21`, `E/design.md:29`, tasks 1.1/2.4: actual download, unique ordered fields, entire applied selection, saved-card-only export and dirty/new-card boundaries. |
| R02 | Field selection is covered; metadata-derived labels are not expressly covered. |
| R12–R22 | Spec line 11 and lines 23–26, design lines 29–31, tasks 1.1/1.2: server bytes, encoding/BOM/separator, backend escaping/formula protection, metadata limit and empty/limit/malformed responses. |
| R23–R30 | Spec line 11, design lines 31–35 and task 1.2 collectively require safe header-derived filename, error handling without false download, session isolation and URL release. See correction dispositions below. |
| R31–R32 | Design lines 35–37, 45 and linked shared permission clauses specify read plus export; release confirmation remains open. |
| R33–R37 | Proposal lines 9, 14; design lines 13, 31; spec line 9 preserve all stage-one exclusions and reject dialog-specific header requirements. |
| R38–R42 | Tasks 1.1/1.2, 2.1 and 2.4 cover the named unit/component/integration obligations without requiring one task per row. |

### Correction disposition: metadata labels — APPROVE

`E/specs/feedback-export/spec.md:9`, `E/design.md:29` and `E/tasks.md:3` prescribe metadata fields and ordering, but not the source of their UI labels. Accepted R02 expressly requires both columns **and labels** from `export_fields`.

**Smallest material plan fix:** add metadata-derived column labels to the existing spec line 9 requirement. Existing verification tasks suffice.

### Correction disposition: invalid/missing filename rejection — REJECT as mandatory

The candidate itself identifies the governing clauses:

- Spec line 11 requires a **safe name from Content-Disposition**.
- Design line 31 requires filename validation.
- Task 1.2 requires filename verification and no false download.

A missing or invalid header-derived filename cannot satisfy that download contract. Requiring these clauses to enumerate the negative branch again is optional precision, not a demonstrated missing behavior. A fabricated fallback is not authorized by the existing requirement.

**Required candidate revision:** classify R23 as covered collectively; move explicit missing/invalid-name rejection wording to optional clarification. Remove it from mandatory findings and summary counts.

### Correction disposition: generic 422 — REJECT as mandatory

Task 1.2 (`E/tasks.md:4`) already lists `404/403/422 EXPORT_LIMIT_EXCEEDED` in response checks and applies “нет ложного скачивания.” Design line 31 preserves common transport safety; spec line 11 requires an actual CSV binary response and rejects JSON/HTML rather than treating them as downloadable success.

Naming the limit code does not establish that another error response may become successful CSV. The candidate supplies no contradictory exception or omitted general failure path; it treats a more explicit enumeration as a mandatory addition.

**Required candidate revision:** classify R26 as covered by existing response/error verification. Explicitly writing “любой 422, включая EXPORT_LIMIT_EXCEEDED” is an optional clarification, not a new required behavior or error taxonomy.

### Finding: P2 — overstated mandatory omissions

**Location:** `spec-1260.md`, requirement mapping R23/R26, “Three narrow precision gaps,” “Start Here / minimal candidates” item 2, and acceptance-report findings.

**Evidence:** The owning safe-filename and no-false-download requirements above already constrain the claimed missing cases.

**Smallest fix:** change those two rows and corresponding summaries from mandatory gaps to covered/optional precision. Retain metadata labels as the sole material export-plan omission. No owning-plan edits are required for R23 or R26.

**Merge verdict: OK with notes** for the underlying planning coverage; **REVISE** the candidate’s mandatory-correction inventory before publication.

## Optional and no-op dispositions

- **Lifecycle 409:** optional local traceability wording; no additional recovery design or test task required.
- **Export default 10000:** optional wording clarification of design line 29; no missing/malformed-metadata fallback may be inferred.
- **Prototype W01–W08:** classifications are acceptable. Metadata-column scope and first-stage exclusions resolve broader section export. Exact modal widgets, button copy, toast placement/duration and dismissal restatements do not establish missing CSV capability. Dismissal must not be equated with request cancellation.
- **Source-only unknowns:** existing plans sufficiently resolve PUT, permission identifiers, session/owner isolation, unknown-outcome reread boundaries, server-owned CSV and prototype/API scope. Detailed copy, transition matrix, cleanup timing and parsing algorithms remain unspecified without becoming automatic blockers.
- **No-op:** do not duplicate already-covered confirmation, saved/applied-data boundaries, scope exclusions or verification assertions across every artifact.

## Constraints and final disposition

No files were edited. No shell commands, tests, code/API implementation inspection, network/browser access or nested delegation occurred. All unchecked feature tasks and release gates remain open. PUT and Q1 boundaries are unchanged.

**Final verdicts: MOS-1256 ACCEPT; MOS-1260 REVISE.**

Artifact path:
`/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/73e30915-ffe6-41cc-ac30-23cd3a1f8689/lifecycle-export-plan-review.md`