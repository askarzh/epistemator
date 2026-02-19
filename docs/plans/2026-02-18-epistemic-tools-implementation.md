# Epistemator: Epistemic Tools Plugin — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a standalone Claude Code plugin with four epistemic analysis frameworks plus a multi-framework comparison agent.

**Architecture:** Skills + Commands + Agent. Each framework is a skill with embedded methodology. Thin command wrappers expose skills as slash commands. An agent orchestrates multi-framework comparison.

**Tech Stack:** Claude Code plugin (Markdown, YAML frontmatter, JSON manifest)

---

### Task 1: Plugin Scaffold

**Files:**
- Create: `.claude-plugin/plugin.json`
- Create: `.gitignore`

**Step 1: Create plugin manifest**

Create `.claude-plugin/plugin.json`:

```json
{
  "name": "epistemator",
  "version": "0.1.0",
  "description": "Epistemic analysis tools — process ideas, texts, and questions through philosophical frameworks",
  "author": {
    "name": "Askar"
  },
  "license": "MIT",
  "keywords": ["epistemology", "analysis", "philosophy", "thinking-tools"]
}
```

**Step 2: Create .gitignore**

```
.DS_Store
*.swp
*.swo
```

**Step 3: Create directory structure**

```bash
mkdir -p skills/scholastic skills/cartesian skills/pirsig skills/lateral
mkdir -p commands agents
```

**Step 4: Commit**

```bash
git add .claude-plugin/plugin.json .gitignore
git commit -m "feat: scaffold epistemator plugin structure"
```

---

### Task 2: Modern Scholastic Skill

**Files:**
- Create: `skills/scholastic/SKILL.md`

**Step 1: Write skill**

Create `skills/scholastic/SKILL.md`:

```markdown
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
- Creative ideation (use Lateral Analysis instead)
- Systems decomposition (use Cartesian Reductionism instead)
- Value/quality judgments without propositional structure (use Pirsig instead)
```

**Step 2: Commit**

```bash
git add skills/scholastic/SKILL.md
git commit -m "feat: add Modern Scholastic analysis skill"
```

---

### Task 3: Cartesian Reductionism Skill

**Files:**
- Create: `skills/cartesian/SKILL.md`

**Step 1: Write skill**

Create `skills/cartesian/SKILL.md`:

```markdown
---
name: cartesian
description: This skill should be used when the user asks to "decompose a problem", "apply Cartesian method", "break this down systematically", "reduce to first principles", "analyze from the ground up", "apply methodical doubt", or wants to process input through Cartesian Reductionism to decompose complex wholes into clear, distinct parts.
version: 0.1.0
---

# Cartesian Reductionist Analysis

## Overview

Apply Descartes' method of analysis from the Discourse on Method and Rules for the Direction of the Mind. This method systematically doubts, decomposes, orders, and enumerates to arrive at clear and distinct understanding of any subject.

Cartesian Reductionism excels at analyzing complex systems, unclear problems, tangled arguments, and any input where the whole is too complex to grasp without decomposition.

## Core Methodology — The Four Rules

1. **Rule of Evidence (Doubt)** — Accept nothing as true that is not clearly and distinctly known to be so. Identify every assumption, presupposition, and received opinion in the input. Suspend judgment on anything that admits the slightest doubt.

2. **Rule of Division (Decompose)** — Divide the subject into as many parts as possible and as necessary for adequate resolution. Each part should be simple enough to be understood in isolation. Continue subdividing until reaching elements that are self-evident or irreducible.

3. **Rule of Order (Reconstruct)** — Begin with the simplest, most easily known elements and ascend step by step to knowledge of the most complex. Each step must follow necessarily from the previous. Build understanding from foundations upward.

4. **Rule of Enumeration (Verify)** — Make enumerations so complete and reviews so comprehensive that nothing is omitted. Check every link in the chain. Ensure no part has been skipped or assumed.

## Key Concepts

- **Clear and Distinct Ideas:** An idea is clear when it is present and accessible to the attentive mind. It is distinct when it is sharply separated from all other ideas, containing nothing that belongs to something else. Both criteria must be met.
- **Methodical Doubt as Tool:** Doubt is not the conclusion but the instrument. It strips away assumptions to reveal what can be known with certainty. After doubt, reconstruction on firm foundations begins.
- **Simple Natures:** The irreducible elements reached through decomposition. In Descartes' system: extension, figure, motion for physical things; thought, doubt, will for mental things. In applied analysis: the atomic concepts or facts that resist further division.
- **Order of Reasons:** The chain from simple to complex must be unbroken. Each conclusion depends only on what precedes it. If any link is uncertain, everything after it is uncertain.

## Analysis Protocol

### Structured Mode (default)

Produce the analysis in this exact section order:

```
## Subject Statement
[What is being analyzed, in one clear sentence]

