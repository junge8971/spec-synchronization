# Code Context

## DELTA-SKILL-MONITORING-EXAMPLE — bounded documentary supplement

**Result:** This compact example fills a historical root-documentation inventory gap and supplies concrete monitoring field descriptions, not an approved/current API, runtime verification or health policy. Existing routes remain MOS-1025 (metrics/freshness) and MOS-1026 (operational details). Findings are report-local, pending review; no new plan, feature activation or closure.

## Files Retrieved

Paths are repository-relative; `A` means `openspec/changes/reconcile-control-center-backlog/audit`.

- `A/work-items/DELTA-SKILL-MONITORING-EXAMPLE.md:1–11`: complete assignment.
- `A/sources/wiki-241074633/r1/metadata.json:1–21`: complete metadata; packet r1, source v4, version time `2026-09-08T17:41:04.581+08:00`, captured `2026-10-19T10:18:28.344Z`.
- `A/sources/wiki-241074633-readable/r1/content.txt:1–136`: complete body, called **B** below; `body-view-chunks.json:1–9`: all seven ordered HTML chunks, including response/table context; `metadata.json:1–14`: complete derivation metadata.
- `A/sources/wiki-241074633/r1/content.json:13,18–19`: targeted attachment-index search observed `next: null`, `results: []`. Canonical body not independently roundtripped or hashed.
- `A/inventory.json:410–474`: existing MOS-1025/1026/1030 routes.
- `A/decisions.md:1–17,147–164`: D-033 capture, D-032 assessment relevance and D-014 accepted monitoring corrections.
- `A/reports/SCENARIO-MOS-1397.md:1–205`: complete prior monitoring report, MOS1397-C01–C14. Its API-r1 absence findings remain historical.
- `A/reports/REL-D031-MPMM-ASSESSMENT.md:1–84`: complete prior assessment relevance report; only operational-assessment comparison used.
- `openspec/changes/mos-1025-skill-monitoring/specs/skill-monitoring/spec.md:1–47`, `design.md:1–26`: metrics/freshness owner and conditional API gate.
- `openspec/changes/mos-1026-skill-operations-info/specs/skill-operations-info/spec.md:1–47`: operational owner, read-only and source states.
- `openspec/specs/control-center-api-integration/spec.md:73–112`: approved truthful-contract and unavailable-state requirements.

## Key Code / documentary evidence

No application code inspected. Values below are examples, not measurements or guarantees. Table rows refer to named tables in **B**, corroborated by all exact HTML chunks.

