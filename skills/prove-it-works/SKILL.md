---
name: prove-it-works
description: Verify a task result against the actual code, app, or artifact before claiming completion. Use when asked to prove a change works, check a fix, or validate a deliverable. Match the evidence to the claimed outcome and report failures or unverified parts explicitly.
---

# Prove it works

Check the result the user cares about directly. A plausible explanation, an agent's summary, or a successful build supports only what it actually demonstrates. Answer in the user's language.

## Define the claim

Read the task's acceptance criteria and repository instructions. State the observable result that would count as success, including behavior that must remain unchanged. Use the agreed requirement as the expected result, not the implementation's current output. If the requirement is ambiguous enough to change the verdict, resolve that ambiguity before calling it verified.

Identify the revision or working-tree state, artifact, environment, and inputs being checked. Confirm that the running app or built output corresponds to the change under review. Evidence from an older build does not verify the current change.

## Choose the smallest sufficient check

Prefer existing project checks and verification instructions. Match the check to the claim:

- CLI: run the actual command and inspect output, exit status, and relevant file effects.
- API or service: exercise the endpoint and check the response and promised side effects.
- UI: drive the affected journey in the running app and observe the action and resulting state.
- Persistence: perform the write through the supported interface and read back the stored value, including after reload or restart when durability is the claim.
- Library: exercise the public interface with representative inputs and assert observable results.
- Document or generated artifact: inspect the actual output and validate its relevant content, links, or rendering. A file existing is not proof that its contents are correct.

Run required repository checks as well. Build, lint, and unit tests provide useful evidence within their scope; do not present them as proof of a user journey they never exercise. Mocks establish behavior against the mocked contract, not that the real integration works.

Keep effort proportional to the change and risk. Do not create a broad harness or a brittle test merely to satisfy a ritual. A small repeatable script is useful when it makes the claim easier to check. For a trivial static edit, direct inspection and a relevant validation may be enough.

## Execute and inspect

Run the selected check and inspect its actual result. Capture the command or interaction, expected result, observed result, and relevant output or artifact path. Check that the intended code path ran and that an error, skipped action, stale screenshot, or cached result did not create a false pass. Inspect delegated evidence before using it in the verdict.

For a bug fix, reproduce the failure before the fix when practical, then run the same scenario after it. Use an isolated baseline checkout if needed; never discard the user's changes to reconstruct the old state. If a failing-before run is unavailable, say so and limit the claim to what the after check establishes.

For a behavior-preserving change, compare equivalent inputs and outputs before and after. For a performance claim, use comparable conditions and repeated measurements; do not claim improvement when the effect cannot be distinguished from noise.

When a check fails, inspect both the observation method and the target before deciding the cause. Do not weaken assertions, replace a baseline, or skip a required scenario to obtain a pass. Change an expectation only when evidence shows the intended contract changed, and explain that change.

If fixing is already authorized, make the scoped correction and rerun the affected checks. A verification-only request reports defects without editing product code. Recheck evidence invalidated by later edits. Stop once the claim and required checks are covered; expand only for a failure, new change, or unresolved risk. A missing capability or persistent blocker is a reported gap, not a reason to retry indefinitely.

## Respect the execution scope

Verification does not authorize deployment, production mutations, external messages, or destructive operations. Use disposable local state and existing authorization for runtime checks. If a necessary action exceeds that scope, complete the safe checks and request only the missing authorization. A substitute environment proves only what it actually exercises; name the difference.

Clean up only processes and scratch state created by this run. Preserve proof artifacts for review, keep secrets out of them, and follow repository conventions for whether checks or evidence belong in version control. This skill does not require a commit or PR.

Use the current environment's tools. No particular model, subagent API, configuration file, or sibling skill is required.

## Report the verdict

Lead with what was verified, failed, or remains unverified. For each material claim, give the check performed, its result, and the evidence needed to inspect or reproduce it. Keep a small task's report short.

Distinguish a demonstrated product failure from a check blocked by the environment. A blocked or inconclusive check is not a pass. Name unmet acceptance criteria and the next check needed, without asking the user to run something you can execute within the existing scope. Never declare the whole task verified while a required part remains unverified.
