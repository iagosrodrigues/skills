---
name: technical-writing
description: Write or review technical documentation, RFCs, READMEs, PR descriptions, and commit messages around the reader's task and verifiable facts. Choose an appropriate document structure, use precise terminology, and make procedures executable and clear.
---

# Technical writing

Write so a reader can understand the point on the first pass and act without guessing. Use the user's language for discussion and the repository's established language and style for artifacts. Preserve the requested audience, purpose, format, and scope.

## Establish the document's job

Read relevant project instructions and inspect the code, existing documentation, or supplied source material. Identify the reader's goal and prior knowledge. Use actual symbol, file, command, flag, and UI names. Do not replace a precise project term with a fashionable synonym.

Choose the primary mode:

| Mode | Reader need | Structure |
| --- | --- | --- |
| Tutorial | Learn by building something | State the outcome, give prerequisites, sequence concrete steps, and show observable results early. Keep background brief and link deeper material. |
| How-to | Complete a known task | Start with the goal and necessary setup, then give actions and meaningful decision branches. Put conditions before the steps they govern. |
| Reference | Look up an exact fact | Mirror the API or system structure. State supported values, defaults, errors, limits, and version scope consistently. Mark unknowns rather than guessing. |
| Explanation | Understand reasons and tradeoffs | Bound the question, establish context, explain alternatives and constraints, and distinguish historical evidence from interpretation. |

Keep each section coherent. Split and link incompatible material when that helps navigation, but do not force a useful README or RFC into several files merely to satisfy a taxonomy. Follow required templates. PR descriptions and commit messages are review briefings, not one of these four documentation modes.

## Make the text precise

- Lead with the outcome or the fact the reader needs. Cut introductory filler and promises of what the document will later explain.
- Prefer familiar words and direct verbs. Name the actor when it matters; passive voice is appropriate when the actor is unknown or irrelevant.
- Give instructions as commands. Put prerequisites, warnings, and conditions before actions they constrain. Explain consequences when a reader needs them to choose safely.
- Keep one main idea per sentence and one purpose per paragraph. Split sentences that require rereading, while retaining conditions and causal connections. Vary sentence length naturally.
- Keep each concept's name consistent. Place “only”, “not”, and similar qualifiers beside what they modify. Resolve ambiguous pronouns and long noun chains.
- Preserve articles and connecting words that prevent ambiguity. Concision must not become fragments or compressed code-like prose.
- Use descriptive links, sentence-case headings, numbered steps for sequences, and bullets for genuinely parallel items. Match the document's existing hierarchy.
- Format identifiers and commands as code; distinguish UI labels when useful. Follow the repository's snippet indentation and formatter conventions rather than imposing one indentation style.

Rules serve clarity. Do not apply English-specific grammar or punctuation mechanically to another language, change exact quoted text, or corrupt command syntax to meet a prose rule. Use technical terms when they add precision and define unfamiliar ones on first use. Avoid invented metaphors and jargon that obscure the mechanism.

## Ground instructions and claims

Verify commands, paths, configuration keys, links, and code examples against the relevant revision or supplied sources. Run safe, appropriate checks within authorization when execution is needed. Label commands as inspected or executed, and distinguish expected output from observed output. Do not fabricate successful examples, counts, performance results, or future product behavior.

For procedures, specify working directory, required setup, and the visible result where ambiguity would prevent success. Keep credentials and private data out of examples. Use explicit placeholders only for user-specific values and explain them. Writing a deployment procedure does not authorize running the deployment.

Preserve uncertainty that the evidence requires. A reference can be exact about known facts while marking unavailable or version-dependent information. If a claim needs historical intent, use the available `why` workflow or inspect the original records; current code cannot establish motivation by itself.

## Write reviewable changes

For a PR, describe the concrete problem and resulting behavior, then relevant verification and material limitations. Scale detail to complexity and link large evidence artifacts. Describe the final implementation, not the conversation or discarded plans unless they explain a tradeoff. For commits, follow repository conventions and explain the non-obvious reason when needed.

Product UI strings follow the product's copy conventions. A documentation task does not authorize unrelated product edits, public posting, or changes to other writing skills. Keep suggestions outside scope separate from applied edits.

Before delivery, check that the reader can find the main point, follow the instructions, and distinguish facts from interpretation. Remove repetition and unsupported claims without losing requirements. Report the artifact, substantive changes, checks performed, and remaining factual gaps when relevant; for a simple rewrite, return the rewritten text directly.
