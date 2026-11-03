# REQ-MOS-1023 — Environment-token source requirements

## Evidence and boundaries

Fresh extraction from the assigned saved sources only; no implementation/API inventory or source-precedence decision. Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

- **J**: `sources/jira-details-MOS-774/r1/content.json`, exact selector `$.items[12]`, verified `key == "MOS-1023"`; requirements from `.description`, title from `.summary`. Status Backlog; updated `2026-10-16T19:22:33.219+0800`. Metadata: `sources/jira-details-MOS-774/r1/metadata.json`, retrieved `2026-10-16T11:49:06.782Z`, SHA-256 `e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208`. Comments/custom fields/attachment bodies were not collected. Other Jira issues were not used.
- **W**: `sources/wiki-241080062/r1/content.json`, `$.bodyView`, heading/requirement or table-row selectors below. Metadata: `sources/wiki-241080062/r1/metadata.json`, version 17, versionWhen `2026-10-09T23:32:41.029+08:00`, retrieved `2026-10-16T11:48:21.710Z`, SHA-256 `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2`. Attachment metadata only; linked pages are not included evidence.

The wiki heading outline was read first, followed by token passages and sandbox prerequisites. HTML was parsed as inert text, never executed. No secret values were extracted. These are skill/environment business tokens, not application-session authentication. No new session, role, credential transport or authorization policy is inferred.

## Exact wiki locators

All W references mean `$.bodyView` within the indicated heading, ending at the next heading.

| Alias | Exact heading and HTML id | In-section locator |
|---|---|---|
| W-POD | `Карточка навыка: подключение (ПОД)`; `id-Админка.Навыки-Карточканавыка:подключение(ПОД)` | ПОД-4–9; ПРТ-ПОД-1–3 |
| W-TOKEN | `5.2. skill_tokens`; `id-Админка.Навыки-5.2.skill_tokens` | Purpose, usage list, table field names, final constraint paragraph |
| W-ENV | `7.3. Состав справочников и значения`; `id-Админка.Навыки-7.3.Составсправочниковизначения` | Three `skill_token_environments` rows |
| W-G | `G. Карточка навыка: подключение`; `id-Админка.Навыки-G.Карточканавыка:подключение` | Table rows T-50–T-53 |
| W-PES | `Песочница (ПЕС)`; `id-Админка.Навыки-Песочница(ПЕС)` | ПЕС-5, ПЕС-8, ПЕС-9; ПРТ-ПЕС-5 |
| W-AUD | `Аудит и история`; `id-Админка.Навыки-Аудитиистория` | АУД-1–2 |

## Atomic extracted requirements

IDs are stable within this work item. “Gate” records unresolved semantics, not permission to invent a fallback.

