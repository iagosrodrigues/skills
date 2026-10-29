# Candidate design brief

The coordinator supplies the task, repository instructions, grounded source paths, target state, isolated output, and action boundaries. Produce one candidate; do not invoke the orchestration workflow recursively.

Write caller-facing usage and realistic call sites before types. Derive the signatures and module structure from that experience. Use pseudocode or explicitly unimplemented bodies in the sketch, without changing product code unless assigned.

Describe core data structures and dominant access patterns. Identify validation boundaries, state ownership, error contracts, retry or crash behavior, and concurrency where relevant. Derive repeated lists from one source of truth. Keep transport and storage representations behind domain interfaces unless exposing them is an explicit contract.

Compare complexity hidden by the public interface against complexity left to callers. Avoid layers that merely forward parameters. Make the flow traceable through types, signatures, and ownership.

Return the sketch, module map when needed, rationale, a structurally different alternative and why it lost, integration risks, and how the proposal could be verified. Do not claim a prototype or runtime check was executed unless it actually was. Develop your own best shape without reading other candidates.
