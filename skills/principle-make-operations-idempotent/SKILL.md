---
name: principle-make-operations-idempotent
description: Design commands, jobs, and lifecycle operations to converge safely after duplicate execution, retries, or partial failure. Use when repeatable mutations or crash recovery need an explicit contract.
---

# Make operations idempotent

Define the intended final state and what identifies the same logical operation. Distinguish a retry from a new legitimate action: two purchases can be intentional, while retrying one purchase must not create a second charge.

Derive steps from observable current state and apply the missing change. Include external effects in the contract, not just the final local record. Reading before writing is not sufficient under concurrency: use transactions, uniqueness constraints, conditional writes, or service-supported idempotency keys where the contract requires them.

Trace interruption points around durable writes, effects, and acknowledgments. A remote effect may succeed before the response or local completion record arrives. Reconcile against durable evidence or reuse the same supported idempotency key; do not blindly repeat an uncertain effect. Record deduplication scope and retention where their limits affect correctness. Do not promise exactly-once behavior without a mechanism that covers the full effect.

Make partial artifacts recognizable and recoverable. Temporary-file publication, resumable checkpoints, or transaction boundaries can help, but use their actual platform guarantees. A timestamp alone does not prove a lock owner is dead; use ownership or lease evidence and prevent stale owners from writing when needed. Do not delete ambiguous state or another process's work as recovery.

Verify a normal run, the same logical operation twice, and recovery from meaningful interruption points in disposable local state. For concurrent execution, check competing attempts as well. Inspect outputs and effect counts, not only return codes. Reason through remaining interruption points and label those not exercised; representative checks do not prove every crash was tested.

Use bounded retries with a stop condition. When outcome cannot be determined safely, report the uncertainty and required reconciliation instead of retrying indefinitely. This principle does not authorize production mutations, duplicate external effects, or expanding a local repair into a new job framework. Explain the convergence mechanism and what remains unverified.
