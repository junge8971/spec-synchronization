# RECON-MOS-1018 — source-to-plan disposition

## Decision

**Accept the extraction as a faithful Jira/wiki extraction; revise the combined-evidence planning conclusion, not its primary quotes.** Minimal factual corrections and explicit decision records are warranted. Do not close task 1.1, implement integration, select source precedence, or relax current-input/send/disclosure gates.

The strongest newly exposed tension is concrete: wiki MAC-6/T-19 blocks wizard send to checking on exact conflicts, whereas the published status description explicitly exempts `draft -> checking` from readiness recalculation. Single-phrase preflight cannot bridge that server-revalidation gap. Saving conflicting phrases is distinct from promoting a skill; automatic rework/training after save is not established by the scoped API descriptions.

## Code Context

### Files Retrieved

Paths below are repository-relative. JSON pointers/HTML heading and requirement IDs identify primary evidence more precisely than physical lines in compact snapshots.

1. `openspec/changes/reconcile-control-center-backlog/audit/work-items/RECON-MOS-1018.md` — complete assignment.
2. `openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-1018.md` — complete extraction, R01–R10 and tensions.
3. `openspec/changes/reconcile-control-center-backlog/audit/reviews/R-SKILL-CHECKS.md` — complete review; particularly findings 6–7 and existing deferrals.
4. `openspec/changes/mos-1018-skill-phrase-conflicts/proposal.md` (1–27), `design.md` (1–26), `tasks.md` (1–18), `specs/skill-phrase-conflicts/spec.md` (1–47) — complete assigned planning artifacts, independently read with line numbers.
5. `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-details-MOS-774/r1/content.json`, only `$.items[7]` (MOS-1018), and corresponding complete `metadata.json`.
6. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241080062/r1/content.json`, selected `$.bodyView` passages identified below, and corresponding complete `metadata.json`.
7. `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`, only the three operation descriptions below.
8. `docs/api/contracts/openapi-2026-10-15.raw`, only historical single-phrase POST operation (chronology).
9. `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511/r1/access-result.json` — complete documented 404 limitation.

### Key evidence / exact locators

**J** = Jira `$.items[7].description`. It requires server checking over the permitted registry, phrase/type/similarity/skill/domain display, exact send blocking, semantic warning, and explicitly asks for normalization and safe cross-team disclosure. Its “в API не определены” is a reported issue, not proof of current API absence.

**W** = wiki `$.bodyView`:
- `Мастер подключения навыка (MAC)`: MAC-5/6/11; ПРТ-МАС-4/5/6/7.
- `Карточка навыка: обучающие фразы (ФРА)`: ФРА-6/7; ПРТ-ФРА-1/4/5.
- `Карточка навыка: проверки (ПРВ)`: ПРВ-2/3/7/8/9/10.
- `Общие принципы раздела`: “Конфликт формулировок решается до обучения” and “Область видимости роли применяется всегда”.
- `Жизненный цикл навыка`: “На проверке” state.
- `Валидации и ошибки`: ПРТ-ВАЛ-4/5.
- `4.4. skill_conflicts`: optional `normalized_phrase`, `created_at`, `updated_at` rows.
- `C. Мастер подключения навыка`: T-18/19/23; `E. Карточка навыка: обучающие фразы`: T-42; `F. Карточка навыка: проверки`: T-47.

**P**, **I**, **S** = saved API exact JSON pointers:
- P: `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1phrase-conflicts~1check/post/description`.
- I: `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1intents/put/description`.
- S: `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post/description`.

P checks **one phrase**, excludes self, compares active groups of nondeleted skills globally, uses exact/blocking versus semantic/warning, returns percentage similarity ordered exact-first then descending semantic, and documents configurable threshold default 0.75. It explicitly saves nothing and changes no readiness checks. It explicitly exposes other-team skill/domain names; that is publication evidence, not approval of safe disclosure. The target skill may itself be inaccessible (documented 404).

I replaces the full group set and recalculates phrase/conflict checks transactionally, including old/new peers. A no-op does not recalculate or increment version. Its response has no checks; the description directs readers to the skill card. This supports save-time calculation, not a promise of automatic training or rework status.

S recalculates readiness for forward progression from checking onward, not `draft -> checking`. Semantic warning does not block. On readiness rejection, status/version/history are unchanged but recalculated checks persist. This does not authorize any new UI transition.

Historical pointer identical to P's operation, without `/description`, exists in `openapi-2026-10-15.raw`, with `requestBody` referencing `PhraseConflictCheckRequest`; the operation has no `description`. Thus **method existed historically; semantics are newly documented relative to that snapshot**, not a newly introduced method. No exact deployment/publication date or runtime behavior is inferred.

## Extraction disposition

| Claims | Disposition against independently read primary evidence |
|---|---|
| R01–R04, R06–R07 | Accept. J and W support global server checking, wizard/save triggers, display and exact/semantic distinction. Existing spec already covers most of this; do not duplicate requirements. R06 does not authorize blocking every forward button. |
| R05, R08 | Accept. W expressly requires highlighting, checks-tab count, table, blocking explanation and correction location. Current MOS-1018 plan does not explicitly cover highlighting/count; add bounded presentation planning, not a synthetic global total. |
| R09 | Accept unresolved normalization/disclosure. P supplies comparison scope, severity and score semantics but not accepted normalization examples or product approval of cross-team names. Do not continue calling all of these API-absent. |
| R10 | Accept as source requirement, not authorization to create `/submit` or reinterpret an existing command. W distinguishes draft save from send and checking state; S's checking exemption exposes an unresolved mapping/revalidation mismatch. |
| Tensions 1–4, 8 | Accept as scoped source omissions/questions. Revise combined wording: P supplies single-input scope and score/order; neither P nor I/S certifies an entire unsaved edited set through preflight. Existing freshness gates remain approved plan constraints even though W does not specify them. |
| Tensions 5–7 | Accept; sharpen with I/S. W ПРТ-ФРА-5 permits save but says rework follows; I establishes recalculation, not that status transition. W's save/send training language and no-training-on-conflict rule are unresolved, not automatically superseded by API descriptions. |
| Linked contract unavailable | Accept with updated evidence: GET returned 404, no body. Deletion, wrong ID and permission masking remain indistinguishable. This is documentation access failure, never business API absence. |

## Minimal proposed planning corrections

All targets below are under `openspec/changes/mos-1018-skill-phrase-conflicts/`. These are proposals only; no artifact edits or task closure performed.

| Exact existing target/text | Minimal replacement or addition | Evidence / unresolved decision |
|---|---|---|
| `proposal.md:25`, “не содержит метода конфликтов, нормализации, шкалы близости…” | Replace blanket absence with: “Опубликован single-phrase preflight; метод существовал в snapshot 2026-10-15, текущие descriptions уточняют scope, self-exclusion, exact/semantic, score/order. BLOCKED: согласованные примеры нормализации, безопасное раскрытие, привязка полного актуального набора и конкретная отправка с серверной повторной проверкой.” | P, historical operation; R-SKILL-CHECKS §6. Keep proposal:26 send decision verbatim. |
| `design.md:3`, “отсутствует global-check метод” | Replace only absence clause with published single-phrase/global-registry distinction; retain “сохранение фраз не подтверждает отсутствие конфликтов”. | P/I; no frontend implementation re-audit or claim about uninspected local `openapi.json`. |
| `design.md:13`, BLOCKED API list; `tasks.md:5`, task 1.1 | Separate documented facts (method/input, scope, self-exclusion, severity, percent/order/configurable threshold) from still-open acceptance (normalization boundary examples, whole-input binding, disclosure, command/server revalidation). Annotate method as existing, descriptions newly added. Keep checkbox open and tasks:3 integration gate unchanged. | P; J; R-SKILL-CHECKS §6. No hardcoded frontend threshold or local normalization algorithm. |
| `design.md:19–22`, Risks; task 1.1 acceptance | Add explicit unresolved matrix: (a) W permits save with conflict but says rework; I saves/recalculates, does not establish rework; (b) W wizard send→checking blocks exact; S exempts draft→checking; (c) W save/send training versus conflict prerequisite. Require owner mapping of save/send/recheck/training before implementation; do not invent training calls or broaden UI commands. | W ФРА-6/7, ПРТ-ФРА-4/5, MAC-6/11, T-23, principles; I/S. Existing deferrals and partial-registration recovery remain intact. |
| `specs/skill-phrase-conflicts/spec.md:18`, display requirement; `tasks.md:10`, 2.1 | Add conflict phrase highlighting in the existing editor/wizard, checks table and count, and corrective location for displayed conflicts, within permitted server data. Require count source/completeness to be agreed; do not equate one preflight response with total skill conflicts. | W ПРТ-МАС-4, ПРТ-ФРА-1, ПРВ-2/3/7/10, T-42. Do not create a second checks UI owner or claim a missing count API from this narrow review. |
| `design.md:13–16`; `tasks.md:13`, 2.4 | Add bounded trigger note: wizard checking and save-time checking are source requirements, but single-phrase preflight, persisted save checks and agreed-send revalidation are different operations. Reuse existing owners; do not block every save or demand a new preflight before every save by inference. | W MAC-5, ФРА-7/T-42; P/I/S. Actual send selection remains gated. |
| `specs/skill-phrase-conflicts/spec.md:35–47`, freshness scenarios | Add “Single-phrase preflight is not set readiness”: a clear response for one phrase neither changes persisted checks nor certifies other groups/current edits or enables the gated send. | P; existing full-input requirement. This strengthens coverage without inventing a batch endpoint. |

### Keep — justified no-op

- `proposal.md:7–10`; spec:9–28: existing global, display, exact/semantic and reuse requirements already cover R01–R04/R06–R07 substantially.
- `design.md:14–16,21–22`; tasks:11–13; spec:30–47: retain current-input invalidation, late-response rejection, pending/error/stale gate, server revalidation and neutral hidden-detail fallback. Wiki omissions do not rescind these decisions; P's cross-team names do not approve disclosure.
- No new `/submit`, `/check-phrases`, training, rerun or other lifecycle command from wiki decomposition. No automatic priority of Jira, wiki, historical contract or new descriptions.
- No task closure, implementation readiness claim, roles model, whole-module API inventory, or reopening of processing/applied-version/sandbox deferrals from R-SKILL-CHECKS.

## Scenario/test planning only

1. Add unit/component scenario for single-phrase clear result versus another unverified/edited group; persisted readiness remains separate. Existing late-response/network tests are kept, not duplicated.
2. Extend task 2.1's component coverage to highlighted conflicting input, table/corrective location, and agreed count with incomplete/unavailable result not shown as zero. Preserve hidden-detail/no-extra-request case already present.
3. After task 1.1 decision only: test save versus agreed send separately, including exact conflict, semantic-only warning, and server revalidation of a conflict introduced after preflight. Do not preselect save blocking or draft→checking behavior.
4. Record training/rework and wizard checking mismatch as acceptance questions, not executable expected transitions until agreed. Test only approved commands and preserve task 2.4's no-second-POST recovery assertion.

## Architecture / Start Here

Start with `proposal.md:25–26` and `design.md:13–16`: remove the stale blanket absence assertion while preserving gates. The architecture has three distinct boundaries: transient one-phrase comparison (P), persisted full-group save/recalculation (I), and selected server lifecycle revalidation (S). Neither state can be freely substituted for another. Resolve command/disclosure questions before attaching a UI gate to these boundaries.

## Validation and residual risks

Read-only local inspection and inert HTML parsing only; no tests, generation, browser/network/MCP, nested agents, or source/status edits. Jira/wiki metadata were read (saved timestamps and limitations, not independently rehashed). Only this bound report was written. Snapshot prose does not verify backend deployment, full input certification or implementation correctness; linked document remains unavailable. No index/staging inspection performed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Independently verified MOS-1018 Jira, selected wiki passages, three scoped API descriptions and historical method; mapped extraction dispositions and precise minimal changes to all assigned planning artifacts."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-1018.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Numbered reads of MOS-1018 proposal/design/tasks/spec and local Python extraction of bound Jira/API/historical operation","result":"passed","summary":"Confirmed existing gates, historical method and newly documented single-phrase/save/status boundaries."},
    {"command":"Local inert HTMLParser extraction of selected wiki phrase/conflict/send passages","result":"passed","summary":"Verified extraction quotes and save/send/training/disclosure tensions."},
    {"command":"Tests, generation, network, browser, MCP","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["Extraction accepted with combined-evidence qualifications; blanket API absence requires correction, not gate closure."],
  "residualRisks": ["Whole-input binding, normalization examples, disclosure and concrete send/server revalidation remain unresolved.","Wizard send-to-checking and training/rework statements require owner alignment; no precedence selected.","Linked documentation returned 404; snapshots are not runtime or deployment evidence."],
  "diffSummary":"Only authoritative review report written; no source/spec/status edits or staging actions.",
  "reviewFindings": ["revise: blanket absence of conflict method/score is stale.","retain gate: draft-to-checking exemption does not satisfy wiki wizard-send revalidation.","keep: approved freshness, neutral disclosure, command and recovery constraints."],
  "manualNotes":"Narrow independent source-to-plan review, not a repeat inventory/API audit. Proposed scenario additions only; no tests run or task completion asserted. Index state not inspected."
}
```
