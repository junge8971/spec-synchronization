# RECON-MOS-959 — independent combined-evidence reconciliation

## Disposition

**REVISE narrowly for combined-evidence handoff; accept the 39 candidates as bounded Jira/wiki extraction, not activated requirements.** No fabricated requirement or blocking input failure found. Preserve IDs. Correct the scope of the remaining gaps as below: published API supplies transport HEX format, skill UUID, bounds, conditional fallback and normalization facts that the extraction intentionally did not import. Also qualify candidate 033 with its source's Prod-only informational-block context. No implementation, task closure, source precedence or activation follows.

D-002 accepts r2 with R-SURFACE-CONFIG corrections and explicitly retains deferral. Newly saved wiki evidence supplements that handoff; older statements that Confluence was uncollected are now outdated **for page 245673187 v18 only**, not for all linked contracts or attachments.

# Code Context

## Files Retrieved

`A` = `openspec/changes/reconcile-control-center-backlog/audit/`; paths below are repository-relative after expansion.

1. `A/work-items/RECON-MOS-959.md` (1–11); `A/reports/REQ-MOS-959.md` (1–117): scope and extraction under review.
2. `A/reports/SCENARIO-SURFACE-CONFIG-r2.md` (1–130), `A/reviews/R-SURFACE-CONFIG.md` (1–90), `A/decisions.md` (1–19): accepted evidence and boundaries, not substitutes for primary verification.
3. `A/sources/jira-api-delta-scenarios/r1/content.json` (43–69, only `/items/2` and `/items/3`); `metadata.json` (1–8).
4. `A/sources/wiki-245673187/r1/content.json` (single logical line 1, selected `/bodyView` sections below); `metadata.json` (1–14). Parsed inert HTML, never executed it.
5. `A/sources/api-live/r1/content.json` (line 1, four relevant operation descriptions and seven named configuration/create schemas); `metadata.json` (1–19).
6. `openspec/specs/surface-lifecycle-publication/spec.md` (177–198, especially 179–192): actual deferral artifact.
7. `openspec/specs/surface-registration/spec.md` (23–59), `openspec/specs/surface-skill-selection/spec.md` (128–145), `openspec/specs/surface-overview-connection/spec.md` (101–123): narrow existing ownership anchors, not implementation review.

### Provenance verified from saved bytes

