# Lane 5 — MOS-1019 bounded join

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Local saved evidence only; no feature acceptance.

## Source and reuse boundary

Audit root **A** = `openspec/changes/reconcile-control-center-backlog/audit/`.
Exact member read: `A/sources/jira-details-MOS-774/r1/content.json#/items/8` (key MOS-1019), entire description, no attachments. It requests server questionnaire/phrase checks, classifier training, autotests, sandbox availability; run identifier, intermediate/final states, errors and update rules; removal of statically successful results; repeat subject to state/permissions. Its possible-problems paragraph lists undefined launch/status/results/ETA/retry contracts. Workflow “Ready for test” is not acceptance. Current-input correlation is a boundary needed to avoid claiming current phrase readiness, not an invented explicit Jira field requirement.

Reused first: `A/reports/SCENARIO-SKILL-CHECKS.md` and `A/reviews/R-SKILL-CHECKS.md` (complete), including accepted five-check semantics and follow-up-owner requirement. Lifecycle reuse: `A/reviews/R-SCENARIO-MOS-909.md:45–56`, especially C05; no repeat lifecycle audit or new correction to its approved command plan. Earlier member ledger `A/reports/G2-JIRA-MEMBER-JOINS.md:193` has MOS-1019 B with adjacent lifecycle evidence; this lane adds direct member/code/assertion joins.

API **S** = `A/sources/api-live/r1/content.json` (single line). **D** = `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/get/description`; **R** = `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/properties`. Independently read D, R fields status/checks/training/training_eta/autotest/autotest_note/version, full SkillCheckResponse/Type/Status schemas, and skills path names. Other mutation semantics below are explicitly reused accepted evidence, not a new operation inspection.

Main **M** = `openspec/specs/skill-checks-training/spec.md`; archive **H** = `openspec/changes/archive/2026-10-02-mos-1019-skill-checks-training/`.
Code **C** = `app/entities/skill/api/skill-details-client.ts`; **Q** = `app/entities/skill/model/use-skill-details-query.ts`; **W** = `app/widgets/skill-details/ui/skill-details.tsx`; **V** = `app/widgets/skill-details/ui/tabs/checks-tab.tsx`; tests **T** = `app/widgets/skill-details/ui/skill-details.test.tsx`.

## Requirement joins