## Doubt Inventory
### Assumptions Identified
- [Assumption 1]: [Why it is doubtable]
- [Assumption 2]: [Why it is doubtable]
- [...]
### What Survives Doubt
- [Element 1]: [Why it is indubitable or well-grounded]
- [...]

## Decomposition Tree
[Break the subject into its constituent parts, recursively]
- Component A
  - Sub-component A.1
  - Sub-component A.2
    - Element A.2.a
    - Element A.2.b
- Component B
  - [...]

## Clear Premises
[List only the elements that are clear and distinct — the foundation for reconstruction]
1. [Premise 1] — [Why it is clear and distinct]
2. [Premise 2] — [Why it is clear and distinct]
3. [...]

## Reconstruction
[Build back up from clear premises to understanding of the whole, step by step]
1. From Premise 1 and 2, it follows that [X]
2. Combined with Premise 3, this entails [Y]
3. Therefore, the complex whole can be understood as [Z]

## Certainty Assessment
[Rate each component of the reconstruction]
- [Conclusion 1]: **Certain** / **Probable** / **Doubtful**
- [Conclusion 2]: **Certain** / **Probable** / **Doubtful**
- Overall assessment: [Summary of what is firmly known vs. what remains uncertain]
```

### Interactive Mode

When the user requests interactive/Socratic analysis:

1. Ask the user to state the subject or problem they want to decompose
2. Walk through the doubt inventory together: present each assumption and ask if the user sees others
3. Decompose collaboratively: propose divisions and ask if they are atomic enough or need further splitting
4. Identify clear premises together: ask the user which elements feel indubitable
5. Reconstruct step by step: present each inference and ask if it follows necessarily
6. Assess certainty together: discuss which conclusions are firm and which are tentative

## When to Apply This Framework

**Strong fit:**
- Complex systems that need to be understood piece by piece
- Problems where hidden assumptions may be causing confusion
- Technical architectures, business processes, or logical arguments that need decomposition
- Any input where "What are the fundamental parts and how do they relate?" is the core question

**Weak fit:**
- Value judgments or quality assessments (use Pirsig instead)
- Evaluating the truth of a specific proposition (use Scholastic instead)
- Generating creative alternatives (use Lateral Analysis instead)
```

**Step 2: Commit**

```bash
git add skills/cartesian/SKILL.md
git commit -m "feat: add Cartesian Reductionist analysis skill"
```

---

### Task 4: Metaphysics of Quality Skill (Pirsig)

**Files:**
- Create: `skills/pirsig/SKILL.md`

**Step 1: Write skill**

Create `skills/pirsig/SKILL.md`:

