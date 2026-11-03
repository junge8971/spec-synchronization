# R-D094-EIGHT — independent review

## Verdict

**ACCEPT all eight reports as bounded local evidence. Mandatory report corrections: none.**

Acceptance is not publication authorization, feature completion, backend acceptance or deployment proof. Parent retains acceptance/register/queue ownership.

All eight members were already P: **zero new U→P**. Preserve **89P/1B/83U**, total 173, and global **11/28**.

`A` below denotes `openspec/changes/reconcile-control-center-backlog/audit`.

| Report | Verdict | Candidate disposition |
|---|---|---|
| API-MOS-717-r2 | **ACCEPT** | Attach structural comparison and existing supplemental-document ownership to existing candidates. Retain contract-status/«Неактуально» questions. No duplicate documentation task. |
| API-MOS-754-r2 | **ACCEPT** | Attach contract/mock evidence to existing stub candidates. Keep effective preview, production update semantics and concurrency questions unresolved. |
| IMPL-MOS-922 | **ACCEPT** | Retain placeholder-versus-contract/mock distinction. Merge overlapping stub evidence with API-MOS-754-r2 rather than publishing another evidence-only product item. |
| IMPL-MOS-1146 | **ACCEPT** | Retain D-082 owner correction as already installed. Attach ordering and dictionary-provenance observations to existing incident candidates; no new owner or editor. |
| IMPL-MOS-1397 | **ACCEPT** | Preserve skill-scoped source and conditional-write gates. Analytics comparison is a bounded exclusion, not a global-settings requirement. Existing owner-plan no-op stands. |
| IMPL-MOS-1398 | **ACCEPT** | Retain responsibility API gate and existing read-only owner. Primary contact is not assignment integration. No replacement-write protocol or editor inferred. |
| IMPL-MOS-1145 | **ACCEPT** | Attach static client/mock/test evidence to existing C/TP candidates. Preserve historical approval and exact mock/test-plan differences without automatic remediation. |
| IMPL-MOS-1027 | **ACCEPT** | Retain mounted skill-card ownership and approved MVP. Impact/duration remain existing scope questions; no duplicate `/ops` toggle plan. |

## Independent checks

All eight completed reports and the wave assignment were read. Review concentrated on their material new claims, controlling review corrections, selected saved source objects, current contracts, connected code and actual assertions—not a fresh requirement audit.

### Contract equality: MOS-717 and MOS-754

Independent parsed-JSON comparison confirmed:

- `docs/api/contracts/assistant-modules.openapi.json`: **five path objects** equal their merged-contract counterparts.
- All **26 standalone module schemas** equal corresponding merged and saved `api-live/r1` schemas.
- Every module operation differs from saved r1 only in its `security` property.
- `assistant-operations.openapi.json`: **three stub path objects/four operations** equal merged counterparts.
- The stub operations’ **18-schema transitive closure** equals merged and saved-r1 definitions.
- Every stub operation differs from saved r1 only in `security`.

These are structural equality claims, not whole-document byte equality. The agreed OR→AND security normalization remains approved; it is neither a new discrepancy nor runtime-enforcement proof.

`docs/api/contracts/assistant-modules.md`, **Ограничения источника**, already documents missing business semantics and mock/backend separation. A new “missing documentation” task would duplicate existing ownership.

### Stub/editor boundary: MOS-754 and MOS-922

Verified against:

- `mocks/stubs.mjs:4–25,37–45,67–93`;
- `mocks/api-update.test.mjs:203–237`;
- `mocks/contract.test.mjs:391–404`;
- `app/pages/operations/ui/operations-page.tsx:6–29`.

Findings support both reports:

- The mounted operations content is a placeholder.
- Mock settings persist in memory; supplied null clears, omission preserves.
- Preview uses `full_stub_text ?? substitute_response_text`; an empty full-stub string therefore takes precedence.
- Preview does not inspect maintenance windows or unsaved editor input.
- Author starts from `state.users[0]`; saving updates time, not author.
- Tests assert selected filtering/save/null/preview behavior, not effective maintenance priority or accurate writer attribution.

