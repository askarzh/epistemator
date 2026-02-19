# Epistemator

Epistemic analysis tools for [Claude Code](https://claude.ai/code) — process ideas, texts, and questions through philosophical reasoning frameworks.

## What It Does

Epistemator is a Claude Code plugin that provides four philosophical analysis frameworks as slash commands. Each framework offers a different lens for examining a topic, and a meta-command lets you combine multiple frameworks for comparative analysis.

## Frameworks

| Command | Framework | Question It Answers |
|---------|-----------|-------------------|
| `/scholastic` | Modern Scholasticism (Aquinas) | "Is X true?" — structured disputation via quaestio disputata |
| `/cartesian` | Cartesian Reductionism (Descartes) | "What are the parts?" — systematic decomposition to first principles |
| `/pirsig` | Metaphysics of Quality (Pirsig) | "What is better?" — analysis through static/dynamic quality patterns |
| `/lateral` | Lateral Thinking (De Bono) | "What else could this be?" — breaking dominant patterns for new perspectives |
| `/epistemic` | Multi-framework orchestrator | Suggests, compares, or lets you pick frameworks |

## Usage

### Single Framework

```
/scholastic Is free will compatible with determinism?
/cartesian Why is our deployment pipeline so slow?
/pirsig Should we prioritize code elegance or shipping speed?
/lateral We've tried everything to reduce churn — what are we missing?
```

Add `--interactive` for Socratic guided analysis instead of structured output:

```
/scholastic --interactive Does consciousness require a physical substrate?
```

### Multi-Framework Analysis

```
# Auto-suggest best frameworks (default)
/epistemic Should our startup pivot to a subscription model?

# Run all four in parallel
/epistemic --compare The tension between individual freedom and collective responsibility

# Choose which frameworks to apply
/epistemic --pick Is democracy the best form of government?
```

Multi-framework runs produce a **Comparative Synthesis**: convergence points, divergence points, synthesis, and a meta-observation about the nature of the question itself.

## Installation

Clone or symlink this repository into your Claude Code plugins directory:

```bash
git clone https://github.com/user/epistemator.git
```

Then add the plugin path to your Claude Code settings. The plugin registers itself via `.claude-plugin/plugin.json`.

## Project Structure

```
.claude-plugin/plugin.json    # Plugin manifest
skills/
  scholastic/SKILL.md         # Framework methodology + prompts
  cartesian/SKILL.md
  pirsig/SKILL.md
  lateral/SKILL.md
commands/
  scholastic.md               # Slash command wrappers
  cartesian.md
  pirsig.md
  lateral.md
  epistemic.md                # Multi-framework meta-command
agents/
  epistemic-analyst.md         # Orchestrator agent
docs/plans/                    # Design and implementation docs
```

## Adding a New Framework

1. Create `skills/<id>/SKILL.md` — write the methodology with YAML frontmatter (`name`, `description`, `version`)
2. Create `commands/<id>.md` — thin wrapper that invokes the skill (copy any existing command as template)
3. Add a row to the Known Frameworks table in `agents/epistemic-analyst.md`

## License

MIT