```markdown
---
name: pirsig
description: This skill should be used when the user asks to "assess quality", "apply Pirsig's framework", "analyze through Metaphysics of Quality", "evaluate static vs dynamic quality", "examine value conflicts", "apply MoQ", or wants to process input through Pirsig's Metaphysics of Quality to understand value, quality, and the tensions between static patterns and dynamic change.
version: 0.1.0
---

# Metaphysics of Quality Analysis (Pirsig)

## Overview

Apply Robert Pirsig's Metaphysics of Quality (MoQ) from Zen and the Art of Motorcycle Maintenance and Lila. This framework treats Quality as the fundamental reality — prior to subjects and objects — and analyzes experience through the interplay of Dynamic Quality (the cutting edge of experience) and Static Quality (the patterns that latch and preserve what Dynamic Quality discovers).

The MoQ excels at analyzing value judgments, quality disputes, cultural and institutional conflicts, and any input where the question is "What is better?" or "Why does this feel right/wrong?"

## Core Methodology

1. **Identify the Quality Event** — Locate the pre-intellectual moment of quality recognition. Before analysis, something was perceived as good, bad, better, or worse. Name that perception without immediately rationalizing it. Quality is the event that precedes and motivates analysis, not the conclusion of it.

2. **Map Static Quality Patterns** — Classify the static patterns at play across Pirsig's four levels:
   - **Inorganic:** Physical laws, material constraints, biological necessities
   - **Biological:** Life processes, health, survival, bodily needs
   - **Social:** Customs, institutions, laws, cultural norms, group expectations
   - **Intellectual:** Ideas, theories, truths, principles, individual understanding

   Higher levels depend on but are not reducible to lower ones. Each level has its own quality patterns.

3. **Locate the Static/Dynamic Tension** — Identify where Dynamic Quality (novelty, evolution, the undefined better) is pushing against Static Quality (established patterns, tradition, stability). Most interesting quality conflicts are tensions between these forces.

4. **Analyze Level Conflicts** — When static patterns at different levels conflict, the MoQ provides a moral hierarchy: intellectual patterns should not be subordinated to social ones; social patterns should not be subordinated to biological ones. But Dynamic Quality supersedes all static patterns. Identify which levels are in conflict and how the hierarchy applies.

5. **Assess Quality Resolution** — Determine how the tension resolves: Does Dynamic Quality succeed in creating a new, better static pattern? Does an existing static pattern rightly resist a change that would degrade quality? Or is the situation a genuine dilemma where quality is lost either way?

## Key Concepts

- **Quality as Pre-Intellectual:** Quality is not a property of objects or a subjective feeling. It is the event of recognition that occurs before the subject/object division. "Quality is the knife that divides subject from object."
- **Dynamic Quality:** The undefined, leading edge of experience. It is what drives evolution, creativity, and improvement. It cannot be defined without becoming static, but it is recognized in the moment of encounter.
- **Static Quality:** The patterns that preserve Dynamic Quality's discoveries. Without static patterns, no progress would be retained. But static patterns can also become prisons when they resist needed change.
- **The Four Levels:** Each level is an evolutionary platform. Inorganic patterns enable biological ones; biological enable social; social enable intellectual. Conflicts between levels are moral conflicts, not merely practical ones.
- **Degeneracy:** When a lower level dominates a higher one (e.g., social conformity crushing intellectual inquiry, or biological urges overriding social obligations). The MoQ treats this as a quality degradation.

## Analysis Protocol

### Structured Mode (default)

Produce the analysis in this exact section order:

```
## Quality Event
[Name the pre-intellectual quality perception — what was recognized as good, bad, better, or worse, before analysis began]

## Static Pattern Map
### Inorganic Level
[Physical/material constraints and patterns at play]
### Biological Level
[Life, health, survival patterns at play]
### Social Level
[Institutional, cultural, normative patterns at play]
### Intellectual Level
[Ideas, theories, principles at play]

## Dynamic/Static Tension
[Where is Dynamic Quality pushing against established patterns? What is the "new" trying to emerge? What is the "old" trying to preserve?]

## Level Conflict Analysis
[Which levels are in conflict? How does the moral hierarchy apply? Is there degeneracy — a lower level dominating a higher one?]

## Quality Resolution
[How does or should the tension resolve? Does a new static pattern emerge? Does an existing pattern rightly hold? Is quality lost either way?]

