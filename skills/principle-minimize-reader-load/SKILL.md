---
name: principle-minimize-reader-load
description: Evaluate structural complexity through the indirections a reader must trace and the mutable state they must understand. Use when a concrete flow is hard to follow or a proposed abstraction needs justification.
---

# Minimize reader load

Maintainability depends on what someone must understand to make a safe change. Inspect two independent costs: layers to trace and state to hold in mind. A flat file with many mutable globals can be as difficult as a stack of adapters. Line count and directory count are evidence of neither quality nor its absence.

Trace one real question, such as where a value comes from or what can change it. Show the files, handoffs, state owners, and hidden preconditions needed to answer it. Name the maintenance scenario affected before proposing a refactor.

- Collapse forwarding layers that add no policy, adaptation, or meaningful abstraction. One caller is a reason to inspect a wrapper, not proof it should be deleted.
- Prefer interfaces that hide decisions and complexity. A smaller signature that forces callers to coordinate internal steps may increase reader load.
- Shrink mutable scope: derive values where practical, return results rather than mutate distant state, and give invariants a clear owner.
- Keep a boundary when it protects a real contract, separate lifecycle, independent implementation, or external consumer.

For a proposed change, compare the same reader question before and after. State which handoffs or hidden assumptions disappear, which remain, and any new coupling. Verify affected behavior through its supported interface. Do not invent a numerical maintainability score or treat a time-to-understand estimate as a measured result.

This principle evaluates a scoped change; it does not authorize a repository-wide rewrite. If the current shape is clear and the proposed layer saves no understanding, leave it alone. Explain the concrete decision this principle changed, in the user's language.
