# Code Context

## Result and boundary

MOS-1015 remains a **Hold request**, not a cancellation: its sole comment says «Переключился на навыки». MOS-885 is Backlog. This audit does not close either task, choose source precedence, approve an API, activate implementation, or attest an audit index.

The report wiki really publishes **18 fields**, not 24. The saved OpenAPI publishes **no report paths, report operation IDs or report schemas**. Dialog selection and richer dialog-card fields are published there, but do not establish report DTO support. Preserve the existing local-draft-only agreement; correct stale reasoning about the absence of *dialog* contracts and reconcile reuse with the already accepted condition builder before any implementation.

MOS-885 requests an isolated **fake backend data-provider** for preview/metrics/CSV, explicitly excluding real dialog retrieval. Its requested DoD is not evidence that the provider, endpoints, tests or enforcement were delivered. This is also distinct from the frontend's local Express/demo fixtures.

## Files Retrieved

Paths below are relative to the repository root; `A` means `openspec/changes/reconcile-control-center-backlog/audit`.

1. `A/work-items/SCENARIO-MOS-1015.md` (lines 1–8): bounded assignment.
2. `A/sources/jira-reports-details/r1/content.json` (items[1], MOS-885 starting line 32; items[4], MOS-1015 starting line 86; only those items analyzed), and `metadata.json`: request, status, comment and provenance.
3. `A/sources/wiki-241085838/r1/content.json` (lines 7–38 version; line 39 inert body, §§1.1–1.3, 1.5, 2.1, 2.4 and relevant validation): report parameters, 18-field matrix, preview and metrics. `metadata.json` read.
4. `A/sources/wiki-241085439/r1/content.json` (lines 7–38 version; line 39 inert body, §§2.4.1–2.4.5 and relevant §2.7 field mappings): selection and dialog semantics. `metadata.json` read. No bearer example executed or reproduced; metadata records eight redacted examples.
5. `A/sources/api-live/r1/content.json` (line 1; `/paths`, `/components/schemas`, matching selection/card dependencies), and `metadata.json`: saved publication, not a runtime probe.
6. `openspec/changes/mos-1015-report-constructor/proposal.md` (1–35), `design.md` (1–100), `tasks.md` (1–27), `specs/report-constructor-draft/spec.md` (1–128), `specs/dialog-selection-draft/spec.md` (1–115): read completely.
7. `openspec/specs/dialog-selection-builder/spec.md` (1–67) and `openspec/specs/dialog-registry/spec.md` (complete): accepted shared selection requirements and application semantics.
8. Complete mandatory prerequisites: `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/{proposal,design}.md` and all six `specs/*/spec.md`; `openspec/changes/archive/2026-10-09-add-local-session-demo/{proposal,design}.md` and all three `specs/*/spec.md`. Truncated inspection outputs were continued until complete. Main `openspec/specs/{mpmm-session,control-center-permissions,local-session-demo}/spec.md` requirement bodies were checked byte-for-byte equal to the corresponding fully read archived bodies. Historical confirmation: auth `tasks.md` lines 48–52 and complete `docs/mpmm-auth-rollout.md`.

No product/source code inspected or changed. Existing dialog UI wiki 243776365 was unnecessary: the report delta already contains the full ordered UI list and the dialog contract supplies relevant field semantics. The Jira description itself does **not** enumerate all 24 columns; the table below uses the explicit delta list, not an invented primary-source list or an independently revalidated prototype.

## Provenance and integrity

Recomputed SHA-256 of saved content bytes matched both supplied expected values (where supplied) and local metadata:

| Saved revision | SHA-256 | Publication/capture |
|---|---|---|
| jira-reports-details/r1 | `c69d3aeaef6121d67440c61f06a0c8cb6b3c8ad605c7cfcec0653e7f7e5f234c` | captured 2026-10-16T13:31:43.125Z; MOS-885 updated 19:20:12.520+0800, MOS-1015 19:22:30.534+0800 |
| wiki-241085838/r1 | `797051024d296c8233d998d15894eaf35b6c6a02980fa37670430d0ae5da2d74` | wiki version 3, 2026-09-09T17:12:02.625+08:00; body contract v1.0; captured 2026-10-16T13:31:51.607Z |
| wiki-241085439/r1 | `974ea35aaf44b9ec7c14c573ba58bdf7ed55397a9ca47d62b37fb39d9886f8bc` | wiki version 15, 2026-10-07T18:54:12.389+08:00; captured 2026-10-16T13:31:52.139Z |
| api-live/r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` | OpenAPI info version 0.1.0; captured 2026-10-16T11:13:29.451Z; no ETag/Last-Modified |

Metadata attributes wiki/Jira capture to parent verified-origin GET and OpenAPI to the Swagger-discovered URL `https://nchat-a-tech.mos.ru/api/control/openapi.json`. These are recorded provenance, not network actions or fresh origin verification by this audit. Wiki metadata says HTTP 200, no attachments; Jira custom fields/attachment bodies were not collected. Hash equality verifies saved bytes, not delivery or approval.

