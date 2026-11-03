# API-MOS-754-r2 — stub/banner contract and local-handler evidence

## Result and scope

**Bounded static evidence added; no backend-delivery acceptance.** Current combined and sectional contracts expose the four stub operations, and local Express handlers plus substantive test assertions exist. The local preview deliberately does **not** implement effective maintenance priority or inheritance. Neither these handlers nor their tests establish editor integration, scheduler behavior, deployed availability, or completion of MOS-754.

Only WAVE-D094 row **API-MOS-754-r2** was executed. MOS-754 remains **P**; **zero new U-to-P**. Candidates below are recommendations for parent review, not accepted queue entries or publication.

Repository-relative paths below use `A = openspec/changes/reconcile-control-center-backlog/audit`.

## Prior evidence and controlling corrections

Read before current implementation inspection:

- `A/reports/SCENARIO-MOS-922.md`, complete.
- `A/reviews/R-SCENARIO-MOS-922.md`, complete.
- `A/decisions.md:623–633`, **D-011**.
- `A/work-items/WAVE-D094-LOCAL-EIGHT.md`.

This report does not repeat the prior 14-candidate requirement audit. D-011 remains controlling:

1. Required body plus required `is_applied` makes absent body/`{}` schema-invalid. Flag-only shape does not establish business acceptance.
2. Only `target_type`, `is_applied`, and `query` filters are nullable; pagination parameters are optional, non-null bounded integers.
3. Prior “defer” means no action authorized by the audit—not approved product postponement or absent accountable ownership.
4. Prefix, update semantics, effective preview, error and concurrency questions remain unresolved.
5. Historical auth approval is neither reopened nor extended to these operations.

The archived `add-local-session-demo` proposal, design and all three delta specifications were read to preserve credential-free business mocks and the prohibition on interpreting mocks as backend authorization.

## Exact source and current boundaries

### Source pointers

- **Jira:** `A/sources/jira-operations-details/r1/content.json:43–60`, `/items/1`, key `MOS-754`.
  - `/description`, first two “Что делаем” bullets: catalog for assistant/module/skill/surface; full stub, substitute response and warning banner; read/change texts, target relationship, applied flag and preview information.
  - `/description`, DoD: contract and priority/transition rules or explicitly identified alternatives; examples.
  - Remaining maintenance-window requirements are acknowledged but **not audited in this seam**.
- **Previously accepted supplemental source:** `A/sources/wiki-241092242/r1/content.json`, `/bodyView`, §§1.2–1.3, 1.5, 2.1–2.4, 2.10–2.11. Semantic findings are inherited from SCENARIO-MOS-922 and its review, not re-audited.
- **Saved OpenAPI:** `A/sources/api-live/r1/content.json`, exact paths:
  - `/paths/~1api~1control~1api~1maintenance~1v1~1stubs~1catalog/get`
  - `/paths/~1api~1control~1api~1maintenance~1v1~1stubs~1{target_type}~1{target_id}/get`
  - Same path `/put`
  - `/paths/~1api~1control~1api~1maintenance~1v1~1stubs~1{target_type}~1{target_id}~1preview/get`
- **Current contracts:** identical selectors in `docs/api/contracts/openapi.json` and `docs/api/contracts/assistant-operations.openapi.json`.
- **Current explanation:** `docs/api/contracts/assistant-operations.md:5–21`.
- **Generated DTOs:** `app/shared/api/schema.d.ts:4735–4810`, `4960–4970`.
- **Normative boundaries:** `openspec/specs/control-center-http/spec.md:102–109`; `openspec/specs/control-center-mock-server/spec.md:23–67`; archived demo packet above.

### New evidence delta

Unlike the earlier scenario report/review, this inspection establishes:

- Structural comparison of all three current stub path objects and their **18-schema transitive closure**.
- Current combined and sectional stub operations and schemas match each other.
- All 18 referenced schemas match saved `api-live/r1`.
- The **only path-object differences** from saved r1 are security normalization on all four operations: two OR alternatives become one object requiring both tokens. This is consistent with the existing HTTP specification, not a new auth decision.
- Concrete local routing, validation, persistence-in-memory, preview implementation and actual test assertions are now located.
- The distinction between a schema-conforming local preview and production-effective output is directly supported by code and documented local conventions.

## Expected / observed / unknown

