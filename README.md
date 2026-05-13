# 🎨 AI Design Master

> A Claude Code skill that turns you into a web design expert — powered by real patterns from **godly.website**, **awwwards**, **siteinspire**, **land-book**, **httpster**, **minimal.gallery**, and **dribbble**.

Stop building websites that look AI-generated. This skill gives you a curated design system of **17 professional styles** (5 of them explicit anti-AI presets), each with real CSS tokens, typography pairings, per-style component examples, and a hard **AI Tells Blocklist** that the model must self-check against before producing output.

[中文說明 →](README.zh.md)

---

## ✨ Features

### Core (M0 baseline)
- **17 Design Styles** — from Swiss Editorial and Magazine Longform to Brutalist and Type-First Monochrome, each with full CSS custom properties, font pairings, and **per-style component snippets** (no more flattening every style into the same Hero+Nav+Card+Button+Footer template)
- **AI Tells Blocklist** — 10 hard-banned patterns the model must avoid by default: pill buttons everywhere, Hero+subtitle-pill, backdrop-blur cards, Inter+Lucide+slate combo, gradient blobs, identical 3-column features grids, etc.
- **Constraints / Anti-AI Mode** — pick 2-3 constraints (no rounded corners, asymmetric layout, two-color palette, type-first hierarchy…) to break out of AI defaults
- **Dual-Variant Output** — every design system ships in two flavors: a conservative Variant A and an experimental Variant B that intentionally violates at least one AI default
- **AI-tell-heavy styles gated** — Glassmorphism, Aurora UI, Claymorphism, Bento Grid are only recommended when you explicitly ask for "AI / futuristic / glass" feel. The default route never goes there.

### Professional layer (M1 — Quality Foundations)
- **Accessibility built-in** — WCAG AA contrast required, semantic HTML enforced, ARIA patterns, per-style focus rings, keyboard nav with skip links. 5 hard a11y gates run before every output.
- **Responsive system** — mobile-first 3-breakpoint CSS required for every component; per-style mobile adaptation rules (Kinetic disables parallax on mobile, Glassmorphism drops blur on mobile, etc.)
- **Iterative Refinement Loop (Step 4)** — after dual variants, user can request local patches ("swap accent color", "make hero asymmetric") and skill emits diffs not full re-renders. Max 5 cycles before suggesting brief revisit.

### Production-ready outputs (M2 — Component × Framework × Industry)
- **20 component library** — Hero, Nav, Features, Pricing, Testimonials, FAQ, CTA, Footer, Form, Card, Table, Stats, Logo Cloud, Blog (index/post), Empty state, Loading/Skeleton, 404, Modal, Toast, Sidebar. Each with canonical HTML+CSS, 17-style variation matrix, a11y checklist, framework conversion notes.
- **5 framework outputs** — React+Tailwind (shadcn-aligned), Vue+Tailwind, Svelte 5, Astro, plain HTML+CSS. User picks output format in Step 1.
- **5 industry bundles** — SaaS, E-commerce, Editorial, Portfolio, Docs. Each bundle pre-defines required components, recommended styles, and industry-specific AI tells to avoid.

### Sensory layer (M3 — Motion + Image)
- **Motion design system** — per-style motion language: Swiss/Brutalist no-motion, Aurora spring, Kinetic parallax, Type-First letter stagger, Magazine slow fade. Universal `prefers-reduced-motion` respect. Duration scale + easing tokens.
- **Image/Asset strategy** — per-style photography/illustration/abstract/none guidance with Unsplash keywords, placeholder URLs, performance defaults (`<picture>` + avif/webp + lazy loading)
- **Mood board generation** — Step 2 recommends styles with mood boards (screenshots + palette swatches + typography sample + motion line + image style line)

### Multi-page coherence (M4)
- **10 page-level templates** — Homepage, Pricing, About, Blog Index/Post, Docs, Landing, 404, Auth, Checkout. Each with anatomy + component composition + per-style adaptations.
- **Revamp R4 completion** — 10 substeps: token diff, component migration map, AI Tells risk warnings, rollback guide with git revert commands, design system integration table. Multi-phase commits supported.