## Key Code / contract requirements

No code change is proposed. Critical published shapes are:

- Report wiki: `{ period: { date_from, date_to }, channel_id: string|null, field_codes: string[] }`. Inclusive calendar dates, start ≤ end, nonempty ordered fields; `null` channel means all. No advanced selection, all-time preset or report timezone field is defined here.
- Dialog `SelectionBody`: `schema_version`, optional `q`, `period`, `channel_ids`, `skill_ids`, `condition_group`, `time_zone`; group is `match: all|any` with up to 30 conditions. No nested groups. Text ≤500 and list ≤100 per dialog semantics; dates/ranges inclusive, number conditions integer. Parts combine with AND; negative plural conditions mean no matching value.
- `ConditionBody`: `attribute`, `operator`, `value`, `values`, `value_from`, `value_to`, `match_mode`, `scope`. Published phrase scopes are dialog/user/assistant/operator/skill; **there is no per-condition skill ID**. Scope skill means skill replies collectively; assistant includes skills and subsystems. Global `skill_ids` selects dialogs with participants and does not substitute for targeting a particular speaker's messages.
- `DialogCardResponse` contains `duration_sec`, `user`, `participants`, `step_count`, `attachment_counts`, `messages`, operator rating/reason/comment. These are dialog DTOs only.

## 24-column mapping: exact coverage and gaps

Order/names are from `report-constructor-draft/spec.md:73–100`. “Report code” below means wiki publication only; **none is an available report DTO in saved OpenAPI**. Dialog candidates provide semantics, not approved report wire mappings or permission to aggregate client-side.

| # / UI column | Report wiki field | Dialog evidence / remaining gate |
|---|---|---|
| 1 Идентификатор чата | `chat_id` string | `chat_id`; report integration still absent |
| 2 Идентификатор сессии | `session_id` string | `session_id` |
| 3 Идентификатор пользователя | `sso_id` string | `user.sso_id` nullable string; confirm report null convention |
| 4 Признак авторизации | **Absent** | `user.authorization`, `authorized_at`; distinguish authorized from start, unauthorized, authorized within dialog; not employee auth |
| 5 Поверхность | `channel` string | `channel_id`, `channel_name`; report request `channel_id` must not be guessed from arbitrary surface ID |
| 6 Участники | **Absent** | `participants[]` with type/id/name/message_count/share_percent; report representation/order unresolved |
| 7 Дата и время обращения | `started_at` datetime | `started_at` |
| 8 Дата и время завершения | `ended_at` datetime | nullable `ended_at`; unfinished display must remain explicit |
| 9 Диалог полностью | `dialog_transcript` string | `messages[]`; report text assembly remains server-owned |
| 10 Текст от пользователя | `user_messages` string | messages with user author; no client report reconstruction |
| 11 Текст от оператора | `operator_messages` string | messages with operator author |
| 12 Продолжительность диалога | **Mismatch:** `bot_duration` string is time with robot | `duration_sec` integer is full dialog duration; cannot rename bot time to full duration |
| 13 Шагов в диалоге | **Absent** | `step_count` integer, distinct from `skill_step_count` and route trace steps |
| 14 Вложений | **Absent** | `attachment_counts.total` integer |
| 15 Вложений оператору | **Absent** | `attachment_counts.to_operator` integer; recipient condition is not this count |
| 16 Причина завершения | `end_reason` string | nullable `end_reason` dictionary object/name; report serialization unresolved |
| 17 Кто завершил диалог | `ended_by` string | nullable enum; unfinished not fabricated |
| 18 Оценки ответов ассистента | **Absent** | skill/subsystem messages' `rating.value` good/poor, optional reason/comment; multi-value representation unresolved |
| 19 Оценка работы оператора | `operator_rating` number | nullable integer in dialog; independent of message ratings |
| 20 Комментарий к оценке | `rating_comment` string | UI means `operator_rating_comment`; report's generic name does not establish operator ownership |
| 21 Причина низкой оценки | **Mismatch/ambiguity:** `low_rating_reason` labeled «Причина низкой оценки ответа» | UI/operator reason is `operator_rating_reason.name`; message reason is `messages[].rating.reason`; do not conflate |
| 22 Категории | `topic_categories` string | dialog `categories[]` plus separate topic; confirm combined report presentation |
| 23 Тип ошибки и целевой ответ | `error_target_answer` string | field exists in report publication; dialog selection `error_type` semantics remain unresolved |
| 24 Кнопка виджета | `widget_button` string | field exists in report publication; dialog selection semantics remain unresolved |

