# R-OPTIONAL-DOMAINS-SEVEN — bounded independent review

## Verdict

All seven reports **ACCEPT as bounded static evidence**, not feature acceptance. Read every report completely. No mandatory substantive report rewrite. Three narrowly scoped corrective planning deltas are warranted; the other four remain no-op. Implementation is not authorized by this review.

| Report | Verdict | Disposition / independently checked ownership |
|---|---|---|
| IMPL-KB-REGISTRY | ACCEPT | No-op. Original KB tasks 4–5 own registry/search/saved filters; later `2026-10-15-update-control-center-api-contracts` tasks 4.1–4.4 explicitly own links_count/skill_names and typed round trips. Current `mocks/knowledge-base/model.mjs:37–39,71–75` supports that migration. Do not restore historical unavailable-field wording. |
| IMPL-KB-EDITOR | ACCEPT | No-op. Original KB tasks 2.2–2.4,6–8 own draft/persistence/error/reference/status behavior. Spot check `knowledge-base-mutations.ts:22–42` confirms remembered creation ID, retry:false and GET-only recovery. No duplicate editor task or new archive/name-uniqueness policy. |
| IMPL-KB-EXPORT | ACCEPT | Current scoped **KB-limit-advice** correction below; otherwise original tasks 9.1–9.3 remain owners. |
| IMPL-AB-REGISTRY | ACCEPT | No-op. Original A/B tasks 4.1–4.4 plus later contract-update tasks 4.1–4.4 own the scenarios. `mocks/ab-testing/model.mjs:50–52,82` publishes/derives numeric groups_count. ABROOT-02 is not missing implementation work. |
| IMPL-AB-EDITOR | ACCEPT | Current scoped **AB-per-group-label** clarification below. Original A/B task 5.1 is the historical owner; no numeric algorithm or lifecycle defect established. |
| IMPL-AB-EXPORT | ACCEPT | No-op. Original A/B tasks 3.6,6.1–6.3 own export. Unlike KB, `ui/ab-testing-export.tsx:55–60` appends conditional narrowing advice for list failures. Limited mounted integration coverage is not proof of a bug or deployed delivery. |
| IMPL-SKILL-DOMAINS | ACCEPT | Current scoped **domain-read-label** correction under accepted D-002/D-007 continuation; selector and inactive-update policy remain separately unresolved. No duplicate baseline CRUD plan. |

## Three corrections: primary evidence and exact scope

### KB-limit-advice — planning delta now; no product choice needed

Original accepted root readable source `sources/wiki-247737907-readable/r1/content.txt:128–129` specifies checkbox export modal, not limit/error semantics. The stronger approved requirement is current `knowledge-base-export/spec.md`, “Server limit exceeded”: show limit **and suggestion to narrow selection** (also original archived export delta/task 9.1).

Connected evidence: `mocks/knowledge-base/handlers.mjs:79` sets `EXPORT_LIMIT_EXCEEDED`; `mocks/managed-search.mjs:94–101` emits HTTP 422 and only “Mock export exceeds 10000 rows”. `app/optional/knowledge-base/ui/knowledge-base-export.tsx:56` displays raw error.message. Component test `ui/export/knowledge-base-export.test.tsx:133–155` injects advice itself under 413/500 and generic ERROR, so it does not demonstrate real-limit advice.

Necessary planning correction: explicitly require narrowing advice for the actual 422 EXPORT_LIMIT_EXCEEDED path and a regression using that envelope without pre-supplied advice; preserve selected fields/no download/no false success. Do not classify every 422 as a limit error, change the row limit, or duplicate export capability work. Real backend behavior remains unverified.

### AB-per-group-label — planning delta now; no product choice needed

Original accepted root `sources/wiki-247742436-readable/r1/content.txt:227` says “Минимальный размер выборки в каждой группе”. Current `ab-testing-editor/spec.md` specifies min_sample_size and bounds but omits the qualifier. `app/optional/ab-testing/ui/editor/editor-main.tsx:44` labels it “Минимальная выборка”; selected existing component assertions at `editor.test.tsx:310,380` use that generic label.

Necessary planning correction: accessible label or associated explanation must say **per group**, with focused component coverage and corresponding scoped specification clarification. Preserve nullable integer 1–2147483647, wire scalar, defaults and execution disclaimer. No calculator, statistical algorithm, traffic enforcement or DTO change follows. Archive task 5.1 stays historical, not reopened.

### domain-read-label — planning delta now for reads; specific choices remain separate

Primary saved API `/components/schemas/DomainResponse/properties/zones` is an array of strings. MOS-1306 `sources/jira-api-delta-scenarios/r1/content.json:/items/1/description`, “Валидация” and “Изменение query repository”, requires retained linked inactive reads, server ordering and unaffected domain/count semantics. Accepted `R-DOMAIN-ZONES.md:79–101` explicitly allows truthful returned-code/read/no-loss planning now, separately from selector expansion. Linked-contract review preserves that distinction despite wiki enum/proposed-cap wording.

Actual `app/entities/skill-domain/api/skill-domain-client.ts:18` restricts list/detail/PUT-response reads to two enum values. `app/widgets/skill-domains-registry/ui/skill-domains-registry.tsx:70–72` labels every non-authenticated value “Открытая”. Current client tests inspected at `skill-domain-client.test.ts:5–57` cover seeded codes and invalid count, not wider codes. This is conditional compatibility failure, not proof of a deployed third code.

