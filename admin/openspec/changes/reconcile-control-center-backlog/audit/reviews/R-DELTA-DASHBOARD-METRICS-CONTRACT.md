# R-DELTA-DASHBOARD-METRICS-CONTRACT

## Review

**Verdict: REVISE — locator corrections only.** DMC-01–12 are substantively supported. No runtime, formula, authorization, ownership or feature acceptance follows.

- **Correct:** The report distinguishes explanatory requirements from published DTO capability, preserves unresolved definitions and approved auth boundaries, and separates business read-audit publication from possible authorization-audit failure.
- **Fixed:** None; read-only review.
- **Finding: P2 — several source ranges omit the evidence they identify.** Exact corrections below.
- **Merge verdict: OK with notes.** Correct the locators before documentary acceptance/publication; no substantive rewrite required.

## Scope and notation

Repository-relative aliases:

- `A = openspec/changes/reconcile-control-center-backlog/audit`
- `W = A/sources/wiki-241095761-readable/r1`
- `T = W/content.txt`
- `P = A/sources/api-dashboard-review-projection/r2`
- `H = openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`
- `C` denotes **one-based** markup chunk numbers: C1 is `$[0]`, physical line 2.

Original-document JSON pointers:

- `G = #/paths/~1api~1control~1api~1analytics~1v1~1dashboard/get`
- `R = #/paths/~1api~1control~1api~1analytics~1v1~1dashboard~1refresh/post`
- `S(Name) = #/components/schemas/Name`

The projection’s `value` wrapper is not part of those original pointers.

## Mandatory minimal correction

**Location:** `A/reports/DELTA-DASHBOARD-METRICS-CONTRACT.md:76,84,92,98,106,114,130,148`.

Some ranges are not merely loose section boundaries: they exclude the substantive rule being cited. In particular, partial-failure rules are T453–457, malformed-GET validation begins at T484, and refresh begins at T505—not T519.

| Report location | Smallest correction | Verified evidence |
|---|---|---|
| DMC-04, line 76 | Change `T142–163` to `T140–159`. | Sparse-series and fixed-zero rules are T140–141; dictionary/Other rules continue through T159. |
| DMC-05, line 84 | Change `T459–494` to `T453–483`; add `T504` for the read-store/global-readiness errors. | T454–455 defines failed aggregates and missing computation rules, including empty-selection precedence; T483 defines empty success; T504 names both 503 cases. |
| DMC-06, line 92 | Change audit range `T795–798` to `T794–798`. | T794 explicitly says partial-widget failure remains audit success. |
| DMC-07, line 98 | Change §3.1.7 to `T484–504` and §3.2 to `T505–532`. | The present ranges omit the initial malformed-GET explanation and refresh request-body definition. |
| DMC-08, line 106 | Change §3.2 to `T505–532`. | Includes method purpose, body, success and subsequent GET as well as concurrency/rate limiting. |
| DMC-09, line 114 | Change combined §3.1.7/3.2 range to `T484–532`. | Covers both error examples and the complete refresh section. |
| DMC-11, line 130 | Change §3.2 reference `T527–528` to `T526`; optionally retain T799 as the shared-section duplicate. | T526—not T527–528—states that refresh has no own data-read event and the following GET publishes it. |
| Start Here, line 148 | Change `T459–532` to `T453–532`. | Ensures the recommended starting range includes the partial-failure rules. |

For section-exact boundaries, §§2.7.1–2.7.2 are T174–213 and §§5.2–5.3 are T746–800. Existing narrower ranges contain the report’s relevant unavailable-widget and audit statements; these boundary refinements do not create additional substantive findings.

Preserve all twelve IDs, dispositions and qualifications.

## Actual independent coverage

Read the complete analyst report and both named work items.

Independently read:

