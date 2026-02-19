# Epistemator

Epistemic analysis tools that process ideas, texts, and questions through four philosophical reasoning frameworks. This is a pure-prompt plugin: no application code, no dependencies, no build system. Everything is markdown files with YAML frontmatter interpreted by Claude Code's plugin system.

## Architecture

Three-tier plugin structure:

- **Skills** (`skills/<id>/SKILL.md`) — The knowledge layer. Each skill contains the full methodology of a philosophical framework with two modes: Structured (deterministic markdown output) and Interactive (Socratic guided analysis).
- **Commands** (`commands/<id>.md`) — The interface layer. Thin wrappers that delegate to a skill or agent, passing `$ARGUMENTS` through. Filename minus `.md` becomes the slash command name.
- **Agent** (`agents/epistemic-analyst.md`) — The orchestration layer. Runs multiple frameworks and produces comparative synthesis. Three modes: Suggest (default, auto-recommends), Compare (`--compare`, all four in parallel via Task tool), Pick (`--pick`, user selects via AskUserQuestion).

```
.claude-plugin/plugin.json   # Manifest (name: epistemator, v0.1.0)
skills/
  scholastic/SKILL.md        # Framework methodologies
  cartesian/SKILL.md
  pirsig/SKILL.md
  lateral/SKILL.md
commands/
  scholastic.md              # Slash command wrappers
  cartesian.md
  pirsig.md
  lateral.md
  epistemic.md               # Multi-framework meta-command
agents/
  epistemic-analyst.md       # Orchestrator agent
docs/plans/                  # Design documents
```

## The Four Frameworks

| ID | Framework | Best For |
|----|-----------|----------|
| `scholastic` | Modern Scholasticism (Aquinas) | Arguments, claims — "Is X true?" |
| `cartesian` | Cartesian Reductionism (Descartes) | Complex systems — "What are the parts?" |
| `pirsig` | Metaphysics of Quality (Pirsig) | Value judgments — "What is better?" |
| `lateral` | Lateral Thinking (De Bono) | Stuck thinking — "What else could this be?" |

## Adding a New Framework

1. Create `skills/<id>/SKILL.md` with YAML frontmatter (`name`, `description`, `version`) and full methodology
2. Create `commands/<id>.md` — copy any existing command, change name/description
3. Add a row to the Known Frameworks table in `agents/epistemic-analyst.md`

## Validation

No automated tests. Manual validation via shell:

```bash
# Verify plugin manifest is valid JSON
python3 -c "import json; json.load(open('.claude-plugin/plugin.json')); print('OK')"

# Verify all skills have YAML frontmatter
for f in skills/*/SKILL.md; do head -5 "$f"; echo "---"; done

# Verify all commands have YAML frontmatter
for f in commands/*.md; do head -5 "$f"; echo "---"; done
```

## Key Conventions

- Skills define a `description` field in frontmatter that acts as the natural-language trigger for Claude Code's skill matching
- Commands use `argument-hint` in frontmatter to show usage syntax in `/help`
- The agent specifies `model: sonnet` and an explicit `tools` whitelist
- The comparative synthesis format (Convergence / Divergence / Synthesis / Meta-Observation) is the standard multi-framework output
- Design docs live in `docs/plans/`
