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

### Slash Commands

Each framework has a slash command. Pass your topic or question as the argument:

```
/scholastic Is free will compatible with determinism?
/cartesian Why is our deployment pipeline so slow?
/pirsig Should we prioritize code elegance or shipping speed?
/lateral We've tried everything to reduce churn — what are we missing?
```

### Natural Language

Frameworks also trigger automatically when Claude detects a matching intent:

```
Analyze the argument that AI will replace all programming jobs
Break down our authentication system into its component parts
Assess the quality tradeoff between test coverage and development speed
Think laterally about why our onboarding conversion is low
```

### Modes

**Structured (default)** — produces a complete formatted analysis in a single output, following each framework's methodology step by step.

**Interactive** (`--interactive`) — a Socratic guided session where Claude walks through the analysis one step at a time, asking for your input and refining the analysis collaboratively.

```
/scholastic --interactive Does consciousness require a physical substrate?
/cartesian --interactive Why do our microservices have circular dependencies?
```

### Multi-Framework Analysis

The `/epistemic` command runs multiple frameworks on the same input and produces a comparative synthesis.

```
# Auto-suggest best frameworks, ask for confirmation (default)
/epistemic Should our startup pivot to a subscription model?

# Run all four frameworks in parallel
/epistemic --compare The tension between individual freedom and collective responsibility

# Choose which frameworks to apply
/epistemic --pick Is democracy the best form of government?
```

The comparative synthesis includes: **Convergence** (where frameworks agree), **Divergence** (what each lens sees that others miss), **Synthesis** (insights only visible through multiple lenses), and **Meta-Observation** (what the pattern of agreement reveals about the nature of the question).

### Analyzing Articles and Videos

Pass a URL and Claude will fetch the content and run the analysis on it:

```
/scholastic https://paulgraham.com/greatwork.html
/cartesian https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/
/pirsig https://www.youtube.com/watch?v=8pTEmbeENF4
/lateral https://www.youtube.com/watch?v=UF8uR6Z6KLc
```

Works with `/epistemic` too — compare multiple lenses on the same piece:

```
/epistemic --compare https://paulgraham.com/superlinear.html
/epistemic --pick https://www.youtube.com/watch?v=kYfNvmF0Bqw
```

## Installation

Install directly from the Claude Code CLI:

```bash
claude plugin add askarzh/epistemator
```

Or install manually by cloning and adding the plugin path:

```bash
git clone https://github.com/askarzh/epistemator.git ~/.claude/plugins/epistemator
claude plugin add ~/.claude/plugins/epistemator
```

After installation, restart Claude Code. The slash commands (`/scholastic`, `/cartesian`, `/pirsig`, `/lateral`, `/epistemic`) will be available immediately.

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
