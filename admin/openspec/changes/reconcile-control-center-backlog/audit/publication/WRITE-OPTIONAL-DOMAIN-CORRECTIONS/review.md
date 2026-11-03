# Fresh bounded corrective-package review

## Verdicts

| Package | Verdict | Mandatory findings / exact patch |
| --- | --- | --- |
| fix-knowledge-base-export-limit-feedback | **ACCEPT** | None; no patch required. |
| clarify-ab-testing-sample-size | **ACCEPT** | None; no patch required. |
| fix-skill-domain-zone-read-compatibility | **ACCEPT** | None; no patch required. |

Planning-package acceptance only. Parent alone integrates accepted new directories; no implementation, runtime, deployed behavior, archive or feature acceptance follows.

## Review evidence

Read the assigned work item, complete seven-lane review, all three writer receipts and all 15 candidate files including metadata. Read all three affected main specifications completely. Independently compared all four MODIFIED requirement blocks: every original paragraph and scenario is retained verbatim; unmodified requirements remain outside the deltas. Proposals, designs, deltas and tasks agree on bounded corrections.

- **KB:** Exact HTTP 422 plus `EXPORT_LIMIT_EXCEEDED` classification, server message retained and locally supplied narrowing advice; regression envelope contains no advice. Different-code 422 is explicitly negative. Selected fields/order survive retry, with no file, false success or automatic replay. Limit, transport, saved-detail/session behavior and optional isolation remain unchanged.
- **AB:** Accessible per-group label (or associated explanation in the requirement), with direct label chosen in design/tasks. New/detail coverage, null default/clearing, inclusive bounds and invalid values are explicit. One nullable scalar, defaults and payload shape stay unchanged; execution disclaimer remains. No statistics, traffic or broad rewrite.
- **Domain:** String-code list/detail/PUT responses, explicit known labels and raw-code fallback; server order/count and linked inactive values retained. Read snapshots remain separate from fixed assignment choices. Editor preservation and generic zone-rejection coverage prohibit silent loss, false success and automatic modified-body retry. Successful PUT response reading does not promise unchanged-inactive write eligibility. Dynamic selector/directory, rejection payload specifics and inactive-update/omission/null policy remain unresolved separately; creation choices, PUT/version/idempotency and uniqueness/address deferrals are retained.

All 14 tasks remain unchecked (5 KB, 3 AB, 6 domain). Metadata consistently declares `spec-driven`, created `2026-10-20`. Receipts attest native dependency-ordered artifacts, strict validation and explicit five-file Prettier checks for each package. Current bytes match those validated manifests. This is proportionate schema/format evidence; no broad validation rerun was needed.

## Integrity and freshness

Source HEAD independently confirmed: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Source staged-name query empty. Local SHA-256 checks matched all 15 output hashes, all four receipt-recorded source-spec hashes and their isolated baseline copies, plus all five KB receipt-recorded implementation-input hashes. Hashes establish current local bytes, not deployment or source-server authenticity.

Source specs (relative to source root):

```text
87733e1890d135f29ef5629b8e1b2a3735e4f8fa3e8c9fdbad995a491c400973 openspec/specs/knowledge-base-export/spec.md
7cffebc09d33477bc300ec9c76f2989c9e095846e2a90fc74747b3393c2d13e9 openspec/specs/ab-testing-editor/spec.md
0013ea05d4c913d321baae18dca1076029792bf58ffc06e6a1715d53eca60366 openspec/specs/ab-testing-module/spec.md
b5f3ffc7329e9315b94484b0ce0333711634708779cd3b07fba734fdbbb66f25 openspec/specs/skill-domain-management/spec.md
```

Reviewed output hashes, paths relative to each exact assigned candidate change root:

### fix-knowledge-base-export-limit-feedback

```text
ff4326f8b42dcf8851877f4f3989c7fecb8f97d8154686d7d74b7281b70e6b9b .openspec.yaml
7fc0c3ce641d76d24006590749d95ff458f236b33abc4b9bede66eebe9e5f7d4 design.md
8aac481ba21906ae1df106d3d4a65c0740d090ff4be503724edc99a068d998c8 proposal.md
d811d2612b24415e32074c60397cf3d73b7669c6e1499f6f9e010fa170baded3 specs/knowledge-base-export/spec.md
0e3cf32ae03d54915f15618663ad4bbece0f7dbecbf159d35a80287efa26e95b tasks.md
```

### clarify-ab-testing-sample-size

```text
ff4326f8b42dcf8851877f4f3989c7fecb8f97d8154686d7d74b7281b70e6b9b .openspec.yaml
7cfeb9eb60671afa465c6a29024c35b259f3595d6654aaa191e1e6da86a6e360 design.md
954782185e03b5e6395f149c295a539a3157262d3ff2cebd8bb8441760945ec1 proposal.md
b1741fd5bde9283f4cdccf85078f8f09e0b4d223c145b5b217fac0980e2508fe specs/ab-testing-editor/spec.md
cbf39a5ca1a4a2067cae448e9b68d762e342484377a8bdeb5146894a80a9ed27 tasks.md
```

### fix-skill-domain-zone-read-compatibility

```text
ff4326f8b42dcf8851877f4f3989c7fecb8f97d8154686d7d74b7281b70e6b9b .openspec.yaml
8b62c36d86fb8c4fd86f6d8aa886d6067660349f8c68f796ae4287ac7b8e0d91 design.md
d3f3e440314acbdf5e0871b0431422b790886e2db77b354de190d928218c970c proposal.md
9cd7ec1d67bbd106d851f5cfd1bce5b4c6baf5af64c319622e32b181a8dd9f95 specs/skill-domain-management/spec.md
5d00d6e69c1d754139b1e12bec759dede78c034c643f129f8a4bc12138f93404 tasks.md
```

## Limits

No project/candidate edits, tests/builds, network/browser, credentials, nested agents, sync or archive. Only this external report was written. No implementation audit was repeated. Runtime accessibility, real backend envelopes and delivery remain unverified. Retained domain policy decisions are not blockers for these read/preservation plans and must not be decided implicitly during implementation. Parent should preserve these bytes and recheck freshness if integration is delayed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Three ACCEPT planning verdicts after complete 15-file review, original-block preservation and current manifest/source freshness checks."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/4e940772-c914-48b5-a110-22fe8d3a4e27/review-optional-domain-correction-plans.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"git rev-parse HEAD; git diff --cached --name-only","result":"passed","summary":"Expected HEAD; no staged files."},{"command":"Local Python SHA-256, complete-original-paragraph and unchecked-task verification","result":"passed","summary":"15 output hashes, four source specs/copies, five KB inputs and four modified blocks matched; 14 tasks unchecked."},{"command":"tests/build/browser/network","result":"not-run","summary":"Prohibited; no broad validation rerun."}],
  "validationOutput": ["All three packages ACCEPT; no mandatory patches.","Writer strict-validation and scoped-format attestations correspond to unchanged output hashes."],
  "residualRisks": ["Planning acceptance only; runtime, accessibility execution, backend and deployment unverified.","Dynamic domain selection/lookup, exact rejection payloads and inactive-update policy remain separate unresolved decisions."],
  "noStagedFiles": true,
  "diffSummary": "External review artifact only; no source or candidate changes.",
  "reviewFindings": ["No blockers or mandatory revisions."],
  "manualNotes": "Parent alone integrates; preserve unchecked tasks and historical archives. Reviewed hashes recorded above."
}
```
