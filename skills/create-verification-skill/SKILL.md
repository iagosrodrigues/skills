---
name: create-verification-skill
description: Create or extend a project-local skill that launches an app, exercises real user behavior, and captures repeatable evidence. Use when a repository needs a reusable verification procedure for its UI, CLI, service, or library. For checking one change with an existing procedure, use that procedure instead.
---

# Create a verification skill

Leave a procedure that a fresh agent can follow without this conversation. Discover the project's real commands and interfaces, write the skill, and exercise its instructions before calling it ready. Use the user's language for the handoff and the repository's conventions for files.

## Discover the project

Read repository instructions and inspect existing skills, run commands, tests, and automation before creating anything. Prefer extending an existing verification skill for the same app over adding a competing procedure. Preserve unrelated content.

Establish from the repository:

- The primary user interface: UI, CLI/TUI, service API, or library API. Identify other interfaces and state which are outside the initial coverage.
- How to build and run the target revision, including environment variables, authentication, fixtures, migrations, and readiness signals.
- How to exercise behavior through the supported interface. Reuse existing browser tests, terminal drivers, HTTP clients, or library tests before introducing tooling.
- Which observations prove the result: output and exit status, response bodies, screenshots, logs, or persisted values.
- How concurrent runs can isolate ports, data directories, accounts, browser profiles, build outputs, and temporary files. If an instance cannot be isolated, require exclusive use and explain how to establish ownership before driving it.

Ask only for facts or choices the repository and current session cannot establish. Do not invent credentials, commands, selectors, or successful outcomes.

## Choose the destination and scope

Honor an explicit destination, then the project's existing skill layout and supported discovery mechanisms. Confirm how the intended agents discover project skills. When several agents use the project, keep one canonical skill body and expose it through the project's supported mechanism. Follow existing conventions for references, links, or adapters. If the destination remains ambiguous, ask one focused question while continuing repository inspection.

Name the generated skill `verify-<app>` with a valid lowercase, hyphenated name. Keep it project-local unless the user asks otherwise. Do not edit plugin caches, personal model settings, or unrelated manifests to make it discoverable.

The request authorizes creating the verification procedure and appropriate local helpers. It does not authorize product fixes, production mutations, deployment, external messages, or changes to unrelated project configuration. Run safe local checks within the session's permissions. Request missing authorization only for a necessary action outside that scope.

If the checkout cannot build or run, distinguish missing setup from a product defect. Complete authorized disposable setup, or report the precise blocker. Do not silently repair product code. A written procedure that could not be exercised remains a draft.

## Write the procedure

Create `SKILL.md` with `name` and `description` frontmatter. The description names the app, supported interfaces, and changes that should trigger verification. Use [the procedure template](references/procedure-template.md) as a checklist, adapting sections to the app. Replace every placeholder with discovered facts.

Include:

- **Launch.** Exact commands and working directories, runtime prerequisites, test configuration, seed data, and migrations. Ready means a usable app, not merely an open port. For a short-lived CLI or library, describe the build and per-invocation setup instead of inventing a server.
- **Doctor.** Read-only checks for the expected instance, revision or build, owned port or process, usable data, and authentication where relevant. Run before driving and after unexpected behavior. Reset a broken session when a healthy process alone cannot establish usable state.
- **Drive.** Concrete commands or interactions through the real interface. Prefer stable accessible names, routes, prompt strings, or explicit test handles over generated selectors and coordinates. Arrange prerequisites with disposable fixtures; do not inject the result being proved through internal setters or hidden endpoints.
- **Evidence.** Capture inputs or actions and their observable results, including promised side effects. Record the revision or working-tree state and environment. Give artifact paths that survive cleanup, exclude secrets, and distinguish real integrations from mocks or substitutes. Verify what a dry-run actually skips rather than trusting its name.
- **Cleanup.** Stop only processes and sessions this run owns and remove only its disposable state. Never kill by process name or delete shared data. Preserve evidence in a separate location and clean failed attempts too.

Add helpers only when they materially improve repeatability. Document each invocation, required runtime, and inputs. Make directly invoked scripts executable and run them. Prefer a small script over a new framework; do not require another skill or model configuration to understand the generated procedure.

## Map the initial features

Create `features/README.md` with the covered journeys and their recipe links, plus one short file per selected feature. Start with the primary journey and a few important neighbors when useful; do not imply complete product coverage.

For each recipe, record the user-visible behavior, entry points, preconditions, exact drive steps, expected observable result, evidence, reset steps, and relevant gotchas. Use the feature recipe in the template. Record documented or source-derived recipes separately from journeys actually exercised. Running one entry point does not verify another.

Missing seed data, permissions, or service availability is a prerequisite gap. Report it without weakening the journey to make it pass.

## Exercise the generated skill

Follow the written instructions as a fresh agent would: launch, doctor, drive at least one mapped journey, inspect its expected result and side effects, capture evidence, and clean up. Confirm that the evidence still exists after cleanup and that owned resources have stopped. For other recipes, verify commands and entry points from source and clearly mark them as not yet run.

Fix errors in the procedure or its helpers and repeat the affected steps, cleaning each failed attempt. Stop at a persistent environment, access, or product blocker and report it; do not turn generation into an unbounded debugging task. A genuine product regression remains a finding, not a documentation edit that redefines success.

Check frontmatter, local links, helper invocations, and unfinished placeholders. Use an available skill validator if present. Structural validation does not replace the live journey. If the target was substituted, name the differences and the steps still unverified on the real target.

## Hand off

Report the generated location, how the intended environment discovers it or what remains unconfirmed, the journey actually run, its outcome and evidence paths, cleanup result, and uncovered or blocked areas. Label an unexercised procedure as a draft. Do not claim that all mapped features passed because one did.

Tell future users to update the recipes when behavior, commands, or prerequisites change and rerun affected journeys. Do not require an unavailable maintenance skill, schedule automation, commit, or open a PR unless the task calls for it.
