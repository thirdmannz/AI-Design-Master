# Brand DNA Extraction & Style Matching

> Mode 5 reference. Defines how to turn brand assets (logo / screenshot / hex / vibe) into a structured Brand DNA profile, then score it against the 17 styles to recommend Top 3 matches.

This file is the lookup table Mode 5 uses. The skill.md flow describes *when* to do each step; this file describes *what* the answer looks like.

---

## 1. Brand DNA schema

Mode 5 B2 produces this exact object. Keep field names stable — Mode 5 B3 scoring reads these keys.

```yaml
brand_dna:
  palette:
    - hex: "#0A2540"
      role: ink            # bg | ink | accent | support
      source: logo         # logo | screenshot | user-provided-hex | guidelines-pdf
    - hex: "#635BFF"
      role: accent
      source: logo
    # ... up to 8 entries

  typography_lean: sans     # serif | sans | display | mono | mixed
  weight_preference: heavy  # light | normal | heavy
  density: airy             # airy | balanced | packed
  formality: corporate      # editorial | corporate | playful | brutalist | luxury
  motion_vibe: subtle-ease  # still | subtle-ease | kinetic | not-specified

  derived_at: 2026-05-13
  source_inputs:
    - type: logo
      note: "vector SVG, 2 colors"
    - type: hex
      note: "user provided #635BFF, #0A2540"
```

### Field rules

| Field | Allowed values | How to infer |
|---|---|---|
| `palette[].role` | `bg`, `ink`, `accent`, `support` | Largest area in logo / lightest = `bg` candidate. Darkest / most-used for type = `ink`. Highest-saturation, smallest area = `accent`. Mid-range = `support`. |
| `typography_lean` | `serif`, `sans`, `display`, `mono`, `mixed` | Look at the logo wordmark if any. No wordmark → check brand guidelines or ask user. |
| `weight_preference` | `light` (300–400), `normal` (500–600), `heavy` (700–900) | Logo stroke weight is the proxy. Thin lines → light. Thick filled forms → heavy. |
| `density` | `airy` (>40% whitespace in screenshot), `balanced`, `packed` | Only fillable from a screenshot. From logo alone → leave `not-specified` and ask user. |
| `formality` | `editorial`, `corporate`, `playful`, `brutalist`, `luxury` | Inferred from palette saturation + typography lean + user-provided vibe description. Low saturation + serif + airy → `editorial`. Bright + sans + heavy → `playful`. Black + sans + packed → `brutalist`. |
| `motion_vibe` | `still`, `subtle-ease`, `kinetic`, `not-specified` | Only fillable if user provides screenshot of existing animated site. Default to `not-specified`. |

---

## 2. Vision vs no-vision input paths

| Input | Vision-capable agent (Claude Code) | Vision-unavailable (Codex / text-only) |
|---|---|---|
| Logo image attached | Read directly; extract 5–8 dominant colors via visual inspection; describe typography character | Ask user to paste hex codes + describe the logo (serif/sans, stroke weight, all-caps?) |
| Screenshot of brand assets | Same as above + extract density signal | Same fallback |
| Hex codes only (no image) | Treat as primary palette input; ask about typography + density separately | Same |
| Vibe description ("Apple but for accountants") | Map keywords to `formality` + `weight_preference` | Same |
| Brand guidelines PDF | Try `anthropic-skills:pdf` if available; extract palette + type specs | Ask user to paste the relevant pages as text |

**Minimum viable Brand DNA**: at least one palette entry + one of `{typography_lean, formality, vibe_description}`. If less than this, do not proceed to B3 — ask follow-up questions instead.

---

## 3. Signal matrix — score each of the 17 styles against the Brand DNA

Each style gets a 0–10 score. Top 3 are presented to the user. Scoring is the sum of four sub-scores:

### 3a. Palette compatibility (0–3)

Does the brand's `accent` fit the style's typical `--color-accent` range?