1. **Assigned source text:** T1–532, T693–800 and T833–854, without substantive omissions. The document has 854 substantive lines; the read tool exposes a trailing physical line. That difference does not excuse or indicate missing substantive text.
2. **All 34 exact markup entries:** `W/body-view-chunks.json`, `$[0]`–`$[33]`, including split tags/words, table headers/cells, examples and ordered final questions. The final combined return truncated after physical line 33; lines 34–36 were explicitly recovered.
3. Complete original and readable source metadata.
4. **Selected API operations:** `P/operations.json:1–150`, indexes 0/1 completely. The opening of index 2 at line 151 was incidental, not audited.
5. Complete `P/metadata.json` and `P/closure.json`.
6. **All 26 selected schema files**, complete:
   `schema-{02,03,04,05,06,07,08,09,10,11,12,13,14,15,16,17,19,20,21,22,24,25,28,31,33,34}.json`.
7. **Before auth interpretation:** complete `H/proposal.md`, `H/design.md`, and all six specs:
   `control-center-api-integration`, `control-center-http`, `control-center-mock-server`, `control-center-permissions`, `control-center-shell`, `mpmm-session`.
8. Complete accepted-context reports and corresponding reviews:
   - `DELTA-ADMIN-TOOLS-ROOT-BRIEFS` / `R-DELTA-ADMIN-TOOLS-ROOT-BRIEFS`;
   - `DELTA-SKILL-MONITORING-EXAMPLE` / `R-DELTA-SKILL-EXAMPLES`;
   - `DELTA-REPORTS-ROOT-DOCS` / `R-DELTA-REPORTS-ROOT-DOCS`.
   Also read `A/decisions.md:57–97`, including D-040/D-036/D-034.
9. Complete MOS-1030 `design.md:1–26` and `specs/skill-result-analytics/spec.md:1–47`.

Board/catalog operation semantics and board-write audit were **not independently audited**. Their markup was structural context only. Accepted monitoring/report/dashboard-brief context was reused, not re-audited against its original sources.

## DMC verification

