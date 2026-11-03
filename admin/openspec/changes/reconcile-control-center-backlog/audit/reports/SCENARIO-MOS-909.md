# Code Context

## SCENARIO-MOS-909 — bounded documentary reconciliation

**Result:** MOS-909's newly saved description does not require reopening the approved three-command/current-state MVP. It expressly distinguishes prototype codes from API codes. Two current-document consistency candidates remain: the already accepted disabled/eight-status correction, and qualification of blanket claims that the API supplies no results/ETA. Broader wiki history visualization and approved/rejected modeling remain source/owner reconciliation, not authorization to extend the UI. No implementation audit was performed.

All paths are repository-relative. **A** = `openspec/changes/reconcile-control-center-backlog/audit`; **C** = `openspec/changes/archive/2026-10-02-mos-909-skill-current-status`; **R** = `openspec/changes/archive/2026-10-02-mos-909-skill-lifecycle-rollout`; **S** = `openspec/specs/skill-lifecycle/spec.md`. These aliases expand to exact paths below.

## Files Retrieved

Complete MOS-909 baseline read, including continuations of truncated tool output:

- `C/.openspec.yaml` (1–2), `C/proposal.md` (1–28), `C/design.md` (1–27), `C/specs/skill-lifecycle/spec.md` (1–41), `C/tasks.md` (1–18).
- `R/.openspec.yaml` (1–2), `R/proposal.md` (1–27), `R/design.md` (1–68), `R/tasks.md` (1–24), `R/verification.md` (1–22).
- `R/specs/skill-lifecycle/spec.md` (1–68), `R/specs/control-center-mock-server/spec.md` (1–57), `R/specs/skill-training-phrases/spec.md` (1–30). Phrase constraints were read for complete archive context, not reopened.
- `openspec/specs/skill-lifecycle/spec.md` (1–98); `openspec/specs/skill-global-toggle/spec.md` (1–94).
- `A/work-items/SCENARIO-MOS-909.md` (complete); `A/sources/jira-MOS-909/r1/content.md` (1–26) and adjacent metadata (complete).
- `A/sources/api-live-status-readable/r1/content.json` (1–894, complete operation and 24 referenced schemas), its metadata and `A/sources/api-live/r1/metadata.json` (complete). Original full API content was not independently re-inventoried.
- `A/sources/wiki-241097511/r2/content.json`: `/version`, complete `/bodyView` via inert HTML text parsing, particularly §§1.3, 2.6, 2.8–2.10, 3–4; adjacent metadata complete.
- `A/sources/wiki-241080062/r1/content.json`: scoped `/bodyView` sections “Жизненный цикл навыка”, ЖЦ-1–6, КАРН-3–6, ПРТ-КАРН, ОТК/ПРТ-ОТК, dictionary §§7.1–7.4, T-26–29/T-34/T-82–87; adjacent metadata complete. JSON pointers/section labels identify these HTML strings, not fictitious physical line ranges.
- `A/decisions.md`: complete file, specifically stable headings D-015–D-017; `A/reviews/R-SCENARIO-MOS-1145.md` (1–181), `A/reviews/R-DELTA-MOS-1119.md` (1–74), `A/reviews/R-DELTA-MOS-1119-TESTPLAN.md` (1–90), complete.
- `openspec/changes/mos-1031-skill-audit-history/design.md` (1–26), `tasks.md` (1–17).
- `openspec/changes/archive/2026-10-02-mos-1019-skill-checks-training/proposal.md` (1–29); `openspec/changes/archive/2026-10-02-mos-1020-skill-review/proposal.md` (1–29); `openspec/changes/archive/2026-10-05-mos-1021-skill-bulk-rollout/proposal.md` (1–28).

### Provenance

Jira capture: 2026-10-19T07:21:29.300Z, external update 2026-10-16T19:22:23.479+0800. **This run independently computed** SHA-256 over the saved normalized Markdown: `b2def825eb88fa33d1e553a33d7c75fca087f4593c1c431e5daf7f68baabda72`, matching assignment/metadata. This is not a raw Jira-response digest.

Other digests are **metadata/parent-attributed, not recomputed here**: catalog wiki `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47`; skills wiki `4920e62124826b90c86ae1d6ec520f49f52a4d381334c94867864c1f218c3ab2`; original API `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`; derived subset `1346f28284551b1b7924132525730e76023fc9ffea7c2a92a60a51c53fb474ef`. Derived subset equality/reference completeness is attributed to parent metadata, not independently recomputed.

