# Code Context

## Verdict: revise (bounded factual corrections)

The nine MOS-960 candidates and the central distinction are supported: entity metadata and a surface status transition do **not** establish a server test session, its tested revision, effective stand configuration or chat launch. Retain the report after correcting the exact schema/status/version statements below. No missing-input blocker requires escalation. This is review evidence, not writer authorization, task closure, source precedence or activation.

## Files Retrieved

Read completely:

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/R-SCENARIO-MOS-960.md` (lines 1–5) and `openspec/changes/reconcile-control-center-backlog/audit/work-items/SCENARIO-MOS-960.md` (lines 1–9): review and original boundaries.
2. `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-960.md` (lines 1–119): reviewed report.
3. `openspec/changes/reconcile-control-center-backlog/audit/reports/LOCAL-001.md` (lines 1–194): discovery routing only; its historical index attestation is not adopted.
4. `openspec/specs/skill-checks-training/spec.md` (lines 1–70), `openspec/specs/skill-connection-settings/spec.md` (1–58), `openspec/specs/skill-catalog-experience/spec.md` (1–112).
5. `openspec/specs/surface-lifecycle-publication/spec.md` (lines 1–196), `openspec/specs/surface-overview-connection/spec.md` (1–123).
6. `openspec/changes/mos-1023-skill-environment-tokens/proposal.md` (lines 1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-environment-tokens/spec.md` (1–47).

Primary JSON files are located by exact JSON pointers and document headings, not fictitious line ranges for embedded HTML. For each row, read its complete adjacent `metadata.json`; independently recomputed SHA-256 of the full content bytes and confirmed equality with metadata:

| Exact content path | SHA-256 | Semantic scope |
|---|---|---|
| `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-sandbox-details/r1/content.json` | `4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8` | `/items/0` only: MOS-960 description and issue metadata |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r2/content.json` | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` | `/bodyView`: introduction, §§1.3–1.5, 2.9, version history; bounded version/context discovery |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241082009/r2/content.json` | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` | `/bodyView`: introduction, §§1.1–1.3, 2.4–2.7, version history |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json` | `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2` | `/text`: ПОД-8, ПЕС-5/8/9, ПРТ-ПЕС-5/6, tables 5.2 and 6.3, T-79 and adjacent T-81 context |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-245673187/r1/content.json` | `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa` | `/text`: sandbox story scenarios 1–2, process «3. Проверка в песочнице», `surface_skills` context |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | Five operations below, all 47 transitively referenced schemas, bounded path-name discovery |

Jira is Backlog, updated 2026-10-15, retrieved 2026-10-16, with zero collected comments. Missing custom fields and uncollected attachment bodies remain collection limitations. None of these metadata facts attests runtime or approval.

## Key Code / exact contract corrections

No application code reviewed. In the saved OpenAPI, independently read:

- `GET /api/control/api/skills/v1/skills/{skill_id}`
- `POST /api/control/api/skills/v1/skills/{skill_id}/status`
- `GET /api/control/api/surfaces/v1/surfaces/{surface_id}`
- `POST /api/control/api/surfaces/v1/surfaces/{surface_id}/sandbox`
- `PUT /api/control/api/surfaces/v1/surfaces/{surface_id}/configuration`

All schema references resolved locally, including complete error envelopes and nested models. Exact schema locators below use `/components/schemas/<name>` in the API content file above.

### Required corrections to the reviewed report

1. **Schema precision — report line 60:** `SurfaceConfigurationResponse` has no `appearance` property. Replace the pseudo-shape with:
   ```text
   accent_color, shape, font, greeting, greeting_fallback, suggestions, cards
   ```
   These seven properties are required. `UpdateSurfaceConfigurationRequest` declares the same top-level property names, with write constraints. `enabled_skills` is a sibling of `configuration` in `SurfaceDetailResponse`, not a declared property of either configuration DTO. The detail envelope is `data: SurfaceDetailResponse`, not an unwrapped response body. The existing warning against mixing wiki and OpenAPI DTOs is correct; make it exact.

2. **Status identity — report line 87:** the surface UI wiki process says literal Russian labels **«Настроена», «Проверка», «Песочница»**, not literal `configured/review/sandbox`. The surface contract wiki §1.1 maps «Проверка» to **`checking`**, whereas OpenAPI `SurfaceStatus` contains **`review`**, not `checking`. Preserve this published vocabulary difference instead of silently normalizing it. The separate eligibility difference is confirmed: the UI story says not «Прод», its process lists the three labels, and OpenAPI sandbox description explicitly permits any original status, including `prod` and `archived`, subject to its documented validation. No precedence or UI expansion follows.

