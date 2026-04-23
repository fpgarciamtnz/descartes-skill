# Descartes Skill

`descartes-skill` adds a planning foundation ledger workflow to agent planning tasks. Use it when you want an agent to separate verified facts, explicit constraints, unresolved assumptions, and the evidence needed before it presents a final plan.

The skill stays narrow on purpose. It is for planning, architecture, and strategy work where evidence quality matters, not for general implementation or review tasks unless you explicitly want the ledger first.

## Install

Install the skill with the `skills` CLI:

```bash
npx skills add fpgarciamtnz/descartes-skill --skill descartes-skill
```

If you want to install it globally or target a specific agent, add the usual `skills` CLI flags. For example:

```bash
npx skills add fpgarciamtnz/descartes-skill --skill descartes-skill -g --agent <agent-name>
```

Restart your agent after installing or updating the skill so it reloads the metadata.

## Use

Ask for the skill directly:

```text
Use $descartes-skill to create a planning foundation ledger before planning the migration.
```

Or describe the behavior you want:

```text
Plan a rollout for the payment refactor, but build a planning foundation ledger first.
```

```text
Before the final plan, audit the assumptions in the planning foundation ledger for this architecture decision.
```
