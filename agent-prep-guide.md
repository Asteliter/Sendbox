# Agent Prep Guide — Legal: Summarizing Contract Clauses for Non-Lawyers

## 1. Suggested pipeline (multi-step agent, not a single call)

A single "read this contract and summarize risks" prompt tends to either over-hedge everything or confidently assert legal conclusions — both violate the brief's guardrails. A staged pipeline holds up better under demo scrutiny:

1. **Segmenter** — splits the raw document into clauses/sections (by heading, numbering, or paragraph boundary). Output: list of `{section_title, text}`.
2. **Classifier + Retriever** — for each clause, tags its category (renewal, liability, termination, payment, dispute resolution, confidentiality, etc.) and retrieves the matching entry from a reference clause library (see `reference-clause-patterns.md`) to compare against typical phrasing.
3. **Explainer** — for clauses that deviate from the typical pattern, writes a plain-language flag: what the clause says, why it's unusual, what a reader should specifically double check. Never states whether the clause is enforceable, favorable, or "normal" — only that it's non-standard and worth a second look.
4. **Guardrail reviewer** — a final pass (can be a second LLM call with a strict checklist, or even a regex/keyword scan) that rejects or rewrites any output containing words like "enforceable," "valid," "you're protected," "this is fine," etc. This is the step most demos skip and it's exactly what the brief's Data & Privacy section is testing for.

Wire steps 1-3 as tool calls or sub-agents in DIAL; step 4 can run as an assistant-level system instruction or a lightweight validator function.

## 2. Draft system prompt (starting point — tune during the workshop)

```
You are a contract-clause assistant. You help non-lawyers understand what a
contract says in plain language. You are NOT a lawyer and you never provide
legal advice or a legal conclusion.

For each clause you are given:
1. Restate what it says in one or two plain-language sentences.
2. Compare it to typical/common versions of this type of clause (using the
   provided reference patterns). If it deviates meaningfully, mark it
   "non-standard."
3. If non-standard, explain concretely what to double check (a deadline, a
   dollar amount, a scope of responsibility) — not whether it's legal.

Hard rules:
- Never say a clause is "enforceable," "unenforceable," "valid," "fair,"
  "normal," "standard," "risky," or "safe" as a conclusion. Only describe
  what it says and how it compares to common patterns.
- Every "non-standard" flag ends with: "This is informational only, not
  legal advice — consider having a licensed attorney review this clause."
- If you are not confident about a classification, say so rather than
  guessing.
- Do not retain, log, or reuse the contents of this document beyond this
  session.
```

## 3. Building it on DIAL

- DIAL exposes an OpenAI-compatible chat completions API, so the Segmenter/Classifier/Explainer steps can just be separate calls (or a single assistant with tool-calling) against whatever model is configured in your DIAL deployment.
- If a RAG/embeddings addon is available in your DIAL setup, load `reference-clause-patterns.md` as the retrieval corpus so the Classifier step grounds its "typical vs. flagged" judgment in retrieved text rather than the model's own unguided opinion — this is also easier to defend live if a judge asks "how do you know that's non-standard."
- Keep the guardrail reviewer as a separate, cheap call (small model is fine) — its only job is pattern-matching for words the brief forbids, so it doesn't need much reasoning power.

## 4. Test fixtures

- `studio-lease-sample.txt` — matches the workshop's user story almost exactly (auto-renewal with 90-day notice, "regardless of cause" liability) plus a few additional clauses not mentioned in the user story (early termination fee = 3 months' rent, mandatory arbitration + jury waiver) so the demo can show the agent catching things the user in the story hadn't even noticed yet — that's a stronger "aha" moment than only reproducing what's already in the prompt.
- Recommend adding one more fixture from a different document type (a vendor agreement or employment offer) before the workshop, since the brief explicitly lists all three — a lease-only demo may prompt "does this generalize?" from judges.

## 5. Quick self-check before presenting

- Does the output ever state a clause is enforceable/unenforceable, fair, or normal? (Should never happen.)
- Does every flagged clause carry the "informational only" disclaimer?
- Does the demo explain, in one sentence, how documents are handled after the session (not retained / not used for training) — this is called out explicitly in the brief and is an easy point to lose if skipped.
- Does the flow work on at least one document the agent hasn't seen tuned specifically for it?
