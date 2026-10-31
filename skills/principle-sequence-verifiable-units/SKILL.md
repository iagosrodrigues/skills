---
name: principle-sequence-verifiable-units
description: Break multi-step changes, sweeps, and migrations into coherent units with explicit checks before dependent work continues. Use when execution or delivery order affects the ability to localize failures and review evidence.
---

# Sequence verifiable units

Choose units by contracts and dependencies, not by an arbitrary file or line count. Each unit should leave a coherent state that can be checked, including the callers or fixtures needed for that state. Group inseparable edits instead of publishing an unusable intermediate step.

Establish the actual baseline: revision, relevant uncommitted work, environment, and check result. Preserve user changes. Do not automatically rebase, reset, stash, or rewrite history to obtain a clean starting point. Record pre-existing failures and determine whether they block the evidence needed for this unit.

For each unit, state the expected result, perform the scoped change, and run its relevant check before starting dependent work. A sweep can use meaningful batches when per-edit execution adds no useful evidence; the batch must still allow a failure to be localized. Do not apply an entire unchecked sweep and call its final test incremental verification.

Order evidence so the causal claim is reviewable: capture a baseline before changing behavior, remove obsolete structure before extending it where safe, or reproduce a failure before fixing it. A red-before/green-after demonstration may occur in a temporary experiment or within one commit. Do not require failing tests to land separately or conflict with repository rules that commits must pass.

When commits or PRs are authorized, arrange them as reviewable units with their checks and dependencies. This principle does not require commits, publication, a PR stack, or branch rewrites. Independent units may proceed in parallel only when already authorized and isolated; validate their combined state before declaring completion.

On a new failure, inspect the current unit and its check before proceeding with dependent changes. Fix within scope or report a blocker; do not weaken the check or continue building on an unverified prerequisite. Rerun evidence invalidated by later changes, then check the integrated outcome with [prove it works](../prove-it-works/SKILL.md).

Report completed units, checks actually performed, and any incomplete dependency. Distinguish observed verification from a planned delivery sequence. Stop when the requested outcome and required checks are complete.
