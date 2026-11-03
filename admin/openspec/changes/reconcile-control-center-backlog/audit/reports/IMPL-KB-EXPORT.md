# KB-EXPORT bounded implementation audit

## Result and authority
HEAD verified before/after: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Current local inputs, not historical equality. Read complete main export/module specs and archive proposal/design/tasks plus export/module deltas. Reused accepted documentary report `DELTA-KNOWLEDGE-BASE-ROOT-DOC.md`, KBROOT-07, and ACCEPT review; no source re-extraction or attachment inspection.

KBROOT-07 anchors captured functional §§3.6/4.1/6.2 (S:42,54,128–131), model usage S:205: field/section choice and export modal, not file-delivery evidence. Current `openspec/specs/knowledge-base-export/spec.md`:9–44 and archive design §7 own CSV/full selection/saved-only/unavailable nested export. Existing archived tasks 9.1–9.3 already own implementation and tests; no new capability or duplicated task warranted.

## Scenario → mounted code → mock/transport → written tests
Paths abbreviated K=`app/optional/knowledge-base`, M=`mocks/knowledge-base`.

| Scenario/spec | Mounted implementation and transport | Mock / written, unexecuted tests |
|---|---|---|
| Full applied selection, field order, empty selection; export spec:9–19 | `K/ui/knowledge-base-registry.tsx:75` mounts list target with `search`, metadata. `K/ui/export/knowledge-base-export-form.tsx:21–57` intersects metadata fields, retains selection; `K/handlers/export.handlers.ts:5–21` appends in selection order and blocks empty/pending submit. `K/api/knowledge-base-export-client.ts:52–63` POSTs fields plus parsed search, including pagination, not loaded rows. | `M/handlers.mjs:45–61,117–120` searches entire collection without page(); `mocks/managed-search.mjs:67` ignores limit/offset as filters. `K/ui/export/knowledge-base-export.test.tsx:55–91,115–131` checks later-page payload/order/empty blocking; `M/search-export.test.mjs`, test “KB CSV uses BOM…” checks both selected rows despite limit=1/offset=1; numeric whole-CSV test checks same applied conditions. |
| Saved-only detail/new/dirty/nested; export spec:21–35 | `K/ui/editor/editor-header.tsx:70–74` passes snapshot ID, dirty and pending to editor export; wrapper `K/ui/export/knowledge-base-editor-export.tsx:15–23` mounts export and metadata retry. `K/model/export-availability.ts:8–10` disables new card. Heading:16–19 warns saved-only; form:50 and `unavailable-export-sections.tsx:8–27` expose disabled sections with linked permanent explanations. Constants:12–20 distinguish flat skill_names from relationships. Client:65–76 sends ID and fields only. | `M/handlers.mjs:83–87,107` exports persisted entry or 404. Component test:93–113 validates dirty warning/disabled accessible sections/flat skills and fields-only body. Mock CSV test rejects nested fields and detail search payload; detail contains only chosen entry. |
| Truthful delivery, safe name, error/pending/session; export spec:37–44; module unsupported/access boundaries | Client:28–50 validates CSV UTF-8 content-type, attachment filename, BOM and non-JSON content, attaches response session. Shared `http-client.ts:143–182` uses existing protected binary request/error/session transport; no new auth. `shared/api/file-response.ts:3–13` sanitizes control/slash filename characters. `K/model/use-knowledge-base-export.ts:14–55` disables retry, guards pending/owner, aborts on unmount, checks response session, creates/revokes object URL. Shared `download-attachment.ts:1–11` removes link in finally. `K/ui/knowledge-base-export.tsx:24–59` displays error versus browser-handoff status, blocks closing during pending. | Client test “exports full applied selection…” checks sanitized filename; second test rejects empty/duplicate/JSON responses. Component tests:133–221 check HTTP failure, retained selection, download throw/resource cleanup, duplicate clicks, former owner and unmount. These are written tests, not execution evidence; browser handoff does not prove disk persistence. |
| Limit exceeded; export spec:16–19 | Heading:12–14 shows metadata row maximum; UI:56 displays raw mutation.error.message. No local export-limit explanatory mapping observed in this chain. | `mocks/managed-search.mjs:94–101` returns 422 `EXPORT_LIMIT_EXCEEDED`, message `Mock export exceeds 10000 rows`; mock CSV test asserts code/no attachment for 10001 rows. Component test:133–155 instead injects 413/500 with message “Сузьте отбор”. See bounded discrepancy below. |

