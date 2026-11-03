# R-ATTACH-DICTIONARY-PROTOTYPES — independent inert-source review

## Review

**ACCEPT — ADP-01–10 are supported as bounded static documentary findings.**

- **Correct:** The report distinguishes declarations, connected handler branches and sample data from rendered behavior, backend mutation and approved policy.
- **Correct:** P’s list-export file-generation and completion-modal branches are independently verified; its card-header export remains toast-only.
- **Fixed:** None; read-only review.
- **Per-ID exceptions:** None.
- **Minimum mandatory corrections:** None.
- **Merge verdict:** **OK**, limited to acceptance of this selected documentary supplement.

No issues found.

## Evidence convention

`A` = `openspec/changes/reconcile-control-center-backlog/audit/`.

- `P` = `A/sources/wiki-attachment-250805153/r1/content.txt`.
- `S` = `A/sources/wiki-attachment-247751845/r1/content.txt`.

All P/S anchors below are saved-file lines, not rendered locations.

Reviewed the original assignment, complete `reports/ATTACH-DICTIONARY-PROTOTYPES.md`, corrected `reports/WIKI-DICTIONARY-DETAIL.md`, both WD reviews and `decisions.md:1–40`, including D-027/028. The original WD REVISE remains historical; its two corrections have separate accepted verification.

Both adjacent attachment `metadata.json:1–24` identify parent **247751846**, version **1**, inert HTML text, status **200** and zero redactions. Metadata provenance and hashes were read, not independently recomputed or acquisition-verified. Neither filename nor date establishes precedence.

## Per-ID verification

| ID | Verdict | Independently verified evidence and limits |
|---|---|---|
| **ADP-01** | ACCEPT | P:400–465 declares filters and five sortable headings; P:832–878,925–1217,1437–1493 connects condition definitions, AND/OR application, selection and sorting. P:1308–1382 saves search/multiselect/conditions; the complete `copyFilterLink` at P:1383–1391 serializes only `q`. S:324–378,780–897 supplies ordinary multiselect/two-character search without a connected advanced constructor or sorting path. No explicit filter-deferral marker was found within these surfaces or targeted file-scoped wording searches. This does not resolve the attributed journal exclusion. |
| **ADP-02** | ACCEPT | P:2083–2149 contains the modal, lowercase regex, exact uniqueness check through P:911–913, optional description/owner, owner fallback and user/list draft defaults. The name-error expression is unsatisfiable as reported. Literal errors are “Укажите название” and “Укажите уникальный код”, not distinct format/duplicate messages. S:1346–1375 checks only nonempty trimmed prompt results and creates a user/list draft owned by Команда ЖКХ. Card declarations at P:491–516 and S:401–413 support the stated action/tab differences. No approved wire validation or new type selector follows. |
| **ADP-03** | ACCEPT | P:1580–1637,1694–1743,1805–1867 distinguishes system protections, rename/delete flags and informational samples with permissive flags at P:724–792. No informational-specific code/deletion guard occurs in the complete relevant handlers. P:1920–1948 saves allow settings only for user dictionaries. S:923–942,987–994,1046–1090,1145–1157 supports the different system policy and the distinction between disabled deletion markup and an unguarded removal handler. These are source facts, not demonstrated bypasses or backend deletion semantics. |
| **ADP-04** | ACCEPT | Complete save/status functions at P:1920–1962 and S:1280–1330 confirm that save does not activate and pause maps paused→active, otherwise→paused, including draft. P rejects system dictionaries; S’s status handler does not. Labels at P:1567–1569 and S:937–939 agree. This establishes a source-defined draft→paused→active path, not approval of first-activation UX, readiness enforcement or an `is_disabled` mapping. |
| **ADP-05** | ACCEPT | P:1815–1835 and S:1091–1112 independently toggle enabled/default without an active-default guard. P:2017–2039 defines ten general and four attachment-only checks: description, MIME and enabled-rule absence are warnings; other unsuccessful predicates are failures. Default cardinality is at most one. Complete P save logic at P:1920–1948 has no check-result gate; its subsequent count refresh is not enforcement. S:1280–1315 validates name/code without an analogous readiness builder. No runtime invalid-save result is asserted. |
| **ADP-06** | ACCEPT | P:629–635,643–827 uses three mutation groups separately from `kind`; S:450–456,527–742 uses two Russian group labels and a separate kind selector. Complete P:2017–2039 emits status/title/detail objects, not stable check-code identities or reference rows. Its fourteen meanings correspond to the accepted WD-04 enumeration; the report correctly attributes the code names to wiki evidence rather than prototype objects. No FK, metadata binding or third collection is inferred. |
| **ADP-07** | ACCEPT | P:709–792 and S:592–626,679–715 confirm the specified classification differences and system attachment-rule samples. P:1746–1835 applies system guards to special-rule controls and shared update/toggle handlers. S:1202–1256 declares editable rule inputs and enabled toggles without a system restriction, connecting to S:1083–1101; deletion markup follows `allowDelete`. These observations do not choose classification, storage, migration or security policy. |
| **ADP-08** | ACCEPT | Complete P:2225–2242 confirms unconditional close confirmation, flag clearing and navigation without restoration. Direct breadcrumb/sidebar declarations at P:472,357 connect to unguarded navigation at P:1396–1407. P:1805–1867 directly modifies sample values; settings are read on save. Modal cancellation/backdrop/Escape declarations supply no draft comparison. S:383,1083–1157,1414–1428 confirms direct list navigation, immediate sample-value mutations and dirty clearing without confirmation. No actual loss, discard or persistence outcome was tested. |
| **ADP-09** | ACCEPT | P:1412–1431 and1915–1919 connects check-tab selection and active-tab dirty recomputation. P:1978–2053 reads the dictionary object, constructs status rows without field-navigation links and emphasizes only the checks tab. Settings inputs are not incorporated into that object until save. S:409–413,953–965 has values/settings/usage switching, not a check/error-tab mechanism. The report correctly avoids equating check-tab emphasis with cross-tab field highlighting or unsaved-settings synchronization. |
| **ADP-10** | ACCEPT | P:385 connects to P:2154–2220: six default fields, two optional fields, filtered selection, CSV quoting/BOM/Blob/anchor construction, then “Выгрузка сформирована”, “Файл готов”, download-folder hint and Close. P:491 is separately toast-only; P:2058–2078 exports values and ends with a toast. S:311,402 is toast-only for list/card headers; complete S:1387–1409 constructs value CSV, including ordinary-value color and attachment note, then a toast without a completion modal. Source-defined completion text is not evidence of successful delivery. |