Exact arithmetic: six UI additions have no row among the 18 published report fields (#4,6,13,14,15,18). The remaining eighteen positions are not eighteen fully approved semantic mappings: full duration and low-rating reason conflict, rating-comment ownership needs clarification, and surface/nullable/format conversions still require an agreed report contract. `ended_at`, `error_target_answer` and `widget_button` are **already published report fields**, not missing additions. The dialog publication adds evidence for the six richer concepts, not report support.

## Architecture / requirement-to-spec reconciliation

| Stable requirement | Evidence and current agreement | Difference / gate |
|---|---|---|
| Period and surface | MOS-1015; report wiki §§1.1/2.1; draft spec §§Calendar period/Surface reference | Draft default 30 days and browser dates are local UI semantics; dialog presets use server clock/timezone, all_time means retention. Report API mapping/all-time/timezone remain unresolved, not inherited automatically from dialogs. |
| Ordered 24 columns | MOS-1015; draft spec 73–110; design B15.1 | Preserve full list, initial first eight, reinsertion-at-end and empty-selection error. Wiki default example has eight *different* fields; do not silently replace agreed UI defaults. Need 24-row approved wire/type/null/display mapping. |
| Applied conditions | MOS-1015; design B15.2; main dialog-selection-builder | Reports remain a local unapplied draft. Dialog selection is already accepted; do not create a second engine or treat it as unavailable globally. Published selection still is not accepted by report-preview. |
| Reuse builder | Draft tasks 2.1–2.3 propose creating `features/dialog-selection`; main builder spec already owns semantics | Reconcile ownership/reuse, not a duplicate 35-attribute catalogue/engine. Preserve three visible-but-disabled attributes operator_group/error_type/widget_button; wiki forwarding unresolved fields is not permission to offer no-op filters. |
| Phrase semantics | Draft condition spec 100–107 requires explicit particular skill; main builder 32–39 and published DTO do not | Concrete unresolved difference: choose whether to revise draft wording or obtain separately agreed support. Do not invent a skill_id on ConditionBody or misuse global skill filter. |
| Backend preview | Wiki §§1.5/2.4: columns/rows/total/metrics; MOS-1015; design B15.4–B15.5 | Wiki says first **five columns / twelve rows**; existing design explicitly records prototype all-column vs 5-column conflict. Preserve this as a decision gate; neither source silently wins. Full total differs from preview size; request failures/stale responses require future agreed integration. |
| Whole-selection metrics | MOS-1015; wiki §1.3; design B15.3 | Published names: dialogs integer; operator_share and solved_share in [0,1]; average_rating number/null. No ratings displays dash; empty example is 0/0/0/null. This defines representation, not complete formulas/denominators, proof of whole-selection implementation, or operator-only average semantics. Do not calculate metrics from preview rows or dictionaries. |
| Availability | Proposal contract boundary; draft spec 112–119 | Saved API absence supports unavailable report results; keep no fake rows, metrics, report calls or false success. “Dialog API absent” in proposal is stale; report wiki publication exists but has not supplied report operations to saved API. |

The main builder already requires typed operators, explicit draft/apply, no hidden deletion, bounded validation, server errors mapped to submitted condition rows, and server execution. Draft-only reporting must compose this ownership without activating server report search. The active plan's shared-feature intent is compatible; its “create a new local editor” and unavailable-all-enums rationale require reconciliation with the accepted owner, not a new algorithm or wider plan.

## Access, mocks and historical release approval

Complete approved auth/demo prerequisites were read before these conclusions. Older report draft wording (“without profile/role checks”, no auth requests in direct entry/tests) must not become a route bypass. Existing agreement places business UI after session/access boundary; report UI remains explicit `*` only until granular policy is separately agreed. Roles in the wiki do not grant UI permissions. No request ACL, client object-scope engine or new report permission is proposed.

Real mode is configuration-selected (production and dev with mocks disabled), not hostname-selected. Dev demo confirms a mock principal; business mocks remain credential-free without role enforcement. Full demo profile does not create report endpoints or fake successful results. Business `user.authorization` fields remain dialog data, not employee session fields.

**Preserve, do not reopen or extend:** `docs/mpmm-auth-rollout.md` records user confirmation on 09.10.2026 («Подтверждаю пункт и архивацию»), mirrored in archived auth task 6.3. It explicitly is user confirmation, not agent-run real-backend verification or proof of deployment. This report neither withdraws that approval nor extends it to missing report operations, a new provider, new permission mapping, changed deployment or current publication/runtime guarantees. Redacted bearer examples are inert historical examples, not a credential protocol to copy.

## Start Here / minimal corrections and decision questions

First open `openspec/changes/mos-1015-report-constructor/design.md:74–96`: its C01–C12 and B15.1–B15.5 preserve the stable requirements and explicitly prevent treating local UI delivery as full MOS-1015 completion.

Minimal follow-up for the owning reconciliation (not performed here):

1. Correct the proposal's blanket dialog-contract absence statement; retain report unavailability and separate wiki publication from saved OpenAPI and runtime delivery.
2. Reconcile tasks/specs with existing condition-builder ownership and auth/demo boundary. Do not duplicate the engine, remove unresolved conditions silently, or blanket-ban legitimate shell `/me` while asserting no report calls.
3. Ask the contract/product owner only the remaining concrete questions: approved 24-field wire/nullable/format matrix; full-duration and rating ownership; report selection/timezone/all-time semantics; particular-skill phrase requirement; preview 5-column versus all-column limit; whole-selection metric formulas/denominators; actual provider/API delivery evidence. These are future integration gates, not blockers to producing this bounded audit.
4. No-op where already aligned: Hold is not cancellation; preserve 24 ordered UI columns, explicit unapplied draft, server-owned preview/metrics, no invented data, separate CSV/templates/scheduling ownership, and historical release approval without extension.

## Validation and residual risks

Only local inspection, inert HTML text parsing and byte/hash/JSON checks were performed. No network/MCP/browser, tests, build, generation, business requests, credential extraction, code changes, source precedence resolution or activation. Only this bound report was intentionally written; shell inspection tools produced their normal truncated-output temporary logs.

Residual risks: no runtime delivery/enforcement evidence; no independent prototype verification; report wiki and dialog field catalog are different contracts; report DTO and 24-column mapping remain unavailable; the published report reason label is semantically inconsistent with the requested operator reason; current draft tasks predate accepted builder/auth agreements. Historical tests mentioned in rollout documentation were not rerun and are not current validation evidence.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Bounded report verifies four saved hashes/versions, maps all 24 declared UI columns with six absent report fields and semantic conflicts, separates requested fake provider from delivery, and records gates without activation."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-1015.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local Python SHA-256/JSON inspection and prerequisite requirement-body equality checks","result":"passed","summary":"Four hashes matched; no report paths/schema names/operation IDs in saved API; three relevant main requirement bodies equal fully read prerequisites."},{"command":"Tests/build/browser/network","result":"not-run","summary":"Forbidden by bounded assignment."}],
  "validationOutput": ["Report-only evidence analysis; no implementation or runtime attestation."],
  "residualRisks": ["Report delivery and runtime enforcement unverified.","24 UI columns are from existing delta spec, not independently revalidated prototype.","Report DTO, advanced report selection and semantic mappings remain unresolved."],
  "noStagedFiles": true,
  "diffSummary": "Only assigned report intentionally written; no staging or source changes performed.",
  "reviewFindings": ["Existing draft must reconcile accepted condition-builder ownership and session/access boundary before implementation.","No audit-execution blocker; integration gates remain open without task closure."],
  "manualNotes": "Read complete mandatory archived auth/demo proposal/design/spec prerequisites and historical 09.10 user release confirmation; preserved approval without extending it. No index attestation. noStagedFiles denotes no staging by this run, not inspection of pre-existing index state."
}
```
