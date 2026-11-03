# R-WIKI-API-REGISTRY — independent documentary review

## Review

**Decision: ACCEPT.**

No issues found.

- **Correct:** WAR-01–12 preserve the distinction between explicit documentary inconsistencies, prototype/model scope differences, and unspecified contracts.
- **Fixed:** None; local read-only review.
- **Per-ID exceptions:** None.
- **Mandatory corrections:** None.
- **Merge verdict:** OK for this documentary report only—not implementation approval, source precedence, permission authority, or global closure.

## Evidence and coverage

Paths below are relative to `openspec/changes/reconcile-control-center-backlog/audit/`.

- **T:** `sources/wiki-247747363-readable/r1/content.txt`, read completely, lines 1–395 including trailing blank line.
- **H:** adjacent `body-view-chunks.json`, read completely in bounded ranges 1–7, 8–15, 16–23. Locators below are file lines, not chunk indexes.
- **C:** `sources/jira-MOS-1386/r1/content.json`, complete selected packet; `/description` at line 7.
- **J:** `sources/wiki-250781168/r1/content.json`, saved primary bodyView and bodyStorage read directly, including row 2 units 1–13 and row 5 physical-table-name discussion.
- Both work-items and `reports/WIKI-API-REGISTRY.md` read.
- Source/derivative metadata for the API page, Jira and journal read.
- API-page original attachment index read directly at `sources/wiki-247747363/r1/content.json:12–35`.

Versions verified from saved metadata:

| Source | Saved revision/version | Updated |
|---|---|---|
| API page 247747363 | r1 / v7 | `2026-10-14T15:38:39.099+08:00` |
| MOS-1386 | r1 | `2026-10-16T19:23:54.084+0800` |
| Journal 250781168 | r1 / v8 | `2026-10-08T18:31:40.254+08:00` |

Chronology does not establish precedence. Prior candidate references and routing are retained as context, not substituted for primary evidence.

## Independent verification by candidate

