# Code Context

## Result and boundary

Bounded documentary supplement, pending independent review. The two newly read historical bodies add a **22-field example, a different 18-field catalog, and template/run storage descriptions**. They do not replace the accepted 24-column MOS-1015 gates, approve an endpoint, establish delivery, or authorize scheduling/export. Existing report owner plans exist; absent main report specifications must not be described as absent planning.

## Files Retrieved

Repository-relative paths; `A` = `openspec/changes/reconcile-control-center-backlog/audit`. E/B below are exact versioned files, not current API references.

- **E**: `A/sources/wiki-238350232-readable/r1/content.txt:1–194`, complete; `body-view-chunks.json:1–10`, complete ordered array, including markup of the blank validation-status cell. Parent source `A/sources/wiki-238350232/r1/metadata.json:1–21` and readable metadata `:1–14`, complete. Page **v33, 2026-09-08T17:41:24.374+08:00**.
- **B**: `A/sources/wiki-241080082-readable/r1/content.txt:1–147`, complete; `body-view-chunks.json:1–9`, complete ordered array. Parent source `A/sources/wiki-241080082/r1/metadata.json:1–21` and readable metadata `:1–14`, complete. Page **v4, 2026-10-01T14:50:18.120+08:00**.
- `A/reports/SCENARIO-MOS-1015.md:1–134`, `A/reviews/R-SCENARIO-MOS-1015.md:1–128`, complete; `A/decisions.md:171–183`, **D-013**, accepted qualifications for this reconciliation.
- `A/inventory.json:377–400,622–643`: four existing change owners. `A/reports/JIRA-MOS-777.md:1–46`: membership only, not description/delivery evidence.
- `A/sources/jira-reports-details/r1/content.json:32–135`, `/items/1..5`: MOS-885/916/919/1015/1016 saved full descriptions/statuses; complete metadata. Located this later increment rather than repeating the older membership report's missing-description limitation. Parent item returned by the read is not used as semantic evidence.
- `openspec/changes/mos-1015-report-constructor/design.md:1–100`, especially B15.1–5 at 90–96.
- `openspec/changes/mos-916-report-templates/design.md:1–74`, especially B916.1–5 at 68–72.
- `openspec/changes/mos-919-report-csv-export/design.md:1–65`, especially B919.1–4 at 60–63.
- `openspec/changes/mos-1016-report-template-scheduling/design.md:1–76`, especially B16.1–5 at 70–74.

Both new metadata records report HTTP 200; separately returned empty attachment indexes are attributed to the work item/parent collection, not independently inspected. Parent content hashes: E `b8dc721f25661837e30611e9657986c828bb2f476d2f80a20a571a269929b3e8`; B `8db9a07f2633aa32feef56ba59e9dcaf205bdb1b663e66cffc67dde51ed6d08f`. Hashes and readable-body roundtrip were **not recomputed**. Chunk markup was read inertly, never rendered/executed. Initial combined output was truncated; omitted beginnings were subsequently read separately.

## Key Code / stable documentary findings

No application code inspected. E/B locators refer to the exact text files above; corresponding HTML tables/keys in the complete chunks preserve cell boundaries.

### RRD-01 — Selection is source-specific, not an agreed DTO

**E:1–18,89–96**, request table: one exported record per dialog with all selected fields, formed on demand at manual/scheduled launch; inclusive `periodStart`/`periodEnd`, `channelId:null` = all channels, `fields` from 22 fields. The heading combines `POST /api/esk/{method_name}` and `POST /api/esk/report`; this is expressly an example, not a current method requirement. This request defines no advanced-condition structure, all-time mode, timezone, pagination or field-order rule.

**B:25–39,78–99,144–146** supplies arbitrary dates/all-or-specific channel and template `field_codes:string[]` explicitly ordered for preview/CSV. Nullable JSONB/object `filters` is not a typed advanced-selection contract. `channel_id:null` means all **available** channels. Presets: today/last_7_days/last_30_days/previous_month/custom, with custom-only date bounds. Scheduler timezone is not report-date timezone. These supplement existing B15.2/B919.1/B16.2–3; they do not settle all-time, calendar clock, particular-skill phrase scope or advanced DTO gates. Document-local omissions do not mean absent owner plans.

### RRD-02 — Four catalogs remain distinguishable

**E:96,103–194** has exactly 22 numbered rows; both 200 sample items contain those 22 keys. **B:27** says “20+”, but **B:100–119 has 18 API-code rows**. The accepted chain concerns a third catalog, wiki241085838 v3's 18 fields, against the 24-column owner UI. Counts alone do not identify equivalent contracts.

E ordered catalog: `chatId, sessionId, ssoId, authFlag, channel, participants, startedAt, finishedAt, fullDialog, userText, operatorText, duration, stepsCount, endReason, endedBy, skillScores, operatorScore, scoreComment, lowScoreReason, categories, errorType, widgetButton`.