### Visual self-validation (M5 — the moat)
- **Step 5: Visual Validation Loop** — uses **Claude Preview MCP** to render output → screenshot 3 viewports → run axe-core → self-score against 12-item rubric → auto-refine (max 3 cycles) if ≥3 items fail
- **Self-Critique Rubric** — 12 hard gates: AI Tells / token consistency / hero alignment / WCAG AA / focus visible / forbidden components / type hierarchy / whitespace / color count / motion fit / mobile / "studio-quality" feel
- **Design validation report** — 3 viewports + 12-item scorecard + axe-core report + refinement log + manual review suggestions

### Brand-aware generation (M6 — Mode 5)
- **Brand DNA extraction** — upload a logo, screenshot, hex codes, brand-guidelines PDF, or describe the vibe; the skill extracts palette + typography lean + density + formality into a structured profile
- **17-style signal matching** — scores every style 0–10 across palette compatibility, typography lean, density, and formality; returns Top 3 matches with reasoning
- **Brand × style token merge** — overrides `--color-accent` (and selected others) from the brand, keeps `--radius-*` / `--shadow-*` as style identity, runs WCAG AA contrast verification on every brand color pair, falls back to a darkened variant if it fails
- **Brand-derived tokens callout** — every output annotates which tokens came from the brand vs the style default, so cross-style refinement later can preserve brand identity

### Design audit (M6 — Mode 6)
- **Audit any URL or pasted HTML** — uses Chrome MCP to fetch + screenshot, falls back to user-pasted HTML on Codex
- **Verdict + 12-item scorecard + AI Tells Index** — same rubric Step 5 uses on the skill's own output, applied to external pages
- **Top 5 concrete improvements** — every entry must cite a real selector, current measured state, a CSS diff with the page's own class names, and a measurable expected impact (contrast ratio delta, AI Tells removed, etc.). Generic phrasings ("improve contrast", "modernize design") are banned by the skill itself.
- **Optional drop-in fix snippet** — packages the fixes as a single CSS append the user can paste
- **Re-audit loop** — paste the fixed version to confirm rubric score improved

### Conversational refinement (M6 — Step 4 upgrade)
- **Natural-language → token mapping** — "make it bolder", "more whitespace", "less corporate", "warmer" map directly to specific `:root {}` token edits
- **Token-level diffs only** — refinement never regenerates the full HTML, only diffs the changed tokens + lists affected selectors; visual loop is opt-in, not re-run per turn
- **Cross-style switching mid-flow** — "switch to Brutalist" diffs the current style's tokens against the target style's tokens without restarting Mode 1; brand-derived tokens (from Mode 5) are preserved across the switch
- **Version history** — every refinement creates `v[N]` and the log accumulates; user can ask "revert to v2" or "what changed between v2 and v4"

### Framework-agnostic + No mandatory build
- Works with React, Vue, Svelte, Astro, plain HTML/CSS, or Tailwind

---

## 🚀 Installation

Works in **Claude Code**, **Codex (OpenAI CLI)**, or any agent with file Read/Edit/Write/Glob/Grep support.

### Claude Code (primary target — full feature set)

```bash
git clone https://github.com/thirdmannz/AI-Design-Master.git
cd AI-Design-Master

# macOS / Linux
cp skill.md ~/.claude/skills/design.md

# Windows
copy skill.md %USERPROFILE%\.claude\skills\design.md
```

Trigger: open any project in Claude Code and type `/design`.

Full feature set includes structured `AskUserQuestion` UI (multi-select, previews) + **Visual Validation Loop** via Claude Preview MCP (renders output → screenshots 3 viewports → axe-core → 12-item rubric auto-refinement).

### Codex (OpenAI CLI)

Codex doesn't have `AskUserQuestion` or `mcp__Claude_Preview__*`, but the skill includes fallbacks (numbered text prompts + text-only critique). See [AGENTS.md](AGENTS.md) for full Codex integration.

**Option A — project-local:**
```bash
git clone https://github.com/thirdmannz/AI-Design-Master.git path/to/your-project/.design-master
# In your project's AGENTS.md, reference .design-master/AGENTS.md or skill.md
```