## Quality Assessment
[Final judgment: What does the MoQ reveal about this situation that other frameworks might miss? What is the quality of the situation, and what would improve it?]
```

### Interactive Mode

When the user requests interactive/Socratic analysis:

1. Ask the user to describe what prompted their inquiry — what felt good, bad, or conflicted
2. Help identify the pre-intellectual quality event before rationalizing
3. Map static patterns level by level, asking the user to identify what patterns they see at each level
4. Explore the dynamic/static tension together: ask what the user feels is trying to change and what is resisting
5. Analyze level conflicts: present the hierarchy and ask the user where they see degeneracy or healthy tension
6. Arrive at the quality resolution collaboratively

## When to Apply This Framework

**Strong fit:**
- Evaluating whether something is good, better, or worse (quality judgments)
- Cultural, institutional, or personal value conflicts
- Situations where "something feels off" but the reason is unclear
- Debates about tradition vs. innovation, stability vs. change
- Any input where "What is the quality here?" is the core question

**Weak fit:**
- Formal logical arguments (use Scholastic instead)
- Systems decomposition (use Cartesian Reductionism instead)
- Generating creative alternatives (use Lateral Analysis instead)
```

**Step 2: Commit**

```bash
git add skills/pirsig/SKILL.md
git commit -m "feat: add Metaphysics of Quality (Pirsig) analysis skill"
```

---

### Task 5: Lateral Analysis Skill (De Bono)

**Files:**
- Create: `skills/lateral/SKILL.md`

**Step 1: Write skill**

Create `skills/lateral/SKILL.md`:

```markdown
---
name: lateral
description: This skill should be used when the user asks to "think laterally", "apply De Bono's method", "break out of this pattern", "generate creative alternatives", "use lateral thinking", "apply provocation", "use Six Hats", "challenge assumptions", or wants to process input through Edward de Bono's Lateral Thinking to escape dominant patterns and generate new perspectives.
version: 0.1.0
---

# Lateral Analysis (De Bono)

## Overview

Apply Edward de Bono's Lateral Thinking method from Lateral Thinking, Po: Beyond Yes and No, and Six Thinking Hats. This method deliberately breaks established thinking patterns to generate new ideas and perspectives. Unlike vertical (logical) thinking which digs the same hole deeper, lateral thinking digs new holes in new places.

Lateral Analysis excels at stuck problems, creative challenges, innovation, and any input where the existing frame of thinking has become a trap.

## Core Methodology

1. **Identify the Dominant Pattern** — Every problem arrives with an established way of thinking about it. Name the dominant pattern explicitly: "The usual way to think about this is X." This pattern is not wrong — it is simply the hole that has already been dug.

2. **Apply Provocation (Po)** — Construct deliberate provocations that violate the dominant pattern. The word "Po" signals that a statement is a provocation, not a proposition. Provocations are not meant to be true or reasonable — they are stepping stones. Techniques:
   - **Reversal:** State the opposite of the normal relationship. "Po: customers pay us to take their product away."
   - **Exaggeration:** Push a variable to an extreme. "Po: the meeting lasts 30 seconds."
   - **Distortion:** Change the normal sequence or relationship. "Po: the packaging is more valuable than the product."
   - **Wishful Thinking:** State an impossible ideal. "Po: everyone already knows the answer."
   - **Random Entry:** Introduce an unrelated word or concept and force a connection.

3. **Movement** — The critical step. From each provocation, move to a practical idea. Do not judge the provocation — extract value from it. Movement techniques:
   - **Moment to Moment:** Follow the provocation forward in time. "If this were true, what would happen next?"
   - **Extract a Principle:** What principle underlies the provocation? "The principle here is that time scarcity forces prioritization."
   - **Focus on the Difference:** What is different about the world the provocation creates? "The difference is that value is in the wrapper, not the content."
   - **Positive Aspects:** What is useful about this, even partially?

4. **Escape** — Identify the boundaries of the dominant pattern that are not actually necessary. Question each constraint: "Is this required, or just assumed?" Remove unnecessary constraints to create new possibility space.

5. **Harvest** — Collect all lateral outputs: new ideas, reframed perspectives, challenged assumptions, alternative approaches. Not all will be useful. Select the most promising for development.

## Key Concepts

- **Vertical vs. Lateral:** Vertical thinking is sequential, logical, and deepens the current approach. Lateral thinking is discontinuous, provocative, and opens new approaches. Both are needed; lateral thinking generates, vertical thinking develops.
- **Po:** A signaling word indicating provocation. "Po" is neither true nor false — it is a thinking operation. It gives permission to state unreasonable things as starting points.
- **Movement vs. Judgment:** The natural response to a provocation is to judge it ("That's ridiculous"). Movement replaces judgment: instead of asking "Is this true?" ask "Where does this lead?"
- **Pattern Asymmetry:** The brain is a self-organizing pattern system. Once a pattern is established, it is very difficult to restructure from within. Lateral thinking provides tools to escape from outside the pattern.
- **Six Thinking Hats (Optional Structuring Device):** White (facts), Red (feelings), Black (caution), Yellow (optimism), Green (creativity), Blue (process). Use when the analysis benefits from separating different modes of thought.

## Analysis Protocol

### Structured Mode (default)

Produce the analysis in this exact section order:

```
## Dominant Pattern
[Name the established way of thinking about this input]
[What assumptions does this pattern carry?]
[What does this pattern make it hard to see?]

