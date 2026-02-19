# Epistemator

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-0.1.0-green.svg)](.claude-plugin/plugin.json)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-plugin-blueviolet.svg)](https://claude.ai/code)
[![No Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen.svg)](#)

Epistemic analysis tools for [Claude Code](https://claude.ai/code) — process ideas, texts, and questions through philosophical reasoning frameworks.

## Why

You can summarize anything in seconds. So what? A summary tells you what someone said. It doesn't tell you whether it's true, what's missing, why it matters, or what you'd see if you looked at it differently.

We're drowning in content — articles, talks, proposals, strategies — and the default AI response is to compress it. But compression isn't thinking. A summary of a bad argument is still a bad argument. A summary of a complex decision hides the tensions that actually matter.

Epistemator doesn't summarize. It *examines*. Each framework asks a different question that a summary never would: Is this claim actually defensible? What are the hidden assumptions? Where is the real value? What would we see if we stopped thinking about it the usual way?

## Quick Start

```bash
claude plugin add askarzh/epistemator
```

```
/scholastic Is free will compatible with determinism?
/sixhats Should we adopt microservices?
/epistemic --compare https://paulgraham.com/greatwork.html
```

## What It Does

Epistemator is a Claude Code plugin that provides four philosophical analysis frameworks as slash commands. Each framework offers a different lens for examining a topic, and a meta-command lets you combine multiple frameworks for comparative analysis.

## Frameworks

| Command | Framework | Question It Answers |
|---------|-----------|-------------------|
| `/scholastic` | Modern Scholasticism (Aquinas) | "Is X true?" — structured disputation via quaestio disputata |
| `/cartesian` | Cartesian Reductionism (Descartes) | "What are the parts?" — systematic decomposition to first principles |
| `/pirsig` | Metaphysics of Quality (Pirsig) | "What is better?" — analysis through static/dynamic quality patterns |
| `/sixhats` | Six Thinking Hats (De Bono) | "How should we think about this?" — structured parallel thinking from six perspectives |
| `/epistemic` | Multi-framework orchestrator | Suggests, compares, or lets you pick frameworks |

## Usage

### Slash Commands

Each framework has a slash command. Pass your topic or question as the argument:

```
/scholastic Is free will compatible with determinism?
/cartesian Why is our deployment pipeline so slow?
/pirsig Should we prioritize code elegance or shipping speed?
/sixhats Should we adopt a microservices architecture?
```

### Natural Language

Frameworks also trigger automatically when Claude detects a matching intent:

```
Analyze the argument that AI will replace all programming jobs
Break down our authentication system into its component parts
Assess the quality tradeoff between test coverage and development speed
Put on the six hats and evaluate our hiring process
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
/sixhats https://www.youtube.com/watch?v=UF8uR6Z6KLc
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

After installation, restart Claude Code. The slash commands (`/scholastic`, `/cartesian`, `/pirsig`, `/sixhats`, `/epistemic`) will be available immediately.

## Project Structure

```
.claude-plugin/plugin.json    # Plugin manifest
skills/
  scholastic/SKILL.md         # Framework methodology + prompts
  cartesian/SKILL.md
  pirsig/SKILL.md
  sixhats/SKILL.md
  epistemic/SKILL.md
commands/
  scholastic.md               # Slash command wrappers
  cartesian.md
  pirsig.md
  sixhats.md
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