**Option B — run inside this repo:**
```bash
cd AI-Design-Master
codex
# Then: "Read skill.md end-to-end and follow it. I want to design a new website."
```

**Option C — global memory:** paste `skill.md` content into codex's global instructions (e.g. `~/.codex/AGENTS.md`).

What Codex users lose vs Claude Code:
- ❌ Structured multi-select / preview question UI (skill emits numbered text prompts instead)
- ❌ Live render + screenshot + axe-core (falls back to text-only rubric critique; user opens `tmp/preview-*.html` in browser to verify)

What Codex users keep:
- ✅ All 17 design styles + AI Tells Blocklist + Constraints mode + Dual-Variant output
- ✅ All a11y + responsive + motion + image strategies
- ✅ Component library, framework outputs, industry bundles, page templates
- ✅ Iterative Refinement Loop (Step 4)
- ✅ Self-Critique 12-item rubric (text-only mode)

### Other agents (Cursor, Cline, generic API agents)

Anything with file Read/Edit/Write/Glob/Grep ops can run this. Point your agent at `skill.md` as the system prompt or initial instruction. See [AGENTS.md](AGENTS.md) for behavior contract.

---

## 🎯 How to Use

### Starting a new design

```
/design
```

Claude will ask you 3 questions:
1. What type of site? (SaaS / Portfolio / E-commerce / Landing Page / Blog / B2B / Game)
2. Who's the audience? (Tech users / Creatives / Enterprise / Consumers / Gen-Z)
3. What feeling? (Professional / Bold / Warm / Luxurious / Modern)

Then it recommends 2–3 styles and outputs:
- Complete `:root {}` CSS token set
- Google Fonts `<link>` tags
- Tailwind config equivalent
- Hero, Nav, Card, Button, Footer CSS
- 3 specific "not AI-generated" implementation tips

### Revamping an existing site

Run `/design` from inside your project directory and choose **"Revamp existing website"**.

Claude will:
1. **Scan** your CSS, HTML, JSX, Vue, config files automatically
2. **Diagnose** current design problems (generic colors, inconsistent spacing, AI-ish shadows)
3. **Recommend** the best upgrade path
4. **Output** a component-by-component migration guide with before/after CSS

### Designing for an existing brand (Mode 5)

```
/design
```

Then say "I have a logo / brand colors — match my brand" (or attach the logo, or paste hex codes). Claude will:

1. **Extract Brand DNA** — palette + typography lean + density + formality from your assets
2. **Score all 17 styles** against the DNA and present Top 3 matches with reasoning
3. **Merge brand into the chosen style's tokens** — `--color-accent` from your brand, `--radius-*` / `--shadow-*` kept as style identity, contrast verified for every text pair
4. **Hand off to the normal Step 2.5 → Step 3 → Step 4 → Step 5 flow** — dual variants come back with your brand baked in

### Auditing an existing site (Mode 6)

Say "audit this page: [URL]" or "score this design". Claude will:

1. **Fetch + screenshot** the page across 3 viewports (mobile / tablet / desktop)
2. **Score on the same 12-item rubric** Step 5 uses on its own output
3. **Run the AI Tells Blocklist** against the page's computed CSS and cite each hit with a selector
4. **Detect the page's style** (which of the 17 it resembles most)
5. **Output Top 5 concrete improvements** — each with a real selector, current measured state, a CSS diff using the page's own class names, and a measurable expected impact
6. **Optionally re-audit** after you apply the fixes to confirm the score improved

Codex (no Chrome MCP) — paste the rendered HTML + CSS and the audit runs in text-only mode.

### Iterating after the first output (Step 4 refinement)

Once Claude has produced dual variants, you can refine conversationally:

- **"make it bolder"** / **"more whitespace"** / **"warmer"** — the skill maps your phrase to specific token edits and emits a token-level diff (not a full re-render)
- **"switch to Brutalist"** — cross-style refinement without restarting; brand-derived tokens (if Mode 5 was used) are preserved
- **"revert to v2"** — every refinement is versioned; you can roll back at any point
- **"show version log"** — see the v1 → vN history of every token change

