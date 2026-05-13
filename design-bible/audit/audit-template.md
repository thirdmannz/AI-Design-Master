# Design Audit Report Template

> Mode 6 reference. Defines the exact structure of an audit deliverable, the scoring rules, and the rule of "concrete vs generic" for improvement suggestions.

This is the template Mode 6 fills in. The 12-item rubric in [design-bible/critique/rubric.md](../critique/rubric.md) and the AI Tells Blocklist in [skill.md](../../skill.md) are both reused verbatim — this file does not redefine them.

---

## When Mode 6 produces this report

Mode 6 A1 fetched the page. A2 extracted signals (palette / typography / layout / motion / a11y). A3 ran the rubric. A4 ran the AI Tells Blocklist. A5 fills this template. A6 lets the user re-run after applying fixes.

---

## Report structure (exact section order)

```markdown
# 🎯 Design Audit — [URL or "Pasted HTML"]

**Date**: [YYYY-MM-DD]
**Verdict**: ✅ PASS (≥9/12) | ⚠️ MARGINAL (7–8/12) | ❌ FAIL (≤6/12)
**Headline**: [one sentence summary, e.g. "Solid layout undermined by 4 AI Tells and a contrast failure."]

---

## 1. Snapshot

[mobile screenshot 375×667]    [tablet 768×1024]    [desktop 1280×800]

If no Chrome MCP / Preview MCP available: skip this section, note "Visual snapshots unavailable — text-only audit."

---

## 2. Rubric scorecard (12 items)

| # | Item | Score | Note |
|---|---|---|---|
| 1 | AI Tells Blocklist | 0 or 1 | "4 of 10 patterns hit — see §3" |
| 2 | Token consistency | 0 or 1 | "Hex literals scattered — no CSS custom properties detected" |
| 3 | Hero alignment vs style | 0 or 1 | "Centered hero on inferred Swiss Editorial style — fail" |
| 4 | WCAG AA contrast | 0 or 1 | "Body text 3.8:1 on #f8f8f8 — fails AA" |
| 5 | Focus visible | 0 or 1 | "Naked `outline: none` on .btn, no replacement" |
| 6 | Forbidden components for style | 0 or 1 | "Features 3-col card grid present despite Magazine inferred style" |
| 7 | Typography hierarchy ≥3 | 0 or 1 | "h1, h2, body — pass" |
| 8 | Whitespace fits style | 0 or 1 | "Section padding 32px desktop — too tight for Swiss" |
| 9 | Color count ≤ style cap | 0 or 1 | "11 distinct colors — exceeds Swiss cap of 3" |
| 10 | Motion fits style | 0 or 1 | "Scroll parallax on Swiss-inferred page — fail" |
| 11 | Mobile layout OK | 0 or 1 | "Horizontal scroll at 375px on .hero" |
| 12 | Studio-quality feel | 0 or 1 | "Reads as v0/Lovable output — fail" |

**Total: X/12**

---

## 3. AI Tells findings

For each pattern from the 10-item Blocklist that the audited page hits:

```
### Hit #1 — Pill button (#1 in Blocklist)

**Where**: `.btn-primary` at body > main > section.hero > button:nth-child(2)
**Evidence**: `border-radius: 9999px` (computed)
**Severity**: ⛔⛔⛔
**Fix**: Change to `border-radius: 4px` (or `var(--radius-default)` if a token exists). Pill is only allowed when the inferred style is Claymorphism.
```

If no AI Tells hit: write "✅ 0/10 — page does not trip any blocklist pattern." and skip to §4.

**AI Tells Index: X/10** (count of distinct hits)

---

## 4. Detected style

Reuse the Mode 3 V2 signal matrix to identify the page's closest style match.

```
**Most likely**: [Style Name] (confidence X/10)
**Second**: [Style Name] (confidence X/10)

