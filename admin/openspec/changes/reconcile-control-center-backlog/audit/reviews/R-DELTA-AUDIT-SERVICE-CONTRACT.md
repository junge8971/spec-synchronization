# R-DELTA-AUDIT-SERVICE-CONTRACT

## Review

**Disposition: REVISE — one chunk-locator correction only.** AUDIT-01–12 are substantively supported; no policy or implementation changes are warranted.

- **Correct:** The report preserves publication fail-open versus reader authorization fail-closed, unresolved dashboard503 applicability, separate service/browser identities, and MOS1031 acceptance gates.
- **Fixed:** None; read-only review.
- **Finding: P2 — incomplete chunk locator**, detailed below.
- **Merge verdict: OK with notes.** Apply the locator correction before documentary acceptance. **Global 6/28 unchanged.**

## Mandatory minimal correction

**Location:** `openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-AUDIT-SERVICE-CONTRACT.md:48`, AUDIT-05.

The row cites §3.1 and §5.3 with correct text ranges, but lists only **C6–8**. Those chunks cover publication; the stable logical-operation identifier and normalized-body hash rules occur in **C14**, with §5.3 beginning in C13.

**Smallest fix:** change its chunk locator to **`C6–8,13–14`**. Preserve the finding, disposition and text ranges.

Evidence: `content.txt:449–455`, particularly **453–454**; `body-view-chunks.json` entries **$[12]–$[13]**, physical lines **14–15**. This is a locator defect, not a substantive disagreement.

## Actual coverage and attribution

Aliases:

