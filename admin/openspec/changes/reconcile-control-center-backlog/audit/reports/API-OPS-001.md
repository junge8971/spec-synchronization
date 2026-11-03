# API-OPS-001 — published operation delta

## Result

Completed local, read-only comparison of the saved 2026-10-16 snapshot, 2026-10-15 historical raw, and local aggregate. No network, MCP, tests, contract generation, nested agents, or project edits. Only this report was written.

- All three inputs: **94 paths, 128 operations, 128 unique operationIds**, none missing.
- Added/removed paths: **0/0**. Added/removed method+path operations: **0/0**. Added/removed/renamed operationIds: **0/0/0** across all pairs.
- Raw → live: **19 changed operation objects**: 18 added descriptions (7 skills, 11 surfaces), and one changed parameter definition. Remaining 109 operations equal.
- Raw → aggregate: **128 security-array changes only** within scope, intentionally normalized OR → AND.
- Aggregate → live: **128 changed operation objects**, comprising 128 security differences plus the same 19 upstream changes (147 changed operation-level fields). Excluding intentional security normalization: 19 changed, 109 equal.
- Top-level metadata, request bodies, response definitions/references, operationIds, summaries and tags: no changes. No path-item-level changes outside operations.
- Schema-key counts only: raw/aggregate 380, live 382. Schema internals deliberately excluded; owned by API-SCHEMA-001.

## Inputs and provenance

Read the work item and saved metadata before comparison. JSON parsed successfully; raw and live SHA-256 verified against their recorded values. Live byte count independently matched **413007**.

| Input | SHA-256 |
| --- | --- |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| `docs/api/contracts/openapi-2026-10-15.raw` | `2f3c48d3542e4486f7c1a501c4a1a4a0b813c662af26079a1e98c9f09d6ea26d` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |

Metadata records retrieval at `2026-10-16T11:13:29.451Z` from `https://nchat-a-tech.mos.ru/api/control/openapi.json`, discovered from Swagger; ETag and Last-Modified absent. Historical delta records retrieval at `2026-10-15T10:42:32Z`. These are saved-document provenance, not independently repeated network observations.

## Exact upstream delta: historical raw → saved live

The aggregate has the same before-values as historical raw for every item below. JSON pointers use RFC 6901 escaping. Absence means missing property, not JSON null. Description evidence below is explicitly an exact opening excerpt, not the entire added description.

### Parameter change (one operation)

OperationId remains `get_domain_list_api_control_api_skills_v1_domains_get`.

At `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2/schema/anyOf/0`:

```json
{"before":{"$ref":"#/components/schemas/SkillZone"},"after":{"type":"string"}}
```

Leaf pointers:
- `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2/schema/anyOf/0/$ref`: `"#/components/schemas/SkillZone"` → absent.
- `/paths/~1api~1control~1api~1skills~1v1~1domains/get/parameters/2/schema/anyOf/0/type`: absent → `"string"`.

Parameter identity remains `name: "zone"`, `in: "query"`, `required: false`; nullable branch remains `{"type":"null"}`. Other five parameters and all other parameter arrays are unchanged. This is an upstream operation-level reference-to-inline-type change, not local security normalization. No inference about the contents of SkillZone or runtime acceptance is made.

### Added descriptions (18 operations)

Every before-value is **absent** in both raw and aggregate. All corresponding operationIds remain unchanged. Each row gives the exact changed pointer and exact opening text of the added live value.

| Exact JSON pointer | After: opening excerpt |
| --- | --- |
| `/paths/~1api~1control~1api~1skills~1v1~1skills/post/description` | Создать навык в статусе `draft` и рассчитать его проверки готовности. |
| `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/get/description` | Получить карточку навыка вместе с результатами проверок готовности. |
| `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/put/description` | Изменить анкету и подключение навыка и пересчитать зависимые проверки готовности. |
| `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/patch/description` | Изменить анкету и подключение навыка и пересчитать зависимые проверки готовности. |
| `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1intents/put/description` | Заменить группы обучающих фраз навыка и пересчитать проверки фраз и конфликтов. |
| `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post/description` | Перевести навык в другой статус жизненного цикла; продвижение требует пройденных проверок готовности. |
| `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1phrase-conflicts~1check/post/description` | Проверить одну фразу на совпадения с фразами других навыков. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces/post/description` | Создать поверхность в статусе `draft` или сразу на проверке - `review`. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces/get/description` | Отдать страницу реестра поверхностей с поиском, отбором и сортировкой. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}/get/description` | Отдать карточку поверхности: описание, статус, конфигурацию виджета и подключённые |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1configuration/put/description` | Сохранить конфигурацию виджета поверхности: оформление и стартовый экран. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1enabled-skills/put/description` | Заменить список навыков, подключённых к поверхности, целиком. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1sandbox/post/description` | Отправить поверхность в песочницу: перевести в статус `sandbox`. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1publish/post/description` | Опубликовать поверхность: перевести в статус `prod`. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1disable/post/description` | Отключить опубликованную поверхность: перевести из `prod` в `disabled`. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1enable/post/description` | Вернуть отключённую поверхность в работу: перевести из `disabled` в `configured`. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1archive/post/description` | Архивировать отключённую поверхность: перевести из `disabled` в `archived`. |
| `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1restore/post/description` | Вернуть поверхность из архива: перевести из `archived` в `configured`. |