| ID | Requirement / source assertion | Short primary evidence and exact locator | Gate or qualification |
|---|---|---|---|
| REQ-MOS-1023-01 | Replace fictitious token availability with server information. | J `.description`: «Заменить фиктивные значения серверными сведениями о доступности токена». | Availability response and states are unspecified. |
| REQ-MOS-1023-02 | Show “not issued” only on the basis of server state. | J `.description`: «Отображать „не выдан“ только по состоянию сервера» (source uses «не выдан»). | Conflicts with unqualified inactive → not-issued wiki wording; see C1. |
| REQ-MOS-1023-03 | Issue system-generated skill tokens by environment. | W-POD ПОД-4: «Система выдаёт токены по контурам»; W-TOKEN purpose: «Значения формирует система». | Issuance API and trigger are open. |
| REQ-MOS-1023-04 | Represent the three environments as token cards. | W-POD ПРТ-ПОД-1: «„Песочница“, „Белые списки“, „Прод“»; W-ENV rows: `sandbox`, `whitelist`, `prod`. | ПОД-4 calls the last environment «продукты»; UI/data terminology requires reconciliation, not a fourth invented environment. |
| REQ-MOS-1023-05 | Highlight the token active for the current skill state. | W-POD ПОД-5: «Действующий для текущего состояния навыка токен выделяется». | Skill-state → token selection rules are absent. Do not infer from environment labels alone. |
| REQ-MOS-1023-06 | Support one-action copying, with a copy control for an active token. | W-POD ПОД-6: «копируется одним действием»; ПРТ-ПОД-3: «Для действующего токена доступна кнопка копирования». | Permission to obtain/disclose the value is not specified; inactive-token copy behavior remains unknown. |
| REQ-MOS-1023-07 | Copy through Clipboard API and acknowledge success. | W-G T-51: «FE: Clipboard API, тост-подтверждение». | Failure behavior and safe disclosure flow are not defined by these sources. |
| REQ-MOS-1023-08 | Support revocation and reissue of a token. | W-POD ПОД-7: «Токен отзывается и выпускается заново»; W-G T-52: «Отзыв действующего и выпуск нового». | Prototype omission is explicit: «В прототипе не показано». Runtime consequences remain open. |
| REQ-MOS-1023-09 | Confirm rotation and update the frontend afterward. | W-G T-52: «FE: подтверждение и обновление». | Confirmation text, affected consumers and failure/partial-success handling unspecified. |
| REQ-MOS-1023-10 | Record issuance/revocation history and rotation audit. | W-TOKEN purpose: «хранится история выпуска и отзыва»; W-G T-52: «с записью в аудит»; W-AUD АУД-1 includes «токенов», АУД-2: «дата и время, автор, действие, объект, подробности». | No permission to put token values into history is established; audit redaction semantics are absent. |
| REQ-MOS-1023-11 | Retain token identity, skill/environment relation and lifecycle metadata in the domain model. | W-TOKEN field rows: `id`, `skill_id`, `environment`, `is_active`, `issued_at`, `revoked_at`, `issued_by_user_id`; quote: «Признак действующего токена». | These are model fields, not a mandate to display every field or return secrets in normal metadata responses. |
| REQ-MOS-1023-12 | Model a unique token value and at most one active record per skill/environment. | W-TOKEN `token_value` row: `varchar(255)`, required, unique; constraint: «уникальный по (skill_id, environment) среди записей с is_active = true». | Storage/model assertion only; no mandated FE secret persistence or exposure. |
| REQ-MOS-1023-13 | Resolve disclosure rules before implementing disclosure semantics. | J `.description`: «Нужны правила раскрытия». | No masking, reveal trigger, one-time reveal, actor permissions, reauthentication or auto-hide rules supplied. |
| REQ-MOS-1023-14 | Resolve token validity periods. | J `.description`: «сроки действия». | W-TOKEN has issue/revocation timestamps, but no expiry field or lifetime rule. Revocation is not expiry. |
| REQ-MOS-1023-15 | Resolve token scopes. | J `.description`: «области». | Environment names do not define access scopes; no scope vocabulary supplied. |
| REQ-MOS-1023-16 | Resolve consequences of rotation. | J `.description`: «последствия перевыпуска». | Immediate invalidation, overlap, propagation, dependent clients and in-flight sandbox calls unspecified. |
| REQ-MOS-1023-17 | Open the sandbox from connection using skill id, never a secret in the URL. | W-POD ПОД-8; J `.description`: «Переход в песочницу передаёт skill id без секрета в URL». | Exact route/query structure is not specified. |
| REQ-MOS-1023-18 | Reuse the common token model in the sandbox; use the verification-environment token. | J `.description`: «Общую модель токенов использовать также в песочнице»; W-TOKEN usage: «использование токена проверочного контура». | Does not establish browser-side credential transport or a session-token model. |
| REQ-MOS-1023-19 | Keep sandbox checking unavailable until classifier additional training completes. | W-PES ПЕС-8: «недоступна, пока не завершено дообучение классификатора». | Authoritative readiness state and blocked-state UI are unspecified. |
| REQ-MOS-1023-20 | Keep sandbox execution on a separate environment without affecting users. | W-PES ПЕС-9: «на отдельном контуре и на пользователей не влияет». | Do not interpret sandbox rotation as production rotation. |
| REQ-MOS-1023-21 | Provide sandbox token reissue as a prototype-derived action. | W-PES ПРТ-ПЕС-5: «Перевыпустить токен». | Subject to the same unresolved rotation contract; target environment and interaction details require confirmation. |
| REQ-MOS-1023-22 | Expose connection context and an explicitly missing service address. | W-PES ПЕС-5: «показывает параметры подключения проверяемого навыка»; W-POD ПОД-9: «Незаполненный адрес сервиса выводится явно и отмечается в проверках». | Neither statement establishes a complete sandbox prerequisite matrix or proves missing address/token must block execution. |

Metadata detail for requirement 11: W-TOKEN declares UUID `id` (PK), UUID `skill_id` (FK `skills.id`), required `environment` varchar(32) (FK `skill_token_environments.code`), required boolean `is_active`, required datetime `issued_at`, optional datetime `revoked_at`, required UUID `issued_by_user_id` (external issuer identifier, «Кто выпустил, идентификатор СУДИР»). This issuer reference is not an application-authentication requirement.

## Disagreements and open gates — no precedence assumed

