# R-DELTA-AB-TESTING-ROOT-DOC

## Review

**Decision: ACCEPT.**  
**Merge verdict: OK** for this bounded documentary supplement only.

No issues found.

Mandatory fixes: none. No files edited.

## Actual inspection

Read completely:

- Analyst report and both analyst/reviewer work-items.
- `sources/wiki-247742436-readable/r1/content.txt`, lines 1–319.
- `sources/wiki-247742436-readable/r1/body-view-chunks.json`, lines 1–21: all 19 entries `[0]–[18]`, in consecutive batches 1–6, 7–11, 12–16 and 17–21.
- Original metadata, lines 1–21, and derived metadata, lines 1–14.
- Original `sources/wiki-247742436/r1/content.json`, metadata lines 1–10 and separate attachment index lines 12–35. Original bodyView was reviewed through the complete chunk artifact, not independently compared byte-for-byte.
- Current `openspec/specs/ab-testing-{module,registry,editor,export}/spec.md`.
- Approved archive `openspec/changes/archive/2026-10-15-add-optional-ab-testing/{proposal,design}.md`.

Source paths above are relative to `openspec/changes/reconcile-control-center-backlog/audit/`. Scoped line-number searches additionally checked the significant source keys and owner requirement boundaries.

## Findings verified

Here **S** denotes the readable source; **M/R/E/X** denote the current module/registry/editor/export specs; **D** denotes archived design.

| Candidate | Review result and evidence |
|---|---|
| **ABROOT-01** | Correct. S 10–44 specifies registry columns, three-click sorting, name/code/group-tag search, any-selected-surface matching and saved selections. R 11–21, 58–98 separately requires server selection/pagination, broader search, `-updated_at` restoration and persistent complete selections. The report does not reduce those guarantees to prototype behavior. |
| **ABROOT-02** | Correct. S 30–35 describes the condition builder. Current R 25–27 and 46 explicitly support metadata-backed numeric `groups_count`, including finite inclusive ranges and NULL exclusion. D 40 still lists group count as unavailable. Priority and surface conditions remain unavailable; the report records the difference without deciding chronological precedence. |
| **ABROOT-03** | Correct. S 81–103 and 135–147 establish group editing, total=100, minimum two groups, at least one surface and unique tags. E 20, 39 and 60–86 add bounded integer validation, preserved IDs, accessible ordering and truthful previews. S 89–91 and 151–152 use `sort_order`/`draft.surfaces[]`; E 39 uses array order/`surface_ids`, without sending `sort_order`. None establishes traffic allocation. |
| **ABROOT-04** | Correct. S 59–60 describes pause/completion shortcuts; S 163 and 262 distinguish the prototype’s missing restriction from the model’s launch-related tag freeze. E 53 uses saved non-draft status, explicitly not historical ever-started identity. E 90 requires clean saved records, status-only commands, server confirmation and no automatic dates. M 48–53 prevents conflating archived, disabled and DELETE. No complete transition machine is inferred. |
| **ABROOT-05** | Correct. S 223 explicitly permits an empty end date for manual completion; S 227 defines sample size per group. S 103–122 and 289–299 describe configuration vocabulary, not measurement windows or algorithms. E 20 and D 43 require a scheduled start date without inventing a datetime scheduler. M 39 and D 13, 75–81 exclude execution, statistics, algorithm assignment and inferred control identity. |
| **ABROOT-06** | Correct. S 190–196, 215–241, 252–281 and 300–319 support seven tables, four dictionaries, UUID joins, unique experiment/surface and experiment/tag pairs, required switches and optional storage fields. S 220’s external UUID differs from E 76/D 44’s external string ID. S 114 uses `return_to_control_on_stop`; S 236 and E 11 use `return_to_control`. E 39 and D 65–67 own API clearing/preservation behavior. E 11/D 51 defaults are properly attributed to the owner rather than independently established by this root. |
| **ABROOT-07** | Correct. S 44, 57, 126–144 and 159–162 describe pickers, demos, notifications and in-memory limitations—not actual CSV delivery, analytics or traffic execution. X 11, 25 and 39 retain whole-selection export, row-limit handling, ordered fields, saved-detail/dirty constraints, flat summaries and truthful file delivery. Attachment-specific behavior is not claimed. |
| **ABROOT-08** | Correct. M 11 and D 25–29 require normal dev/typegen/production registration without a separate feature flag. Optional means removable, not disabled by default. M 25–35 preserves existing access boundaries and denies business loading on forbidden screens; D 21 prohibits cross-optional and foreign business dependencies. M 39 distinguishes configuration/status persistence from traffic start/stop. No new grants or activation procedure is invented. |

## Evidence and integrity limits

- Original metadata identifies wiki **247742436**, revision **r1**, page version **4**, page timestamp `2026-10-14T15:05:13.679+08:00` and capture timestamp `2026-10-19T11:33:31.678Z`.
- Chunk `[0]`, line 2, references attachment **250800308**, `АБ_Тестирование_Прот.html`, version 2.
- The separate index confirms status 200, size 2 and `next: null`, with attachments **250800308** and **247742415**. This is index coverage only; neither attachment body nor PDF was inspected.
- Hashes and concatenation equality remain **metadata/parent-attributed**, not independently recomputed or verified here.
- Root statements about PDF consistency and archived accounts of prior attachment/image review are not fresh attachment coverage.
- No network/browser activity, rendering, source execution, application-code/API census, business calls, tests, builds or nested delegation occurred. No staging-state attestation is made.
- Acceptance does not establish implementation conformance, current API absence, precedence, a new implementation plan or whole-module completion. Global **6/28 remains unchanged**.