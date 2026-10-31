---
name: principle-separate-before-serializing-shared-state
description: Eliminate unnecessary shared mutation before adding synchronization. Use when concurrent agents or processes may write the same files, branches, records, or runtime state.
---

# Separate before serializing shared state

Inventory the actual mutable resources and their writers: files, Git indexes, branches, database rows, ports, caches, profiles, and remote objects. Different fields in one read-modify-write JSON file still share a write target. Separate checkouts can still share a database or external service.

First ask whether actors publish independent facts or must preserve one shared invariant. For independent facts, give each actor an owned file, key, checkout, or state directory and merge through an explicit integration owner or read boundary. Define collision handling and the consistency readers need; splitting storage must not break an invariant that requires atomic updates.

When one canonical mutable object is necessary, serialize access structurally using a single writer, non-overlapping execution phases, transactions, locks, or atomic compare-and-swap. Choose the mechanism for the actual contention domain. A process-local mutex does not coordinate separate machines, and an atomic file replacement alone does not prevent lost updates.

Ownership instructions help coordinate agents but do not themselves enforce mutual exclusion. Prevent overlapping writes through isolation or controlled scheduling; stop or drain an old worker before reassigning its target. Do not clear a lock merely because a worker appears slow. Account for failure and stale ownership where locks or leases are used.

Verify the conflict scenario with overlapping attempts or a controlled interleaving when practical. Check that independent updates survive, shared invariants hold, and readers observe the promised consistency. Recheck the integrated result: isolated successes do not establish that a merge works. Distinguish source-based reasoning from an executed concurrency check.

This principle guides concurrency design; it does not request subagents or authorize new workers, infrastructure, or changes outside the task. Explain which sharing was removed, which remains necessary, and how that remaining access is enforced.