| Boundary | Expected evidence | Observed current evidence | Unknown or limit |
|---|---|---|---|
| Catalog and targets | J754 first catalog bullet; four target types and three texts | `mocks/stubs.mjs:4–26` constructs assistant ID `assistant` plus current modules, skills and surfaces; initializes nullable texts and false flag; preserves existing settings and refreshes target names. `:49–59` filters before `page()`. | No backend catalog population, target visibility or external freshness established. |
| Read and save | J754 second bullet; GET settings and PUT existing target | `mocks/stubs.mjs:28–35,60–79`: lookup returns 404 when missing; GET includes nested preview; PUT changes only present text properties, assigns required flag, updates timestamp and returns summary. | Local null clears and omission preserves are local conventions, not owner resolution of production semantics. No real durable storage established. |
| Input validation | Required body/flag, enum and query types from current schema | `mocks/app.mjs:62–79` installs contract validation before handlers. `mocks/contract.mjs:84–120,140–177` coerces booleans, validates parameters and body, returns 422 detail errors. | No new empty-string business prohibition exists in inspected stub handler/schema. Whitespace/clearing and previous live-text behavior remain owner questions. |
| Effective preview | Accepted prior source interpretation: server-effective output including applicable maintenance priority | `mocks/stubs.mjs:37–45,80–93`: applied flag selects `full_stub_text ?? substitute_response_text` and banner; otherwise null result/banner. Card source is explicitly `local-mock`; state is flag-derived normal/warning. | This is not production-effective priority resolution. It neither consults maintenance windows nor accepts unsaved editor input. |
| Audit metadata | Target relationship and change metadata | Initial `by.id` comes from `state.users[0]`; PUT updates `updated_at` but not `by`. Existing summary schema carries both. | Not evidence of authenticated editor attribution or “what changed” history. No backend audit-storage absence inferred. |
| Concurrency | Preserve unresolved prior contract questions | No stub version/precondition field appears in unchanged DTO. `mocks/app.mjs:85–99` excludes stub PUT from its selected idempotency operations. | No stale-write protection, idempotency or uncertain-result recovery guarantee established for backend. |
| Contract versus UI | Publication must not activate screens | `docs/api/contracts/assistant-operations.md` describes API, while `mocks/README.md:176–183` explicitly calls these HTTP mocks, not new UI integration. | Editor/client implementation is assigned to IMPL-MOS-922 and not audited here. |
| Scheduler | Maintenance and effective-output behavior are separate responsibilities | `mocks/README.md:182–183` expressly says no background scheduler and no production priority/inheritance simulation. | No scheduler or maintenance lifecycle implementation audit; no full MOS-754 DoD closure. |

**Important preview edge:** nullish selection means an empty full-stub string would take precedence over substitute text in this local handler. The schema has no minimum string length, and the handler adds no empty-string guard. This is a static local observation, not a recommendation to weaken the published empty-string rule or a claim that production accepts such input.

## Test evidence — assertions read, not executed

### `mocks/api-update.test.mjs:203–237`

Test: **“stub settings filter booleans, preserve nullable texts and follow renamed targets”**.

Assertions/readable sequence cover:

- Initial `is_applied=false`.
- PUT applied full text and warning banner.
- Renaming the underlying skill followed by a catalog query combining target type, applied flag and renamed text.
- Filtered total equals one and saved full text is returned.
- Dedicated preview banner equals saved banner.
- PUT false with explicit `full_stub_text:null`.
- Detail read confirms null clearing, omitted banner preservation and disabled nested preview banner null.
- True catalog becomes empty; false catalog remains nonempty.
- Invalid boolean and invalid target type return 422.
- Missing target returns 404.
- PUT without `is_applied` returns 422; subsequent full detail equals the prior snapshot.

The helper at `:8–26` asserts HTTP status and reads JSON; it does not independently schema-check each response.

### `mocks/contract.test.mjs:9–64,391–405`

The four stub operations are exercised through the shared `call()` helper, which resolves the matching operation and validates the successful response against its OpenAPI response schema.

Specific stub assertions establish:

- Saved full text is returned as `preview.result_message`.
- Filtered catalog target IDs equal the selected skill ID.

The surrounding maintenance requests do **not** assert that a maintenance window changes stub preview. They therefore cannot support effective-priority coverage.

### Explicit coverage limits

In these inspected stub assertions, no dedicated check establishes:

- Maintenance override, inheritance or tie-breaking.
- Substitute-only preview fallback.
- Empty/whitespace text behavior.
- Flag-only PUT business semantics.
- Stub-specific absent-body/`{}` behavior.
- Accurate writer attribution.
- Stub-specific pagination edges.
- Concurrent saves or production durability.

These are bounded observations about the inspected assertions, not a repository-wide claim that every such test is absent. No test suite was run.

## Bounded candidate dispositions

