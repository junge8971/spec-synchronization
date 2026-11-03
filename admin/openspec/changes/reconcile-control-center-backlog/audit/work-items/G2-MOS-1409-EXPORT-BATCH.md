# G2-MOS-1409 — four independent source lanes

Status queued; Astra low authorized. Target is one previously unexamined member MOS-1409, not the whole skill module. Root `/home/user/my/work/codesrc/projects/CAM/tsam-admin-front`, HEAD `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Parent sole project writer; outputs only through distinct configured artifacts. One independent package review/reconciliation after four reports. All source types stay separate; backend-task identity does not automatically create frontend scope.

Common constraints: no project edits, browser/network, tests/build/typegen, credentials, nested agents or external mutations. Verify HEAD and input SHA256. Do not execute source examples. Stop on infrastructure error or genuine product decision; return explicit uncertainty when evidence absent. Report concise exact locators, actual read boundary and no implementation/deployment acceptance. Return NONEMPTY final pointing to configured report.

## REQ-MOS-1409

Owner requirement analyst; output req-mos-1409.md. Read only MOS-1409 item in saved `sources/jira-details-MOS-774/r1/content.json`, metadata and membership in reports/JIRA-MOS-774 / reports/G2-JIRA-MEMBER-JOINS; parse selected item without re-extracting neighboring tasks. Source content SHA256 e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208. Extract atomic requirements/locators for list/card POST, whole selection, fields/defaults, CSV safety/format, permission/filter/error/limits. Separate backend delivery from any explicit frontend obligation; do not infer UI entrypoints from task title. No code/API/spec analysis. Output requirements and open questions, not a new change.

## API-MOS-1409

Owner API analyst; output api-mos-1409.md. Inspect saved `sources/api-live/r2/{content.json,metadata.json}`, local docs/api/contracts/openapi.json and generated schema only for skill list/card export operations and transitive DTOs. Resolve actual method/path and schema pointers, including errors/header/file contract, filters/fields/defaults/limits/permission metadata. Compare saved r2 versus local, not today's live API. Distinguish unknown prose details from missing operation; retain approved security normalization. Named targets POST /api/control/api/skills/v1/skills/export and /api/control/api/skills/v1/skills/{skill_id}/export are inspection targets, not assumed present. No unrelated export/report/Feedback audit or code analysis.

## SPEC-MOS-1409

Owner OpenSpec analyst; output spec-mos-1409.md. Read main skill-catalog-experience, skill-card-editing and control-center-api-integration specs; bounded search for skill export coverage among active changes and relevant archived `2026-10-15-update-control-center-api-contracts` and `2026-10-01-skills-prototype-alignment` artifacts. Read complete relevant owner artifacts before judging. Locate explicit export UI ownership or recorded exclusions; no capability-name analogy or auto-new-change. Record exact coverage/gaps and recommend keep/update/new/question only with evidence. Do not implement or re-audit unrelated capabilities.

## IMPL-MOS-1409

Owner implementation analyst; output impl-mos-1409.md. Anchors `app/pages/skills`, `app/widgets/skill-details`, `app/entities/skill`, relevant skill-list features, shared download helper and skill mock handlers/tests. Follow only mounted list/card export entrypoints and connected client/query/file download behavior, or establish bounded absence. Distinguish generated operations and mock handlers from UI delivery; inspect written tests without running. Verify field/filter/sort/whole-selection and safety only where connected implementation exists; do not treat neighboring dialog export as skill export. No requirement/API census; use code evidence, with schema lookup only if necessary to identify invoked operation.

## Acceptance and review

Each source lane reports its own evidence, not assumed results of others. Parent compares four lanes and assigns one independent review, including any exact proposed patch in the same package when possible. Missing frontend ownership is a question, not permission to invent it. Preserve backend authorization and local credential-free mock distinction. Feature tasks and global audit gates stay open until full criteria, not report counts, are met.
