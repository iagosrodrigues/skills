# Evaluate code quality through maintenance evidence

Use for requests about AI slop, overengineering, difficult maintenance, or refactoring an established project. Honor audit-only scope. Begin with one representative flow or a named pain point; expand only when findings justify it.

## Establish value before changing structure

Use source and available project history to name a concrete maintenance task or defect affected by the structure. Trace its callers, handoffs, state owners, and verification. Separate a demonstrated failure, a structural maintenance cost, and a style preference. A bug is not required to justify simplification, but the maintenance claim needs source evidence.

For each worthwhile finding, record the affected locations, a realistic change scenario, the current obstacle, and the smallest correction. Compare leaving it alone, a local change, and a structural change. Do not fabricate recurrence, saved hours, or a quality score. Prioritize a few opportunities by impact, expected effort, and regression risk; no finding is an acceptable outcome.

Read only the relevant principles:

| Evidence or choice | Principle |
| --- | --- |
| Too many handoffs or hidden mutable context | [Minimize reader load](../../principle-minimize-reader-load/SKILL.md) |
| Choosing local correction versus another abstraction | [Laziness protocol](../../principle-laziness-protocol/SKILL.md) |
| Obsolete machinery carried into a new design | [Subtract before you add](../../principle-subtract-before-you-add/SKILL.md) |
| Flags or branches duplicating domain invariants | [Model the domain](../../principle-model-the-domain/SKILL.md) |
| Scattered checks or unclear trust transitions | [Boundary discipline](../../principle-boundary-discipline/SKILL.md) |
| Brittle tests or uncertain regression protection | [Test behavior, not implementation](../../principle-test-behavior-not-implementation/SKILL.md) |

## Make a bounded improvement

When implementation is authorized, choose a coherent unit and state the behavior that must remain equivalent and the maintenance obstacle to remove. Capture a useful baseline through existing checks. If coverage is insufficient, add the smallest meaningful behavior check before changing structure.

Keep compatibility, dynamic entry points, persistence, authorization, and operational requirements visible. Use `architect` for a consequential change in ownership or public boundaries; do not launch an architecture competition for every cleanup. Use `correct` only for demonstrated recurring mistakes or explicit prevention work.

After the change, repeat the behavioral check and trace the same maintenance scenario. Show which coordination, duplicated decision, or hidden dependency disappeared, and whether new coupling was introduced. Smaller files or fewer lines alone do not prove improvement. If the proposed shape increases complexity without the promised benefit, revise or remove only your own change while preserving user work.

Report the concrete gain, preserved behavior and evidence, tradeoffs, and remaining opportunities. Avoid a repository-wide beautification sweep, automatic test deletion, or a claim that AI-generated code is defective because of its origin.
