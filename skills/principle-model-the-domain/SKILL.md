---
name: principle-model-the-domain
description: Choose data structures and ownership that express actual domain states, transitions, and access patterns. Use when stateful logic accumulates synchronized flags, duplicated rules, or branching across files.
---

# Model the domain

Start with what must always be true, the valid transitions, who owns each change, and how callers read the data. Choose a structure that expresses those facts instead of distributing them across conditions.

Useful choices include a discriminated union or state machine for mutually exclusive states, a typed model for meaningful values, a registry for real keyed dispatch, a reducer for coordinated transitions, or an index suited to a demonstrated access pattern. These are options, not a checklist of structures to introduce.

Organize modules around knowledge and invariants they own. Execution stages such as load, validate, and save do not automatically define independent owners. Keep one authoritative representation of a fact and derive secondary views where practical.

Before adopting a new model, walk realistic caller usage and at least one invalid transition through it. Show which invalid combinations, duplicated rules, or lifecycle risks it prevents. A map that hides arbitrary business branches is not automatically better than a clear conditional.

For a migration, inspect persisted data and external consumers as well as in-memory callers. Preserve required compatibility and define how existing states convert. Do not claim compiler enforcement for states that still enter through unchecked casts or unvalidated inputs.

Prefer boring, local code when the existing shape is clear. Add structure only when it reduces a concrete domain problem; verify observable behavior after the change. Explain the invariant and the decision it changed in the user's language.
