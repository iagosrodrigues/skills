---
name: setup
description: Configure one shared model and reasoning effort by role for noam in a project. Detect supported controls, preserve existing choices, and make the project policy discoverable without changing workflow skills.
---

# Setup

Write or update the project-root `.noam.json`. One model applies to every role; only reasoning effort varies. Answer in the user's language. This skill configures future work; do not change the current task's model or claim that writing a file changes runtime settings.

## Inspect capabilities and current state

Read repository instructions and the existing `.noam.json`, if present. Detect the model identifiers and reasoning-effort controls actually available to subagents in the current environment, using exposed tool schemas, runtime metadata, or installed help. Do not guess supported values from a model name or append effort suffixes to identifiers.

Use `inherit-parent` when the user wants the active model. It means omit an explicit model override for every worker, so all roles inherit the same parent model within that session. An explicit model identifier must be confirmed available. Retain it on subsequent runs unless the user changes it. Never replace an unavailable model with a different family without resolving the choice with the user.

Model and effort are independent settings. A runtime may accept a particular effort only for some models, or expose no per-worker effort control at all. Record those limits; validate only what this environment can establish. Portability of the file does not prove every runtime can honor it.

## Choose the budget and roles

Honor choices already given in the request. Otherwise ask for the missing model preference and budget, showing current values. Offer these target budgets, with unsupported targets clearly marked:

| Budget | Target effort |
| --- | --- |
| small | medium |
| medium | high |
| large | xhigh |
| unlimited | max |

These are preferences, not claims of runtime support. For a supported effort ladder, resolve a target to the highest available level at or below it and show the fallback. Do not invent ordering for unfamiliar levels. If no valid level exists at or below the target, ask for a supported choice instead of silently increasing cost. When no override is supported, use `inherit` and explain that effort cannot be enforced by role here.

Use the selected target as `default_effort`. Let the user override individual roles, all using the same model:

- `exploration`: locating and tracing source or history.
- `implementation`: ordinary coding and refactoring.
- `design`: architectural candidates and synthesis.
- `review`: adversarial checks and independent judgment.
- `verification`: execution and analysis of acceptance checks.
- `writing`: documentation and explanations.

Unclassified work uses `default_effort`. A role describes the assigned work, not a particular skill name. Do not configure panel counts, model races, speed tiers, or a separate judge model here. Independent reviewers can share a model; that is not cross-model review.

Preserve existing explicit role choices on reruns unless the user requests a reset or a change affecting them. If an old file has per-role models or model lists, propose a migration to one shared model and show what would be replaced; do not silently choose one from a mixed set. Retain unrelated keys and report obsolete settings before removing them.

## Show and write the resolved policy

Present one model, the requested budget, resolved default effort, all six role efforts, and capability limits. Ask for a decision only where a preference or migration remains unresolved. An explicit request containing all choices already authorizes the write; do not ask for the same approval again.

Use this shape, with values replaced by resolved choices:

```json
{
  "version": 1,
  "model": "inherit-parent",
  "budget": "medium",
  "default_effort": "high",
  "roles": {
    "exploration": "medium",
    "implementation": "high",
    "design": "high",
    "review": "high",
    "verification": "medium",
    "writing": "medium"
  }
}
```

The example is illustrative, not a preset to write without checking support or user preference. `inherit` is valid for an effort field and means omit that override. Each role value is an effort string, never a model object or a list. Write valid JSON and re-read it. Preserve user content when updating an existing file; stop and explain malformed or incompatible configuration rather than replacing it blindly.

## Make the policy discoverable

An arbitrary JSON file is not automatically read by agents. Use the project's established agent-instruction mechanism to add or update a bounded managed block pointing to `.noam.json`. Prefer the existing canonical instruction file and its established adapters; avoid duplicating policy. If no discovery convention exists, resolve the intended instruction-file destination with the user before creating it. Do not modify plugin caches, global runtime configuration, or workflow skill bodies, including `guide-me`.

Use this managed block, adapting only the relative config path:

```text
<!-- noam-model-policy:start -->
Before delegating noam work, read the project-root .noam.json when present.
Use its single model for every role; inherit-parent means omit the model override.
Choose the effort for the assigned role, falling back to default_effort; inherit
means omit that override. Apply only controls supported by the active runtime
and permitted by higher-priority instructions. Report unavailable settings;
do not silently change models or claim effort was applied when it was not.
Independent same-model review is allowed; do not claim model diversity.
<!-- noam-model-policy:end -->
```

Replace only this marked block on reruns. Preserve surrounding instructions and do not duplicate it. If existing instructions conflict with the policy, surface the conflict and resolve it within the user's scope; the JSON does not override instruction priority. A workflow explicitly requesting a model comparison is incompatible with the single-model policy unless the user authorizes an exception.

## Verify and report

Check JSON parsing, one shared model, string-valued efforts, valid role names, supported choices or explicit inherit values, the managed block, and its resolved path. Inspect the final diff for unrelated changes. Do not spawn paid trial workers merely to validate a preference file; use a live delegation check only when requested or necessary and authorized.

Report the written paths and resolved model/effort table. Distinguish configuration validation, instruction discovery, and actual runtime application. Tell the user which settings could not be enforced or tested. New sessions can use the policy when their instruction loader reads the managed block; do not promise automatic reload or cross-runtime support that was not verified. Commit and publication remain separate actions unless requested.