| Candidate | Disposition proposed to parent | Reason and ownership boundary |
|---|---|---|
| API754-r2-C01 — catalog/read/save publication | **Keep; update evidence** | Preserve existing source candidates. Add current combined/sectional equivalence, unchanged schema closure and handler/test locators. Publication is not backend acceptance. |
| API754-r2-C02 — preview authority | **Keep; update evidence** | Retain server-effective requirement. Record that local output is explicitly `local-mock`, not a maintenance-aware resolver or unsaved editor preview. |
| API754-r2-C03 — local update semantics | **Update existing question** | Null clears, omission preserves and false suppresses local output in concrete code/tests. These observations do not settle production draft/live-version semantics or authorize clearing policy. |
| API754-r2-C04 — provenance and edge assertions | **New bounded evidence note**, not a new product requirement | Record unchanged fixture `by.id`, nullish text selection, and the specific assertion gaps above. Parent may attach this to existing API-owner questions; do not infer a new audit endpoint. |
| API754-r2-C05 — prefix/errors/concurrency | **Keep questions open** | Current schemas and paths do not resolve previously accepted wiki-prefix, error-envelope or stale-write questions. No fallback, precedence or new protocol selected. |
| API754-r2-C06 — task completion | **No-op on closure/status** | J754 combines stub/banner and scheduler requirements. This seam is insufficient to accept its entire DoD; Review status is not acceptance. |

Only the parent may accept, queue or publish these dispositions. No candidate was registered or published by this run.

## Input hashes

SHA-256 computed from local bytes; hashes establish inspected inputs, not external freshness.

| Input | Bytes | SHA-256 |
|---|---:|---|
| `A/work-items/WAVE-D094-LOCAL-EIGHT.md` | 4247 | `da5e3681c7b882ef8fc6a44a50e7dd8562068f43ac4a74c71a8f5b82e61fd0e0` |
| `A/reports/SCENARIO-MOS-922.md` | 20266 | `705c767c60fba8e40bbb21de13fda1f2cf5ca6c22b4d03153a09923b1d31ff61` |
| `A/reviews/R-SCENARIO-MOS-922.md` | 14428 | `89620a68ccc0644948f33b7105c2122ca9a3dcbaad7f78e9462f8989a9f38d12` |
| `A/decisions.md` | 143407 | `dbf814a620a9ee1ff1435e912db50efb4672c3e40712f684855a14cc91df796e` |
| Jira operations r1 content | 9933 | `ecb2169e1a28ef91adcb0915cc1092443b03d2155e6cbc6545e82895ef8e140f` |
| Wiki 241092242 r1 content | 68316 | `e7b78965be979f2bd450b25881574cf7e8b94cf424be5d052bb2be9df1995158` |
| API live r1 content | 413007 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `docs/api/contracts/openapi.json` | 642329 | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `docs/api/contracts/assistant-operations.openapi.json` | 48374 | `08a20a68c35caa2ea3e136edcc6e928387978fbdcf1c4833bfc0d290be72cb4c` |
| `docs/api/contracts/assistant-operations.md` | 3058 | `94abf436ea63e56a584264721d4fa243c00e09eac7c1ab2780f0637008df879f` |
| `app/shared/api/schema.d.ts` | 424097 | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |
| `mocks/stubs.mjs` | 3356 | `766968f8229d564747bbc00251fcc8bb2d35963fb5dce37a26aae4de9f71aaf3` |
| `mocks/app.mjs` | 4866 | `b3dd41cc09a6aac9f6ffa023d4cd048fef75735926e1a8efa21b567c46d7efd0` |
| `mocks/contract.mjs` | 7223 | `ffca4d574568b6f81791279af6022a98077ac82f4e4ec90a672406261a383371` |
| `mocks/list.mjs` | 950 | `e1af394687dd92e656f0e0def06e3206a9eb217a43a5f366e6d410d622a34b7c` |
| `mocks/api-update.test.mjs` | 12330 | `793fb807cae6203c3d1336c15be1fd0b09d785b949e601a7dca75ee9c1e74ddb` |
| `mocks/contract.test.mjs` | 25896 | `a7096b8cf8ff74a162245ae96260cb282b09cdb21e278ccafaca298406c441d0` |
| `mocks/README.md` | 49365 | `ee00f203531ca8d30d2736d46919740e344b3d0fa2298235eeee4c6c69710259` |

## Historical, deployment and validation limits

- Jira metadata records capture at `2026-10-16T13:02:57.872Z`; selected issue is **Review**, updated `2026-10-16T19:22:17.361+0800`, with empty attachments and zero comments. Custom fields and attachment bodies were uncollected.
- Prior accepted provenance distinguishes wiki revision 4/body contract v1.0 from OpenAPI 3.1.0/service 0.1.0. This run did not refetch or re-audit those publications.
- Current supplemental documentation labels its source live OpenAPI dated 13.10.2026. That label is repository evidence, not a fresh deployment observation.
- Structural equality of stub schemas does not establish real request acceptance, authorization, effective output, scheduler execution or production rollout.
- No mandatory input was missing and no infrastructure failure occurred. One exploratory grep targeted a nonexistent top-level `tests` directory; the actual tests were subsequently located under `mocks`. This was a discovery miss, not a missing mandatory artifact.
- Validation consisted only of local reads/searches, SHA-256 hashing and structural JSON comparison. No application code was executed.
- No writes, network, browser, tests, build, lint, typecheck, Git inspection/mutation or nested agents. Index state was not inspected.
- Report returned for runtime persistence at the assigned authoritative output path; no report file was written by tools.