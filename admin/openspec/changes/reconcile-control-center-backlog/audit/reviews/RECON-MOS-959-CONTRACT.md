# RECON-MOS-959-CONTRACT — linked-contract configurator delta

## Disposition

**REVISE narrowly by supplemental evidence note; not no-material-delta.** The previously accepted handoff remains valid for its then-read sources. Newly read page 241082009 introduces genuine versioned contract differences, so its “no demonstrated same-layer contradiction” conclusion cannot be extended to this expanded evidence set. Neither later capture nor page version selects authority. Preserve D-004 configurator deferral, unresolved product policy, candidate IDs and historical reports. No implementation, writer authorization, active plan, task closure or runtime delivery is established.

# Code Context

## Files Retrieved

`A = openspec/changes/reconcile-control-center-backlog/audit`. All abbreviated paths below expand under A.

1. `A/work-items/RECON-MOS-959-CONTRACT.md` (1–9), `A/reviews/RECON-MOS-959.md` (1–107), `A/decisions.md` (1–29): bounded assignment, prior handoff and D-004.
2. `A/sources/wiki-241082009/r2/content.json` (1–48; inert `/bodyView` parsing), `metadata.json` (1–50), `attachments.json` (1): new primary source and provenance. Only configuration-related sections inform findings; surrounding HTML text was mechanically rendered, not audited.
3. `A/sources/jira-api-delta-scenarios/r1/content.json` (selected `/items/3/description`, within 43–69): direct MOS-959 link membership.
4. `A/sources/api-live/r1/content.json` (single logical line 1): configuration PUT, create defaults/configuration validation, detail readback, enabled-skills stale-card behavior, and configuration/card/action/shape/font schemas only.
5. `A/sources/wiki-245673187/r1/content.json` (single logical line 1): selected `/bodyView` Configurator, common-tab rows, configuration dictionaries and JSONB configuration/card sections.
6. `openspec/specs/surface-lifecycle-publication/spec.md` (177–198): unchanged deferral owner, especially 179–192.

### Independently verified saved-byte SHA-256

| Source | SHA-256 |
|---|---|
| New linked wiki content r2 | `13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b` |
| Its attachment listing | `70590629831676a0bfde3fc46438aaeb623b3915746bbab62c1221b13e3fb960` |
| Jira selected capture r1 | `b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed` |
| Published API r1 | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| UI wiki 245673187 r1 | `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa` |

New metadata: retrieved `2026-10-16T12:28:15.837Z`, page version **5**, version.when `2026-09-08T18:24:09.893+08:00`. Exact saved title is “API-контракт управления поверхностями”; **v5 is the page revision, while the body says contract v1.0**, dated 08.09.2026 in its version history. It is newly collected, not necessarily newer contractual intent. Metadata records successful verified wiki-origin page26 collection after the failed r1 attempt; neither attempt was changed. Attachments `/data/results=[]`, `/data/size=0`, no `/data/_links/next`; this page's listing is complete and empty, not proof about other sources' attachments.

## Key Code / source locators

New wiki citations mean `/bodyView` under exact heading IDs with prefix `APIконтрактуправленияповерхностями-`:
- **N1:** `1.Цельзадачи`.
- **N13:** `1.3Конфигурация`, example, field table and concluding placeholder paragraph.
- **N23:** `2.3Зарегистрироватьповерхность`, with `Телозапроса`, `Проверки`, `Начальныенастройки`.
- **N24:** `2.4Получитькарточкуповерхности`, `Успешныйответ.3` configuration/timestamp example.
- **N25:** `2.5Сохранитьконфигурацию`, `Телозапроса.1`, `Успешныйответ.4`, `Архивнаяповерхность`.

API pointers: `C=/components/schemas`; `S=/paths/~1api~1control~1api~1surfaces~1v1~1surfaces`; `SAVE=S~1{surface_id}~1configuration/put/description`; `CREATE=S/post/description`; `DETAIL=S~1{surface_id}/get/description`; `SKILLS=S~1{surface_id}~1enabled-skills/put/description`; `U=C/UpdateSurfaceConfigurationRequest`. Concatenate literally.

UI wiki headings under `/bodyView`: `id-Бизнесанализ:Поверхности-Вкладка"Конфигуратор"` (**UI-C**), `id-Бизнесанализ:Поверхности-Общиедлявсехвкладок.1` (**UI-G**), `id-Бизнесанализ:Поверхности-4.3.Составсправочниковизначения` (**UI-D**), `id-Бизнесанализ:Поверхности-5.1.surfaces.configuration` and `id-Бизнесанализ:Поверхности-5.2.surfaces.configuration.cards[]`.

## Exact delta and contradictions

