# Generated procedure checklist

Use this shape when writing the project skill. Replace placeholders with observed project facts and omit inapplicable details. The generated skill must stand alone; it must not require this generator or template to run.

```markdown
---
name: verify-<app>
description: Verify <app> through <supported interface> when <relevant behavior changes>.
---

# Verify <app>

## Scope

<Covered behavior, excluded interfaces, and permitted test environment.>
Read [the feature map](features/README.md) and select the affected recipes.

## Launch

<Working directory, prerequisites, exact setup and run commands, disposable
state, instance ownership, and usable readiness signal.>

## Doctor

<Read-only commands that identify the expected app, revision, and usable state.
Run before driving and repeat after unexpected behavior.>

## Drive

<Available driver, exact invocation, and selection of feature recipes.
Use the supported user interface to produce the result.>

## Evidence

<Inputs, actions, outputs, exit codes or state assertions, and artifact paths.
Record the revision and environment. Capture side effects and preserve evidence
outside disposable state. State limits of mocks or substitute environments.>

## Cleanup

<Commands that stop only owned resources and remove only disposable state,
including after failure. Confirm that evidence survives.>
```

The feature map index lists each recipe, its supported entry points, and whether it was exercised or only inspected from source. Record the revision or working-tree state and prerequisites for the exercised recipes so later changes do not silently inherit their verdicts.

Each feature file follows this compact shape:

```markdown
# <Feature>

<What the user can do and what observable result proves it.>

## Preconditions and entry points

<Test account, data, permissions, flags, service availability, and user paths.>

## Drive and verify

<Exact commands or interactions, with expected results derived from the contract.
Name which entry point this recipe exercises and where its evidence is saved.
Include read-back or other side-effect checks when relevant.>

## Reset and gotchas

<How to restore disposable state for another run; wrong surfaces, unavailable
prerequisites, and cases not covered by this recipe.>
```

Store measured results in evidence artifacts. Keep the recipe focused on what a future run must do, rather than turning one successful run into a permanent claim that the feature works.
