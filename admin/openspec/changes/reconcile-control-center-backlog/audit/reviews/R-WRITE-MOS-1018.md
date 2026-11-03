# R-WRITE-MOS-1018 — independent publication review

## Verdict: ACCEPT

The actual four artifact revisions match the operator-approved scope. No revision requested. This accepts the documentation publication only; parent alone accepts publication, and implementation remains blocked on task 1.1. Earlier review proposals for broader presentation/count coverage were correctly not included.

## Code Context / Files Retrieved

Repository-relative target prefix: `openspec/changes/mos-1018-skill-phrase-conflicts/`.

- `proposal.md` lines 1–27; `design.md` lines 1–29; `tasks.md` lines 1–18; `specs/skill-phrase-conflicts/spec.md` lines 1–52: complete current artifacts and direct unified diffs against their immutable copies.
- `openspec/changes/reconcile-control-center-backlog/audit/work-items/R-WRITE-MOS-1018.md` and `work-items/WRITE-MOS-1018.md` under the same audit root: complete review assignment and exact approved scope.
- Audit `publication/WRITE-MOS-1018/baseline.json` and all four named `before/` copies: complete baseline and independently hashed bytes.
- Audit `reports/WRITE-MOS-1018.md`, `reviews/RECON-MOS-1018.md`, `reviews/R-SKILL-CHECKS.md`: complete reports, treated as claims/context, not primary proof.
- Audit `sources/api-live/r1/content.json`: the three exact operation descriptions identified below.
- `docs/api/contracts/openapi-2026-10-15.raw`: historical preflight operation keys and request body.
- Audit `sources/wiki-241080062/r1/content.json`: `$.bodyView`, inert HTML extraction of MAC-6, ПРТ-МАС-5/6/7 and T-19.

## Exact diff findings

| Target/current lines | Before → after evidence and disposition |
| --- | --- |
| `proposal.md:25` | Sole changed line: blanket method/score absence → historical single-phrase method plus newly documented semantics. Normalization, safe disclosure, full-input binding and concrete send/revalidation remain blocked. Lines 26–27 and all intent/scope text unchanged. Accept. |
| `design.md:3,13–15,24` | Replaces blanket absence and old undifferentiated gate; distinguishes publication facts from remaining acceptance decisions and transient preflight from persisted save checks and agreed-send validation. Adds unresolved wiki/status tension, without choosing precedence or transition policy. Accept. |
| `tasks.md:5,11` | Only tasks 1.1 and 2.2 text changed. Integration prohibition at line 3, eight unchecked task IDs/states, and all other tasks preserved. The new freshness coverage stays within the approved boundary. Accept. |
| `specs/skill-phrase-conflicts/spec.md:39–43` | Exactly one scenario inserted under existing freshness requirement. Removing this insertion reproduces the baseline byte-for-byte. No new requirement, count or presentation obligation. Accept. |

The new `design.md:13` phrase “exact блокирует” is explicitly introduced as a published fact, corresponding to API exact/blocking classification. It does not select a UI send policy: lines 14, 17 and 24 retain the agreed-command gate; proposal line 26 and tasks lines 3, 5, 13 preserve it independently. The draft-to-checking exemption is recorded as source tension, not implemented or silently reconciled.

Unchanged safeguards verified in direct diffs: `design.md:16–19` current-input/skill-ID invalidation, stale-response rejection, transport/AbortSignal, pending/error handling, neutral disclosure without extra requests/client RBAC, and FSD composition; lines 23, 25, 29 retain TOCTOU, reuse and migration boundaries. `tasks.md:13` retains partial-registration recovery without second POST and blocking only the send agreed in 1.1. Existing spec scenarios remain unchanged. No lifecycle command, disclosure approval, frontend threshold, source precedence or completion claim was added.

## Independent primary-source verification

Let API base be `/api/control/api/skills/v1/skills/{skill_id}` in audit `sources/api-live/r1/content.json`:

1. `$.paths[base + '/phrase-conflicts/check'].post.description` explicitly says “Проверить одну фразу”, “Метод ничего не сохраняет и результаты проверок готовности не меняет”; excludes self; compares active groups of nondeleted skills globally; classifies exact/blocking versus semantic/warning; documents percentage similarity, exact-first/descending-semantic ordering, configurable default 0.75, and other-team skill/domain names. Supports proposal 25, design 13/15 and the new scenario, but does not authorize disclosure or whole-set certification.
2. The identical historical operation in `docs/api/contracts/openapi-2026-10-15.raw` exists with request schema `#/components/schemas/PhraseConflictCheckRequest` and no `description` key. Supports “method existed; semantics newly documented relative to snapshot,” not a new-method or deployment-date claim.
3. `$.paths[base + '/intents'].put.description` states full group replacement, transactional phrase/conflict recalculation, no-op without recalculation/version increment, and response without checks directing readers to the skill card. Supports design 15. It does not establish conflict-free readiness or choose save as the blocked action.
4. `$.paths[base + '/status'].post.description` explicitly exempts `draft -> checking` from readiness requirements/recalculation and describes forward checking-to-prod progression. Wiki `$.bodyView` MAC-6 and T-19 explicitly block wizard “Отправить на проверку” on exact conflicts; ПРТ-МАС-7 gives resulting “На проверке”. Supports the precise unresolved tension at design 24/tasks 5, not a selected transition policy.