---

## 🎨 The 17 Design Styles

### Default-recommendable styles (the skill prefers these)

| # | Style | Best For | AI-tell strength |
|---|-------|----------|------------------|
| 📐 | **Swiss Editorial** ⭐NEW | Agency portfolios, design studios, design-savvy SaaS, enterprise reports | ✅ Low |
| 📰 | **Magazine Longform** ⭐NEW | Media sites, deep features, brand stories, product launches | ✅ Low |
| 👗 | **Fashion / Luxury** ⭐NEW | Fashion, beauty, jewelry, high-end hospitality, perfume brands | ✅ Low |
| 🧱 | **Brutalist / Anti-Design** ⭐NEW | Personal portfolios, experimental, artist sites, technical blogs | ✅ Low |
| 🅰️ | **Type-First Monochrome** ⭐NEW | Design-savvy SaaS, AI products (sic), design tools, portfolios | ✅ Low |
| 🕊️ | **Minimal Float** | Luxury brands, high-end portfolios | ✅ Low |
| 🖤 | **Dark Luxury** | Premium brands, hospitality, jewelry | ✅ Low |
| 🌿 | **Organic Nature** | Health, food, sustainable brands, wellness | ✅ Low |
| 📰 | **Editorial Maximal** | Media brands, design studios, magazines | ✅ Low |
| 🏢 | **Corporate Clean** | B2B, fintech, enterprise, healthcare | ✅ Low |
| 🔩 | **Neobrutalism** | Portfolios, creative tools, bold brands | ⚠️ Medium |
| ⚡ | **Kinetic Editorial** | Brand stories, interactive portfolios | ✅ Low |
| 🌐 | **3D Immersive** | Games, premium products, interactive art | ⚠️ Medium |

### Gated styles (only when you explicitly ask for "AI / futuristic / glass" feel)

| # | Style | Why gated |
|---|-------|-----------|
| 🪟 | **Glassmorphism** | Hallmark of v0/Lovable/Bolt — only opt-in |
| 🌌 | **Aurora UI** | Same family as Glassmorphism — only opt-in |
| 🫧 | **Claymorphism** | The pill-button-everywhere style — only opt-in |
| 🍱 | **Bento Grid** | Heavily AI-trained pattern — only when you actually need a structured dashboard |

Each style includes:
- Complete CSS custom properties (`:root {}`)
- Tailwind config equivalent
- Font pairings with Google Fonts
- Hero, Card, Button component examples
- 3 "not AI-generated" techniques specific to that style

---

## 💡 Anti-AI Design Principles

The skill enforces three layers of anti-AI guidance, in priority order:

### 1. AI Tells Blocklist (hard bans, default-applied)

The model must self-check against these 10 patterns before producing output. They are gated — only unlocked when the user explicitly picks the corresponding style.

- ⛔ `border-radius: 9999px` on all buttons / badges (pill-everything) — only Claymorphism unlocks
- ⛔ Hero with emoji subtitle pill ("✨ New", "🎉 Launch") — **never unlocked**
- ⛔ Card with default `backdrop-filter: blur()` — only Glassmorphism unlocks
- ⛔ Background gradient blob / aurora — only Aurora UI unlocks
- ⛔ Inter + Lucide + slate-* / gray-* combo — **never unlocked**
- ⛔ "Trusted by" logo cloud locked under hero — only Corporate Clean unlocks
- ⛔ 3-column features card grid with identical icon style — **never unlocked**
- ⛔ All-centered hero / section / CTA — only Aurora / Glass unlock
- ⛔ Same `box-shadow: 0 2px 4px rgba(0,0,0,0.1)` on every card — never unlocked
- ⛔ "Get started" + "Learn more" CTA pair (filled + outlined) — only Corporate Clean / Bento unlock

### 2. Constraints / Anti-AI Mode

After picking a style, the user picks 2-3 constraints from a checklist (no rounded corners, no gradients, two-color palette, asymmetric layout, type-first hierarchy, no card shadows, etc.). These force the model out of comfortable defaults.