## Provocations
### Provocation 1 (Reversal)
Po: [Reversal of a key relationship]
→ Movement: [Where this leads]
→ Idea: [Practical concept extracted]

### Provocation 2 (Exaggeration)
Po: [Extreme version of a variable]
→ Movement: [Where this leads]
→ Idea: [Practical concept extracted]

### Provocation 3 (Distortion/Random Entry)
Po: [Changed sequence or random connection]
→ Movement: [Where this leads]
→ Idea: [Practical concept extracted]

## Escape Analysis
### Constraint Audit
- [Constraint 1]: **Required** / **Assumed** — [rationale]
- [Constraint 2]: **Required** / **Assumed** — [rationale]
- [...]
### Possibilities from Removed Constraints
[What becomes possible when assumed constraints are dropped?]

## Alternative Framings
[2-3 completely different ways to frame the original input]
1. [Reframe 1]: [How this changes the problem/opportunity]
2. [Reframe 2]: [How this changes the problem/opportunity]
3. [Reframe 3]: [How this changes the problem/opportunity]

## Lateral Output
### Most Promising Ideas
[Ranked list of new ideas, perspectives, or approaches generated]
### Recommended Next Steps
[Which ideas merit development through vertical thinking]
```

### Interactive Mode

When the user requests interactive/Socratic analysis:

1. Ask the user to describe the situation or problem they want to think about differently
2. Name the dominant pattern together — ask what the "obvious" way of thinking about it is
3. Generate provocations collaboratively: offer one, ask the user to react and generate one of their own
4. Practice movement together: when the user judges a provocation, redirect to "Where could this lead?"
5. Audit constraints together: list assumptions and ask which ones are truly necessary
6. Harvest ideas: collect what emerged and ask the user which feel most promising

## When to Apply This Framework

**Strong fit:**
- Stuck problems where the same solutions keep being proposed
- Innovation and creative challenges
- Situations where "we've always done it this way" is blocking progress
- Generating alternatives when the current approach feels stale
- Any input where "What else could this be?" is the core question

**Weak fit:**
- Evaluating truth claims (use Scholastic instead)
- Systematic decomposition of complex systems (use Cartesian Reductionism instead)
- Value/quality judgments (use Pirsig instead)
```

**Step 2: Commit**

```bash
git add skills/lateral/SKILL.md
git commit -m "feat: add Lateral Analysis (De Bono) skill"
```

---

### Task 6: Framework Slash Commands

**Files:**
- Create: `commands/scholastic.md`
- Create: `commands/cartesian.md`
- Create: `commands/pirsig.md`
- Create: `commands/lateral.md`

**Step 1: Write all four commands**

Create `commands/scholastic.md`:

```markdown
---
description: Analyze through Modern Scholastic method (quaestio disputata)
argument-hint: [--interactive] <input>
---

Invoke the `scholastic` skill to analyze the user's input.

If the user includes `--interactive` in their arguments, use Interactive Mode as described in the skill. Otherwise, use Structured Mode.

The user's input to analyze: $ARGUMENTS
```

Create `commands/cartesian.md`:

```markdown
---
description: Decompose through Cartesian Reductionism (methodical doubt)
argument-hint: [--interactive] <input>
---

Invoke the `cartesian` skill to analyze the user's input.

If the user includes `--interactive` in their arguments, use Interactive Mode as described in the skill. Otherwise, use Structured Mode.

The user's input to analyze: $ARGUMENTS
```

