# KB-REGISTRY — bounded implementation audit

## Result / authority

**Planning disposition: no-op.** No necessary new registry requirement or duplicate implementation task established in the inspected paths. Preserve current registry spec, archived history and all task checkboxes. This is static traceability, not feature completion or deployment approval.

Verified HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Tracked working and staged diffs were empty. OpenSpec inputs below are current local bytes, not Git-history equality claims.

Read complete current `knowledge-base-registry/spec.md` and `knowledge-base-module/spec.md`, accepted `DELTA-KNOWLEDGE-BASE-ROOT-DOC.md` and its ACCEPT review. Used their KBROOT-01 source extraction (root functional §§3.1–3.6, captured lines 11–42; model lines 193–205) without re-extracting source or attachments. Read complete proposal/design/tasks of archived `2026-10-14-add-optional-knowledge-base` and `2026-10-15-update-control-center-api-contracts`. The latter’s design decision 4 and tasks 4.1–4.4 own the numeric/skill-name extension; do not restore the earlier archive’s unsupported-condition labels or rewrite its tasks 3.4/5.2 retrospectively.

## Scenario → mounted code → transport/mock → written tests → owner

Paths below are repository-relative; `K` = `app/optional/knowledge-base`, `M` = `mocks/knowledge-base`. Symbol names are exact locators.

| Scenario / requirement | Mounted implementation and transport/mock | Written, unexecuted evidence / planning owner |
|---|---|---|
| Ordinary registry registration; removable ownership; existing access | `app/application/constants/application-routes.constants.ts:3–6` composes public `knowledgeBaseRoutes` unconditionally. `K/constants/descriptor.constants.ts:14–35` defines registry/new/detail and Content navigation; `K/routes/registry.tsx:1–5` mounts `KnowledgeBaseRegistry`. `K/model/knowledge-base-queries.ts`, `useKnowledgeBaseEntriesQuery`, metadata/lookups hooks retain `usePermissions('*')`, AbortSignal and owner checks before/after reads. `use-knowledge-base-registry.ts` uses public entity skill catalog, not another optional module. | Module spec “Default section inclusion”, “Removable module ownership”, “Shell integration”; original archive tasks 1.1–1.4, 10.1–10.2 already own registration/access/build evidence. Build graph and whole-shell access were not revalidated here. |
| Server columns, multi-filters, search threshold, sort/pagination and total | `K/ui/knowledge-base-registry.tsx` mounts Filters/Conditions/SavedFilters/Results. `registry-filters.tsx` applies trimmed ≥2-character query and category/status selection with offset 0. `registry-results.tsx` uses server `pagination.total_items`; `registry-table.tsx` displays material/code/category/skill-ID-derived names/count/status as text and real Links. No comma splitting to recover skill identities. `K/api/knowledge-base-client.ts:36–46` POSTs validated search through shared `apiRequest`. `M/handlers.mjs`, `search` and `list_kb_entry` apply `searchManaged` before `page`. | `K/ui/registry/registry.test.tsx:94–225` contains assertions for combined filters from page two, total 43, safe text, ID-bound comma-containing skill names, keyboard navigation under basename, 0/1/2 characters, sort cycle back to `-updated_at`, and history. `M/search-export.test.mjs:6–106` search-specific tests assert AND/OR, case-sensitive equality, sorting and pagination. Current registry “Server-owned registry selection”; original tasks 4.1–4.3. |
| Draft/applied conditions; numeric and skill-name semantics | `K/ui/registry/registry-conditions-draft.tsx`, `RegistryConditionsDraft`, holds separate draft, AND/OR, add/delete/clear/cancel and 50-row limit; Apply calls `validateRegistrySearch`. `K/api/knowledge-base-search-schema.ts` validates finite numeric thresholds, ordered two-number ranges and ≤50 items, rejects numeric text/boolean/null. `K/model/registry-search.ts`, `validateRegistryCondition`, checks metadata operators/type and unsupported archive. `M/model.mjs:29–46` publishes numeric links_count operators; `entryResponse:63–77` resolves skill_names from nondeleted linked skills. | `registry-conditions.test.tsx:26,52,67,95,114` written cases cover cancel, invalid rows, empty enums, 51st row and blank numeric range. `registry-search.test.ts:193` covers metadata type/operator confirmation. `M/search-export.test.mjs:238–317,320–346` contains typed-boundary and current/nondeleted skill-name cases (export assertions not audited). Registry “Metadata-driven supported conditions” and “Unsupported prototype conditions”; contract-update tasks 4.1–4.4 already own these. |
| URL sharing, malformed selection, Back/Forward | `registry-search.ts`, `decodeRegistrySearch` rejects unknown/duplicate URL keys, malformed/oversized JSON and invalid complete search; `encodeRegistrySearch` preserves JSON types. `use-knowledge-base-registry.ts` disables entries query absent valid search. Mounted registry exposes explicit reset; filters use location/navigation type to restore applied query on POP. Copy action passes current full `window.location.href` to existing handler. | `registry.test.tsx:200–230` assertions preserve numeric OR group across history and assert zero search calls for malformed URL. `registry-search.test.ts:33,107,115,132` has round-trip, size/50-condition and clipboard/basename cases; clipboard handler test was located, not executed. Registry “URL selection round trip”; original task 5.3 and contract-update task 4.3. |
| Persistent saved filters; confirmation/errors and pagination | `K/ui/registry/registry-saved-filters.tsx` applies full validated stored search, leaves invalid entries deletable and paginates server results. `use-knowledge-base-registry-saved-filters.ts` uses limit 20/offset; clears input/invalidate only after successful create, no optimistic deletion, no mutation retry and checks session ownership. `K/api/knowledge-base-directory-client.ts:34–42,58–103` preserves raw saved search until Apply, validates name 1–150/nonblank, resource and ID, and uses shared transport. | `registry-saved-filters.test.tsx:82,106,127,148,174` written cases cover remount, separate equal-name IDs, later-page application preserving offset, failed delete/create, invalid persisted filter and numeric range types. `M/search-export.test.mjs:108–158` contains saved-search validation/replacement/pagination/equal-name tests. Registry “Persistent saved filters”; original task 5.4 and contract-update tasks 4.3–4.4. |
| Truthful loading/error/empty and unsupported archive | `registry-results.tsx` separates loading, errors with retry, no matches and no records; skill lookup failures display IDs with retry, not fixtures. `registry-table.tsx` preserves unknown codes and disabled status. Current selection validator disallows archived requests rather than translating to disabled/DELETE. | `registry.test.tsx:78,120,126,232–255` contains read compatibility, loading, archive disabled label, error retry and empty/no-match assertions. Module “Unsupported features remain visible and truthful”, “Accessible states”; original tasks 4.1–4.3. No new archive task or policy inferred. |

