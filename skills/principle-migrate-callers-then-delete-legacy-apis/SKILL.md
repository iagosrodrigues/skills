---
name: principle-migrate-callers-then-delete-legacy-apis
description: Replace an internal API by migrating its consumers and removing the obsolete path in one coordinated change. Use when consumers are controlled and compatibility does not require retaining the old contract.
---

# Migrate callers then delete legacy APIs

Establish who consumes the old API before replacing it. Inspect direct calls, public exports, dynamic dispatch, configuration, generated clients, persisted references, and independently deployed components. No static references does not prove no consumers exist.

Apply coordinated replacement when all affected consumers are under control and can migrate together. Define the replacement contract, update callers and relevant fixtures, and delete the old implementation and exports in the same coherent unit. Avoid leaving aliases, fallback branches, or adapters without a concrete compatibility obligation.

If external users, rolling deployments, stored formats, or independently released clients still require the old contract, preserve the necessary compatibility and plan a staged migration within scope. State the evidence and removal condition. Do not claim this principle requires breaking supported consumers or invent a compatibility layer for hypothetical ones.

Update tests to assert the intended supported contract. Retain regression coverage for behavior that remains required; remove tests only when their contract is explicitly retired or they exclusively encode replaced internals. A failing test is not sufficient evidence that it is obsolete. Read [test behavior, not implementation](../principle-test-behavior-not-implementation/SKILL.md) when that distinction is unclear.

Verify migrated callers through supported interfaces and check for residual old paths, including non-code references. Run relevant build or type checks as well as behavioral checks. If consumer coverage is uncertain, report it and defer deletion instead of claiming migration complete.

Keep the coordinated unit usable and preserve user work. This principle does not independently authorize a new public contract, data migration, or broad refactor. Report the consumers migrated, obsolete machinery removed, and any compatibility still required.
