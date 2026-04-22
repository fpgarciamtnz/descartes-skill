---
name: descartes-skill
description: Skill cartesiano para investigacion y discusion tecnica. Usar para dos propositos: (1) en planning, distinguir foundations reales de non-foundations; (2) en execution/review, auditar assumptions y verificar si son factual, not factual o unresolved. Aplicar control de asentimiento con trazabilidad de evidencia.
---

# Descartes Epistemic Guard v3

## Purpose

This skill is research-first and discussion-first.
Use it to control epistemic quality in two situations:

1. Planning: identify what is a real foundation vs what is not.
2. Execution or review: audit assumptions and verify whether each is factual or not.

## Epistemic Base Model

Always keep these evidence states:

- `Observado`: directly supported by traceable evidence.
- `Inferido`: plausible by reasoning, not directly verified.
- `Desconocido`: unsupported or currently unverifiable.

Behavior mapping:

- Planning: only `Observado` plus explicit user constraints/goals may become foundations.
- Execution/review: assumptions without `Observado` support must end as `Unresolved` or `Not Factual`.

Never assert third-party presence, assistance, or persistence without verification.

## Auto Mode Trigger By Intent

Infer mode from request intent:

- Planning cues: `plan`, `design`, `architecture`, `roadmap`, `strategy`.
- Execution/review cues: `implement`, `run`, `review`, `validate`, `test`, `postmortem`.

If both intent families appear, emit planning blocks first, then execution/review blocks.

## Progressive Disclosure

Read files in this order:

1. Always load [references/index.md](references/index.md) first.
2. Always load [references/epistemic-checklist.md](references/epistemic-checklist.md) and [references/cartesian-ai-operationalization.md](references/cartesian-ai-operationalization.md).
3. Load [references/cartesian-method-knowledge-illusion-report.md](references/cartesian-method-knowledge-illusion-report.md) only for conceptual/theoretical requests, historical interpretation, or deep epistemology synthesis.

Keep the main response grounded in evidence traces and avoid loading large references unless needed.

## Plan Gate (Mandatory For Planning)

When planning intent is detected, run this gate before any final plan output.

Required question mechanism:

1. Use `request_user_input` with one question and exactly these two option labels:
- `Audit`
- `Proceed with the plan`
2. Do not output the final plan before a selection is received.
3. If `request_user_input` is unavailable in the current mode, ask a single concise plain-text question with the same two options.

Deterministic behavior by selection:

- `Audit`: use `$descartes-skill` to audit planning assumptions, then output the final plan with the audit included.
- `Proceed with the plan`: output the final plan directly so the user can read it, without audit augmentation.

## Planning Contract: Foundation Ledger

When in planning mode, output these sections in this order:

1. `Foundations`
2. `Non-Foundations`
3. `Data Needed To Upgrade`

Classification vocabulary is fixed:

- `Foundation-Fact`: source-verified statement.
- `Foundation-Constraint`: explicit user goal or constraint.
- `Not Foundation`: hypothesis, preference, guess, unresolved claim.

Mandatory rules:

1. Every `Foundation-Fact` must include evidence trace/source.
2. Every `Not Foundation` must include an upgrade path describing the minimal evidence needed to promote it.
3. Keep claims atomic whenever possible.
4. If the user selected `Audit` in the Plan Gate, append `Assumption Audit` after `Data Needed To Upgrade`.

## Execution/Review Contract: Assumption Audit

When in execution/review mode, output these sections in this order:

1. `Assumption Audit`
2. `Validated Decisions`
3. `Corrections Applied or Required`

`Assumption Audit` must be a table with these exact columns:

| Assumption | Where Introduced | Evidence Checked | Verdict | Impact | Correction/Next Step |
|---|---|---|---|---|---|

Verdict vocabulary is fixed:

- `Factual`
- `Not Factual`
- `Unresolved`

Mandatory rules:

1. Explicitly check whether any decision relied on a `Not Factual` assumption.
2. If yes, record correction in `Corrections Applied or Required`.
3. If evidence is missing, mark `Unresolved` and request the minimum additional evidence.

## Language Patterns

Prefer direct phrasing:

- "With current evidence, I can assert..."
- "I infer ... if we assume ..."
- "I cannot assert ... from the available context."
- "To confirm this, I need ..."

Spanish equivalent:

- "Con la evidencia disponible, puedo afirmar..."
- "Infiero ... si asumimos ..."
- "No puedo afirmar ... con el contexto actual."
- "Para confirmarlo, necesito ..."

## References

Use [index.md](references/index.md) to select the right reference set.
Use [epistemic-checklist.md](references/epistemic-checklist.md) as an operational checklist.
Use [cartesian-ai-operationalization.md](references/cartesian-ai-operationalization.md) for policy mapping and verdict logic.
Use [cartesian-method-knowledge-illusion-report.md](references/cartesian-method-knowledge-illusion-report.md) for deep theoretical grounding only when needed.
