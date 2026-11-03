# Lane 1 — skill registry bounded join

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. Read-only local audit; no feature acceptance, deployment verification or external freshness claim.

Paths: **A** = `openspec/changes/reconcile-control-center-backlog/audit`; **S** = `openspec/specs/skill-catalog-experience/spec.md`; **H** = `openspec/changes/archive/2026-10-01-skills-prototype-alignment/tasks.md`.

## Evidence reused first

`A/reports/JIRA-MOS-774.md` establishes independent nested descriptions at jira-subtasks items 7–9 and attachment metadata-only limits. `A/reports/G2-JIRA-MEMBER-JOINS.md:186–188,303–305` leaves these six members U, rather than transferring neighboring implementation evidence. Its independent review `A/reviews/R-G2-JIRA-MEMBER-JOINS.md:110` explicitly preserves independent nested analysis. This join supplies that missing attribution, not a replacement inventory. Exact parent descriptions were read from `A/sources/jira-details-MOS-774/r1/content.json#/items/1/description`, `/items/2/description`, `/items/3/description`; subordinate descriptions independently from `A/sources/jira-subtasks/r1/content.json#/items/7/description` through `/items/9/description`.

## Source → API → owner/spec → code → written assertions → disposition

### MOS-675: page/header

- Exact saved requirement: create a page and add its header; referenced screenshot and HTML attachments are metadata, not inspected visual bytes (`/items/1/attachments`). CLOSED is saved Jira status, not audit acceptance.
- API: header composition has no data endpoint requirement. No header content inferred from attachment filenames.
- S, “Prototype-aligned visual composition” and “Contextual catalog actions and tabs”; H tasks 3.1–3.2 already own compact header, divider, registration and help navigation.
- `app/pages/skills/ui/skills-page/skills-page-intro.tsx:8–42` implements header, h1, separator and links.
- `app/pages/skills/ui/skills-page.test.tsx:21–40` actually asserts one h1, visible introduction, no obsolete read-only copy, `/skills/new` and `/docs?article=skill-register` hrefs. Registry is mocked here: not proof of integrated backend or geometry.
- Disposition: no new implementation owner warranted for textual page/header requirement. Retain visual attachment limitation; do not reopen historical task checkboxes or declare screenshot acceptance.

### MOS-676: notification and filters

- `/items/2/description` asks for notification and filters according to screenshot/example; does not independently specify notification semantics. Nested defects below have their own textual requirements.
- Saved API `A/sources/wiki-241097511-readable/r1/readable-text.txt:418–474`, §2.5, supplies query/domain/team, sorting and server pagination. This older readable body lacks current status in its illustrated response; current client status support is not evidence that this saved body promises it. No notification source in the inspected list response.
- S “Contract-backed registry columns and filters” and “Entity-specific warnings” explicitly defer unsupported warning sources, disallow synthetic all-clear and local-page filtering. H 7.2 owns URL/debounce/directory pagination; H 8.1/8.2 preserve hidden unsupported warnings and deferred source-backed integration.
- `app/features/skill-registry-filter/ui/skill-registry-filters.tsx:25–130` has search debounce and status/domain/team selects. `app/entities/skill/api/skill-registry-client.ts:54–78` passes filter IDs/status/sort/limit/offset, returns server total. Warning absence is intentional under S, not automatically an implementation defect against unavailable screenshot content.
- `app/widgets/skills-registry/ui/skills-registry.test.tsx`, tests “renders contract fields…”, “filters by API domain and team UUIDs”, “filters by status, restores page…”, “selects domain and team options from beyond the first hundred” assert actual request parameters, back/forward/page reset, 101st options, no warning/all-clear placeholders. Assertions were read, not executed.
- Disposition: no-op for already owned basic filters; unresolved visual/notification-reference comparison. Do not invent a notification or use absence as proof that Jira requirement was removed. Existing deferred warning owners remain, without re-auditing their domains.

### MOS-677 and independent MOS-1052: table and sorting

