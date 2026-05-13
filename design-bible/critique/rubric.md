# Self-Critique Rubric

> 12 項評分。Skill 在 Step 5 (visual validation loop) 用這個 rubric 自評輸出。任 ≥ 3 項 fail → 進入自動修正迴路（max 3 cycles）。

## Scoring

每項 0 或 1：
- **1**：明確 pass
- **0**：明確 fail 或可疑

> **0.5 不允許** — 強迫做決定。

## Rubric

### 1. AI Tells Blocklist 全部 pass

| 對照 | Pass 條件 |
|------|---------|
| 主 CTA 不是 9999px pill | ✓ |
| Hero 沒有 subtitle pill `✨ New` | ✓ |
| Card 沒有預設 `backdrop-filter: blur`（除非 Glassmorphism） | ✓ |
| 沒有 gradient blob bg（除非 Aurora UI） | ✓ |
| 沒有 Inter + Lucide + slate-* 三件套 | ✓ |
| Hero 沒緊跟 Trusted-by logo cloud | ✓ |
| Features 不是 3-col card grid + lucide icon | ✓ |
| 不是全部置中對齊 | ✓ |
| `box-shadow: 0 2px 4px rgba(0,0,0,0.1)` 萬用 shadow 沒出現 | ✓ |
| Inter + Lucide + slate/gray-* 不是預設 | ✓ |

**任 1 條 fail → 整 rubric 第 1 項 fail。**

### 2. 風格 token 套用一致

- 所有 element 用 `var(--color-*)` 不直接寫 hex
- Font-family 用 `var(--font-display)` / `var(--font-body)`
- Radius 用 token (`--radius-*`)
- Spacing 不是隨機數字（用 scale）

### 3. Hero alignment 符合風格慣例

| 風格 | 期望 |
|------|------|
| Swiss / Magazine / Type-First / Brutalist / Fashion | left or asymmetric — **不可置中** |
| Aurora / Glassmorphism / Claymorphism | center 允許 |
| Corporate Clean / Editorial / Minimal Float | left preferred（但 center 不算 fail） |

### 4. 對比 WCAG AA pass

- Body text on bg ≥ 4.5:1
- Large text (≥18pt) on bg ≥ 3:1
- Accent on bg ≥ 3:1 (when used as text)
- Focus ring on bg ≥ 3:1

Tool: 用 axe-core or `mcp__Claude_Preview__preview_eval` 跑 contrast check。

### 5. 焦點狀態可見

- 所有 button / link / input / details / summary 有 `:focus-visible` CSS
- 沒有裸 `outline: none`（除非有替代）
- Tab 走完整頁，每 stop 看得到 focus

### 6. 元件選擇符合該風格禁出清單

| 風格 | 禁出 |
|------|------|
| Swiss Editorial | ❌ Card, ❌ Logo Cloud, ❌ Pill button |
| Magazine | ❌ Features 3-col grid, ❌ Trusted-by, ❌ CTA button |
| Fashion / Luxury | ❌ Card, ❌ Button pill, ❌ 置中 hero |
| Brutalist | ❌ box-shadow, ❌ border-radius, ❌ backdrop |
| Type-First | ❌ Features grid, ❌ Logo cloud, ❌ Icons |

Output 出現任一禁出 → fail。

### 7. 字體 hierarchy ≥ 3 階

- 至少 3 種字級可見（h1 / h2 / body）
- Font-weight 對比明顯
- Display vs body font 區別清楚

### 8. 留白比例符合風格

| 風格 | 期望 |
|------|------|
| Minimal Float / Swiss / Fashion / Editorial | section padding ≥ 8rem on desktop |
| Bento Grid / Corporate Clean | section padding 4-6rem |
| Brutalist | section padding 自由（可極小） |
| Magazine Longform | 大量 marginalia + reading column 留白 |

### 9. 顏色數量 ≤ 風格上限

| 風格 | 上限 |
|------|------|
| Swiss / Brutalist / Type-First / Fashion | 3 (bg + ink + 1 accent) |
| Corporate / Editorial / Minimal | 5 |
| Aurora / Glass | 7 (含 gradient stops) |
| Bento Grid | 5-8（多 surface variants） |
| Neobrutalism | 5-7（多 accent） |

數真實用到的顏色（不含 muted variations）。

### 10. Motion 符合風格

| 風格 | Motion 期望 |
|------|----------|
| Swiss / Brutalist | **無 motion** 或 instant cut |
| Aurora / Glass / Clay | spring / bounce |
| Kinetic | parallax / scroll-pinned |
| Type-First | letter-by-letter / scroll-driven type |
| 其他 | 短 transition (150-250ms) |

