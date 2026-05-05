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

## Planning Gate UX

The skill's planning gate should render as a structured Codex question, using the same arrow-style choice UI as normal clarification prompts. The default gate options are:

- `Audit this plan`
- `Do not review the plan`

Expected behavior:

- `Audit this plan`: run the Descartes assumption-audit pass and include the `Assumption Audit` section before the final plan.
- `Do not review the plan`: skip the audit pass and continue with the normal planning response for that turn.

The gate should not silently fall back to a plain-text option list during long conversations, context compaction, or prompt merging. If the host cannot render the structured question UI, that should be surfaced as an explicit degraded fallback, not treated as intended UX.

Example prompt:

```text
Plan a rollout for the payment refactor, then ask whether to audit the plan before finalizing it.
```

Expected result:

- If the user selects `Audit this plan`, the response includes `Assumption Audit` and then the final plan.
- If the user selects `Do not review the plan`, the response skips `Assumption Audit` and returns the final plan directly.

## Validation Notes

- `quick_validate` should still report `Skill is valid!`
- A mock planning prompt should show the new gate labels.
- Plain-text rendering of the gate is a degraded fallback, not the intended UX to validate against.
