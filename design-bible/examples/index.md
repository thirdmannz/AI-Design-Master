# Real Example Pages Library

> Complete, production-ready HTML+CSS reference pages. Each shows a specific style × industry × page-type combination. Use these as the ground truth for "what this style actually looks like shipped."

## Combinations

| File | Style | Industry | Page Type | Anti-AI Notes |
|------|-------|----------|-----------|---------------|
| [saas-swiss.html](saas-swiss.html) | Swiss Editorial | SaaS | Landing page | Grid-based, no cards, numbered sections |
| [saas-type-first.html](saas-type-first.html) | Type-First Monochrome | SaaS | Landing page | Text-only hero, no images, letter-stagger |
| [pricing-neobrutalism.html](pricing-neobrutalism.html) | Neobrutalism | SaaS | Pricing page | Hard borders, no rounded cards, blunt copy |
| [pricing-brutalist.html](pricing-brutalist.html) | Brutalist | Agency | Pricing page | Monospace, table-based, no decoration |
| [portfolio-fashion.html](portfolio-fashion.html) | Fashion/Luxury | Portfolio | Project grid | Asymmetric, full-bleed images, serif |
| [editorial-magazine.html](editorial-magazine.html) | Magazine Longform | Editorial | Article page | Drop cap, marginalia, pull quote |
| [landing-aurora.html](landing-aurora.html) | Aurora UI | Product | Landing page | Gradient mesh, spring motion, no blobs |
| [landing-corporate.html](landing-corporate.html) | Corporate Clean | SaaS | Landing page | Professional, table-like features, WCAG AAA |
| [agency-brutalist.html](agency-brutalist.html) | Brutalist | Agency | Homepage | Raw HTML feel, border-only design |
| [portfolio-minimal.html](portfolio-minimal.html) | Minimal Float | Portfolio | About page | Whitespace-first, no decoration |

## How to use

1. Open any `.html` file directly in a browser — all self-contained
2. View-source to read the CSS — tokens in `:root {}`, components follow
3. Use as reference when Skill says "output similar to X style"
4. In Revamp mode (R3), point user to the matching style example

## Design decisions documented

Each example file has inline comments explaining:
- Why this layout is NOT the AI default
- Which AI tells were deliberately avoided
- Token values and why they were chosen
- Mobile adaptation strategy

## Validation status

All examples have been checked against the 12-item rubric:
- AI Tells Blocklist: ✅ 0 violations
- WCAG AA contrast: ✅ (all body text ≥ 4.5:1)
- Mobile layout: ✅ (tested at 375px)
- Studio-quality: ✅ (none look like v0/Lovable output)