Create `commands/pirsig.md`:

```markdown
---
description: Evaluate through Metaphysics of Quality (Pirsig)
argument-hint: [--interactive] <input>
---

Invoke the `pirsig` skill to analyze the user's input.

If the user includes `--interactive` in their arguments, use Interactive Mode as described in the skill. Otherwise, use Structured Mode.

The user's input to analyze: $ARGUMENTS
```

Create `commands/lateral.md`:

```markdown
---
description: Generate alternatives through Lateral Analysis (De Bono)
argument-hint: [--interactive] <input>
---

Invoke the `lateral` skill to analyze the user's input.

If the user includes `--interactive` in their arguments, use Interactive Mode as described in the skill. Otherwise, use Structured Mode.

The user's input to analyze: $ARGUMENTS
```

**Step 2: Commit**

```bash
git add commands/scholastic.md commands/cartesian.md commands/pirsig.md commands/lateral.md
git commit -m "feat: add slash commands for all four epistemic frameworks"
```

---

### Task 7: Epistemic Analyst Agent

**Files:**
- Create: `agents/epistemic-analyst.md`

**Step 1: Write agent**

Create `agents/epistemic-analyst.md`:

```markdown
---
name: epistemic-analyst
description: Use this agent when the user invokes /epistemic for multi-framework analysis — compares epistemic lenses, auto-suggests frameworks, or lets user pick interactively. Examples:

 <example>
 Context: The user is creating a code-review agent that should be called after a logical chunk of code is written.
 user: "/epistemic Is democracy the best form of government?"
 assistant: "I'll use the epistemic-analyst agent to suggest which frameworks would best illuminate this question."
 <commentary>
 The /epistemic command triggers multi-framework analysis. Default mode is suggest.
 </commentary>
 </example>

 <example>
 Context: User wants to compare multiple philosophical perspectives on a topic.
 user: "/epistemic --compare The tension between individual freedom and collective responsibility"
 assistant: "I'll use the epistemic-analyst agent to run all four frameworks in parallel and produce a comparative synthesis."
 <commentary>
 The --compare flag triggers running all frameworks and producing comparative output.
 </commentary>
 </example>

 <example>
 Context: User wants to select specific frameworks to apply.
 user: "/epistemic --pick Should our startup pivot to a subscription model?"
 assistant: "I'll use the epistemic-analyst agent to let you choose which frameworks to apply."
 <commentary>
 The --pick flag presents framework choices before running analysis.
 </commentary>
 </example>

model: sonnet
color: cyan
tools:
  - Task
  - AskUserQuestion
  - Read
  - Glob
---

You are the Epistemic Analyst, an orchestrator that applies multiple philosophical analysis frameworks to a single input and synthesizes the results.

**Your Core Responsibilities:**
1. Determine which epistemic frameworks best fit the user's input
2. Run selected frameworks (via subagents or sequentially)
3. Synthesize results into a comparative analysis

**Known Frameworks:**

| ID | Name | Best For |
|----|------|----------|
| scholastic | Modern Scholasticism | Arguments, claims, propositions — "Is X true?" |
| cartesian | Cartesian Reductionism | Complex systems, unclear problems — "What are the parts?" |
| pirsig | Metaphysics of Quality | Value judgments, quality disputes — "What is better?" |
| lateral | Lateral Analysis | Stuck thinking, creative challenges — "What else could this be?" |

**Modes of Operation:**

### Suggest Mode (default)

1. Read the user's input carefully
2. Classify it: Is it an argument/claim? A complex system? A value judgment? A stuck problem?
3. Recommend 2-3 frameworks with brief reasoning for each
4. Use AskUserQuestion to let the user confirm or adjust the selection
5. Run the confirmed frameworks sequentially, applying each skill's Structured Mode
6. Produce a Comparative Synthesis (see output format below)

### Compare Mode (--compare)

1. Run all four frameworks on the input
2. Use the Task tool to run frameworks in parallel where possible (one subagent per framework)
3. Each subagent should apply the framework's Structured Mode analysis
4. Collect all results and produce a Comparative Synthesis

### Pick Mode (--pick)

1. Present all four frameworks with one-line descriptions using AskUserQuestion (multi-select enabled)
2. Run only the selected frameworks
3. Produce a Comparative Synthesis

**Comparative Synthesis Output Format:**

After running multiple frameworks, always produce this synthesis:

```
## Comparative Analysis

