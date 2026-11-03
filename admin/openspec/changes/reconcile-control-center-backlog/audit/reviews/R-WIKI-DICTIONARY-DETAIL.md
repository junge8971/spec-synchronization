# R-WIKI-DICTIONARY-DETAIL — independent documentary review

## Review

**REVISE — WD-12 arithmetic and the report’s chunk-count convention require correction.** The other thirteen candidates are accepted as bounded documentary findings.

- **Correct:** Primary wiki, Jira and journal evidence supports the substantive reconciliation, including unresolved mutation policies, complex-filter scope and fourteen explicit check identities.
- **Fixed:** None; local read-only review.
- **Finding — P1:** WD-12 miscounts the classifications: **29 system / 10 informational**, not 30 / 9.
- **Finding — P2:** Coverage statements claim 27 HTML chunks; the saved array contains **26**.
- **Merge verdict:** **BLOCK** documentary acceptance pending these small corrections. No implementation defect or feature-acceptance conclusion follows.

`A` = `openspec/changes/reconcile-control-center-backlog/audit/`; `T` = `A/sources/wiki-247751846-readable/r1/content.txt`; `H` = adjacent `body-view-chunks.json`. `P` and `M` denote the page’s “Описание” and “Таблицы” headings. Chunk references below are **one-based array elements**, not file lines.

## Mandatory corrections

### 1. WD-12: correct the independently recounted classification totals

**Location:** `A/reports/WIKI-DICTIONARY-DETAIL.md:52`.

The total **39** is correct, but its partition is not. I manually counted the actual field rows and their classification cells in M “Справочные значения”, checked against exact markup in **H chunks 12–16**:

| Section | System | Informational | Total |
|---|---:|---:|---:|
| Обратная связь | 8 | 1 | 9 |
| База знаний | 3 | 3 | 6 |
| Шаблоны ответов | 1 | 3 | 4 |
| A/B эксперименты | 3 | 1 | 4 |
| API | 5 | 1 | 6 |
| Состояние системы | 5 | 1 | 6 |
| Справочники | 4 | 0 | 4 |
| **Total** | **29** | **10** | **39** |

The informational rows are: low-rating reasons; knowledge category, material type and language; template type, owner and scope; experiment metric; API landing category; system-state “Влияет на”.

In particular, the template-owner entry is **one complete table row** in H chunk 14, despite its multiline text extraction.

**Smallest fix:** Replace “30 system/9 informational” with “29 system/10 informational” and retain a short per-section recount. The source’s own summary remains demonstrably inconsistent: **24/8/0 = 32**, versus the listed **29/10/0 = 39**. This arithmetic does not resolve journal accounting questions or establish a migration requirement.

### 2. Correct the chunk coverage convention

**Locations:** report lines **7, 12 and 77**.

Direct bounded reads establish:

- H line 1: opening `[`.
- H lines **2–27**: **26** string elements.
- H line **28**: closing `]`.
- Final chunk **26**, at line **27**, ends with M §8’s seven-table inventory.

**Smallest fix:** Change “27 chunks” to “26 chunks”; change “chunk 27 is line 28” to “chunk 26 is line 27; line 28 closes the array”; correct the claimed substantive file span accordingly, including the acceptance-report block.

This is a counting/locator error, **not evidence of an unread body region**. The report’s candidate references through chunk 26 remain usable.

## Per-ID verification

