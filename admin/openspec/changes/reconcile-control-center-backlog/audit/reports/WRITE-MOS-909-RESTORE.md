# WRITE-MOS-909-RESTORE — corrective planning package

## Result and boundary

Created `openspec/changes/mos-909-restore-approved-lifecycle-actions` using native spec-driven scaffold. All four schema artifacts and their transitive dependencies are present; strict validation passed. **Fresh independent review pending. No implementation or task closure.** All six future tasks remain unchecked.

D-020 explicitly authorizes preserving draft → checking, sandbox → review and whitelist → prod and planning removal of the other four generic triggers. Read D-018–D-020, the corrected IMPL-MOS-909 report and its independent review, and SCENARIO-MOS-909/report review. Inspected actual feature map/hook/UI/confirmation/handler, shared client/mutation/error/query/status constants, mounted widget and full lifecycle component tests, review hook and separate review design, and full lifecycle/review/toggle specifications. Existing assertions were read, not executed.

The plan limits future code changes to the feature action constant and mounted lifecycle component test. It preserves separate review, bulk and dedicated toggle ownership; broader shared enum/status API; neutral scale and recognized disabled; polling, permissions, validation, accessibility, snapshots, pending lock, uncertain outcomes/GET recovery and server-derived caches. Corrected IMPL909-07 is respected: published 409 SKILL_CHECKS_BLOCKED already enters GET recovery; no false missing-reread fix is planned.

No application/test edits, main-spec/archive edits, auth/models/API/transport/mock policy changes, generated DTO changes, checks UI, unrelated copy/debt repair, network/browser execution, nested delegation, commit/stash/reset or staging occurred. Native CLI completion is planning completeness only. External publication freshness and backend deployment were not rechecked.

## Artifacts and before/after SHA-256

Target directory was absent at preflight; every artifact baseline is **absent**, not an empty-file digest. Metadata is native scaffold output. The report itself is the sole additional authorized output; its self-hash is intentionally not embedded.

| Path | Before | After SHA-256 |
|---|---|---|
| `openspec/changes/mos-909-restore-approved-lifecycle-actions/.openspec.yaml` | absent | `b552ab6519df8f66b705724100f565c5cd842bc9389aeaa177da9cec3d02a685` |
| `openspec/changes/mos-909-restore-approved-lifecycle-actions/design.md` | absent | `ce5c459eee2c491e70c773e24f5ef5530734faf26730bf0c6ca2e2413224e49b` |
| `openspec/changes/mos-909-restore-approved-lifecycle-actions/proposal.md` | absent | `03df2244a11422a244b860bf0d29d424174603b4f0669c012e14f12d6043f30d` |
| `openspec/changes/mos-909-restore-approved-lifecycle-actions/specs/skill-lifecycle/spec.md` | absent | `d75265e70aef97dce00dd6b044bcf13011f508d134830b1e927f0ac526a95ed0` |
| `openspec/changes/mos-909-restore-approved-lifecycle-actions/tasks.md` | absent | `d64b2c25d0aef7d7a9b7f48717a4bf2ba5a1a49dc08eb4d1ae3f1a9f0b6f6172` |

## Source freshness

The first three anchors were computed before scaffold and rechecked after all artifacts, matching the assignment exactly. Remaining hashes match the corrected IMPL report. No material source change was found; source inspection remained read-only.

