# MOS-959 author completion — planning only

## Current disposition and authority

Complete native planning packet; stop before apply/runtime implementation. This report supersedes the earlier pre-scaffold stop report (SHA-256 `894df0d7270f84ad4d7dc157564ff11a07a28eeef41acdb9449167f4fa62cb13`). That initial stop was correct under then-current authority. Parent subsequently reported explicit user «Подтверждаю» to these exact policies:

1. Color presets PLUS arbitrary #RRGGBB.
2. Local preview using demonstration data, no requests and no execution of card actions, separate fallback preview.
3. Explicit configuration save button; publication unavailable while either configuration or skills has unsaved changes; successful save followed by fresh GET; failed readback retries ONLY GET, never the successful write.

These approvals and D-096 are recorded in proposal/design, without editing shared decisions. The earlier combined save/publish recommendation, navigation prompts and persona-editing proposals were NOT approved and are not introduced. Supervisor additionally directed retention of existing clean enabled-skills PUT during confirmed Publish: dirty blocking does not authorize removing the established preparation write. Readback recovery does not replay that write or implicitly publish; a new explicit publication retains confirmation/preparation.

No remaining material product question blocks this packet. Exact demonstrative sample text is a recorded minor presentation detail, not live identity/time policy. Parser/Unicode/duplicate-normalization edges remain backend-authoritative without new client algorithms. Fresh independent review is still required; planning completion is not implementation acceptance or task closure.

## Artifacts and scope

- `openspec/changes/mos-959-surface-configurator/.openspec.yaml`
- `openspec/changes/mos-959-surface-configurator/design.md`
- `openspec/changes/mos-959-surface-configurator/proposal.md`
- `openspec/changes/mos-959-surface-configurator/specs/surface-configurator/spec.md`
- `openspec/changes/mos-959-surface-configurator/specs/surface-lifecycle-publication/spec.md`
- `openspec/changes/mos-959-surface-configurator/specs/surface-overview-connection/spec.md`
- `openspec/changes/mos-959-surface-configurator/tasks.md`

Proposal, design, three delta specs and 13 unchecked testable tasks are complete, plus native metadata. New capability surface-configurator; modified lifecycle publish/deferral and overview checklist requirements are complete replacements, not partial fragments. All 14 original scenario names across the three modified requirements are retained; four scenarios added. The unavailable-editor scenario remains a conditional protection, not a continuing feature deferral.

Only the new change directory was written inside the repository. No code/contracts/config/main specs/archive/audit registers changed; no commit, staging, tests, browser, network or agents. HEAD remains bc0d9800f25a90989b9c73c76f91996f8300f1d3. OpenSpec files are ignored by Git, so empty git diff is supplemented by explicit output hashes below. Original inspected input digest manifest was verified unchanged after authoring.

## Evidence used and reuse

Primary saved Jira MOS-959/MOS-1237, UI Wiki 245673187 r1, linked contract Wiki 241082009 r2 and published API r2 were independently inspected before the first stop. Existing accepted reviews/extraction were reused, not reinventoried. Exact pointers/headings and source hashes are in design.md and the input manifest. API r2 capture is 2026-10-19T08:11:44.238Z; no external freshness or deployment claim. Attachment bodies remain unavailable.

Selected API comparison: POST surface, GET detail, PUT configuration and PUT enabled-skills operation objects/descriptions differ from local docs/api/contracts/openapi.json. The plan does not wholesale replace operations/security. The seven required configuration fields, shape/font enums and string fallback agree; local schemas lack the published greeting/item/card/action length and list-count constraints. Narrow later alignment is tasked, no contract files edited now. Published wire authority resolves older Wiki vocabulary/null/default/combined-payload disagreements.

Inspected reuse: surface-details-content.tsx placeholder/default tab/presentation controls; use-surface-details-operations.ts lock/owner/skill orchestration; surface entity client/configuration mutation; existing component/transport tests; mocks/surfaces.mjs and surfaces.test.mjs. Mock configuration currently synthesizes configured/timestamp; targeted later alignment is documented, not treated as deployed evidence. Auth/mock approved proposal/design/specs were read from their 2026-10-09 archive locations; current permission model and credential-free local mock isolation are retained, not expanded.

