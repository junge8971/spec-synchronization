# R-DELTA-TEMPLATES-STUBS-ROOT-DOCS

## Review

**Disposition: REVISE — one citation correction only.** All twelve candidate dispositions are substantively supported. No ownership, implementation or scope correction is required.

- **Correct:** The report preserves response templates, stub library, module controls, skill commands, maintenance windows and report schedules as distinct domains.
- **Finding: P2:** TSROOT-07 cites P dictionary structure as **226–232**, but that range omits `code`, `display_name`, `description` and `sort_order`, and includes the following section heading/header. The actual dictionary structure is **220–230**.
- **Smallest mandatory correction:** In TSROOT-07 replace `Dictionary structure 226–232` with `Dictionary structure 220–230`. No other text needs changing.
- **Fixed:** None; review-only.
- **Merge verdict: OK with notes**, subject to that documentary locator correction. This is not implementation acceptance or global closure.

## Evidence inspected

Paths below are repository-relative. **A** means `openspec/changes/reconcile-control-center-backlog/audit/`.

- Complete assigned review work-item, original work-item and `A/reports/DELTA-TEMPLATES-STUBS-ROOT-DOCS.md`.
- **P:** `A/sources/wiki-247744768-readable/r1/content.txt:1–270`, complete; adjacent `body-view-chunks.json:1–18`, complete in two reads; adjacent derived metadata, complete. Parent `wiki-247744768/r1/metadata.json`, complete: page v5.
- **B:** `A/sources/wiki-241080097-readable/r1/content.txt:1–64`, complete; adjacent `body-view-chunks.json:1–6`, complete through closing bracket; adjacent derived metadata, complete. Parent `wiki-241080097/r1/metadata.json`, complete: page v1.
- `openspec/specs/skill-global-toggle/spec.md:1–94`, complete.
- `openspec/changes/archive/2026-10-13-mos-1027-skill-global-toggle/{proposal,design}.md`, both complete.
- `openspec/specs/control-center-mock-server/spec.md:137–201` and `openspec/specs/control-center-shell/spec.md:65–94`.
- Actual proposals for `mos-916-report-templates` and `mos-1016-report-template-scheduling`, both complete.
- `A/reports/JIRA-MOS-1388.md` and `A/reports/DELTA-SYSTEM-STATE-ROOT-DOCS.md`, complete; `A/decisions.md:1–12`, including D-037.
- Targeted inventory owner matches; actual MOS1388 hierarchy row and MOS1387 member-index record.

## Candidate verification