| Source | SHA-256 |
|---|---|
| `app/features/skill-lifecycle/constants/skill-lifecycle.constants.ts` | `d6de7f6bf778308a900e8f99cbe983380019202c18de44803180375313fe4e3e` |
| `app/widgets/skill-details/ui/skill-lifecycle.test.tsx` | `32f12cc726f767880c4bb4e34d640c580abe942a5570e295ef4b31e6158a7645` |
| `openspec/specs/skill-lifecycle/spec.md` | `0d568a12a535816dae50fe6831d8a8b1232d360a5ea0649a5526b9e43bfbf30c` |
| `app/features/skill-lifecycle/model/use-skill-lifecycle.ts` | `8c5a90a1d39522a4d30138677c19da82b1d70577419bc0cf688f5aa8c509ae0d` |
| `app/features/skill-lifecycle/handlers/skill-lifecycle-handlers.ts` | `acc50ac92ab552659cb8710aa37a46098145607240791b437c357bb4cd2e71e0` |
| `app/features/skill-lifecycle/ui/skill-lifecycle.tsx` | `fe99d1cdc3960e1d5246e147dff47bb7a1129fac74351a7797cd32040c1933e7` |
| `app/entities/skill/api/skill-details-client.ts` | `de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6` |
| `app/entities/skill/model/use-change-skill-status-mutation.ts` | `3a08a27c6a404b824d2a077ba9ef4af5040eb940c17b86f03c991147df0ae10b` |

## Commands and results

All commands below passed. Read-only `cat`, `sed`, `rg`, file reads and Python hashlib inspection supplemented the native workflow; large combined outputs were continued where needed.

- `openspec context --json` — Resolved nearest local root; no store selected.
- `test ! -e openspec/changes/mos-909-restore-approved-lifecycle-actions` — Passed before native scaffold: target absent.
- `openspec new change mos-909-restore-approved-lifecycle-actions` — Created native spec-driven scaffold and .openspec.yaml.
- `openspec list --specs` — Confirmed existing capability inventory.
- `openspec show "skill-lifecycle" --type spec --json --no-scenarios` — Read requirements overview.
- `openspec show "skill-lifecycle" --type spec` — Read complete capability and scenarios.
- `openspec show "skill-review" --type spec --json --no-scenarios` — Read requirements overview.
- `openspec show "skill-review" --type spec` — Read complete capability and scenarios.
- `openspec show "skill-global-toggle" --type spec --json --no-scenarios` — Read requirements overview.
- `openspec show "skill-global-toggle" --type spec` — Read complete capability and scenarios.
- `openspec instructions proposal --change mos-909-restore-approved-lifecycle-actions --json` — Read native instructions/rules/template and reread completed dependencies before writing.
- `openspec instructions specs --change mos-909-restore-approved-lifecycle-actions --json` — Read native instructions/rules/template and reread completed dependencies before writing.
- `openspec instructions design --change mos-909-restore-approved-lifecycle-actions --json` — Read native instructions/rules/template and reread completed dependencies before writing.
- `openspec instructions tasks --change mos-909-restore-approved-lifecycle-actions --json` — Read native instructions/rules/template and reread completed dependencies before writing.
- `openspec status --change mos-909-restore-approved-lifecycle-actions --json` — Run after scaffold and each artifact; final proposal/specs/design/tasks done; transitive dependency set complete.
- `openspec status --change mos-909-restore-approved-lifecycle-actions` — 4/4 planning artifacts complete; not implementation completion.
- `openspec validate mos-909-restore-approved-lifecycle-actions --strict` — Change 'mos-909-restore-approved-lifecycle-actions' is valid
- `git rev-parse HEAD` — bc0d9800f25a90989b9c73c76f91996f8300f1d3
- `git diff --check` — Passed, no tracked diff errors; ignored planning files reviewed directly.
- `git status --short` — Empty before and after; ignored OpenSpec files are not represented by this output.
- `git diff --cached --name-only` — Empty: no staged files.
- `sha256sum openspec/changes/mos-909-restore-approved-lifecycle-actions/.openspec.yaml openspec/changes/mos-909-restore-approved-lifecycle-actions/design.md openspec/changes/mos-909-restore-approved-lifecycle-actions/proposal.md openspec/changes/mos-909-restore-approved-lifecycle-actions/specs/skill-lifecycle/spec.md openspec/changes/mos-909-restore-approved-lifecycle-actions/tasks.md app/features/skill-lifecycle/constants/skill-lifecycle.constants.ts app/widgets/skill-details/ui/skill-lifecycle.test.tsx openspec/specs/skill-lifecycle/spec.md app/features/skill-lifecycle/model/use-skill-lifecycle.ts app/features/skill-lifecycle/handlers/skill-lifecycle-handlers.ts app/features/skill-lifecycle/ui/skill-lifecycle.tsx app/entities/skill/api/skill-details-client.ts app/entities/skill/model/use-change-skill-status-mutation.ts` — Artifact and source digests listed below; three freshness anchors match before/after and assignment.

