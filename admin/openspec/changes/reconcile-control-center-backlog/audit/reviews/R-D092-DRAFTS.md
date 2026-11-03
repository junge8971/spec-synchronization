# R-D092-DRAFTS — independent bounded review

## Disposition

| Package | Verdict |
|---|---|
| `fix-dialog-registry-presentation-and-reset` | **revise** — reset design masks a concrete behavior change behind an unresolved-policy exclusion. |
| `fix-surface-registration-text-feedback` | **accept** — coherent bounded planning package; no mandatory correction identified. |

**Publication remains held for both packages.** The latest external freshness attempt failed with `Failed to fetch`. This local review does not satisfy or bypass that gate. Publication requires a successful explicit source check or an authorized scope decision. No implementation, deployment, or backend acceptance is implied.

HEAD independently checked: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`.

## Independent evidence

Read both proposed packages completely, including all nine embedded artifacts, and both prerequisite reviews.

Independently inspected:

- Saved Jira `sources/jira-subtasks/r1/content.json#/items/2,3,4,5,13,14`, including exact descriptions.
- Saved wiki-243776365 `bodyView`: СПС-25, reset scenario, СПС-32.
- Saved wiki-241085439 `bodyView`: server duration snapshot, continuation wording, failure indicator, null rating and independent server fields.
- Saved API r1/r2 search request references and `DialogListItemResponse` fields: boolean failure, nullable completion/rating, integer duration.
- Complete current main specs for `dialog-registry`, `dialog-selection-builder`, `surface-skill-selection`, `surface-registration`, and `surface-overview-connection`.
- Actual dialog filter, registry composition, condition editor/lifecycle, quick-filter normalization, row and shared rating implementations.
- Actual surface selection item, registration details/step composition, watched-domain computation, parser and validation schema.
- Relevant existing dialog reset tests and registration normalization, validation, payload and local-domain-feedback test bodies. Tests were read, not executed.

## Dialog package: required revision

### R1 — blocking: complex-only pending reset is not behavior-neutral

**Locations:** proposed `design.md`, Decisions 2–3; `tasks.md` 2.1–2.2; reset ADDED requirement and package claims that existing complex-draft behavior remains unchanged.

The proposed two-part predicate considers applied selection and pending quick filters only. This necessarily hides reset in this reachable state:

1. Applied selection is initial/default.
2. Quick controls remain unchanged.
3. User opens the condition editor and adds or changes an unapplied condition.

Current code does not hide reset in that state:

- `app/pages/dialogs/ui/dialog-filters.tsx` renders **Сбросить всё** unconditionally and invokes `onReset`.
- `app/pages/dialogs/ui/dialog-registry.tsx` increments `editorVersion`; the keyed `DialogSelection` remount discards the condition draft.
- `app/features/dialog-selection/ui/dialog-selection/dialog-condition-editor.tsx` owns that draft privately.
- `dialog-selection.tsx` unmounts the editor on close; separate group clearing also exists, but neither makes removal of the existing global-reset action behavior-neutral.

Thus implementing task 2.1 literally removes an existing way to clear complex-only pending changes. “This change defines no policy” and “do not lift private draft” do not prevent that outcome. The implementation already requires the decision that design §3 postpones conditionally.

СПС-25 says reset is hidden when there is nothing to reset; it does not explicitly settle whether an unapplied complex draft counts. Main builder requirements preserve draft/application and global-reset semantics but do not unambiguously resolve this visibility question. Neither a mandatory hidden policy nor a mandatory visible policy can be attributed to those sources alone.

**Exact minimal correction:**

1. Replace the conditional future escalation in design §3 with an **explicit unresolved reset-implementation gate**. Record the concrete existing visible/remount behavior and the regression produced by the proposed predicate.
2. Mark the two-part predicate as **incomplete, not implementation-ready**, until the complex-only case is resolved. Remove the categorical prohibition on communicating draft state if it would preclude the approved resolution.
3. Add an unchecked task **before 2.1** requiring an authorized decision for complex-only pending changes. State that reset visibility implementation cannot proceed before it; the three row corrections are independently specified.
4. After that decision, align proposal/design/reset delta/tasks and add the corresponding component regression: default applied selection, unchanged quick controls, edited complex draft, visibility and reset lifecycle. Preserve the separate clear-group and close-without-apply semantics.
5. Do not characterize omission of this case as proof that behavior is preserved.

This review does **not** choose the product policy. If approval of a complete implementation-ready reset package is required now, that policy must be escalated to its authorized owner. A revised planning draft may instead retain the explicit gate.

### Other dialog findings

