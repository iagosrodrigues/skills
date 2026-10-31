---
name: reflect
description: Review a session with three independent lenses, identify durable workflow lessons, and propose evidence-backed changes to existing skills. Use when asked to reflect on agent execution or improve skills from observed friction; ordinary progress capture is not reflection.
---

# Reflect

Turn demonstrated execution problems into a small set of decision-changing improvements. Answer in the user's language. A reflection request produces proposals; apply changes only when the user authorizes the selected edits. Honor explicit authorization already provided instead of requesting it again.

## Establish the session evidence

Read repository instructions and identify the session the user means. Use its explicitly available transcript, current conversation, authorized observations, and artifacts. If no transcript is accessible, prepare a concise digest with concrete prompts, actions, outcomes, corrections, and evidence pointers. Label omissions and uncertainty; do not treat a digest as a complete record.

Do not assume a transcript directory or search unrelated conversations. If project memory is available and needed, use its existing retrieval workflow and exact project/session scope. Reading session evidence does not authorize consolidation, durable memory writes, consuming handoffs, or modifying memory routing.

Distinguish a durable lesson from a typo, transient environment failure, one-off preference, or a rule already followed correctly. A trivial session or one with no justified improvement can end with no findings; do not manufacture edits to satisfy the workflow.

## Run three independent reviews

Launch three read-only subagents in parallel within runtime capacity, using waves if necessary. Give each the same session evidence, repository instructions, accessible skill paths, task scope, and [the review contract](references/review-contract.md), assigning one lens:

- **Judgment:** decisions, corrections, scope choices, and repeated friction that could change future execution.
- **Tooling:** avoidable manual work, missed available retrieval, reusable technical constraints, and opportunities for executable enforcement. A tool being available does not prove it could access the needed context.
- **Divergent:** unsupported assumptions, omitted verification, downstream effects, and alternatives that complicate the obvious lesson. Do not require contrarian findings when evidence supports none.

Reviewers inspect evidence and referenced context, not write files or external records. Select supported tools that retain needed read access. Follow the project's shared model and effort policy where available; different lenses do not require different model families. Do not claim model diversity from same-model reviewers.

If a reviewer fails, record missing coverage. If delegation is unavailable, complete useful direct analysis and disclose that the three-reviewer process did not run. Do not silently present self-review as independent review.

## Synthesize and route

After collecting results, use a fresh read-only synthesizer with all findings, the original evidence, and [the synthesis criteria](references/synthesis.md). It must inspect proposed target skills before accepting edits and spot-check material evidence. The coordinator verifies the synthesis before presenting it. Direct synthesis, if required by unavailable delegation, carries an explicit limitation.

Route a body edit to an existing workflow actually used in the session, or a description change to a visible skill that demonstrably missed its intended trigger. Do not infer invocation merely because the agent ran a generic shell command. Propose a new skill only for a recurring pattern with no suitable existing owner.

Prefer structural enforcement when a lint, type, script, metadata field, or runtime check can reliably prevent the problem. Put that implementation in Backlog rather than adding a redundant prose rule. An execution failure despite clear existing guidance is not automatically a defect in the skill.

## Present concrete proposals

Return Accepted, Rejected, and Backlog, with evidence and reasons. Accepted means recommended for application, not approved by the user. For each Accepted row show the observed failure, the exact proposed replacement or addition, the canonical destination and section, and the behavior a future agent should change. Prepare the proposed text before requesting approval; drafting in scratch does not require editing the installed skill.

Resolve source ownership before editing. Do not edit generated plugin caches or copy cached skills into new discovery roots by default. Locate the maintained source; if its destination is genuinely unknown, explain the missing information. Never silently shadow an installed skill with a competing copy.

For reflection-only requests, ask which concrete proposals to apply. For already-authorized edits, apply the scoped subset directly. Keep backlog items in the report unless the user requests filing them externally. Do not create tickets, send messages, commit, or push simply because a reflection produced an actionable item.

## Apply and verify authorized changes

Re-read the target before applying an approved proposal and preserve intervening user edits. Make the smallest correction that changes the demonstrated decision. Use an available skill-authoring workflow for substantive edits or new skills; otherwise follow the repository's conventions. Do not turn one incident into an unrelated universal restriction.

Validate touched skill structure and references. Where the change affects routing or judgment, exercise a realistic scenario that would expose the original issue, and label simulated reasoning separately from actual runtime execution. Existing lessons already expressed clearly should not be duplicated.

Report applied paths and what changed, remaining proposals, rejected findings and reasons, structural backlog, verification performed, and review gaps. A no-change result is valid. Preserve evidence and distinguish proposed, authorized, applied, and verified states.