Necessary planning correction: separate read representation from fixed assignment choices; accept/preserve returned string codes and use truthful code fallback rather than anonymous/open mislabeling. Cover list/detail and affected response adapter, unknown-code display, retained linked inactive values, order/count preservation and no-loss rejection. Do not prescribe a successful unchanged-inactive save. Known rejection cases may be planned without inventing exact error envelopes or frontend enforcement.

Still unresolved: owner approval for dynamic/additional-code selection; exact lookup endpoint/key, labels/order and inactive inclusion; unchanged-inactive resubmission/omission/null semantics; concrete zone-rejection payloads. Preserve current fixed selector, PUT/version/idempotency, uniqueness/address deferrals. Do not add lookup as a current CRUD dependency, silently remove values, impose proposed max-two policy, or infer deployment. For downstream citations use stable **D-002 domain-zone bullet / D-007 headings**: old physical decisions.md line numbers have shifted (D-002 now starts at 623). This is a citation consumption note, not a substantive report rejection.

## Integrity

Root and HEAD match assignment: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Current-local SHA256 verification found **all 78 report-recorded input hash occurrences matching the corresponding local files** (11/8/11/11/10/13/14 respectively). This verifies current bytes, not Git history, source-server authenticity or fresh capture. Input hash lists remain in the seven accepted reports, avoiding duplication here.

Current report SHA256 (audit/reports/ prefix):

```text
5a5cc05bc67a4bf3e082d4528f136922e03f8669aee0ac5e45a63f6ca243c0ab IMPL-KB-REGISTRY.md
6ac15499b9b190f7a75d73b2e74d38c6488b74ac5e0af38a2e34efb566122e91 IMPL-KB-EDITOR.md
56748224928c54e02cb4089d02fa733b7ee1c4afb2510b196908121c59fa39b6 IMPL-KB-EXPORT.md
bd8acbe0a676bdd89498da6d8214502451724402e36022362fc70dae0d9659e1 IMPL-AB-REGISTRY.md
b5628e85dd0d0760ce726087b601296064e12a92ecf9f70c7202c218ae3af118 IMPL-AB-EDITOR.md
5cb4d93688400199c26a40b72468488b817f6d0f0c0fc72597edfd4fd8651e05 IMPL-AB-EXPORT.md
449d1b9b531da58b888483fc3b45f5487f06601b3e0064b2dc1e85d5f78e47a2 IMPL-SKILL-DOMAINS.md
```

Additional directly checked primary-input SHA256 (audit/ prefix):

```text
549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06 sources/api-live/r1/content.json
b1ac1c3a087a6ebed2e5d2b3bef6a2e92c9a71676e3be4fbaf8dd802423d6aed sources/jira-api-delta-scenarios/r1/content.json
11e852b8690c432086f05fc32bb03ee47512bcf46c354471b4fef578e5b7e797 sources/wiki-247742436-readable/r1/content.txt
6ed0b91afcfcbc3ca504d34fa2fa55609d782d0ffe6766ce4d679ab65d03ada1 sources/wiki-247737907-readable/r1/content.txt
57d3d6cf410f4620009d5ba8a1a6b5a95a3db21766f1dcfaea5e29c137be1664 work-items/R-OPTIONAL-DOMAINS-SEVEN.md
```

## Limits

No project changes, tests/build/browser/network/credentials or nested agents. Tracked working/staged diffs were empty. Only selected primary-source sections, relevant current specs/code/test assertions and existing task owners independently checked; no broad re-extraction or every-test census. Report partial-read limits, attachment limits and historical task states remain intact. Mock behavior is not real API evidence; optional isolation, production graph, accessibility runtime and deployment are not recertified. No global checkbox, feature closure or archived task change follows from seven ACCEPT verdicts.

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Seven complete report reads, all recorded input hashes matched, three primary-evidence-backed scoped corrections and four owner-supported no-op dispositions."}],
  "changedFiles": ["/home/user/.pi/agent/sessions/--home-user-my-work-codesrc-projects-CAM-tsam-admin-front--/subagent-artifacts/outputs/c7f90fbc-3fb2-4d62-b954-88a8a89b758e/review-optional-domains-seven.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"git rev-parse HEAD; local SHA256 verification","result":"passed","summary":"Expected HEAD; seven report hashes and all 78 recorded input occurrences verified."},{"command":"git diff --name-only; git diff --cached --name-only","result":"passed","summary":"Both empty."},{"command":"tests/build/browser/network","result":"not-run","summary":"Prohibited."}],
  "validationOutput": ["Seven ACCEPT dispositions; three scoped planning deltas, no implementation authorization."],
  "residualRisks": ["Runtime, deployment and full conformance unverified; partial-read limits retained.","Domain selector/directory and inactive-update semantics remain unresolved."],
  "noStagedFiles": true,
  "diffSummary": "External review artifact only; no project changes.",
  "reviewFindings": ["KB limit advice, A/B per-group wording and truthful wider domain reads warrant scoped planning corrections now."],
  "manualNotes": "Preserve archive/task history, later migration ownership and all global/feature checkboxes; use stable D-002/D-007 headings rather than stale physical line citations."
}
```