### 3. Per-style component overrides

The skill **does not** emit Hero+Nav+Card+Button+Footer for every style. Each style has its own component list — Swiss Editorial gets `Masthead+Kicker+Numbered Index+Dateline+12-col baseline grid`, Brutalist gets `Slab heading+Index list+Raw form+Default underline link`, Magazine Longform gets `Masthead+Kicker+Lede+Drop cap+Pull quote+Marginalia+Full-bleed image`. The universal template was the structural cause of "AI shape" — it's gone.

### 4. Cosmetic touches (last priority)

- Negative letter-spacing on headlines (`-0.03em`)
- Off-white backgrounds (`#fafaf8` not `#fff`)
- Asymmetric glows
- Three shadow elevations (xs / sm / md)
- `clamp()` fluid typography
- Organic border-radius (`30% 70% 70% 30% / 30% 30% 70% 70%`)
- Intentional misalignment

---

## 📁 File Structure

```
AI-Design-Master/
├── skill.md                          ← Install this to ~/.claude/skills/design.md
├── design-bible/
│   ├── styles/                       ← 17 style references (12 original + 5 new anti-AI)
│   │   ├── swiss_editorial.md
│   │   ├── magazine_longform.md
│   │   ├── fashion_luxury.md
│   │   ├── brutalist.md
│   │   ├── type_first_mono.md
│   │   └── ... (12 more)
│   ├── a11y/                         ← M1: Accessibility reference
│   │   ├── contrast-rules.md
│   │   ├── semantic-patterns.md
│   │   ├── aria-patterns.md
│   │   ├── focus-states.md           ← Per-style focus CSS for all 17 styles
│   │   └── keyboard-nav.md
│   ├── responsive/                   ← M1: Mobile-first breakpoint system
│   │   └── breakpoints.md            ← Per-style mobile adaptation rules
│   ├── components/                   ← M2: 20 component library
│   │   ├── hero.md
│   │   ├── nav.md
│   │   ├── features.md
│   │   ├── pricing.md
│   │   ├── testimonials.md
│   │   ├── faq.md
│   │   ├── cta.md
│   │   ├── footer.md
│   │   ├── form.md
│   │   ├── card.md
│   │   ├── table.md
│   │   ├── stats.md
│   │   ├── logo-cloud.md
│   │   ├── blog.md
│   │   ├── empty-state.md
│   │   ├── loading.md
│   │   ├── 404.md
│   │   ├── modal.md
│   │   ├── toast.md
│   │   └── sidebar.md
│   ├── frameworks/                   ← M2: 5 framework outputs
│   │   ├── react-tailwind.md
│   │   ├── vue-tailwind.md
│   │   ├── svelte.md
│   │   ├── astro.md
│   │   └── html-css.md
│   ├── industry/                     ← M2: 5 industry bundles
│   │   ├── saas.md
│   │   ├── ecommerce.md
│   │   ├── editorial.md
│   │   ├── portfolio.md
│   │   └── docs.md
│   ├── motion/                       ← M3: Per-style motion language
│   │   └── motion-system.md
│   ├── images/                       ← M3: Per-style image/asset strategy
│   │   └── image-system.md
│   ├── pages/                        ← M4: 10 page-level templates
│   │   └── page-templates.md
│   ├── critique/                     ← M5: Self-validation rubric
│   │   └── rubric.md
│   ├── brand/                        ← M6: Brand DNA schema + 17-style signal matrix
│   │   └── brand-extraction.md
│   └── audit/                        ← M6: Audit report template + concrete-vs-generic rule
│       └── audit-template.md
├── scraper/                          ← Source extractors for style references
│   ├── lib/extract-tokens.js         ← Shared token extraction
│   ├── scrape-godly.js
│   ├── scrape-dribbble.js
│   ├── scrape-awwwards.js            ⭐NEW
│   ├── scrape-siteinspire.js         ⭐NEW
│   ├── scrape-landbook.js            ⭐NEW
│   ├── scrape-httpster.js            ⭐NEW
│   ├── scrape-minimalgallery.js      ⭐NEW
│   ├── compile-bible.js              ← Multi-signal classifier (rewritten with source-aware bias)
│   └── inject-new-styles.py          ← One-shot bootstrap if you can't run Node
└── data/
    └── design-bible.json             ← 17-style database (5 new ones bootstrapped from manual references)
```

