---
name: code-gardening
description: Make bounded, behavior-preserving improvements to existing code using concrete maintenance evidence and the bundled code-quality principles. Use for code gardening, incremental cleanup, or reducing AI slop in a specific flow; honor assessment-only requests.
---

# Code gardening

Make the next realistic change easier and safer. Working code can merit structural improvement, but unfamiliar style, generated origin, line count, and a preference for elegance are not sufficient reasons to change it. No worthwhile change is a valid outcome.

## Choose a patch of ground

Read repository instructions, inspect the working tree, and preserve existing user work. Honor the requested scope and mode: assessment-only produces findings; an implementation request permits scoped local edits without another routine approval.

Start with the named module or flow. If none is named, inspect entry points, available recent changes, and verification instructions, then choose one representative flow and state the choice. Do not turn an open-ended gardening request into a repository-wide rewrite. Default to one coherent improvement per round unless the user requested a larger scope. Necessary callers and checks belong to that unit.

Trace a concrete maintenance question: where a rule changes, who owns a state transition, or how an input reaches an effect. Record the relevant locations, handoffs, state owners, and contracts. Distinguish a demonstrated defect, a source-backed maintenance obstacle, and a style preference. A realistic change scenario may be hypothetical; do not describe it as an observed incident.

## Select the improvement through principles

Read [minimize reader load](../principle-minimize-reader-load/SKILL.md) and [laziness protocol](../principle-laziness-protocol/SKILL.md). Compare leaving the code alone, a local correction, and a structural change. Choose the least machinery that removes the demonstrated obstacle. Prioritize value to the traced scenario, effort, and regression risk; do not fabricate scores or time savings.

Read additional principles only when their decision applies:

| Finding or decision | Principle |
| --- | --- |
| Obsolete paths, forwarding layers, or redundant machinery | [Subtract before you add](../principle-subtract-before-you-add/SKILL.md) |
| Synchronized flags, duplicated invariants, or unclear state ownership | [Model the domain](../principle-model-the-domain/SKILL.md) |
| Repeated validation, error translation, or trust assumptions | [Boundary discipline](../principle-boundary-discipline/SKILL.md) |
| Missing regression protection or tests coupled to internals | [Test behavior, not implementation](../principle-test-behavior-not-implementation/SKILL.md) |
| A failure or workaround whose cause is unclear | [Fix root causes](../principle-fix-root-causes/SKILL.md) |

The linked bodies are the source of truth; read them before applying them. Resolve sibling paths relative to this file. If a required skill is unavailable, disclose the gap and limit claims to the work actually performed.

Before editing, state the obstacle, the chosen intervention, the observable behavior to preserve, and how to check it. This is a short execution plan, not a mandatory approval gate. If evidence supports no useful intervention, explain why and stop without manufacturing a diff.

## Preserve contracts while gardening

When replacing an internal API, read [migrate callers then delete legacy APIs](../principle-migrate-callers-then-delete-legacy-apis/SKILL.md) to distinguish coordinated deletion from required staged compatibility.

Use existing focused checks to establish a baseline. Add a small behavior check when an exposed contract lacks meaningful protection and the change warrants it. Record pre-existing failures separately; a baseline failure does not authorize unrelated repairs.

Inspect consumers before removing code: static references alone miss dynamic registration, public exports, configuration, deployment variants, and external users. Preserve supported persistence formats, error semantics, authorization, ordering, and side effects. Lack of evidence of a consumer is not proof that a public contract is unused.

Implement the chosen unit. Avoid speculative frameworks, broad renaming, dependency churn, and formatting unrelated to the improvement. A discovered bug that requires changed behavior is a separate finding unless fixing it is already authorized; do not silently fold it into a behavior-preserving refactor.

Do not automatically sweep comments or tests. If strict comment cleanup is part of the requested scope, read [no-comments](../no-comments/SKILL.md) and follow its independent editing review and narrow keep list. Use [blast-radius](../blast-radius/SKILL.md) when indirect consumers make impact uncertain. If the improvement requires a consequential redesign beyond the chosen unit, report that opportunity instead of silently expanding the work.

## Review and verify the result

Review the diff against the promised obstacle and preserved contracts. Use [prove-it-works](../prove-it-works/SKILL.md) to run appropriate checks on the actual final state. Compare equivalent inputs and observable outputs before and after where practical. Do not weaken assertions or rewrite snapshots merely to make the refactor pass.

Trace the same maintenance question again. Show which handoffs, duplicated decisions, or hidden preconditions disappeared and what new coupling remains. Passing tests alone do not prove the change became easier to maintain; fewer lines alone do not prove behavior was preserved.

If the intervention fails its promised benefit, revise or undo only your own edits while preserving user work. For a persistent verification blocker, stop expanding the patch and report the unverified contract. If two attempted corrections fail the same check, read [attack the premise](../principle-attack-the-premise/SKILL.md) before another patch based on the same assumption.

Independent review is useful for a consequential patch when delegation is authorized. Give a reviewer the maintenance claim, preserved contracts, diff, and check evidence; require actionable findings. Review alone never substitutes for execution. For requested parallel work, use [swarm](../swarm/SKILL.md) to separate ownership and verify the integrated result; do not let agents concurrently edit the same flow without coordination.

## Finish the round

Report the improvement (or why no edit was justified), the before/after maintenance trace, checks actually run and their results, and remaining risks. Keep deferred opportunities brief and evidence-backed. Identify whether review was independent and what remains unverified.

Stop after the selected unit and its checks. Do not create a recurring job, commit, push, or open a PR unless authorized. Gardening is incremental maintenance, not permission to keep finding more work indefinitely.