| ID | Verdict | Independent evidence and retained qualification |
|---|---|---|
| **WD-01** | ACCEPT | P §§3.3–3.5, H 2–3: five sortable columns, three-click cycle, two-character search over name/code/description and type/status multiselects. MOS-1321 `/description`, ordinary search/filter requirements, agrees. No default order or transport protocol follows. |
| **WD-02** | ACCEPT | P §§4,6,8 and M §3.1 verify metadata, tabs, user-only modal creation, code pattern/uniqueness checks, draft defaults and immediate card opening. Journal row2 bullets 3–4 retain conditional page accounting and distinct error-message requirements. M’s creation-field mention does not authorize a type selector. Model column lengths are not independently established UI/wire validation rules. |
| **WD-03** | ACCEPT | P §§5.4,9, H 7,10: selected list-export fields, filtered selection, UTF-8 BOM and all-value CSV; attachment export includes note. MOS-1321 DoD 7 requests list/card/value export. Journal bullet 6 additionally requests completion modal; its semantics and separate card payload remain unspecified. |
| **WD-04** | ACCEPT | M §§4.2–4.3, H 22–24, explicitly supplies code-PK structure and all fourteen check identities. P §7.2 distinguishes ten general checks from four attachment checks. MOS-1399 requests these seeds and read-only system references, not proof of deployed data or working checks. Historical missing-identity statements can now be qualified for current use. |
| **WD-05** | ACCEPT | P §§3.6–3.8,13 expressly describes complex conditions, saved filters and URL selection. Primary journal row2 `li[2]` expressly says not to insert complex filtering now and to retain a future marker. This is a genuine documentary scope disagreement. Ordinary filtering and saving ordinary selections are not independently prohibited. |
| **WD-06** | ACCEPT | P §2 explicitly permits informational-value deletion; §§5.1–5.2/6.2 describe editable rows/code and settings-dependent deletion. M §3.1 specifies soft deletion. MOS-1321 “Что делаем” bullet 2 expressly forbids informational-value deletion **and code changes**. Soft deletion does not remove that disagreement. Dictionary deletion is separately restricted to user dictionaries by both sources. |
| **WD-07** | ACCEPT | P §§4.1,8.2,10.1 and M §3.1 support draft creation, informational/user suspension and user-only `is_disabled`. The mapping between status and that field is not supplied. Journal bullet 5 leaves separate activation control versus dynamic label unresolved; Suspend does not settle first activation. |
| **WD-08** | ACCEPT | P §5.2 allows clearing default; P §7.2/M §4.3 say **at most one**. MOS-1321 DoD 5 adds active-default validation. Missing guard explanation is not an explicit instruction to accept inactive defaults. Optional creation fields versus readiness checks may reflect warnings or staged validation; no universal blocking interpretation is justified. |
| **WD-09** | ACCEPT | M’s field inventory and §5 assign different classifications to categories, low-rating reasons and template types. Domain-storage prose and the shared-user-table entries also require reconciliation. The explicit prototype basis and reasons-migration note must remain visible: these are documentary classification/storage tensions, not proof of faulty runtime storage or authority to migrate domains. |
| **WD-10** | ACCEPT | P §§5.3–5.4/M §3.2 describe attachment-rule operations, while M §5 classifies `attachment_rules` as system and general rules prohibit system mutations. No special-kind override is stated. Missing `deleted_at` in the listed rule fields is a model clarification, not proof soft deletion cannot exist. Upload/auth-zone prose authorizes no session or security changes. |
| **WD-11** | ACCEPT | M uses `dictionary_type → ref_dictionary_types.code`; MOS-1399 explicitly requires preserved `group` FK and metadata binding. Same seeds narrow the terminology issue without establishing wire equivalence. Its two required system registrations are absent from M §5’s **prototype-based** eleven-entry roster; completeness needs clarification, not a claim of runtime absence or a definitive contradiction between differently scoped inventories. |
| **WD-12** | **REVISE** | Shared storage, per-dictionary identity and the ambiguous 1:1 wording are correctly bounded. Replace the incorrect classification split with the independent **29/10** recount above. The eleven registry entries count a different unit from the 39 field rows. |
| **WD-13** | ACCEPT | P §§7,11 supports summary colors/icons, problematic-check count, tab emphasis, changing counters, dirty-card close confirmation and updated date. Journal bullets 7,11–12 remain broader: widget experiment, all-creation departure behavior and other-tab field discoverability are not fully answered by these dictionary-card details. |
| **WD-14** | ACCEPT | M §§3–8 supplies documentary fields, four references and seven tables. Jira’s namespace/lookup requirements remain requested contracts, not inspected API publication. Immediate-propagation prose and cache duration do not establish a consistency protocol. Attachments, frontend assignment and runtime readiness remain unverified. |