3. **Publication versus body versions — report line 24:** correctly identifies Confluence revisions 6/5/17/18, but add the distinct body labels required by the assignment. Catalog wiki revision **6** says **«Версия контракта: v1.0»** in its introduction while its history includes **v1.1 (14.09.2026)** and v1.0 (11.09.2026). Surface wiki revision **5** says **v1.0**, with v1.0 history dated 08.09.2026. Saved `r1/r2`, Confluence revisions, body labels, entity `version`, `display_version`, and connection `contract_version` are separate identities. Do not pick a corrected contract label or equate any with a tested snapshot.

4. **Complete the bounded DTO comparison — report line 88:** its nesting mismatch is valid but omits pertinent context differences already present in the inspected schemas. Wiki configuration includes `enabled_skills` in its PUT body; OpenAPI's configuration request does not declare it. Wiki `greeting_fallback` permits null; OpenAPI response/request require a string (the write description allows empty conditionally). Wiki `shape` values are `round/soft/square`, versus `round/moderate/strict`; `font` is `moscow/system/golos`, versus `moscow_sans/system/golos_text`. Wiki card examples have `id`; OpenAPI card models do not declare it. `SurfaceSkillResponse.parameters` is a string-valued map. Record these as publication differences, not an invented unified shape or a conclusion that undeclared properties necessarily produce rejection.

5. **Citation correction — report line 29:** the current `LOCAL-001.md` ends at line **194**, not 210. Use 1–194. Its capability names and archive inventory are routing evidence only, as the report already says.

### Important no-op findings

- D-002's accepted readiness-check publication is not reopened. Saved detail publishes `checks`; status advancement describes fresh checks. `SkillCheckResponse` contains type/status/blocking/message/time, but no tested revision or server test-session identity. The report correctly avoids the obsolete blanket absence-of-checks claim. No full checks audit was performed.
- Surface sandbox is bodyless and responds through `TsamResponseSchema_SurfaceStatusResponse_` with `surface_id`, `status`, `updated_at`. The operation description says external-service failure prevents saving status. This is documentation, not observed behavior or chat launch.
- Surface GET and PUT configuration descriptions explicitly say `updated_at` is creation/last status-change time and is not changed by configuration saving; GET also excludes enabled-skill saves. The wiki instead labels it last modification time. Neither interpretation supplies a tested-configuration revision. Keep this metadata difference visible.
- Integer skill `version` supports optimistic concurrency; `display_version` is a string; `connection.contract_version` describes the implementation contract. No scoped DTO declares any of them as the test-session binding. A check timestamp is not that binding either.

## Nine-candidate verification

All nine candidates are explicitly grounded in Jira `/items/0/description`; IDs below preserve the original report IDs.

| Candidate | Independent disposition |
|---|---|
| MOS-960-C01 chosen skill | Supported. Skill detail establishes identity. MOS-1023 delta lines 35–42 covers secret-safe ID navigation, not test-session creation. |
| MOS-960-C02 chosen surface | Supported. Detail supplies saved identity/configuration; wiki ПРТ-ПЕС-6 and surface_skills usage supply surface context/warnings. Neither establishes the loaded stand snapshot. |
| MOS-960-C03 endpoint | Supported, ambiguity retained. Catalog §1.5 explicitly calls it the implementation address. No authority to reinterpret it as the chat/stand endpoint. |
| MOS-960-C04 available contour | Supported. ПЕС-9 explicitly requires isolation; table 5.2 is a token storage model by environment, not an available-contours API or runtime readiness proof. Preserve MOS-1023's documented gate without designing transport. |
| MOS-960-C05 scenario composition | Supported. Saved enabled skill IDs/parameters and skill intents are published. Effective test composition is not thereby established; apply the DTO corrections above. |
| MOS-960-C06 greeting | Supported for surface saved content. Required-string versus wiki-nullable fallback difference matters. No skill-only greeting source found in the inspected context models; not-applicable and unknown must remain distinct. |
| MOS-960-C07 synchronization state | Supported requirement, missing scoped state contract. ПРТ-ПЕС-5/T-79 name synchronization action; that is not a state DTO. MOS-962 is a dependency, not implementation evidence. |
| MOS-960-C08 server test session | Supported requirement. Table 6.3 `skill_sandbox_checks` models a check/history record (`id`, skill, author, result, trace, created_at), not a declared session lifecycle. T-81 names an analytical sandbox-view integration; it does not provide the missing session DTO. Do not claim no sandbox-related models or integration mentions exist. |
| MOS-960-C09 tested version binding | Supported requirement and bounded gap. No binding found in the inspected operation/schema closure and context publications. Do not promote metadata/concurrency/check IDs to an immutable tested snapshot. |

