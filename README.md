# Descartes Skill

A Codex skill for planning foundation ledgers.

`descartes-skill` helps Codex build a planning foundation ledger before it presents a final plan. A planning foundation ledger separates verified facts, explicit user constraints, unresolved assumptions, and the evidence needed to upgrade weak claims.

This repo intentionally keeps the skill narrow. It is not a general implementation, code review, research, or philosophy skill unless the user explicitly asks for a planning foundation ledger.

## Included Files

- `skills/descartes-skill/SKILL.md`: main skill instructions and trigger behavior.
- `skills/descartes-skill/agents/openai.yaml`: optional Codex UI metadata.
- `skills/descartes-skill/references/`: concise reference material loaded only when useful.

## Install

Recommended install with the Codex skill installer, if available:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo fpgarciamtnz/descartes-skill --path skills/descartes-skill
```

On Windows PowerShell, a manual local install is also possible:

```powershell
$dest = "$env:USERPROFILE\.codex\skills\descartes-skill"
New-Item -ItemType Directory -Force $dest | Out-Null
Copy-Item -Recurse -Force .\skills\descartes-skill\* $dest
```

Restart Codex after installing or updating the skill so the metadata is reloaded.

## Usage

Good prompts:

```text
Use $descartes-skill to create a planning foundation ledger before planning the migration.
```

```text
Plan a rollout for the payment refactor, but build a planning foundation ledger first.
```

```text
Before the final plan, audit the assumptions in the planning foundation ledger for this architecture decision.
```

## Behavior Contract

- The skill produces a planning foundation ledger with `Foundations`, `Non-Foundations`, and `Data Needed To Upgrade`.
- `Foundation-Fact` entries include evidence traces.
- Explicit user goals or constraints can become `Foundation-Constraint`.
- Unsupported or inferred claims stay in `Non-Foundations` until evidence is supplied.
- The optional `Assumption Audit` is a planning-gate step, not a standalone code review or execution workflow.
- Before final plan output, Codex asks the configured planning gate question when the environment supports it.

## Evaluation Plan

Use these prompts after installation to check whether the skill triggers correctly.

| Case | Prompt | Should trigger? | Expected behavior |
|---|---|---:|---|
| Positive 1 | `Use $descartes-skill to plan a migration from JSON files to SQLite.` | Yes | Outputs the planning foundation ledger sections and marks repo facts separately from assumptions. |
| Positive 2 | `Create a planning foundation ledger before designing the new billing architecture.` | Yes | Uses `Foundation-Fact`, `Foundation-Constraint`, and `Not Foundation` classifications. |
| Positive 3 | `Before the final plan, audit assumptions in the planning foundation ledger for this rollout strategy.` | Yes | Runs the planning gate and includes an assumption audit if audit is selected. |
| Negative 1 | `Fix the typo in README.md.` | No | Proceeds with normal implementation behavior; no planning foundation ledger unless explicitly requested. |
| Negative 2 | `Summarize Descartes' Meditations in three bullets.` | No | Gives a normal summary; does not force planning foundation ledger sections. |

## Smoke Test Commands

Run from any workspace after installing the skill:

```bash
codex exec --json 'Use $descartes-skill to plan a migration from JSON files to SQLite. Show the planning foundation ledger before the final plan.'
```

Expected result: JSON output includes assistant text with `Foundations`, `Non-Foundations`, and `Data Needed To Upgrade`.

```bash
codex exec --json 'Create a planning foundation ledger before designing a safer billing architecture rollout.'
```

Expected result: JSON output uses the fixed classification vocabulary and does not treat guesses as facts.

```bash
codex exec --json 'Before the final plan, audit assumptions in the planning foundation ledger for a payment API refactor.'
```

Expected result: Codex runs or simulates the planning gate, then includes an assumption audit when audit is selected.

```bash
codex exec --json 'Fix the typo in README.md.'
```

Expected result: No Descartes planning foundation ledger appears unless the user explicitly asks for one.

```bash
codex exec --json 'Summarize Don Quixote in three bullets.'
```

Expected result: No Descartes planning foundation ledger appears.

## Validation

This repo includes a local PowerShell validator one directory above the repo in the current workspace. If available, run:

```powershell
..\quick_validate.cmd .\skills\descartes-skill
```

Expected result:

```text
Skill is valid!
```

This validator is useful for local checks, but it is not a substitute for real trigger smoke tests.
