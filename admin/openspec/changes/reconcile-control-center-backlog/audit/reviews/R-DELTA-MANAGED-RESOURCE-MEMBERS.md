# R-DELTA-MANAGED-RESOURCE-MEMBERS — independent documentary review

## Review

**ACCEPT — MR-D01–MR-D12, without mandatory corrections.**

No issues found.

- **Correct:** The twelve candidates faithfully supplement historical missing-description findings while preserving unresolved UI choices, existing routing and evidence limitations.
- **Fixed:** None; read-only review.
- **Mandatory corrections:** None.
- **Merge verdict:** OK for bounded documentary evidence only. Parent acceptance/publication remains required; no implementation approval or global closure follows.

`A` means `openspec/changes/reconcile-control-center-backlog/audit/`. `C1321`, `C1399` and `C1386` mean the respective `A/sources/jira-MOS-<number>/r1/content.json` files. Description locators below refer to `/description` at line 7; bullet numbers count top-level bullets within the named heading.

## Per-ID dispositions

| Candidate | Verdict | Independently checked evidence and retained boundary |
|---|---|---|
| **MR-D01** | ACCEPT | All three complete selected packets and adjacent metadata now supply descriptions, embedded acceptance/DoD, empty returned attachment/subtask arrays and both returned comment entries. This qualifies D-025 and the historical inventory/journal gaps, without rewriting their original evidence boundaries. Custom acceptance fields, independent parent objects and frontend assignment remain unprovided. |
| **MR-D02** | ACCEPT | C1321 “Что делаем” 2–6 and DoD 2–6 directly support all three mutation groups, protected group/type/storage table, immutable system/informational dictionary codes, per-dictionary value identity/isolation and a common user-value table without dynamic tables. DoD 5 permits at most one active default; it does not require a default in every dictionary. Shared form lookups do not settle accounting questions JR-02-08/09. |
| **MR-D03** | ACCEPT | C1321 “Что делаем” 1 and DoD 2 specify ordinary search/filtering; DoD 5 concerns stored value order. Journal JR-02-01/02 separately requests registry sorting and excludes complex selection conditions now while retaining a future marker. No conflict, precedence or API-registry analogy is invented. |
| **MR-D04** | ACCEPT | C1321 “Что делаем” 3–4,7 and DoD 2–5 do not resolve journal JR-02-03/04/05/07. The report preserves definite modal→card/tab intent, conditional page accounting, distinct Latin/uniqueness errors, the unselected activation alternatives and unapproved widget experiment. Value-code identity is not a dictionary service-code regex or error protocol. |
| **MR-D05** | ACCEPT | C1321 DoD 7 explicitly requests CSV list/card/value exports. JR-02-06 supplies selection/completion modal intent, not byte format, completion semantics or failure handling. C1386’s selectable export fields are correctly not transferred to dictionaries. |
| **MR-D06** | ACCEPT | C1399 “Что сделать” 1–7 and acceptance 1–5 identify exactly two collections, code PKs, three named dictionary-group seeds, fourteen asserted but unenumerated check types, group FK/metadata, registration, lookup inclusion and prohibited value mutations. Acceptance 1–2 genuinely says “типа влияния”/“тип влияния”; preserving this ambiguity without inventing a third collection is correct. Physical-name latitude does not authorize wire-name changes or loss of existing group values. |
| **MR-D07** | ACCEPT | C1321 common user-value storage and C1399 system references do not prove replacement of skill-specific persistence. Accepted MOS1119-D01–05 and TP01/08 preserve the explicit `updated_at` disagreement, MOS-1031 reader gate, disabled-restoration questions and distinction between seeds and UI commands. The report retains these rather than asserting a migration, reader publication or new owner plan. |
| **MR-D08** | ACCEPT | C1386 “Что делаем” 1–2,8 and DoD 1–6 directly request CRUD/PUT/soft deletion, the three tables, atomic nested save, preserved existing child IDs/order, the stated uniqueness rules, required sources for incoming/outgoing groups and an external-user string identifier without local projection. None proves an actual transaction or specifies Disable/Suspend commands. JR-02-13’s create/card action distinction remains intact. |
| **MR-D09** | ACCEPT | C1386 “Что делаем” 3,5–7 and DoD 7–10 support selection/sorting/group counts, selectable-field CSV exports, reference collections, metadata and namespace/access/OpenAPI/testing requirements. These are requested contracts, not inspected publication, seed completeness, frontend compatibility or export-completion protocol. API counts and selection conditions do not override dictionary journal qualifications. |
| **MR-D10** | ACCEPT | C1321 “Что делаем” 7 and C1386 “Что делаем” 7–8/DoD 9 provide field-validation/metadata intent, not universal departure guards or cross-tab error discoverability. JR-02-11/12 remain bounded per-owner follow-up. Earlier partial specification coverage is explicitly attributed, not freshly certified. |
| **MR-D11** | ACCEPT | C1321’s explicit exclusion concerns automatic user-dictionary form wiring and external-system business logic; its relevant-form shared lookup requirement remains distinct. C1386 “Что делаем” 4 and the exclusion paragraph distinguish stored publication configuration from landing generation, request execution, availability checking and call-log storage. Business authorization fields and general access checking do not approve app-session changes. |
| **MR-D12** | ACCEPT | All three `/issueStatus` values are Hold. Each `/comments` records `startAt:0,maxResults:2,total:2` and two saved entries, with the automated MR body intentionally omitted. Testing statements establish no successful tests, deployment or frontend ownership. D-022/023’s r2 qualification remains intact; no fresh API audit is claimed. |

