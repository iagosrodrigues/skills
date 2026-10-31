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

- [`correct`](skills/correct/SKILL.md) prevents recurring agent mistakes through architecture, types, actionable checks, and behavioral tests, proving that enforcement rejects the recorded mistake.

- [`swarm`](skills/swarm/SKILL.md) coordinates parallel subagents across task slices or competing approaches, with isolated ownership, evidence checks, and validation of the integrated result.

- [`architect`](skills/architect/SKILL.md) grounds nontrivial changes and compares independent designs before synthesizing caller usage, types, and module boundaries.

- [`arena`](skills/arena/SKILL.md) compares independent candidate artifacts, obtains a read-only judgment, and synthesizes a verified result.

- [`show-me-your-work`](skills/show-me-your-work/SKILL.md) keeps an append-only decision trail, audits evidence, and requests independent review before handoff.

- [`guide-me`](skills/guide-me/SKILL.md) guides an end-to-end task through the relevant bundled workflows, from onboarding to verified delivery.

- [`no-comments`](skills/no-comments/SKILL.md) reviews comment quality with an independent reader, removes confirmed noise, preserves meaningful rationale and tool directives, and proves constraint enforcement before dropping reminders.

- [`setup`](skills/setup/SKILL.md) configures one shared model and reasoning effort per role in a project-local `.noam.json`, with a managed project-instruction block for discovery and explicit runtime capability checks.

- [`why`](skills/why/SKILL.md) investigates historical rationale through parallel source readers and independent synthesis, with cited confidence levels and explicit coverage gaps.

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

Example request after loading `correct`:

```text
Investigue erros recorrentes nas correções recentes deste projeto.
Para os padrões comprovados, implemente a prevenção mais adequada:
arquitetura, tipos, lint ou testes; documentação por último.
Mostre evidências das ocorrências e prove que o guardrail rejeita o erro.
```

Example request after loading `swarm`:

```text
Use subagentes em paralelo para implementar esta tarefa: [objetivo].
Defina os critérios de conclusão, distribua arquivos sem sobreposição,
integre as mudanças e valide o resultado combinado.
Informe as evidências e qualquer parte bloqueada.
```

Example request after loading `architect`:

```text
Desenhe a arquitetura para [objetivo]. Compare duas estruturas distintas com subagentes. Mostre uso, tipos, limites dos módulos e tradeoffs. Pare antes de implementar.
```

Example request after loading `arena`:

```text
Use a arena para produzir [artefato]. Gere candidatos independentes, compare com critérios concretos e sintetize a melhor solução. Mostre a verificação final.
```

Example request after loading `show-me-your-work`:

```text
Mantenha uma trilha de decisões para esta tarefa, com evidências. Antes de encerrar, audite o registro e peça uma revisão independente dos riscos e lacunas.
```

Example request after loading `guide-me`:

```text
Sou novo neste projeto. Guie-me até implementar [objetivo]: explique o fluxo relevante, escolha as etapas necessárias, implemente e verifique. Avance no trabalho local e me consulte nas decisões de produto que estiverem faltando.
```

Example request after loading `no-comments`:

```text
Revise os comentários do diff com um subagente independente.
Remova narração redundante e corrija afirmações comprovadamente obsoletas.
Preserve razões úteis, contratos, avisos ainda não resolvidos e diretivas.
Proponha guardrails para restrições importantes; não refatore o produto ainda.
Verifique o que os comentários alterados influenciam.
```

Example request after loading `setup`:

```text
Configure o noam neste projeto com o modelo da sessão para todas as funções.
Quero effort high por padrão e medium para exploração e escrita.
Confira o que o ambiente suporta e mostre qualquer fallback necessário.
```

Example request after loading `why`:

```text
Investigue por que [decisão ou trecho] foi implementado dessa forma.
Use o histórico e as fontes disponíveis, com investigadores em paralelo.
Separe motivos documentados, inferências e lacunas. Não altere o código.
```

These skills use shared `SKILL.md` instructions for Codex and Claude Code, without Cursor-specific tool names or model identifiers.

