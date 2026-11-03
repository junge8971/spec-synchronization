# Dictionaries author handoff — blocked before scaffold

No project edits or scaffold. The supervisor confirmed the pre-scaffold pause: unresolved material policies cannot be selected by the author. One encompassing `add-reference-dictionaries` remains the intended change; nothing has been reduced to an MVP or split into product changes.

## Decision required

Two acceptable next paths require user authorization:

1. Create the **single full-scope planning change with explicit unresolved product/backend gates**, clearly not implementation-ready. Preserve requirements and alternatives without making contradictory behaviors normative or treating prerequisites as delivered.
2. Resolve the material policies below **before creating the change**.

### Material blockers

- **Save and checks:** Wiki Описание §§7,11,13 describes blocking checks and saved changes; Таблицы §7 requires server-computed results. Published value mutations commit separately, with no aggregate atomic save or server checks contract. Choose an explicitly reconciled staged/partial-success editor or require an atomic backend contract; server checks remain a prerequisite unless separately changed by the user. Prototype `saveDict` does not enforce check failures and is not acceptance evidence.
- **Mutation, classification and deletion:** Wiki Описание §§5–6 allows informational mutations under editable allow flags; published flags are computed and informational code changes/deletion are prohibited. Wiki Таблицы §3 says soft-only deletion; CRUD documentation §18 describes physical whole-dictionary deletion. Attachment and other roster classifications conflict. Choose approved policy/source reconciliation or retain exact backend/product gates; do not seed, migrate, delete physically or expose editable-but-unsaved settings by assumption.
- **Lifecycle and consumption:** Explicit draft creation is supported, but activation/readiness is unresolved. Wiki Описание §§10,13 promises paused exclusion and automatic consumption; published status/cache/publication fields do not enforce those effects. Attachment rules storage likewise does not establish upload enforcement. Preserve named consumer boundaries and require owner-backed propagation, matching and lifecycle semantics rather than claiming local success.
- **User-visible persistence boundaries:** Define actual discard/dirty navigation and lifecycle sequencing, full-selection URL restoration and saved-filter replacement/apply semantics, and card-export versus values-export behavior. Published server saved-filter and export operations are recommended reuse, not an invitation to invent alternatives. Creation validation must reconcile Wiki Latin wording/default owner with wire constraints. Minor route naming/default presentation details need not become blocking product questions.

The user's entire-section scope includes advanced conditions. Future artifacts must explicitly reconcile the historical journal exclusion rather than omit them. Missing type sorting, numeric value-count conditions, writable allow flags/change comments and server checks are precise contract prerequisites, not ordinary fetch failures. Unknown deployment behavior must be tracked separately from missing publication.

## Evidence checked by author

Read `work-items/PLAN-DICTIONARIES.md`, `openspec/config.yaml`, and `.agents/skills/openspec-propose/SKILL.md`. Consumed both supplied bounded analysis handoffs. Independently inspected these exact primary seams, without claiming another full source read:

- `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247751846/r2/readable.txt`: lines 101–223, 244–282, 554–560 (Описание §§5–8,10–11,13; Таблицы §7).
- `openspec/changes/reconcile-control-center-backlog/audit/sources/local-dictionaries-prototype/r1/content.html`: lines 1915–1977, `markDictDirty`, `saveDict`, `togglePauseDict`, `deleteDict`; inert text inspection only.
- `docs/api/contracts/crud-api.md`: targeted matches at 1382–1388 (computed flags and paused non-enforcement), 1541 (per-request transactions), 1588–1590 (physical user deletion).
- `app/application/model/route-access.ts`: existing unmapped wildcard fallback. Preserve it; no new permission mapping, session behavior or credential policy is proposed.

Primary source URL: https://wiki.mos-team.ru/spaces/KR/pages/247751846/ . Supplied capture identifies version 10; no network refresh was performed by this author.

Recomputed SHA-256:

| Repository-relative source | SHA-256 |
| --- | --- |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247751846/r2/readable.txt` | `002d6b34375939d9f8847350ef0cdf9ff6db8f151028f297da6750ba0d1c0957` |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/wiki-247751846/r2/content.json` | `6f4a85bf911634a724e3411138c517fe3ce295d2036e09d573444dc9d6d04588` |
| `openspec/changes/reconcile-control-center-backlog/audit/sources/local-dictionaries-prototype/r1/content.html` | `385f230467db6b8b2fdf26dbc08f9154ca7fd1651db037c6227eccc9fc8fa310` |

## Validation and artifact manifest

- `git rev-parse HEAD`: `d2af6c5b61146306f0795b6a272c5a74bdfa08f7`.
- `git status --porcelain` and `git diff --cached --name-only`: empty at inspection; no Git mutations performed.
- `openspec context --json`: passed; nearest authoritative root `/home/user/my/work/codesrc/projects/CAM/tsam-admin-front`.
- `sha256sum` of the three primary files: passed, matching handoff hashes.
- Read-only `sed`, `rg`, `cat`: passed. Prototype scripts not executed.
- Scaffold/status/instructions/dependency rereads, strict target validation and scoped Prettier: **not run**, because creation stopped at the required ambiguity gate. No target artifacts exist from this author.
- Application/unit/component/browser/E2E tests: **not run**; no implementation or test edits, and browser/E2E remain prohibited.
- Manifest: only this requested managed output report; project changed-files and tests-added lists are empty. No proposal/design/delta-spec/tasks artifact hashes exist.

Full section coverage remains the contract: registry/search/conditions/saved selections/exports; detail, settings, ordinary values and attachment rules; creation/lifecycle/checks/dirty protection; API and all documented consumption boundaries. The requirements lane's section matrix is evidence for future authoring, not an authored/validated normative spec here. Existing owners, optional-module independence, credential-free mocks and backend authorization remain untouched.

Recommended next step: independent review of blocker materiality, then parent obtains authorization for one of the two paths. Do not start implementation.
