# Feature

Use for new or deliberately changed behavior. The coordinator owns the design, plan, review, and final verification. Delegate implementation with a concrete brief. A request for a proposal or design stops before implementation.

## 1. Trace the affected subsystem

Follow one representative journey through entry points, data ownership, state transitions, consumers, and existing verification. Define observable acceptance criteria and the smallest usable increment that works end to end. Identify product decisions that the code cannot answer; resolve those before dependent work proceeds.

## 2. Choose the data shape before writing logic

Name the domain model, its organizing structure, and the invariants it must enforce. Read [model the domain](../../principle-model-the-domain/SKILL.md) when choosing among a state machine, typed model, table, registry, or collection. Prefer an existing dependency or established project pattern when it meets the requirement.

For a nontrivial architecture or ownership decision, use [architect](../../architect/SKILL.md) to compare distinct designs and settle caller usage, types, and module boundaries. For a small feature with an established shape, record that choice directly. Build the simplest design that meets the full requirement, with useful end-to-end increments rather than scaffolding intended for replacement.

## 3. Record the throughput checkpoint

Keep these four items in the plan, including `n/a: <reason>` when an item does not apply. Update them at phase boundaries as dependencies become clearer.

- **Blocking first steps.** Name the contracts, decisions, or checks that must finish before dependent implementation starts.
- **Independent workstreams.** Identify work that can proceed independently, its owner, and its file or artifact boundaries.
- **Shared mutable state.** Identify shared files, services, databases, or running app state. Read [separate before serializing shared state](../../principle-separate-before-serializing-shared-state/SKILL.md) when workers could share writes. Split targets first; serialize only where an invariant requires it.
- **Smallest safe decomposition.** Choose the fewest owners that preserve clear review and integration. If one implementation worker is best, state why.

Keep a coupled feature under one implementation owner. That owner may split disjoint work after prerequisites pass. Coordinator-level fan-out is for independent artifacts, such as investigations or competing experiments, rather than fragments of one unresolved contract.

## 4. Delegate implementation and review the result

Give the implementation owner the goal, source locations, chosen data shape, acceptance criteria, file ownership, execution boundaries, required checks, and completion condition. Include paths to the selected skills. Use the active runtime's supported delegation tools and model settings. If delegation is unavailable or prohibited, disclose that limitation, implement directly, and perform a separate review pass without claiming independent review.

When materially different implementation approaches need comparison, use [arena](../../arena/SKILL.md) with isolated candidates and explicit judging criteria. Do not turn routine implementation choices into a competition.

Keep the working product usable as each increment lands. For dependent units, read [sequence verifiable units](../../principle-sequence-verifiable-units/SKILL.md) and check each prerequisite before starting the next. Check every affected consumer of a changed shared primitive.

When replacing an internal API, read and follow [migrate callers then delete legacy APIs](../../principle-migrate-callers-then-delete-legacy-apis/SKILL.md) for consumer discovery, coordinated replacement, and deletion criteria. Explicit user and repository instructions take precedence over its compatibility guidance. If they prohibit compatibility layers and discovery exposes consumers outside the coordinated change, establish the impact and authorized scope before deletion; do not add a wrapper or assume those consumers can be broken.

Review the actual diff against the brief and acceptance criteria before accepting the delegate's report. Resolve findings within scope and review the resulting changes again. For a consequential contested design, use [interrogate](../../interrogate/SKILL.md) before delivery.

## 5. Verify the integrated feature

Use [prove-it-works](../../prove-it-works/SKILL.md) against the integrated result on the surface the user will use. Exercise a UI journey for a UI feature, the real command for a CLI, or the public interface for a library or service. Run relevant existing checks and add behavioral coverage where it protects a meaningful new contract.

Compilation, an isolated worker's checks, or a mock of the affected boundary does not establish end-to-end success. Mark wrong-surface or inconclusive results explicitly. Record the observed outcome, evidence, and remaining gaps against each acceptance criterion.

## 6. Deliver

Report what changed for the user, the chosen design and its tradeoffs, the throughput checkpoint, verification evidence, and open decisions or blockers. Compare alternatives in a table when useful. Do not claim the whole feature complete when only one increment passed.

Commits, history rewriting, PRs, and publication follow existing session authorization. When delivery through commits or PRs was requested, keep units small and ordered by their verified dependencies. Completing this playbook does not itself authorize those actions.
