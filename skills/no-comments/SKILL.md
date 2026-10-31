---
name: no-comments
description: Apply strict comment cleanup with an independent editing reviewer, a narrow keep list, and scoped root-cause fixes. Delete comments that do not qualify, flag internal surprises for restructuring, and report constraints that remain unenforced.
---

# No comments

Default to deletion. A comment stays only when a specific keep-list exception is established. Internal complexity should be corrected in code rather than defended in prose. Answer in the user's language.

## Establish scope

Read repository instructions. Use the user's named files or diff; otherwise establish the actual branch base and review its merge-base diff through relevant working-tree changes. Record the target state. Preserve unrelated user edits and stay inside the requested scope.

Invoking this cleanup workflow includes comment edits and the smallest in-scope root-cause fixes for accepted findings. Honor an explicit audit-only request by reporting proposed deletions and fixes without editing. Publication, commits, external writes, and out-of-scope redesign are not implied.

## Independent editing pass

Spawn a fresh subagent with [the strict reviewer brief](references/reviewer-brief.md), repository instructions, exact scoped files, and the target state. Give it exclusive ownership of scoped comment edits or an isolated checkout matching that state. The reviewer may edit comments and identify application-code targets; only the coordinator edits application code. Do not run simultaneous writers on those files.

Use supported delegation tools and the project's model/effort choices. No vendor-specific agent type is required. If independent review cannot run, report that the strict workflow is incomplete; do not silently substitute self-review.

## Inspect the report and diff

Reject application-code changes by the reviewer, scope escapes, deletions protected by an established keep exception, unsupported `MUST KILL` reasons, and findings that condemn intentional behavior legitimately covered by an exception. Inspect scoped lint and type-check suppressions for missed correctness or safety violations.

Restore a deleted comment only with a concrete keep-list exception and scoped evidence. Do not restore internal-workaround explanations simply because the underlying code still needs fixing. Investigate thin IMPORTANT or do-not-remove claims through source and, when necessary, history using available `how` or `why` workflows. If a keep remains ambiguous or is refuted, delete it. Ambiguity after investigation is not a keep reason.

For a rejected pass, undo only the reviewer's rejected edits, preserving pre-existing work, and rerun once with the failure explained. After a second rejected pass, report the strict workflow as failed with open findings. Never reset the user's working tree to retry.

## Correct accepted findings

Fix trivial accepted targets directly, such as a dead path, obsolete parameter, or misuse of an existing API. For findings that require a different shape, run the available architecture workflow once for the accepted set and surrounding code, stopping at a sketch before implementation. If unavailable, produce an equivalent grounded sketch and disclose the missing workflow.

Implement the smallest root-cause correction within scope. Remove named workarounds rather than adding symptom guards or rewording their justification. When the true cause is outside scope, implement only a justified in-scope correction and report remaining work. Do not claim a workaround is fixed when only its comment was removed.

For correctness or safety suppressions, remove the suppression and address the flagged code. Do not replace it with another broad bypass. Run the relevant check; a remaining failure is open work and prevents a successful verdict. Preserve genuine negative type-test assertions only when their test contract establishes that purpose, rather than treating production error suppression as a test.

## Handle constraint comments

For constraints such as do not remove, do not change wording, or talk to someone first, retain only proven keep-list exceptions about constraints the project cannot reshape. Otherwise offer the cheapest useful type, runtime check, behavioral test, or lint that encodes the constraint.

Show the concrete encoding and its scope before requesting approval, unless the user already authorized that work. If approved, encode, verify, and delete the comment. If not approved or outside scope, delete the non-exempt comment anyway, report the constraint as unenforced, and describe the remaining work. Audit-only requests report this action instead of applying it. Never present an unenforced constraint as mechanically protected.

## Verify and report

Inspect the integrated diff and run checks appropriate to changed code, suppressions, public documentation, or tool-consumed directives. Parse syntax rather than deleting comment-like text from strings or templates. Executable directives need consumer analysis and relevant checks; being tool-consumed alone is not an additional keep-list exception. Repository requirements and explicit user exclusions still apply.

Report deletion count, keeps with their exact exceptions, restorations, rejected passes and reruns, architectural sketch, root-cause fixes, encoding proposals and implementations, unenforced constraints, checks and evidence, and remaining work. Distinguish completed cleanup from unverified or failing changes. Do not restore non-exempt prose to conceal incomplete implementation.
