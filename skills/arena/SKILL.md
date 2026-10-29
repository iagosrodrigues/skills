---
name: arena
description: Produce independent candidate artifacts with parallel subagents, compare them against a task-specific rubric, and synthesize a verified result. Use for design or implementation bakeoffs where competing approaches can improve the final artifact.
---

# Arena

Keep a phase checklist: frame, fan out, cross-judge, pick, graft, verify. Answer in the user's language. This workflow requires independent subagents; do not label direct execution an arena.

## Frame

Read repository instructions. Establish the requested artifact, authorized actions, target revision and relevant working-tree changes, and shared grounding. Derive three to six concrete grading criteria before spawning. Keep the judging rubric separate from candidate briefs; candidates receive the same requirements and constraints, without the picker's scorecard.

Choose at least two candidates unless the user explicitly requests one. Use supported model defaults and honor available user-specified choices. Different models are useful for judgment-sensitive work; independent runs of the same model are valid candidates, but not model diversity. Do not assume a vendor API, fixed model name, or personal model configuration.

Give each candidate its own output directory or isolated checkout matching the target, including scoped uncommitted changes. Candidates never overwrite one another or the user's working tree. Isolate mutable runtime resources too. Planning requests produce sketches; they do not authorize product edits. Publication and external actions require authorization beyond running this workflow.

## Fan out

Launch candidates concurrently within capacity, in waves if necessary. Each self-contained brief includes the goal, identical task contract, source grounding, repository instructions, target state, owned output, execution boundaries, verification expectations, and required artifact plus a short rationale explaining alternatives considered and rejected.

Ask candidates to develop independent approaches rather than converge on each other's work. Wait until candidate writing has finished before judging. Account for dropouts; continue useful work with surviving candidates but disclose when fewer than two completed. If delegation is unavailable, report that the arena could not run and label any direct work accordingly.

## Cross-judge and pick

Spawn a read-only judge after candidates finish. Prefer an available model family different from the coordinator's when supported; otherwise use an independent judge on the available default and disclose the absence of cross-model review. If no independent judge can run, disclose the missing review. Do not invent a model identity or diversity claim.

Give the judge the task, rubric, target context, and candidate paths under neutral labels. Request criterion-by-criterion scores, evidence, and a recommended base. The coordinator reads every candidate end to end and scores it independently while the judge works. Resolve disagreements by checking artifacts and requirements; agreement alone does not prove correctness.

Choose the base easiest to extend without violating invariants. In a tie, prefer clearer ownership and a smaller public interface that hides meaningful complexity. Record why the base won and what the rubric could not settle.

## Graft

Revisit each other candidate for useful ideas, typically one or two rather than most of its design. Adapt selected parts coherently into the base; inspect compatibility and invariants instead of mechanically pasting code. The coordinator owns synthesis and final integration.

When candidates converge, report the convergence; grafting is unnecessary. If divergence exposes conflicting interpretations, clarify or experimentally settle the contract before rerunning affected candidates. Do not average incompatible requirements. Bound reruns to resolving concrete failures; persistent uncertainty remains a reported gap.

## Verify and report

Verify the synthesized artifact against the task through the real interface where applicable. Run required repository checks and inspect observed results. For a design, validate usage/type consistency and integration assumptions, distinguishing source inspection from executable probes. Do not claim an unimplemented sketch passed runtime checks.

If verification exposes a missed candidate insight, revisit grafting; if the contract was wrong, reframe. Do not weaken acceptance criteria to obtain a pass. Stop owned processes, preserve evidence, and account for all workers. Leave candidate artifacts available for review without publishing them unless requested.

Deliver one synthesized artifact and a concise synthesis note with the rubric comparison, base and reason, judge verdict or missing review, each graft's source, rejected ideas and reasons, convergence or dropouts, and verification evidence or blockers. A partially verified artifact remains explicitly partial.