| Style | Accent range | +3 if brand accent is | +2 if | +0 if |
|---|---|---|---|---|
| Swiss Editorial | single high-saturation accent (red / orange / electric blue) | saturated single hue | muted single hue | desaturated palette (no accent) |
| Magazine Longform | warm earth / oxblood / mustard | warm muted | any earth | electric / neon |
| Fashion / Luxury | monochrome + 1 muted neutral | desaturated single | warm muted | bright / playful |
| Brutalist | black + 1 raw accent (yellow / red / cyan) | pure primary | high-saturation single | gradient / muted-only |
| Type-First Mono | monochrome + 1 accent (any) | single accent + grayscale | 2 colors | 4+ colors |
| Corporate Clean | blue / teal / muted brand color | corporate blue family | any muted | neon / brutal accent |
| Editorial Maximal | 2–3 color editorial palette | 2–3 hues | single hue | 5+ colors |
| Minimal Float | 1 muted accent + neutrals | desaturated single | any muted | bright / saturated |
| Dark Luxury | gold / champagne accent on near-black | warm metallic | warm muted | bright / cool-only |
| Neobrutalism | bright primary (yellow / pink / lime) | bright single primary | any bright | muted / desaturated |
| Organic Nature | earth tones (sage / clay / sand) | earth palette | warm muted | electric / neon |
| Kinetic Editorial | editorial 2–3 color | editorial palette | any 2–3 color | single neutral |
| 3D Immersive | gradient / metallic | gradient or chrome | bright | flat single |
| Aurora UI | gradient (purple → pink / blue → teal) | gradient pair | any 2 bright hues | flat single neutral |
| Glassmorphism | blue / purple gradient on dark | gradient pair | bright single | flat dark / earth |
| Claymorphism | pastel multi-color | pastel 3+ | any 3+ | monochrome |
| Bento Grid | 4–6 distinct surface colors | 4+ distinct | 2–3 | single |

If the user explicitly provides only neutrals + no accent, treat as `+1` everywhere — the style will provide the accent.

### 3b. Typography lean match (0–3)

| Style | Preferred lean | +3 | +2 | +0 |
|---|---|---|---|---|
| Swiss | sans (geometric / grotesk) | sans | display sans | serif-only |
| Magazine | serif display + sans body | serif or mixed | sans-only | mono-only |
| Fashion | serif display (Didot-family) or wide sans | serif or display | sans | mono |
| Brutalist | sans (default system / Helvetica / Arial) | sans | mono | ornate serif |
| Type-First | sans grotesk or mono | sans or mono | display | serif-only |
| Editorial Maximal | serif display + sans body | serif or mixed | display | sans-only |
| Corporate | sans (Inter / Söhne / Aktiv) | sans | display sans | brutalist serif |
| Minimal Float | sans (light weight) | light sans | normal sans | heavy display |
| Dark Luxury | serif display (high contrast) + sans body | serif or display | mixed | sans-only |
| Neobrutalism | sans heavy + display | heavy sans | display | light serif |
| Organic Nature | rounded sans + handwritten/serif accent | rounded sans or mixed | sans | brutalist mono |
| Kinetic Editorial | display serif or variable font | display or variable | serif | mono-only |
| 3D Immersive | display sans (geometric) | display | sans | brutalist |
| Aurora UI | sans (light to medium) | sans | display | brutalist |
| Glassmorphism | sans (Inter family) | sans | display | brutalist |
| Claymorphism | rounded sans | rounded sans | sans | brutalist mono |
| Bento Grid | sans (Inter / Söhne) | sans | display sans | brutalist |

### 3c. Density match (0–2)

| Style | Preferred density | +2 if brand says | +0 if |
|---|---|---|---|
| Minimal Float / Swiss / Fashion / Editorial | airy | airy | packed |
| Aurora / Glass / Clay / Bento / Corporate / Neo / Organic / Magazine / Kinetic / 3D / Dark Luxury | balanced | balanced or airy | (no penalty) |
| Brutalist / Type-First | airy or packed (intentional) | airy or packed | balanced |

### 3d. Formality match (0–2)