Not run: `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check` (planning-only assignment; prescribed for later implementation). `yarn api:check` and `yarn build` unnecessary absent API-type/build changes. No E2E/browser tests created, changed or run.

## Remaining risks and next step

No drafting/infrastructure blocker. Independent artifact review is required before publication acceptance. Implementation remains unperformed and needs a later explicit apply request. Known obsolete disabled/eight-status and API-results wording outside the targeted requirement remains separate documentary debt; this plan must not reintroduce disabled rejection. No backend admissibility or runtime integration evidence is claimed. Git status does not inventory ignored OpenSpec; artifact paths/content and hashes above are the review evidence.

```acceptance-report
{
  "criteriaSatisfied": [
    {
      "id": "criterion-1",
      "status": "satisfied",
      "evidence": "Only native scaffold plus proposal/design/existing-capability delta/unchecked tasks and this bound report written; D-020 three-command scope preserved."
    },
    {
      "id": "criterion-2",
      "status": "satisfied",
      "evidence": "Native command results, artifact/source hashes, freshness checks and independent-review boundary provided."
    }
  ],
  "changedFiles": [
    "openspec/changes/mos-909-restore-approved-lifecycle-actions/.openspec.yaml",
    "openspec/changes/mos-909-restore-approved-lifecycle-actions/design.md",
    "openspec/changes/mos-909-restore-approved-lifecycle-actions/proposal.md",
    "openspec/changes/mos-909-restore-approved-lifecycle-actions/specs/skill-lifecycle/spec.md",
    "openspec/changes/mos-909-restore-approved-lifecycle-actions/tasks.md",
    "openspec/changes/reconcile-control-center-backlog/audit/reports/WRITE-MOS-909-RESTORE.md"
  ],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {
      "command": "openspec context --json",
      "result": "passed",
      "summary": "Resolved nearest local root; no store selected."
    },
    {
      "command": "test ! -e openspec/changes/mos-909-restore-approved-lifecycle-actions",
      "result": "passed",
      "summary": "Passed before native scaffold: target absent."
    },
    {
      "command": "openspec new change mos-909-restore-approved-lifecycle-actions",
      "result": "passed",
      "summary": "Created native spec-driven scaffold and .openspec.yaml."
    },
    {
      "command": "openspec list --specs",
      "result": "passed",
      "summary": "Confirmed existing capability inventory."
    },
    {
      "command": "openspec show \"skill-lifecycle\" --type spec --json --no-scenarios",
      "result": "passed",
      "summary": "Read requirements overview."
    },
    {
      "command": "openspec show \"skill-lifecycle\" --type spec",
      "result": "passed",
      "summary": "Read complete capability and scenarios."
    },
    {
      "command": "openspec show \"skill-review\" --type spec --json --no-scenarios",
      "result": "passed",
      "summary": "Read requirements overview."
    },
    {
      "command": "openspec show \"skill-review\" --type spec",
      "result": "passed",
      "summary": "Read complete capability and scenarios."
    },
    {
      "command": "openspec show \"skill-global-toggle\" --type spec --json --no-scenarios",
      "result": "passed",
      "summary": "Read requirements overview."
    },
    {
      "command": "openspec show \"skill-global-toggle\" --type spec",
      "result": "passed",
      "summary": "Read complete capability and scenarios."
    },
    {
      "command": "openspec instructions proposal --change mos-909-restore-approved-lifecycle-actions --json",
      "result": "passed",
      "summary": "Read native instructions/rules/template and reread completed dependencies before writing."
    },
    {
      "command": "openspec instructions specs --change mos-909-restore-approved-lifecycle-actions --json",
      "result": "passed",
      "summary": "Read native instructions/rules/template and reread completed dependencies before writing."
    },
    {
      "command": "openspec instructions design --change mos-909-restore-approved-lifecycle-actions --json",
      "result": "passed",
      "summary": "Read native instructions/rules/template and reread completed dependencies before writing."
    },
    {
      "command": "openspec instructions tasks --change mos-909-restore-approved-lifecycle-actions --json",
      "result": "passed",
      "summary": "Read native instructions/rules/template and reread completed dependencies before writing."
    },
    {
      "command": "openspec status --change mos-909-restore-approved-lifecycle-actions --json",
      "result": "passed",
      "summary": "Run after scaffold and each artifact; final proposal/specs/design/tasks done; transitive dependency set complete."
    },
    {
      "command": "openspec status --change mos-909-restore-approved-lifecycle-actions",
      "result": "passed",
      "summary": "4/4 planning artifacts complete; not implementation completion."
    },
    {
      "command": "openspec validate mos-909-restore-approved-lifecycle-actions --strict",
      "result": "passed",
      "summary": "Change 'mos-909-restore-approved-lifecycle-actions' is valid"
    },
    {
      "command": "git rev-parse HEAD",
      "result": "passed",
      "summary": "bc0d9800f25a90989b9c73c76f91996f8300f1d3"
    },
    {
      "command": "git diff --check",
      "result": "passed",
      "summary": "Passed, no tracked diff errors; ignored planning files reviewed directly."
    },
    {
      "command": "git status --short",
      "result": "passed",
      "summary": "Empty before and after; ignored OpenSpec files are not represented by this output."
    },
    {
      "command": "git diff --cached --name-only",
      "result": "passed",
      "summary": "Empty: no staged files."
    },
    {
      "command": "sha256sum openspec/changes/mos-909-restore-approved-lifecycle-actions/.openspec.yaml openspec/changes/mos-909-restore-approved-lifecycle-actions/design.md openspec/changes/mos-909-restore-approved-lifecycle-actions/proposal.md openspec/changes/mos-909-restore-approved-lifecycle-actions/specs/skill-lifecycle/spec.md openspec/changes/mos-909-restore-approved-lifecycle-actions/tasks.md app/features/skill-lifecycle/constants/skill-lifecycle.constants.ts app/widgets/skill-details/ui/skill-lifecycle.test.tsx openspec/specs/skill-lifecycle/spec.md app/features/skill-lifecycle/model/use-skill-lifecycle.ts app/features/skill-lifecycle/handlers/skill-lifecycle-handlers.ts app/features/skill-lifecycle/ui/skill-lifecycle.tsx app/entities/skill/api/skill-details-client.ts app/entities/skill/model/use-change-skill-status-mutation.ts",
      "result": "passed",
      "summary": "Artifact and source digests listed below; three freshness anchors match before/after and assignment."
    }
  ],
  "validationOutput": [
    "Change 'mos-909-restore-approved-lifecycle-actions' is valid",
    "4/4 planning artifacts complete; six implementation tasks unchecked.",
    "No staged files; source freshness anchors unchanged."
  ],
  "residualRisks": [
    "Fresh independent artifact review pending.",
    "No implementation or application-test execution.",
    "Unrelated lifecycle documentary debt remains deferred.",
    "No backend/runtime integration attestation."
  ],
  "noStagedFiles": true,
  "diffSummary": "Five new native/planning artifacts and bound report only; no product files edited.",
  "reviewFindings": [
    "Self-review found no scope blocker; independent reviewer acceptance not claimed."
  ],
  "manualNotes": "Stop after planning. Parent owns fresh review and any subsequent explicit apply authorization."
}
```
