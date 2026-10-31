---
name: unslop
description: Edit prose to remove filler, vague claims, repetitive framing, invented jargon, and other distracting patterns while preserving meaning, evidence, uncertainty, and the intended voice. Use for a requested prose cleanup or a final clarity pass.
---

# Unslop

Make the text specific, natural, and useful. Preserve the author's intended meaning and tone, the user's format, and the language of the artifact. These are editing heuristics, not a detector of whether a person or model wrote the text.

## Establish what must survive

Read the whole passage before editing. Identify the main point, audience, factual claims, conditions, uncertainty, citations, and action the reader should take. Respect exact quotations, identifiers, commands, API contracts, legal wording, and user-mandated terminology. A prose pass does not authorize modifying code or removing a substantive requirement.

When a claim is unsupported, do not invent a source or measured improvement. Remove it only when meaning remains intact; otherwise flag it, ask for missing evidence when necessary, or clearly qualify it. Preserve the difference between “may”, “does”, and “proved”.

## Edit the distracting patterns

- **Empty framing and flattery:** remove canned acknowledgments, praise, offers to help, and generic introductions or conclusions that do not serve the passage.
- **Filler:** replace long phrases with their direct equivalent and delete throat-clearing. Retain conditions and causal explanations that matter.
- **Vague attribution:** name the actual source when provided. “Experts say” is not evidence. Do not erase an important unresolved sourcing gap by making the claim sound certain.
- **Vague impact:** replace “significantly improves” or “seamlessly integrates” with an observed mechanism or supported result. If no evidence exists, keep the limitation visible.
- **Decorative vocabulary:** prefer plain words over ornate synonyms, abstract metaphors, and unnecessary nominalizations. Keep established technical meanings such as a mathematical vector or a test harness when they are precise.
- **Unnecessary contrast:** state the point directly instead of repeatedly introducing “not just X, but Y” or a false alternative. Preserve contrast when the distinction is the substance.
- **Forced symmetry:** remove artificial groups of three, meaningless “from X to Y” ranges, and parallel phrasing that distorts the actual ideas.
- **Synonym cycling:** use one name for one concept. Repetition of the correct term is clearer than teaching several names for the same thing.
- **Heavy formatting:** reduce decorative bold, emoji, repeated inline headings, and headings that merely repeat the next sentence. Keep lists and tables when they make comparison or sequence easier.
- **Punctuation as a crutch:** rewrite repeated dash or colon pivots into sentences with clear relationships. Follow language and repository typography rather than altering code, quoted punctuation, or every valid colon mechanically.
- **Over-hedging:** replace stacked qualifiers with one accurate expression of uncertainty. Do not turn an inference into a fact.
- **Dense sentences and passive constructions:** clarify the actor, split overloaded clauses, and resolve pronouns. Keep passive voice when the actor is unknown or unimportant.
- **Over-compression:** restore articles, verbs, and explicit relationships where fragments, arrows, or abbreviations make the reader decode the prose.

Apply judgment instead of global word replacement. A word that is filler in one sentence may be necessary terminology in another. Do not remove useful specifics merely because a sentence could appear in another project's documentation.

## Verify the rewrite

Compare original and revised claims, including negations, quantities, conditions, attribution, certainty, and exceptions. Check that links and literal technical content survive. The revision should convey the same supported information with less friction, not a more confident or different story.

For a file edit, inspect the diff and perform checks relevant to changed links or examples; do not run unrelated application tests for a prose-only change. For a rewrite request, return the improved text, adding only material factual concerns the user needs. Explain editing rules only when asked. Do not automatically edit this skill or create a permanent rule from one phrase.