| Topic | Newly read linked contract versus accepted evidence | Classification / supplemental correction |
|---|---|---|
| Placeholders | N13 explicitly names `{имя}`, `{отчество}`, `{время суток}`. SAVE already names all three and rejects other brace words/unpaired braces. | Confirmation, not a new unresolved blocker. The linked source itself now answers the MOS-959 exact-name publication concern. UI-C #23's `{время суток)` remains a typo, not a token. N13 supplies no escaping/nesting/case/time mapping. |
| HEX | N13 says `#RRGGBB`; sample `#0B6B3A`, N23 initial `#B3121B`. API U/accent_color pattern remains `^#[0-9a-fA-F]{6}$`. | Confirms transport shape. Does not resolve UI-C #26 arbitrary-versus-presets or bare-HEX input conversion; no case-normalization rule added. |
| Shape/font codes | N13 permits `round, soft, square` and `moscow, system, golos`; N25 uses `soft/golos`. API `C/SurfaceConfigurationShape/enum` is `round, moderate, strict`; `C/SurfaceConfigurationFont/enum` is `moscow_sans, system, golos_text`, also matched by UI-D. | **Genuine same-layer allowed-value contradiction across versioned sources.** Do not silently alias codes or pick the newer-looking source. |
| Fallback | N13 explicitly permits “Строка или null” and says mandatory when greeting contains `{имя}`. N25 says request contains N13 object. API `U/properties/greeting_fallback/type=string`, U/required includes it; SAVE requires nonempty for name **or patronymic**, otherwise permits empty string, and allows only time placeholder. | **Genuine nullability contradiction for configuration PUT**, not merely optional stored JSONB. Name-only paragraph is incomplete relative to API, not an explicit assertion that patronymic needs no fallback. Preserve already-known API conditional rule; ask only source reconciliation, not rediscovery of validation. |
| Counts/text bounds | N13: nonempty greeting, at most five nonempty suggestions/four cards. No numeric text bounds, duplicate rule or detailed card constraints. | Confirms maxima; silence does not negate SAVE/U/card bounds already accepted (500 greeting/fallback, 100 suggestion/title, 200 subtitle, message 500, link 2000). Do not reopen those as absent documentation. |
| Skill identity/action validation | N13 message action and N25 skill action show UUID-shaped skill value; N13's explicit UUIDv7 annotation is for `enabled_skills[].skill_id`, not card action. | Confirms concrete identifier example, not a separate “skill code” payload or UUIDv7-only card rule. No new link restrictions, action whitelist, canonicalization or connected/nondeleted action validation; accepted SAVE rules remain available. |
| PUT responsibility/model | N25 says “Запрос содержит объект из раздела 1.3”, includes `enabled_skills` and validates its parameters; examples also include card `id`. API U defines seven appearance/content fields only; card request has no id; skill replacement/validation is separately described by SKILLS. | **Material same-operation contract responsibility/model divergence**: wiki assigns skill persistence to configuration PUT, unlike accepted split. Extra-field rejection cannot be inferred: U/card schema does not state `additionalProperties:false`. Card id is an example/model difference, not demonstrated required-field contradiction. Do not send hidden combined payloads or activate configuration writes. |
| Creation defaults | N23 initial settings: font `moscow`, fallback `Здравствуйте`, suggestions `["Что ты умеешь?"]`; CREATE: `moscow_sans`, fallback `Здравствуйте! Чем помочь?`, no suggestions. Both initial color `#B3121B`, round shape and empty cards. N23 uses top-level required greeting, whereas CREATE accepts optional nested configuration. | **Genuine versioned default/payload difference**, restricted here to configuration initialization. Do not turn N13 sample green/personalized greeting into defaults or reopen general registration audit. |
| Save/readback/timestamps | N24 prod example updated_at `09:00`; N25 save response `09:15`, no status change; N1.2 describes updated_at generically as last modification. SAVE/DETAIL explicitly say configuration save does **not** change it. | **Example/description tension**, weaker than an explicit wiki timestamp-update rule: examples are not proven sequential observations. Record it, not a runtime contradiction or proof of timestamp updates. |
| Prod application | N1 says one mutable configuration, saving published surface applies immediately without republication/re-embedding. N25 explicitly says prod changes take effect immediately, status unchanged, code unchanged. | **New explicit publication claim about immediacy.** Prior UI-G #14 alone was not a timing guarantee; supplement that narrow statement with linked-contract claim. No evidence of deployed latency, cache behavior or propagation SLA. No conflict with SAVE's unchanged embed token/code. |
| Archive/save | N25 explicitly forbids archival edits with `409 SURFACE_ARCHIVED`; SAVE's listed errors omit this restriction/code. | Additional versioned contract claim; omission is not affirmative API permission to edit archived surfaces. Do not invent a proven opposite behavior or reopen lifecycle inventory. |
| Preview/normalization/stale references | No local Greeting/Dialog preview policy, mock identity/time examples, edge trimming, canonical skill UUID, or disconnect remediation is specified by N13/N25. | No material delta to accepted UI-C #22–25 preview intent, SAVE trimming/lowercase UUID, CREATE format-only card check, and SKILLS no-card-recheck facts. No auto-removal/block-disconnect policy follows from wiki skill parameter validation. |

