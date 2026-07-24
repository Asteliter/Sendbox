# Sendbox — AI Jam Design Workshop 2.0

Legal: Summarizing Contract Clauses for Non-Lawyers

## Structure

- `agent-prep-guide.md` — proposed pipeline (Segmenter → Classifier/Retriever → Explainer → Guardrail reviewer), draft system prompt, and notes on building this on DIAL.
- `materials/reference-clause-patterns.md` — short reference library of common clause categories (renewal, liability, termination, arbitration, payment, non-compete) with typical vs. flagged patterns, for grounding the agent's comparisons.
- `materials/studio-lease-sample.txt` — synthetic test contract based on the workshop's user story, with a couple of extra flagged clauses (early termination fee, mandatory arbitration) beyond what the user story already mentions, for a stronger demo.

## Constraints from the brief

- Informational only — never state a clause is enforceable, valid, fair, or "normal."
- Every non-standard flag ends with a disclaimer recommending review by a licensed attorney.
- No retention of uploaded documents beyond the session; no use of clause content for model training.
