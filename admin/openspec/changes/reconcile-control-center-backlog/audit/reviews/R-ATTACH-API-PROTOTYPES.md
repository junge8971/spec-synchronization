# R-ATTACH-API-PROTOTYPES — independent inert-source review

## Review

**Decision: ACCEPT.**

No issues found.

- **Correct:** AAP-01–11 accurately distinguish static markup, defined handler effects, prototype data and unresolved product/backend requirements.
- **Fixed:** None; read-only review.
- **Per-ID exceptions:** None.
- **Minimum mandatory corrections:** None.
- **Merge verdict:** OK for this documentary report only. This is not feature acceptance, implementation approval, source precedence or global closure.

## Evidence convention

All paths are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

- **P:** `sources/wiki-attachment-250800526/r1/content.txt`
- **B:** `sources/wiki-attachment-247747361/r1/content.txt`
- **Report:** `reports/ATTACH-API-PROTOTYPES.md`

Both work-items, the report, accepted `reports/WIKI-API-REGISTRY.md`, `reviews/R-WIKI-API-REGISTRY.md`, and D-027 at `decisions.md:11–18` were read.

Both attachment metadata files were read completely. They identify P as version 2 and B as version 1, captured at `2026-10-19T09:15:22.006Z` and `.071Z`, respectively, with zero recorded redactions. The saved attachment index at `sources/wiki-247747363/r1/content.json:12–35` independently confirms the two version-qualified entries and `next: null`. Hashes and capture-method assertions were not independently recomputed or reproduced.

## Verification by finding

| ID | Result | Independently checked evidence and qualification |
|---|---|---|
| **AAP-01** | Accept | P:472–478 and B:1678–1683 define generic card actions. P:1680–1727 and B:4137–4176 initialize creation and open that same card. Connected creation helpers contain no creation-only action suppression in the inspected flow. This supports the reported source-level mismatch with accepted JR-02-13, not a demonstrated browser defect. Archive, Disable and soft delete remain distinct unresolved concepts. |
| **AAP-02** | Accept | P:688–693 contains four status values without `paused`; P:2026–2040 mutates draft status and repopulates the select without saving API_DATA or setting `deleted_at`. P:717 supplies raw-code fallback. B:1678–1683 calls only toast for Suspend/Disable; B:1752–1755,2010 contains four status labels. The toast helper at B:2749–2755 only updates notification presentation. Actual select state and persistence were not executed. |
| **AAP-03** | Accept | P:681–686,1782 uses source code `mppm`; targeted sample hits at P:842–870 distinguish that field from descriptive `mpmm` codes, paths and tags. B:3991–3996 maps МПММ to CSS class `mpmm`, not a wire source code. P:524–529,1762–1796 separates group/source draft updates from source-select rebuilding; P:1997–2025 saves draft without rereading source DOM. Thus the reported retained-draft-source path is supported textually. Neither inspected save validator enforces source compatibility or conditional requiredness. |
| **AAP-04** | Accept | P:711–715 defines `ms`/`pg`; P:728,752 uses those IDs. P:540–542,1741–1759 binds and populates `responsible_user_id`. B:1760–1763 uses a display-name select; targeted B:2017,2034 hits use `responsible` names. These are non-UUID examples versus the UUID prose attributed to accepted WAR evidence, not proof of valid external identities or live SUDIR/session integration. |
| **AAP-05** | Accept | P:1657–1678 copies data and assigns local child `_id` values. P:1870–1899 defines parameter array reordering; P:1997–2025 maps selected child fields, omits child identity/order fields, and writes a deep copy into local API_DATA. B:4097–4135 copies children; B:4196–4205 validates and only toasts. B:4242–4281,4383–4434 connects parameter rendering to shared array-splice drag behavior. Fully inspected response functions contain no response-reorder handler. None of this satisfies or withdraws the accepted atomic backend card+children save requirement, including existing IDs and both orders. |
| **AAP-06** | Accept | P:1706–1711 and B:4140–4144 seed 200/400 during creation. P:1941–1948 and B:4346–4353 append one 200 per Add action. Connected response render/update functions and save validators contain no response-code uniqueness check. The creation-versus-Add distinction and possible duplicate local codes are supported without inferring backend behavior. |
| **AAP-07** | Accept | P:2045–2061 defines unconditional close confirmation and confirmed draft clearing. P:457,1470–1481 and B:1665,2706–2732 define direct breadcrumb navigation without that guard. P:1486–1500 and B:2859–2873 toggle panels only. P:1984–2004 and B:4178–4205 mark name/code wrappers and toast without explicitly revealing another tab; empty path has no corresponding wrapper error in these handlers. P inputs update draft, while B inputs invoke uniqueness validation. These are bounded textual omissions, not demonstrated recovery or departure behavior. |
| **AAP-08** | Accept | P:2067–2124 and B:4483–4495,4545–4602 define API export selection and completion states. Both complete `doExport` bodies reject empty selection and otherwise replace modal text; neither contains data serialization, file production/download or an export request. Completion wording is not generation evidence. Dictionary-only JR-02-06 is not transferred to API. |
| **AAP-09** | Accept | P:984 initializes `savedFilters.api` as an empty array; P:1298–1385 defines named local save, replacement, application, deletion and incomplete link serialization. B:2635–2659 defines prompt/toast-only named save and links containing search, method selection and condition count, not predicates/source/status. Both clipboard calls are unawaited. Inspected initialization contains no query hydration; exact storage/query-symbol searches were negative, without proving universal absence of alternative mechanisms. |
| **AAP-10** | Accept | P:1552–1562 and B:4011–4021 count all API_DATA independently of list filtering. P:1579–1638 and B:4037–4094 calculate separate filtered totals, use the two-character search threshold across name/code/path/description, and compose group/source sort values. P:936–963 contains nine advanced-filter fields including landing category; B:2222–2232 uses label-valued API enum fields. Server counts, transport encoding and exhaustive filter semantics remain unverified. |
| **AAP-11** | Accept | P:724–746 contains descriptor/sample fields and manual request text; P:548–574 binds publication/auth configuration. B:1770–1778 provides corresponding static controls. These are not executed requests, session principals, permission contracts or evidence of landing generation. Model/PDF, DTO, database and backend conformance remain outside this evidence. |

