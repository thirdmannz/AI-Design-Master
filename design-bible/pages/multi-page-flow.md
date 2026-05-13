# Multi-Page Flow (Mode 7)

> M7 reference. Generates 5–15 cross-page-coherent pages from a locked manifest in a single run. Reads from `.design-master/design-system.json`, writes to `.design-master/pages/`.

The skill.md Mode 7 section describes *when* each step runs; this file describes *how* each step works in detail. Page anatomies live in [page-templates.md](page-templates.md) (M4) — Mode 7 *executes* that documentation rather than reinventing it.

---

## Prerequisite

**A locked manifest must exist** at `.design-master/design-system.json` with `locked: true`. Mode 7 will not generate from defaults. If absent:

> Multi-Page requires a locked design system. Run /design (Mode 1 or Mode 5) first, then come back with "build the full site".

---

## Step P1 — Page selection

Use `AskUserQuestion` (Claude Code) / numbered text (Codex) with `multiSelect: true` from the 10 page types in [page-templates.md](page-templates.md):

```
Which pages do you want to generate? (homepage is required)
  1. Homepage             ← required
  2. Pricing
  3. About
  4. Blog index
  5. Blog post
  6. Docs
  7. Landing (campaign page)
  8. 404
  9. Auth (login / signup)
  10. Checkout
```

Homepage must be included — every other page links back to it. Record the picks in the manifest's `pages` array.

---

## Step P2 — Read page anatomies

For each picked page, read its anatomy from [page-templates.md](page-templates.md). Each template specifies:

- Required sections (e.g. Homepage: hero / features / social proof / CTA / footer)
- Recommended sections per industry
- Per-style adaptations (Swiss Editorial homepage looks different from Aurora homepage)
- Component composition (which of the 20 components from [design-bible/components/](../components/) to use)

**Do not deviate from page-templates.md anatomy unless the manifest's `design.applied_constraints` requires it.**

---

## Step P3 — Shared element extraction

Three blocks are *byte-identical* across every generated page:

1. **`<head>`** — meta, fonts, the `:root {}` token block, base reset CSS
2. **`<nav>`** — same nav items, same structure, same active-state logic
3. **`<footer>`** — same columns, same copyright line

Generate each block exactly once. How to share depends on the manifest's `design.framework`:

| Framework | Shared-element strategy |
|---|---|
| `html-css` | Copy-paste the block into every page with a clear `<!-- SHARED: nav-v1 (do not edit per-page) -->` comment marker. Add a `<!-- /SHARED -->` close marker. P5 cross-page check validates these blocks are byte-identical. |
| `react-tailwind` | Generate `components/shared/Nav.tsx`, `components/shared/Footer.tsx`, `app/layout.tsx`. Each page imports them. |
| `vue-tailwind` | Same as React, generate `components/Nav.vue`, `Footer.vue`. |
| `svelte` | Generate `lib/components/Nav.svelte`, `Footer.svelte`. |
| `astro` | Generate `src/layouts/Layout.astro` with `<slot />` + import shared `Nav.astro` / `Footer.astro`. |

**The token block (`:root {}`)** comes verbatim from the manifest's `design.tokens`. No regeneration. No drift.

---

## Step P4 — Per-page generation

For each page in the picked set, run the equivalent of Mode 1 Step 3 (per-style component output) with two locks:

**Token lock**: every CSS value comes from `var(--*)` referring to the manifest. No inline hex. No inline font-family. If a component spec in [design-bible/components/](../components/) needs a value not in the manifest, *add it to the manifest* first (and append a version_log entry like "Mode 7 expanded tokens for component X").

**Constraint lock**: the manifest's `design.applied_constraints` apply to every page. If "no-card-shadows" is locked, the pricing cards on `pricing.html` cannot suddenly have shadows.

**Per-page differences are allowed** in:
- Hero copy (different per page)
- Section ordering (homepage hero ≠ pricing hero)
- Page-specific components (pricing table on pricing.html, FAQ on landing.html)

**Per-page differences are NOT allowed** in:
- Token values (look at the manifest)
- Nav structure (P3 shared block)
- Footer structure (P3 shared block)
- Color / type / spacing scales (manifest tokens)
- Motion language (manifest tokens)

---

## Step P5 — Cross-page coherence check (automated)

Before writing the files, run these checks. Each must pass or surface a fix.

### 5a. `:root` byte-identity

Extract the `:root {}` block from each generated page's HTML/CSS. They must be byte-identical (after normalizing whitespace).

```
✅ All 5 pages share identical :root block (18 tokens)
❌ pricing.html :root differs at --space-section (8rem vs 6rem)
   → Force-replace with manifest value, log to version_log as "P5 sync"
```

### 5b. Internal link graph closure

Every `<a href>` that starts with `/` or matches a picked page filename must resolve to a generated page. No dead internal links.

```
✅ 23 internal links, all resolve
❌ /blog/post-1 → not in picked pages
   → Either remove the link or add the page to the set
```