## Commands and results

Exact workflow/verification commands (repeated status checks collapsed):

- `openspec context --json` — passed, expected root (before first stop).
- `openspec new change mos-959-surface-configurator` — passed after explicit approval.
- `openspec status --change mos-959-surface-configurator --json` — passed after each artifact stage; final all four required artifact categories done.
- `openspec instructions proposal --change mos-959-surface-configurator --json` — passed before proposal.
- `openspec instructions design --change mos-959-surface-configurator --json` — passed before design.
- `openspec instructions specs --change mos-959-surface-configurator --json` — passed before specs.
- `openspec instructions tasks --change mos-959-surface-configurator --json` — passed before tasks; dependencies re-read from disk.
- `openspec list --specs` — passed, native required capability inventory only.
- `openspec show <id> --type spec --json --no-scenarios` and `openspec show <id> --type spec` — passed for surface-lifecycle-publication, surface-skill-selection, surface-overview-connection, surface-registration.
- `yarn exec prettier --write openspec/changes/mos-959-surface-configurator` — passed, target only.
- `openspec validate mos-959-surface-configurator --strict` — initially failed because the old unavailable-editor scenario name was replaced. Corrected by retaining its conditional protective scenario in the full modified requirement. Final rerun passed: Change 'mos-959-surface-configurator' is valid.
- `yarn exec prettier --check openspec/changes/mos-959-surface-configurator` — passed, all matched files use Prettier style.
- `openspec status --change mos-959-surface-configurator` — passed, 4/4 complete.
- `git rev-parse HEAD`, `git status --short`, `git diff --stat`, `git diff --cached --name-only` — passed; expected HEAD, no tracked/index changes.
- Read-only Python original-scenario inclusion and checkbox assertions — passed: original scenarios 8+3+3 retained, additions 2+1+1, 13 unchecked tasks. SHA-256 input unchanged assertions passed.
- Bounded cat/sed/rg/find and standard-library JSON/inert HTML inspection — completed; full exact invocations remain in run transcript. Exploratory `ls contracts` and `ls api` failed (nonexistent paths); correct contract found via generator. Reads at unarchived auth/demo paths failed; corrected to their actual archive paths. No findings rely on those failed path guesses.
- Runtime tests/typecheck/lint/build/API generation/global formatting — NOT RUN; planning-only scope and explicit prohibitions. Later quality gates are unchecked tasks, not claimed results.

## Input hashes

