# Task 3 — Voice & Assets

## Screen & states

**Screen:** the Clause Review screen — appears right after a user uploads a contract and the assistant has segmented it into clauses.

| State (our words) | Meaning |
|---|---|
| **Common clause** *(everyday)* | Matches a known, typical pattern for this clause type — no flag, nothing to double-check. |
| **Worth a second look** *(needs-attention)* | Wording deviates from the common pattern — this is the state the whole product exists for. |
| **Comparing…** *(in-progress)* | The assistant is still segmenting/comparing this clause against the reference library. |
| **Not sure — ask a professional** *(can't-tell-you)* | Couldn't confidently match the clause to a known pattern. Task 1's missing-data rule: an honest "not sure" beats false confidence. |

Two key user actions: **Upload a document** · **Export summary**.

---

## Tone-of-voice prompt (filled in)

```
Role: Legal Clause Explainer's copywriter.
Context: the Clause Review screen, right after the assistant has scanned
  an uploaded contract — the moment just before the user decides whether
  a clause needs a second look.
Style: plain-spoken, neutral, cautious — calm and precise, like a
  knowledgeable friend, never a lawyer rendering a verdict.
Constraints: never state a clause is enforceable, valid, fair, or
  "normal"; every non-standard or uncertain flag ends with an
  informational-only / attorney-review line; never invent clause
  content that isn't in the document.
Scope — one line per state:
  Common clause (everyday):        (standard line, no special copy —
                                     clause shown plainly, no badge)
  Worth a second look (needs-attention): "This clause is worded
    differently from what we usually see here — worth a second look."
  Comparing… (in-progress): "Comparing this clause against common
    patterns…"
  Not sure (can't-tell-you): "We couldn't confidently match this clause
    to a common pattern. Informational only, not legal advice — a
    licensed attorney can tell you more than we can here."
  Upload a document (action 1): "Upload a document to scan"
  Export summary (action 2): "Export summary"
```

---

## Asset generation prompt (filled in)

```
# Role
You are a senior product designer producing production-ready UI assets
for the Legal Clause Explainer. Follow the design context below exactly
— do not invent features, states, or extra assets.

# Context
Product: Legal Clause Explainer — flags non-standard contract clauses
  in plain language for non-lawyers.
User & moment: someone reviewing an AI-scanned contract, deciding
  whether a specific clause needs a second look.
Tone: plain-spoken, neutral, cautious — a knowledgeable friend, never a
  lawyer rendering a verdict.
States & microcopy:
  Worth a second look: "This clause is worded differently from what we
    usually see here — worth a second look."
  Comparing…: "Comparing this clause against common patterns…"
  Not sure: "We couldn't confidently match this clause to a common
    pattern. Informational only, not legal advice — a licensed
    attorney can tell you more than we can here."

# Task
Produce exactly these assets — don't add, merge, or substitute:
  Asset 1: "non-standard flag" — appears on the Worth-a-second-look state
  Asset 2: "uncertain / can't classify" marker — appears on the Not-sure state
  Asset 3: "compared-against-pattern" cue — appears beside any flagged
           clause, showing the flag is grounded in a reference pattern,
           not just the model's opinion
  Asset 4: "scanning / in progress" — appears on the Comparing… state

# Requirements
- SVG, flat, single-weight line, 24×24 viewBox.
- Works in pure black-and-white: shape + label carry the meaning, never
  colour alone. (All four ship colourless — currentColor stroke only,
  no fill dependency — so this is automatic, not just tested for.)
- Must NOT resemble scales-of-justice, a gavel, a checkmark/seal-of-
  approval, or any other symbol implying a legal verdict or
  certification — the product must never look like it's rendering a
  judgment.
- Never imply more certainty, alarm, or judgment than the data supports.

# Output
See `assets/` — 4 SVGs + `assets/README.md` with rationale + alt text
for each, and a rendered preview at `visuals/assets-preview.html`.
```

### Verify (self-check against the Requirements)

- SVG, flat, single-weight line, 24×24 viewBox — all four confirmed (`stroke-width: 1.6`, `viewBox="0 0 24 24"`).
- Black-and-white safe — all four use `stroke="currentColor"` only, no color fill carries meaning; nothing to fail under CVD since no hue is used at all.
- No verdict/certification symbols — swapped an early checkmark draft in Asset 3 for a neutral compare/equals mark between two clause outlines, specifically because a checkmark reads as "approved," which the brief forbids.
- No overclaiming — none of the four icons use exclamation marks, red, or alarm-style shapes; "worth a second look" and "not sure" stay descriptive, not alarmed.
