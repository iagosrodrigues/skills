# Design rationale checklist

Keep this proportional to the change and replace prompts with concrete project facts.

- **Problem and constraints:** intended behavior, existing integration, and source evidence.
- **Caller usage:** imports, realistic calls, results, and errors; write this first.
- **Shape:** core types, signatures, module map, state owners, boundary validation, and invariants. Explain which complexity the public interface hides.
- **Synthesis:** chosen candidate and why, judge result or limitation, grafted ideas with their sources, and rejected ideas.
- **Tradeoffs and alternatives:** structurally different options, the complexity each exposes, and why the selected shape fits better.
- **Risks and open decisions:** distinguish testable assumptions from product choices, with proposed checks.
- **Implementation and verification:** first step, migration needs, acceptance checks, and what has actually been run.