| Candidate | Independent result and evidence |
|---|---|
| **DMC-01** | Supported. T38–94,214–267; C2–6,14–17 distinguish metric units, distribution summary unit and category measure. `S(MetricUnit)/enum`, `S(Measure)/enum`, and metric/distribution properties provide the typed vocabulary, not per-ID formulas, ranges or precision. T87 and final question 1 retain provisional IDs. Response titles and slot-dependent presentation are correctly separated. |
| **DMC-02** | Supported. T95–111 and questions 2/3/7/14/18–21; C6–7,32–34 preserve dialog/request/operator-rating/distinct-resident denominators and unresolved definitions. Selected schemas expose no separate numerator/denominator fields. Prototype arithmetic is not measurement evidence; identical percentages across populations are not mathematically impossible. No client formula or sample threshold is adopted. |
| **DMC-03** | Supported. T112–139; C7–9; questions 4/21. Relative percent change differs from percentage-point/seconds/score differences. Retention, empty base, unavailable aggregate, undefined values and zero relative-change base justify null—not measured zero. Required comparison bounds in `S(PeriodResponse)/required` do not prove available comparison data. Rounding prose and JSON lexical precision remain distinct. |
| **DMC-04** | Supported after locator correction. T140–159; C9–10. Sparse UTC daily series, fixed-category zeros, empty-distribution exception, server truncation and native/collapsed Other are correctly distinguished. `SeriesGranularity`, `SeriesPointResponse` and distribution properties do not enforce sorting, category uniqueness or limits. No-resident five-zero prose versus empty-dialog empty-items remains unresolved rather than silently synthesized. |
| **DMC-05** | Supported after locator correction. T174–213 identifies **10 markup-dependent and 4 Writer-dependent** unavailable widgets; C11–14 confirms their table columns. T303 excludes catalog-unavailable widgets independently of board composition. T453–483/C21 distinguishes failed available widgets from successful empty selection; T504 supplies read-store and globally unready 503 cases. Empty selection takes precedence over checking an uncomputed widget aggregate. No current catalog/runtime availability is certified. |
| **DMC-06** | Supported after audit locator correction. T304–305,451–457,794; C18,20–21,31. One coherent snapshot and HTTP200 partial failure are documentary intent, represented by required dashboard metadata and widget failure branch. No snapshot identifier, atomicity, freshness or refresh-to-GET identity guarantee follows from these structures. `chat_bd` remains an unresolved source label, not a browser database connection. |
| **DMC-07** | Supported after locator correction. T295–303,484–532,712–713; C17–18,21–23,27. Inclusive start/exclusive end, independently filled defaults, UTC normalization, unclipped explicit intervals and single channel are correctly retained. Numeric timestamp coercion is source prose; formal query/body schemas remain string date-time/null. GET parse errors versus period errors and POST validation are distinct. Required body is not equivalent to required body fields. No foreign presets, timezone or skill filter is imported. |
| **DMC-08** | Supported after locator correction. T505–532; C22–23. R publishes200 metadata followed by GET, not202/job/polling semantics. T528–530 adds sliding-window counting, ceil/minimum-one Retry-After, normalized submitted bounds without defaults, channel/scope deduplication excluding employee identity, and possible409/429/new success. `R/description` omits429 in its retry sentence but lists429 separately. No Idempotency-Key or reusable refresh result is declared; no automatic mutation replay is authorized. |
| **DMC-09** | Supported after locator correction. `G` and `R` formally declare200/422 only. Their422 references resolve to `HTTPValidationError` → `ValidationError`, not the prose envelope. Success data is required/nonnullable; errors is optional; ResponseCode is string. `WidgetResponse/anyOf` has no discriminator; defaults do not make type/status required. Failed payload exclusion is not structurally enforced by `additionalProperties:false`. These are publication differences, not observed malformed responses. |
| **DMC-10** | Supported. T13–17,718–745; C1,27–29 versus `G/description`, `R/description` and their security arrays. Bearer/session-only/no403/role scope conflicts with two-header/action/assignment prose; alternative security objects express OR. Approved archive retains both raw headers, exact/resource/explicit-wildcard UI matching, backend scope/authorization, no request ACL, bounded401 recovery without replay and403 without refresh. No chronology-based precedence or frontend role grant follows. |
| **DMC-11** | Supported after locator correction. T746–800,526; C29–31,22. No-store and fresh GET are documented; successful response headers are not formally declared. T788 makes event identity stable across publication attempts, not refresh-result idempotency. T794 preserves partial-failure audit success. T800 is fail-open business publication, while both operation descriptions permit audit-service503 and separately mention MPMM permission-check audit. The report correctly retains the possibility of different stages and does not certify a runtime contradiction, guaranteed accepted event or frontend telemetry mandate. |
| **DMC-12** | Supported. T3–28,214–240,833–854; C1–2,14–15,32–34, together with D-034/D-036/D-040 and MOS-1030. MOS-1030 spec7 explicitly forbids substituting the general dashboard or a local dialog selection for per-skill analytics; design3/13 retains the skill-ID/definition API gate. Monitoring, reports and dashboard remain distinct. No new scheduler, worker, aggregate-service owner or global missing-owner conclusion is created. |

## Closure and provenance assessment

Manually followed the selected operation references and their projected schema dependencies. Five direct reference occurrences resolve through the **26 schemas actually read**. The report correctly distinguishes that selected closure from the parent projection’s five-operation/34-schema/46-edge total.

Original capture, HTML extraction/roundtrip, hashes, original-pointer equality and acquisition/index claims remain **parent/metadata-attributed**. Reading the projection independently verifies its selected structures and reference destinations, not equality with a newly parsed original API document. Security-scheme definitions remain outside this closure.

D-040 accepts the corrected brief report while preserving its original REVISE review; no later reviewer ACCEPT is fabricated.

## Residual limits

No runtime behavior, numerical validity, final formula, audit delivery, source precedence, implementation ownership or feature delivery is accepted. All identified definition, auth, audit-stage and per-skill/report integration gates remain open.

Local read/find/grep inspection only. No browser/network, storage or credential access, requests/downloads, source execution/rendering, application-code audit, tests/build, nested delegation or repository edits. Tests were not run because this assignment prohibits them. No Git/index inspection or staging attestation.

**Global progress remains 6/28.**