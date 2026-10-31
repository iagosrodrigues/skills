---
name: swarm
description: Coordinate parallel subagents across distinct task slices or competing approaches, collect their evidence, and return one consolidated result. Use when the user requests a swarm, parallel coverage, exploration, or a race between approaches.
---

# Swarm

Coordinate a bounded group of subagents through framing, execution, aggregation, and reporting. Keep a short phase checklist using the environment's planning tool or run notes. Answer in the user's language.

## Frame

Read repository instructions. State the completion condition and expected artifact or report. Establish the authorized scope, worker count, resource limits, and whether workers inspect, verify, or implement. Parallelism does not expand permission to edit, publish, or use external services.

Choose a shape:

- **Partition:** distinct slices whose results together satisfy the goal.
- **Race:** identical goals with independent approaches.
- **Mixed:** partition the task and race selected slices.

For races, declare the selection rule before launching: first verified pass, rank all, or best-of. Define acceptance and ranking criteria. A fast worker's PASS label is not itself a verified pass. Avoid racing against a shared implementation or mutable app instance.

Use supported subagent tools and current model defaults. Honor explicit model choices when available; disclose unavailable choices and any substitution. Claim model diversity only when workers actually use different models. No personal configuration file, vendor-specific API, sibling skill, or fixed model identifier is required.

Subagents are required for a swarm. If unavailable, report the limitation and complete useful direct work within scope, clearly labeled as direct execution rather than a swarm.

## Assign ownership and evidence

When workers may share a mutable target, read [separate before serializing shared state](../principle-separate-before-serializing-shared-state/SKILL.md) before choosing isolation or synchronization. Include resources outside the checkout in that decision.

Give every worker a self-contained brief containing:

- Goal, completion criteria, repository and relevant instructions.
- Exact slice or race arm, permitted actions, exclusions, and dependencies.
- Target revision and relevant working-tree changes; exact commit SHAs for commit comparisons.
- Verification procedure, required evidence, and result format.
- Owned write paths or isolated checkout, scratch output location, and mutable-resource boundaries.

For measurements, define the method in advance: sample count, what constitutes a sample, execution order, and comparable environment. Require workers to record target revisions and method with results. Include uncommitted changes in the target snapshot when they are part of the task; a checkout of HEAD alone does not include them.

For implementation, give workers disjoint file ownership or isolated checkouts. Agree on shared interfaces before dependent edits; the coordinator owns shared files and final integration. If a worker discovers it needs another worker's paths, have it report the dependency instead of editing across ownership. Never reset, stash, or discard the user's working tree to isolate workers.

For live verification, isolate ports, databases, profiles, accounts, and outputs. Where isolation is unavailable, serialize the driving under one owner. Concurrent measurements that compete for resources are not comparable evidence.

## Fan out and drain

Launch independent workers concurrently up to the environment's limit, using waves for remaining work. Do not assume a particular cloud or local execution mode. Select a supported environment that has the required repository state and resources; do not push a branch just to make it available without authorization.

Each worker reports **PASS**, **ISSUES**, or **BLOCKED**, with evidence paths, performed checks, target state, changed files when applicable, and unresolved gaps. A worker reports every defect it can substantiate within its slice. A blocker is not a product defect or a pass.

Track worker completion, failures, and missing slices. Resolve dependencies before starting affected work. If a worker drops out, continue unaffected work and record the gap. Do not duplicate active write ownership while replacing a worker.

For a first-pass race, verify the leading result before selecting it, then cancel or drain the remaining workers through supported tools. For rank-all or best-of, collect every required arm or disclose missing comparisons. Account for every launched worker and owned resource before finishing; stop owned processes while preserving evidence.

## Aggregate and integrate

Read terminal results and inspect material evidence. Reject unsupported success claims. If a result omits the required revisions or measurement method, request a corrected result or rerun that slice once. After another miss, record an explicit gap. Stale evidence must be rerun against the intended target.

For coverage, every required slice needs a supported result. For races, apply the declared selection criteria consistently. Do not change the criteria to favor a preferred answer. Merge duplicate findings by root cause while retaining distinct proven defects and conflicting evidence.

For implementation, inspect each worker's diff, integrate only scoped changes, resolve interface conflicts, and run checks on the combined state. Passing slices do not establish that their integration works. Preserve independent user edits and avoid importing unrelated worker changes. Keep each candidate isolated until selected in a race.

If required evidence, integration checks, or slices remain blocked, report partial completion rather than declaring the whole task passed. Do not silently expand the swarm into unrelated repairs.

## Report

Return one consolidated answer with the goal, overall outcome, and a compact table of slices or arms, worker status, verified outcome, and evidence. Include proven issue summaries, integrated artifacts or changed locations, checks actually run, missing coverage, dropouts, and cleanup status. Name the race rule and selected result when applicable. Summarize findings instead of pasting raw worker dumps.