`prefers-reduced-motion` 必含。

### 11. Mobile layout 不 break

- 寬度 375px 可閱讀，無 horizontal scroll
- Touch target ≥ 44×44px
- Font ≥ 16px in inputs
- Nav 在 < 768px 有 mobile 解法（漢堡 / drawer）
- Hero 在 mobile 不爆字級

### 12. 整體像「真實工作室出品」

主觀但必判：
- 看起來像 Pentagram / Bureau Borsche / Vercel Design 那種出貨網站？
- 還是看起來像 v0 / Lovable / Cursor 預設模板？

**判斷句**：「這個輸出是否會被設計師同行誤認為 AI 生成？」是 → fail。

## Total scoring

- **12/12**：完美輸出
- **10-11/12**：可 ship，有 1-2 個 minor issue 可選擇修
- **9/12 以下**：必修，進入自動修正迴路

## 自動修正迴路

```
while (fail_count >= 3 && cycle < 3) {
  identify_failing_items()
  generate_minimal_patch()  // 只改 fail 的部分
  re_render()
  re_score()
  cycle++
}

if (cycle === 3 && fail_count >= 3) {
  output_partial + warn_user(
    "tried 3 refinement cycles, still failing on: [list]. " +
    "These may be inherent constraints. Manual review needed."
  )
}
```

## 輸出格式

```markdown
## 🎯 設計驗證報告

| # | 項目 | 結果 | 備註 |
|---|------|------|------|
| 1 | AI Tells Blocklist | ✅ | 全 10 條 pass |
| 2 | Token 一致性 | ✅ | — |
| 3 | Hero alignment | ✅ | left-aligned 符合 Swiss |
| 4 | WCAG AA contrast | ⚠️ | body 4.6:1（接近邊界），建議深 1 階 ink |
| 5 | Focus visible | ✅ | — |
| 6 | 風格禁出清單 | ✅ | 無 Card / Logo Cloud |
| 7 | 字體 hierarchy | ✅ | 3 階清楚 |
| 8 | 留白比例 | ✅ | section padding 10rem |
| 9 | 顏色數量 | ✅ | 3 色（bg + ink + accent） |
| 10 | Motion | ✅ | 標註「無 motion」 |
| 11 | Mobile layout | ✅ | 375px 通過 |
| 12 | 工作室感 | ✅ | 不像 AI 模板 |

**總分：11/12（1 個 warning）**

**建議修正**：
- 把 `--color-ink` 從 `#1a1a1a` 改 `#0a0a0a` 提升 contrast 到 7:1
```

---

# Performance Gates (M7 — Step 5.4b 用)

> 12 項 rubric 是 **靜態可判** 的視覺 + a11y 評分。Performance Gates 是 **runtime 量測**,跑 Step 5.4b 時用 Chrome MCP 在 rendered page 上採集真實數據。
> 兩者分開記分:rubric 給「設計是否好」,gates 給「設計是否能 ship」。

## 5 個 gates

| # | 指標 | 預設 budget | 量測方式 |
|---|------|------------|---------|
| P1 | LCP (Largest Contentful Paint) | < 2.5s | `PerformanceObserver` on `largest-contentful-paint` |
| P2 | CLS (Cumulative Layout Shift) | < 0.1 | `PerformanceObserver` on `layout-shift`,加總 sources without recent input |
| P3 | FCP (First Contentful Paint) | < 1.8s | `performance.getEntriesByType('paint')` filter `first-contentful-paint` |
| P4 | TBT proxy (long tasks > 50ms) | total < 200ms | `PerformanceObserver` on `longtask`,加總 duration |
| P5 | Total transfer weight | < 500 KB | `performance.getEntriesByType('resource')` 加總 `transferSize` |

**Budget 來源優先級**:
1. `.design-master/design-system.json` 的 `performance_budget`(若存在)
2. 上表預設值(若 manifest 沒設或 manifest 不存在)

## 量測 script(在 rendered page eval)

```javascript
async function measurePerf() {
  return new Promise((resolve) => {
    const result = { lcp: null, cls: 0, fcp: null, tbt: 0, weight_kb: 0 };

    // FCP
    const fcpEntry = performance.getEntriesByType('paint').find(e => e.name === 'first-contentful-paint');
    if (fcpEntry) result.fcp = fcpEntry.startTime / 1000;

    // LCP — observe and finalize on visibility change or after 3s
    new PerformanceObserver((list) => {
      const entries = list.getEntries();
      result.lcp = entries[entries.length - 1].startTime / 1000;
    }).observe({ type: 'largest-contentful-paint', buffered: true });

    // CLS
    new PerformanceObserver((list) => {
      for (const entry of list.getEntries()) {
        if (!entry.hadRecentInput) result.cls += entry.value;
      }
    }).observe({ type: 'layout-shift', buffered: true });

    // TBT (long tasks during load)
    new PerformanceObserver((list) => {
      for (const entry of list.getEntries()) {
        result.tbt += Math.max(0, entry.duration - 50);
      }
    }).observe({ type: 'longtask', buffered: true });

    // Total transfer weight
    result.weight_kb = performance.getEntriesByType('resource')
      .reduce((sum, r) => sum + (r.transferSize || 0), 0) / 1024;

    // Allow async observers to finalize
    setTimeout(() => resolve(result), 3000);
  });
}
return await measurePerf();
```

## Auto-fix mapping(fail 時建議)

| Gate fail | 建議 fix |
|-----------|---------|
| LCP > 2.5s | preload hero image (`<link rel="preload" as="image" fetchpriority="high">`)、inline critical CSS、移除阻塞 above-the-fold 的 script、用 `<picture>` + avif/webp |
| CLS > 0.1 | 給 `<img>` / `<video>` 設定 explicit `width` + `height` 屬性、為 ads / embeds 預留位、用 `font-display: optional` 或 preload font 避免字體切換時跳動 |
| FCP > 1.8s | 減少阻塞的 CSS(inline critical CSS 餘下 lazy)、preload key fonts、用 `font-display: swap`、移除 above-the-fold blocking JS |
| TBT > 200ms | defer 非 critical JS(`<script defer>` 或 `type="module"`)、code-split、考慮較輕的 framework、避免主執行緒長任務 |
| Weight > 500 KB | 找出最大的 3 個 resources(從 `performance.getEntriesByType('resource')` 排序)、image 換 avif/webp、檢查 fonts 是否載多餘字重、tree-shake JS |

## 輸出格式

```markdown
## ⚡ Performance Gates