| Source | Saved version/capture | SHA-256 (matches metadata) |
|---|---|---|
| API | r1; 2026-10-16T11:13:29.451Z; no ETag/Last-Modified | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` |
| Selected Jira | r1; 2026-10-16T11:23:51.742Z | `b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed` |
| Wiki 245673187 | r1; page v18, versionWhen 2026-10-09T23:34:11.543+08:00; retrieved 2026-10-16T11:45:08.223Z | `d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa` |

These are historical captures, not fresh network retrievals. Jira statuses remain Backlog (959) and Ready for test (1237); neither establishes delivery.

## Key Code / exact source locator key

API JSON-pointer prefixes: `C=/components/schemas`; `S=/paths/~1api~1control~1api~1surfaces~1v1~1surfaces`. `SAVE=S~1{surface_id}~1configuration/put/description`, `CREATE=S/post/description`, `DETAIL=S~1{surface_id}/get/description`, `SKILLS=S~1{surface_id}~1enabled-skills/put/description`. Concatenate literally. `U=C/UpdateSurfaceConfigurationRequest`.

Wiki locators all refer to `/bodyView`, exact heading ID plus source table row/field:
- W-C: `id-Бизнесанализ:Поверхности-Вкладка"Конфигуратор"`.
- W-G: `id-Бизнесанализ:Поверхности-Общиедлявсехвкладок.1`.
- W-D: `id-Бизнесанализ:Поверхности-4.3.Составсправочниковизначения` (only configuration dictionaries relied on).
- W-J: `id-Бизнесанализ:Поверхности-5.1.surfaces.configuration`.
- W-K: `id-Бизнесанализ:Поверхности-5.2.surfaces.configuration.cards[]`.

J959 and J1237 mean the respective `/items/3/description` and `/items/2/description` in the Jira capture.

## Per-category reconciliation and actionable corrections

| Category / extraction IDs | Supported facts and classification | Remaining unknown / correction |
|---|---|---|
| Exact placeholders, 011, 027–030 | **Supported, consistent layers.** W-C #0, W-J greeting and SAVE name `{имя}`, `{отчество}`, `{время суток}`. SAVE rejects other words in braces and unpaired braces. W-C #23 contains the literal defect `{время суток)`; this is not a fourth supported token. | Retire J959's exact-name **publication** blocker. Keep typo as source correction candidate; no parser rule inferred. Escaping, nesting, casing and time mapping remain unspecified. |
| Appearance, 001–008 | **Supported UI plus published contract.** W-C #2 and W-D give the five extracted presets/labels; W-C #3 requires manual HEX input; shape/font codes and round/moscow_sans defaults agree with API enums and CREATE. `U/properties/accent_color/pattern` is `^#[0-9a-fA-F]{6}$`, not a preset enum. CREATE default is `#B3121B`. | W-C #26 explicitly asks whether input is arbitrary/preset-only and with/without `#`. Transport format is no longer unknown; UI acceptance/conversion of bare HEX and any desired preset restriction remain product decisions. Do not claim the API resolves those UI choices or normalize case without evidence. In 002, “exactly listed presets” must not mean only those colors can be saved. |
| Content controls, 009–010, 013–024 | **Supported desired UI.** W-C #8–21 supplies grouping, initial greeting, add/delete controls, hints, empty states and disabled Add at five/four. The extracted hint strings are exact; the suggestion hint is not saved content. | No reorder policy, dirty equality algorithm or defaults overriding saved server values supplied. API support is not editor availability. |
| Actions / skill identity, 023–025 | **Supported; terminology needs precision, not invented contradiction.** W-D and `C/SurfaceCardActionType/enum` agree on message/skill/link. W-K says “код навыка”; SAVE precisely says “идентификатор навыка (UUID), сохраняется в каноническом виде строчными буквами”. Message ≤500; link absolute HTTPS ≤2000, query allowed, credentials/fragments forbidden. Generic `C/SurfaceCardActionRequest/properties/value/minLength=1`; type-dependent rules are prose. | Annotate 025: “code” is loose wiki terminology, not evidence of a separate skill-code payload. No need to decide between two concrete identifier formats: only API defines one. Selector display, link opening context and real preview action execution remain undecided. |
| Text/list bounds, 017, 022, 034–039 | **Supported publication, runtime unknown.** `U`: greeting 1–500; fallback max500/no min; suggestions max5, each 1–100; cards max4. `C/SurfaceCardRequest`: title 1–100, subtitle 1–200, required title/subtitle/action; optional accent defaults false. SAVE allows empty lists and forbids duplicate suggestions. | Supplement extraction rather than claiming Jira supplied numbers. MOS-1237 blank-input concern is not proof of deployed rejection. No `uniqueItems` or duplicate comparison algorithm; no UI accent-card control extracted from API's optional accent field. |
| Optional / missing / empty / whitespace | **Consistent layers, not demonstrated conflict.** W-J/W-K mark JSONB fields “нет”; they do not define PUT requests. `U/required` lists all seven configuration fields; action requires type/value. SAVE says missing field → REQUIRED, other rule violations → INVALID. `C/CreateSurfaceRequest/properties/configuration/anyOf` allows DTO or null and configuration is not required. | Do not turn optional stored-model descriptions into partial PUT permission, or J1237 into unconditional nonempty fallback. Empty collections differ from blank entries. SAVE requires nonempty greeting/items/card text/action; trims text edges. Whitespace-only acceptance is not authorized by minLength alone; exact trim/validation order remains unverified. |
| Fallback, 012, 035 | **Supported semantic refinement.** W-J: “Резервный текст приветствия, если имя неизвестно”; SAVE: for unauthenticated zone without resident name, only `{время суток}` allowed; required field, ≤500, nonempty when greeting uses name/patronymic, otherwise may be empty. CREATE gives default “Здравствуйте! Чем помочь?”. | Retire “fallback validation condition unknown” as a contract gap, not the editor gap. Wiki W-C does not supply fallback layout/help/preview treatment. No contradiction between broad use description and conditional save rule. A stricter desired rule would require an explicit product decision. |
| Transient preview, 026–030 | **Supported desired UI, not endpoint/runtime evidence.** W-C #22–25 gives Greeting/Dialog, styled mock substitutions, assistant greeting first then suggestions in Dialog, updates “без сохранения”. J959 requires examples explicitly populated. | This now has positive wiki evidence beyond earlier API-only absence. No exact persona/time samples, sample editing, fallback toggle or actual action execution policy supplied. Unsaved preview changes do not imply autosave or a preview API. |
| Normalization | **Partly specified contract, remaining edges unknown.** SAVE: “Текстовые значения сохраняются без пробельных символов по краям”; DETAIL returns saved configuration; UUID canonical lowercase explicit. | Replace blanket combined-evidence “no normalization statement” with these facts. Unicode length, trim-versus-length order, duplicate equality, greeting token canonicalization and input display policy remain open. No suggestion deduplication algorithm is authorized. |
| Save, 031–033 | **Supported UI intent + contract, deferred scope.** W-G #7 default Configurator tab; #13 Save changes visible when dirty. SAVE: full replacement, unchanged token/embed_code; DETAIL saved readback; updated_at not changed by configuration save. CREATE omission defaults and main spec omission/null are distinct from required complete PUT. | Correct 033: W-G #14 is an informational block **for Prod**, saying no surface release/re-embedding required, not a general timing/deployment guarantee. API invariant supports no re-embedding, not live application latency. Preserve unknown error/retry UX, dirty reset, navigation prompts and write-success/read-failure editor handling. |
| Stale skills / adjacent lifecycle | **Supported boundary, remediation unknown.** SAVE validates connected/nondeleted skill at save; CREATE only UUID format for card skill; SKILLS does not recheck cards after disconnect. W-G #9 explicitly leaves sandbox audience unclear; #12 describes save/publish. | Retained-reference/later rejection is a documented implication, not observed runtime. Do not auto-remove cards, block disconnect, tighten creation integrity, activate sandbox/publication save behavior or use hidden PUT to change lifecycle state. |

