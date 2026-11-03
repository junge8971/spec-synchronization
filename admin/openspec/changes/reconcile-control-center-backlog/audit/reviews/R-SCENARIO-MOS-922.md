# Code Context

## Independent review R-SCENARIO-MOS-922

**Verdict: REVISE (bounded wording/contract precision), not implementation authorization.** All 14 candidates have material source support. Hashes, publication versions, prefix discrepancy, server-effective preview, response differences and conservative auth boundaries independently check out. Corrections below prevent an audit boundary becoming a product deferral and distinguish schema-invalid empty input from genuinely unspecified update semantics. No reporting blocker; no precedence, task closure, endpoint activation or runtime acceptance established.

## Files Retrieved

Repository-relative paths; `A` means `openspec/changes/reconcile-control-center-backlog/audit`.

- `A/work-items/R-SCENARIO-MOS-922.md` (1–3); `A/reports/SCENARIO-MOS-922.md` (1–144): assignment and reviewed report, especially candidate table 41–54, schema discussion 67–74 and ownership 88–94.
- `A/sources/jira-operations-details/r1/content.json` (43–60, 79–96; JSON `/items/1`, `/items/3`), `metadata.json` (1–42): backend contract task and explicit MOS-922 behavior.
- `A/sources/wiki-241092242/r1/content.json` (1–64, `/bodyView` at 39), `metadata.json` (1–54): general/business rules, §§1.2–1.3, 1.5, 2.1–2.4, 2.10–2.11, version history; §2.9 cancellation influence only. HTML parsed as inert text. An extraction boundary mismatch incidentally displayed maintenance model/form sections; those were not audited or used to expand scope.
- `A/sources/api-live/r1/content.json` (line 1): three `/api/control/api/maintenance/v1/stubs/…` paths (four operations), full transitive schema closure, `/components/securitySchemes`, `/openapi`, `/info`; `metadata.json` (1–19).
- `A/reports/LOCAL-001.md` (1–173): discovery guide only. Fresh enumeration and literal scan of exactly `openspec/changes/*/proposal.md` (21 files) and `openspec/specs/*/spec.md` (40 files); no dedicated MOS-922 proposal/spec found by these selectors. Archive/product internals not exhaustively searched.
- `openspec/specs/control-center-http/spec.md` (1–138), `openspec/specs/control-center-permissions/spec.md` (1–91), `openspec/specs/control-center-shell/spec.md` (210–241); discovery additionally located shell lines 156, 187–189 for stubs canonical tab/UI policy.
- Auth prerequisites, read before security conclusions: `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md` (1–38), `design.md` (1–171), `specs/control-center-api-integration/spec.md` (1–64), `specs/control-center-http/spec.md` (1–71), `specs/control-center-mock-server/spec.md` (1–27), `specs/control-center-permissions/spec.md` (1–89), `specs/control-center-shell/spec.md` (1–101), `specs/mpmm-session/spec.md` (1–138); `tasks.md` (43–52) for historical confirmation.
- Demo prerequisites: `openspec/changes/archive/2026-10-09-add-local-session-demo/proposal.md` (1–28), `design.md` (1–70), `specs/control-center-mock-server/spec.md` (1–106), `specs/control-center-shell/spec.md` (1–55), `specs/local-session-demo/spec.md` (1–123). No demo implementation inspected.

## Key Code / primary evidence comparison

No application code inspected. `J` = selected Jira description; `W` = wiki `/bodyView` section; `O` = saved OpenAPI selectors above.

