# R-DELTA-TEAMS-API-CONTRACT

## Review

**Disposition: ACCEPT.**  
**Merge verdict: OK** for the bounded documentary report.

No issues found.

- **Correct:** TEAMAPI-01–08 accurately distinguish saved wire shapes, explanatory prose, approved policy and unresolved runtime/owner questions.
- **Fixed:** None; review was read-only.
- **Mandatory fixes:** None.
- **Global progress: 6/28 unchanged.**

## Actual coverage and attribution

Aliases:

- **A** = `openspec/changes/reconcile-control-center-backlog/audit`
- **H** = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions`
- **S** = `A/sources/wiki-241080659-readable/r1/content.txt`
- **O** = `A/sources/api-live/r2/content.json`
- **Q** = `A/sources/api-teams-review-projection/r2`
- **P** = `/paths/~1api~1control~1api~1teams~1v1~1teams`
- **C** = `/components/schemas`

Read the complete reviewer assignment, analyst assignment and `A/reports/DELTA-TEAMS-API-CONTRACT.md`, including its acceptance block.

Before policy interpretation, read complete H proposal, design and all six specifications: control-center-api-integration, control-center-http, control-center-mock-server, control-center-permissions, control-center-shell and mpmm-session. No dedicated demo comparison was undertaken.

Independently read:

- S **1–328**, complete.
- `wiki-241080659-readable/r1/body-view-chunks.json:1–10`, all eight entries, **zero-based 0–7 / human 1–8**, as inert text.
- Original selected `wiki-241080659/r1/content.json:1`, including the full `/bodyView` and separate `/attachments`.
- Original and readable metadata completely.
- Saved API r2 metadata completely.
- Q `operations.json:1–602`, all eight complete operation objects.
- Q `schema-01.json` through `schema-29.json`, all complete schema objects.
- Q `closure.json:1–339` and `metadata.json`, completely.

**Extraction limitation:** O is one approximately 410 KB line, exceeding the read tool’s limit. No parsing tool was available. I requested a narrow projection from the supervisor rather than claiming an independent original-file parse. The supervisor supplied Q and attributed its extraction, pointer-resolution equality assertions, recursive closure computation and hash computation to the parent. I independently inspected every projected operation/schema and their reference relationships. Original-to-projection equality and hashes remain **parent-attributed**.

Reused, without rerunning their source audits:

- DELTA-TEAMS-ROOT-DOC and R-DELTA-TEAMS-ROOT-DOC; D-039.
- DELTA-ACCESS-ROLES-ROOT-DOCS and its review; D-042.
- REQ-MOS-905 and RECON-MOS-905; D-008.

Read the relevant decisions at `A/decisions.md:9–13,37–41,55–59,209–221,297–305`. D-046 supplies acquisition relevance/authority, not semantic acceptance.

## Source identity and structure

The saved envelope and metadata agree on page **241080659**, revision r1, wiki version **5**, timestamp `2026-09-16T18:26:00.056+08:00`, capture `2026-10-19T13:03:50.342Z`, HTTP 200 and zero recorded redactions. S2 identifies contract **v1.1**.

The separately returned `/attachments` object contains status 200, start 0, limit 100, size 0, next null and results `[]`. This establishes the saved empty returned index only—not global attachment absence or an empty document.

All eight HTML chunks were inspected, including split table markup and the final version-history continuation. Four-column request tables and three-column model tables support the readable derivative’s interpretation.

S3 and S325–328 claim synchronization with implementation. Those remain **source assertions**, not runtime proof or a precedence rule. The exact contract is now available; historical “uncollected” statements in the MOS905 chain are not current acquisition gaps. Earlier discovery failures remain historical discovery failures. No additional root membership follows.

Hashes, acquisition authenticity and chunk roundtrip were not independently recertified.

## Eight-operation locator verification

The following are exact pointer concatenations in O; `~1` escapes a slash within a path key. Q’s operation array indices are zero-based.

| Q index | Method and path suffix after `/api/control/api/teams/v1/teams` | Exact operation pointer | Success schema, under C | Source section / lines / zero-based chunks |
|---|---|---|---|---|
| 0 | GET, empty suffix | P`/get` | `TsamResponseSchema_PaginatedResponseSchema_list_TeamResponse___`, 200 | §2.1 / 83–141 / 2–3 |
| 1 | GET `/{team_id}` | P`~1{team_id}/get` | `TsamResponseSchema_TeamResponse_`, 200 | §2.2 / 142–165 / 3 |
| 2 | GET `/{team_id}/members` | P`~1{team_id}~1members/get` | `TsamResponseSchema_PaginatedResponseSchema_list_TeamMemberResponse___`, 200 | §2.3 / 166–205 / 3–4 |
| 3 | POST, empty suffix | P`/post` | `TsamResponseSchema_TeamMutationResponse_`, 201 | §2.4 / 206–233 / 4 |
| 4 | PATCH `/{team_id}` | P`~1{team_id}/patch` | `TsamResponseSchema_TeamMutationResponse_`, 200 | §2.5 / 234–247 / 4–5 |
| 5 | POST `/{team_id}/members` | P`~1{team_id}~1members/post` | `TsamResponseSchema_TeamMemberMutationResponse_`, 201 | §2.6 / 248–272 / 5 |
| 6 | PATCH `/{team_id}/members/{user_id}` | P`~1{team_id}~1members~1{user_id}/patch` | `TsamResponseSchema_TeamMemberMutationResponse_`, 200 | §2.7 / 273–284 / 5–6 |
| 7 | POST `/{team_id}/members/{user_id}/actions/remove` | P`~1{team_id}~1members~1{user_id}~1actions~1remove/post` | `TsamResponseSchema_RemoveTeamMemberResponse_`, 200 | §2.8 / 285–303 / 6 |

Success references occur at each operation plus `/responses/{status}/content/application~1json/schema/$ref`. All eight declare 422 at the corresponding response pointer, referencing C`/HTTPValidationError`; no other error responses appear in these selected objects.

All five mutations have required request bodies. Their `/requestBody/content/application~1json/schema/$ref` targets are respectively CreateTeamRequest, UpdateTeamRequest, AddTeamMemberRequest, UpdateTeamMemberRequest and RemoveTeamMemberRequest.

Parameter indices also agree:

- Team list: query **0**, sort **1**, limit **2**, offset **3**.
- Member list: team_id **0**, query **1**, membership_role **2**, sort **3**, limit **4**, offset **5**.
- Member update/removal: team_id **0**, user_id **1**.

## Schema closure and field checks

The **29-schema claim is supported by the inspected projection**, not merely repeated from the analyst report. The closure consists of:

- **6** success envelopes listed above.
- **5** request schemas listed above.
- **8** business response schemas: TeamResponse, TeamMutationResponse, TeamMemberResponse, TeamMemberMutationResponse, RemoveTeamMemberResponse, TeamDomainResponse, TeamSkillResponse, TeamSurfaceResponse.
- **2** paginated schemas: `PaginatedResponseSchema_list_TeamResponse__` and `PaginatedResponseSchema_list_TeamMemberResponse__`.
- **8** shared schemas: PaginationDto, FullName, TeamMemberRole, SurfaceStatus, ResponseCode, ErrorItem, HTTPValidationError, ValidationError.

Every inspected `$ref` resolves within those 29 projected schema objects. Q’s 54-edge list comprises 21 operation references and 33 schema references. Security scheme definitions are outside this schema-reference closure; operation security arrays were inspected directly.

Verified at each named C child’s `/properties` and `/required`:

- TeamResponse requires all ten fields; TeamMutationResponse requires the six summary fields. Their declared fields are non-nullable.
- TeamMemberResponse requires id/full_name/email/roles/membership_role/valid_from. Mutation response requires id/membership_role/valid_from; removal response requires id.
- FullName requires family_name/name; middle_name is optional and nullable.
- User identifiers are plain strings in the four cited schemas and update/removal path parameters. Team and related entity identifiers declare UUID format.
- TeamMemberRole is lead/member. SurfaceStatus has the seven reported values.
- CreateTeamRequest and UpdateTeamRequest require name, department_name and reason. Name/department bounds are 1–200; reason bounds are 1–1000. Membership requests require their reported fields and reason bounds. PATCH is not an all-optional request.
- Both paginated DTOs require items/pagination. PaginationDto requires all five integer fields; its response fields do not independently declare the query bounds.
- Query and member-role filters are optional nullable strings. Sort is an optional non-nullable string, defaulting to name/full_name. Limit is 1–100, default 50; offset is at least 0, default 0.
- All six success envelopes require code/data/message. Data is a non-nullable referenced object; errors is an optional non-nullable array.
- ResponseCode is unrestricted string. ErrorItem requires message; field/code/details are optional nullable fields, with details an object when non-null.
- HTTPValidationError’s detail array is optional; its items reference ValidationError, which requires loc/msg/type. Loc accepts string/integer elements; input and ctx are optional.

No version or Idempotency-Key declaration appears in the selected operations and schema closure. This is a scoped publication observation, not a prohibition of additional properties, a whole-API absence finding or a backend capability claim.

## TEAMAPI-01–08 dispositions

| Candidate | Decision and evidence |
|---|---|
| **TEAMAPI-01** | **ACCEPT.** S5–11,38–44,318–319 and chunks 0/6 support Bearer, request-ID and administrator/member/lead prose. All eight operation `/security` arrays contain separate AdminToken and AccessToken objects: formal OR. H HTTP 3–7, permissions 7–41/77–89 and design 143–149 preserve approved raw-header AND normalization, exact UI permissions and backend scope. No role-derived grant, transport ACL or wildcard global-data inference follows. |
| **TEAMAPI-02** | **ACCEPT.** S45–81,99–165 and C TeamResponse/TeamMutationResponse support expanded list/card versus summary mutations. Related DTOs, domain skills_count and statuses match. Computed counts and membership-driven updated_at remain prose semantics. No association-write operation, wizard atomicity or resolution of earlier creation contradictions follows. |
| **TEAMAPI-03** | **ACCEPT.** S87–91,141,170–175 and the checked parameter indices support prefix search, pagination and ordering candidates. Sort defaults are explicitly published; allowed sort combinations, prefix behavior, comma-separated role interpretation, final id tie-breakers and nested ordering are not encoded as validation/enforcement guarantees. Members order lead before member then id; surfaces name then id. No client-side filtering or actual server enforcement is inferred. |
| **TEAMAPI-04** | **ACCEPT.** S58–67,253–255 versus the cited identifier schemas/path parameters establishes UUID prose versus plain-string publication. FullName optionality/nullability is accurately reported. Functional roles, team membership role and authenticated principal/permissions remain separate; no coercion, enum expansion or directory mapping is warranted. |
| **TEAMAPI-05** | **ACCEPT.** S210–214,238–240,250–255,277–278,289–290 and the five request schemas support required fields and bounds. Trimming is explicitly stated in create §2.4, not verified globally. S48 and S250 support case-insensitive name uniqueness and no duplicate same-team membership. Neither resolves exactly-one-lead, duplicate-email, default-view or employee-derived-role ambiguities. |
| **TEAMAPI-06** | **ACCEPT.** S273–303 explicitly preserves valid_from on role change and specifies POST removal, physical membership deletion and a domain audit event. These are distinct from proposed soft deletion of the team entity. Date-time schema typing does not prove preservation. Event prose supplies no history reader endpoint, retention, ordering, completeness or reader grant; MOS1031 remains gated. |
| **TEAMAPI-07** | **ACCEPT.** S12–31,304–324 versus the eight 422 references and C HTTPValidationError/ValidationError establishes the documentary representation difference. ResponseCode and ErrorItem qualifications are correct. Source 401/403/404/409/422 conditions do not establish runtime error priority. Approved observable-error handling remains intact without a SUCCESS-only enum assumption or hidden retry. |
| **TEAMAPI-08** | **ACCEPT.** S325–328, chunks 6–7, supplies the attributed v1.1 removal statement; selected publication objects contain no version/idempotency declaration. This does not establish timeout, replay, concurrency or exactly-once semantics and does not revoke shared same-user logical-operation preservation, owner/generation isolation or the prohibition on automatic mutation replay. |

## Preserved boundaries and residual limits

The report correctly preserves:

- Approved UI permissions versus backend request authorization and object scope, including for `*`.
- Business member/contact DTOs versus confirmed session principal.
- Team:view versus wildcard-only audit UI, and UI visibility versus MOS1031 reader-service acceptance.
- MOS1023 token, source-conflict, owner/session, partial-save and no-sandbox gates.
- Bounded absence of detailed team-owner acceptance; no renewed issue search or global absence claim.
- D-008’s already-reconciled shell routes/tabs/fallback, without duplicate shell tasks or team CRUD-delivery inference.
- D-046 acquisition authority as distinct from semantic approval.
- Documentary omissions as scoped to the inspected publication, not backend absence.

No runtime behavior, deployment, CORS, refresh rotation, restricted-account enforcement or source precedence was verified. No application code, tests or implementation assertions were inspected.

Only local read/discovery tools and the blocking supervisor projection request were used. No shell commands, network/browser access, storage or credential inspection, requests, downloads, rendering/source execution, code changes, tests/builds, nested delegation or repository mutation occurred. Staging state was not inspected or attested.