| Stable finding | Substantive coverage and exact locators | Existing route / bounded comparison |
|---|---|---|
| SME-01 — status | B:31–32,96–99; `monitoringStatus` rows 1–2: string `status="normal"` and `statusDescription` claiming thresholds respected, systems responding, timely updates. Response fields are top-level; table heading does not establish a wrapper. | MOS-1025, MOS1397-C05–C07. No enum, priority, equality, null/zero or insufficient-sample semantics follow from one healthy example. Do not rename schema or map `normal` automatically to requested `evaluated`. |
| SME-02 — daily metrics | B:33–40,100–107; `dailyMetrics` rows 1–6: float availability value/threshold `0.996/0.995`, float mean response value/threshold `1.1/3` seconds, float good-rating share/threshold `0.88/0.85`. Tables explicitly say availability/rating 0..1 and “Показатели за сутки”. | MOS-1025, MOS1397-C02/C05. Adds documentary units and daily scope; prior requested backend settings use 0–100 for availability/rating. Representation difference is not permission to convert current contracts. Day boundaries/timezone, rolling/calendar window, denominators, aggregation, sufficient sample, equality and maintenance exclusion remain unspecified here. Not SLA/uptime evidence or MOS-1030 30-day analytics. |
| SME-03 — service freshness | B:41–47,108–114; `serviceInfo` rows 1–5: string `dataUpdatedAt=2026-08-14T07:45:00+03:00`, integer `dataAgeDays=24`, string `updateReglament="ежедневно до 08:00"`, string `lastCallAt=2026-08-14T09:52:00+03:00`, resident-facing `failureMessage` about technical works and hotline/mos.ru form. | MOS-1025 freshness/MOS-1026 operational context, MOS1397-C08. Separate update/invocation dates agree with MOS-1025 spec:21–28. No as-of timestamp reconciles age 24 with “timely”; unresolved sample context, not proof of a stale incident. Offset examples do not define all date/timezone rules. Schedule is neither polling cadence nor maintenance window; fallback text does not prove a current failure. |
| SME-04 — people/dependencies | B:48–66,115–125. `responsiblePersons` rows 1–3: string owner Феофан Терентьев, technical representative Герасим Кочетов, deputy Епифаний Ефимов. `dependencies` rows 1–4: string name/team/status/checkedAt; ЕИРЦ meter readings and МОЭК outage register both have Команда ЖКХ, `Доступна`, `2026-08-14T09:40:00+03:00`. | MOS-1026, MOS1397-C03/C08/C09, D-014. Illustrative skill responsibilities are not accountable implementation owners, identities or grants. No IDs, contact channels, multiplicity/missing-deputy policy, dictionary codes or live-check cadence. Dependency check time differs from invocation/data update. |
| SME-05 — incident | B:67–79,126–136; `incidents` rows 1–9: `P1`, delays after outage-register update, float `impact=0.06` explicitly 0..1 influence share, occurrence `2026-07-29T11:20:00+03:00`, skill-configuration cause, platform-team side, resolved status, resolution `2026-07-29T12:40:00+03:00`, example `postmortem="готов"`. Table row 9 instead names string `condition`, example `разбор: готов`. | MOS-1026, D-014/MOS-1146 corrections. **Internal example/table key mismatch**, not an approved schema rename. No influence denominator, severity/status dictionary, resolution deadline, responsible individual, incident ID or external incident URL. Side is not a person; resolution time is not deadline. No live integration/editor follows. |
| SME-06 — envelope/failures | B:1–29,80–94: documentary POST `/api/esk/skills/{id}/monitoring`, required path ID example `s-water`; request-body `sudir_id`/`access_token` comments allowing anonymous null; 200/422/500 examples, errors with `error_type`/`error_message`. | Existing API/product route through MOS-1025/1026; accountable people unknown. Error examples do not define retries, partial failure or empty/unavailable/not-connected states. No request execution, token retrieval, endpoint adoption or session-policy change. Null comments concern historical request fields, not monitoring-result nullability. |

## Architecture / bounded comparison

**Historical gap, not gate closure.** D-033 records newly captured root documentation; D-032 accepts relevance only. This body strengthens the existing metrics/operational evidence, especially units and separate timestamps, without closing integration gates. Approved `openspec/specs/control-center-api-integration/spec.md:77–104` requires agreed and connected contracts, visible unavailable explanations and no synthetic health data. Documentary use agrees with that boundary; treating sample numbers/POST as runtime truth would conflict. No inspected approved clause requires this POST or these camelCase keys. Current API r2 exists but was not inspected; prior API-r1 absence claims remain historical/unverified for current publication, never backend absence.

**Assessment is not checking.** D-032-accepted report section `238324852 — Ассессмент навыков` cites source v8 text:1–26,42–58 for operational review of monitoring, thresholds, dependencies, incidents, responsible parties and planned windows, with unfinished scenarios and incident/communication questions. This example supplies information for that subset only: no assessment decision, disablement, concierge redirection, reassessment, planned-work period/reason, dialog investigation or incident-recording workflow. It does not merge operational health with skill checking/publication review. Those contracts/owners were not inspected here.

**Unresolved within existing routes:** accepted representation and incident key mismatch; metric windows/timezones/aggregation/sample sufficiency; freshness as-of/stale criteria; refresh, source failure, partial availability, empty/null semantics; contact identity and incident provenance. These are documentary questions, not new implementation tasks. Prior MOS1397 priority, equality and maintenance rules remain attributed to accepted prior evidence, not supplied or overridden by this example. No date-based precedence, external credentials, live incident integration or runtime SLA inference.

## Start Here

Review **B:96–136** alongside MOS-1025 spec:7–47 and MOS-1026 spec:7–47. Preserve existing owners and gates; no new frontend owner is inferred from sample people or teams.

## Coverage, validation and residual risks

Complete 136-line body, metadata and seven HTML chunks read locally; empty returned index observed. Hash/integrity/roundtrip claims remain parent-attributed, not independently verified. Body coverage is not coverage of current API r2, backend/runtime, auth/session, checking/review, unrelated owners or linked sources. Historical proposals may differ from approved contracts; sample inconsistencies and unspecified policies remain open.

Only this report written. No network/browser, source/sample execution, credentials/business calls, tests/build, application-code scan, nested delegation, source/main-spec/archive edits or global closure. Local `wc -l` verified cited file extents. Git/index state uninspected; no staging performed, not an empty-index attestation.