No genuine same-layer contradiction is established by the scoped combined evidence. Wiki desired UI, JSONB optionality, complete transport DTO and approved deferral address different layers. If stakeholders intend wiki optionality as **PUT omission permission**, that would conflict with `U/required` and “Конфигурация заменяется целиком”; ask that narrow mapping question only if such intent is asserted, rather than choosing precedence now.

## Architecture

Creation optionally carries the same `UpdateSurfaceConfigurationRequest` used by complete configuration PUT. Cards use `SurfaceCardRequest → SurfaceCardActionRequest → SurfaceCardActionType`. Desired editor controls feed transient previews; explicit persistence remains a separate concern. Saved normalization/readback cannot be inferred from preview state or unchanged timestamps. Existing skill persistence must not write configuration. Published API facts constrain future integration, while main-spec deferral governs current scope.

## Narrow ownership / no-op disposition

- **Current factual reconciliation owner:** this audit, `A/reports/REQ-MOS-959.md` and this review, interpreted alongside `A/reports/SCENARIO-SURFACE-CONFIG-r2.md`, `A/reviews/R-SURFACE-CONFIG.md`, `A/decisions.md` D-002. Candidate writer-gate updates only: add API cross-references without changing extraction provenance; qualify 002/025/033; distinguish resolved documentation gaps from outstanding UI choices; update “Confluence uncollected” only for the newly captured page. Historical reports remain preserved; this review is not writer authorization.
- **Actual deferral owner:** `openspec/specs/surface-lifecycle-publication/spec.md:179–192`, “MVP editing and deferred functionality boundaries” and “Configuration editor is not available”. It reserves PUT for a separate configurator and forbids fake/default/hidden configuration writes. **No-op now.** W-G default-tab intent does not revoke this boundary.
- **Existing adjacent owners, no edits now:** registration `:23–59` owns optional atomic configuration/defaults and unknown creation outcomes; skill selection `:128–145` owns enabled-skills persistence without configuration writes; overview `:101–123` owns **skill** draft/write/read recovery, not future editor recovery. Do not silently broaden those scenarios.
- Accepted r2/review already found no active configurator plan in their bounded discovery. This run did **not** repeat inventory or assert universal absence. Their hypothetical `openspec/changes/mos-959-surface-configurator/` proposal/design/tasks and `specs/surface-configurator/spec.md` remain hypothetical, not an existing owner or approved work. Future activation and any deferral delta require separate approval. No new active change is inferred.

