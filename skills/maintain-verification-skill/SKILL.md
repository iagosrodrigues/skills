---
name: maintain-verification-skill
description: Maintain an existing project verification skill with parallel source-reading subagents per feature and a coordinated live pass. Repair stale instructions, feature maps, and owned helpers. Use for verification-procedure audits; for checking one product change, use that project's procedure instead.
---

# Maintain a verification skill

Keep an existing verification procedure repeatable and its coverage honest. Inspect the source and exercise the mapped behavior before declaring the procedure current. Answer in the user's language and follow repository conventions for files.

## Establish the target

Read repository instructions and locate the verification skill named by the user, or an existing project-local procedure with launch, health checks, drive instructions, and a feature map. Follow the project's actual layout; do not assume a particular skill directory or agent runtime.

If several candidates remain plausible, ask which one while continuing safe inspection. If none exists, explain that a verification procedure must first be created; do not invent one as a maintenance target. A separate generator skill is not required to maintain an existing procedure.

Read the procedure, its feature index, recipes, and owned helpers. Establish the review scope and the app revision or working-tree state being exercised, including relevant uncommitted changes. By default cover the full existing map; honor an explicitly narrower scope and label the result accordingly. A mapped subset is not complete product coverage.

The edit scope is the verification skill's own instructions, feature recipes, and helpers it owns. Preserve unrelated edits and existing discovery conventions. Do not change product code, shared infrastructure, personal settings, or plugin caches. Maintenance does not by itself authorize commits, pushes, PRs, external messages, or scheduled automation. A read-only audit request also excludes procedure edits.

## Reconcile the map with source

Compare the feature index with its recipe files. Resolve broken links, duplicate entries, and unindexed recipes without deleting useful coverage merely because it is hard to run. Inspect references before removing or renaming a file.

For every feature in scope, identify its user-visible contract, source entry points, prerequisites, likely documentation drift, and a concrete live recipe. Inspect relevant recent changes for missing user-facing behavior and require a source path before calling a feature missing. Keep newly discovered coverage proportional to the requested maintenance scope; record broader gaps rather than claiming an exhaustive product inventory.

Launch one read-only subagent per feature recipe file, in parallel up to the environment's concurrency limit; use successive waves when necessary. Each reader explains its feature from source and returns a feature summary, source entry points, suspected drift with citations or none, and one concise live recipe. Give every reader the same target state, repository instructions, its assigned file, and execution boundaries. Readers never drive the app or edit files. Use the environment's supported delegation tools without requiring a particular vendor or model identifier.

Subagent source review is part of this workflow, not an optional optimization. If delegation is unavailable or prohibited, continue useful direct inspection but report the pass as incomplete; do not present self-review as the required source wave. Account for every assigned feature file and any failed or missing reader results before declaring source coverage complete.

Collect every reader's result and merge overlapping recipes into as few app states as practical. Spot-check cited drift; do not repeat every clean source investigation. Reconcile suspected drift against requirements, acceptance criteria, or documented intended changes. Current implementation alone does not establish the intended behavior. Do not rewrite an expectation to match a regression. When the contract remains ambiguous, preserve it, describe the discrepancy, and ask only if that ambiguity prevents a necessary decision.

## Exercise the procedure

Follow the existing launch model and use supported interfaces and disposable fixtures. For a server or UI, reuse one owned instance when practical; for short-lived commands or library checks, use the procedure's per-invocation setup. One coordinator owns live execution and edits. Keep source readers away from shared mutable state.

Source inspection alone cannot complete the audit. Exercise every feature in scope at least once, with a meaningful expected-result check and relevant side-effect checks. Combine setup where useful, but do not count one route as proof of another. Track which entry points actually ran.

Maintain these execution constraints:

- Establish ownership or exclusive use before driving a shared instance. Isolate ports, data, profiles, accounts, and outputs where supported; do not interfere with another session.
- Run the procedure's health checks before the first drive, for each fresh session where applicable, and after unexpected behavior. A healthy process may still have unusable UI or data state; reset owned state or relaunch when needed before continuing.
- Capture actions, expected and actual outcomes, target state, and evidence paths. Store evidence outside disposable state, exclude secrets, and confirm it survives cleanup.
- Clean failed-attempt residue promptly. For a reused instance, remove only the attempt's disposable state while it is still needed. Stop owned processes and sessions after the final drive, including rechecks after helper fixes. Never kill by process name or delete shared data.

If a health check or driver fails because the procedure is stale, make a scoped correction and retry once, restarting only what the correction invalidates. Run changed helpers through their documented invocation. A persistent failure remains a blocker; do not turn maintenance into unbounded product debugging.

For unavailable credentials, permissions, services, or platform requirements, record the concrete missing prerequisite and the route attempted. Mark the feature blocked or not exercised, never passed. Complete safe setup and unaffected checks within existing authorization. Do not trigger real external side effects to obtain evidence; request specific missing authorization only when necessary.

## Correct drift without hiding failures

Classify discrepancies before editing:

- **Documentation drift:** the intended behavior, command, or prerequisite changed and the procedure is stale. Update the instructions and exercise the corrected recipe.
- **Helper gap:** the supported behavior works but the procedure cannot drive or observe it reliably. Fix only owned helpers, document their runtime and invocation, make directly invoked scripts executable, and rerun the affected journey.
- **Product defect:** the app violates the intended behavior. Preserve the expectation and report the failure with evidence. Do not fix the product or weaken the recipe to obtain a pass.
- **Unresolved discrepancy:** evidence or intent is insufficient to classify the difference. State what remains unknown and the check needed to resolve it.

Keep the feature index consistent with recipes and actual coverage. Preserve distinctions between source-inspected, exercised, and blocked paths. Record measured results with the tested revision or working-tree state in run evidence; do not turn a past successful run into a permanent claim that a feature works.

Review changed files, local links, and helper invocations. Use an available skill validator when useful, but structural validation does not replace execution. Recheck affected journeys after corrections. If product code changes during the pass, identify the drift and rerun affected checks against the new target or report them as stale.

If a blocker prevents validating a procedure edit, distinguish it from proven corrections and label it unverified. Do not revert pre-existing user changes. Keep concise run notes in a scratch location, outside the maintained skill, and preserve evidence through final cleanup.

## Report the outcome

Use an outcome scoped to the requested coverage:

- **Clean:** every in-scope feature has subagent source coverage and successful live coverage, with no corrections needed or unresolved discrepancies.
- **Updated:** the scoped audit completed and the procedure corrections were exercised successfully.
- **Incomplete:** any in-scope coverage or correction remains unverified, blocked, or failing. Useful corrections may still be present; list their validation status separately.

Report the target procedure and app state, outcome, corrected files, features and entry points actually exercised, evidence paths, cleanup result, and remaining prerequisites or product findings. Disclose source-reader coverage and any missing results. Do not call a partially exercised map current.

Leave local changes reviewable by default. If publishing was requested and the outcome is updated, collect the proven procedure corrections into at most one PR after rereading the changed files. Do not include product fixes or scratch run notes. For clean or incomplete outcomes, report the result without opening a PR. If requested publication is blocked, state that separately from the completed verification work.
