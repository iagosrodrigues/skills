---
name: show-me-your-work
description: Keep an append-only decision trail with evidence for long-running, unattended, or multi-phase work, then audit its claims and obtain independent review. Use when a user needs to inspect why decisions were made and what was actually verified.
---

# Show me your work

Keep one canonical TSV decision log. Answer in the user's language. Record decisions and their observable support, not private internal reasoning or a transcript of every action.

## Format and location

Use [the header template](references/decision-log-template.tsv). Columns are `ts` (ISO8601), `phase`, `decision`, `why` (a concise rationale), `evidence` (resolvable pointers), and `result` (observed outcome, open, or inconclusive). Cells are single-line; evidence is a path, revision, or link rather than a paragraph. Never log secrets or unrelated conversation contents.

Keep the log local by default, in an agreed working-artifact location such as `.audit/<task>.tsv` or a task scratch directory. Keep it out of staged files unless the user requests a committed trail. Do not alter global ignore settings to hide it. Ensure evidence paths survive temporary-state cleanup.

Append rows with `bash <skill-directory>/scripts/log.sh <logfile> <phase> <decision> <why> <evidence> <result>`. The helper timestamps entries, creates the header, normalizes tabs and newlines, and neutralizes leading spreadsheet formula characters. It does not provide concurrent-write locking: one coordinator owns the canonical log, while subagents return evidence for that coordinator to record.

## Record checkpoints

Log meaningful choices, completed units with verification, pivots, rejected work, blockers, and loop iterations. Use concrete plain language. Do not manufacture a passing result from a worker summary or claim a command ran merely because it was proposed.

A run is one conversation, including later turns. A new conversation or replacement agent starts another run. When appending to an existing log, first append a `start` row identifying the current run and the timestamp range inherited from other runs. On resuming, inspect recent rows; if another run appended since yours, append another `start` marker before continuing. Use a genuine session identifier when available, or a locally assigned run label; do not invent platform metadata. Reserve `start` for these boundaries.

The log is append-only. Supersede wrong decisions or evidence with a new row referring to the original row's timestamp and claim. Do not rewrite history, even for an invented or disproven entry. Preserve previous user records.

## Audit against available evidence

Before handoff, check this run's rows against actual tool results, artifacts, and the current conversation. Use an authorized transcript for this run if the runtime exposes one. Do not assume a transcript directory, search unrelated chats, or require access the environment does not provide. If no transcript is accessible, disclose that the audit used available conversation and artifacts and what it could not establish.

Check that each entry reflects a real action or decision, evidence resolves and supports the claim, and material pivots or abandoned approaches are recorded. Add missing entries and superseding corrections. Never mark an evidence check complete when the pointer could not be inspected.

## Independent review

Before handoff, request a read-only subagent review of the trail and authorized run evidence. Prefer a different model family when available; otherwise use an independent reviewer on the supported default and disclose that cross-model review was unavailable. Self-review is not independent review. If subagents cannot run, state the missing review explicitly and present the trail with that limitation.

The reviewer flags unsupported entries, missing verification, scope expansion, symptom fixes, and risks a casual reader could miss. It does not redo the implementation or edit the canonical log. Give it only task-relevant authorized evidence. Do not fabricate a reviewer identity or treat silence as approval.

Hand off the canonical log path, evidence locations, audit scope, and an **Attention** section naming the actual reviewer when known, its flags with row pointers, or an explicit absence of independent review. “No flags” is valid only after a completed review. Preserve unresolved or inconclusive results instead of turning the trail into a success narrative.