The API is the 2026-10-16 saved publication, not a fresh deployment observation. Skills wiki is page revision 17; catalog wiki page revision 6 has body heading v1.0 versus history v1.1 dated 14.09.2026. Preserve the earlier catalog r1 failure and unknown cause. Capture/page/body revisions do not establish source precedence.

## Key Code / Contract Evidence

No application code inspected. In the readable API packet, `/operation` corresponds to original pointer **OP**:

`/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1status/post`

Schema locators below mean original `/components/schemas/<name>`, available as literal keys `#/components/schemas/<name>` under the derived packet's `/references`.

- `SkillStatus/enum`: draft, checking, training, autotest, sandbox, review, whitelist, prod, **disabled**; no approved/rejected.
- `ChangeSkillStatusRequest`: required status and integer expected_version ≥ 1; optional nullable string reason. OP requires UUIDv7 skill_id and UUID Idempotency-Key.
- OP 200 references `TsamResponseSchema_SkillResponse_`, whose data references **`tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse`** (not an unqualified SkillResponse schema).
- That DTO requires status/version, checks, training, training_eta, autotest and autotest_note. Training/autotest are strings; ETA/note are nullable strings. `SkillCheckResponse` requires check_type/status/blocking/message/checked_at. None of these fields alone supplies a completed lifecycle history or binding of a run to the current phrase revision.
- OP `/description` publishes fresh readiness calculation, named failures, queue behavior and permission/header requirements. `/responses` explicitly describes only 200 and 422; the latter references HTTPValidationError. Named business-error prose is not a complete matching response-schema guarantee.

## Stable candidates and disposition

### MOS909-C01 — Existing current-state/command ownership: no-op

**Evidence:** Jira content lines 10–13 asks for scale and state-dependent commands and agreement on codes; C proposal 7–11/design 13–17 covers read-only current status. R proposal 7–9, design 17–46 and S:11–35,49–74 explicitly approve the eight-stage neutral scale and only `draft → checking`, `sandbox → review`, `whitelist → prod` in this feature.

**Disposition:** No duplicate plan or new approval gate for these existing commands. R explicitly replaces the earlier G5 restriction while retaining the read-only header; C's historical “no scale/commands” is not the current policy. Preserve confirmation, version/status snapshot, one pending request, server-derived result, mismatch warning and unknown-outcome read recovery. Backend admissibility is not guaranteed by the frontend matrix. Jira shorthand adds traceability, not a fourth command.

### MOS909-C02 — approved/rejected: resolved MVP distinction, unresolved broader source model

**Evidence:** Jira line 10 lists approved/rejected but expressly says prototype codes must not be declared API codes. Skills wiki `/bodyView`, lifecycle list and §7.3 skill_statuses, lists eleven states including approved/rejected/disabled; published `SkillStatus/enum` lists nine without approved/rejected. R design 30 already rejects adding these prototype codes. MOS-1020 proposal 7–11,26–29 explicitly approves `review → whitelist`, postponing persisted decisions/return and forbidding invented approved. MOS-1021 proposal 8–11 separately postpones approved→whitelist.

**Disposition:** Do not mislabel this as a newly discovered missing MOS-909 implementation or demand runtime approved/rejected. The approved mapping is already decided for the MVP. The broader wiki state model versus published enum remains an unresolved product/contract model difference for lifecycle/review owners: does a future revision introduce states or retain separate review decisions? Do not choose aliases (`approved=whitelist`, `rejected=draft`) or reopen existing review approval. The generic no-command-at-review rule belongs to MOS-909's card feature, not a prohibition on the separately approved review capability.

### MOS909-C03 — disabled is no longer an unknown enum: bounded correction, already owned

**Evidence:** S:37–40 calls disabled unpublished and S:78–83 only describes eight published statuses; saved `SkillStatus/enum` includes disabled. Current `skill-global-toggle/spec.md:11–27,38–46,58–64` requires recognized disabled state and dedicated disable/enable, preserving the 13.10.2026 prod→disabled→prod approval. D-015 and R-SCENARIO-MOS-1145 C02 already accept this precise current-document correction candidate; D-016–017 retain it.

