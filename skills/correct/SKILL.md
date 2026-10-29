---
name: correct
description: Prevent recurring agent mistakes in a repository with architecture, types, actionable lint checks, or behavioral tests. Use when the user asks to address repeated corrections or make a known mistake harder to repeat. Prove the enforcement catches the actual mistake; use documentation for remaining judgment calls.
---

# Correct

Turn repeated corrections into enforceable repository constraints. Assume a contributor may see only a few files, copy the nearest example, and take the shortest path that compiles. Make that path lead to correct behavior. Answer in the user's language.

## Establish the recurring mistakes

Read repository instructions, the user's corrections, and relevant recent commits, reverts, tests, and workaround comments. Use review history when it is available within existing access. Cite concrete occurrences; count a mistake class as recurring only with at least two distinct occurrences. An explicit request to prevent a first occurrence is valid, but label it preventive rather than inventing history.

Group occurrences by root cause, identify the intended contract and current enforcement, and prioritize the most frequent or consequential classes within the requested scope. A review suggestion or present implementation alone does not establish the contract. If evidence is insufficient, report the gap instead of creating speculative rules.

Keep the work proportional to the demonstrated pattern. Preserve unrelated changes. The task authorizes scoped repository corrections and local verification, not unrelated redesign, external writes, commits, pushes, or PRs unless separately requested. An audit-only request produces recommendations without edits.

## Choose the strongest practical enforcement

For each class, work down this order and explain why a higher level is unsuitable when choosing a lower one:

1. **Architecture.** Give state one owner and a task one supported path. Hide internals behind module boundaries, replace hand-synchronized lists with one source of truth, and remove obsolete examples after checking their consumers. Prefer eliminating the opportunity for error over checking it repeatedly. Avoid disproportionate migrations for a narrow mistake.
2. **Types.** Represent valid states and transitions so the bad state cannot be expressed through the supported interface. Do not conceal the problem with casts, unchecked escape hatches, or permissive types.
3. **Lint or CI checks.** When bad code still compiles, add a focused check whose diagnostic names the supported file, type, or function and the corrective action. For widespread legacy violations, use an explicit baseline or changed-code boundary that rejects new violations without silently grandfathering them in later runs.
4. **Behavioral tests.** Assert the user-visible contract through a stable interface. Verify that the test fails when that behavior breaks and survives harmless implementation changes. Repair ineffective relevant tests rather than adding assertions that merely repeat the implementation.
5. **Documentation or agent instructions.** Reserve prose for judgment calls that cannot usefully be enforced. Place guidance where contributors actually discover it. A written rule is not a mechanical guardrail.

Use existing tools and repository conventions. Do not require a particular agent runtime, model, sibling skill, or new framework for this workflow.

When choosing between a local correction and more machinery, consult [laziness protocol](../principle-laziness-protocol/SKILL.md). When adding or assessing regression protection, consult [test behavior, not implementation](../principle-test-behavior-not-implementation/SKILL.md). Read a selected principle before applying it and connect it to the actual failure class rather than appending generic rules.

## Fix and prove

Correct the scoped instances and add the selected enforcement. Keep each mistake class reviewable as a coherent change; make separate commits only if commits were requested.

Prove the guardrail rejects a real recorded mistake. Reproduce the historical pattern in an isolated checkout, disposable fixture, or negative compilation case without resetting, stashing, or corrupting the user's working tree. Capture the command, failing result, and actionable diagnostic. A failure caused by missing setup or unrelated code does not prove the guardrail works.

Run the same check on the corrected state and confirm it passes. Include a valid neighboring case when needed to show that legitimate behavior is accepted. For architecture or type changes, exercise affected callers and show the forbidden path is inaccessible or rejected. Run relevant repository checks and required validation after the final edits.

If CI enforcement is part of the solution, wire the same reproducible command into existing CI and run it locally. Do not claim remote CI passed unless observed. When the historical case cannot be reconstructed, state that limitation; a representative synthetic case is supporting evidence, not proof against the actual past mistake.

Do not weaken expectations to obtain a pass. Any unavoidable exception must be narrow, explain its reason and review or expiry condition, and follow repository approval conventions. Do not invent human approval or add a broad bypass. Stop at a persistent blocker and report which correction or enforcement remains unverified.

## Maintain the rule table

Use the repository's existing agent instruction file or its canonical shared reference to keep a compact rule-to-enforcement table. Follow existing discovery conventions; avoid competing instruction files or duplicating the same table across runtimes. If no location is established, propose one and resolve the destination before creating it.

For each retained rule, name the invariant and concrete enforcement location or command. Label judgment-only rules as unenforced. When an existing rule has been broken again, investigate why its enforcement did not catch the mistake and repair that gap. Remove obsolete reminder rules once the architecture makes the mistake impossible, retaining the explanation where the architectural boundary is maintained.

This skill governs the current correction task. It does not install hooks, schedule future runs, or establish a new permanent approval policy. Recommend using the same loop when another recurring correction is identified.

## Report

For each class, give its occurrence evidence, root cause, chosen enforcement level, why higher levels were unsuitable, changed locations, and failing-before and passing-after evidence. Distinguish mechanical prevention from detection and prose guidance. Include remaining exceptions, blockers, and checks not run. Do not claim a mistake is impossible when a check only detects it later.