| Exact member description clause | Saved API → baseline/owner | Actual implementation → written assertions | Disposition |
|---|---|---|---|
| “Отобразить серверный процесс… проверка анкеты и фраз” | S:D explicitly returns persisted checks, does not run them, permits empty array. SkillCheckType has anketa/phrases/exact_conflicts/semantic_conflicts/endpoint; SkillCheckResponse has status/blocking/message/checked_at. M:9–21,63–70 still limits display to status; H proposal:7–11 consciously deferred individual results. Accepted R-SKILL-CHECKS §1 owns documentary proposal, implementation follow-up owner unresolved. | C:15–51 validates status and legacy process strings but has no declared checks decoder; z.looseObject may retain unknown checks, so this is NOT evidence they are stripped. V:6–20 takes only status and displays unavailable-result notices. T:1153–1191 asserts status changes and unavailable notices, not actual five-check rendering. | Narrow planning delta warranted, already accepted; no full-result implementation/acceptance. |
| “дообучение классификатора, автотесты… промежуточные/конечные состояния… правила получения обновлений” | S:R/status plus training/autotest plain strings; ETA/note nullable strings without run protocol in inspected DTO. M:9–47 specifies read-only conditional observation. H tasks:5–6,10 explicitly owns MVP. | Q:7–20 opts into processing-only interval, stops on read error, background false; W:15 enables one observer. T:1051–1080 asserts 4999/5000 ms boundary, unchanged stage after 60 seconds and GET-only requests; 1083–1117 hidden/unmount/reopen; 1153–1179 stage updates and stop at sandbox. | Direct bounded observation join; no evidence of actual training/autotest execution or terminal run outcomes. Preserve narrower archived scope. |
| “Нужны идентификатор запуска” and readiness of current input | S:R/version is record version; checks.checked_at is a timestamp, not run/input revision. Inspected detail/check schemas provide no run identifier or processed-input binding. Accepted checks report peer-freshness finding says checks may change without peer version/updated_at changes. M:11,63–70 and H proposal:11 retain run/current-version deferral. | V:14–16 expressly disclaims current phrase readiness. T:1182–1191 asserts no run ID/ETA/progress/sandbox or repeat-training button. T:1119–1151 asserts abort and isolation on skill-ID change; this protects entity identity, not run correlation. T:1230–1274 preserves editing drafts and expected_version=2 after server version=5; this protects optimistic locking, not applied training revision. | Unresolved API/product owner decision; no client-generated ID, inference from timestamps, or readiness from current status. |
| “ошибки” | S:D documents read errors separately from check-result message/status. SkillCheckStatus includes failed, but accepted R-SKILL-CHECKS §1 forbids inventing technical-error mapping. M:49–61 distinguishes reading failure from processing failure; full process errors deferred by M:65. | W:32–36 shows last-loaded-data alert; Q:14 pauses interval on error. T:1194–1228 checks 503 read failure retains training, never says training failed, pauses polling and manual read recovers. No inspected assertion verifies process error payload or per-check corrective messages. | Observation error handling supported; process/check-result error UI remains outside delivered MVP, not absent backend proof. |
| “Повторную проверку разрешать по состоянию и правам” | S:D explicitly says GET does not launch checks; inspected skills path names contain no dedicated training rerun endpoint. Accepted checks/lifecycle evidence documents mutation-driven recalculation, not an approved repeat-training policy. M:25–27,65 and H proposal:25–29 preserve existing commands without new rerun. | W:22,53 uses refetch for read recovery; T:1194–1228 asserts retry remains GET-only and resumes only in training, not sandbox. T:1188–1191 asserts no repeat-training button. | Manual read retry is not recheck/retrain. No new permission mapping, automatic POST retry, or command authorization follows. Owner must supply state/permission/run-result contract for full request. |
| “Удалить статически успешные результаты”; “доступность песочницы” | S:D persisted results are actual returned facts but do not prove sandbox availability; accepted checks report distinguishes endpoint field completeness from service health/token/readiness. M:63–70 expressly forbids sandbox inference. | V:12–20 truthful current-stage and unavailable-result text. T:1069–1074 and 1182–1191 assert absence of invented success/progress and sandbox launch, even after sandbox status. | No-op for current MVP anti-fabrication boundary; not proof all server checks pass or sandbox works. Keep token/security work separate. |

## Minimal planning dispositions

1. **Attributable B → P suggestion for MOS-1019 member join only**, append a new reviewed MOS-1019 B→P overlay with this evidence; preserve G2-JIRA-MEMBER-JOINS.md:193 and its recorded hash verbatim: “Direct MOS-1019 description joined to archived status-observation scope, current GET-only code and written polling/error/draft assertions; persisted checks published but not displayed; run/current-input correlation, process errors/repeat and sandbox readiness remain deferred/unresolved.” This is traceability advancement, not feature/task closure or tests-passed claim.
2. Reuse the existing accepted readiness follow-up candidate (SCENARIO-SKILL-CHECKS / R-SKILL-CHECKS), do not duplicate it. No active implementation owner was established in this bounded lane. Parent should retain owner selection as unresolved rather than create a second owner or reopen historical tasks.
3. Exact suggested wording for approved follow-up amendment to M:9–11,63–70: “UI SHALL display returned persisted readiness checks, their status, corrective message and checked_at; an empty checks array means results have not been calculated. Reading the detail SHALL NOT be described as executing checks. Returned checks and status SHALL NOT establish training of the current edited phrase set or sandbox availability. Run identifiers, process outcomes/errors, rerun eligibility and processed-input correlation remain outside the observation MVP until their contracts and scope are agreed.” Add typed decoding and component assertions for ordered results, empty/uncomputed, failed/warning, stale read, same-version changed checks. This is proposed planning only, not authorization to implement.
4. Preserve H proposal/tasks verbatim as historical delivery boundary. Do not reinterpret its old API-absence wording as present publication truth. No new lifecycle correction: accepted C05 and the existing readiness rejection-refresh candidate already cover those seams.

