# noam

Personal Claude Code (and Codex) plugin marketplace by Iago Sousa. It ships a single plugin, `noam-plugin`, which bundles the skills and commands I use day to day.

## Install

Claude Code:

```sh
claude plugin marketplace add iagosrodrigues/skills
claude plugin install noam-plugin@noam
```

## Skills

- [`how`](skills/how/SKILL.md) explains existing code, traces a user or runtime flow, and identifies module ownership and extension points. It works directly by default, with optional delegation when supported and authorized. It requires no model configuration or sibling skills.

- [`prove-it-works`](skills/prove-it-works/SKILL.md) verifies a result against the actual app, code, or artifact. It uses proportional checks, reports evidence and gaps, and requires no model configuration or sibling skills.

- [`create-verification-skill`](skills/create-verification-skill/SKILL.md) creates a project-local verification procedure with launch, doctor, drive, evidence, cleanup, and a feature map. It exercises at least one journey before calling the generated procedure ready.

- [`interrogate`](skills/interrogate/SKILL.md) challenges a change with isolated reproductions, verifies candidate defects, and reports confirmed findings separately from unproven risks. Independent reviewers are optional when supported and authorized; product fixes are outside its scope.

- [`maintain-verification-skill`](skills/maintain-verification-skill/SKILL.md) audits an existing verification procedure with parallel source-reading subagents per feature and one coordinator driving the app. It repairs instructions and owned helpers, reports blocked coverage, and opens a PR only when requested.

Example request after loading `how`:

```text
Sou novo neste projeto. Explique como uma requisição percorre o sistema,
onde ficam as regras de negócio e quais comandos verificam essa jornada.
Não altere arquivos nem inicie serviços. Separe o que você leu do que executou.
```

Example request after loading `prove-it-works`:

```text
Verifique esta correção no cenário que apresentava o problema.
Mostre o resultado esperado, o observado e a evidência.
Não altere código. Deixe explícito o que não conseguiu verificar.
```

Example request after loading `create-verification-skill`:

```text
Crie uma skill de verificação para este projeto, seguindo a organização
existente de skills. Use dados locais descartáveis e valide uma jornada real.
Não altere código do produto. Informe as funcionalidades ainda não exercitadas.
```

Example request after loading `interrogate`:

```text
Revise as mudanças desta branch e tente reproduzir falhas reais.
Inclua minhas alterações ainda não commitadas e preserve a árvore de trabalho.
Não corrija o produto. Separe defeitos confirmados de riscos não comprovados
e informe se houve revisão independente.
```

Example request after loading `maintain-verification-skill`:

```text
Atualize a skill de verificação deste projeto e seu mapa de funcionalidades.
Use um subagente de leitura por funcionalidade, em paralelo.
O coordenador deve executar as jornadas mapeadas com dados descartáveis.
Corrija apenas a documentação e os helpers da skill, sem alterar o produto.
Informe evidências, bloqueios e quais jornadas não conseguiu executar.
Não faça commit nem abra PR.
```

These skills use shared `SKILL.md` instructions for Codex and Claude Code, without Cursor-specific tool names or model identifiers.

`how` is adapted from [pstack's how skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/how/SKILL.md) and its explanation templates, by Lauren Tan. The upstream [MIT license](skills/how/LICENSE) is preserved alongside the skill.

`prove-it-works` is adapted from [pstack's Prove It Works principle](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-prove-it-works/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/prove-it-works/LICENSE) is preserved alongside the skill.

`create-verification-skill` is adapted from [pstack's verification skill generator](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/create-verification-skill/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/create-verification-skill/LICENSE) is preserved alongside the skill.

`interrogate` is adapted from [pstack's interrogate skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/interrogate/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/interrogate/LICENSE) is preserved alongside the skill.

`maintain-verification-skill` is adapted from [pstack's verification skill maintenance workflow](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/maintain-verification-skill/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/maintain-verification-skill/LICENSE) is preserved alongside the skill.

## Layout

- `.claude-plugin/marketplace.json` — Claude Code marketplace manifest
- `.claude-plugin/plugin.json` — Claude Code plugin manifest
- `.agents/plugins/marketplace.json` + `.codex-plugin/plugin.json` — Codex equivalents
- `skills/<name>/SKILL.md` — skills
- `commands/<name>.md` — slash commands