- Parent `/items/3/description`: table per screenshot/example and sorting. Nested `jira-subtasks#/items/9/description` independently quotes РЕЕ-12: name, domain, status, dialog count and modification date; steps identify clickable headers. Its attachments are explicitly empty, not missing bytes.
- Saved API §2.5 lines 429–434 explicitly permits `name`, `domain_name`, `created_at`, `updated_at` and descending variants. This is concrete positive evidence for domain sorting, not an assumption that all requested fields are supported. Status/dialog sort are not listed there.
- S requires server-backed supported sorting, excludes unsupported dialog column and local-page substitute. H 5.1 and 6.1–6.3 are historical composition/extension work; do not turn their old completion/block states into current acceptance.
- `app/widgets/skills-registry/ui/skills-registry-table.tsx:39–60` offers name and updated_at sort buttons; domain/team and status headers are plain text. Dialog column is absent. `app/features/skill-registry-filter/model/constants/skill-registry-filter.constants.ts:4–9` admits only ±name and ±updated_at, so saved-supported domain_name is not exposed.
- Table component assertions in `skills-registry.test.tsx` check name/purpose/service ID/version, dates, links, domain/team, server total and absent dialog column. `app/entities/skill/api/skill-registry-client.test.ts:112–156` asserts full query including sort=-updated_at and offset=10. `app/features/skill-registry-filter/model/registry-search-params.test.ts:12–27,47–70` asserts unsupported status-sort normalization. None of these is an assertion of clickable domain sort or all five РЕЕ-12 fields; registry fetch mock does not sort returned items.
- Disposition: partial requirement coverage; actionable supported domain-sort gap separate from unresolved status/dialog contract extension. Suggested narrowly scoped corrective owner (no matching active tasks/proposal found in bounded key search): **“MOS-1052 — подключить сортировку domain_name/-domain_name по сохранённому контракту списка навыков: заголовок домена, allowlist/URL, сброс страницы и серверный запрос; проверить оба направления и отсутствие локальной сортировки страницы. Статус и число диалогов оставить отдельной зависимостью согласованного расширения, не объявлять РЕЕ-12 выполненным целиком.”** Before implementation, reconcile the saved readable sort contract with authoritative generated/API input; this audit does not authorize typegen or assume backend deployment. No invented created-date UI requirement.

### MOS-1050: select alignment

- Independent `/items/7/description` specifies status/domain dropdown displaced from field; expected no displacement. Attachment bytes not available in inspected packets.
- API: none for popup positioning (directory data is not geometry evidence).
- S visual composition/narrow layout and H 2.2 are existing visual requirement homes, but no independently attributable active MOS-1050 owner found in bounded active task/proposal key search.
- Filter selects use shared `SelectContent`; `app/shared/ui/select.tsx:55–93` delegates to Base UI positioner, align=center, alignItemWithTrigger=true, anchor-width popup. This is code configuration, not confirmation of defect or fix.
- Registry test “shows an unknown status…” explicitly avoids pointer-dependent positioning in JSDOM; it asserts expanded list/options only. No geometric assertion found in inspected bodies.
- Disposition: unresolved reproduction/visual evidence, not confirmed current defect. Minimal planning wording: **“MOS-1050: проверить положение списков статуса/домена относительно поля по сохранённому описанию; component-проверки открытия не считать геометрической приёмкой. Исправление только после подтверждения воспроизводимости; browser/E2E требует отдельного разрешения.”** Do not add a speculative shared positioning change.

### MOS-1051: Russian result-count inflection

- Independent `/items/8/description` specifies incorrect inflection for 1,2,3 etc. after training-status filter; expected correct word form. Requirement does not depend on screenshot interpretation.
- API §2.5 pagination.total_items provides count; no new backend policy needed.
- S server-total scenario is existing behavior baseline; H 7.1 retains count but contains no inflection fix. No active MOS-1051 owner found in bounded key search.
- `app/widgets/skills-registry/ui/skills-registry.tsx:101` renders fixed `{registry.data.total} навыков`.
- Actual assertions in `skills-registry.test.tsx` explicitly expect `2 навыков` in mixed-list test and `1 навыков` in long-text test; these preserve the reported linguistic defect, not coverage of correctness. Other assertions expect 0/11 навыков.
- Disposition: concrete current frontend defect. Minimal new corrective scope: **“MOS-1051 — склонять подпись серверного total реестра (навык/навыка/навыков), сохраняя серверный подсчёт и фильтры; заменить ошибочные ожидания 1/2 навыков, проверить 0,1,2,3,4,5,11–14,21–24 и отбор status=training.”** No sorting/notification redesign bundled into this fix.

## Planning attribution and limits

Recommend U→P for MOS-675/676/677 and MOS-1050/1051/1052 **only as attributable requirement comparisons now supplied**, subject to parent's independent package review. P does not mean implemented, visual-tested, approved or closed. For 1050 the comparison concludes unresolved geometry, not defect acceptance. No B→P claims, parent/module aggregate closure or Jira status edits.