**Disposition:** Reuse that candidate rather than create a second plan: qualify current lifecycle/header enum wording and disabled handling under separate toggle ownership in a future authorized documentary pass. Do not append disabled as a successful ninth linear progression step, permit generic POST status disable/enable, or loosen unknown-state validation. OP's disabled queue exemption is not a dedicated-command bypass. Preserve approved prod-disabled-prod behavior; externally disabled non-prod restoration/dictionary integration remains the existing owner question, not a reason to revoke approval or invent a latest-history-row algorithm. Historical MOS-909 archives stay intact.

### MOS909-C04 — Future-stage visualization is not completed history

**Evidence:** Skills wiki `/bodyView` ЖЦ-3, КАРН-3 and T-26 request completed/current/future stages; R design 32–34 and S:15–16,30–35 deliberately show all eight stages with only current highlighted, every other stage neutral. MOS-1031 design 13–17/tasks 3–5 retains a history Query API gate. The inspected status DTO has no transition-history array.

**Disposition:** Future/later stage labels are already present in the approved scale; no-op for their visibility. Do not turn “future” into predicted next action, ETA or guaranteed path. Completed-stage checkmarks are a genuine broader source-versus-approved-MVP difference, but consciously excluded, not an accidental missing scale. Lifecycle owner must reconcile any future richer visualization with a real history reader and branching/repeated/disabled semantics; MOS-1031 remains the reader owner. Persistence descriptions or current enum order cannot fill this gap. No synthetic completion or new reader plan.

### MOS909-C05 — Readiness/currentness: narrower API wording candidate, not readiness activation

**Evidence:** S:30 says the API supplies no completion/errors/ETA and S:78 correctly denies that status proves current-phrase readiness. R design 5 and 32–34 describe the historical publication. The saved namespaced SkillResponse now has required checks/training/autotest and nullable training_eta/autotest_note. OP `/description` requires recalculation of all five checks on forward advancement; draft→checking and review→draft/whitelist→review exceptions do not recalculate. Missing results are not passed; semantic-conflict warnings do not block. On readiness refusal, status/version/history remain unchanged while recalculated checks and checked_at persist.

**Disposition:** Candidate narrow qualification of S:30's blanket API-absence rationale against this saved publication: distinguish available check/process metadata from unavailable completed-stage history/current-input-bound readiness. Do not remove neutral scale safety or infer valid ETA semantics from a nullable string. MOS-1019 proposal 7–11,21–29 owns status observation and explicitly defers run/result/current-version proof; MOS-909 retains its existing three commands. Any follow-up should preserve refusal context and truthful reread of checks, not assume whole-card rollback. D-017/R-DELTA-MOS-1119-TESTPLAN TP07 already preserve the persisted-check exception. No fresh check UI, rerun command, readiness bypass or frontend recomputation is authorized.

### MOS909-C06 — Unknown, stale and uncertain state safety: no-op with publication-aware enum

**Evidence:** S:18–26,49–59,71–98; C design 16 and R design 42–46. OP description includes VERSION_CONFLICT, SKILL_CHECKS_BLOCKED, PHRASE_REGISTRY_BUSY and IDEMPOTENCY_KEY_REUSED; explicit 422 schema differs from named-error prose. Catalog wiki `/bodyView` §2.9 describes generic key/method/URI/body/user scope and replay, without retention duration; it is not a complete status-command operation contract.

**Disposition:** Keep strict unknown/missing/non-string detail errors, no default draft/prod, no stale confirmation, no optimistic transition or automatic POST retry, and new conscious confirmation after successful recovery read. Disabled is the known exception addressed by C03, not a general unknown fallback. A newer status/error publication may inform a bounded owner contract update, but neither source examples nor queue-busy “can retry” wording overrides the approved conscious-retry boundary. No declaration of exactly-once delivery, guaranteed replay, universal rollback or error precedence.

### MOS909-C07 — Linked catalog contract is not missing lifecycle agreement

**Evidence:** Jira directly links wiki241097511. Its saved `/bodyView` §1.3 skill model omits status, §§2.1–2.8 publish catalog CRUD, §2.8 mutable fields omit status, and §2.9 describes concurrency/idempotency. The inspected API OP separately publishes status POST; R proposal/design explicitly selected it.