B catalog: `chat_id, session_id, sso_id, communication_channel, request_datetime, full_dialog, user_text, operator_text, completion_time, completion_reason, bot_duration, completed_by, operator_consultation_rating, rating_comment, low_response_rating_reason, topic_and_categories, error_type_and_target_answer, widget_button`.

E documents four concepts absent from B and accepted report-v3 catalogs: authorization, participants, steps and assistant ratings. **Neither new table supplies attachments or attachments-to-operator**, still required by the 24-column UI. This supplements, not overturns, D-013's six-absent-rows finding about its named v3 catalog. The 22-field example does not close the 24-field mapping gate.

B codes are not automatic aliases for accepted v3 `channel`, `started_at`, `dialog_transcript`, `ended_at`, `operator_rating`, `topic_categories`. E `duration` labels full dialog duration; B `bot_duration` labels robot time. E `categories` versus B `topic_and_categories` differs in scope. Generic E `lowScoreReason`/`scoreComment` do not establish operator ownership; B explicitly labels low response rating reason. B15.1 semantic/type/null/display reconciliation remains, without approved renames.

### RRD-03 — Samples expose unresolved presentation

**E:27–78** repeats the same chat/session and all values in two items despite one-dialog-per-record prose at E:2. This is sample duplication, not authority to duplicate records or runtime evidence. `stepsCount`/`operatorScore` are quoted strings; examples do not approve types.

**E rows8–11/18, lines125–148,170–172**: finish precision differs (UI minutes/file seconds); full-dialog UI is “9 messages” versus transcript; user text is truncated versus full; operator text is “present” versus full; comment is dash in UI but populated in file/sample. **E:98–102** wants synonymous report/interface names while acknowledging differences and pending edits for fields9–11. Their notes explicitly await changes. Rows16/19/21/22 defer unknown formats to available data, not defined assistant-rating arrays, low-reason text, error/target shape or widget shape. B15.1/B15.4/B919.2–3 already own fidelity. New precision for that owner: resolve these exact representations and duplicated sample, not adopt example serialization.

### RRD-04 — Export, null and errors remain bounded

**B:29–32,37–39** requires CSV, preview/full row counts, no-data messages and error/retry. **E:81–88**, Responses table: `error_type/error_message`; validation status cell is blank, not justified 400/422; internal error explicitly has 500. Success is JSON `items`, not CSV bytes/file response. Neither body defines BOM/delimiter/filename/CORS or exhaustive JSON missing-value rules. E's sample dashes are not empty-CSV policy.

Preserve D-013's correction: accepted wiki241085838 §1.2 already defines empty CSV strings for missing values; §1.5 demonstrates `operator_rating:null`; exhaustive 24-field conversions remain open. MOS-919 B919.1–4 already preserve whole-selection, one record/dialog, server bytes, UTF-8 BOM/`;`, ordered fields, zero distinct from null, quoting/newlines and rejecting JSON/HTML errors as files. Existing coverage is not a new gap. Dialog-export message rows/selected IDs/trailing parameters and its separately published headers/formula rules are **not** imported by analogy.

### RRD-05 — Preview and performance are comparison points

**B:31–32** says first 10–20 rows; **B:38–39** requires report row count; **B:51–53** gives historical targets: 1000 dialogs within 5 seconds, preview within 2 seconds, export up to 10,000 rows. Accepted twelve-row preview fits 10–20: not an incompatible count by itself. Neither new body resolves five-selected-columns versus all-columns or whole-selection metric formulas/denominators. B15.3–5/B919.1 retain these gates. Numbers are documentary targets, not current caps, measurements or authorization to impose limits.

### RRD-06 — Launch wording differs; ownership exists

**B:21–24,62–70** describes “Launch” generating/downloading, but also opening a template in the constructor. **E:2** describes generation on manual/scheduled launch. Saved MOS-916 `/items/2/description` and B916.3 make launch/open transfer parameters, not execute or update last-run; selected-template-ID export is separate (B916.4). Preserve this wording disagreement for the existing owner, not a new combined action. Never-run `last_run:null` remains distinct from a real zero-row run. Five historical template names (B:35) do not authorize fixtures or establish delivered catalog content.

### RRD-07 — Tables supplement lifecycle, not scheduler API

**B report_templates:69–99**: UUID identity/creator; UTC creation/update/nullable soft deletion; name/nullable description; `schedule_type_id:UUID`; manual/cron prose; manual-null/cron-required configuration; five-part cron/timezone example; presets, ordered fields and nullable filters. Dictionary heading calls it `schedule_type`, not table `schedule_type_id`; mapping is unstated. No write method, uniqueness, ownership rights or relative-period evaluation algorithm follows.

