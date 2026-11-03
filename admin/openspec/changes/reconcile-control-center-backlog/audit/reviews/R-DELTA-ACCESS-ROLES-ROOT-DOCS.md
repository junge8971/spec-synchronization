# R-DELTA-ACCESS-ROLES-ROOT-DOCS

## Review

**Disposition: ACCEPT.**  
**Merge verdict: OK** for this bounded documentary report only.

No issues found.

- **Correct:** ACCESS-ROOT-01–11 preserve the saved sources’ distinctions and the approved auth/demo boundaries.
- **Fixed:** None; review was read-only.
- **Mandatory fixes:** None.

## Evidence and coverage

Aliases:
- **A** = `openspec/changes/reconcile-control-center-backlog/audit/`
- **R** = `A/sources/wiki-241102892-readable/r1/content.txt`
- **B** = `A/sources/wiki-238333356-readable/r1/content.txt`
- **T** = `A/sources/wiki-241080100-readable/r1/content.txt`
- **H** = `openspec/changes/archive/2026-10-09-integrate-mpmm-auth-permissions/`
- **D** = `openspec/changes/archive/2026-10-09-add-local-session-demo/`

Read the complete assigned reviewer work-item, analyst work-item and `A/reports/DELTA-ACCESS-ROLES-ROOT-DOCS.md`.

Before source comparisons, read complete H proposal/design and all six specifications: mpmm-session, control-center-permissions, control-center-http, control-center-api-integration, control-center-mock-server and control-center-shell. Also read complete D proposal/design and all three specifications before evaluating demo switching.

Independently read:
- R **1–146**, r1/v7; all **six** ordered body chunks.
- B **1–57**, r1/v7; all **three** ordered body chunks.
- T **1–56**, r1/v1; all **three** ordered body chunks.
- All six corresponding original/readable metadata files.
- Each original `content.json:12–22` attachment-index region.
- `A/reports/DELTA-TEAMS-ROOT-DOC.md:1–40` solely for the cited membership-evidence limit and TEAMS-ROOT-02.

## Candidate verification

| Candidate | Verified evidence and disposition |
|---|---|
| ACCESS-ROOT-01 | R **1–27**, “Роли” and “Ресурсы”; chunk **0** confirms three blank superadministrator cells. The role table has nine role rows, not three; B has eight, T names six. The report correctly describes R as adding the blank superadministrator row, without synthesizing an enum or grant matrix. Only skill-team/surface-owner rows supply explicit own-object scope text. |
| ACCESS-ROOT-02 | R **28–55**, “Разрешения”, preserves lowercase historical codes, including separate review/rollout entries. They are not TSAM aliases. H permissions **27–28, 38–41** retains the published common `change_status`, not new reviewer/rollout granularity. |
| ACCESS-ROOT-03 | R **56–128, 141–146** covers the remaining catalog. R **68** combines archive/return under `surface:archive`; H permissions **29** distinguishes archive and restore. Sandbox token labels authorize no inspection. Unmapped business UI remains explicit-`*`-only, subject to availability—not a transport ACL. |
| ACCESS-ROOT-04 | R **129–135, 137–140** separately names role/user administration and security/object logs. The report does not conflate them with team membership, a delivered audit API or existing reader-service acceptance. |
| ACCESS-ROOT-05 | R **136**, `users:role_switch`, is explicitly demo prose. D local-session-demo **45–49, 99–103** bounds it to fixed local fixtures and reload; no production switch, arbitrary editor or additional grant follows. |
| ACCESS-ROOT-06 | B **1–9, 21–23** contains six storage/display tasks and separates administrative interface from Control Center. These do not authorize new role-management storage, APIs or UI. |
| ACCESS-ROOT-07 | B **11–20**, R **3–13**, T **29** substantiate the different role inventories and security-administrator descriptions. Differences remain attributed, without hierarchy, synonym grants or active-session/logout scope expansion. |
| ACCESS-ROOT-08 | B **24–57**, chunks **0–2**, confirms empty acceptance and main-scenario content, including collapsed regions. The maintenance heading and Smoke “да” do not supply completed acceptance or approval. |
| ACCESS-ROOT-09 | T **3–4, 16–18, 25–27, 52–53** describes business ownership, members and contacts. TEAMS-ROOT-02 at the reused report **27** supports only the stated membership-role ambiguity. No authenticated principal, UUID mapping or issue ownership is inferred. |
| ACCESS-ROOT-10 | T **12–18, 29, 31–38, 45–50** supports historical role-only access and staged integration intent. Neither “authorized” nor platform-admin labels replace permissions. T **38** excludes an object-rights management system, not backend data scoping. |
| ACCESS-ROOT-11 | T **19–22, 28, 39–46, 48, 54–56** supports audit fields, filters, CSV, failure/retry prose, latency targets and FSTEC wording. These are requirements, not schema delivery, benchmarks or compliance evidence. Team:view does not unlock audit. |

## Policy boundaries

The report correctly retains H permissions **7–89**, HTTP **3–7**, and shell **66–76**:

- Exact case-sensitive action/resource/literal-`*` matching; no role/team-name grants.
- Hidden forbidden UI versus access denial for an existing direct route; unknown routes remain distinct.
- Backend request authorization and data scoping, including with `*`.
- Assignment permission/scope association without frontend cross-assignment unions.
- Existing business validation and unavailable functionality remain limiting conditions.
- No role editor, global logout, new auth model, permission expansion or policy-reapproval request.
- No present API/backend absence inferred from document omissions or chronology.

## Actual limits

Attachment indexes independently inspected show status 200, start 0, limit 100, size 0, next null and empty results. This proves only the saved returned indexes, not global attachment absence or complete exports.

Hashes and chunk roundtrip remain **parent-attributed**, not recomputed. Ordered chunks were read as inert text, not reassembled or rendered. Earlier issue searches and inventory evidence remain attributed and membership-only; no issue graph or owner acceptance was independently established.

No current implementation, API availability, backend enforcement, deployment readiness, reader-access acceptance, CORS or refresh-rotation claim is made. The independent 212-line session source was not read.

Only local read/discovery tools were used. No repository mutations, browser/network access, credentials or storage inspection, requests, execution, code/tests/builds, nested delegation or staging inspection occurred. Global **6/28 remains unchanged**.