```text
89b4c1fee49fc94a59f0801376311544500fd3ff94da8c1b18578a5cf5172c6b  .agents/skills/openspec-propose/SKILL.md
07a48798af3c9a8fa9e7b857c0747de7ddc9603d3f6fe1530dc6cdd5f58f2201  openspec/config.yaml
675265a0ba98b45f1d659f6048fe97f2e590a0597d7eda304cdcfe9854ebdd91  openspec/specs/surface-lifecycle-publication/spec.md
c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7  docs/api/contracts/openapi.json
d2730d5da1651bc590c49130f49fd8dc9afc015044841a9a5a5b78b4cdcb162b  openspec/changes/reconcile-control-center-backlog/audit/work-items/WRITE-MOS-959.md
077801c5e785d938c644b1abffe02fc0da3c81f12804815da677589e0bb013dd  openspec/changes/reconcile-control-center-backlog/audit/decisions.md
3b815364676a07193aab0d9a529408983afd3e4579c51f698a544efe1fd9e47a  openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-959.md
ef2e754d63a4cccd7f807b60009c14381d2099f9f608db87ed75c63e82a35713  openspec/changes/reconcile-control-center-backlog/audit/reviews/RECON-MOS-959-CONTRACT.md
efb8bc1da327e803938798b9bb2e2063ef28b0135b9fae7404614f66fa0a3e64  openspec/changes/reconcile-control-center-backlog/audit/reports/REQ-MOS-959.md
ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993  openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r2/content.json
444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba  openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r2/metadata.json
b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed  openspec/changes/reconcile-control-center-backlog/audit/sources/jira-api-delta-scenarios/r1/content.json
d539752b3e0f424d0a251426a490319b07d03f4ff8dfdcf3074a62ee53d34eaa  openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-245673187/r1/content.json
13ff11a35b27fe17db263039ba4c9a2b5c335728bad7615d06aed3d94ab2d86b  openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241082009/r2/content.json
d236139b0cd425670f6f41eadcf2d2bf487d43601bc0ce55a638a8cdd19658a2  app/widgets/surface-details/ui/surface-details/surface-details-content.tsx
bd29277f023382cd8559ac486e4175aa96d5a6c3cf6bc32573c934791f4ae3c2  app/widgets/surface-details/ui/surface-details/model/use-surface-details-operations.ts
65b8274f149b8a076e44d5281367832a4b32c0ce59d5249968937ef2fa36773e  app/entities/surface/model/use-update-surface-configuration-mutation.ts
de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05  app/entities/surface/api/surface-registry-client.ts
a225bd153667722264514c9cc77e2cf0ea34e84bc26999951bfeed0b67cb7d8f  mocks/surfaces.mjs
f593d5787af815c94f2e1711506effdfb0c476503923b4379425e25cff1d114d  mocks/surfaces.test.mjs
5ff98d3c6e74786075c2060fb207171f56be28a70a9802e13d0fb6e50b9def3c  app/widgets/surface-details/ui/surface-details.test.tsx
```

## Additional input hashes

```text
51f9dc1a1d7b92ccdb059b7fda0117bf6c898378fa9a9fe185c7e2045044d193  openspec/specs/surface-overview-connection/spec.md
e27eb8b354e4370da3519b5387cff5369a2f083e6c3be05f82d8631746c19ee0  openspec/specs/surface-skill-selection/spec.md
31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5  openspec/specs/surface-registration/spec.md
0caae10e8eac783119004fb538898be9e7ce60480e86fe2492eb2bd2ac670d58  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/proposal.md
abad61fde268e29440a61ca3781c364ea925f5ff8dcc43b84b34eb55c7631357  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/design.md
2b45da1ca4206b0e12d5d25cda068050196b40f676464d83e1b5ad0e5d600536  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/specs/control-center-api-integration/spec.md
49e3ee8bd60b702d5a6e4e86706a02d7fa24d607f0bed35a273d9f706dd5e241  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/specs/control-center-http/spec.md
65881139d1fcbbfe295513b613263a4f40942ceae63f7bbc3e04b972b5861533  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/specs/control-center-mock-server/spec.md
c6461f73efbbedea7a0f19907e1d9454a707775db208578d600b33eba997cc9d  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/specs/control-center-permissions/spec.md
80a31db0c4d23540ab42856e1ae7ddec4295effc7f01e19d2a1669c0f33245ca  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/specs/control-center-shell/spec.md
c2f9a3e32789e8782ab6c81aabe65a911493883aaa1449728c5957c4e7040e37  openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/specs/mpmm-session/spec.md
6a752ccfa3a8ec9676c7e9657fd038cfc9fee792125cb55ff92a737040e701b6  openspec/changes/archive/2026-10-09-add-local-session-demo/proposal.md
0a9a23ad13bd87d5203c266a19fb16620ca0f24d0bb0144e19f13e01bb1f343c  openspec/changes/archive/2026-10-09-add-local-session-demo/design.md
faea88ab06472789297262e9f646ac5faea43d1292948d5ccf67bc4365f45dfb  openspec/changes/archive/2026-10-09-add-local-session-demo/specs/control-center-mock-server/spec.md
eaa7a9abf2bea3a29b9480fa3c0d7efdf8fe3685eec680679e02fb5bc7fc1fa1  openspec/changes/archive/2026-10-09-add-local-session-demo/specs/control-center-shell/spec.md
e022b6a8a24c5ca29e2c3cdb79c3db8abe3a030dc13243a88dbd5cb75384f010  openspec/changes/archive/2026-10-09-add-local-session-demo/specs/local-session-demo/spec.md
```