**Per-ID exceptions: none.**

## Exact source and provenance checks

The testing comments are correctly identified:

- C1321 `/comments/items/1`: **1129414**, “Готово, тестируем вместе с фронтендом”.
- C1399 `/comments/items/1`: **1131702**, “Готово, тестировать вместе с фронтендом”.
- C1386 `/comments/items/1`: **1131540**, “Готово, тестируем вместе с фронтендом”.

The intentionally omitted automated mention bodies belong to **1129117**, **1131561** and **1131237**, respectively. Complete returned pagination is not a claim that original MR bodies were inspected or that all externally visible issue evidence was collected.

The report’s retrieval/update timestamps match `/retrievedAt`, `/updated` and adjacent metadata. Metadata explicitly describes selected authorized-page packets recovered from the parent’s local transcript, not full Jira exports.

Declared SHA-256 values were read, **not recomputed**:

| Source | Metadata digest |
|---|---|
| MOS-1321 r1 | `91650bd4949d81320b92c2c48634dd6f6d0822fd3596dcfbbd4a7c53c1a712ef` |
| MOS-1399 r1 | `492c8657adefc973041498ff0c7363180492491a8d6064645a9a12c562f630ff` |
| MOS-1386 r1 | `25faae6338d2fb4be09763d392ad167a253326df47654495a6768cf31d8a4e59` |
| Journal r1 | `cd74e398e690d48e3da571a6c2adf02d8c755856948d98747b8d447ad628244d` |

## Independent journal and inventory comparison

Unlike the analyst’s explicitly attributed journal comparison, this review directly inspected `A/sources/wiki-250781168/r1/content.json` `/bodyView` and `/bodyStorage` at lines 10–11, restricted semantically to the legend and rows2/4/5.

Confirmed:

- Row2: `table/tbody/tr[3]/td[2]/div/ol/li[1–13]`, with OPEN status.
- Row4: `tr[5]/td[2]/div/p[2],p[4],p[6]`, with CLOSED status: integration target and attributed temporary generation remain distinct.
- Row5: `tr[6]/td[2]/div/p[2],p[3]`, with CLOSED status: physical table-name latitude only.

The new member descriptions neither select JR-02-05’s alternatives nor approve JR-02-07’s experiment. They do not supply JR-02-08/09 meeting outcomes, resolve domain-code provisioning or convert OPEN/CLOSED labels into runtime evidence.

Directly inspected raw inventory excerpts:

- `A/sources/jira-hierarchy/r1/content.json:29,33`: MOS-1327 → MOS-1321/MOS-1399; MOS-1403 → MOS-1386.
- `A/sources/jira-member-index/r1/content.json:1197–1212,1253–1260`: selected member summaries, Hold statuses, historical update timestamps and empty subtasks.

These corroborate the reported routes, not frontend ownership. Global inventory uniqueness, hidden membership, subtask completeness and supplementary-packet absence were **not independently rescanned**; those broader census claims remain attributed to the accepted inventories.

## Actual verification boundary

Read:

- Both assigned work items and the complete twelve-candidate report.
- Complete selected content and metadata for all three new Jira packets.
- Complete `JOURNAL-REMAINING-ROWS` report and independent review.
- Relevant D-025, D-022/023 and D-016/017 decision sections.
- Complete JIRA-MOS-1327/1403 inventory reports and the raw excerpts listed above.
- Scoped MOS1119 report/review passages: `DELTA-MOS-1119:30–74`, `R-DELTA-MOS-1119:36–74`, `DELTA-MOS-1119-TESTPLAN:40–93`, and `R-DELTA-MOS-1119-TESTPLAN:42–90`.
- Primary journal body fields and metadata, with assessment limited to the assigned rows and legend.

MOS1119 original storage/test-plan packets, current owner specifications and domain implementation/contracts were not freshly audited. Their accepted qualifications remain prior evidence, not new independent verification here.

Only local documentary reads occurred. No direct edits, shell commands, tests/builds/E2E, code scan, network/browser/MCP, credentials/business calls, linked Jira traversal, API-schema scan or nested delegation occurred. Hash integrity, deployment, runtime behavior, repository index state and current API completeness remain unverified.

This acceptance supplies documentary review evidence only. It selects no policy alternative, changes no source precedence, authorizes no implementation and closes no global task.