| ID | Result | Primary evidence and assessment |
|---|---|---|
| **WAR-01** | Accept | J `/bodyStorage`, `table/tbody/tr[3]/td[2]/div/ol/li[13]`, UUID `979b7b80-e137-4c6b-82cf-0b32e289e07f`, explicitly requests Save-only API creation and Disable/Suspend/Export/Save in the card. T:77,89–94; H:5–6 describe empty-card opening and generic card actions, not explicitly their visibility during creation. No proven creation-action contradiction. T:241 “выключение”, Archive at T:93, and C DoD 2 soft delete do not establish equivalent commands. |
| **WAR-02** | Accept | J row 2 units 11–12 explicitly concern departure from creation screens and errors hidden on another tab. T:13,94,170–186; H:3,6,10–11 provide local close confirmation, invalid-field highlighting and modal dismissal. They do not settle browser navigation/refresh, cross-tab discovery, dirty-state handling or preservation after failure. C “Что делаем” 8 requires understandable field errors without supplying those UI rules. |
| **WAR-03** | Accept | T:15–69; H:3–5 establish four UI tabs, three persisted groups, five sortable column groups, three-state sorting, two-character search and code-inclusive search. T:235; H:13 has a shorter search enumeration without code, not an exclusion. C “Что делаем” 5 and DoD 7 establish broader search/filter/sort/count intent. Counter scope, combined-column keys and transport remain unspecified. |
| **WAR-04** | Accept | T:49–78; H:4–5 substantiate multiselects, nine condition fields, AND/OR, eight text operators, enum inclusion/exclusion, chips/count and named-filter/URL actions. T:205–206,379–381; H:12,21 leave storage unconfirmed. C metadata/conditions requirements do not prove durable saved-filter storage or operator encodings. J row 2 units 2 and 7 remain dictionary-scoped and do not govern API conditions or approve widgets. |
| **WAR-05** | Accept | T:92; H:6 explicitly toggles `paused`/`active`. T:157,341–344; H:9,19 enumerate only `draft`, `active`, `deprecated`, `archived`; T:253; H:14 makes status a dictionary FK. This is an explicit intra-page inconsistency. The report correctly does not choose a fifth seed or reinterpret another status. |
| **WAR-06** | Accept | T:156; H:9 spells the static source code `mppm`; T:338; H:18 spells it `mpmm`. This is an explicit code disagreement. T:111–114,252; H:7,14 and C “Что делаем” 8 / DoD 5 support conditional source requiredness, not a contradiction with a generally nullable column. Reset/error behavior remains unspecified. |
| **WAR-07** | Accept | T:122–150,175–176,190–191,269–305; H:8–11,15–17 support flat children, order fields, parameter drag ordering, response preview and default response pair. C DoD 3 explicitly requires atomic card/parameters/responses saving with existing child identifiers and ordering preserved. Prototype draft arrays neither demonstrate nor contradict that backend intent. Response duplicate handling and reorder UI are appropriately left open. |
| **WAR-08** | Accept | T:99–106,177–182,244–267,297–305; H:6–7,10,14–17 separate shorter UI validation prose from model requiredness and uniqueness. C “Что делаем” 8 / DoD 4–5 additionally require relationship, JSON, source and uniqueness validation. T:208 describes prototype-only client validation; it does not withdraw backend requirements. Error paths and JSON/null-version details are not established. |
| **WAR-09** | Accept | T:107–108,162,198,208–211,254–255; H:7,10–12,14 distinguish string owner, unused `team_id`, external responsible-user reference, UUID model type and static prototype users. C DoD 6 specifies a string external-user identifier without local projection. UUID restricts the possible identifier format, but textual UUIDs can satisfy string serialization; the report correctly presents a format question rather than inevitable contradiction. No live SUDIR or app-session integration follows. |
| **WAR-10** | Accept | T:78,90,171,243; H:5–6,10,13 establish field/section selection modals. C “Что делаем” 6 / DoD 7 establish CSV list/card export. Neither settles completion/error protocol or nested serialization. J row 2 unit 6’s selection/completion-modal request belongs to the surrounding dictionary discussion and cannot be transferred to API; unit 13 separately supplies API action placement. |
| **WAR-11** | Accept | T:2–8,115–121,135,165–168,201–212,257–263,276,375–381 substantiate publication configuration, examples, business auth fields and prototype exclusions. C “Что делаем” 4 and its exclusion paragraph expressly distinguish stored configuration from landing generation, request execution, availability checks and call logs. Administrative labeling and C DoD 8 common access checking do not define permission mapping or authorize session changes. |
| **WAR-12** | Accept | T:306–394; H:17–22 explicitly list five main dictionaries plus separate `api_param_locations`, then three entity tables and six reference tables: nine total. No enumeration contradiction. J row 2 unit 10 and row 5 concern physical database table names only, not wire keys, routes, fields or FKs. The original attachment index confirms exactly two HTML entries, no PDF entry, and `next: null`; attachment/PDF conformance remains unverified. |

The journal row containing units 11–13 is explicitly **Открытый**. Acceptance of this report does not change that status or resolve its questions.

## Verification limits

- **Unread API-page body sections:** None within T and H.
- Reading the original API JSON body line directly hit the tool’s 50 KB single-line limit. Full body coverage was obtained through H, not by claiming the oversized original line was independently consumed.
- Hashes were **not recomputed**. The source SHA-256 `515b2c72850a30ea69de2dc412a03ea6e958c6bcc2aec7a73a3dd0e1f4e7cefe`, derivative hashes and chunk-to-source roundtrip remain **parent-computed metadata assertions**.
- Both HTML attachment bodies, embedded image/thumbnail content and referenced PDF remain unread. Only attachment metadata and embedded markup were inspected.
- Jira is a selected packet, not a full export. Hold status and comment `1131540` (“Готово, тестируем вместе с фронтендом”) are not passed-test evidence; automated mention `1131237` remains intentionally omitted.
- No application code, runtime, current API compatibility, frontend assignment or repository index state was audited.
- No edits, execution, network access, tests/build/E2E, prototype/cURL execution, credential use, linked-source traversal or nested delegation occurred.

**Acceptance is limited to the twelve documentary candidates and their stated qualifications.**