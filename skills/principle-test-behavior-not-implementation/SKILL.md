---
name: principle-test-behavior-not-implementation
description: Design or assess tests against observable contracts, so behavior regressions fail and harmless internal refactors pass. Use when choosing assertions or evaluating brittle or ineffective tests.
---

# Test behavior, not implementation

A test protects what an end user, caller, or external system can observe: returned values, errors callers handle, persisted state, outgoing effects, or documented invariants. Derive the expected result from the requirement, not the current implementation or data the test fabricated without exercising the code.

Judge a relevant test against two changes:

1. Break the promised behavior: return a wrong result, omit an effect, or perform it twice. Would the test fail for that reason?
2. Preserve the contract while restructuring internals. Would the test still pass?

Use concrete inputs through a supported interface and assertions precise enough for the contract. An empty list is the exact answer when nothing matches, but a weak assertion if the fixture never exercised matching. Expected values computed by the same code under test can repeat its mistake.

The contract determines whether an interaction is behavior. A payment client receiving no charge for an empty cart can be the behavior; pair it with a charging case to show the observation detects calls. The exact sequence of private helpers is usually implementation. A required ordering, error message, protocol payload, or compile-time invariant is behavior when consumers actually depend on it.

Use focused negative or mutation probes when they materially establish test sensitivity, in isolated temporary changes or fixtures. Do not damage the user's working tree to demonstrate a failure. Label the two-change assessment as reasoning unless you actually ran the probes.

Repair ineffective assertions and brittle coupling within scope. Investigate consumers before deleting tests; small unit checks and mocks can protect a real contract, but do not establish a live integration passed. Add tests when they protect meaningful behavior, not to mirror trivial edits. Report what was exercised, what broke under a probe, and what remains unverified, in the user's language.
