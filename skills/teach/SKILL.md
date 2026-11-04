---
name: teach
description: Teach a change or subsystem through a plain, evidence-backed explanation of what it is, how it works, and why it took its current shape. Use when the user wants to understand a body of work at their own pace; compose how and why rather than implementing changes.
---

# Teach

Help the person understand the work well enough for their purpose. Infer their familiarity, goal, and useful depth from the conversation: preparing a change, reviewing, debugging, or learning the project. Skip what they already know. Ask only when the target is too ambiguous to investigate usefully; do not start with a knowledge quiz.

This is an explanation workflow. Read repository instructions and inspect the target without editing product files, installing dependencies, starting services, or mutating external state. Use runtime observations only within existing authorization. If teaching is part of a broader authorized implementation task, complete the explanation and then return to that task.

## Ground the explanation

Read the relevant entry points or diff to orient the investigation. Select a few things the person should understand and keep the research bounded to those questions.

Read and apply [how](../how/SKILL.md) for current mechanics and [why](../why/SKILL.md) for historical rationale. These are actual investigations under their own contracts, not names to mention or conclusions to invent from the current code. For a subsystem, use both. A narrow question may need only one when the other adds no useful information.

For independent how and why questions, run read-only subagents in parallel when available, within the runtime's capacity. Give each the user's question, repository and target revision, relevant uncommitted changes, the absolute skill path, scope, read-only boundaries, and expected evidence. Respect why's investigator and independent-synthesis requirements; allow waves rather than oversubscribing workers or recursively launching teach. If delegation is unavailable, perform useful direct investigation and disclose the missing independence.

Keep why narrow by default: ask about a specific decision, its Git history, and one or two relevant sources. Its coverage map must still account for skipped or unavailable categories. Widen on concrete leads or when historical rationale is the user's main question. Reuse already collected evidence that still matches the target instead of repeating the research.

Check material claims and citations before combining the findings. Preserve why's confidence language: a documented reason, an inference, and an unknown remain different after simplification. Explain present-day usefulness separately from author intent. Do not imply a command or test ran because its source was inspected.

## Teach at the person's pace

Start with the common name and a plain definition, then connect it to this project. Give the smallest complete answer first, usually one or two sentences for an open conversational request. Build the explanation around the actual mechanism and the problem it solves. Follow one concrete input, user action, or state transition instead of listing functions and constants.

In conversation, stop at a useful point and let the person guide the next layer. Do not quiz them, demand that they repeat an explanation, print pacing labels, or announce that a part is difficult or important. If they explicitly request a complete walkthrough or the task is one-shot, deliver that scope in one coherent response instead of withholding required content behind follow-up questions.

Use inspectable code excerpts, a diff, or diagrams where they make the mechanism clearer. When teaching several interacting parts, build the picture progressively: begin with the smallest useful relationship, then add a component or transition while retaining the previous context. Prefer a short series when one large diagram would overload the explanation; do not redraw a trivial flow just to meet a quota.

Use Mermaid for flows and ownership when labels carry the meaning. For spatial behavior such as overlap, layout, or scroll position, use an available visual tool or a clear annotated sketch suited to the environment. Follow the tool's instructions. Do not require a particular image generator or pretend an illustration is runtime evidence. A simple point needs no figure.

## Deliver the explanation

Apply [unslop](../unslop/SKILL.md) to the prose. Write in the user's language, with ordinary sentences and one consistent name per concept. Remove filler and stock framing while retaining the causal mechanism, uncertainty, and citations. Prefer short sentences to a dense paragraph or an outline full of labels.

Return the explanation itself, not a report about running skills. Keep source references beside material claims and state limitations where they affect understanding. Preserve the selected skills' required evidence and coverage disclosures, presenting them compactly after the main explanation when needed. Do not dump raw investigator reports into the lesson.

End at the requested depth. An optional next thread should arise from the explanation, not a generic offer or a compulsory exercise. If a required sibling is missing, disclose that and explain only what the available evidence supports; do not claim its investigation completed.
