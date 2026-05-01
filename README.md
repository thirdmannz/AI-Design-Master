# 🎨 AI Design Master

> A Claude Code skill that turns you into a web design expert — powered by real patterns from **godly.website** and **dribbble.com**.

Stop building websites that look AI-generated. This skill gives you a curated design system of **12 professional styles**, each with real CSS tokens, typography pairings, component examples, and "anti-AI" techniques — distilled from 131 real websites and 320 design shots.

[中文說明 →](README.zh.md)

---

## ✨ Features

- **12 Design Styles** — from Glassmorphism to Neobrutalism, each with full CSS custom properties, font pairings, and component snippets
- **New Design Mode** — answer 3 questions, get a complete design system ready to implement
- **Revamp Mode** — paste your existing codebase, get a diagnosis + step-by-step migration guide
- **Anti-AI Principles** — specific techniques that make your site feel hand-crafted, not generated
- **Framework-agnostic** — works with React, Vue, Next.js, plain HTML/CSS, or Tailwind

---

## 🚀 Installation

**1. Clone or download this repo**
```bash
git clone https://github.com/thirdmannz/AI-Design-Master.git
```

**2. Copy the skill file to your Claude Code skills directory**

macOS / Linux:
```bash
cp skill.md ~/.claude/skills/design.md
```

Windows:
```powershell
copy skill.md %USERPROFILE%\.claude\skills\design.md
```

**3. That's it.** Open any project in Claude Code and type `/design`.

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

---

## 🎨 The 12 Design Styles

| # | Style | Best For |
|---|-------|----------|
| 🪟 | **Glassmorphism** | SaaS, AI products, dark interfaces |
| 🔩 | **Neobrutalism** | Portfolios, creative tools, bold brands |
| 🕊️ | **Minimal Float** | Luxury brands, high-end portfolios |
| 🍱 | **Bento Grid** | SaaS feature pages, app landing pages |
| 🖤 | **Dark Luxury** | Premium brands, hospitality, jewelry |
| 🌌 | **Aurora UI** | AI products, tech startups, creative tools |
| 🫧 | **Claymorphism** | EdTech, games, fun SaaS, kids products |
| 🌿 | **Organic Nature** | Health, food, sustainable brands, wellness |
| 📰 | **Editorial Maximal** | Media brands, design studios, magazines |
| 🏢 | **Corporate Clean** | B2B, fintech, enterprise, healthcare |
| ⚡ | **Kinetic Editorial** | Brand stories, interactive portfolios |
| 🌐 | **3D Immersive** | Games, premium products, interactive art |

Each style includes:
- Complete CSS custom properties (`:root {}`)
- Tailwind config equivalent
- Font pairings with Google Fonts
- Hero, Card, Button component examples
- 3 "not AI-generated" techniques specific to that style

---

## 💡 Anti-AI Design Principles

Things this skill teaches you that make designs feel hand-crafted:

- **Negative letter-spacing** on headlines (`-0.03em`) — AI defaults leave letters too loose
- **Off-white backgrounds** (`#fafaf8` not `#fff`) — subtle but adds texture
- **Asymmetric glows** — place light sources at corners, not dead-center
- **Three shadow elevations** — xs, sm, md for different UI layers, not one-size-fits-all
- **`clamp()` fluid typography** — hero text that scales correctly, not fixed `px`
- **Organic border-radius** — four-value syntax `30% 70% 70% 30% / 30% 30% 70% 70%` for natural shapes
- **Intentional misalignment** — one element breaking the grid to create tension

---

## 📁 File Structure

```
AI-Design-Master/
├── skill.md                    ← Install this to ~/.claude/skills/design.md
├── design-bible/
│   └── styles/
│       ├── glassmorphism.md    ← Detailed reference for each style
│       ├── neobrutalism.md
│       ├── minimal_float.md
│       ├── bento_grid.md
│       ├── dark_luxury.md
│       ├── aurora_ui.md
│       ├── claymorphism.md
│       ├── organic_nature.md
│       ├── editorial.md
│       ├── corporate_clean.md
│       ├── kinetic_editorial.md
│       └── three_d_immersive.md
└── data/
    └── design-bible.json       ← Compiled style database
```

---

## 🔧 Requirements

- [Claude Code](https://claude.ai/code) (CLI or desktop app)
- No other dependencies — the skill runs entirely through Claude

---

## 📖 Design Style Quick Reference

### Style Selection Matrix

| Site Type | First Pick | Alternatives |
|-----------|-----------|-------------|
| SaaS / Tool | Aurora UI, Glassmorphism | Bento Grid, Corporate Clean |
| Portfolio | Minimal Float, Neobrutalism | Editorial, Kinetic |
| E-commerce / Brand | Organic Nature, Dark Luxury | Claymorphism, Editorial |
| Marketing Landing | Aurora UI, Kinetic Editorial | Glassmorphism, Bento Grid |
| Enterprise / B2B | Corporate Clean, Minimal Float | Bento Grid |
| Game / Interactive | 3D Immersive, Kinetic Editorial | Neobrutalism |
| Health / Lifestyle | Organic Nature, Minimal Float | Claymorphism |
| AI Product | Aurora UI, Glassmorphism | Bento Grid |

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

*Design knowledge sourced from [godly.website](https://godly.website) and [dribbble.com](https://dribbble.com) — the best curation of real-world web design.*
