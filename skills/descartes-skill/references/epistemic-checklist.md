# Epistemic Checklist v2

Use this checklist before finalizing any planning, execution, or review response.

## Planning Checklist (Foundation Ledger)

1. Candidate claims listed
   - Enumerate all candidate foundations before deciding.
2. Evidence state assigned
   - Mark each item as `Observado`, `Inferido`, or `Desconocido`.
3. Foundation classification applied
   - Use only: `Foundation-Fact`, `Foundation-Constraint`, `Not Foundation`.
4. Traceability attached
   - Every `Foundation-Fact` includes evidence trace/source.
5. Constraint integrity checked
   - Every `Foundation-Constraint` maps to explicit user goals/constraints.
6. Upgrade path documented
   - Every `Not Foundation` includes minimal evidence required to upgrade.
7. Required planning sections present
   - `Foundations`, `Non-Foundations`, `Data Needed To Upgrade`.

## Execution/Review Checklist (Assumption Audit)

1. Assumptions enumerated
   - List assumptions that influenced implementation or review.
2. Evidence checked per assumption
   - Capture what evidence was checked and from where.
3. Verdict assigned from fixed vocabulary
   - Use only: `Factual`, `Not Factual`, `Unresolved`.
4. Dependency risk checked
   - Explicitly verify whether any decision relied on `Not Factual` assumptions.
5. Corrections captured
   - Record correction in `Corrections Applied or Required` when needed.
6. Missing evidence handled
   - Mark `Unresolved` and request minimal additional evidence.
7. Required execution/review sections present
   - `Assumption Audit`, `Validated Decisions`, `Corrections Applied or Required`.

## Cartesian Guardrail

Never assert third-party presence, assistance, or persistence without direct verification.