### 5c. Nav consistency

The nav block on every page must be byte-identical (after the active-state class is normalized to `aria-current="page"` on the matching link).

```
✅ Nav byte-identical on all 5 pages after active-state normalization
```

### 5d. Token drift detection

Scan every generated CSS file for inline `#hex`, raw `rgb()`, raw font names, raw px values that aren't `0` or `1px`. Every value must reference a `var(--*)` token from the manifest.

```
✅ No token drift detected
❌ landing.html line 142: background: #f0f0f0 (not a manifest token)
   → Replace with var(--color-surface) or add #f0f0f0 to manifest as new token
```

### 5e. Footer consistency

Same as 5c, but for the footer block.

### 5f. Component coherence

Components must follow the per-style override rules from [page-templates.md](page-templates.md) and the AI Tells Blocklist (skill.md L1305). If "Swiss Editorial" is the locked style, no page can suddenly have a `border-radius: 9999px` pill button.

---

## Step P6 — Bulk visual validation (abbreviated Step 5)

For each generated page:

1. Render via `mcp__Claude_Preview__preview_start` (or skip + text-only if no MCP)
2. Screenshot 3 viewports (375 / 768 / 1280) — desktop only is acceptable for non-homepage pages if time-constrained
3. Inject axe-core (reuse Step 5.3)
4. Score against the 12-item rubric

**Differences from Step 5 full run**:
- Skip the auto-refinement loop (Step 5.5) unless a page scores ≤8/12 — multi-page can't afford 3 cycles × N pages
- Pages scoring ≤8/12 get flagged in the sitemap report; user picks whether to auto-refine or accept
- Performance gates (Step 5.4b) run on homepage only by default; user can opt into running on all pages

---

## Output: sitemap.md

After P6, write `.design-master/pages/sitemap.md`:

```markdown
# Multi-Page Generation — Sitemap

**Project**: acme-saas
**Locked design**: Swiss Editorial (v3, brand-aware)
**Generated**: 2026-05-13T15:32:00Z
**Pages**: 5

| Page | File | Rubric | AI Tells | Performance | Notes |
|---|---|---|---|---|---|
| Homepage | index.html | 12/12 ✅ | 0/10 | ✅ all gates pass | — |
| Pricing | pricing.html | 11/12 ⚠️ | 0/10 | (skipped) | mobile layout marginal at 375px |
| About | about.html | 12/12 ✅ | 0/10 | (skipped) | — |
| Blog index | blog/index.html | 12/12 ✅ | 0/10 | (skipped) | — |
| 404 | 404.html | 12/12 ✅ | 0/10 | (skipped) | — |

## Cross-page coherence
- ✅ :root byte-identical across all 5 pages
- ✅ Internal link graph closed (no dead links)
- ✅ Nav byte-identical
- ✅ Footer byte-identical
- ✅ No token drift

## Files written
- .design-master/pages/index.html
- .design-master/pages/pricing.html
- .design-master/pages/about.html
- .design-master/pages/blog/index.html
- .design-master/pages/404.html

## Next steps
- Open .design-master/pages/index.html in browser to preview
- Refine: say "tighten pricing page hero" or "switch nav to centered" (token-level refinement at Step 4)
- Export tokens for Figma: say "export tokens"
```

---

## Failure modes & recovery

| Failure | Recovery |
|---|---|
| Manifest missing | Refuse, route to Mode 1 / Mode 5 |
| Manifest `locked: false` | Warn: "Design system is unlocked. Mode 7 needs a locked baseline." Offer to relock or re-pick. |
| Page in page-templates.md absent | This shouldn't happen — all 10 are there. If it does, the skill needs to update page-templates.md, not silently skip. |
| P5 5a–5f fails | Auto-fix and log to version_log as "P5 sync". If auto-fix isn't safe (e.g. a new color was inlined), surface to user. |
| P6 page scores ≤8/12 | Flag in sitemap. Do not block delivery. User can request auto-refine on that specific page later. |
| Performance gates fail on homepage | Surface in sitemap, suggest fixes (see Step 5.4b). Do not block delivery. |
| No Chrome MCP / Preview MCP | Skip P6 visual validation; text-only critique against rubric. Mark pages as "rubric-text-only" in sitemap. Performance gates skipped. |

---

## Why this design

- **Manifest is the single source of truth** — no token drift across pages because there's no parallel state to drift from
- **page-templates.md is the page anatomy** — we don't duplicate "what goes on the pricing page", we execute what M4 documented
- **Shared blocks are byte-identical** — easiest way to guarantee coherence is mechanical equality, not "looks the same"
- **Abbreviated Step 5** — full Step 5 × N pages × 3 viewports × 3 refinement cycles is too expensive; truncate to rubric-only for non-homepages
- **Failure modes don't block** — if one page is marginal, the sitemap surfaces it but ships the bundle anyway; user picks whether to refine