**Disposition:** Source coverage/version difference, not proof the backend has no lifecycle API or that approval must restart. Record the catalog link as historical CRUD context. Do not send status through PATCH or infer extra endpoints from wiki decomposition examples. Preserve existing historical auth approval as carried by D-015–017; cookie/header prose differences are not authority to change transport/security. This report performs no new auth reconciliation.

### MOS909-C08 — Evidence and neighboring scope: no closure

**Evidence:** Jira content lines 20–26 includes two comments, one MR18 mention and one assertion of checks for eight statuses, data refresh and bad values. C tasks 13–18 and R verification 5–22 record historical verification and limitations. Skills wiki КАРН-4, ОТК/ПРТ-ОТК and T-27/T-87 request duration/live-state behavior; current toggle spec 13 explicitly excludes durations/metrics from MVP.

**Disposition:** These comments and archived records are attributed claims, not this run's code/test/runtime attestation. MOS-909 newly saved source supplies no independently verified implementation delta. Preserve separate MOS-1027 toggle/live-state boundary, MOS-1020 review, MOS-1021 bulk, MOS-1019 observation and MOS-1031 history ownership. Richer duration/propagation/history requests are not proved delivered by a confirmed status. No task/feature/global closure or new activation follows. D-016–017 storage/test-plan conclusions are reused only with their named reviews; this run does not redo MOS-1119 storage analysis or execute its test plan.

## Architecture

Existing detail reading supplies the common header and lifecycle state; the approved MOS-909 feature offers three guarded status commands, with server replies updating detail/registry and uncertainty resolved by reading. Review, bulk, observation, dedicated global toggle and future history reader have separate owners. This describes approved documentary architecture from R design 36–46 and neighboring proposals, not inspected implementation. Historical current-status restrictions were deliberately superseded by rollout; later disabled support must not be rejected using the earlier eight-state snapshot.

## Start Here

Open `openspec/specs/skill-lifecycle/spec.md:28–40,76–83` alongside `openspec/specs/skill-global-toggle/spec.md:11–27,38–64` and D-015 before any separately authorized correction. C03 is already accepted documentary debt; C05 is a bounded wording candidate. C01/C06/C07 need no new plan, and C02/C04 need no reopening of approved MVP choices.

## Limitations

No code inspection, tests/builds, network/browser/MCP, endpoints, SQL, credential operations, nested delegation, Git operations, product edits, source edits, sync or archive occurred. Only this designated report was written. Repository index/worktree state is uninspected; no empty-index attestation. No new complete API inventory or live environment verification. Source chronology does not choose precedence. Historical test claims are not current execution evidence; lifecycle history, revision-bound readiness and backend transition/restoration enforcement remain unverified. This report is candidate evidence for parent review, not acceptance of product delivery.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Eight stable evidence-located candidates distinguish existing MOS-909 approval, unresolved broader source differences, disabled documentation debt and bounded readiness wording; complete MOS-909 archives/main spec read."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/SCENARIO-MOS-909.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local find/read/grep and read-only Python JSON/HTML inspection; hashlib.sha256 of saved jira-MOS-909/r1/content.md","result":"passed","summary":"Read required documentary packets; MOS-909 saved Markdown digest matches assignment and metadata."},
    {"command":"Tests/builds, network, browser, endpoints and Git inspection","result":"not-run","summary":"Outside bounded documentary assignment; no implementation or index attestation."}
  ],
  "validationOutput": ["MOS-909 SHA256 b2def825eb88fa33d1e553a33d7c75fca087f4593c1c431e5daf7f68baabda72", "Historical approvals retained; no new generic command or source precedence selected."],
  "residualRisks": ["Implementation/runtime/test execution unverified.", "Broader wiki history and approved/rejected model remain owner reconciliation; disabled correction already owned.", "Saved API has readiness/ETA metadata but does not establish completed history or current-input readiness binding.", "Index/worktree state uninspected; non-Jira digests and derived-subset equality remain attributed metadata evidence."],
  "diffSummary":"Only designated documentary report written; no project product/source changes.",
  "reviewFindings":["No blocker to returning bounded evidence; independent parent review remains required."],
  "manualNotes":"Documentary candidate mapping only. No task closure, feature activation, source precedence or renewed historical approval request. No fresh implementation audit."
}
```