### Points of Convergence
[Where do the frameworks agree? What do multiple lenses confirm?]

### Points of Divergence
[Where do the frameworks disagree? What does each see that others miss?]

### Synthesis
[What is learned by seeing the input through multiple lenses that no single lens would reveal?]

### Meta-Observation
[What does the pattern of agreement/disagreement tell us about the nature of the question itself? Is it primarily a truth question, a complexity question, a quality question, or a creativity question?]
```

**Quality Standards:**
- Never run a framework without the user's awareness of which frameworks are being applied
- In suggest mode, always explain WHY a framework fits before running it
- The comparative synthesis is the primary deliverable — individual framework outputs are supporting material
- Keep individual framework analyses complete but concise; the synthesis is where the value compounds

**Edge Cases:**
- If the input is extremely short or vague, ask for clarification before selecting frameworks
- If only one framework is selected/suggested, skip the comparative synthesis and just run that framework directly
- If the user provides a --mode flag that is not recognized, default to suggest mode and inform the user
```

**Step 2: Commit**

```bash
git add agents/epistemic-analyst.md
git commit -m "feat: add epistemic-analyst agent for multi-framework comparison"
```

---

### Task 8: Epistemic Meta-Command

**Files:**
- Create: `commands/epistemic.md`

**Step 1: Write command**

Create `commands/epistemic.md`:

```markdown
---
description: Multi-framework epistemic analysis — compare, suggest, or pick frameworks
argument-hint: [--compare|--pick] <input>
---

Invoke the `epistemic-analyst` agent with the user's input.

Determine the mode from arguments:
- If `--compare` is present: use Compare mode (run all frameworks in parallel)
- If `--pick` is present: use Pick mode (let user choose frameworks)
- Otherwise: use Suggest mode (auto-recommend frameworks, ask user to confirm)

The user's input to analyze: $ARGUMENTS
```

**Step 2: Commit**

```bash
git add commands/epistemic.md
git commit -m "feat: add /epistemic meta-command for multi-framework analysis"
```

---

### Task 9: Validate Plugin Structure

**Step 1: Verify all files exist**

```bash
ls -R .claude-plugin/ skills/ commands/ agents/
```

Expected output:
```
.claude-plugin/:
plugin.json

skills/:
scholastic/  cartesian/  pirsig/  lateral/

skills/scholastic/:
SKILL.md

skills/cartesian/:
SKILL.md

skills/pirsig/:
SKILL.md

skills/lateral/:
SKILL.md

commands/:
scholastic.md  cartesian.md  pirsig.md  lateral.md  epistemic.md

agents/:
epistemic-analyst.md
```

**Step 2: Verify plugin.json is valid JSON**

```bash
python3 -c "import json; json.load(open('.claude-plugin/plugin.json')); print('Valid JSON')"
```

Expected: `Valid JSON`

**Step 3: Verify all SKILL.md files have valid frontmatter**

```bash
for f in skills/*/SKILL.md; do echo "=== $f ==="; head -5 "$f"; echo; done
```

Expected: Each file starts with `---` and has `name:` and `description:` fields.

**Step 4: Verify all command files have valid frontmatter**

```bash
for f in commands/*.md; do echo "=== $f ==="; head -5 "$f"; echo; done
```

Expected: Each file starts with `---` and has `description:` field.

**Step 5: Verify agent file has valid frontmatter**

```bash
head -10 agents/epistemic-analyst.md
```

Expected: Has `name:`, `description:`, `model:`, `color:`, `tools:` fields.

**Step 6: Final commit if any fixes were needed**

```bash
git status
# If clean, no commit needed
# If fixes were made:
git add -A && git commit -m "fix: correct any validation issues"
```
