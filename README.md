# noam

Personal Claude Code (and Codex) plugin marketplace by Iago Sousa. It ships a single plugin, `noam-plugin`, which bundles the skills and commands I use day to day.

## Install

Claude Code:

```sh
claude plugin marketplace add iagosrodrigues/skills
claude plugin install noam-plugin@noam
```

## Layout

- `.claude-plugin/marketplace.json` — Claude Code marketplace manifest
- `.claude-plugin/plugin.json` — Claude Code plugin manifest
- `.agents/plugins/marketplace.json` + `.codex-plugin/plugin.json` — Codex equivalents
- `skills/<name>/SKILL.md` — skills
- `commands/<name>.md` — slash commands