### Signals
- [Signal 1]: [observed evidence]
- [Signal 2]: [observed evidence]
- [Signal 3]: [observed evidence]
```

This drives §2 item 3 (hero alignment), §2 item 6 (forbidden components), §2 item 9 (color cap), §2 item 10 (motion fit).

---

## 5. Top 5 concrete improvements

⚠️ **Concrete, not generic.** Each improvement must:
- Name the specific element/selector on this page
- Show a before/after CSS snippet using the page's own class names
- State the expected measurable impact (contrast delta, AI Tells removed, etc.)

Bad example (generic — do not write):
> "Improve color contrast on body text."

Good example (concrete):
> **#1 — Raise body text contrast to AA**
> **Element**: `.article-body p` (computed `color: #888` on `background: #ffffff`)
> **Current contrast**: 3.5:1 (fails AA)
> **Fix**:
> ```diff
> .article-body p {
> -  color: #888;
> +  color: #4a4a4a;
> }
> ```
> **New contrast**: 9.7:1 (AAA). Affects ~340 paragraph nodes across blog/index pages.

Output exactly **5** improvements, ranked by impact. If fewer than 5 exist (page is in good shape), output only as many as are warranted and say so.

---

## 6. Optional: improved-version snippet

If the audit identifies fixes that can be packaged as a drop-in patch (typically 5–20 lines of CSS), include them at the end as a single block the user can paste:

```css
/* Drop-in fixes for [URL]. Apply after existing styles. */
.btn-primary { border-radius: 4px; }       /* removes pill — Blocklist #1 */
.article-body p { color: #4a4a4a; }         /* contrast 3.5:1 → 9.7:1 */
.hero { text-align: left; }                 /* hero alignment matches Swiss */
```

Skip this section if fixes require structural changes (HTML restructuring) that can't be expressed as a CSS append.

---

## 7. Re-audit instruction

> Apply the fixes and re-run this audit with `paste-improved` mode to confirm the rubric score improved.

```

---

## Scoring rules (strict)

1. **Each rubric item is 0 or 1.** Half-credit forbidden, same as Step 5 self-critique.
2. **Verdict thresholds**:
   - **≥9** → PASS (ship-worthy)
   - **7–8** → MARGINAL (works but improvable)
   - **≤6** → FAIL (needs work)
3. **AI Tells Index is separate from the rubric** — it's an additional metric, 0–10. A page can have AI Tells = 0/10 and still score badly on rubric (e.g. broken contrast), and vice versa.
4. **Style detection drives several rubric items.** If style detection has confidence <5/10, flag the rubric verdict as low-confidence and give the user two readings (one per likely style).

---

## "Concrete vs generic" rule (for §5)

Every improvement entry must contain:

1. A **CSS selector or DOM path** that exists on the audited page (not "buttons" — name the class)
2. A **measured current state** (computed value, ratio, count)
3. A **diff** with the page's actual class names
4. An **expected impact** that's measurable (ratio number, count of removed Blocklist hits, etc.)

If you cannot fill all four, the improvement isn't ready. Either dig deeper into the DOM or drop it from the top 5.

Forbidden generic phrasings:
- "Improve contrast" — say which selector, what current ratio, what target
- "Use better fonts" — say which font, why, and the replacement
- "Simplify the layout" — say which section, what to remove or reorganize
- "Modernize the design" — refuse to write this; it's not actionable

---

## Codex / no-MCP fallback (Mode 6 A1)

When Chrome MCP and Preview MCP are unavailable:

1. Ask the user to paste the rendered HTML + the CSS (or a link to a `view-source:` if they can fetch it).
2. Skip §1 Snapshot. Note explicitly: "Visual snapshots unavailable — text-only audit."
3. Skip §2 rubric items that require visual rendering: item 11 (mobile layout — partial, can still infer from breakpoints in CSS) and item 12 (studio-quality feel — partial, infer from token structure + class names). Mark these `?` instead of 0/1.
4. Still run §3 AI Tells (purely from CSS), §4 style detection (from CSS + DOM), and §5 improvements.
5. State the partial-audit caveat in the verdict line.

The audit is still useful in text-only mode — just less complete.

---

## Self-audit sanity check

Before delivering the report, the skill should run the rubric on its own example pages in [design-bible/examples/](../examples/) once. Every reference example must score ≥10/12. If any example scores below that, the rubric or the example is broken — fix before shipping the skill update.
