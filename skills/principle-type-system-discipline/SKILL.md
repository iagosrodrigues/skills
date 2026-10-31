---
name: principle-type-system-discipline
description: Use static types to reject invalid domain states, mismatched semantic values, and unhandled variants. Apply when designing typed models or signatures, or reconciling them with authoritative schemas.
---

# Type system discipline

Make the compiler enforce demonstrated domain distinctions. Read [model the domain](../principle-model-the-domain/SKILL.md) when valid states or ownership are unclear; types should express those decisions rather than disguise uncertainty.

Use distinct semantic types for values that must not be interchangeable, such as UserId and OrderId. Prefer the language's supported newtypes, opaque types, or branded types and validated constructors. Apply this where confusion violates a real contract, rather than wrapping every primitive mechanically.

Represent mutually exclusive states as explicit variants and handle them exhaustively. Keep related state under one owner instead of allowing callers to synchronize flags. Do not bypass enforcement with unchecked casts, broad escape types, or fabricated default cases.

Derive shapes from the authoritative schema when one exists. Reuse existing generation or inference facilities before adding a pipeline, and do not hand-edit generated files. Keep transport shapes and domain models distinct when they express different contracts, with explicit translation between them.

External data remains untrusted until parsed: JSON, configuration, network messages, persisted records, and untyped callers. Read [boundary discipline](../principle-boundary-discipline/SKILL.md) to locate validation. Static types do not authorize access, validate deserialization, or protect an invariant after uncontrolled mutation.

Verify the intended enforcement with the project's type checker and a focused invalid-use check when warranted. Exercise valid caller usage and relevant invalid runtime input as well. Do not claim compile-time protection in a language or path that cannot enforce it. Report the invalid case now rejected and the remaining runtime responsibilities. Keep migrations within the authorized scope.