| Style | Formality bucket |
|---|---|
| Swiss / Corporate / Minimal Float / Type-First / Editorial | corporate or editorial |
| Magazine / Fashion / Dark Luxury / Editorial Maximal | editorial or luxury |
| Brutalist / Neobrutalism / Kinetic | brutalist or playful |
| Organic Nature / Claymorphism | playful or editorial |
| Aurora / Glass / 3D / Bento | corporate (AI / tech vibe) |

+2 if brand `formality` matches the style's bucket. +0 if it's a 2-step mismatch (e.g. `brutalist` brand vs Aurora UI).

### Scoring output format

```markdown
## Top 3 style matches

| Rank | Style | Score | Why |
|---|---|---|---|
| 1 | Swiss Editorial | 9/10 | Palette: single saturated accent (+3). Sans grotesk lean (+3). Airy density (+2). Corporate formality (+1, slight under-match). |
| 2 | Type-First Monochrome | 8/10 | … |
| 3 | Corporate Clean | 7/10 | … |

**Recommended**: Swiss Editorial — strongest signal alignment.
```

---

## 4. Token override rules (Mode 5 B4)

Once the user picks a style, apply these rules to merge Brand DNA into the style's default tokens:

| Token | Behavior |
|---|---|
| `--color-accent` | **Always** override with brand's primary `accent`. |
| `--color-bg` | Keep style default unless brand explicitly defines a `bg` role color AND it's not pure white (style's default of off-white / #fafaf8 is intentional). |
| `--color-ink` | Keep style default unless brand explicitly defines `ink`. If overridden, verify contrast ≥ 7:1 (AAA) against `--color-bg`. |
| `--color-support` | Use brand's `support` color if present, otherwise keep style default. |
| `--font-display` | If brand provides a display font AND it's compatible with the style's typography lean (e.g. brand serif + Magazine style → use it), substitute. Otherwise keep style default and flag in the output: "Brand font not used — incompatible lean (serif brand vs Swiss sans-grotesk default)". |
| `--font-body` | Same as `--font-display`. |
| `--radius-*` | Never override from brand. Style's radius is part of its identity. |
| `--shadow-*` | Never override from brand. |
| Motion tokens | Use brand's `motion_vibe` only if style allows motion (skip for Swiss / Brutalist). |

### Contrast fallback

If the brand's chosen accent fails WCAG AA against the style's `--color-bg`:

1. **Try a darkened variant**: reduce L (lightness in OKLCH) by steps of 5% until contrast ≥ 4.5:1 for text use, ≥ 3:1 for large-text use.
2. **Try the brand's support color** if available.
3. **Last resort**: flag the failure to the user, suggest using brand color only for non-text decoration (borders, dividers), and use the style's default accent for text.

Always output the contrast ratio for every brand color pair used in text contexts. Format:

```markdown
## Brand contrast verification

| Pair | Ratio | WCAG |
|---|---|---|
| brand accent #635BFF on bg #ffffff | 5.2:1 | ✅ AA |
| brand ink #0A2540 on bg #ffffff | 16.4:1 | ✅ AAA |
| brand accent on style.surface #f8f7f4 | 4.9:1 | ✅ AA |
```

---

## 5. Brand-derived tokens callout (Mode 5 output addition)

After B4, output a callout block that shows which tokens came from where. This is the user-facing receipt of what Mode 5 actually did.

```markdown
## 🏷️ Brand-derived tokens

| Token | Value | Source |
|---|---|---|
| `--color-accent` | #635BFF | Brand (logo primary) |
| `--color-ink` | #0A2540 | Brand (user-provided hex) |
| `--color-bg` | #ffffff | Style default (Swiss) — brand had no bg override |
| `--font-display` | "Söhne Breit", "Inter Tight", sans-serif | Style default (Swiss) — brand had no display font |
| `--font-body` | "Söhne", "Inter Tight", sans-serif | Style default (Swiss) |
| `--radius-default` | 0 | Style default (Swiss) — radius never overridden from brand |

**Notes**:
- Brand font (Söhne Schmal) is on brand guidelines but kept Swiss's default because Söhne Breit is the wider sibling and pairs better with the style. Switch if user prefers strict brand fidelity.
- All brand color pairs verified ≥ AA contrast (see contrast table).
```