---

## 🔧 Requirements

### To use the skill

- [Claude Code](https://claude.ai/code) (CLI or desktop app)
- No other dependencies — the skill runs entirely through Claude

### To re-run the scrapers (optional, for refreshing style references)

- [Node.js 20+](https://nodejs.org)
- Run: `cd scraper && npm install && npm run all`
- This will scrape all 7 sources (godly, dribbble, awwwards, siteinspire, land-book, httpster, minimal.gallery), classify them with the new multi-signal classifier, and regenerate `design-bible.json` with full token data.
- Individual scrapers: `npm run scrape:awwwards`, `npm run scrape:siteinspire`, etc. Each accepts `--dry-run` to test selectors against ~5 sites before doing the full run.

If you don't have Node installed, the skill still works — `inject-new-styles.py` already bootstrapped the 5 new styles into `design-bible.json` using manually-curated reference URLs.

---

## 📖 Design Style Quick Reference

### Style Selection Matrix (default route — never recommends gated styles unprompted)

| Site Type | First Pick | Second Pick | Alternatives |
|-----------|-----------|-------------|-------------|
| SaaS / Tool | **Type-First Monochrome** ⭐, Corporate Clean | Editorial Maximal, Minimal Float | Bento Grid (only for structured dashboards) |
| Portfolio | Minimal Float, Neobrutalism | **Brutalist** ⭐, **Swiss Editorial** ⭐ | Editorial, Kinetic |
| E-commerce / Brand | **Fashion / Luxury** ⭐, Dark Luxury | Organic Nature, Editorial | Magazine Longform |
| Marketing Landing | **Magazine Longform** ⭐, Editorial Maximal | Type-First Monochrome, Corporate Clean | Kinetic Editorial |
| Enterprise / B2B | Corporate Clean, Minimal Float | Type-First Monochrome | Editorial Maximal |
| Game / Interactive | 3D Immersive, Kinetic Editorial | Neobrutalism | Brutalist |
| Health / Lifestyle | Organic Nature, Minimal Float | Magazine Longform | Editorial Maximal |
| AI Product | **Type-First Monochrome** ⭐ (sic), Editorial Maximal | Corporate Clean, Minimal Float | Aurora UI (only when explicitly asked for) |
| Media / Content | Magazine Longform, Editorial Maximal | Swiss Editorial | Type-First Monochrome |
| Design Studio / Agency | Swiss Editorial, Editorial Maximal | Type-First Monochrome, Brutalist | Kinetic Editorial |

> **Why "AI Product → Type-First Monochrome"?** Because the visual language of "AI products" (glass, aurora, gradient blobs, pill chips) is now the default of every AI codegen tool. The way to actually look like a serious AI product is to look unlike AI codegen output — which means typographically-driven, monochrome, no decoration. Linear, Vercel, Stripe, MSCHF, Readymag — all live there.

---

## 🤝 Contributing

Found a great design pattern not covered here? Open a PR to add it to `design-bible/styles/`.

Each style file follows this structure:
- Style description and best use cases
- Complete CSS tokens
- Typography pairings
- Component examples
- "Not AI-generated" techniques

---

## 📄 License

MIT — use freely in personal and commercial projects.

---

*Design knowledge sourced from [godly.website](https://godly.website), [awwwards.com](https://www.awwwards.com), [siteinspire.com](https://www.siteinspire.com), [land-book.com](https://land-book.com), [httpster.net](https://httpster.net), [minimal.gallery](https://minimal.gallery), and [dribbble.com](https://dribbble.com) — with manual hand-picks from Pentagram, Bureau Borsche, Loewe, Jacquemus, Bloomberg Businessweek, MSCHF, Linear, Vercel Design, Stripe Press, and other top-tier shipped sites that intentionally avoid AI defaults.*
