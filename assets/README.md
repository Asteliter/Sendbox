# Asset kit — Clause Review screen

Four assets, one per non-everyday state. The everyday ("Common clause") state deliberately gets **no** icon — per the journey map, confirming "this looks normal" shouldn't be over-signaled with its own badge; quiet is the correct treatment there.

## 1. `flag-nonstandard.svg` — Worth a second look

**Rationale:** A pennant/report-flag shape is a common, non-legal-specific "marked for attention" pattern — it reads as "flagged," not as a verdict.
**Alt text:** "Flag: worth a second look"

## 2. `uncertain-review.svg` — Not sure

**Rationale:** A dashed (not solid) circle around a question mark signals "incomplete/unconfirmed" through the stroke style itself, doubling down on the honest-uncertainty message before the label is even read.
**Alt text:** "Uncertain: not sure, ask a professional"

## 3. `compared-pattern.svg` — Compared against a reference pattern

**Rationale:** Two document outlines — one solid (the clause in hand), one dashed (the reference pattern) — with a small compare mark between them. Early drafts used a checkmark here; swapped it out because a checkmark reads as "approved," which the brief explicitly forbids. This version shows *a comparison happened*, not that the clause passed one.
**Alt text:** "Compared against a reference pattern, not just the model's opinion"

## 4. `scanning-inprogress.svg` — Comparing…

**Rationale:** A document with a sweeping dashed line reads as active scanning/checking without needing animation — works as a static state too (e.g., in a screenshot or a reduced-motion context).
**Alt text:** "Comparing this clause against common patterns"

---

All four: SVG, single-weight line (`stroke-width: 1.6`), 24×24 viewBox, `stroke="currentColor"` with no fill dependency — so they work in pure black-and-white and inherit whatever text color surrounds them, with no CVD risk since no hue is used at all. See `../visuals/assets-preview.html` for a rendered preview alongside the microcopy from `voice-prompt.md`.