These observations do not convert agreed mock simplifications into production defects or authorize weaker production validation. The historical empty-string constraint question remains unresolved.

**Queue integration:** API754-r2-C04 and IMPL922-E01 should be attached to existing candidates, not become separate evidence-only publications.

### Incidents: MOS-1146

The saved source `jira-monitoring-details/r1/content.json#/items/1/description` explicitly requests status grouping and descending detection time, dictionary-backed active-code validation, and read-only public access.

Current evidence supports the reported limitations:

- `mocks/skill-operations.mjs:100–108` filters by skill without sorting.
- `:63–84` checks skill existence and percentage range, but not dictionary membership/activity.
- `mocks/api-update.test.mjs:163–201` and `mocks/contract.test.mjs:378–389` use `critical`/`backend` and only one incident.
- Those fixtures do not demonstrate dictionary provenance or ordering. Different seed codes alone do **not** prove invalidity in an extensible dictionary.
- The D-014 nonstandard percentage annotations remain attached to the non-null union, not misrepresented as standard numeric constraints.

**Read-order deviation:** disclosed and not retroactively cured. Nevertheless, the substantive D-082 evidence is preserved: the report recognizes existing GET/DTO/mock support, the installed owner correction, and the still-open broader UI gate. No repeated blanket-contract-absence correction should be queued.

### Monitoring settings: MOS-1397

`jira-monitoring-details/r1/content.json#/items/2/description` unmistakably specifies **skill-scoped** settings and explicitly conditional writes.

Independent contract inventory confirmed **94 paths/380 schemas**. Bounded identifier searches corroborated the absence of monitoring/threshold identifiers in the inspected app/mock/contract boundaries.

`mocks/analytics.mjs:70–105` and `mocks/contract.test.mjs:427–450` concern dashboard refresh and board widget composition, not threshold persistence or dependency synchronization.

The report correctly refuses to derive a global editor from the wave wording. Its “global metric-settings boundary” title is potentially easy to skim incorrectly, but the result and candidate table expressly resolve that ambiguity; no mandatory correction is needed.

**Read-order deviation:** later reading of the observability review remains disclosed. D-082’s monitoring no-op, documentary questions and conditional-write gates survive substantively. Do not turn IMPL1397-04 into a new global-policy requirement.

### Responsibility assignments: MOS-1398

The selected source `/items/3` supports separate assignment identity, nullable enrichment/provenance, unchanged-pair preservation and conditional replacement writes.

Verified current boundaries:

- `app/entities/skill/api/skill-details-client.ts:15–50` validates one primary contact, not assignments.
- Its loose object schema does not imply rejection of every unknown field.
- `skill-details-tabs.tsx` and `tabs/overview-tab.tsx` do not compose an assignment block.
- Bounded contract/mock searches do not establish responsibility endpoints or provenance.
- Unrelated surface-registration `responsibles` identifiers do not contradict the skill-assignment finding.

D-014’s corrections remain intact: unchanged **`(role,user_id)` pairs**, **at most one** enrichment request per unique user, and backup/prod **scope tension**, not removal of prerequisites.

### Toggle implementation: MOS-1145 and MOS-1027

Verified against the command client/schema, handlers, current toggle specification, mock handler/idempotency implementation, client assertions and selected mock assertions.

The reports correctly distinguish:

- Dedicated commands from substitute-text saving and generic lifecycle mutations.
- Trimmed frontend validation from direct mock length-only validation.
- Matching receipt validation from an action-conditioned target-status guarantee.
- Confirmed mutation followed by failed GET from command rejection.
- Local predecessor-map restoration, including default `draft`, from backend restoration guarantees.
- Fixture actor/in-memory histories from authenticated provenance and durable audit.
- Mutation-before-`sendSuccess` response validation from transactional rollback.
- Mock `409 INVALID_STATE` versus historical test-plan `422 VALIDATION_ERROR`.
- Mock `IDEMPOTENCY_CONFLICT` versus historical `IDEMPOTENCY_KEY_REUSED`.
- JSON-stringified-body replay caching from durable/distributed idempotency.