`how` is adapted from [pstack's how skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/how/SKILL.md) and its explanation templates, by Lauren Tan. The upstream [MIT license](skills/how/LICENSE) is preserved alongside the skill.

`prove-it-works` is adapted from [pstack's Prove It Works principle](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-prove-it-works/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/prove-it-works/LICENSE) is preserved alongside the skill.

`create-verification-skill` is adapted from [pstack's verification skill generator](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/create-verification-skill/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/create-verification-skill/LICENSE) is preserved alongside the skill.

`interrogate` is adapted from [pstack's interrogate skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/interrogate/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/interrogate/LICENSE) is preserved alongside the skill.

`maintain-verification-skill` is adapted from [pstack's verification skill maintenance workflow](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/maintain-verification-skill/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/maintain-verification-skill/LICENSE) is preserved alongside the skill.

`correct` is adapted from [pstack's correct skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/correct/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/correct/LICENSE) is preserved alongside the skill.

`swarm` is adapted from [pstack's swarm skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/swarm/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/swarm/LICENSE) is preserved alongside the skill.

`architect` is adapted from [pstack's architect skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/architect/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/architect/LICENSE) is preserved alongside the skill.

`arena` is adapted from [pstack's arena skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/arena/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/arena/LICENSE) is preserved alongside the skill.

`show-me-your-work` is adapted from [pstack's show-me-your-work skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/show-me-your-work/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/show-me-your-work/LICENSE) is preserved alongside the skill.

`guide-me` is a scoped adaptation of the workflow routing in [pstack's poteto-mode skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/poteto-mode/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/guide-me/LICENSE) is preserved alongside the skill.

`guide-me` composes the ported workflows; it does not include the upstream mode's full playbook suite or platform-specific automation.

## Code-quality principles

These are canonical principle skills, usable directly or loaded on demand by workflows. They guide decisions; they do not authorize a refactor or replace verification. `guide-me` includes a [code-quality workflow](skills/guide-me/references/code-quality.md) that starts with maintenance evidence and applies only the relevant principles.

| Principle | Decision it helps make |
| --- | --- |
| [Minimize reader load](skills/principle-minimize-reader-load/SKILL.md) | Reduce unnecessary indirection and hidden mutable context. |
| [Laziness protocol](skills/principle-laziness-protocol/SKILL.md) | Choose the smallest coherent correction without speculative machinery. |
| [Subtract before you add](skills/principle-subtract-before-you-add/SKILL.md) | Remove proven obsolete structure before extending it. |
| [Model the domain](skills/principle-model-the-domain/SKILL.md) | Encode real states and invariants in data and ownership. |
| [Boundary discipline](skills/principle-boundary-discipline/SKILL.md) | Establish validation and error contracts at actual trust boundaries. |
| [Test behavior, not implementation](skills/principle-test-behavior-not-implementation/SKILL.md) | Protect observable contracts while allowing internal refactoring. |

Example request after loading `guide-me`:

```text
Avalie a qualidade estrutural do fluxo [X], sem editar ainda.
Mostre onde a estrutura dificulta uma mudança concreta e compare manter,
corrigir localmente ou refatorar. Priorize até três oportunidades.
Diferencie evidências de preferências de estilo e indique como preservar
os comportamentos antes de propor a implementação.
```

`architect` selects design principles as needed; `correct` and `prove-it-works` consult the behavior-testing principle when evaluating checks. The principle bodies remain the source of truth, rather than being copied into each workflow.

These six principles are adapted from Lauren Tan's pstack principles: [`principle-minimize-reader-load`](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-minimize-reader-load/SKILL.md) ([MIT license](skills/principle-minimize-reader-load/LICENSE)), [`principle-laziness-protocol`](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-laziness-protocol/SKILL.md) ([MIT license](skills/principle-laziness-protocol/LICENSE)), [`principle-subtract-before-you-add`](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-subtract-before-you-add/SKILL.md) ([MIT license](skills/principle-subtract-before-you-add/LICENSE)), [`principle-model-the-domain`](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-model-the-domain/SKILL.md) ([MIT license](skills/principle-model-the-domain/LICENSE)), [`principle-boundary-discipline`](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-boundary-discipline/SKILL.md) ([MIT license](skills/principle-boundary-discipline/LICENSE)), [`principle-test-behavior-not-implementation`](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/principle-test-behavior-not-implementation/SKILL.md) ([MIT license](skills/principle-test-behavior-not-implementation/LICENSE)). Runtime trust, compatibility, and task scope qualify the upstream absolutes.

`no-comments` is adapted from [pstack's no-comments workflow](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/no-comments/SKILL.md) and [Comment Sicko reviewer](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/agents/comment-sicko.md), by Lauren Tan. Its upstream [MIT license](skills/no-comments/LICENSE) is preserved alongside the skill. The port retains independent review while using evidence-based deletion, preserving unresolved constraints and tool-consumed comments.

`setup` is adapted from [pstack's setup-pstack skill](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/setup-pstack/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/setup/LICENSE) is preserved alongside the skill. This port uses one shared model and separate effort settings, with project instruction discovery instead of a platform-specific global rule.

`why` is adapted from [pstack's why skill and references](https://github.com/cursor/plugins/blob/1ba91fc25c0977741dd0e267849e6234b037ed0a/pstack/skills/why/SKILL.md), by Lauren Tan. Its upstream [MIT license](skills/why/LICENSE) is preserved alongside the skill.

## Layout

- `.claude-plugin/marketplace.json` — Claude Code marketplace manifest
- `.claude-plugin/plugin.json` — Claude Code plugin manifest
- `.agents/plugins/marketplace.json` + `.codex-plugin/plugin.json` — Codex equivalents
- `skills/<name>/SKILL.md` — skills
- `commands/<name>.md` — slash commands