Actual reads: exact parent JSON (whole one-line packet; only assigned members analyzed), subtask lines150–219, accepted inventory report, member-join/review targeted matches; S in full; H in full (neighbor sections not audited); API readable §2.5 only; header and page test; registry table and registry test; filter UI, client, client-test112–176, search-param test1–80, shared select55–134; targeted grep for count/sort/active owner keys. No repeated domain/token/history/monitoring/export audit. No tests/build/typecheck/network/browser/credentials/subagents used. Broader schema completeness and live sort behavior remain outside this lane. Historical visual-test summaries in H are not current MOS-1050 evidence.

Current-input SHA256 manifest follows; hashes are local bytes, not git-show baselines.

```text
0d1083ea677d8b380789a33f5e56cd30357132ee476bd3362dc31243fc89fd59  openspec/changes/reconcile-control-center-backlog/audit/work-items/G2-SKILL-REMAINING-SEVEN.md
e082adf172c47760787f15ea7a856107d25d2e4c085f2e3ca3a0bc93d7079208  openspec/changes/reconcile-control-center-backlog/audit/sources/jira-details-MOS-774/r1/content.json
c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e  openspec/changes/reconcile-control-center-backlog/audit/sources/jira-subtasks/r1/content.json
04f21e1039acdcf56460ba84a0e01101a4b0131a1e9f0d3f47f3191c4a22719c  openspec/changes/reconcile-control-center-backlog/audit/reports/JIRA-MOS-774.md
dc9b199c2a9500b2ff1857de1feaec9282e8130fa1b78720f551913907618b44  openspec/changes/reconcile-control-center-backlog/audit/reports/G2-JIRA-MEMBER-JOINS.md
d13686b9bb0df5722c397c84f116938835b5f7d66983038a4013aa2ef0791a8b  openspec/changes/reconcile-control-center-backlog/audit/reviews/R-G2-JIRA-MEMBER-JOINS.md
c6dd8857060fa4e87a7170fb604486d12d03a8e74d1ac24c4704554eba67b2df  openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-241097511-readable/r1/readable-text.txt
21bff8f61b30215d95b59b0adbb1059ac3b64e80be358fa6bfa64b3e7cbed942  openspec/specs/skill-catalog-experience/spec.md
fca3825b59ad64394fc0714e8cb22cc3934eb8e2c7ec73bd9c587d393295e1b2  openspec/changes/archive/2026-10-01-skills-prototype-alignment/tasks.md
15816a309fccb6c751cb91eaa83b2808e4d009337bad8db35d253f0c0a89f74d  app/pages/skills/ui/skills-page/skills-page-intro.tsx
9bbe4833c6b32936e98f3c6a0b0b97925fc09d15120111a4d22e7a87a5f0e6be  app/pages/skills/ui/skills-page.test.tsx
b6a8eebad1f95a3691f1a9c99a550c897edbcbf90060a4e977e1eca025a64eff  app/widgets/skills-registry/ui/skills-registry.tsx
ccf6d6eefcdcdfd195af8cd52eb2bf4da11578d14c1d32d6bf32bd4e94ba9a4a  app/widgets/skills-registry/ui/skills-registry-table.tsx
63977dd1e46c05dc90d83d6593a53fbacceabcacfd942993b6534e5167843270  app/widgets/skills-registry/ui/skills-registry.test.tsx
b02cbfb6c8abb25465d640891e891c261efa0df30ee2368024fc05ef5d1eb972  app/features/skill-registry-filter/ui/skill-registry-filters.tsx
3691a3ad75b8779ec2c011098fa4dc490a33ca2dd7b620d381a83f4b806324e2  app/features/skill-registry-filter/model/constants/skill-registry-filter.constants.ts
27b0b30a63ed838880b5bf8215d0d71a1ef57056b2b8d89a9cfc269ecc6aca31  app/features/skill-registry-filter/model/registry-search-params.test.ts
fe22d8076a52c22ea245853b2bbe3f7103a1f515776920a6ecf76b6a6fcd5969  app/entities/skill/api/skill-registry-client.ts
afafe2c26cee8843d47040e99a701acaf0899d44dc9a662b3417aba8caf5e398  app/entities/skill/api/skill-registry-client.test.ts
87858971de8d53f575fcea4c524c2dfd9009ff5ea0a31103f6ca9cfc90d12e04  app/shared/ui/select.tsx
```

Final: six attributable joins delivered; one confirmed count-label defect, one saved-supported domain-sort gap, one unresolved geometry report. No feature acceptance or source changes.
