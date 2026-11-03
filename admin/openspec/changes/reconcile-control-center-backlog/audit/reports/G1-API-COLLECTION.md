# G1-API-COLLECTION — task 2.4 collection evidence

## Conclusion: incomplete

The historical API snapshot is retained and locally verifiable. Task 2.4 is **not yet sufficiently evidenced for closure**: Swagger URL discovery is asserted in metadata but its original discovery receipt is not retained in the inspected audit packet; completeness/disposition of available explanatory documents is not established. This is a collection-gate finding only, not a semantic API audit, G1 acceptance, or task closure.

All `A/` paths below expand to `openspec/changes/reconcile-control-center-backlog/audit/`.

## Exact acceptance assessment

| Task 2.4 element | Evidence and result |
|---|---|
| Published snapshot saved | Satisfied locally: `A/sources/api-live/r1/content.json`, line 1. Parsed successfully; 413007 bytes; SHA-256 `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06`, matching metadata. Independently counted 94 paths, 128 HTTP operations, 382 schemas. |
| URL established from docs, not guessed | **Incomplete documentary provenance.** `A/sources/api-live/r1/metadata.json:4–7,17` names `https://nchat-a-tech.mos.ru/api/control/docs` and `https://nchat-a-tech.mos.ru/api/control/openapi.json`, asserting Swagger discovery. No saved Swagger HTML/configuration, visible-link extraction, or original discovery response was located. Repeated downstream attribution is not independent discovery evidence. This does not prove the collector guessed the URL. |
| Retrieval metadata/time | Present: metadata lines 2–7,15–18 record source ID, revision, URLs, retrieval `2026-10-16T11:13:29.451Z`, method and capture limitations. Hash/bytes are independently checkable; retrieval itself is a collector assertion, not re-observed remotely in this run. |
| Versions/hashes | Present: content line 1 `/info/version` = `0.1.0`, `/openapi` = `3.1.0`, `/info/title` = `TSAM Assistant Management Service`; version is retained in the content even though not duplicated in metadata. Metadata lines 8–14 retain digest, counts and null ETag/Last-Modified. No extra server version can be inferred; their documented unavailability is not itself a closure blocker. |
| Available explanatory docs saved | **Partially evidenced, not absent.** See inventory below. No collection receipt establishes the Swagger-linked explanatory-document set or disposes of all relevant discovered candidates. OpenAPI has no `externalDocs` keys; that does not prove Swagger/wiki expose no additional documentation. |
| No Try it out/business operations | Metadata line 18 expressly says no backend business operation invoked; capture method is documentation GET. Work-item restrictions and checkpoints are consistent. No independent historical browser trace was found; this is recorded collector attestation, not runtime certification. This run used no network/browser/business calls. |

## Explanatory-document packets already retained

These are existing evidence, not a claim that all are required by task 2.4 or that the set is exhaustive. JSON pointers `/title`, `/version`, `/bodyView` (or `/text`) identify content; matching `metadata.json` in each revision records provenance.

| Exact content path | Retained material / revision |
|---|---|
| `A/sources/wiki-241082009/r2/content.json:1–49` | API-контракт управления поверхностями; page version 5 |
| `A/sources/wiki-241097511/r2/content.json:1–49` | API-контракт реестра доменов и каталога навыков; version 6 |
| `A/sources/wiki-241085439/r1/content.json:1–64` | API-контракт модуля диалогов; version 15 |
| `A/sources/wiki-241085838/r1/content.json:1–64` | API-контракт модуля отчётов; version 3 |
| `A/sources/wiki-241088180/r1/content.json:1–64` | API-контракт управления глобальными модулями ассистента; version 4 |
| `A/sources/wiki-241092242/r1/content.json:1–64` | API-контракт управления заглушками, баннерами и техническими работами; version 4 |
| `A/sources/wiki-241080062/r1/content.json:1` | Админка. Навыки; version 17 |
| `A/sources/wiki-245673187/r1/content.json:1` | Бизнес-анализ: Поверхности; version 18 |
| `A/sources/wiki-243776365/r1/content.json:1` | Бизнес-анализ: Диалоги; version 13 |
| `A/sources/wiki-247734813/r1/content.json:1–135` | Раздел «Обратная связь»; version 11 |

Additional explanatory evidence: `A/sources/jira-api-delta-scenarios/r1/` retains selected descriptions/attachment metadata; `A/sources/jira-lifecycle-details/r2/` and `A/sources/jira-attachment-833803/r1/` retain later lifecycle clarification/test-plan text. A test-plan document is not an executed test. `A/sources/jira-skill-switch-details/r1/metadata.json` explicitly records attachment 835759 body unread. This is an unresolved candidate, not proven unavailable or automatically a task 2.4 requirement.

`A/sources/api-live-status-readable/r1/` and readable wiki derivatives preserve convenient extracts, not independent acquisitions or fresh versions. Local `docs/api/contracts/README.md:3–18` identifies historical snapshots, normalization rationale and supplemental `crud-api.md`; these local historical materials do not replace provenance for the 2026-10-16 capture. Existing redactions, failed-attempt history and r2 supplements must remain intact.

