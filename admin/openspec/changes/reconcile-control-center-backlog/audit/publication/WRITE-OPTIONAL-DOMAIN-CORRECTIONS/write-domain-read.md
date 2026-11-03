# Domain writer (3): completed planning package

Created `/tmp/tsam-corrective-plans-QuJh3q/domain-read/openspec/changes/fix-skill-domain-zone-read-compatibility` using native scaffold and dependency-ordered schema instructions. All four required artifacts exist; all six implementation tasks remain unchecked. Existing capability only: two complete MODIFIED requirement blocks (registry and version-safe editing), preserving original scenarios. Creation requirement remains untouched.

Scope: truthful string-code list/detail/PUT reads; explicit known labels/raw fallback; order/count/linked inactive preservation; fixed selector isolation and no-loss rejection coverage. No inactive-save success promise, dynamic lookup prerequisite, assignment expansion, new backend policy or archive rewrite.

Read the source openspec-propose skill, common contract, complete domain audit and complete review (used only domain findings), current full capability and bounded adapter/type/registry/form-schema/client-test source. Source HEAD matches `bc0d9800f25a90989b9c73c76f91996f8300f1d3`.

## Validation

- Native list/context/new/status/instructions workflow completed; final status 4/4 artifacts complete.
- `openspec validate fix-skill-domain-zone-read-compatibility --strict`: valid, including after formatting.
- Source-installed Prettier invoked only on the five explicit isolated change files, write then check: all matched files use Prettier code style.
- Source staged diff empty. No source-project edits, main-spec/config/archive changes, tests/builds/network/browser or nested agents.

## Freshness and output SHA256

Source `openspec/specs/skill-domain-management/spec.md`, before and after: `b5f3ffc7329e9315b94484b0ce0333711634708779cd3b07fba734fdbbb66f25`; isolated main-spec copy matched before drafting.

All package output hashes (relative to the change root):

| File | SHA256 |
| --- | --- |
| `.openspec.yaml` | `ff4326f8b42dcf8851877f4f3989c7fecb8f97d8154686d7d74b7281b70e6b9b` |
| `proposal.md` | `d3f3e440314acbdf5e0871b0431422b790886e2db77b354de190d928218c970c` |
| `design.md` | `8b62c36d86fb8c4fd86f6d8aa886d6067660349f8c68f796ae4287ac7b8e0d91` |
| `tasks.md` | `5d00d6e69c1d754139b1e12bec759dede78c034c643f129f8a4bc12138f93404` |
| `specs/skill-domain-management/spec.md` | `9cd7ec1d67bbd106d851f5cfd1bce5b4c6baf5af64c319622e32b181a8dd9f95` |

## Residual risks

Directory contract, dynamic selector approval, exact business rejection payloads and unchanged-inactive update semantics remain separately unresolved. Fixtures are not backend/deployment evidence. Wider response types must not accidentally widen assignment types; the design and unchecked tasks explicitly require that boundary. Parent freshness review and package review remain necessary before copying; no apply/sync/archive performed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Complete native-scaffold domain-only planning package; strict validation and explicit-path formatting passed; hashes and retained policy risks recorded."}],
  "changedFiles": ["openspec/changes/fix-skill-domain-zone-read-compatibility/.openspec.yaml", "openspec/changes/fix-skill-domain-zone-read-compatibility/proposal.md", "openspec/changes/fix-skill-domain-zone-read-compatibility/design.md", "openspec/changes/fix-skill-domain-zone-read-compatibility/tasks.md", "openspec/changes/fix-skill-domain-zone-read-compatibility/specs/skill-domain-management/spec.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"openspec validate fix-skill-domain-zone-read-compatibility --strict","result":"passed","summary":"Change valid after formatting."},{"command":"Prettier --write and --check on five explicit isolated artifact paths","result":"passed","summary":"All matched files use Prettier code style."},{"command":"openspec status --change fix-skill-domain-zone-read-compatibility","result":"passed","summary":"4/4 planning artifacts complete; implementation tasks unchecked."},{"command":"tests/build/browser/network","result":"not-run","summary":"Prohibited by assignment."}],
  "validationOutput": ["Strict valid; formatting clean; source spec hash unchanged."],
  "residualRisks": ["Dynamic selection/lookup and inactive-update policy remain separate owner decisions.","No runtime or real backend validation performed."],
  "noStagedFiles": true,
  "diffSummary": "Five new isolated planning files; no original-project changes.",
  "reviewFindings": ["No known planning blockers; package review pending."],
  "manualNotes": "Source main-spec before/after and all package output hashes recorded above. Planning only; parent controls integration and future implementation authorization."
}
```