**Per-ID exception:** WD-12 only. The chunk-count correction applies to report-wide evidence accounting.

## Fourteen-check identity verification

Confirmed directly in M §4.3, H chunks **23–24**:

1. `name_filled`
2. `code_filled`
3. `code_unique`
4. `description_filled`
5. `owner_filled`
6. `values_exist`
7. `value_codes_filled`
8. `value_names_filled`
9. `value_codes_unique`
10. `single_default`
11. `rule_extensions`
12. `rule_mime`
13. `rule_zones`
14. `rule_enabled`

`single_default` explicitly means **“Не более одного значения по умолчанию”**. `rule_enabled` requires at least one enabled attachment rule. Neither implies that every dictionary must have a default or that all fourteen checks apply to every kind.

## Primary journal and Jira comparison

Independently inspected `A/sources/wiki-250781168/r1/content.json:10–11`, both body representations, assessing only the legend and assigned rows:

- Dictionary units: `/bodyStorage`, `table/tbody/tr[3]/td[2]/div/ol/li[1–13]`; source row is **OPEN**.
- Physical naming: `tr[6]/td[2]/div/p[2],p[3]`; source row is **CLOSED**.

The report faithfully retains definite requests, unresolved alternatives, experimental widgets and uncollected accounting outcomes. CLOSED naming latitude concerns physical table names, not API properties, lookup keys, FK semantics or group preservation.

Both complete selected Jira packets and their metadata were read:

- MOS-1321 r1: updated **2026-10-14T14:03:49.652+0800**.
- MOS-1399 r1: updated **2026-10-16T19:23:59.073+0800**.

Both are **Hold**. Comments **1129414** and **1131702** request testing with frontend, not attest successful tests. Automated mention bodies **1129117** and **1131561** are intentionally omitted. Returned empty attachment/subtask arrays and complete saved comment pagination are not global completeness guarantees.

## Verification coverage and boundaries

Read independently:

- Both assigned work items and the complete fourteen-candidate report.
- Entire readable wiki body, continuing at T line 448 after the initial 50KB truncation.
- Entire exact chunk array through its closing delimiter, using bounded reads: lines 1–8, 9–15, 16–22 and 23–end; terminal lines rechecked separately.
- Wiki source and derivative metadata, plus primary attachment index.
- Both selected Jira content packets and adjacent metadata.
- Primary journal body representations and metadata, limited semantically as above.
- D-025/D-026, both accepted prior reviews, and relevant dictionary/journal report passages for routing and preserved gates.

Wiki **247751846 v10**, updated **2026-10-15T20:10:40.182+08:00**, and journal **250781168 v8**, updated **2026-10-08T18:31:40.254+08:00**, match their saved metadata. Hashes were **not recomputed**; derivative roundtrip equality remains explicitly attributed to parent computation.

No saved dictionary-body region remains unread. Both HTML attachment bodies remain unread:

- **250805153** — `Справочники_Прототип.html`
- **247751845** — `Справочники отдельно.html`

The index has two entries and no next page; neither prototype rendering, thumbnail bytes nor a PDF was inspected.

Existing MOS-1327 → MOS-1321/MOS-1399 routing remains prior accepted routing, not newly assigned frontend execution. Skill status/transition/history ownership, the separate `updated_at` disagreement, MOS-1031 reader gate, restoration questions, three generic commands, dedicated toggle and historical toggle/auth approvals remain unchanged. Original skill packets and current implementation were not freshly audited.

Only local documentary reads and targeted search occurred. No edits, network/browser/MCP, shell commands, code audit, tests/build/E2E, source execution, credentials/business requests or nested delegation occurred. No source precedence, UI alternative, migration, implementation authorization or global closure is selected.

**Acceptance can follow correction of the two documentary errors above; product disagreements remain unresolved evidence, not review failures or runtime defects.**