| Candidates | Independent verification |
|---|---|
| C01–C04 | J `/items/3/description` explicitly names four target types and three text fields. W §§1.2–1.3 agrees; O `MaintenanceTargetType`, `StubSettingsSummaryResponse` require corresponding enum and nullable text fields. Retain candidates; “Defer” is not sourced approval. |
| C05 | J explicitly says inline editor saves an existing record. W §§2.2–2.3 and O settings GET/PUT support read/update, not a create/upsert/delete promise. |
| C06–C07 | J and W §2.3 explicitly distinguish false=draft from true=immediate application subject to maintenance priority. Neither describes preservation/removal of previously live text when saving false, separate persisted live/draft versions, or activation success from the returned flag alone. |
| C08 | J and W §2.4 require effective server-priority output. O preview GET has only target path parameters, no draft body/sample-message query. Local unsaved input cannot be represented as this server result. |
| C09–C10 | W business rules and §1.5 publish active-window override, larger priority, specificity surface > skill > module > assistant, then later updated_at; completed windows do not influence output. §2.9 states canceled windows stop influencing output. Exact ties after all criteria and cross-target applicability remain questions, not a client algorithm. |
| C11 | W §2.1/O catalog GET expose target_type, is_applied, query (target name), limit/offset and server pagination. O limit 1–100 default 20, offset >=0 default 0. No sort or target-directory operation established. |
| C12 | W §2.3 permits one/several/all texts and forbids empty string. O UpdateStubSettingsRequest requires is_applied; texts optional/nullable with no string minimum. This documents a publication constraint gap, not backend acceptance of invalid input. |
| C13 | W business rules say who/when/what; O summary has by.id/updated_at but no explicit change-delta/history field. Gap is in inspected representation, not proof backend lacks audit storage or that a new history endpoint is needed. |
| C14 | W §2.11 restricts collections and specifies inaccessible-object 404. Role table is publication evidence, not approved frontend grants. Current permissions spec lines 25–38 and 79–91 retain wildcard-only unmapped UI and backend object authority. |

### Confirmed material differences and preserved limits

- W base `/api/control/api/assistant-ops/v1` versus O `/api/control/api/maintenance/v1`: unresolved publication discrepancy, not alias/fallback/precedence evidence.
- W §§1.2/2.2 uses stable `assistant` key and UUIDv7 for other targets; O `target_id`, `StubTargetResponse.id`, and `ByResponse.id` are strings without those formats. Missing schema constraints do not prove backend accepts arbitrary identifiers; do not convert assistant into a UUID.
- O PUT 200 is `TsamResponseSchema_StubSettingsSummaryResponse_`, not preview. Settings GET adds nested `StubPreviewResponse`; dedicated preview returns `StubPreviewCardResponse`. Acknowledged save and failed subsequent preview/readback are different outcomes. No atomicity/freshness or polling guarantee is published.
- O nested preview fields are required nullable; W §1.3 marks them optional. O card state is normal/warning; source is a string, not a one-value enum inferred from W example `maintenance_window`.
- W §2.10 lists stub-relevant 400/401/403/404/409/422, including STUB_TARGET_CONFLICT for changed/incompatible target. O declares 200 and HTTPValidationError 422; its detail[] differs from W errors envelope. Undeclared statuses are not impossible statuses. No expected_version, If-Match, idempotency header or stale-write protocol is specified on these O operations; updated_at is not a precondition. Preserve explicit recovery and no automatic mutation replay without inventing fields or idempotency guarantees.
- O security OR conflicts with both scheme descriptions requiring both raw tokens. Approved auth design lines 145–147 explicitly authorizes OR→AND normalization; current HTTP lines 23–27 retains both headers and forbids transport permission ACL. Keep this correction, not a new negotiation to weaken auth.
- Current wildcard-only policy is UI visibility, not a recommendation to grant wildcard, a backend role model or runtime availability. Demo full profile likewise does not implement missing APIs (archived demo spec lines 56–59). Mock fixtures/scenarios do not attest real authorization.
- Auth tasks line 52 records user confirmation dated 09.10.2026 and explicitly no agent real-backend testing. Preserve this historical approval with its scope; neither invalidate it because this review did not test runtime nor extend it to stub runtime acceptance.

## Required correction candidates

1. **Report lines 41–44, 51, 88: replace ambiguous “Defer”.** Suggested wording: “Retain explicit source candidate; dedicated product-spec ownership/placement unresolved within the bounded discovery; this audit does not authorize implementation or establish an approved product deferral.” No dedicated active packet found is not “no owner,” product exclusion, or approval to postpone MOS-922. Jira already identifies FE/backend task routing; named responsible people and plan ownership are not established by the selected records. C07 activation and MOS-923 separate audit boundaries should be explicitly labeled audit scope, not approved product deferral.
2. **Report line 71: split empty request from flag-only semantics.** O settings PUT `/requestBody/required` is true and `UpdateStubSettingsRequest/required` is `["is_applied"]`: absent body or `{}` is schema-invalid, not unspecified at the publication level. `{ "is_applied": false }` meets declared required-property shape, but business behavior still needs confirmation. Omission versus null, empty string versus whitespace, clearing, and previous live text remain open; schema-valid does not establish backend acceptance.
3. **Report line 73: narrow “Optional query schemas allow null.”** Only target_type/is_applied/query use nullable anyOf. limit and offset are optional but non-null integer schemas. Suggested wording: “The three optional filters are nullable in O; pagination parameters are optional non-null bounded integers. Do not serialize absent filters as literal null/undefined.”