## Before/after SHA-256 verification

Independently recomputed from bytes; every immutable copy matches `baseline.json`, and every current hash matches the writer report. Paths below are relative to the target prefix above.

| Artifact | Verified immutable before | Verified current after |
| --- | --- | --- |
| `proposal.md` | `9afa3083fcead3b03c892d3fce3f7aeea2e0a802a4d1e4c470f4d3c2332215f5` | `8a5437a6850b21aa0d1b6343527b22f2c002cb87e14b5b2416a7b43daffd01df` |
| `design.md` | `339d8a7a338c3a9937c8a252d2c340e188e5328a3c414bf9c2ad8325e6f87b0f` | `624af037030f75831ab0dc3068808b0659f007088a1441b2aac88c07d1624a0a` |
| `tasks.md` | `ee02382ebeafe2f35b9f9b646e25934b1b4b17aac9b8f033a1063ae9d3fe63ef` | `fd18b43481483c2c42aeb08aeaf73b9f339d1d7b317eb725b954daf0ef1fb66a` |
| `specs/skill-phrase-conflicts/spec.md` | `499103ce10274ddf12eed84974757f5a169f21e17f55c8cf83e5a888ebc17b6c` | `479fc93a9e4133d32af81e763c686730395114641386a36d72ef510d8d355808` |

Checkbox comparison independently passed for 1.1, 1.2, 2.1–2.4, 3.1, 3.2: all remain unchecked.

## Architecture / Start Here

Start with `design.md:13–18,24`: transient single-input comparison, persisted save-time checks and agreed-send server validation are separate boundaries. Task 1.1 still owns unresolved acceptance; no integration may proceed based on publication alone.

## Validation and residual risks

Local read-only Python hashing, direct diffs, numbered reads, JSON extraction and inert HTML parsing passed. Strict OpenSpec validation was not independently rerun; the writer reports success, not reviewer validation. Tests/build/generation/browser/E2E/network/MCP, archive/sync and nested agents were not run. Only this report was written.

The four baseline-bound artifacts are fully compared; no repository-wide ignored-file integrity claim is made, and no index/staging state was inspected. Saved descriptions are not deployment/runtime evidence. Normalization examples, safe disclosure, full-current-input binding and concrete send/revalidation policy remain unresolved. The linked wiki-contract 404 limitation remains unchanged and was not used to infer API absence.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Accept: independently compared all four actual artifacts to immutable copies, verified all before/after hashes, checked primary API/historical/wiki evidence, and preserved eight unchecked tasks and unresolved gates."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reviews/R-WRITE-MOS-1018.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Read-only Python SHA-256, direct unified diffs and numbered target reads","result":"passed","summary":"All four immutable hashes match baseline; all four current hashes match writer report."},
    {"command":"Read-only Python primary API/historical JSON and inert wiki HTML extraction","result":"passed","summary":"Verified changed factual claims and draft-to-checking source tension independently."},
    {"command":"Read-only checkbox comparison and exact spec-insertion removal comparison","result":"passed","summary":"Eight unchecked IDs preserved; remaining spec bytes unchanged."},
    {"command":"Strict OpenSpec validation","result":"not-run","summary":"Optional; writer result not represented as independently rerun."},
    {"command":"Tests, build, generation, network, browser/E2E, MCP, archive/sync","result":"not-run","summary":"Prohibited by assignment."}
  ],
  "validationOutput": ["ACCEPT documentation publication only; no implementation acceptance or task closure."],
  "residualRisks": ["Normalization, disclosure, whole-input binding and concrete send/revalidation remain gated.","Saved publication does not prove deployment/runtime correctness.","Review establishes four baseline-bound diffs, not repository-wide ignored-file integrity; index state not inspected."],
  "diffSummary":"Only bound review report written; four reviewed product artifacts not modified by reviewer.",
  "reviewFindings": ["No blockers: exact four approved revisions, no broader presentation/count obligations or policy selection."],
  "manualNotes":"Fresh independent review used primary saved sources rather than author summaries. Parent alone accepts publication; integration remains blocked on task 1.1. No staging actions performed."
}
```
