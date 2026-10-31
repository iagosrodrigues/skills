---
name: benchmark-checklist
description: Validate performance measurements before reporting a speedup, regression, or choosing an implementation. Check actual work, correctness, bottlenecks, comparable tuning, repeatability, and end-to-end relevance using run evidence.
---

# Benchmark checklist

Make the claimed performance result reproducible and explain what it actually measures. Answer in the user's language. Use observed evidence, not an assumption inferred from code alone.

A user-requested rough estimate may use one run, labeled as such, after confirming correct output and actual work inside the timed region. A comparison used to choose an option or claim an improvement requires the fuller procedure below.

## Define the measurement

Read repository instructions and the harness before running it. Write the claim to be tested, the decision it would inform, and the observable workload. Name the metric, unit, timed boundaries, dataset, concurrency, warm or cold state, and practical effect worth detecting. Identify what the harness excludes.

Record exact versions or commit SHAs, relevant uncommitted changes, dependencies, build flags, environment, and commands for each side. Ensure running artifacts match those targets. Preserve the user's working tree; use isolated checkouts and disposable data when needed.

Inspect machine load and available CPU, memory, storage, and runtime resources using tools supported by the operating system. Do not assume Linux commands exist. Do not stop another user's processes to obtain a quiet machine. Record interference, interleave comparable runs, and report a blocker when contention prevents a meaningful result.

Use authorized local resources. A benchmark request does not authorize production load, billable cloud jobs, real external side effects, or publishing results. Resolve missing authorization for such actions while completing safe preparation.

## Check seven questions

1. **What limits it?** Profile a separate diagnostic run; do not mix profiler overhead into reported timings. Use suitable runtime profiles or system counters and map the limiter to a source path or resource. Check the load generator as well as the target. An unchanged result may mean the edited code was not the bottleneck. If the limiter is unknown, keep observations but mark causal or optimization conclusions inconclusive.

2. **Are configurations comparable?** Use appropriate release builds, production-relevant flags, versions, data, batching, transaction boundaries, pools, and cache conditions. Record intentional differences. A default or untuned side supports a comparison of those configurations only. For an adoption recommendation, tune relevant settings or explicitly leave the choice unresolved; do not generalize one poor configuration to the entire implementation.

3. **Does the arithmetic make sense?** Compare reported work with resource ceilings and measured time shares. If a component accounts for fraction p of baseline elapsed time, eliminating it entirely saves at most p of total time, giving a maximum speedup of 1/(1-p), under the same-work assumptions. Distinguish latency reduction from throughput increase. Unexpected results require investigation of caches, skipped work, parallelism, units, and correctness before acceptance.

4. **Did it produce correct results?** Count successful work, errors, rejected requests, retries, and timeouts. Verify actual output and relevant effects, not just file existence or exit status. A fast failure must not count as successful throughput. If the harness omits these observations, add an authorized focused check or report the measurement as inconclusive.

5. **Does it reproduce?** For a comparison, normally run at least five measured repetitions per side, after explicit warmup where appropriate. Alternate or counterbalance order so drift does not consistently favor one side. Reset disposable state consistently. Report raw samples, count, median, and range; distinguish a median across runs from a request-level percentile within a run. When variance prevents distinguishing the effect, report no measurable difference under these conditions or an inconclusive comparison. Use appropriate harness statistics when available; do not treat five runs or a significance test alone as proof.

6. **Does it matter to the user?** Pair microbenchmarks with the end-to-end path and realistic scale or concurrency before claiming a user-visible improvement. Report the changed component's share of total time. If the full path cannot be measured, keep the conclusion scoped to the microbenchmark and name the missing check.

7. **Did the work actually happen inside the timer?** Confirm requests reached the target, writes completed, bytes were consumed, and results were used. Await asynchronous work, consume lazy iterators, and prevent dead-code elimination using the established harness. Exclude neither essential setup nor completion silently. A dry run, cache hit, timeout, or unconsumed promise may measure a different workload.

## Preserve the experiment

Keep commands, configuration, raw samples, correctness and work counts, and profiler evidence in a reviewable artifact. Exclude secrets and sensitive input data. Separate diagnostic runs from measured ones. If a harness changes, rerun both sides under the same revised method rather than comparing incompatible samples.

Do not weaken correctness assertions to obtain a favorable number. Tune or repair benchmark setup within scope, but report product defects rather than silently expanding into fixes. Bound repetitions and diagnosis by the requested scope and available resources; persistent instability is a result to disclose, not an invitation to run indefinitely.

Stop owned processes and remove only owned disposable state while preserving evidence. A local artifact does not need to be committed or published unless requested.

## Report

Lead with faster, slower, no measurable difference under the tested conditions, or inconclusive. Attach the metric and units, baseline and candidate values, run counts, variation, workload, configuration differences, and identified limiter. State whether the conclusion is end-to-end or local to a component.

Explain what was verified, observed errors, evidence location, and any missing question. When work execution or output correctness cannot be established, the measurement is inconclusive. Distinguish a measured configuration difference from a proven cause or recommendation. For a short report or PR, use one primary result and link the detailed evidence rather than hiding caveats behind a percentage.