Saved API evidence: `docs/api/contracts/managed-resources.openapi.json:1310–1413` declares the two KB POST export operations, UUID detail parameter, CSV binary success, request schema references and existing token security. This is a saved contract, not a live service check or exhaustive DTO audit. Shared transport is reused rather than generic report/dialog/skill export substituted. Export implementation stays inside optional KB and imports shared/public session APIs; server mock stays separate. Global routing, production bundling, removal and backend authorization enforcement were not re-audited.

## Necessary correction / no-op
**One narrow existing-requirement discrepancy:** full-selection limit scenario requires an explicit suggestion to narrow selection. The actual connected mock returns only an English limit statement; the UI renders it verbatim, while its component test supplies the missing advice artificially and uses statuses other than the actual 422 mock response. Header states the maximum but does not suggest narrowing. Record this as a residual correction under existing export scenario/task 9.1, not a new export capability or reopening completed archive checkboxes. Parent may track a focused active delta referencing this existing requirement: surface the limit-specific narrowing advice and cover the real 422 `EXPORT_LIMIT_EXCEEDED` envelope. Do not reinterpret all 422 validation errors as size errors or change backend policy. Existing no-file-on-error handling is present.

Otherwise **planning no-op** for list/detail/file-lifecycle ownership: main spec and archived tasks already cover the observed implementation and written tests. No nested export endpoint, activation gate, new permissions, import/publication workflow or deployment completion should be inferred.

## Integrity (current local SHA-256)
- common work-item `openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-OPTIONAL-DOMAINS-SEVEN.md`: `9720c147622d55b007071126202799405226f607c8935d431761f980c476e89a`
- main export spec: `87733e1890d135f29ef5629b8e1b2a3735e4f8fa3e8c9fdbad995a491c400973`
- main module spec: `7e9d5498dd603b9ef5e7b241f81857dc767c3532009fa68ede116f4e496809f0`
- accepted report (audit/reports/DELTA-KNOWLEDGE-BASE-ROOT-DOC.md): `7e3c4896fab81b800821506eca17cffacc0009408f288b6a035dfc3c69c049ad`
- accepted review (audit/reviews/R-DELTA-KNOWLEDGE-BASE-ROOT-DOC.md): `5be777bdc3e3f4e13d5dec27b6e621a795cc796c5388b0977726037f4e8b4eb3`
- archive `2026-10-14-add-optional-knowledge-base/proposal.md`: `2ad551556756d7a32617702fba28b14302f5212546d96e66291f7d993b63e095`
- archive design.md: `76110bb2afca215e8404fcd00c81c1ddc9f0c29caddef3af07a0a833beff2667`
- archive tasks.md: `8da528d3d8cc27463bfea88b49dcb002aa07f2969bb0721531c5178045097e6d`
- archive export delta: `bf212f9c9d3c1b0801be80fc63f7b08c5f47edbaf294188f6b11980819ed6b62`
- archive module delta: `1aaad0aad54ba9222a4198a1aaf009a39aa4e6ea57c43d19facc5ebb3b3a8dd1`
- saved managed-resources.openapi.json: `cc4cb5603b449f0d7a98224bfcfc1795f509ecc09a3155fdc87f8ff2b270c7cf`

## Limits
No project writes, network/browser, tests/build/typegen, credentials, commits or nested agents. Registry/editor inspected only at export mounting seam; mixed mock test file read but no other-lane conclusions extracted. No raw accepted source rereading. No historical Git comparison of ignored OpenSpec. No feature-completion/deployment inference. Staged-name query was empty; working-tree cleanliness not asserted. Only configured external report written.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Source-backed export scenario/code/transport/mock/written-test mapping, local input hashes and one bounded existing-requirement correction recorded."}],
  "changedFiles": [],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"git rev-parse HEAD (before/after)","result":"passed","summary":"Expected bc0d9800f25a90989b9c73c76f91996f8300f1d3"},{"command":"sha256sum scoped local spec/report/archive/API inputs","result":"passed","summary":"Hashes recorded above"},{"command":"git diff --cached --name-only","result":"passed","summary":"Empty"}],
  "validationOutput": ["Read-only static inspection; all tests referenced are written and unexecuted."],
  "residualRisks": ["Actual browser download, live API and deployment unverified.","Actual 422 mock limit message lacks required narrowing suggestion; component test injects advice rather than covers real envelope.","No whole-module architecture or independent accepted-source extraction audit."],
  "noStagedFiles": true,
  "diffSummary": "No project changes; configured external report only.",
  "reviewFindings": ["Existing export task 9.1 owns limit advice discrepancy; no duplicated feature backlog needed."],
  "manualNotes": "Complete owning specs and relevant archive planning artifacts read. Accepted documentary report/review reused. Global and feature checkboxes unchanged."
}
```
