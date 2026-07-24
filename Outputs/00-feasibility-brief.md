# 00 — Feasibility Brief

## Legal: Summarizing Contract Clauses for Non-Lawyers

| | |
|---|---|
| **User's problem** | Signs a contract (lease, vendor agreement, employment offer) with no lawyer of their own. Skims for the obvious stuff (rent, dates) but gets stuck on dense clauses like "Renewal" or "Liability" — reads them three times, still can't tell if they're normal or a trap, googles a phrase and only finds generic law-firm blog posts that don't speak to *their* document. Signs anyway and hopes it never becomes a problem. |
| **Business goal + metric** | Fewer "can you explain this clause?" escalations to human reviewers — put a number on it: **-40% in 6 months**, measured as escalation volume per document reviewed. |
| **Does the user see AI output?** | **Yes** — this is the core of the product, unlike a lookup-only assistant. The user reads the AI's plain-language flag directly on screen for each non-standard clause. Because of that, output must be tightly constrained: structured template (quote → category → what to double-check), never freeform legal opinion. |
| **Data & privacy** | Documents may contain PII, business financials, and negotiated terms considered confidential. No retention beyond the session unless the user explicitly opts in; clause content is never used for model training. Must respect attorney-client privilege boundaries where applicable. |
| **If a clause can't be confidently classified** | Don't force a verdict — say "couldn't confidently categorize this clause — recommend review by a licensed attorney" rather than guessing or staying silent. An honest "not sure" beats false confidence, same principle as the reference case's "couldn't confirm" merchant. |
| **Voice / brand** | Plain-spoken, neutral, cautious. Reads like a knowledgeable friend pointing at what to double-check — never like a lawyer rendering a verdict. Every non-standard flag ends with: "informational only, not legal advice — consider having this reviewed by a licensed attorney." Never states a clause is enforceable, valid, fair, or "normal." |
| **Approved tools** | CodeMie / Claude / DIAL / Figma Make. |

### AI in the product
**Yes** — the AI reads the contract, segments it into clauses, compares each against a reference library of typical/flagged patterns, and generates the plain-language explanation the user reads directly. Nothing about the *comparison logic* is invented per-session — it's grounded against a fixed reference library (see `materials/reference-clause-patterns.md`) so flags are explainable, not just the model's unguided opinion.

### AI in your work
**Yes** — approved tools (Claude / DIAL / Figma Make) speed up building the screen and the agent pipeline, but only against de-identified/synthetic contract data (see `materials/studio-lease-sample.txt`) during design and testing — never real user documents.

---

## Regulatory / ethical class

Not a legal determination — a working assumption for design scope, to confirm with compliance before ship (same "flag, don't verdict" principle as the product itself).

| Framework / concern | Applies? | Note |
|---|:---:|---|
| **EU AI Act** | Likely limited-risk | Informational aid only — no legal conclusion or adjudication generated, doesn't sit in an "administration of justice" role. Still triggers a transparency obligation: user must be told content is AI-generated. |
| **GDPR / data privacy** | Yes | Contract text can carry PII (names, addresses, financial terms) — no retention beyond session without opt-in, no training use (already in Data & privacy above). |
| **Unauthorized practice of law (UPL) statutes** | Yes — varies by jurisdiction | Output must never render an enforceability/legal verdict; framed strictly as descriptive/comparative against a reference library, never advisory. |
| **Consumer / unfair-contract-terms law** | Possibly relevant | Could inform what counts as "unusual" per region. v1 assumes a single reference jurisdiction (see Out of scope). |

## Worst-case failure scenario

The agent either invents a legal-sounding conclusion ("this clause is enforceable") or stays silent on a genuinely predatory clause because it wasn't in the reference library — the user reads that silence as reassurance, signs, and the clause is later enforced against them. They say "the tool told me it was fine," even though it never should have implied that. Result: real harm to the user, reputational exposure, and a plausible unauthorized-practice-of-law complaint.

## Out of scope for v1

- No OCR / scanned-PDF support — assumes machine-readable text input
- Single reference jurisdiction only — no jurisdiction picker
- English-language contracts only
- Flagging only, no negotiation/redline suggestions
- No multi-document comparison