## Documentary boundaries retained

The report correctly supplements rather than rewrites historical WD statements that both attachments were unread. Selected attachment evidence now exists, especially for list-export completion; whole-attachment semantic acceptance does not follow.

Wiki/Jira/journal comparisons remain explicitly attributed to corrected accepted WD evidence and its reviews. No challenged discrepancy required fresh extraction of primary wiki/Jira/journal passages in this review.

The following remain unresolved or outside acceptance:

- Complex-filter scope and requested future marking.
- Informational/system mutation policy and classification differences.
- Activation alternatives, active-default validation and approved readiness severity.
- Group/FK/metadata contracts, storage and accounting questions.
- Cross-form departure/error discoverability and actual discard semantics.
- Export failure handling, delivery guarantees and separate card payload.
- Frontend execution ownership and implementation readiness.

Existing DICT / MOS-1327 → MOS-1321/MOS-1399 routing is retained as documentary routing, not a new frontend assignment. Skill lifecycle qualifications and historical gates are unchanged. Source-defined contradictions are not application defects.

## Actual verification limits

Independently read, as inert text:

- **P:350–2253**, in contiguous bounded reads.
- **S:285–1436**, in contiguous bounded reads.
- Both complete attachment metadata files.
- The assigned work items, complete target report, corrected WD report and both WD reviews.
- Decisions lines **1–40**.

File-scoped searches additionally checked deferral wording, dirty-state references, and selected check/sort/type/mapping terms. Absence conclusions rely on complete relevant function bodies and their connected declarations, not isolated snippets. Search coverage does not constitute semantic acceptance of unread regions.

P:1–349 and S:1–284 were not semantically inspected beyond incidental search hits. No full attachment or application audit was performed.

Only local reads and grep occurred. No rendering, imports, evaluation, executable parsing, source execution, network/browser/MCP, linked asset loading, credentials/business requests, tests/build/E2E, repository edits or nested delegation occurred. No hashes, original download bytes, decoding fidelity or runtime reachability were independently verified.

This review accepts only the ten selected static findings. It authorizes no product policy, implementation, main-spec/archive change or global closure.