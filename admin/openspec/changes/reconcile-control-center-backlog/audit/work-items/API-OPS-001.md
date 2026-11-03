# API-OPS-001 — published operation delta

Status: review; owner: scout Astra medium; reviewer: R-API-001. Author run: 257cd13f-9314-486e-bd2c-2148f0a14dec. Report: ../reports/API-OPS-001.md; parent has read it; no publication decision yet.
Inputs (all repository-relative): `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/content.json`; `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r1/metadata.json`; `docs/api/contracts/openapi-2026-10-15.raw`; `docs/api/contracts/openapi.json`; `docs/api/contracts/README.md`; `docs/api/contracts/delta-2026-10-15.md`.
Objective: compare only top-level metadata, paths/methods/operationIds, parameters/request/response references, and security across current live, historical raw and local aggregate. Do not deeply analyze component schema internals (API-SCHEMA-001 owns those).
Acceptance: added/removed/changed operation IDs and exact JSON pointers with before/after evidence; distinguish intentional local normalization from upstream drift; count operations independently. No production availability claims.
Output: reports/API-OPS-001.md, runtime-bound. No project edits except configured report; no network/MCP/tests/generation/nested agents.
Stop: invalid/unavailable input or unclear authority; return exact limitations. Dependencies: API snapshot captured and hash matched. Decisions/publication remain with supervisor and independent review.