- **Lossless MODIFIED block passes.** Every original normative paragraph and both original scenarios occur unchanged in the proposed replacement. New clauses are additive; neighboring main requirements are not replaced.
- Failure-dot placement and accessible text are supported; no invented geometry is imposed.
- Duration stays a server snapshot, including zero, with no client timer or polling.
- Registry-local null rating avoids changing shared/card presentation.
- Applied conditions, invalid quick drafts, pending return to defaults and simultaneous all-five reset are addressed coherently.
- Existing tests do not resolve R1: the inspected combined reset test clears and applies the group before global reset.

## Surface package: accepted locally

No mandatory correction identified.

- MOS-1166 supports limiting the displayed descriptive text. The package correctly targets current `skill.purpose` without asserting equality with detail description or introducing detail-fetch, a 200-character data limit, tooltip policy, or fixed line count.
- `SkillSelectionItem` currently connects the full paragraph through `aria-describedby`. The proposed requirement preserves the full value and accessible description, keyboard selection and parameters.
- MOS-1167 supports separate visible feedback from entered domains. Existing `useSurfaceRegistration` already computes normalized domains; forwarding those values avoids new state or parsing.
- Current validation requires a nonempty normalized list, not DNS validity or availability. The draft accurately preserves this boundary.
- Separate capability owners and ADDED requirements leave existing catalog, persistence, creation recovery and server-connection requirements intact.
- Shared editing consumers receive explicit regression protection without expanding the Jira requirement to unrelated geometry.
- DOM/style checks are explicitly not browser-geometric proof. Missing historical images and unresolved MOS-1110/1164/1165 questions remain outside scope.

**Minimal corrections:** none. Acceptance remains planning-only and publication-held.

## Fingerprints

SHA256 of exact local bytes.

### Complete reviewed draft documents

Paths relative to `openspec/changes/reconcile-control-center-backlog/audit/publication/`:

| File | SHA256 |
|---|---|
| `DRAFT-DIALOG-D090.md` | `dfbabb417f41bb580a7ad793d298524bac856f4929de71f027c0da4a7733e319` |
| `DRAFT-SURFACE-D091.md` | `de98a82303e6a4ff8b673583b6c2a18a36864d90a1d91b478bfa19fd1d7da77f` |

### Exact proposed artifact contents

Hashes cover the UTF-8 content inside each `markdown` fence, including its trailing newline and excluding fence delimiters.

| Package / artifact | SHA256 |
|---|---|
| Dialog `proposal.md` | `532b304ada9946f3c94834d3074e46af23f60f07da6b7ee5db90cd0ec17b78a6` |
| Dialog `design.md` | `72f59c94e598a752cd91d50d1eed8b3959b6d514288124beaf8c85f25fc3e3df` |
| Dialog `tasks.md` | `25ef487f42f367e6821896c6d5002db53668289994bcdcb45c59b9e340ccc4a3` |
| Dialog `specs/dialog-registry/spec.md` | `8aff75feebe0a55441c17b0ecfdb216c8f57e759b9c8aeae09ba3303ff66ed31` |
| Surface `proposal.md` | `2304598677031fca36387dc0d43f72f1e97bd504c0d0869f3632029867d70de4` |
| Surface `design.md` | `eacdf4c563752554f3222c4c06c8736b9e1bf68a58a8db3792a4ca0c684fb387` |
| Surface `tasks.md` | `9fdbbbc3042f59493bc1bb0d55812aafffdc5faef53005753126e5120df2b36e` |
| Surface `specs/surface-skill-selection/spec.md` | `314e658faf05d1daeda2545e342480ed37fcfbd4ed1af5d21933dff29a237094` |
| Surface `specs/surface-registration/spec.md` | `16f3e95d00b92ce85e987092651280c94e82c8e0ca04f6a3a09f5ed3fa50b534` |

### Independently recomputed main baselines

Paths relative to `openspec/specs/`:

| File | SHA256 |
|---|---|
| `dialog-registry/spec.md` | `ef9e52b7dba2ff4f0fa1dd1a9fa3d7cfaa78890277c376d70ed0301423bf6f83` |
| `dialog-selection-builder/spec.md` | `87d9ad1687832a1f1eb54a69b65d168cfe04a94fdc5bed1f95ea25983afc8ca6` |
| `surface-skill-selection/spec.md` | `e27eb8b354e4370da3519b5387cff5369a2f083e6c3be05f82d8631746c19ee0` |
| `surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| `surface-overview-connection/spec.md` | `51f9dc1a1d7b92ccdb059b7fda0117bf6c898378fa9a9fe185c7e2045044d193` |

Original complete row requirement, including trailing blank line: `19e49512a8bbef7aaa16288958d6284406e82b320fd975ef2406910d01db7526`.

## Execution boundaries

No file writes, scaffolding, tests, network, browser activity, delegation or git mutations performed. Tracked diff and staged-file listing were empty. This full report is returned for runtime persistence to the authoritative output path. Native scaffold/schema validation and parent API overlay remain separate.