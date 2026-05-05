---
name: descartes-skill
description: "Build planning foundation ledgers that separate verified facts, explicit constraints, unresolved assumptions, and upgrade evidence. Use for planning, architecture, strategy, roadmap, or design requests where Codex must show evidence before a final plan."
---

# Descartes Planning Foundation Ledger

## Single Responsibility

Use this skill to make planning safer by building a planning foundation ledger before presenting a final plan.

Do not use this skill as a general execution, code review, test, postmortem, research, or philosophy skill. Use it for those areas only when the user explicitly asks for a planning foundation ledger before a plan.

## Trigger Guidance

Use this skill when the user asks to:

- Plan, design, architect, sequence, or choose a strategy.
- Separate foundations, facts, constraints, assumptions, or unknowns for a plan.
- Audit planning assumptions before a final plan.
- Invoke `$descartes-skill` directly.

Do not use this skill when the user asks only to:

- Implement, edit, run, test, debug, or review code without a planning request.
- Summarize Descartes or discuss philosophy without applying it to planning.
- Produce a quick answer where a planning foundation ledger would add friction and was not requested.

## Core Vocabulary

Evidence states:

- `Observado`: directly supported by traceable evidence in the prompt, files, tools, or user statements.
- `Inferido`: plausible from reasoning, but not directly verified.
- `Desconocido`: unsupported, missing, or currently unverifiable.

Planning classifications:

- `Foundation-Fact`: an `Observado` statement with an evidence trace.
- `Foundation-Constraint`: an explicit user goal, boundary, preference, or instruction.
- `Not Foundation`: a hypothesis, guess, preference not stated by the user, unresolved claim, or inferred claim.

Audit verdicts:

- `Factual`: supported by `Observado` evidence.
- `Not Factual`: contradicted by checked evidence.
- `Unresolved`: not sufficiently supported or contradicted.

## Required Workflow

1. Gather available evidence before asking questions when repository or system context can answer them.
2. Atomize candidate claims into short, testable statements.
3. Classify each claim with the fixed vocabulary.
4. Keep `Foundation-Fact` and `Foundation-Constraint` separate.
5. Put every unsupported or inferred claim in `Non-Foundations`.
6. For every `Not Foundation`, state the minimum evidence needed to upgrade it.
7. Before final plan output, use one structured planning gate question through the host's structured choice UI.
8. Treat plain-text rendering of the planning gate as a degraded fallback state that should be called out explicitly, not as a normal equivalent of the structured UI.

## Planning Gate

Before presenting a final plan, ask one structured choice question with exactly these option labels:

- `Audit this plan`
- `Do not review the plan`

Behavior:

- `Audit this plan`: run an assumption-audit pass, then include `Assumption Audit` before the final plan.
- `Do not review the plan`: skip the assumption-audit pass and continue with the normal planning response for that turn.

Host requirement:

- Render this gate through the same structured question UI used for normal Codex clarification prompts.
- Do not silently downgrade the gate into a plain-text option list during long threads, context compaction, or prompt merging.
- If the host truly cannot render the structured question UI, explicitly state that the gate degraded to plain text and treat that as a fallback bug, not as intended UX.

## Output Format

When this skill is active, produce a planning foundation ledger with these sections in this order unless the user asks for a shorter form:

1. `Foundations`
2. `Non-Foundations`
3. `Data Needed To Upgrade`
4. `Assumption Audit` only when requested by `Audit this plan` or by an explicit planning-assumption audit request
5. `Final Plan`

Use this table for `Foundations`:

| Claim | Class | Evidence |
|---|---|---|

Rules:

- `Class` must be `Foundation-Fact` or `Foundation-Constraint`.
- `Foundation-Fact` evidence must identify the prompt, file, command output, source, or tool result.
- `Foundation-Constraint` evidence must point to the user's explicit instruction.

Use this table for `Non-Foundations`:

| Claim | Evidence State | Why Not Foundation | Upgrade Path |
|---|---|---|---|

Rules:

- `Evidence State` must be `Inferido` or `Desconocido`.
- `Upgrade Path` must name the smallest practical check, source, or user answer needed.

Use this table for `Assumption Audit`:

| Assumption | Evidence Checked | Verdict | Risk | Plan Impact | Next Step |
|---|---|---|---|---|---|

Rules:

- `Verdict` must be `Factual`, `Not Factual`, or `Unresolved`.
- If any plan decision depends on `Not Factual`, revise the plan before presenting it.
- If any plan decision depends on `Unresolved`, either mark it as an assumption or ask for the missing evidence.

## Reference Loading

Load references only when they help the current request:

- Read [references/index.md](references/index.md) when unsure which reference supports the current planning foundation ledger.
- Read [references/epistemic-checklist.md](references/epistemic-checklist.md) for the operational checklist.
- Read [references/cartesian-ai-operationalization.md](references/cartesian-ai-operationalization.md) when the planning request needs more detail on evidence states or assent control.
- Read [references/cartesian-method-knowledge-illusion-report.md](references/cartesian-method-knowledge-illusion-report.md) only when the user asks for the Descartes theory behind the workflow.

## Language Pattern

Prefer direct phrasing:

- "With current evidence, I can assert..."
- "I infer ... if we assume ..."
- "I cannot assert ... from the available context."
- "To confirm this, I need ..."

Spanish equivalents are acceptable when the conversation is in Spanish:

- "Con la evidencia disponible, puedo afirmar..."
- "Infiero ... si asumimos ..."
- "No puedo afirmar ... con el contexto actual."
- "Para confirmarlo, necesito ..."