**B reports:120–147**: template FK; `status_id:UUID` versus dictionary heading `status` (pending/running/ready/failed); nullable requester explicitly null for automatic runs; UTC request/start/completion times; actual date bounds; parameter snapshot; nullable file key/size/rows/error; service-generated download URL from `file_key`. Run timestamps are not dialog timestamps. Null automatic requester does not permit a fabricated user; nullable rows is not zero. Snapshot contains channel/ordered fields/filters; dates are separate run fields. Template FK does not explain standalone-constructor persistence.

New details route into existing B16.1–5/B916.2: storage-ID/DTO mapping, run-to-last-run/constructor relationships, relative periods and result access. They do not supply writes, polling, retry/cancel transitions, worker behavior, URL expiry/access policy or browser scheduling. E's “on the fly” generation and B's persisted statuses need relationship clarification, not assumed synchronous/asynchronous incompatibility or invented protocol.

### RRD-08 — Priority, privacy and backend boundaries

**B:34–60**: MUST CSV/preview/counts/five templates; SHOULD XLSX/save/daily-weekly schedules; COULD email/BI; WON'T edit data or visualize beyond tables. Phases put two templates in November MVP, additional templates/XLSX in December, save/schedule/email in 2027. Weekly quality-template naming versus later scheduling, and five MUST templates versus phased delivery, need interpretation—not automatic reprioritization of MOS-1016, deployment proof or new XLSX/email/BI scope.

**B:4,25,55–56** identifies audiences, authorized-user precondition, core-ESK data and role-limited access, not granular permission/private-shared ownership policy. **E:11–12,91–92** mandatory-but-anonymous-null `sudir_id/access_token` prose is historical documentation, not session change, credential instruction or access grant. `authFlag` is dialog data. B15 privacy retains in-memory drafts without identifiers/phrases in URL/storage/logs. Preserve accepted session/access boundary and historical 09.10 approval without reopening/extending it.

**MOS-885 `/items/1/description`** requests an isolated fake backend provider and excludes real-dialog retrieval. B's core-data aspiration does not establish current real integration; requested DoD/status is not delivery. That provider is separate from frontend demo fixtures. MOS-1015 Hold is not cancellation. No precedence follows from page versions/capture dates.

## Architecture

MOS-1015 owns constructor/selection/preview; MOS-919 report CSV; MOS-916 template navigation/opening/selected-template export; MOS-1016 save/schedule intent and future persistence; MOS-885 requested backend work. Accepted builder evidence establishes agreed semantics/ownership, **not reusable implementation existence/usability**. All integration gates remain; storage prose does not activate local-draft plans.

## Start Here

Read `openspec/changes/mos-1015-report-constructor/design.md:90–96` with D-013 and its review. Existing candidate routes are B15/B916/B919/B16, not missing plans. Newly precise questions concern catalogs/representations, sample duplication, launch wording, storage-ID mapping and run/result relationships. Any owner-plan update needs separate authorization; none performed.

## Validation and residual risks

Local file inspection only; complete new bodies/chunks read. No execution/rendering, network/browser/MCP, business calls/credentials, tests/build or application-code inspection. No raw attachment-index/hash/roundtrip revalidation, linked-page/prototype traversal, current API re-audit, main-spec/auth prerequisite reread or whole-module census. Prior API/auth conclusions are carried from accepted evidence, not renewed. Other report scenario/review bodies were not reread; D-013 and directly inspected owner designs bound their use. Index uninspected; no staged-files attestation. Only this report intentionally written; tool truncation automatically produced temporary inspection logs. Final line-count check corrected source-range citations.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Eight bounded findings reconcile complete historical bodies/chunks with owner plans and corrected MOS-1015 acceptance, using version/table/key/line locators."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/DELTA-REPORTS-ROOT-DOCS.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"Local read/find/grep and cat/nl/sed/wc inspections","result":"passed","summary":"Complete new bodies/chunks and scoped owner/acceptance evidence read; truncated beginnings recovered and citation line counts checked."},{"command":"Tests/build/browser/network/source execution","result":"not-run","summary":"Forbidden by assignment."}],
  "validationOutput": ["Documentary reconciliation only; no implementation/runtime/source-precedence/completion verdict."],
  "residualRisks": ["Independent review pending; hashes/roundtrip and attachment indexes parent-attributed.","Mappings, launch wording, lifecycle and ownership remain integration gates.","No runtime/current-API/implementation/index verification."],
  "diffSummary": "Only bound report intentionally written; no owner-plan/code edits.",
  "reviewFindings": ["No required-evidence blocker; accepted gates preserved."],
  "manualNotes": "Applied D-013 corrections: no index attestation, builder agreement not implementation, known CSV empty-value evidence retained. Historical catalogs do not supersede 24-column requirements."
}
```
