---
name: principle-subtract-before-you-add
description: Sequence an authorized addition or refactor by removing proven obsolete or redundant structure before building on it. Use when existing complexity would otherwise be carried into a new design.
---

# Subtract before you add

Before extending a system, inspect what no longer needs to exist. Simplify the base where that directly serves the requested change. Removal requires evidence: an unfamiliar path, sparse tests, or no static references alone does not establish dead code.

Check callers, dynamic registration, public exports, configuration, deployment variants, and relevant documentation before deleting. Preserve supported compatibility, security checks, recovery behavior, and external contracts. A repeated validation may protect a different trust boundary; establish its purpose before removing it.

Sequence useful subtraction as a verifiable unit, then add the required capability. Keep removal and construction traceable even when they must land together to preserve a contract. Do not leave an unusable intermediate state in a shared environment.

Prefer observed usage over speculative extension points. Remove obsolete references rather than keeping empty stubs. For instruction files, remove redundant directives and templates only after checking the behavior or routing they provide.

Verify affected consumers after removal and the final behavior after construction. State what was removed, why it was safe, and which complexity no longer carries forward. If removal is uncertain or unrelated, defer it and complete the scoped task. This principle does not authorize destructive cleanup of user data or unrelated work. Explain the decision in the user's language.
