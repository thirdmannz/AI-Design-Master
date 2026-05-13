# Design System Manifest — Schema & Lifecycle

> M7 reference. The manifest is `.design-master/design-system.json` in the user's project. It is the single source of truth for the locked design system across sessions.

This file defines the schema, the lifecycle rules, and the lock/unlock semantics. The skill.md flow describes *when* to read/write it; this file describes *what* it looks like and *how* it behaves.

---

## 1. File location

```
<user-project-root>/
  .design-master/
    design-system.json   ← THIS FILE — single source of truth
    exports/             ← Token export adapter outputs (regenerable)
    pages/               ← Multi-page generation outputs (regenerable)
```

The skill writes `.design-master/design-system.json` at Mode 1 / Mode 5 Step 4.6 (final delivery) and updates it on every subsequent refinement turn. The folder lives at the user's project root, NOT in the skill's own directory.

---

## 2. Schema (v1.0)

```json
{
  "version": "1.0",
  "skill_version": "M7",
  "locked": true,
  "locked_at": "2026-05-13T14:32:00Z",
  "updated_at": "2026-05-13T15:10:00Z",
  "project_name": "acme-saas",

  "design": {
    "style": "swiss_editorial",
    "applied_constraints": ["no-rounded-corners", "no-card-shadows", "strict-grid"],
    "framework": "react-tailwind",
    "industry": "saas",
    "tokens": {
      "--color-bg": "#ffffff",
      "--color-ink": "#0A2540",
      "--color-accent": "#635BFF",
      "--color-rule": "rgba(10,37,64,0.12)",
      "--font-display": "\"Söhne Breit\", \"Inter Tight\", sans-serif",
      "--font-body": "\"Söhne\", \"Inter Tight\", sans-serif",
      "--font-mono": "\"JetBrains Mono\", monospace",
      "--letter-spacing-display": "-0.04em",
      "--font-weight-body": "400",
      "--font-weight-display": "700",
      "--radius-default": "0",
      "--shadow-none": "none",
      "--grid-cols": "12",
      "--grid-gap": "1.5rem",
      "--baseline": "8px",
      "--space-section": "8rem",
      "--line-height-body": "1.6",
      "--motion-duration": "0",
      "--motion-easing": "linear"
    },
    "tokens_provenance": {
      "--color-accent": "brand",
      "--color-ink": "brand",
      "--color-bg": "style-default",
      "--font-display": "style-default",
      "--radius-default": "style-default"
    }
  },

  "brand_dna": {
    "palette": [
      { "hex": "#0A2540", "role": "ink", "source": "user-provided-hex" },
      { "hex": "#635BFF", "role": "accent", "source": "logo" }
    ],
    "typography_lean": "sans",
    "weight_preference": "normal",
    "density": "airy",
    "formality": "corporate",
    "motion_vibe": "subtle-ease"
  },

  "version_log": [
    {
      "v": "v1",
      "intent": "Initial Variant A",
      "changes": [],
      "ts": "2026-05-13T14:00:00Z"
    },
    {
      "v": "v2",
      "intent": "make it bolder",
      "changes": [
        "--font-weight-body: 400 -> 600",
        "--font-weight-display: 700 -> 900",
        "--letter-spacing-display: -0.04em -> -0.05em"
      ],
      "ts": "2026-05-13T14:15:00Z"
    },
    {
      "v": "v3",
      "intent": "more whitespace",
      "changes": ["--space-section: 6rem -> 8rem"],
      "ts": "2026-05-13T14:32:00Z"
    }
  ],
  "current_version": "v3",

  "performance_budget": {
    "lcp_seconds": 2.5,
    "cls": 0.1,
    "fcp_seconds": 1.8,
    "tbt_ms": 200,
    "total_weight_kb": 500
  },

  "pages": ["index", "pricing", "about"],

  "audit_history": [
    {
      "ts": "2026-05-13T15:00:00Z",
      "rubric_score": 11,
      "ai_tells_index": 1,
      "perf_pass": true
    }
  ]
}
```

### Field rules

| Field | Required | Notes |
|---|---|---|
| `version` | yes | Schema version. Bump on breaking changes. |
| `skill_version` | yes | The skill release that wrote this file (M7, M8, …). |
| `locked` | yes | `true` = active source of truth; `false` = historical reference. |
| `locked_at` / `updated_at` | yes | ISO 8601 UTC. `locked_at` is set once on first write; `updated_at` on every save. |
| `project_name` | no | Free text, defaults to the project folder name. |
| `design.style` | yes | One of the 17 style IDs from [design-bible/styles/](../styles/). |
| `design.applied_constraints` | yes | Array of constraint IDs (see Step 2.5 in skill.md). Empty array allowed. |
| `design.framework` | yes | `react-tailwind` / `vue-tailwind` / `svelte` / `astro` / `html-css`. |
| `design.industry` | no | Industry bundle ID if Step 1 captured one. |
| `design.tokens` | yes | Final token state at `current_version`. Keys are CSS custom property names. |
| `design.tokens_provenance` | yes | Per-token: `brand` / `style-default` / `user-override`. Drives Step 4.3b cross-style preservation. |
| `brand_dna` | no | Mode 5 schema; `null` if Mode 5 was not used. |
| `version_log` | yes | Append-only. Never delete entries — `revert to v2` adds a new entry, doesn't remove. |
| `current_version` | yes | Pointer into `version_log`. |
| `performance_budget` | no | Defaults applied if absent (see §5). |
| `pages` | no | Mode 7 multi-page output list. Empty if single-page only. |
| `audit_history` | no | Mode 6 audit results when audit was run against this project's own site. |

