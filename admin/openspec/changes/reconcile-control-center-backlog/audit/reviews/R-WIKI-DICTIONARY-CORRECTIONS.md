# R-WIKI-DICTIONARY-CORRECTIONS — focused verification

## Review

**ACCEPT — both mandatory documentary corrections are verified.**

- **Correct:** WD-12 now states **29 system / 10 informational = 39**, supported by an independent manual recount of exact HTML classification cells.
- **Correct:** The saved array contains **26 chunks**, on file lines **2–27**, with the closing bracket on line **28**. Report coverage and acceptance-block statements agree.
- **Fixed:** None by this reviewer; read-only verification.
- **Merge verdict:** **OK**, limited to these two report corrections.

No issues found.

## Evidence

`A` = `openspec/changes/reconcile-control-center-backlog/audit/`; `H` = `A/sources/wiki-247751846-readable/r1/body-view-chunks.json`; `T` = adjacent `content.txt`.

### 1. Classification partition

Manually recounted the actual table rows and classification cells in **H chunks 12–16, file lines 13–17**, cross-checking **T:234–295**:

| Section | System | Informational | Total |
|---|---:|---:|---:|
| Обратная связь | 8 | 1 | 9 |
| База знаний | 3 | 3 | 6 |
| Шаблоны ответов | 1 | 3 | 4 |
| A/B эксперименты | 3 | 1 | 4 |
| API | 5 | 1 | 6 |
| Состояние системы | 5 | 1 | 6 |
| Справочники | 4 | 0 | 4 |
| **Total** | **29** | **10** | **39** |

The template-owner entry is one complete `<tr>` in **H chunk 14, file line 15**. Its classification cell says **Информационный**; embedded `<br/>` elements explain the multiline text extraction and do not create additional rows.

The corrected partition and section subtotals match **`A/reports/WIKI-DICTIONARY-DETAIL.md:52`**, its correction note at **line 73**, and **D-027, `A/decisions.md:7`**.

The source’s own **24 system / 8 informational / 0 user = 32** summary remains visible in **H:17–18 / T:290–295**. The report correctly preserves that source disagreement rather than treating 32 as its own recount.

### 2. Chunk count and file-line convention

An exhaustive structural line search of H independently identified:

- Line **1**: `[`.
- Lines **2–27**: **26** quoted string-element lines.
- Line **28**: `]`.

A bounded terminal read confirmed that the final string at **H:27**, therefore **chunk 26**, ends with the seven-table inventory; **H:28** is only the array delimiter.

The complete report read and targeted occurrence search confirm coherent corrections at:

- **Line 7:** one-based chunk/file-line convention.
- **Line 12:** substantive file span **1–28**, containing **26** chunks.
- **Line 73:** explicit correction history and delimiter explanation.
- **Line 81:** acceptance-report evidence says **26** chunks.
- **D-027, decisions.md:7:** matching count and file-line mapping.

No contrary current count claim remains. Historical read requests ending at **29** are explicitly distinguished from chunk counts.

## History and limits

`A/reviews/R-WIKI-DICTIONARY-DETAIL.md` still records the original **REVISE**, both mandatory findings, and acceptance of the other thirteen candidates. The report correction note and D-027 explicitly preserve that history; this verification supplements rather than replaces it.

Only these two corrections were independently assessed. The other candidates retain their prior review disposition; no full feature, Jira/journal, policy, implementation or runtime acceptance is implied.

Local read/find/grep only. No edits, executable parsing, tests/builds, network/browser, source execution or nested delegation. Source hashes, byte-history equality and derivative roundtrip were not independently verified. No global task closure is authorized.