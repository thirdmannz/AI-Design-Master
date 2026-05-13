# AGENTS.md — AI Design Master

This repository is a Claude Code / Codex / generic agent **skill** that turns the host agent into a senior web designer. It works across:

- **Claude Code** (primary target — full feature set including `AskUserQuestion` + Claude Preview MCP for visual validation)
- **Codex** (OpenAI CLI) — works fully except: questions become plain-text prompts with numbered options, visual validation falls back to text-only critique
- **Other agents** with file Read/Edit/Write/Glob/Grep support — same fallback path as Codex

## The skill

Everything the agent needs is in [skill.md](skill.md). Read it once at start. It describes:

- The 17 design style library (with per-style tokens, components, motion, image strategies)
- The AI Tells Blocklist (10 hard bans)
- Mode 1: New Design — Step 1 (collect info via questions) → Step 2 (recommend 2-3 styles + mood board) → Step 2.5 (Constraints) → Step 3 (dual-variant output with framework targeting) → Step 4 (refinement loop — token-level diffs, NL→token map, cross-style switching, version history) → Step 5 (visual validation loop)
- Mode 2: Revamp — Step R1 (scan code) → R2 (diagnose) → R3 (recommend target) → R4 (10-substep migration guide with token diff, component map, AI tells removal, rollback, A/B preview)
- Mode 3: Reverse — URL → identify style + extract tokens + AI Tells diagnosis → Clone or Counter-design strategy
- Mode 4: Copy / Microcopy — per-style headline formulas + per-industry copy patterns + Anti-AI Copy Checklist
- Mode 5: Brand-Aware — logo / screenshot / hex / vibe → Brand DNA extraction → 17-style signal matrix → Top 3 matches → brand × style token merge with WCAG contrast verification. Reference: [design-bible/brand/brand-extraction.md](design-bible/brand/brand-extraction.md)
- Mode 6: Design Audit — URL or pasted HTML → 12-item rubric scorecard + AI Tells Index + detected style + Top 5 *concrete* improvements (selector + diff + measured impact) → optional re-audit after fixes. Reference: [design-bible/audit/audit-template.md](design-bible/audit/audit-template.md)

## Platform-specific notes

### When running in Codex

1. **Questions**: When skill says "use AskUserQuestion", emit plain text instead:
   ```
   問 user 以下問題：
     1. Option A — description
     2. Option B — description
     3. Option C — description
   （輸入數字或自由文字）
   ```
2. **Visual Validation Loop (Step 5)**: Codex doesn't have `mcp__Claude_Preview__*` tools by default. Fall back to:
   - Write tmp HTML to `tmp/preview-<timestamp>.html`
   - Run text-only critique against [design-bible/critique/rubric.md](design-bible/critique/rubric.md) 12-item scorecard
   - Output the rubric scorecard + tell user "open `tmp/preview-*.html` in browser to verify visually"
3. **Mode 5 without vision**: If the host agent can't read image attachments:
   - Skip vision-based palette/typography extraction from logo
   - Ask user to paste hex codes + describe the logo (serif/sans, stroke weight, all-caps, etc.) per [design-bible/brand/brand-extraction.md](design-bible/brand/brand-extraction.md) §2
   - Density signal usually `not-specified` — ask follow-up question
   - Brand DNA scoring (§3 signal matrix) works identically once the DNA object is filled
4. **Mode 6 without Chrome MCP**: If `mcp__Claude_in_Chrome__*` and `mcp__Claude_Preview__*` are unavailable:
   - Ask user to paste rendered HTML + the CSS (or fetch from `view-source:`)
   - Skip §1 Snapshot and mark verdict "partial audit — text-only"
   - Rubric items 11 (mobile layout) and 12 (studio-quality feel) may be `?` instead of 0/1 — note this
   - AI Tells scan (§3) and detected style (§4) still work fully from CSS
   - Top 5 improvements (§5) still must follow the "concrete vs generic" rule
5. **Tool names**: Translate Claude Code tool names to Codex equivalents:
   - `Read` → `read_file` / view file via `codex` shell
   - `Edit` → `edit_file` / `apply_patch`
   - `Write` → `write_file`
   - `Glob` → search by pattern
   - `Grep` → grep / ripgrep
   - `Bash` → shell run

### When running in Claude Code

Use the full tool stack:
- `AskUserQuestion` for structured user input (supports multi-select, previews)
- `mcp__Claude_Preview__preview_start/screenshot/eval/inspect` for Step 5 visual loop
- `mcp__Claude_in_Chrome__*` (optional) for cross-browser verification on Revamp mode

## File entry points

