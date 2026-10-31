---
name: principle-fix-root-causes
description: Trace a failure from its visible symptom to the earliest demonstrated contract violation and correct it within scope. Use when debugging or deciding whether a guard, retry, or workaround fixes a legitimate state or hides the source of an invalid one.
---

# Fix root causes

Reproduce the failure when practical, establish the expected behavior, and trace the actual state backward to where the system first violated that contract. A plausible explanation or a disappearing symptom alone does not establish the cause. Answer in the user's language.

Use observed inputs, errors, transitions, and outputs. When evidence is missing, add focused instrumentation or a small repeatable probe within authorization. Avoid collecting secrets. If reproduction is blocked, state the hypothesis and missing evidence rather than presenting the diagnosis as confirmed.

Ask whether the triggering state is legitimate:

- If the contract permits it, handling it at the appropriate boundary may be the complete fix. Empty results, transient failures, cancellation, and retries can be normal conditions.
- If the state violates an invariant, trace who produced or failed to protect it. Silently clamping, discarding, swallowing, or retrying can conceal the fault while leaving other consumers exposed.
- If the boundary's trust or availability model requires defensive handling, retain that protection even while correcting an upstream cause. A mitigation can be useful, but label it separately from a demonstrated causal fix.

For restart-only failures, inspect persisted configuration, caches, locks, and serialized state alongside startup logic. Treat these as hypotheses to test, not a predetermined diagnosis. Concurrent failures may have multiple contributing conditions; do not force a single cause when evidence shows several.

Inspect similar paths for the same demonstrated fault. Fix authorized instances and report those outside scope. Root-cause work does not authorize a broad rewrite, production mutation, or deletion of user data. A long explanatory comment may expose a workaround worth investigating, but its length does not prove the code is wrong.

Verify the causal claim with a focused before/after scenario where feasible, then exercise legitimate neighboring cases and affected consumers. Use isolated reproduction state and preserve unrelated changes. Remove obsolete workarounds only after establishing that their protection is no longer needed. Do not weaken the behavioral expectation to obtain a pass.

If the decisive fact was difficult to observe, propose a low-cost diagnostic signal that would expose it earlier, with appropriate data and operational limits. Add it only when in scope. Report the observed fault, causal evidence, correction or mitigation, verification, and remaining uncertainty. A diagnosis-only request ends with evidence and recommendations.
