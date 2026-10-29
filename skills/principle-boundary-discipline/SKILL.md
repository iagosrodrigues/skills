---
name: principle-boundary-discipline
description: Place validation, translation, and error handling at real trust and system boundaries, with explicit domain contracts inside. Use when wiring external inputs, adapters, or repeated defensive checks.
---

# Boundary discipline

Identify where trust, representation, ownership, or failure semantics change. CLI arguments, configuration, network payloads, persisted data, plugins, and public library calls can be boundaries even when they run in one process.

Parse external values into a validated domain representation at each actual entry path, including non-HTTP and untyped callers. Give errors a useful contract, translate them at the appropriate edge, and keep transport, storage, and framework details behind adapters unless they are the intended public interface. Keep business decisions independent of framework wiring where that makes them easier to exercise.

Inside a validated domain, rely on established invariants instead of repeating the same check in every consumer. That reliance requires evidence: static types do not validate runtime input, prevent unchecked casts, or protect an invariant after mutation. Untyped callers, deserialization, stale data, extension points, and concurrency can require another boundary or invariant check.

Do not remove authorization checks, transaction constraints, or protections at distinct trust boundaries merely because input was parsed earlier. Parsing a valid identifier does not authorize an operation. Handle legitimate runtime failures where recovery or propagation belongs; pure domain code can still return meaningful errors.

For a change, trace one input from raw form through domain use and one invalid or failing case back to the caller. Identify where each invariant is established and who preserves it. Verify rejection at the boundary and valid behavior through the supported interface. Avoid scattering guards or claiming unconditional internal trust without that trace. Explain the concrete boundary decision in the user's language.
