# JIRA-MOS-1246 — hierarchy inventory

Report destination: `openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-1246.md`  
Runtime-bound report; no repository files written.

## Evidence locators

All paths are repository-relative:

- **W:** `openspec/changes/reconcile-control-center-backlog/audit/work-items/JIRA-MOS-1246.md`, lines 1–10: assignment and scope.
- **H:** `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-hierarchy/r1/content.json`, lines 2–6, 28: capture provenance, completeness caveat, and module membership.
- **D:** `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-feedback/r1/content.json`, lines 1–114: 12 selected-field issue records.
- **M:** `openspec/changes/reconcile-control-center-backlog/audit/sources/jira-feedback/r1/metadata.json`, lines 2–10: revision, retrieval time, extraction fields, provenance and omissions.

## Reconciliation result

**11 unique observed member keys match exactly 11 issue records, plus the module record: 12 unique records total.** No missing records, extra records, duplicate keys or conflicting membership found.

MOS-1246 is **Q key result**, not a literal Epic. All 11 members are **Development task**. Membership comes from H, not from the standard `parent` field.

| Key | Inventory label | Saved status | Saved `updated` (verbatim) | D lines |
|---|---|---|---|---|
| MOS-1246 | Module “Обратная связь” | Backlog | `2026-10-09T15:03:47.673+0800` | 5–13 |
| MOS-1231 | Backend feedback section | Hold | `2026-10-13T14:28:07.591+0800` | 14–22 |
| MOS-1249 | FE API, lookup values and metadata | Ready for test | `2026-10-16T18:44:03.867+0800` | 23–31 |
| MOS-1250 | FE survey registry and basic filtering | Development | `2026-10-16T18:44:42.569+0800` | 32–40 |
| MOS-1251 | FE survey card and display rules | Backlog | `2026-10-12T21:10:48.642+0800` | 41–49 |
| MOS-1254 | FE question and option builder | Backlog | `2026-10-12T20:49:05.464+0800` | 50–58 |
| MOS-1255 | FE interactive questionnaire preview | Backlog | `2026-10-12T20:49:12.702+0800` | 59–67 |
| MOS-1256 | FE survey status changes and deletion | Backlog | `2026-10-12T21:13:38.503+0800` | 68–76 |
| MOS-1257 | FE tags, segments and operator groups | Backlog | `2026-10-12T20:49:41.953+0800` | 77–85 |
| MOS-1258 | FE advanced selection conditions | Backlog | `2026-10-12T21:16:28.873+0800` | 86–94 |
| MOS-1259 | FE server-side saved filters | Backlog | `2026-10-12T20:50:17.071+0800` | 95–103 |
| MOS-1260 | FE registry/card CSV export | Backlog | `2026-10-12T20:50:27.969+0800` | 104–112 |

Member status totals: **8 Backlog, 1 Hold, 1 Ready for test, 1 Development**. Module status: Backlog.

## Nested subtasks and dependency evidence

- Every record explicitly contains `subtasks: []`: D lines **11, 20, 29, 38, 47, 56, 65, 74, 83, 92, 101, 110**. Nested-subtask fields were checked for all 12 records; no nested keys were exposed for further inventory.
- The module’s empty `subtasks` does **not** negate its 11 hierarchy-panel members: these are distinct evidence fields.
- MOS-1231 remains **backend dependency evidence**, not frontend implementation scope. Its description references the shared CRUD mechanism MOS-1142 (D line 21). That referenced issue is not an observed member of this module and was not retrieved or assessed in this inventory.

## Version context and limitations

- Hierarchy capture: **`2026-10-16T11:08:08.629Z`** (H line 2).
- Issue packet: **revision 1**, retrieved **`2026-10-16T11:17:16.813Z`** (M lines 3–4; D line 2).
- These are saved snapshots, not live Jira verification or issue history. Status and update timestamps above are retained without inferring implementation completion.
- All 12 records contain descriptions and the displayed identity/status/type/update/subtask fields. No issue detail record is missing within the observed set.
- `parent` is absent from every extracted record, although named in the request-field locator (M line 6). No parent relationship is inferred from that omission.
- **Comments, attachments and custom acceptance fields were not collected** (M line 10). Acceptance text embedded in descriptions is present but was not semantically assessed.
- The hierarchy capture found no more/next controls, but explicitly does not prove completeness against hidden or permission-filtered issues (H line 6). Empty saved subtask arrays likewise do not establish universal absence.
- No whole-section requirements analysis, implementation review, network/MCP access, tests, generation or repository edits performed.