## Decisions versus source gaps

**Product/design decisions still needed if activated:** HEX input UX/preset restriction; preview sample identities/time mapping and safe action behavior; fallback editor/help/default presentation/preview; stale-reference remediation and any stricter creation policy; dirty-state, navigation and recovery UX. Adjacent sandbox audience, publish/save orchestration and lifecycle choices remain outside this activation-free reconciliation.

**Contract/source clarification:** parser escaping/nesting/case, Unicode counting, normalization order and duplicate equality. UI default samples are not recoverable from the current evidence. Linked Jira contract wiki page 241082009 was not read; only 245673187 was collected here. MOS-1237 test-plan attachment is metadata-only (`/items/2/attachments/0`), comments/custom fields and attachment bodies remain unavailable. Collection remains globally incomplete.

**Runtime verification, not a product decision:** actual deployment, validation/error-envelope fidelity, persistence and resident-widget application timing. No saved status or published text establishes these. Nothing closes MOS-959/MOS-1237.

## Start Here

Read `openspec/specs/surface-lifecycle-publication/spec.md:179–192`, then this report's category table with SAVE and W-C #26. The immediate outcome is a factual evidence correction with unchanged deferred scope, not implementation authorization.

## Verification and limitations

Independently read material primary evidence and verified all three saved hashes. No completed code audit, historical API comparison or active-plan inventory was rerun. A narrow filename discovery for deferral returned only an unrelated archive directory; no archive contents were opened or relied on. Only the bound report was written. No network/browser/MCP, tests/build/generation, nested agents, Git mutations, source/spec/archive changes or external operations. No input/infrastructure blocker. Git index state was not inspected.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Reconciled all candidate categories against primary saved Jira/wiki/API evidence, supplied exact locators and verified hashes, actionable narrow corrections, unresolved decisions and unchanged deferral ownership."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-959.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python scoped JSON selection, SHA-256 and inert HTMLParser inspection","result":"passed","summary":"Verified three saved source digests and material configurator evidence without executing HTML or scripts."},
    {"command":"Bounded file reads, find deferral filenames, wc -l report inputs","result":"passed","summary":"Confirmed acceptance/deferral and narrow existing ownership; no inventory or code audit repeated."},
    {"command":"tests / build / generation / browser / network / MCP","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Accept bounded extraction; revise combined-evidence handoff with precise API qualifications and Prod context for candidate 033.","No demonstrated same-layer contradiction, scope activation, Jira closure or implementation claim."],
  "residualRisks": ["Publication does not establish deployed/runtime behavior.","Source collection incomplete; attachment bodies and linked contract page not inspected.","Preview, fallback editor, normalization edges, stale-reference remediation and adjacent lifecycle decisions remain open."],
  "diffSummary": "Only runtime-bound independent review report written.",
  "reviewFindings": ["No input blocker; narrow extraction/handoff corrections documented, deferral preserved."],
  "manualNotes": "Primary combined evidence independently checked. No implementation or task closure, source precedence, writer authorization or activation. Git index not inspected or changed."
}
```