| # | 指標 | 量測 | Budget | 結果 |
|---|------|------|--------|------|
| P1 | LCP | 2.1s | < 2.5s | ✅ |
| P2 | CLS | 0.04 | < 0.1 | ✅ |
| P3 | FCP | 1.3s | < 1.8s | ✅ |
| P4 | TBT | 80ms | < 200ms | ✅ |
| P5 | Weight | 312 KB | < 500 KB | ✅ |

**Performance verdict: ✅ PASS (5/5 gates)**
```

或 fail 時:

```markdown
| P1 | LCP | 3.4s | < 2.5s | ❌ |
| P5 | Weight | 820 KB | < 500 KB | ❌ |

**Performance verdict: ❌ FAIL (3/5 gates)**

### 建議修正
- **LCP 3.4s → < 2.5s**: hero image (380 KB JPEG) 是 LCP element。建議:
  ```html
  <link rel="preload" as="image" fetchpriority="high" href="/hero.avif" type="image/avif">
  <picture>
    <source srcset="/hero.avif" type="image/avif">
    <source srcset="/hero.webp" type="image/webp">
    <img src="/hero.jpg" alt="..." width="1280" height="720">
  </picture>
  ```
  預估 LCP 改善 ~1.2s

- **Weight 820 KB → < 500 KB**: 3 個最大 resources:
  1. hero.jpg (380 KB) → 換 avif (~80 KB)
  2. analytics.js (210 KB) → defer 或換輕量替代
  3. icons.css (80 KB) → tree-shake 未用 icon
```

## 與 12-item rubric 的關係

- 12-item rubric 是「設計品質」門檻 — ≥9/12 才能 ship
- Performance Gates 是「商業可上線」門檻 — 5/5 才能 ship
- **兩者獨立** — 一個視覺滿分(12/12)的設計可能 LCP 4s 不能 ship;一個 LCP 1s 的設計可能視覺 4/12 也不能 ship
- Step 5 自動修正迴路同時看兩者:**任一不過就進入修正**

## Codex / no-MCP fallback

Performance gates 需要 rendered page + Chrome runtime API。Codex / 無 Chrome MCP 時:
- 跳過 5.4b,在 Step 5 報告標注「Performance gates skipped — no Chrome MCP」
- 不 block 交付 — 設計部分仍可 ship,但提醒 user 自己在瀏覽器跑 Lighthouse 驗一次

