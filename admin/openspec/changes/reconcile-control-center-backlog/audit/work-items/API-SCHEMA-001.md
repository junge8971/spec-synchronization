# API-SCHEMA-001 — published component schema delta

Status: review; owner: scout Astra medium; reviewer: R-API-001. Author run: f0fddb25-b7d8-4dd9-b949-80551b299d49. Report: ../reports/API-SCHEMA-001.md; parent has read it; no publication decision yet.
Inputs: repository-relative `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json` and `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/metadata.json`; `docs/api/contracts/openapi-2026-10-15.raw`; `docs/api/contracts/openapi.json`; `docs/api/contracts/README.md`.
Path clarification: initial ENOENT came from resolving sources/ at change root instead of audit/. Supervisor confirmed these exact paths and authorized continuation in the same run; no execution-mode change.
Objective: compare components/schemas only: independently count 382 current vs historical/local, list additions/removals/changes with exact JSON pointers and before/after values. Map changed schema references back to impacted operations for routing, without duplicating full operation-level comparison.
Acceptance: deterministic structural comparison, hashes validated, complete changed-component list with evidence and uncertainty. No claims about backend runtime, product priority or automatic feature completion.
Output: reports/API-SCHEMA-001.md, runtime-bound. Local read-only including permitted comparison commands; no source/spec edits, network/MCP, tests, generation, nested agents. Stop on input/tool blockers; no fallback.
