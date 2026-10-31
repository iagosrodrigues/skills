---
name: principle-attack-the-premise
description: Test a shared assumption when two or more attempted fixes fail the same acceptance check. Use to interrupt repeated patching based on an unverified cause, without turning the investigation into an unrelated redesign.
---

# Attack the premise

When two or more fixes rely on the same assumption and fail the same acceptance check, write down that assumption before another fix. Repeated failure is reason to test the premise, not proof that it is false. Answer in the user's language.

Record what each attempt changed, the target state and check actually run, and what failed. Confirm that the attempts exercised comparable conditions and the intended code. Stale builds, missing setup, different inputs, or a faulty check can mimic failure of a sound premise.

State the shared assumption in a falsifiable sentence. Choose an observation that would differ if it were wrong. Define the predicted results and their interpretation before running the probe. Prefer the smallest real-code check or targeted instrumentation that distinguishes explanations. Look at which inputs, timings, states, or consumers fail, not only the aggregate count.

Run the discriminating check within the task's permissions and preserve its evidence. Use disposable fixtures or an isolated checkout rather than resetting the user's work. A mock that assumes the disputed premise cannot establish it. An unobserved or inconclusive outcome remains unproven.

- If evidence contradicts the premise, stop proposing fixes that depend on it. Investigate the common conditions the old explanation missed.
- If evidence supports it, trace the causal chain further using [fix root causes](../principle-fix-root-causes/SKILL.md). The attempted corrections may have addressed a consequence or omitted another necessary condition.
- If the check or environment is invalid, repair the observation method within scope and repeat the relevant comparison.
- If the premise cannot be tested with available access, report the blocker and any safe independent work. Do not present another speculative patch as a validated correction.

Prefer correcting the demonstrated condition over adding repeated compensation when the contract allows it. Retain legitimate safeguards and compatibility requirements. Consult [laziness protocol](../principle-laziness-protocol/SKILL.md) when choosing the smallest coherent correction. This principle challenges an assumption; it does not by itself justify replacing the architecture.

Before resuming implementation based on that premise, record the probe result and revised conclusion. If the user explicitly asks for a provisional mitigation while investigation is blocked, label its purpose and limitations and verify what it can establish. Report the premise, discriminating check, observations, and resulting next step. Bound further attempts to concrete evidence instead of an indefinite patch loop.
