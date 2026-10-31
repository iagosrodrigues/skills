---
name: guide-me
description: Guide a project task from orientation through scoped planning, implementation, independent review, and evidence-based verification. Use when the user asks for an end-to-end workflow or help navigating an unfamiliar project, choosing the relevant bundled skills as the task progresses.
---

# Guide me

Help the user move from their current understanding to a verified outcome. State the goal and next concrete step in the user's language, then proceed within the authorized scope. Guide through explanations and visible evidence; do not require confirmation after every reversible step.

## Establish the task

Read repository instructions, inspect the working tree, identify relevant entry points and existing run or verification procedures, and clarify the expected outcome. Ask only for missing product choices, scope, or access that cannot be established from the project or a safe experiment. Preserve uncommitted user work.

Classify the work as orientation, investigation, bug fix, feature, refactor, design exploration, or verification maintenance. Use a short plan for nontrivial work, with verifiable units and a clear stopping condition. Scale effort to the task; a small edit does not require a design competition or full adversarial review.

## Route to the right workflow

Bundled skills are sibling directories. Resolve them relative to this file as `../<name>/SKILL.md`, read a selected skill before applying it, and include its absolute path in relevant delegate briefs. Load only skills needed for the current step. Do not send a subagent to recursively run this entire guide.

| Situation | Workflow |
| --- | --- |
| New contributor or unfamiliar subsystem | `how`: trace a representative flow, ownership, prerequisites, and verification commands. |
| Historical rationale, unexplained constraints, or a decision to revisit | `why`: investigate recorded reasons and tradeoffs before treating current behavior as evidence of intent. |
| Nontrivial architecture or ownership decision | `architect`: ground the design, explore distinct shapes, and synthesize usage and types. |
| Competing artifact approaches | `arena`: generate independently, judge, synthesize, and verify. |
| Independent task slices worth parallelizing | `swarm`: assign ownership, isolate writes and runtime state, integrate and check. |
| Adversarial review or consequential contested change | `interrogate`: reproduce candidate defects and distinguish confirmed findings from risks. |
| Redundant or misleading comments, prose-only constraints, or suppression cleanup | `no-comments`: independent comment review, scoped cleanup, and verification of affected directives or contracts. |
| Downstream compatibility or unclear impact beyond a diff | `blast-radius`: trace indirect consumers and execute checks of the critical safety assumptions. |
| Result ready to be claimed | `prove-it-works`: check the actual deliverable against acceptance criteria. |
| Missing reusable verification procedure | `create-verification-skill`, when creating that procedure is part of the requested work. |
| Stale verification procedure or feature map | `maintain-verification-skill`, when maintenance is in scope. |
| Demonstrated recurring agent mistake | `correct`: enforce prevention through structure or checks. It is not a generic fix-review-findings command. |
| Long, unattended, or multi-phase work needing a trail | `show-me-your-work`: canonical decision log, evidence audit, and independent review. |

If a sibling skill is unavailable, disclose it and perform the scoped task directly where possible. Preserve the distinction between direct execution and workflows requiring independent subagents; do not claim the missing workflow completed. Use supported runtime tools and model defaults, honoring explicit available choices without assuming personal model settings or vendor APIs.

## Code-quality and refactoring requests

For AI slop, structural maintenance concerns, or refactoring an established project, read [the code-quality workflow](references/code-quality.md). Start with concrete maintenance evidence, compare leaving the code alone with a scoped improvement, and preserve observable behavior. The reference routes to six canonical principle skills only when their decision is relevant; do not load the full set by default. A request to assess quality does not itself authorize a rewrite.

## Execute in verifiable units

For a bug, reproduce the reported behavior when practical, establish the intended contract, trace the cause, make a scoped correction, and repeat the scenario. Distinguish setup failures from product defects. For a feature, define observable acceptance criteria and the data shape before implementing. For a refactor, verify behavior remains equivalent through affected public interfaces. A design-only or read-only task stays within those bounds.

Delegate only independent work with self-contained briefs, target state, file ownership, execution boundaries, evidence expectations, and a completion condition. Never let concurrent workers silently share write paths or mutable app state. Review delegated outputs and run checks against the integrated result. Model agreement does not replace execution evidence.

When a check fails, inspect the target and the check before changing either. Do not weaken expectations, hide a regression in documentation, or extend the task into unrelated repairs. Repeated failures resting on one premise call for testing that premise, not another patch that assumes it. Keep retries bounded; report persistent blockers and complete unaffected work.

## Autonomy and checkpoints

Continue authorized local inspection, implementation, and verification without redundant approvals. Honor an explicitly requested design checkpoint or pause. This guide does not grant blanket access to external services, messages, publication, deployment, destructive actions, or unrelated configuration. Existing session authorization governs those actions; request only genuinely missing authorization when needed.

Keep commits and PRs optional unless requested. Do not automatically install hooks, model configuration, scheduled jobs, or an ongoing orchestration program. For a long task, leave progress and evidence sufficient for a fresh session to resume; record remaining units without claiming future work already completed.

## Hand off

Lead with the achieved outcome. Explain the material changes or findings, verification actually performed, evidence paths, outstanding blockers, and any decision the user must make. Clearly label source-derived, observed, and unverified claims. Stop owned processes and disposable state while preserving artifacts. Apply the trail's independent-review and Attention requirements when a decision log was used.

For a newcomer, include the concrete next coding location and relevant commands with known prerequisites. A successful unit or partial map does not prove the whole project. Finish when the requested outcome and required checks are complete, or identify precisely what prevents completion.
