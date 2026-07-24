# Brand style — colors & typography

Personality target from the quiz: **calm confidence** — assured without being loud, so it doesn't fight the brief's voice ("a knowledgeable friend, never a lawyer rendering a verdict"). Confidence comes from restraint and consistency, not saturation.

Accessibility target: **WCAG AA, light + dark**, both selected (not an auto dark-mode filter — its own stepped values, per the same method used in `visuals/journey-map.html`). Every pairing below is computed, not eyeballed — ratios shown are the actual WCAG relative-luminance formula, run through a small script, not estimated.

---

## 1. Brand color — blue

Blue tested best against "explaining unfamiliar contract clauses to non-lawyers": reads as trustworthy and calm rather than alarming (red), overly reassuring (green — risks contradicting a product whose whole job is sometimes to say "double-check this"), or cold/corporate (navy-only). Drawn from the same validated sequential ramp already used for the journey-map chart and the focus ring, so nothing new is being introduced — just formalized into brand roles.

| Role | Light | Dark | Used for |
|---|---|---|---|
| **Brand fill** (solid buttons, filled badges) | `#256abf` | `#256abf` *(same value both modes — see rationale below)* | Primary button background |
| **Brand ink** (text, links, icons, focus ring) | `#2a78d6` | `#3987e5` | Links, focus ring, icon accents |
| **Brand fill hover** | `#1c5cab` | `#1c5cab` | Primary button hover |
| **Brand fill active/press** | `#184f95` | `#184f95` | Primary button pressed |
| **Brand subtle background** | `#cde2fb` | `rgba(57,135,229,0.16)` | Info banners, selected rows |

**Why the fill color stays constant across modes, while the ink color shifts:** a button needs white text on top of its fill at ≥4.5:1 (WCAG 1.4.3, normal text — button labels at 13px/600 weight don't clear the "large text" bold exception, so the stricter threshold applies). `#256abf` is the lightest step on the ramp that clears 4.5:1 with white text in **both** light and dark contexts, so one value works everywhere. Ink-role blue (used as text/icon on the surface, never as a fill) instead needs to contrast against the *page*, which is a lighter surface in light mode and a near-black one in dark mode — so it uses the mode-appropriate lighter step instead.

### Contrast, computed

| Pair | Ratio | Passes |
|---|---|---|
| White text on brand fill `#256abf` | 5.39:1 | AA normal text ✓ |
| Brand fill `#256abf` vs. dark surface `#1a1a19` (button edge visibility) | 3.23:1 | AA non-text (1.4.11, needs 3:1) ✓ |
| Brand ink `#2a78d6` vs. light surface `#fcfcfb` | 4.30:1 | AA normal text ✓ |
| Brand ink `#3987e5` vs. dark surface `#1a1a19` | 4.79:1 | AA normal text ✓ |

**Rejected:** using the lighter step (`#2a78d6`/`#3987e5`) as the button fill directly, because white-on-`#3987e5` only reaches 3.64:1 — fails normal-text AA. This is exactly the kind of near-miss that's invisible without computing it, which is why it's called out here rather than left as "looks fine."

---

## 2. Ink & surface (unchanged, re-confirmed)

| Role | Light | Dark | Contrast vs. own surface |
|---|---|---|---|
| Primary ink | `#0b0b0b` | `#ffffff` | 19.17:1 / 17.42:1 |
| Secondary ink (body copy, disclaimers, anything the user must read) | `#52514e` | `#c3c2b7` | 7.73:1 |
| Muted ink (decorative only — dashed strokes, chart axis ticks; **never** load-bearing text) | `#898781` | `#898781` | 3.50:1 — below AA, which is exactly why its use is restricted |

**Fix applied this pass:** the clause card's disclaimer line ("Informational only, not legal advice…") was styled in muted ink at 3.50:1 — a real AA failure on text that is functionally important, not decorative. Moved to secondary ink (7.73:1). This is the kind of thing "looks like a caption, so it's probably fine to mute" quietly breaks — the disclaimer is arguably the single most legally load-bearing line in the whole product, so it gets the higher-contrast tier, full stop.

---

## 3. Status palette (unchanged — from the asset/badge work, re-stated for completeness)

Good `#0ca30c` · Warning `#fab219` · Serious `#ec835a` · Critical `#d03b3b` (dark: `#e66767`). Kept visually distinct from brand blue on purpose — a status color must never double as a brand/series color (so "flagged" never reads as "on-brand-emphasis" and vice versa).

---

## 4. Typography

**One grotesk family, weight does the contrast work — not a font pairing.** Chosen: **Inter** (Google Fonts, OFL-licensed, free for commercial use). Reasoning: near-universal language/glyph coverage, hinted for small UI sizes (this product is read at 12–14px a lot — clause excerpts, badges, disclaimers), a full 100–900 weight range so headline-vs-body contrast doesn't need a second family, and it already approximates the `system-ui` stack we prototyped with — so nothing shifts underneath the work already shipped, it just gets loaded explicitly instead of falling back to whatever OS font resolves.

Google Fonts embed:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```
```css
font-family: 'Inter', system-ui, -apple-system, "Segoe UI", sans-serif;
```
(`system-ui` etc. kept as fallback, not removed — same stack as before, Inter just loads on top of it.)

### Type scale

| Token | Size | Weight | Used for |
|---|---|---|---|
| Display / H1 | 22–26px | 700 | Screen title |
| H2 | 15–16px | 650 | Section labels (already uppercase + letter-spaced in the prototype) |
| Body | 13–14px | 400–500 | Explanations, clause excerpts |
| Body — emphasis | 13–14px | 600 | Button labels, badge labels |
| Caption / meta | 11–11.5px | 500–600 | Alt text, footnotes — **not** used for anything load-bearing (see the muted-ink rule above) |

### Alternate, if more visual character is wanted later
**Manrope** (also Google Fonts, OFL) — same one-family/weight-contrast approach, slightly more geometric/confident letterforms at the heavier weights, still calm at regular. Swap-in only; doesn't change any of the above roles or ratios.

---

## Applied to the prototype

`visuals/assets-preview.html` updated: Inter loaded, primary button now uses brand-fill blue (was plain ink-colored), disclaimer text moved off muted ink onto secondary ink, focus ring re-confirmed to use brand-ink (distinguishable from the fill via the white surface-gap, not via a second hue).
