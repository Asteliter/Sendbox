# Task 3+ — Component spec (buttons & core controls)

Extends `voice-prompt.md` with the actual controls Task 4's screen will be built from. Same voice, same constraints — every component below inherits the brief's rules: never state a clause is enforceable/valid/normal, every non-standard or uncertain flag keeps its disclaimer visible (not hidden behind a click), never a verdict icon.

Live, interactive version of everything below: `visuals/assets-preview.html`.

---

## 1. Primary button

**Purpose:** the one main call-to-action per screen — starting a scan, or the equivalent single most-important next step.

| State | Visual | Copy | Notes |
|---|---|---|---|
| Default | solid fill, primary ink | "Upload a document to scan" | |
| Hover | fill lightens ~8% | (same) | pointer cursor |
| Focus-visible | 2px ring, dedicated focus-blue (not the red redesign-accent, to avoid confusing focus with the "flagged" signal) | (same) | ring must be visible on both light and dark |
| Active / pressed | fill darkens ~8% | (same) | |
| Loading | button disabled, spinner replaces leading space, text swaps | "Scanning your document…" | `aria-live="polite"` so screen readers announce the state change; button un-clickable, not just visually dimmed |
| Disabled | 45% opacity, `not-allowed` cursor | "Upload a document to scan" | used before a file is chosen, e.g. for a dependent secondary action |

## 2. Secondary button

**Purpose:** a supporting action that isn't the page's main CTA.

| State | Visual | Copy | Notes |
|---|---|---|---|
| Default | outline only, no fill | "Export summary" | |
| Hover | subtle page-tint background | (same) | |
| Focus-visible | same 2px focus-blue ring as primary | (same) | |
| Disabled | 45% opacity | "Export summary" | disabled until a scan has produced results — never let the user export nothing |

## 3. Ghost / text button

**Purpose:** a low-emphasis, in-context action — used inside a clause card, never as a page's main action.

| State | Visual | Copy | Notes |
|---|---|---|---|
| Default | no border/fill, text only | "Why was this flagged?" | |
| Hover | underline appears | (same) | |
| Expanded | chevron rotates, reveals the reference-comparison detail | "Hide details" | toggles, doesn't navigate away |

## 4. Status badge

**Purpose:** formalizes the four Task 3 icons into one reusable pill component — icon + label, never icon alone (per the brief's colour-blind / black-and-white requirement, the label is load-bearing, not decorative).

Anatomy: 16–18px icon + label text, pill background one step off the surface, 1px hairline border. No background-fill semantics carried by hue — the red ring used earlier only marks *this specific instance* is the redesign target for our own workshop artifact, not a badge convention to reuse in the product itself.

| Badge | Icon | Label |
|---|---|---|
| Worth a second look | `flag-nonstandard.svg` | "Worth a second look" |
| Comparing… | `scanning-inprogress.svg` | "Comparing…" |
| Not sure | `uncertain-review.svg` | "Not sure — ask a professional" |
| Compared against pattern | `compared-pattern.svg` | "Compared against a reference pattern" |

## 5. Clause card (composed component)

**Purpose:** the repeating unit of the Clause Review screen — one per clause the assistant segmented out.

**Anatomy (top to bottom):**
1. Clause excerpt, quoted verbatim from the document (never paraphrased in the quote itself — paraphrase only happens in the explanation below it).
2. Status badge (component 4).
3. Explanation line, in voice-prompt.md's microcopy for that state.
4. If flagged or uncertain: the disclaimer line, **always visible**, never behind the "Why was this flagged?" toggle — hiding it behind a click would contradict the brief's requirement that every non-standard flag carries the disclaimer.
5. Ghost button "Why was this flagged?" → reveals the reference-pattern comparison (component 3 + badge 4), e.g. "Reference pattern: renewal clauses typically require 30–60 days notice; this one requires 90 and auto-renews for a full additional term."

**States:** collapsed (default) / expanded (detail visible) — independent of the four content-states, which apply to *which* card variant is shown (common / flagged / comparing / uncertain).

---

## Verify (self-check)

- No component hides a required disclaimer behind a click — confirmed in the clause card anatomy above.
- Focus states use a dedicated color distinct from the redesign/flag red, so keyboard focus is never mistaken for a content flag.
- Loading and disabled states both have distinct copy and are announced via `aria-live` / are truly non-interactive (not just dimmed), not just visual.
- No component introduces a new icon beyond the four already checked against the no-verdict-symbol rule.
