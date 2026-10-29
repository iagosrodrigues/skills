---
name: architect
description: Ground a nontrivial change in existing code, explore structurally distinct designs with subagents, and synthesize caller usage, types, signatures, and module boundaries before implementation. Use when architecture or ownership decisions need deliberate design.
---

# Architect

Track grounding, sketching, agreement when requested, implementation when authorized, and redesign when evidence requires it. Answer in the user's language. Scope follows the request: a design-only task ends with the design package; an implementation task continues against the selected sketch without an unnecessary approval checkpoint.

## Ground

Read repository instructions and trace the affected flows, callers, state owners, interfaces, and checks. Use the bundled `how` skill when available, or perform that source-grounded investigation directly. Existing ownership rationale needs historical evidence; do not infer motivation from current code alone. Skip this phase only for genuinely greenfield work without surrounding integration.

Identify the desired behavior and constraints, including compatibility and migration needs. Mark unresolved product decisions separately from facts that can be learned through source inspection or a small authorized experiment. Avoid asking the user to decide an empirical question that can be tested.

## Design principles

Read only the principle relevant to the decision at hand: [model the domain](../principle-model-the-domain/SKILL.md) for state and access patterns, [boundary discipline](../principle-boundary-discipline/SKILL.md) for validation and adapters, [minimize reader load](../principle-minimize-reader-load/SKILL.md) for interface complexity, or [subtract before you add](../principle-subtract-before-you-add/SKILL.md) when replacing existing structure. Pass selected principle paths to candidate runners. Explain the specific design choice they changed; do not require every principle for every sketch.

## Sketch independently

Explore at least two structurally distinct candidates through parallel subagents. Use the bundled `arena` workflow when available; otherwise give independent readers the same grounded task and isolated output locations, compare them against explicit criteria, and synthesize one design. Different names inside the same shape do not count as alternatives. If delegation is unavailable, disclose the limitation and label direct alternatives as unreviewed by independent candidates.

Pass [the candidate brief](references/candidate-brief.md) with the task, grounding, output path, and boundaries. Each runner produces caller usage first, then derives types, signatures, ownership, and pseudocode. Candidate runners do not recursively launch another arena. Screen all candidates using [design red flags](references/design-red-flags.md) before choosing a base.

Prefer a small interface that hides substantial complexity. Concentrating capability in a module is different from spreading a call chain across many layers. Validate external data at boundaries, model domain invariants in types where supported, and keep state under clear ownership. Isolate concurrent writers before adding synchronization.

Produce a design package using [the rationale checklist](references/rationale.md). A small change may need one sketch file; larger work needs a module map and type definitions. Keep incomplete scaffolds in design artifacts or isolated candidate outputs unless actual source scaffolding is authorized. Do not leave the user's working implementation broken merely to show a sketch.

## Agree and implement

When the user explicitly requests a checkpoint, present the synthesized package and wait before implementation. Otherwise continue only if implementation is already in scope. A plan request alone does not authorize product changes, commits, or publication.

Implement against the sketch's behavior and interfaces. Surface material deviations with the evidence behind them. Resolve routine details directly; ask only for a product choice or required authorization that the current task does not establish. Rerun affected checks after changes, including integrated callers and realistic behavior. A compiling scaffold does not prove the feature works.

## Redesign when warranted

Repeated workarounds, unrelated edge cases needing the same special branch, unchecked type escapes, unexpected shared state, or callers depending on internals can indicate a wrong shape. Two independent deviations of the same kind deserve investigation; one ordinary edge case need not invalidate the design.

When the pattern is real, re-ground in what was learned, redesign as if those constraints were known initially, subtract obsolete structure, and repeat independent design exploration. Preserve useful work and user edits; scrapping a sketch never authorizes resetting or discarding their working tree. Stop at a persistent blocker rather than indefinitely reopening design.

Report the chosen shape, alternative comparison and synthesis, material deviations, implementation status, verification evidence, and unresolved decisions. Distinguish a reviewed design from a runtime-verified implementation.
