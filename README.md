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

- [`code-gardening`](skills/code-gardening/SKILL.md) makes one evidence-backed maintenance improvement at a time, applies the relevant principles, and verifies preserved behavior and reduced reader load.

- [`no-comments`](skills/no-comments/SKILL.md) applies strict comment deletion with a narrow keep list, an independent editing reviewer, scoped root-cause fixes, and explicit reporting of unenforced constraints.

- [`setup`](skills/setup/SKILL.md) configures one shared model and reasoning effort per role in a project-local `.noam.json`, with a managed project-instruction block for discovery and explicit runtime capability checks.

- [`why`](skills/why/SKILL.md) investigates historical rationale through parallel source readers and independent synthesis, with cited confidence levels and explicit coverage gaps.

- [`blast-radius`](skills/blast-radius/SKILL.md) traces downstream impact beyond direct callers and tests the critical assumptions that make a change safe.

- [`reflect`](skills/reflect/SKILL.md) reviews session evidence through judgment, tooling, and divergent lenses, then proposes concrete skill improvements or structural backlog with independent synthesis.

- [`benchmark-checklist`](skills/benchmark-checklist/SKILL.md) validates performance claims through real-work checks, correct outputs, comparable tuning, bottleneck evidence, repeated runs, and end-to-end relevance.

- [`technical-writing`](skills/technical-writing/SKILL.md) structures technical documents around the reader's task and checks instructions, terminology, and factual claims.

- [`unslop`](skills/unslop/SKILL.md) edits prose for clarity and specificity while preserving meaning, literal technical content, evidence, and uncertainty.

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

Example request after loading `code-gardening`:

```text
Faça uma rodada de code gardening no fluxo [X]. Identifique um obstáculo
concreto de manutenção, escolha uma melhoria pequena e preserve os contratos.
Implemente, verifique o comportamento e mostre o que ficou mais fácil de entender.
Se não houver ganho justificável, explique e não altere o código.
```

Example request after loading `no-comments`:

```text
Aplique no-comments ao diff com um revisor independente.
Mantenha apenas comentários que comprovem uma exceção da lista estrita.
Remova os demais e corrija as causas dos achados dentro do escopo.
Mostre propostas de guardrails antes de aplicá-las e informe restrições
que continuarem sem proteção. Execute as verificações relevantes.
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

Example request after loading `blast-radius`:

```text
Investigue o que este diff pode quebrar fora dos arquivos alterados.
Identifique as premissas críticas e execute verificações focadas no código real.
Mostre evidências, riscos ainda não comprovados e cenários descartados.
Não aplique correções no produto.
```

Example request after loading `reflect`:

```text
Reflita sobre esta sessão com três revisores independentes.
Identifique aprendizados duráveis e confira as skills antes de propor alterações.
Mostre o texto e o destino das propostas, rejeições e backlog estrutural.
Não aplique mudanças nem abra tickets ainda.
```

Example request after loading `benchmark-checklist`:

```text
Compare o desempenho de [baseline] e [candidato] no cenário [X].
Confira o trabalho executado, a correção dos resultados e as configurações.
Repita as medições, investigue o gargalo e mostre os dados e as limitações.
Não execute carga em produção.
```

Example request after loading `technical-writing`:

```text
Escreva a documentação de [X] para [público], com comandos e exemplos verificados.
Escolha a estrutura adequada e indique o que não conseguiu confirmar.
```

Example request after loading `unslop`:

```text
Revise este texto para remover linguagem vaga, repetição e jargão desnecessário.
Preserve os fatos, as condições, as referências e o grau de certeza.
```

These skills use shared `SKILL.md` instructions for Codex and Claude Code, without Cursor-specific tool names or model identifiers.

`guide-me` composes the ported workflows; it does not include the upstream mode's full playbook suite or platform-specific automation.

## Code-quality principles

These are canonical principle skills, usable directly or loaded on demand by workflows. They guide decisions; they do not authorize a refactor or replace verification. `guide-me` includes a [code-quality workflow](skills/guide-me/references/code-quality.md) that starts with maintenance evidence and applies only the relevant principles.

| Principle | Decision it helps make |
| --- | --- |
| [Type system discipline](skills/principle-type-system-discipline/SKILL.md) | Reject invalid states and semantic mix-ups through types and authoritative schemas. |
| [Make operations idempotent](skills/principle-make-operations-idempotent/SKILL.md) | Make repeated and interrupted operations converge without duplicating effects. |
| [Separate before serializing shared state](skills/principle-separate-before-serializing-shared-state/SKILL.md) | Separate concurrent writers before introducing locks or shared-state coordination. |
| [Migrate callers then delete legacy APIs](skills/principle-migrate-callers-then-delete-legacy-apis/SKILL.md) | Migrate controlled consumers and remove obsolete APIs without breaking supported compatibility. |
| [Attack the premise](skills/principle-attack-the-premise/SKILL.md) | Test the shared assumption behind repeated failed corrections before another patch. |
| [Fix root causes](skills/principle-fix-root-causes/SKILL.md) | Trace the earliest demonstrated contract violation while retaining legitimate safeguards. |
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

## Layout

- `.claude-plugin/marketplace.json` — Claude Code marketplace manifest
- `.claude-plugin/plugin.json` — Claude Code plugin manifest
- `.agents/plugins/marketplace.json` + `.codex-plugin/plugin.json` — Codex equivalents
- `skills/<name>/SKILL.md` — skills
- `commands/<name>.md` — slash commands

## Attribution

Adapted from Lauren Tan’s pstack. See [upstream sources and license notices](ATTRIBUTION.md).