All affected WAR/JR/MR references retain the report’s existing **MOS-1403 → MOS-1386 requirements/backend-document routing**. No frontend assignment is inferred.

## Actual inspection coverage

### Fully read selected text ranges

- **P:** 455–758, 936–988, 1000–1013, 1298–1387, 1460–2169.
- **B:** 1663–1787, 2006–2010, 2222–2232, 2615–2734, 2744–2759, 2855–2879, 3989–4435, 4483–4496, 4542–4631.

Shared functions were assessed only for API-connected behavior. Unrelated branches, declarations or initialization calls incidentally returned by these reads were excluded from assessment.

### Targeted searches

File-scoped searches checked source spelling, responsible-user samples, API creation/save call sites, relevant state references, filter-link wiring and helper definitions. Searches for `beforeunload`, `localStorage`, `sessionStorage` and `location.search` returned no matches in either attachment. Returned searches were not capped.

These negative results support only the specified symbol-search boundary. They do not establish universal absence of navigation guards, persistence or hydration by every possible mechanism.

## Inspection limits

- This was selective API-only source inspection, not whole-attachment acceptance. Remaining styling, shell/list markup, sample records and intermediate filtering helpers were not comprehensively reviewed.
- Primary Jira, journal and API-page prose were not independently reread. Their requirements and comparisons remain attributed to accepted WAR report/review and D-027.
- No rendering, imports, evaluation, source execution, asset loading, URL navigation, network access, credentials, business calls, tests/build/E2E, application audit, direct edits or nested delegation occurred.
- No repository diff/index inspection or hash recomputation occurred.
- Textual wiring does not prove runtime reachability, browser selection behavior, clipboard success, error recovery, persistence, export generation or backend correctness.
- Attachment versions and filenames establish neither replacement nor source precedence. Permissions/session policy, frontend ownership, product choices and global closure remain unassigned and unresolved.