Locators: `mocks/skill-operations.mjs:5–40`, `mocks/idempotency.mjs`, `mocks/contract.mjs:180–197`, attachment835759 `content.md:169–322`, and `mocks/api-update.test.mjs:66–117`.

The client test **“sends only the published %s request”** indeed permits a disable receipt with known `prod` status/null fallback; the reports appropriately describe structural validation rather than semantic transition proof.

The current toggle specification explicitly excludes durations and surface lists and preserves the **13.10.2026 approval without claiming an integration run**. Neither report reopens that approval or the historical **09.10.2026 auth approval**.

## Source status and historical cutoff

Selected pointers and saved statuses agree with the reports:

| Source pointer | Saved status |
|---|---|
| Operations `/items/0` — MOS-717 | CLOSED |
| Operations `/items/1` — MOS-754 | Review |
| Operations `/items/3` — MOS-922 | Backlog |
| Monitoring `/items/1` — MOS-1146 | Ready for test |
| Monitoring `/items/2` — MOS-1397 | Development |
| Monitoring `/items/3` — MOS-1398 | Backlog |
| Skill-switch `/items/1` — MOS-1145 | Ready for test |
| MOS-774 details `/items/15` — MOS-1027 | Ready for test |

Historical captures remain:

- Operations: **2026-10-16T13:02:57.872Z**.
- Monitoring: **2026-10-16T13:48:06.559Z**.
- Skill-switch: **2026-10-16T13:58:59.883Z**.
- MOS-774 details: **2026-10-16T11:49:06.782Z**.
- API r1: **2026-10-16T11:13:29.451Z**.
- Attachment835759: **2026-10-19T09:25:25.254Z**, not its authorship date.

No external freshness, deployment or historical visual equivalence follows.

## Reviewed fingerprints

SHA-256 recomputed from installed report bytes:

| Report | SHA-256 |
|---|---|
| API-MOS-717-r2.md | `8cd2474d492081224b9c725414b8ad9b4fd9e87c38986a945aded4384776790f` |
| API-MOS-754-r2.md | `4a634051a5b17a2c1857527b942e6870cdb66855a7b7aa3ee7b8539ea8340fd5` |
| IMPL-MOS-922.md | `8b25bb922707918369a10eab3cdb24d60a98a2b3cbe7da98714aac7aa94cdfd1` |
| IMPL-MOS-1146.md | `b6b0f9bc4a20ed838dc4c3b5d1eaa532b7859abf88c952f9e82e9026e693dd3c` |
| IMPL-MOS-1397.md | `29afc9909780a2ad6120891bd5deda1a93801a42c9667a836b4775064d0461c2` |
| IMPL-MOS-1398.md | `87938e144bf2fbfdd9cc10c100f08ef5d46a5142c61af68b19adec8a81f85722` |
| IMPL-MOS-1145.md | `cb930269eff20bf95c115efd832416c67f6d1d33f421d0777a99825e36fc23a5` |
| IMPL-MOS-1027.md | `c51c6961f97eba26b5ec302e80720cb7af537859805ce051e28e3fd8ee27eff7` |

All **104 distinct input digest values** recorded across the reports were found in independently hashed current local files; none was unmatched. This value-level check is not an assertion that every alias/table occurrence underwent a separate path-resolution audit or every hashed file received complete semantic review.

## Limitations and handoff

No mandatory source was missing. No tests, builds, format/type checks, application code, browser/network/business API calls or nested agents were executed. No project files, registers or publication artifacts were written. Git HEAD/index were not inspected; no empty-index attestation is made.

Primary inspection was bounded to material claims above, not every ancillary line or test in all eight reports. Test assertions are evidence of intended checks, **not passing results**. Backend transactions, execution suppression, effective preview, durable persistence, authorization and deployment remain unverified.

Preserve originals and prior review history. Consolidate overlapping annotations into existing candidates; do not create duplicate evidence-only publications.