The registry passes full applied search to its export target (`K/ui/knowledge-base-registry.tsx`), but export implementation/CSV/download correctness belongs exclusively to KB-EXPORT and was not assessed. Editor internals and mutation semantics were not assessed.

## Necessary correction / limits

- No active delta justified by this bounded static comparison. Existing tasks already own registry scenarios; accepted KBROOT-01 remains traceability rather than new work.
- Keep documentary search breadth distinction: mounted placeholder says name/code/description/tags, mock search additionally includes category and skill names (`M/handlers.mjs:45–61`). Accepted source and approved API adaptation are not identical descriptions; no local filtering or policy replacement is warranted. Real search breadth is unverified.
- Contract-facing client implementation and contract-derived mock metadata are not proof of deployed backend support. No independent full saved OpenAPI audit was performed.
- Test titles/selected assertion bodies were inspected, not all test bodies or shared managed evaluator/transport internals. Numeric NULL/ne behavior is owned by current spec/update tasks but was not independently traced through the shared evaluator here. No global architecture/session re-audit, source re-extraction, network, browser, credentials, tests, build or nested agents. Production graph and actual accessibility interaction remain unverified.

## Current local SHA-256 input record

`openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-OPTIONAL-DOMAINS-SEVEN.md`
`9720c147622d55b007071126202799405226f607c8935d431761f980c476e89a`

`openspec/specs/knowledge-base-registry/spec.md`
`909cde42dadfff0bad8caa5a75e09c01f5b3c538b6c2033c8cfe2d4a6b1f1733`

`openspec/specs/knowledge-base-module/spec.md`
`7e9d5498dd603b9ef5e7b241f81857dc767c3532009fa68ede116f4e496809f0`

`openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-KNOWLEDGE-BASE-ROOT-DOC.md`
`7e3c4896fab81b800821506eca17cffacc0009408f288b6a035dfc3c69c049ad`

`openspec/changes/reconcile-control-center-backlog/audit/reviews/R-DELTA-KNOWLEDGE-BASE-ROOT-DOC.md`
`5be777bdc3e3f4e13d5dec27b6e621a795cc796c5388b0977726037f4e8b4eb3`

Under `openspec/changes/archive/2026-10-14-add-optional-knowledge-base/`:
- `proposal.md`: `2ad551556756d7a32617702fba28b14302f5212546d96e66291f7d993b63e095`
- `design.md`: `76110bb2afca215e8404fcd00c81c1ddc9f0c29caddef3af07a0a833beff2667`
- `tasks.md`: `8da528d3d8cc27463bfea88b49dcb002aa07f2969bb0721531c5178045097e6d`

Under `openspec/changes/archive/2026-10-15-update-control-center-api-contracts/`:
- `proposal.md`: `6ece6e82490038d5ce491f19acf089c10a27dc845f74c2cf035ac37826c13bd8`
- `design.md`: `58f8cdbd387508c10285387b3fcdbf208bfdb73559a8243997af676e38df6156`
- `tasks.md`: `6002750f35319a52ce0c9fcd50731385ada811844c6edc3499943d87051dd478`

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Registry-only scenario/code/client/mock/written-test/spec/task mapping with current HEAD and eleven local input hashes; no-op recommendation and explicit limits."}],
  "changedFiles": [],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD","result":"passed","summary":"Matches assigned bc0d9800f25a90989b9c73c76f91996f8300f1d3."},
    {"command":"sha256sum scoped OpenSpec inputs","result":"passed","summary":"Eleven current local hashes recorded."},
    {"command":"git diff --name-only; git diff --cached --name-only","result":"passed","summary":"Both empty."},
    {"command":"tests/build/browser/network","result":"not-run","summary":"Prohibited by audit contract."}
  ],
  "validationOutput": ["Read-only static mapping; test results and deployment are not attested."],
  "residualRisks": ["Shared evaluator/transport, full shell/build graph and live backend not independently verified.","Only selected test assertions inspected; no tests executed.","Search documentary/API breadth difference retained without selecting new policy."],
  "noStagedFiles": true,
  "diffSummary": "No project edits; only configured external report written.",
  "reviewFindings": ["No necessary new registry planning delta established in inspected paths."],
  "manualNotes": "Accepted source extraction reused; editor/export and other lanes excluded. Existing checkboxes unchanged. OpenSpec hashes attest current local bytes only."
}
```
