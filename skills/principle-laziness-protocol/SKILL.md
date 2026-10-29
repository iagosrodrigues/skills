---
name: principle-laziness-protocol
description: Choose the smallest coherent change that solves a demonstrated problem, especially when refactoring or considering new abstractions, configuration, or layers.
---

# Laziness protocol

Minimize the work the system and its future maintainer must keep doing. Prefer deletion and consolidation when they solve the actual problem. The smallest correct change is not necessarily the fewest edited lines: a tiny workaround that preserves duplicated policy can cost more than a coordinated correction.

Identify the requirement or observed maintenance cost. Consider leaving the code as it is, a local correction, and a structural change before choosing the least machinery that satisfies the contract.

- Consolidate a repeated decision under one owner instead of synchronizing it across callers. Choose a flag, domain value, or operation according to the real meaning; do not introduce flags that permit contradictory states.
- Reuse an existing supported path before adding a helper, option, registry, framework, or compatibility layer.
- Prefer a few explicit statements over a speculative abstraction. Extract when a clear policy boundary, meaningful concept, shared invariant, or concrete variation justifies it; a single caller does not invalidate that purpose.
- Include necessary caller migration and verification in the scope. Do not minimize a diff by leaving the original fault elsewhere.

Justify added machinery by the complexity it removes now. Verify the requested outcome and affected contracts, and report deferred opportunities separately. Do not turn aesthetic preference into an acceptance criterion or expand a small fix into unrelated cleanup. Explain the concrete choice in the user's language.
