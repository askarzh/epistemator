---
name: scholastic
description: This skill should be used when the user asks to "analyze an argument", "apply scholastic method", "use quaestio disputata", "examine a thesis", "find objections and replies", "apply Thomistic analysis", or wants to process input through the Modern Scholastic framework of structured disputation.
version: 0.1.0
---

# Modern Scholastic Analysis

## Overview

Apply the quaestio disputata method — the structured disputation framework refined by Thomas Aquinas and the medieval Scholastics. This method systematically examines a proposition by articulating the strongest possible objections, then responding to each with precise distinctions.

The Scholastic method excels at analyzing arguments, claims, propositions, and any input where the goal is to determine the truth or validity of a position through rigorous dialectical examination.

## Core Methodology

1. **Formulate the Question (Quaestio)** — Convert the input into a precise yes/no question or a clearly stated thesis. The question must be specific enough to admit determinate answers.

2. **Present the Thesis (Videtur Quod)** — State the initial position to be examined. Present it as a defensible claim with its strongest supporting reasons.

3. **Raise Objections (Objectiones)** — Construct 3-5 steel-manned objections against the thesis. Each objection must be the strongest possible case against the position, not a straw man. Apply the principle of charity: formulate each objection as a thoughtful interlocutor would.

4. **Offer the Sed Contra** — Present the counter-authority or counter-argument that supports the thesis against the objections. This is typically the strongest single reason favoring the thesis.

5. **Determine the Response (Respondeo)** — Provide the main analysis and resolution. This is not a compromise between thesis and objections but a deeper understanding that addresses why the objections fail or succeed. Use precise distinctions (distinguo) to resolve apparent contradictions.

6. **Reply to Each Objection (Ad Objectiones)** — Address each objection individually, showing exactly where it succeeds, fails, or requires qualification. Use the formal distinction pattern: "The objection holds insofar as X, but fails insofar as Y."

7. **Final Determination (Determinatio)** — Synthesize the analysis into a clear, qualified conclusion. State what has been established, what remains uncertain, and what further questions arise.

## Key Concepts

- **Distinguo (Distinction):** The primary analytical tool. When a claim appears both true and false, distinguish the senses in which it is each. Example: "The claim is true in the formal sense but false in the material sense."
- **Principle of Charity:** Every objection must be constructed at maximum strength. Weak objections produce weak analysis.
- **Sed Contra vs. Respondeo:** The sed contra is a single authoritative counter-point; the respondeo is the full analytical resolution. They serve different functions.
- **Qualification over Refutation:** The goal is rarely to completely destroy a position but to determine the precise conditions under which it holds or fails.

## Analysis Protocol

### Structured Mode (default)

Produce the analysis in this exact section order:

```
## Quaestio
[The precise question under examination]

## Videtur Quod (Thesis)
[The position and its supporting reasons]

## Objectiones
### Objection 1
[Steel-manned objection]
### Objection 2
[Steel-manned objection]
### Objection 3
[Steel-manned objection]

## Sed Contra
[The strongest counter-authority or counter-argument]

## Respondeo
[Main analysis with distinctions]

## Ad Objectiones
### Reply to Objection 1
[Precise reply using distinctions]
### Reply to Objection 2
[Precise reply using distinctions]
### Reply to Objection 3
[Precise reply using distinctions]

## Determinatio
[Final qualified conclusion]
```

### Interactive Mode

When the user requests interactive/Socratic analysis:

1. Begin by asking the user to state their position or question clearly
2. Help refine the quaestio through clarifying questions
3. Present one objection at a time and ask the user to respond before offering the next
4. After all objections are raised, present the sed contra and ask for the user's initial synthesis
5. Offer the respondeo as a collaborative refinement of the user's thinking
6. Conclude with the determinatio, noting where the user's understanding evolved

## When to Apply This Framework

**Strong fit:**
- Evaluating truth claims or propositions
- Analyzing philosophical or ethical arguments
- Examining policy positions with competing considerations
- Any input where "Is X true/valid/justified?" is the core question

**Weak fit:**
- Creative ideation (use Six Thinking Hats instead)
- Systems decomposition (use Cartesian Reductionism instead)
- Value/quality judgments without propositional structure (use Pirsig instead)