## Exact remaining collector requests

1. Recover the **original** saved discovery receipt for `https://nchat-a-tech.mos.ru/api/control/docs`, if retained outside this packet: the minimal inert HTML/configuration/link extract identifying the spec URL, with source locator, retrieval time, format/redaction limits and hash. Bind it to `api-live/r1`; do not fabricate a historical receipt. If unrecoverable, record that fact and leave historical discovery independently unverified. A new docs read may supply a separately dated supplemental receipt, but cannot retroactively prove the old discovery.
2. Provide a narrow disposition of explanatory documentation linked from that documentation entrypoint: identified URLs/locators, saved revision or access outcome, and inclusion/exclusion reasons. Reuse the packets above. Do not infer that absent `externalDocs` means no available explanatory docs. No fresh live contract is required merely to finish historical acquisition provenance.
3. Coordinate the already discovered wiki **API** candidate with the wiki registry owner: `A/sources/wiki-238324523/r1/content.json#/pages/3` is `["241085256","API"]`; `A/source-checkpoint-r1.json:129–134` marks its body uncollected, relevance/priority pending. No `wiki-241085256` packet was found. Determine relevance/access and retain either relevant content+metadata or an explicit disposition. This source locator supplies an ID/title, not a specific URL to invent here. Do not classify it as inaccessible or require crawling all 42 wiki links for this lane.

## Code Context

### Files Retrieved

- `openspec/changes/reconcile-control-center-backlog/proposal.md:1–31`, `design.md:1–134`, `tasks.md:9–16`: collection authority, docs-derived URL rule, metadata/extraction requirements and exact task 2.4 acceptance.
- `A/work-items/G1-API-COLLECTION.md:1–9`: this bounded assignment.
- `A/sources/api-live/r1/metadata.json:1–19`, `content.json:1`: primary provenance and programmatically parsed bytes.
- `A/source-checkpoint-r1.json:1–140` and relevant registry matches; `source-checkpoint-r2.json:1–31` and packet references; `collection-checkpoint.md:1–41`: incremental collection state, not completeness certificates.
- `A/work-items/API-OPS-001.md:1–8`, `API-SCHEMA-001.md:1–8`, `R-API-001.md:1–7`; `A/reports/API-OPS-001.md:1–25,97–134`, `API-SCHEMA-001.md:1–32,199–224`; `A/reviews/R-API-001.md:1–31,100–120`: existing integrity checks and limits. Their semantic findings were not recomputed or used to close collection.
- Wiki content/metadata inventory above, inspected locally for identity/version/packet presence; `docs/api/contracts/README.md:1–33`: historical context.

### Key Code / Architecture

No application code was inspected. Read-only Python used `Path.read_bytes`, `json.loads`, `hashlib.sha256` and the eight OpenAPI HTTP method keys for independent hash/count verification. Source metadata attributes acquisition; content retains the version and actual bytes; checkpoints index packets; analysis/review reports consume them but do not create missing acquisition evidence. A local recursive filename/exact-string inspection included ignored audit files, avoiding false absence from ignore-respecting discovery.

### Start Here

Open `A/sources/api-live/r1/metadata.json:4–7,17–18`, then locate the original Swagger discovery receipt. This is the smallest unresolved provenance dependency; semantic API review is already separate.

## Validation and limits

Only local read-only inspections plus this requested report write occurred. One combined line-numbered read exceeded the display cap; targeted follow-up recovered the relevant provenance/checkpoint sections. No code/spec/checklist changes, tests, builds, network, credentials access, nested delegation or task closure. Snapshot hash/counts were independently recomputed; explanatory document bodies were not semantically re-audited. Local search cannot establish remote accessibility or recover unsaved historical browser observations. Staging state was not inspected or changed.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Task 2.4 assessed as incomplete with exact discovery-receipt and document-disposition gaps; retained version, timestamp, hash/counts and explanatory packets identified."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/G1-API-COLLECTION.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Local Python snapshot hash/count/version inspection","result":"passed","summary":"413007 bytes; matching SHA-256; 94 paths, 128 operations, 382 schemas; info.version 0.1.0."},
    {"command":"Local packet inventory, exact discovery-string search and numbered provenance reads","result":"passed","summary":"No original Swagger discovery receipt located; existing explanatory packets and uncollected API candidate identified."},
    {"command":"Tests/build/network/browser","result":"not-run","summary":"Prohibited by this read-only collection assignment."}
  ],
  "validationOutput": ["Snapshot integrity and retained version confirmed locally; historical URL discovery remains metadata-attested only."],
  "residualRisks": ["Original discovery evidence may exist outside the inspected packet; no claim that URL was guessed.","Available explanatory-document completeness and API-page relevance/access remain unresolved.","No remote freshness, backend behavior or staging-state verification."],
  "diffSummary":"Only the assigned collection report written; no source, metadata or task edits.",
  "reviewFindings": ["Collection gate incomplete; semantic API analysis does not discharge acquisition provenance."],
  "manualNotes":"Historical snapshot completion does not require a fresh live contract. Preserve security normalization, source revisions and redactions; do not close task 2.4 from this report."
}
```