## Architecture and boundaries

Entity reads provide selected IDs and saved metadata. The missing documented connection is from those values to a server test context and the actual loaded revision/composition. MOS-961 chat and MOS-962 synchronization remain dependencies only. Discovery of an owner/change is not a new product deferral.

The **actual existing** surface MVP prohibition remains explicit in `openspec/specs/surface-lifecycle-publication/spec.md:37–68`; lines 134–138 preserve `SANDBOX_CHECK_REQUIRED` handling without hidden sandbox launch. `surface-overview-connection/spec.md:80–94` distinguishes saved facts from successful checks. MOS-1023's complete artifacts preserve its token API/security gate and exclude dialog implementation. No policy precedence is selected.

Auth/access/mock behavior is not adjudicated. The previously recorded auth release approval remains confirmed as supplied review context; it is not downgraded, freshly re-attested, or extended to sandbox. The archived auth/demo prerequisite sets and rollout were not needed or read because this report makes no new auth/access/mock gate-status finding. Historical auth restrictions appearing in business specs are not used to reverse that approval. Business token schema references are not application auth context.

Bounded non-archive product Markdown discovery independently reproduced the report's sandbox/MOS-960 routing result: matches only in MOS-1023's artifact set. This says nothing about code completeness, archives, undocumented backend capabilities, or all possible semantic synonyms. Path-name discovery in the saved API returned only the surface sandbox path for sandbox/session/sync/context/version terms; the substantive absence claim rests on the five-operation schema closure and inspected context sections, not names alone.

## Start Here

Correct `openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-960.md:60,87–88` first: invented `appearance` and normalized `review` obscure the exact DTO/status differences. Then add the separate body-version labels at line 24. This review itself does not authorize edits beyond its sole output.

Remaining owner questions are unchanged: what endpoint/contour is intended, what is the server test-session identity/lifecycle, what revision it binds, how saved versus effective greeting/composition is distinguished, and what synchronization state MOS-962 supplies. These are product/backend questions, not blockers to this bounded evidence review. No supervisor decision was required.

## Limitations

Local saved publications only; no application-source audit, runtime verification, auth design, business calls, credential extraction, HTML execution, tests, builds, browser, network, MCP, git mutation or nested agents. Hashes establish saved-byte identity, not current external truth. No git-index assertion is made. Only this review report was intentionally written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently verified nine MOS-960 candidates, six saved primary hashes, five operations and 47 transitive schemas; returned revise with precise schema/status/version corrections and bounded limitations."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SCENARIO-MOS-960.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local read/find/grep and read-only Python JSON, SHA-256, inert HTML extraction, scoped reference traversal and product Markdown discovery","result":"passed","summary":"Six content digests match metadata; all scoped schema references resolve; mandatory matching local artifacts read completely."},
    {"command":"Tests/build/browser/network/MCP/runtime and git inspection","result":"not-run","summary":"Forbidden or outside bounded review; no index assertion."}
  ],
  "validationOutput": ["Nine candidates retain primary grounding.","Required corrections: appearance is not a property; literal Проверка is not an established review mapping; distinguish source and body versions; complete relevant DTO differences; repair LOCAL-001 range."],
  "residualRisks": ["Saved publications do not prove runtime readiness or tested snapshot correspondence.","Session/version/state absence is limited to inspected publications and scoped schemas.","Eligibility and shape differences remain unresolved without selecting precedence; auth approval is preserved but not sandbox approval."],
  "diffSummary": "Sole bounded independent review report; no reviewed-report, product, source, spec or task edits.",
  "reviewFindings": ["revise: precise factual corrections required; central nine-candidate analysis retained.","No blocking missing audit input or required supervisor decision."],
  "manualNotes": "Full local matching specs/MOS-1023 artifacts read; D-002 checks publication not reopened. Auth/mock adjudication excluded. No task closure, activation, new deferral or unverified index attestation."
}
```
