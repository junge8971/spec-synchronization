## Context

See proposal.md for motivation and evidence. This short design records the distinction between two transitions that share the same target status and resolves the notification-versus-dialog ambiguity before implementation.

`use-dictionary-editor-handlers.ts` snapshots the current editor state before calling `performDictionaryLifecycle`, updates confirmed state after success, and currently calls `notifySuccess('Статус сохранён.')`. `model/dictionary-lifecycle.ts` already validates the returned UUID and requested status, classifies rejected/unknown outcomes, and applies owner/abort guards. `use-dictionary-lifecycle-actions.ts` preserves dirty-edit decisions and confirms deletion only. `shared/ui/notifications/use-operation-notification.ts` supplies the existing one-at-a-time operation toast with context/unmount protection. Component tests already render the notification provider.

## Goals / Non-Goals

**Goals:** Select a truthful action label at the existing confirmed-success point and prove it is visibly rendered with the shared notification infrastructure.

**Non-Goals:** No new notification framework, state machine, API, status transitions, confirmation dialog, consumer integration, auth change or general notification redesign. Do not treat the screenshot as evidence of a reproduced rendering failure.

## Decisions

1. **Reuse the existing success call, not an additional UI channel.** Replace the generic lifecycle success title using the existing operation notification hook. A new modal contradicts the clarified requirement and the operation-feedback spec; a second toast or inline success would duplicate feedback. Preserve the existing inline downstream caveat because it is context, not a duplicate success.
2. **Use the pre-request snapshot plus the validated target.** Draft to active means activation; paused to active means resumption; active to paused means pause. Reading only the returned active status cannot distinguish activation from resumption. Keep message selection local to the optional module; if named runtime text constants are introduced, place them under its `constants/` segment rather than expanding shared code.
3. **Keep all success guards in their existing order.** Announce only the updated outcome after UUID/status and owner checks. Do not announce on pending, error, unresolved, refetch or reconciliation observation. Keep write locks and dirty Save/Discard/Stay untouched. A preceding successful dirty save remains its own operation, but must not be mistaken for status success if the subsequent transition fails.
4. **Verify rendered feedback rather than only mocking the notifier.** Extend `ui/detail/dictionary-editor.test.tsx` with all three transitions, delayed and rejected responses, mismatched success responses, dirty continuation/cancellation, repeat clicks and stale completions. Reuse shared notification accessibility tests rather than redesigning the provider. Local mock Playwright MCP checks should exercise visible titles, error absence of success, and keyboard dismissal after separate explicit authorization required by AGENTS.md. The broader browser allowance in openspec/config.yaml is not treated as permission to bypass that restriction; record an authorization or availability blocker if applicable. No automated E2E suite changes or external UI checks are included.

## Risks / Trade-offs

- [Activation and resume both return active] -> Select wording from the captured source status, not the updated card.
- [A generic toast already exists, but deployed visibility was not reproduced] -> Assert actual rendered notifications and perform authorized local visual checks; do not claim the deployed issue is verified from source inspection alone.
- [A prior save notification could obscure whether lifecycle succeeded] -> Assert absence of lifecycle-specific success while status is pending or failed, and one status notification after confirmation.
- [Wiki describes downstream suppression when paused] -> Retain the approved stored-status boundary and existing caveat; no consumer-effects claim is added.

## Migration Plan

No data or API migration is needed. Deliver the local message change and regression tests together. Rollback restores the generic status notification without changing persisted data or lifecycle semantics.
