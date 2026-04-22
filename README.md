# Descartes Skill

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo fpgarciamtnz/descartes-skill --path skills/descartes-skill
```

Restart Codex after installing the skill.

## What Is This?

Descartes Skill is a Codex skill for clearer AI planning and review.

It helps an AI assistant separate what is actually known from what is only assumed. In planning, it creates a foundation ledger so decisions are grounded in evidence. In review or execution, it audits assumptions and marks them as factual, not factual, or unresolved.

## How It Helps With AI

AI can sound confident even when a claim is only a guess. This skill adds a simple discipline:

- Treat verified facts differently from assumptions.
- Make uncertainty visible.
- Ask for the minimum evidence needed to upgrade a weak claim.
- Audit decisions before they become final.

Use it when you want more careful plans, technical reviews, research discussions, or postmortems.

## What Is Included

- `skills/descartes-skill/SKILL.md`: the main skill instructions.
- `skills/descartes-skill/agents/openai.yaml`: Codex UI metadata.
- `skills/descartes-skill/references/`: supporting reference material for planning and assumption audits.

## Install

Run the command at the top of this README, then restart Codex so the new skill is loaded.
