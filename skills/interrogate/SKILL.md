---
name: interrogate
description: Challenge a change or design by trying to reproduce failures against its intended behavior. Use for adversarial review, stress-testing a diff, or finding blind spots before shipping. Report confirmed defects separately from unproven risks; do not apply product fixes.
---

# Interrogate

Try to break the change, then verify each reported failure. A convincing explanation or agreement between reviewers does not establish a defect. Answer in the user's language.

## Establish the review target

Read repository instructions. Use the scope the user names. Otherwise identify the branch's base from repository or PR context and review the diff from its merge base through the current working tree. Include relevant staged, unstaged, and untracked files without collecting unrelated files or secrets. Do not assume the base branch's name; ask if different plausible bases would materially change the review.

State the intended behavior from the request, acceptance criteria, and relevant change context. Distinguish requirements from your interpretation. If ambiguity prevents deciding whether an outcome is wrong, resolve it before reporting a defect.

Record the base and target revisions and any uncommitted changes included in the review. A head SHA alone does not identify a dirty working tree. Keep a scoped snapshot or patch with the evidence when needed. If the target changes during review, identify the drift and repeat affected checks rather than applying an old verdict to new code.

## Isolate execution

Review does not authorize changes to product code, commits, pushes, merges, deployments, or external comments. Keep reproduction scripts and temporary tests in a separate scratch location or isolated checkout. Preserve the user's working tree. Do not reset, stash, or clean it to make a reproduction convenient.

When creating a review checkout, reproduce the scoped working-tree changes as well as committed code. Verify that the relevant files match the intended target before running checks. A checkout of the branch tip alone misses uncommitted changes.

Use disposable fixtures and isolate mutable resources such as ports, databases, profiles, and output directories. Run local checks within existing authorization. If a check needs unavailable access or an action outside that scope, complete safe inspection and report the gap or request the specific missing authorization. Do not trigger real external side effects to prove a hypothesis.

## Choose the reviewers

Use fresh reviewers independent of the implementation when subagents are available and their use is authorized. Choose distinct failure angles when they add coverage, such as input boundaries, state transitions, persistence, or affected callers. Do not force a panel for a narrow change.

Each reviewer receives the same intended behavior and exact target, its assigned scope, repository instructions, an isolated output location, execution boundaries, and the evidence contract below. Keep reviewers' conclusions separate until their investigations finish. Use the current environment's supported tools and model choices; no fixed vendor API, model identifier, or configuration file is required.

If independent review is unavailable, perform the review directly and disclose that limitation. If you authored the change, call the result self-review. A fresh reviewer using the same model can provide another investigation, but do not claim model diversity when there was none. Missing or failed reviewers leave explicit coverage gaps.

## Attempt failures

Trace the changed behavior and affected consumers. Use existing checks first, then a focused reproduction against real code when useful. Prefer reachable edge cases and concrete regressions over style, naming, speculative future changes, or unrelated cleanup.

For each candidate defect, capture:

- The violated requirement and realistic preconditions.
- The exact command or interaction, environment, and target state.
- The expected result and the actual output or observed state.
- The affected source location and user impact.
- A reproduction artifact and enough setup to repeat it.

For a change review, compare the same scenario against the base when practical. If it fails on the base too, report it as pre-existing unless the change introduces a newly reachable case or worsens the behavior. If the base cannot run, label regression attribution as unverified rather than guessing.

For a design or plan, use an isolated prototype or a probe of the existing code to test a specific assumption. State what that experiment establishes and where it differs from the proposed design. An unimplemented design with no executable evidence does not yield a confirmed implementation bug.

Do not modify the implementation to manufacture a failure, weaken the expected behavior, or treat environment startup errors as product defects. A scenario that cannot run remains unverified. Stop a line of investigation when further attempts need unavailable prerequisites or exceed the agreed scope; report the gap without inventing a finding.

## Verify and consolidate

Inspect each candidate's evidence and rerun its reproduction against the intended target before accepting it as a confirmed finding. For flaky failures, record attempts and observed frequency; a non-reproduction does not prove the candidate false, but it remains unconfirmed if you cannot validate it. Check that the failure violates the stated intent rather than an assumption introduced by the test.

Merge findings with the same root cause. Keep every independently verified defect, not only the list from one preferred reviewer. Reject disproven candidates and explain why. Put consequential but unexecuted risks in a separate, clearly unconfirmed section with the missing check; do not mix them into confirmed findings.

Clean up owned processes and disposable state, preserving reproduction evidence for review. Apply no product fixes. A later request to fix the findings is a separate task with its own scope.

## Report

Lead with the reviewed intent and target, then the findings ordered by impact. For each confirmed defect, give the source location, triggering conditions, expected and observed result, exact reproduction command or steps, and evidence path. State whether it is a demonstrated regression or whether attribution remains uncertain.

Say "no confirmed findings" when none survive. That means the performed checks found no confirmed defect; it is not a guarantee of correctness. Include the checks actually performed, unverified areas, material unconfirmed risks, and rejected candidates with reasons when present. Disclose whether the review was independent or self-review and any reviewer gaps. Keep the report proportional to the change.