| Candidate | Result | Independently verified basis |
|---|---|---|
| TSROOT-01 | ACCEPT | P:1–9 describes conversational texts; B:1–4 describes unavailability messages and maintenance. Shell:76–79 supplies an unfinished operations entry, not a completed library. Actual report proposals concern reporting, not conversational templates or technical works. MOS1387 membership does not assign frontend implementation. |
| TSROOT-02 | ACCEPT | P:10–46 supports columns, three-step sorting, minimum-two-character search across name/code/response text, 8/4/6 filter counts, AND/OR and all eight text operators plus enum inclusion/exclusion. Saved selections, links and export presentation do not establish persistence or downloads. Module query conventions remain separately scoped. |
| TSROOT-03 | ACCEPT | P:47–79 and 113–118 distinguish required type/scope and Latin code from the shorter save checklist. Storage lengths are not UI validation limits. P:132–138 explicitly describes prototype-local limitations, not current backend behavior. |
| TSROOT-04 | ACCEPT | P:59–60,77,98,125 distinguishes status, active switch and editing object. P:196 says «Выключить», unlike «В архив» at line60. B:23–25 describes event-conditioned display; B:35 separately asks for currently-visible indication. Module preview does not prove library activation or delivery. |
| TSROOT-05 | ACCEPT | P:92 explicitly requires selected skill **and** selected surface. P:97 versus dictionary rows preserves `edu/health` versus `education/healthcare`; P:252 keeps dictionaries independent. Empty-set and `all` semantics remain unresolved rather than inferred. Association chips do not authorize global skill commands. |
| TSROOT-06 | ACCEPT | P:76,136,216 identifies placeholders and unchecked validity. P:138 limits multilingual support in the described model/prototype. B:45–46 scopes text-only/no-full-HTML-editor wording to stubs. Neither body supplies interpolation, escaping or attachment-payload contracts. |
| TSROOT-07 | REVISE, locator only | Proposed fields, unique indexes, external responsible identity, six local tables versus seven-count prose including external dependency, dictionary availability and unused soft deletion are supported. Replace dictionary structure citation with **P:220–230**. Archive does not imply `deleted_at`; display identity does not establish authenticated actor identity. |
| TSROOT-08 | ACCEPT | B:16–25,33–35,52,60 supports library editing/toggling and identifier links, not module-disable commands. Mock spec:161 distinguishes impact confirmation from saved `user_message`. Skill spec:30–54 and archived design require empty-start, user-entered trimmed reason/fallback; library selection or prefill is not authorized. D-037/SYSROOT03–04 distinctions remain intact. |
| TSROOT-09 | ACCEPT | B:18–30,37,50 requires audit and describes errors/repeat. P:132–138 describes no prototype history; timestamps do not supply it. These are source-specific domains, not a forced merged contradiction. SYSROOT10 remains separate; skill recovery is not transplanted into library mutations. |
| TSROOT-10 | ACCEPT | B:26–30,36,62–64 supplies start/end date-time, surfaces and warning hours. The midnight-crossing example lacks explicit end date/year/timezone. Report scheduling and SYSROOT12 module re-enable are different operations, not maintenance owners. |
| TSROOT-11 | ACCEPT | B:31–46,54–57 supports MUST/SHOULD/COULD/WON’T and November/December2026/2027 phases. MUST maintenance versus phase-two placement and temporary activation versus automatic scheduling remain visible without new commitments. |
| TSROOT-12 | ACCEPT | P:3 and B:48–53 are desired latency/access/effect statements, not measurements or enforcement evidence. P:107’s toast duration is unrelated. Skill spec:32,64 and archived design preserve historical approval without promising measured propagation or integration execution. |

## Scoped negative-claim support

An exact-literal search for `MOS-1387` within **A/sources**, using the tool’s normal `.gitignore`-respecting coverage, returned only:

- `jira-hierarchy/r1/content.json:32`;
- `jira-member-index/r1/content.json:1246`.

The surrounding records were read: MOS1388 lists MOS1387; its member record says `[B] Реализовать раздел "Шаблоны ответов"`, Development task, Hold, with empty `subtasks`.

This supports the report’s qualified local-search statement only. It does not establish global issue-description absence, complete Jira coverage, missing frontend ownership or current implementation status.

Absence statements about template/stub schemas, variable handling, scheduling details and delivery contracts are bounded to the two complete inspected bodies. Current API absence was neither investigated nor inferred.

## Verification limits

- Attachment-index counts **2/0**, pagination/completeness and collection outcomes remain parent-attributed. Metadata declarations were read, not independently replayed.
- Hashes and chunk-to-original roundtrip were not recomputed. Both derived readable bodies and exact chunk sets were independently read completely.
- HTML attachment **250800324 v1** was observed only as a page reference. Attachment bodies, PDF contents and prototype behavior were not inspected, rendered or executed.
- D-037 was checked as the accepted comparison chain; its underlying system-state sources were not independently re-audited here.
- Historical **13.10.2026** MOS1027 approval remains intact, without conversion into integration-run evidence.
- No network/browser/downloads, credentials, business calls, application-code inspection, tests/builds, nested delegation or repository edits occurred. No Git/index inspection or staging-state attestation.
- This review authorizes no source precedence, auth expansion, API adoption, owner-plan change, feature activation or global closure.