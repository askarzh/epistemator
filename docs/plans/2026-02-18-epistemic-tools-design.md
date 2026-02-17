# Infotune: Epistemic Tools Plugin — Design Document

## Overview

Infotune is a standalone Claude Code plugin that processes input (concepts, documents, questions, problems) through epistemic frameworks. Users select a framework by slash command or use a meta-command to compare multiple frameworks.

## Frameworks

| ID | Name | Core Method | Best For |
|----|------|-------------|----------|
| scholastic | Modern Scholasticism | Quaestio disputata (Aquinas) | Arguments, claims, propositions |
| cartesian | Cartesian Reductionism | Methodical doubt + decomposition (Descartes) | Complex systems, unclear problems |
| pirsig | Metaphysics of Quality | Static/dynamic quality distinction (Pirsig) | Value judgments, quality disputes |
| lateral | Lateral Analysis | Provocation + movement (De Bono) | Stuck thinking, creative challenges |

## Architecture: Skills + Commands + Agent

### Plugin Structure

```
infotune/
  .claude-plugin/
    plugin.json
  skills/
    scholastic/SKILL.md
    cartesian/SKILL.md
    pirsig/SKILL.md
    lateral/SKILL.md
  commands/
    scholastic.md
    cartesian.md
    pirsig.md
    lateral.md
    epistemic.md
  agents/
    epistemic-analyst.md
```

### Components

**Skills (4)** — Each SKILL.md contains the framework's methodology and prompt structure. Hybrid depth: embedded key concepts and methodology summaries sufficient to anchor analysis, without full academic reference material.

**Commands (5)** — Thin wrappers. Four framework commands invoke their corresponding skill. One meta-command (`/epistemic`) invokes the agent.

**Agent (1)** — `epistemic-analyst` orchestrates multi-framework analysis. Uses `model: sonnet` for orchestration speed. Delegates deep analysis to skills via Task tool subagents.

## Skill Template

Each framework skill follows this structure:

```markdown
---
name: <framework-id>
description: <when-to-use trigger description>
---

# <Framework Name> Analysis

## Core Methodology
<3-5 key principles>

## Key Concepts
<Terminology and definitions>

## Analysis Protocol

### Structured Mode (default)
<Step-by-step output sections>

### Interactive Mode
<Socratic questioning sequence>

## Output Structure
<Headings the analysis produces>
```

## Framework Output Structures

### Modern Scholastic
- Question (quaestio)
- Thesis (videtur quod)
- Objections (steel-manned, sed contra)
- Replies (respondeo)
- Determination (synthesis)

### Cartesian Reductionism
- Doubt inventory
- Decomposition tree
- Clear premises (clear and distinct ideas)
- Reconstruction (simple to complex)
- Certainty assessment

### Metaphysics of Quality (Pirsig)
- Quality event identification
- Static/dynamic tension
- Level analysis (inorganic, biological, social, intellectual)
- Quality resolution

### Lateral Analysis (De Bono)
- Dominant pattern identification
- Provocations (po)
- Movement from provocation
- Alternative framings
- Lateral output

## Command Design

### Framework Commands (scholastic, cartesian, pirsig, lateral)

```markdown
---
name: <framework-id>
description: <one-line description>
arguments:
  - name: input
    description: The concept, text, or question to analyze
    required: true
  - name: interactive
    description: Use Socratic mode instead of structured output
    required: false
---

Invoke the `<framework-id>` skill. If --interactive, use Interactive Mode.
```

### Meta-Command (epistemic)

```markdown
---
name: epistemic
description: Multi-framework epistemic analysis
arguments:
  - name: input
    description: The concept, text, or question to analyze
    required: true
  - name: mode
    description: compare | suggest | pick
    required: false
---

Invoke the epistemic-analyst agent. Default mode: suggest.
```

## Agent Design

### Modes

**suggest (default)** — Classifies input, recommends 2-3 frameworks with reasoning, asks user to confirm, runs selected frameworks.

**compare** — Runs all frameworks in parallel via Task tool subagents. Produces comparative synthesis with: convergence points, divergence points, synthesis, meta-observation.

**pick** — Presents frameworks via AskUserQuestion (multi-select), runs selected ones, compares.

### Comparative Output Structure

```
## Comparative Analysis
### Points of Convergence
### Points of Divergence
### Synthesis
### Meta-Observation
```

## Extensibility

Adding a new framework requires:

1. `skills/<framework-id>/SKILL.md` — copy template, write methodology
2. `commands/<framework-id>.md` — copy any existing command, change name/description
3. Add row to the Known Frameworks table in `agents/epistemic-analyst.md`

## Skill Content Depth (Hybrid)

Each SKILL.md embeds:
- Core methodology (3-5 principles)
- Key terminology and definitions
- Step-by-step analysis protocol
- Output structure specification

Each SKILL.md does NOT include:
- Full philosophical histories
- Biographical context
- Academic citations
- Exhaustive concept coverage

## Modes of Operation

**Structured (default)** — Produces markdown output following the framework's natural sections.

**Interactive (--interactive)** — Socratic mode. The skill asks probing questions, guides the user through the framework step by step.

## Summary

| Component | Count | Purpose |
|-----------|-------|---------|
| Skills | 4 | Framework methodology + prompt |
| Commands | 5 | User-facing /slash entry points |
| Agent | 1 | Multi-framework orchestration |
| Total files | 12 | Including plugin.json |