These are report corrections, not authority to edit product specs or create a change.

## Architecture / owner questions

Existing owners cover cross-cutting boundaries, not the library/editor itself: HTTP spec lines 9–27 and 63–109 own request/error/auth/non-activation behavior; permissions lines 25–38, 60–91 own UI policy and server scope; shell line 218 owns honest unfinished content. Shell lines 156, 187–189 additionally own canonical stubs-tab routing and access, not business-library completeness. The fresh scan supports only “not found in direct active proposals/main specs by MOS-922/заглуш/stubs,” not repository-wide absence or absent product ownership.

Retain report questions to MOS-754/API and MOS-922/product owners: agreed prefix; omission/null/clearing and required flag; draft versus previous effective text; effective preview labeling and readback failure; error shape/stale writes/uncertain outcomes; exact remaining ties/applicability. Permission owner must confirm granular mapping separately. No owner answer is required to complete this evidence review; answers are required before resolving those product/contract ambiguities. No actual blocker required escalation.

## Provenance verification

Fresh SHA-256 over saved content bytes matched metadata:

| Source r1 | Bytes | SHA-256 |
|---|---:|---|
| jira-operations-details | 9933 | ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f |
| wiki-241092242 | 68316 | e7b78965be979f2bd450b25881574cf7e8b94cf424be5d052bb2be9df1995158 |
| api-live | 413007 | 549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06 |

Jira MOS-754 Review/MOS-922 Backlog, respective updated timestamps 2026-10-16T19:22:17.361+0800 and 2026-10-15T14:46:44.693+0800, zero selected comments/attachments match. Wiki page revision 4 (2026-09-25T16:59:13.813+08:00) differs from body contract v1.0/history 10.09.2026. OpenAPI 3.1.0 differs from service 0.1.0 and capture r1. Capture timestamps/origins match report; collection provenance is metadata testimony, not a fresh fetch. No ETag/Last-Modified or business approval inferred.

## Start Here

Revise the reviewed report's candidate dispositions and lines 71/73 using the three narrow corrections above. Then retain unresolved API/product questions without selecting publication precedence or activating UI.

## Limits

Read-only local JSON/hash/schema inspection and inert HTML parsing; no source/runtime/code audit, maintenance-form audit, network/MCP/browser, tests/build/generation, git/index inspection or mutation. Sole intentional repository write is this review. Initial auth directory lookup failed because the required packets are archived; archived packets were then located and read. No index-state assertion.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent primary-evidence comparison verifies all 14 candidates and three source hashes; three exact report corrections and bounded residual questions recorded."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-922.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python SHA-256/JSON inspection and transitive stub schema traversal","result":"passed","summary":"All three saved-byte hashes matched; four operations and referenced schemas inspected."},
    {"command":"Inert HTML text extraction and scoped proposal/main-spec discovery","result":"passed","summary":"14 candidates checked; 21 direct proposals and 40 main specs scanned; incidental maintenance text not audited."},
    {"command":"Tests/build/network/browser/git","result":"not-run","summary":"Forbidden or outside bounded review."}
  ],
  "validationOutput": ["Verdict REVISE: clarify audit-only deferral, explicit empty-body schema invalidity, and nullable filter versus pagination distinction."],
  "residualRisks": ["Prefix, update/null/draft semantics, preview freshness, concurrency/errors and granular grants require owners; no runtime verification.","Discovery does not establish repository-wide absence, no owner or approved product deferral."],
  "diffSummary":"Only the authoritative review report written; no product/source/code edits.",
  "reviewFindings":["revise: report lines 41–44/51/88 ambiguous defer disposition","revise: report line 71 empty body is schema-invalid, not unspecified","revise: report line 73 nullable query claim excludes limit/offset"],
  "manualNotes":"Auth and demo proposal/design/delta specs read before security conclusions. Historical approval retained without runtime attestation; no index-state claim or writer authorization. No reporting blocker."
}
```
