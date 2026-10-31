---
name: blast-radius
description: Investigate what a change could break beyond its diff and execute focused checks of the assumptions its safety depends on. Use for impact analysis, downstream compatibility, or a small change with unclear consequences.
---

# Blast radius

Trace consequences beyond direct callers and test the assumptions that determine whether a change is safe. Answer in the user's language. A caller list or convincing explanation alone does not establish compatibility.

## Anchor the change

Read repository instructions and establish the requested diff, proposal, or symbols. Identify the actual base and target revisions and relevant staged, unstaged, and untracked changes; do not assume a branch name. Record which state the analysis and checks cover. For a proposal without implementation, distinguish hypothetical effects from observed behavior.

Read changed definitions and their consumers, including deleted paths and implicit behavior changes. Use `how` for an unclear runtime flow and `why` for historical constraints when available. A historical motivation does not prove present safety.

Impact analysis authorizes inspection and appropriate local verification, not product fixes, publication, deployment, or production mutations. Keep reproduction scripts in a scratch location or isolated checkout, preserve user changes, and use disposable fixtures. Honor an explicit read-only request by reporting checks that require execution beyond its scope.

## Identify the critical assumptions

State the one or two facts that would resolve the most consequential risks, such as whether eviction has side effects, whether old readers tolerate a new field, or whether cleanup can race a pending callback. Wide changes may have several independent assumptions; do not force them into one blanket safety claim.

Trace realistic failure paths beyond symbol search:

- Inspect the actual pinned dependency version and any local patches, not a different release's API description.
- Follow lifecycle and ordering: initialization, retries, queued work, cancellation, teardown, restart, and concurrent readers or writers.
- Inspect serialized data, storage schemas, public APIs, wire formats, other languages, feature flags, configuration, and deployed-version compatibility where affected.
- Trace indirect consumers, dynamic registration, generated code, and downstream effects until the relevant contract is clear.

Use concrete preconditions and source evidence. A search with no hits describes that search, not proof that an external or dynamic consumer cannot exist. Mark unavailable consumer code or environment details as gaps. Assess likelihood qualitatively from reachability and impact; do not invent probabilities or callers.

## Prove the assumptions

For each critical fact, record the strongest evidence actually obtained:

1. **Unproven:** a hypothesis without sufficient support.
2. **Source-grounded:** exact implementation or contract locations support the claim.
3. **Path-analyzed:** a traced failure scenario cannot reach the bad state under explicit preconditions.
4. **Executed:** a focused check calls the actual code or pinned dependency and fails if the claimed behavior is false.
5. **Observed in the app:** the realistic journey reproduces or clears that specific scenario in the running target.

These levels describe evidence, not a guarantee covering all inputs. Prefer a small executable probe through the real interface for material assumptions. Run existing suitable checks before introducing helpers. Capture setup, command, target state, expected and observed results, and evidence paths. Assert side effects where they matter; a successful exit alone may not establish the contract.

Compare against the base when practical to establish whether a failure is new. Use isolated state without resetting or stashing the user's work. If the base cannot run, label regression attribution uncertain. A missing dependency or failed startup is a blocked check, not proof of a product defect. A mock or substitute environment proves only its modeled contract.

For a broad or cross-cutting change, use independent subagents to investigate the same critical questions, with isolated outputs and a shared target. Use the available `arena` workflow when its candidate comparison helps. Same-model independent review is valid; disclose unavailable model diversity or delegation. Inspect all returned evidence and verify material claims before synthesis.

Stop at persistent blockers and report what remains unproven. Recheck evidence invalidated by target changes. Clean owned processes and disposable state while preserving reproduction artifacts. Do not silently turn discovered risks into an implementation task.

## Report

Explain what changed, the critical safety assumptions and their evidence levels, confirmed defects with triggering conditions and impact, unresolved risks, and scenarios checked and cleared. Include source locations and actual reproduction commands or evidence paths. Distinguish a confirmed failure from a plausible risk and from a historical pre-existing issue.

End with the smallest remaining check needed before relying on the change. If all scoped checks passed, state what they establish and the boundaries of coverage. Never label the entire change safe merely because one assumption or one scenario was verified. Keep private data out of any artifact intended for sharing; do not publish without authorization.