- **C1 — inactive versus unissued:** W-POD ПРТ-ПОД-2 says «Недействующий токен помечается как не выданный». J requires server-state-based “not issued.” A revoked/expired/inactive record is not defined as never issued. Preserve both claims; product/backend must approve the state vocabulary and display mapping. Loading, request failure and missing metadata must not be silently equated with an explicit unissued state under J.
- **C2 — proposed endpoints versus undefined contract:** W-G T-50 proposes `GET/POST /api/v1/skills/{id}/tokens`; T-52 proposes `POST .../tokens/{env}/rotate`. J states «в API не определены: выдача, раскрытие, отзыв и перевыпуск токенов навыка по контурам». Wiki task decomposition is not proof of an agreed or implemented contract. The linked contract page in J was not fetched or audited. No timestamp-based precedence is applied.
- **C3 — copy/value model versus disclosure:** W-TOKEN names a stored `token_value` and W-POD/W-G require copying; J explicitly requests disclosure rules. Neither copying nor the storage field settles whether values are returned masked, separately revealed, once-only, or restricted by role. The secret-free URL rule is precise; additional disclosure safeguards remain undecided.
- **G1 — lifecycle model gap:** `is_active`, `issued_at`, `revoked_at` do not define expiry, scopes, state-specific active-token selection, rotation overlap or effect on existing consumers. Resolve requirements 05 and 13–16 before committing behavior.
- **G2 — sandbox prerequisites gap:** Training completion and isolated verification environment are explicit. Missing/expired/revoked token handling, issuance prerequisite, readiness source and rotation while a check is running are not. Do not substitute a generic endpoint/key presence test or invent a full prerequisite matrix.
- **G3 — prototype versus delivery detail:** Rotation is required in ПОД-7 despite explicit absence from the connection prototype; sandbox reissue exists in ПРТ-ПЕС-5, while the selected `K. Песочница` decomposition rows T-74–T-81 do not separately specify it. This omission does not cancel the source requirement.

## Explicit deferrals and scope decisions

1. Defer disclosure, lifetime, scope and rotation-consequence policy pending decisions; the Jira text requests these decisions rather than supplying policy. Defer concrete issue/reveal/revoke/rotate integration pending an agreed contract. This is an audit finding, not a claim that the business capabilities are cancelled.
2. Do not invent reveal permissions, session refresh/login, global logout, OIDC, credential forwarding, role editing or new authorization policy. Skill `auth_required`/`auth_type` and issuer identity are subject-matter fields; separate wiki session/SUDIR task wording is outside this item.
3. Sandbox audit is limited to navigation without secrets, shared verification token model, token reissue and directly stated prerequisites/isolation. Conversation, tracing, sync, failure simulation, surface configuration, complete lifecycle and module behavior are deferred to their own work items.
4. No inferred UI display obligation for issuer/timestamps, no inferred expiry from `revoked_at`, no inferred scopes from environment, no assumed reveal endpoint from generic connection wording. Remaining unknowns stay open.
5. Saved source limitations remain: no Jira comments/custom fields/attachment bodies, no linked contract contents. Findings attest to these snapshots only, not backend availability or implementation compliance.

## Validation

Read the work item and both metadata files; selected exactly MOS-1023 from Jira; inspected wiki headings before targeted inert-text extraction. No network, browser, MCP, tests, generation, saved-command execution, source/spec edits or other report writes. Only this bound report was written.

```acceptance-report
{
  "criteriaSatisfied": [{"id": "criterion-1", "status": "satisfied", "evidence": "Fresh primary-source extraction with 22 stable requirement IDs, exact JSON/heading/row locators, quotes, conflicts and explicit open gates."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-1023.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command": "Local read-only Python JSON selection and HTMLParser heading/targeted-text inspection", "result": "passed", "summary": "Selected only Jira MOS-1023; inspected wiki outline and relevant token/sandbox passages without executing HTML."}],
  "validationOutput": ["Primary-source citations checked against the assigned saved snapshots; no tests run (prohibited for this task)."],
  "residualRisks": ["Token disclosure/lifetime/scopes/rotation consequences and sandbox prerequisite details remain unspecified.", "Inactive/not-issued wording and endpoint-contract status require reconciliation without assumed source precedence.", "Saved comments, attachment bodies and linked contract contents are unavailable within assigned evidence."],
  "diffSummary": "Only the bound requirement-extraction report was written.",
  "reviewFindings": ["Open product/contract gates documented; no implementation compliance conclusion attempted."],
  "manualNotes": "Read-only source inspection; no secret values extracted, credentials used or embedded commands executed."
}
```