- [skill.md](skill.md) — main instructions (read this first)
- [design-bible/styles/](design-bible/styles/) — 17 style references
- [design-bible/a11y/](design-bible/a11y/) — accessibility rules
- [design-bible/responsive/](design-bible/responsive/) — breakpoints
- [design-bible/components/](design-bible/components/) — 20 component refs
- [design-bible/frameworks/](design-bible/frameworks/) — 5 framework outputs
- [design-bible/industry/](design-bible/industry/) — 5 industry bundles
- [design-bible/motion/](design-bible/motion/) — motion language
- [design-bible/images/](design-bible/images/) — image strategy
- [design-bible/pages/](design-bible/pages/) — page templates
- [design-bible/critique/](design-bible/critique/) — 12-item self-validation rubric
- [design-bible/copy/](design-bible/copy/) — copy system (Mode 4)
- [design-bible/brand/](design-bible/brand/) — Brand DNA schema + 17-style signal matrix (Mode 5)
- [design-bible/audit/](design-bible/audit/) — Audit report template + "concrete vs generic" rule (Mode 6)
- [design-bible/examples/](design-bible/examples/) — 9 reference HTML pages
- [data/design-bible.json](data/design-bible.json) — compiled style + representative sites database

## Install

### Claude Code

```bash
# Clone repo
git clone https://github.com/thirdmannz/AI-Design-Master.git
cd AI-Design-Master

# Install as user skill
# macOS/Linux:
cp skill.md ~/.claude/skills/design.md

# Windows:
copy skill.md %USERPROFILE%\.claude\skills\design.md
```

Trigger with `/design` in any project.

### Codex

Option A — **project-local AGENTS.md**: copy this entire repo into your project root, codex auto-discovers `AGENTS.md`.

```bash
git clone https://github.com/thirdmannz/AI-Design-Master.git path/to/your-project/.design-master
# Then in your project AGENTS.md, link to .design-master/AGENTS.md or import skill.md
```

Option B — **standalone**: run codex in the cloned repo directory, then prompt:

```bash
cd AI-Design-Master
codex
# Then: "Read skill.md and run it. I want to design a new website."
```

Option C — **global codex memory**: paste `skill.md` content into codex's global instructions (`~/.codex/AGENTS.md` or equivalent).

### Other agents

Anything that supports Read/Edit/Write/Glob/Grep file ops can run this. Just point the agent at `skill.md` as the system prompt or initial instruction.

## Behavior contract

When invoked, the agent MUST:

1. Read `skill.md` end-to-end before responding
2. Detect platform (Claude Code with MCP / Claude Code without MCP / Codex / other) and pick appropriate fallback per "🔌 平台相容性" section of `skill.md`
3. Route to the correct Mode based on user intent: Mode 1 (new design) / Mode 2 (revamp) / Mode 3 (reverse) / Mode 4 (copy) / Mode 5 (brand-aware) / Mode 6 (audit)
4. Follow the Step 1 → 2 → 2.5 → 3 → 4 → 5 flow for new designs, R1 → R4 for revamps, B1 → B5 for brand-aware (then hand off to Mode 1 Step 2.5), A1 → A6 for audits
5. Run the AI Tells Blocklist self-check before any design output (Mode 1, 2, 5)
6. Run the Accessibility self-check (5 hard gates) before any design output
7. Output Variant A + Variant B (not single output) on first design pass for Mode 1 / Mode 5
8. Enter Refinement Loop (Step 4) after dual variants — token-level diffs only, do not regenerate full HTML, preserve brand-derived tokens across style switches
9. Run Visual Validation Loop (Step 5) (or text-only fallback) before final delivery for Mode 1 / Mode 5
10. For Mode 6 audit improvements: every entry in Top 5 improvements MUST be concrete (selector + measured state + diff + measurable impact) — generic phrasings are forbidden

## Failure modes to avoid

- ❌ Don't output AI-typical templates (pill button, subtitle pill hero, centered everything, 3-col features with lucide icons)
- ❌ Don't skip the dual-variant requirement
- ❌ Don't skip a11y self-check
- ❌ Don't claim visual validation pass without actually rendering (or without explicitly disclaiming "text-only critique, no render")
- ❌ Don't suggest gated styles (Glassmorphism / Aurora / Claymorphism / Bento) unless user explicitly asks for "AI / futuristic / glass" feel
- ❌ **Mode 5**: don't override `--radius-*` or `--shadow-*` from brand — those are style-identity tokens
- ❌ **Mode 5**: don't use brand colors as text without verifying WCAG AA contrast; if fails, follow the contrast fallback in [design-bible/brand/brand-extraction.md](design-bible/brand/brand-extraction.md) §4
- ❌ **Mode 6**: don't write generic improvements ("improve contrast", "modernize design") — every item must cite a real selector and a measurable delta
- ❌ **Step 4 refinement**: don't regenerate full HTML/CSS per refinement turn — only token-level diffs; don't re-run Step 5 visual loop per turn (only on final delivery); don't overwrite brand-derived tokens during cross-style switching