## Actual reads and limits

Read common contract; complete member /items/8; complete accepted checks report/review; selected lifecycle review rows; complete main spec and archive proposal/tasks; complete C/Q/W/V; T:1025–1304 (assertion bodies, not just names). Targeted file/path searches and ledger matching lines only elsewhere. API inspection limited to named DTOs/GET and path names; no claim to exhaustive absence across every backend service. No wiki body re-audit: linked catalog context reused through accepted lifecycle/checks evidence. No archive test result is represented as a current execution. Missing run contract/owner remains unresolved; no new policy chosen. No source edits, credentials, network, browser, tests/build/typegen, or nested agents. Only this artifact written. Index state not inspected; no staging performed.

## Current-local SHA256 inputs

Paths use aliases above; hashes are current bytes, not git-show baselines.

```text
0d1083ea677d8b380789a33f5e56cd30357132ee476bd3362dc31243fc89fd59 A/work-items/G2-SKILL-REMAINING-SEVEN.md
e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208 A/sources/jira-details-MOS-774/r1/content.json
549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06 S
6f7d55e19d37b668de2df544ae6cfd371cb90500c39b125dced1713742459c5b A/reports/SCENARIO-SKILL-CHECKS.md
64c8e4caab3d46614cbb63b0ce6d691bd354ed124fae7150deb31651116df909 A/reviews/R-SKILL-CHECKS.md
8c930323b3a2d6644d8ea4613ae490a5237c11ab55b1d67e0d0de56c5e67cb5c A/reviews/R-SCENARIO-MOS-909.md
9ac5fe8a92ecff214ccdd1998b7d69a2d9083d0bd222ff62541945567c1152cc M
620afb965e1c05ab8ead562250526cdfa6b80b59849b9fd8323d9ea11498a8c4 H/proposal.md
95618108c97afdbf6f7b2920e8596d5fc2556754c9ccc2e20c1b8f36b4be0e08 H/tasks.md
de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6 C
88db0ee56655ee10d1dbd6df477679ecaedb838181d8339478214d39a16e1bbe Q
d7a1b1c2f751f4a00170637ae0b5f997be2448d4254b1ea8f5440d899101e067 W
a69b0948e9aecf25618b1db83c27d06a804885b61ab8848e55f84d260f1558a5 T
5d0cb5e0a71746e4d4b1e3e57d61f47974c80e79e5cdf6bf2383c6e4113fb3e0 V
```

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"MOS-1019 exact member joined to saved API, accepted evidence, baseline/archive, actual code and assertion bodies; minimal dispositions and current-local hashes recorded."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/d6423b11-4674-417a-a7c8-0db499c5efc6/join-skill-checks.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"git rev-parse HEAD; targeted rg; read-only JSON extraction; sha256sum","result":"passed","summary":"Local evidence and hashes obtained."},{"command":"tests/build/browser/network","result":"not-run","summary":"Prohibited by bounded audit."}],
  "validationOutput": ["Written assertions support status observation only; actual check results remain undisplayed."],
  "residualRisks": ["No runtime or deployment verification; process-run/current-input/retry contracts and follow-up owner unresolved.","Saved publication is not feature acceptance; parent package review pending."],
  "diffSummary":"Only configured output artifact written; no project source changes.",
  "reviewFindings": ["Reuse accepted persisted-check follow-up; do not duplicate lifecycle correction or close MOS-1019."],
  "manualNotes":"Read-only lane 5 only. No staging actions; existing index state not inspected. Historical validation is not current execution."
}
```