The added text also documents constraints, permission names and errors; these are published descriptions, not new response-map entries or permission-model approval. In particular surface descriptions now discuss error status/envelope labels and field pointers; their presence does not constitute observed backend error samples. The historical delta's surface-example limitation must not be confused with an assertion that the newer descriptions are absent.

## Intentional local normalization — not upstream drift

Every operation's `security` is identical between historical raw and saved live:

```json
[{"AdminToken":[]},{"AccessToken":[]}]
```

Every aggregate operation instead contains:

```json
[{"AdminToken":[],"AccessToken":[]}]
```

This is OpenAPI OR versus AND, respectively. Exactly **128** operation-level security arrays differ between either published input and aggregate. The exhaustive affected set is every HTTP-method operation under `/paths`; there are no exceptions. For example, exact pointers are `/paths/~1api~1control~1api~1auth~1v1~1me/get/security` and `/paths/~1api~1control~1api~1skills~1v1~1domains/get/security`. The same before/after applies to `/security` appended to each of the 18 operation pointers in the description table (replace `/description`). This set rule covers all 128 operations, rather than incorrectly presenting the examples as the full set.

`docs/api/contracts/README.md` and `docs/api/contracts/delta-2026-10-15.md` explicitly document this intentional AND normalization. It is not a newly introduced upstream change or evidence of deployed authorization behavior.

Unchanged in all three:
- `/components/securitySchemes/AdminToken`: `{"type":"apiKey","description":"Admin-service token. Supply both AdminToken and AccessToken as raw tokens.","in":"header","name":"X-Admin-Token"}`.
- `/components/securitySchemes/AccessToken`: `{"type":"apiKey","description":"OpenID access token. Supply both AdminToken and AccessToken as raw tokens.","in":"header","name":"X-Access-Token"}`.
- Root `/security` is absent.

## Top-level comparison and unchanged operation contracts

Before = after in all three:
- `/openapi`: `"3.1.0"`.
- `/info/title`: `"TSAM Assistant Management Service"`.
- `/info/version`: `"0.1.0"`.
- Root keys are exactly `openapi`, `info`, `paths`, `components`; therefore `/servers`, `/tags`, `/externalDocs` and root `/security` are absent throughout.
- Components contain `schemas` and `securitySchemes`; the latter is unchanged, the former excluded except independent key counts.

All operation requestBody/response objects, their media types, status codes, headers and references are equal. No new request/response reference is introduced by these operation-level changes. This does **not** assert unchanged referenced schema internals. Existing method+path-to-operationId mappings are identical across all three inputs.

README counts 94/128/380 describe the historical baseline, not the saved current schema-key count 382. The historical delta's 16 added operations and export-ID replacements are relative to an earlier aggregate, not additions or renames between the three inputs examined here. Likewise its statement that live matches the planning baseline concerns the historical capture, not the newer snapshot.

## Code Context

### Files Retrieved

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/API-OPS-001.md` (lines 1–8): scope, authority, stop conditions.
2. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/metadata.json` (lines 1–18): capture provenance, digest and count expectations.
3. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` (line 1): saved published contract; inspected programmatically, excluding schema internals from comparison.
4. `docs/api/contracts/openapi-2026-10-15.raw` (line 1): historical published baseline.
5. `docs/api/contracts/openapi.json` (lines 1–22075, parsed locally): aggregate; only top-level, paths and non-schema components compared.
6. `docs/api/contracts/README.md` (lines 1–35): normalization and historical count context.
7. `docs/api/contracts/delta-2026-10-15.md` (lines 1–105): provenance and historical delta context.

### Key Code / Architecture

No application source inspected or changed. Comparison traversed parsed JSON dictionaries recursively, treating arrays as complete values initially and then inspecting the one changed parameter array. Operations were independently enumerated using OpenAPI HTTP methods `get`, `put`, `post`, `delete`, `options`, `head`, `patch`, `trace`. JSON object ordering and file formatting were not semantic changes. Published raw/live and intentionally normalized aggregate are distinct comparison authorities; aggregate normalization must be separated from upstream deltas.

### Start Here

Open saved `sources/api-live/r1/metadata.json`, then resolve the exact changed pointers above in its `content.json`. For normalization rationale use the contract README; for component internals use the separate schema audit.

## Validation and residual risks

Three local Python inspection commands parsed inputs, verified digests/bytes, counted operations, compared scoped structures and printed selected before/after evidence. All completed successfully. The first command's displayed output was truncated; compact follow-up inspection recovered counts and every upstream changed field. No invalid/unavailable input or infrastructure failure occurred.

No backend operation invoked; no production availability, runtime validation, authentication behavior, response-example fidelity or deployed error semantics certified. No code fix or product priority proposed. Schema internals, generated types, split contracts and application behavior remain outside scope. Independent review and publication remain with the supervisor.