---

## 3. Lifecycle

### 3a. First write (Mode 1 / Mode 5 Step 4.6)

After the user accepts the final design (Step 4.6 final delivery), the skill writes the manifest:

1. Compose the schema from the in-session state (chosen style, constraints, current token state, brand DNA if Mode 5 was used, full version log).
2. `locked: true`, `locked_at: <now>`, `updated_at: <now>`.
3. Write to `<project-root>/.design-master/design-system.json`.
4. Surface to user:
   ```
   🔒 Design system locked → .design-master/design-system.json
   Future /design runs in this project will pick up where you left off.
   ```

### 3b. Subsequent invocation in same project

Before the mode router runs, check for `.design-master/design-system.json`:

- **Found + `locked: true`** → load and surface:
  ```
  Detected locked design system: Swiss Editorial (v3, locked 2026-05-13)
    Tokens: 18 (3 brand-derived) · Brand DNA: present
    Last refinement: "more whitespace"

  Continue?
    1. Refine further (loads v3, you can do v4, v5, ...)
    2. Audit current site against locked tokens (Mode 6 with drift detection)
    3. Generate more pages (Mode 7 multi-page)
    4. Export tokens to Figma / Style Dictionary
    5. Unlock and pick a fresh style
  ```
- **Found + `locked: false`** → load as historical reference, surface:
  ```
  Found an unlocked design system from [date]. Reference only — pick a fresh path.
  ```
- **Not found** → normal mode router (Mode 1 / 2 / 3 / 4 / 5 / 6 / 7 selection).

### 3c. Refinement updates (Step 4)

Every Step 4 turn:
1. Apply the token diff (Step 4.3) or cross-style diff (Step 4.3b)
2. Append a new entry to `version_log`
3. Update `current_version` to the new v
4. Update `design.tokens` to the new state
5. Update `tokens_provenance` if any token's provenance changed (e.g. cross-style switch reassigned some `style-default` tokens to new style defaults)
6. Update `updated_at`
7. Overwrite the file

### 3d. Revert

User says "revert to v2":
1. Take a snapshot of `design.tokens` at v2 (replay version_log entries v1 → v2)
2. Add a NEW entry to `version_log` with `intent: "Revert to v2 snapshot"` and `changes: <delta from current to v2>`
3. Set `current_version` to the new entry's v
4. Save

Never delete history. Revert is a new entry, not an undo.

### 3e. Mode 6 (Audit) of own project

When Mode 6 runs against a URL/path that matches this project AND a manifest exists:
1. Run normal audit (rubric, AI Tells, detected style, top 5 improvements)
2. **Add a "Token drift" section** to the audit report:
   - Compare each token in `design.tokens` to the live computed value
   - List drifts: which tokens are different, what the live value is, what the manifest expects
   - Suggest a "sync" patch
3. Append a new entry to `audit_history`

### 3f. Mode 2 (Revamp)

When the project being revamped already has a locked manifest:
1. Treat the manifest's `design.tokens` as the **target design system** for the revamp
2. Skip R3 (recommend target style) — already locked
3. Go straight to R4 (migration guide) using manifest tokens

### 3g. Unlock

User says "解鎖" / "unlock the design system":
1. Set `locked: false`
2. Update `updated_at`
3. Save
4. Confirm:
   ```
   Design system unlocked. The file is kept as historical reference at
   .design-master/design-system.json. Next /design run will pick fresh.
   ```

---

## 4. .gitignore policy

The manifest itself (`design-system.json`) **should be committed** so teammates inherit the locked system. Generated artifacts should be ignored:

```gitignore
# Recommended for .design-master/
.design-master/exports/    # Regenerable from manifest
.design-master/pages/      # Regenerable from manifest
# .design-master/design-system.json  # Commit this — it's the source of truth
```

The skill *suggests* this but does not enforce — at first write, surface a one-liner: "Recommendation: commit `.design-master/design-system.json`, gitignore `exports/` and `pages/`." User can override.

---

## 5. Default values

If `performance_budget` is absent or partial, apply these defaults:

```json
{
  "lcp_seconds": 2.5,
  "cls": 0.1,
  "fcp_seconds": 1.8,
  "tbt_ms": 200,
  "total_weight_kb": 500
}
```

If `tokens_provenance` is absent (e.g. manifest from non-Mode-5 flow), default every entry to `style-default`.

---

## 6. Migration / schema evolution

When skill releases bump the schema (e.g. M8 adds `motion_budget`):
1. Read the existing `version` field
2. If `version` < target schema version, run a migration that adds missing fields with defaults
3. Update `version` and `skill_version`
4. Save

Never delete unknown fields — a forward-compat skill release might have added them.

---

## 7. Why a single file (not a folder of files)

One file is easier to:
- Read atomically in one tool call
- Write atomically (single-file `Write` tool)
- Diff in git
- Inspect manually

The structured `design.tokens` + `version_log` + `brand_dna` blocks keep the file readable up to ~500 lines even for heavily-iterated projects.

If the file ever exceeds ~1MB (extreme version_log accumulation), suggest a "compact" command that collapses the version_log to the last 10 entries plus a summary of older history.