## Output SHA-256 manifest

```text
30cfdee007123f96b2ab27ca107e406084602caf445d6b7cd2130ab329668ed3  openspec/changes/mos-959-surface-configurator/.openspec.yaml
6eb264befb7c972f06c521b64d58843998bfdd04212516dd0aaadf189df2c4f6  openspec/changes/mos-959-surface-configurator/design.md
2d00f1217087717787e5cb3c3dedb6af12ed6b4c5c7fa3e7fc6069d4b179b08c  openspec/changes/mos-959-surface-configurator/proposal.md
321ec9622d76a71cf85b34cf8b2fc36281a396f9e9599667fe4b48daa224d716  openspec/changes/mos-959-surface-configurator/specs/surface-configurator/spec.md
c1a048bafd90b3435295f8afb313e88b7ba3ed4ae7f772ad1dcd368b40131f93  openspec/changes/mos-959-surface-configurator/specs/surface-lifecycle-publication/spec.md
96c9c8f8b26b78eca885cb30909debf118f01383b7898c1f2cc76471d35a7d45  openspec/changes/mos-959-surface-configurator/specs/surface-overview-connection/spec.md
cd6608497a34e7d6cfa9c1aa64dfafdd6b2993e821b3e3c87c81f263e9858c67  openspec/changes/mos-959-surface-configurator/tasks.md
```

The report digest is returned separately to avoid a self-referential hash.

```acceptance-report
{
  "criteriaSatisfied": [
    {
      "id": "criterion-1",
      "status": "satisfied",
      "evidence": "Only approved new planning directory authored; all three explicit policies and preserved clean-skills preparation reflected without implementation."
    },
    {
      "id": "criterion-2",
      "status": "satisfied",
      "evidence": "Full artifact/input hashes, source locators, exact principal commands, retained-scenario checks and validation history supplied."
    }
  ],
  "changedFiles": [
    "openspec/changes/mos-959-surface-configurator/.openspec.yaml",
    "openspec/changes/mos-959-surface-configurator/design.md",
    "openspec/changes/mos-959-surface-configurator/proposal.md",
    "openspec/changes/mos-959-surface-configurator/specs/surface-configurator/spec.md",
    "openspec/changes/mos-959-surface-configurator/specs/surface-lifecycle-publication/spec.md",
    "openspec/changes/mos-959-surface-configurator/specs/surface-overview-connection/spec.md",
    "openspec/changes/mos-959-surface-configurator/tasks.md",
    "/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/1b0c3a28-138d-4a16-ab7e-7a845f7f0950/mos959/author.md"
  ],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {
      "command": "openspec validate mos-959-surface-configurator --strict",
      "result": "passed",
      "summary": "Final rerun valid; initial omitted-scenario failure corrected and disclosed."
    },
    {
      "command": "yarn exec prettier --check openspec/changes/mos-959-surface-configurator",
      "result": "passed",
      "summary": "Target formatting passes."
    },
    {
      "command": "git diff --cached --name-only",
      "result": "passed",
      "summary": "Empty."
    }
  ],
  "validationOutput": [
    "All four planning artifact categories done.",
    "13 unchecked tasks; all original modified-requirement scenario names retained."
  ],
  "residualRisks": [
    "Fresh independent reviewer acceptance remains required.",
    "Saved source evidence is not external freshness or deployment verification.",
    "No runtime tests executed; implementation requires separate apply authorization."
  ],
  "noStagedFiles": true,
  "diffSummary": "Native metadata, proposal/design/tasks, one new capability and two complete modified capability deltas; external report updated.",
  "reviewFindings": [
    "No known remaining material product blocker; reviewer must use follow-up approval, not obsolete initial stop recommendations."
  ]
}
```
