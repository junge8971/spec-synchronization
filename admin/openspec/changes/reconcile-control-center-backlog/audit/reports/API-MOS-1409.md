# API-MOS-1409 — saved-contract lane

## Result
Both requested skill-export POST operations are **missing from the saved r2 and local OpenAPI documents**, and absent from the generated schema path declarations. This is a documentation/contract finding, not proof that a backend implementation does not exist. No frontend scope, implementation status, deployment acceptance or requirement compliance is inferred.

Exact negative JSON-pointer locators (in each OpenAPI input):
- `/paths/~1api~1control~1api~1skills~1v1~1skills~1export/post`
- `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}~1export/post`

The enclosing path keys themselves are absent. Inspection of skill path names and operation identity metadata did not identify an alternative skill list/card export method/path. A metadata search also matched a dialog export operation; it was excluded without inspecting its contract and is not evidence of skill export.

## Evidence and comparison
- Saved source: `openspec/changes/reconcile-control-center-backlog/audit/sources/api-live/r2/content.json`, `/paths` and `/components/schemas` key inspection. No skill-export path or schema-name candidate exists.
- Local source: `docs/api/contracts/openapi.json`, same pointers and same absence result. This comparison establishes agreement on export absence only; the complete skill path sets are not identical, and unrelated differences were not audited.
- Generated source: `app/shared/api/schema.d.ts`: skill list path at line 563, card path at 581; remaining skill paths at 946, 963, 1365, 1382, 1399 and 1416. File-wide case-insensitive search `skills.*export|export.*skills|Skill.*Export|Export.*Skill` returned no matches; a literal skill path-declaration search returned only those eight entries.
- No export operation means no reachable export request/response DTO graph to traverse. Existing skill CRUD DTOs are not substitutes for an export contract.

## Missing versus unknown
- **Missing in these artifacts:** both target paths/POST operations; generated skill-export operation declarations.
- **Unknown for skill export:** request filters, sorting, selected IDs/whole-selection behavior, field selection, defaults, limits, permission metadata, error statuses/bodies, CSV media type/encoding/escaping/formula safety, filename and response headers (including Content-Disposition), and file delivery shape. There is no operation contract from which to establish any of these; do not label the backend behavior defective or implemented from this absence.
- **Security retained, not changed:** both OpenAPI inputs define `/components/securitySchemes/AdminToken` as header apiKey `X-Admin-Token` and `/components/securitySchemes/AccessToken` as header apiKey `X-Access-Token`; their descriptions say to supply both raw tokens. Neither input has root `/security`. Because the export operations are absent, export-specific security requirements cannot be resolved. No security normalization was altered, and no permissions, anonymous access or credential-bearing mock behavior is inferred.

## Provenance and verification
HEAD verified: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (matches work-item pin).

SHA256 observed:
- Saved r2 `content.json`: `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` — matches `metadata.json#/sha256`.
- Saved r2 `metadata.json`: `444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba`.
- `docs/api/contracts/openapi.json`: `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7`.
- `app/shared/api/schema.d.ts`: `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d`.

Only saved content has an independent expected digest in the assigned inputs; other digests are recorded fingerprints, not asserted matches to an unprovided baseline. Metadata `/retrievedAt` is `2026-10-19T08:11:44.238Z`; `/limitations` explicitly denies deployment validation and historical-discovery proof. This report compares that saved publication, not today's live service.

## Actual boundary and residual risks
Read the work-item common contract/API lane, complete r2 metadata, parsed the two OpenAPI documents locally to inspect skill path keys, operation identity metadata candidates, skill-export schema names and security scheme definitions; searched generated schema as described above. No requirement, OpenSpec ownership, application/mock implementation or test source analysis was performed. No source examples were executed. No network/browser, credentials, tests/build/typegen, nested agents or project edits occurred; only this configured report was written.

Residual risk: an undocumented endpoint or later publication may exist; this lane cannot establish its behavior or deployment. Parent reconciliation must retain API-contract absence separately from requirement ownership and implementation evidence. No product decision is made here.