- **A** = `openspec/changes/reconcile-control-center-backlog/audit`
- **W** = `A/sources/wiki-241077434-readable/r1`
- **T** = `W/content.txt`
- **H** = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`
- **M** = `openspec/changes/mos-1031-skill-audit-history`
- **Cn** = one-based exact markup chunk; C1 is `$[0]`, physical line2.

Independently read:

1. Complete analyst report and both assigned work items.
2. **T1–480**, complete.
3. **All fifteen exact ordered markup chunks**, `$[0]–$[14]`, through physical lines1–18 in two reads. Tables, split-tag continuations, examples and the seven-item ordered question list were inspected inertly, not rendered.
4. Complete canonical and readable metadata and `W/envelope-index-projection.json`.
5. Before policy interpretation, complete H proposal, design and all six specs: API integration, HTTP, mock server, permissions, shell and MPMM session.
6. Complete M proposal, design, specification, tasks and `.openspec.yaml`.
7. Complete original metrics, board and team reviews; targeted corrected **DMC-11**, **BOARD-08**, **TEAMAPI-06** report passages; `A/decisions.md:1–32,225–244`; storage report passages `DELTA-MOS-1119.md:29–58` and `DELTA-MOS-1119-TESTPLAN.md:85–96`.

The exact local read of `docs/api/contracts/audit.md` returned **ENOENT**. This verifies an unavailable/stale plan pointer—not backend absence, an alternative document identity or permission to repair the plan.

Canonical-envelope parsing, original/projection equality, extraction, roundtrip and hash computation remain **parent/metadata-attributed**. I inspected the supplied projection, not an independently parsed canonical original. Prior dashboard/team/storage source audits were reused, not repeated. Saved dashboard API descriptions were **not freshly inspected**.

## Source identity and scope

Metadata and the parent projection identify wiki **241077434**, packet r1, page version **2**, timestamp `2026-09-07T19:22:13.762+08:00`, capture `2026-10-19T14:00:29.066Z`, HTTP200 and zero recorded redactions. T17 identifies contract **v1.0**.

The projected complete attachment index records status200, start0, limit100, size0, next null and results `[]`. This establishes only the **saved empty returned index**, not global attachment absence.

The four documented methods are:

| Method | Path under `/api/audit-service/api/v1` | Evidence |
|---|---|---|
| POST | `/events` | T148–251, C6–8 |
| GET | `/records` | T252–334, C8–10 |
| GET | `/records/{record_id}` | T335–385, C10–11 |
| GET | `/records/export` | T386–412, C11–12 |

This separate service base does not establish Control API routing, compatible credentials, deployment, availability or reader authorization.

## Candidate verification

| Candidate | Independent result |
|---|---|
| **AUDIT-01** | **Supported.** T3–24,440–448/C1,13 separate ingest and query consumers, credentials and guards. Ingest guard requires agreement; neither a TSAM permission mapping nor an object-scope algorithm is supplied. |
| **AUDIT-02** | **Supported.** T26–87,125–137/C1–6 distinguish record/event/service identity from historical employee subject. Employee requires employee_id; unknown omits it. Object ID is context-dependent, name is a snapshot, and denied/error require reason. No employee_id↔user_id/sso_id mapping or automatic-actor projection follows. |
| **AUDIT-03** | **Supported, including the tension.** T88–117,137,188/C4–7 require correlation_id and define optional trace/request IDs and opaque selection criteria/matched_count. T95 says criterion-read selection is permissible; T188 makes it conditionally required. Neither pagination total nor frontend telemetry is implied. |
| **AUDIT-04** | **Supported.** T118–124,259–270,330–332/C4–5,8–10 distinguish source occurrence time from receipt time, mandatory occurrence-time filtering, default received_at descending and chosen-sort-value+record_id keysets. Late-delivery caveats do not establish completeness, backfill or refresh timing. |
| **AUDIT-05** | **Supported after the chunk correction.** T148–251,449–455/C6–8,13–14 establish synchronous single-event publication, service-derived source_service, stable source/event key, normalized-body hash comparison, duplicate200 with original identifiers and conflicting409 without a new record. Publisher retries do not authorize business-mutation or refresh replay. |
| **AUDIT-06** | **Supported.** T259–270,311–334/C8–10 establish mandatory inclusive/exclusive occurrence interval, optional filters, object-ID-with-type, default50/max200, unchanged filters/sort for cursor traversal and no total. T476/C15 explicitly leaves maximum page size unresolved. M design13–17 and spec9–27 require type+skill-ID on every UI page despite the broader service query. |
| **AUDIT-07** | **Supported.** T335–385,468–469/C10–11,15 define full detail,404/401/403/503, append-only public methods and internal retention deletion. Expired operational records and archive exclusion do not settle retention deployment or sensitive-field redaction. |
| **AUDIT-08** | **Supported.** T386–412,475–477/C11–12,15 define identical search filters and mandatory interval, no limit/cursor, synchronous CSV/JSONL file success, JSON errors, Content-Type distinction and pre-construction413 cap enforcement. Numeric cap and final column requirements remain open; report-worker/download-job semantics are not adopted. |
| **AUDIT-09** | **Supported.** T247–251,456–467/C8,14–15 distinguish publisher fail-open from reader fail-closed access decisions. Publisher401/403 alerting and sent/accepted metrics belong to the source service. Audit-reader ACCESS_CHECK_UNAVAILABLE does not identify the dashboard’s audit-unavailable stage or resolve DMC-11 applicability. |
| **AUDIT-10** | **Supported.** T254–256,333,336–338,388–390,442–448 and H HTTP/session/permissions preserve the integration mismatch: source Bearer prose is not approved raw-X-header transport or credential-destination authorization. Service-auth alternatives are not browser credentials. Explicit-* audit UI visibility does not activate a reader or confer global data scope. |
| **AUDIT-11** | **Supported.** T125–146,478–480/C5–6,15 provide stable action vocabulary, not a complete producer/reader mapping. Reused BOARD-08 explicitly has iam_id; this source has sudir_id. They are not established aliases. TEAMAPI-06 and D-016/017 establish neither journal publication nor a lossless storage/event projection. |
| **AUDIT-12** | **Supported by actual source inspection.** T65/183 reference nonexistent §2.5; actual action naming is §2.4. T146 references7.5 for catalog ownership, but item5 concerns self-audit. T334 references7.6 for protected journal reading, but item6 concerns changed attributes. These defects and the selection/page-limit tensions remain unresolved. |

All seven source questions were checked in **T474–480/C15**:

1. Publisher authentication mechanism.
2. Operational/archive retention.
3. Search-interval, page and export limits.
4. Export columns/order.
5. Journal self-read/export auditing.
6. Old/new attribute values.
7. Sufficiency of a relation object for two-object actions.

The report correctly attributes the missing publication component/self-audit behavior to source prose, not observed implementation.

## Preserved acceptance boundaries

D-049 accepts corrected metrics candidates after eight locator fixes while preserving the original **REVISE** review; it does not invent a later reviewer ACCEPT. Board acceptance and D-048 team acceptance are retained. D-016/017 preserve storage-versus-reader distinctions and MOS1031 ownership.

The source narrows the documentary availability gap only. MOS1031 still requires accepted routing and credential destination, backend reader authorization, wire identity/event projection, DTO/error handling, safe details/redaction, period/retention reconciliation, pagination and event-consistency behavior. Its unchecked tasks and unavailable-before-acceptance gate remain unchanged.

Publication may continue while reader access is closed. This neither guarantees accepted events nor proves that dashboard503 is the same dependency failure. No source precedence, new role model, permission, reader activation or frontend event generation follows.

## Limits

Local read/find/grep only; no repository edits. No browser/network, storage or credential inspection, requests/downloads, rendering/source execution, application-code review, tests/builds or nested delegation. Tests were intentionally not run under this assignment. No acquisition, hash-recomputation, Git/index or staging attestation.

**Global progress remains 6/28.**