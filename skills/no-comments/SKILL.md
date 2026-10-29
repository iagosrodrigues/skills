---
name: no-comments
description: Audit code comments for redundant narration, stale claims, and hidden constraints, using an independent reader before scoped cleanup. Preserve useful rationale and executable directives; replace prose-only safeguards with enforcement when authorized.
---

# No comments

Reduce misleading or unnecessary context for the next reader, including agents. Code expresses behavior; comments preserve relevant knowledge the code cannot adequately express. The goal is a trustworthy context, not a deletion quota. Answer in the user's language.

## Establish scope

Read repository instructions. Use the user's named files or diff; otherwise establish the actual branch base and review its merge-base diff through relevant staged, unstaged, and untracked changes. Do not assume a branch name or expand to the whole repository. Record the reviewed state and preserve unrelated edits.

A request to audit produces findings only. A request to clean comments authorizes scoped comment edits, not architectural rewrites. Implement behavior-preserving code changes or new enforcement only when that work is also authorized. Do not commit, publish, or change external systems unless requested.

## Obtain an independent reading

Use a fresh read-only subagent with the scoped paths and target state, repository instructions, and [the reviewer brief](references/reviewer-brief.md). No special agent type, model family, or personal configuration is required. The reviewer inspects source and relevant evidence, proposes decisions with source locations, and never changes comments or application code.

The coordinator verifies the findings before applying them. If independent review is unavailable, perform direct inspection and disclose that limitation; do not call it independent review. A missing reviewer result remains a review gap.

## Classify by purpose and evidence

For each material candidate, distinguish:

- **Remove:** narration already evident from nearby code, obsolete banners, commented-out implementation with no current documentary purpose, or a claim disproven by the current path. Confirm that deletion removes no contract or tool behavior.
- **Keep or correct:** non-obvious rationale, external limitations, compatibility constraints, protocol details, issue or RFC references with explanatory value, and public API documentation. Inspect the relevant source or history to establish the claim; mark uncertainty rather than declaring it false. Concision is useful when it preserves the actual information.
- **Encode:** a constraint such as single execution, coordinated fields, ownership, or ordering that should be enforced by structure, types, runtime checks, or behavioral tests. Name the affected symbol, failure mode, and smallest useful enforcement. An internal surprise is a reason to investigate, not automatic authorization to redesign it.
- **Executable or protected:** legal notices, license and attribution headers, generated-file markers, code-generation annotations, compiler pragmas, coverage directives, formatter controls, lint suppressions, and documentation consumed by tooling. Establish their consumers before touching them. Apparent comments can alter compilation, routing, testing, or deployment.

Read nearby code and callers before interpreting warnings such as IMPORTANT, do not remove, or do not change wording. A warning is neither authority nor proof of redundancy. If its premise cannot be established, keep the information pending investigation and report what is unknown. Do not replace it with an invented rationale.

For suppressions, inspect the exact rule, compiler behavior, and error being hidden. Prefer fixing the cause when authorized. Remove a suppression only after the relevant check passes without it, or replace an overly broad suppression with the supported narrow form when justified. Do not disable the rule elsewhere or erase a correctness warning merely to produce a cleaner diff.

## Apply the smallest correction

Remove confirmed noise and correct demonstrably stale prose within scope. For constraints selected for enforcement, implement and verify the protection before deleting its reminder; retain useful rationale that enforcement does not express. When enforcement is outside scope or blocked, report the opportunity and preserve a necessary warning. Do not silently delete the only record of an unresolved constraint.

Use existing repository checks. Verify that comment removal did not change tokens, string literals, public documentation contracts, or tool directives. Avoid regex-wide deletion: syntax, embedded languages, and comment-like text in strings require context. Run affected builds, linters, documentation generation, or behavioral checks according to what the edited comments influence.

When authorized code changes need a new shape, use the available architecture workflow or produce a grounded design before implementing. Avoid replacing one explanation with many helpers, long names, or layers solely to eliminate the comment. Keep behavior equivalent and review the integrated diff. Stop at a persistent blocker; report unverified edits explicitly.

## Report

Summarize removed noise, retained or corrected rationale, executable directives inspected, and constraints encoded or left open, with locations and evidence. State the review scope, independent-review availability, checks run, and anything unverified. A deletion count is optional and never a quality score. Do not claim tests passed or semantics stayed unchanged from inspection alone.