## Newly answerable versus remaining questions

**Now factually answerable:** the directly linked contract is available and contains exact placeholder names; it explicitly claims immediate Prod application, unchanged status/embed code, combined skill/configuration PUT, nullable fallback and the older code/default set above. Page-local attachment listing is empty. Prior linked-page absence statements in the review and D-004 are outdated for **241082009 r2 only**. None of these facts establishes authority or delivery.

**Remaining source reconciliation:** which contract vocabulary, fallback nullability, initialization defaults and skill-write boundary is intended for a future approved configurator; whether wiki timestamp examples/archive restriction should be revised or carried forward. These are newly exposed disagreements, not a request to discard accepted API facts. No source precedence is selected here.

**Unchanged product/design policy:** HEX input/preset restrictions; fallback editor/help/preview; mock names/time samples, time mapping and safe preview action execution; stale-skill remediation and any stricter creation integrity; dirty equality/reset, navigation and write/read recovery. Parser escaping/nesting/case, Unicode length, trim/validation order and duplicate equality remain unspecified. Adjacent sandbox audience and publication orchestration remain outside scope. No new uncertainty is assigned to already documented API bounds, placeholders, transport HEX, UUID format, trimming or full replacement.

## Architecture

The accepted API separates complete appearance/content configuration replacement from enabled-skill replacement; creation may carry configuration, detail reads saved values, preview is transient UI. The newly read wiki describes a combined configuration containing skills. That is an evidence-model divergence, not permission to change this architecture or the approved scope.

## Start Here / recommended supplemental corrections only

Read `A/decisions.md` D-004 alongside `openspec/specs/surface-lifecycle-publication/spec.md:179–192`: deferral remains the controlling scope boundary, with no fake/default/hidden PUT. Then add a separately approved supplemental handoff, not a rewrite of historical evidence, covering:

1. Linked page now collected; exact hash/revision/body-version distinction and empty local attachments.
2. Qualify previous no-same-layer-contradiction statement to its original evidence set; enumerate enum/nullability/default/combined-PUT differences above, separating timestamp examples and omission-only archive tension.
3. Retain candidate 002/025/033 qualifications. For 033 add that this linked publication explicitly asserts immediate Prod application, without turning it into deployment verification or global timing policy.
4. Preserve all already-resolved API facts and all unresolved UI/product choices; no changes to main-spec deferral, active plans or task statuses.

## Validation and limitations

Fresh local primary-source reading and SHA-256 computation; inert standard-library HTMLParser only, no embedded scripts/source commands executed. No repeated 39-candidate extraction, broad API/code inventory or completed audit. No missing input/infrastructure blocker. Only this report written. No network/MCP/browser, nested agents, tests/build/generation, code/product/source edits, archive/sync or Git mutation. Other sources' attachment bodies (including MOS-1237 test plan) remain unread; no deployed behavior evidence. Git index state was not inspected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independent linked-contract delta review with verified source hashes, exact headings/pointers, versioned contradictions, remaining policy questions and narrow supplemental corrections; deferral preserved."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-959-CONTRACT.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python JSON/SHA-256/inert HTMLParser inspection","result":"passed","summary":"Verified five saved content/listing digests and compared only relevant configuration evidence."},
    {"command":"Bounded file reads and wc -l of named inputs","result":"passed","summary":"Confirmed prior accepted handoff, D-004 and main-spec deferral ownership."},
    {"command":"tests/build/network/MCP/browser/code inventory","result":"not-run","summary":"Outside scope or expressly prohibited."}
  ],
  "validationOutput": ["REVISE by narrow supplement: newly collected linked contract materially differs from accepted API evidence.","No precedence, activation, task closure or runtime conclusion."],
  "residualRisks": ["Versioned contract disagreements require owner reconciliation before any future activation.","Other-source attachment bodies remain unread; collection is not globally complete.","No deployed persistence, validation or propagation behavior verified; unresolved product policy retained."],
  "diffSummary": "Only bound independent review report created.",
  "reviewFindings": ["No input blocker; material enum, nullability, configuration-default and skill-write model differences documented."],
  "manualNotes": "Page revision 5 must not be confused with body contract v1.0. Historical sources and decisions were not edited. Git index not inspected or mutated. No writer authorization implied."
}
```
