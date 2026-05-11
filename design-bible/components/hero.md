# Hero

> 頁面進入區。承載主要 value prop + primary CTA。AI 最常產出失敗版（置中三件套 + subtitle pill + 3 column features 緊跟）— 看 [AI Tells Blocklist](../../skill.md#-ai-tells-blocklist最高優先級硬性禁令)。

## Anatomy

- `<h1>` headline（**一頁只一個 h1**）
- Subtitle / lede（解釋 headline）
- Primary CTA（1 個，不要兩個競爭）
- 可選：secondary link / 視覺元素

## Canonical HTML (semantic)

```html
<section class="hero" aria-labelledby="hero-title">
  <h1 id="hero-title">Build software, faster.</h1>
  <p class="hero-lede">A single platform for shipping production code from idea to deploy.</p>
  <a href="/start" class="btn-primary">Start free</a>
</section>
```

> 注意：**沒有** subtitle pill (`<span class="pill">✨ New</span>`)。AI tell #2。

## Canonical CSS (Mobile-first, 3 breakpoints)

```css
.hero {
  padding: 4rem 1.25rem;
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  align-items: flex-start; /* 預設左對齊，不要置中 */
}
.hero h1 {
  font-family: var(--font-display);
  font-size: clamp(2.25rem, 8vw, 3.5rem);
  line-height: 1.05;
  letter-spacing: -0.025em;
  max-width: 18ch;
  margin: 0;
}
.hero-lede {
  font-family: var(--font-body);
  font-size: 1.0625rem;
  line-height: 1.5;
  color: var(--color-muted);
  max-width: 52ch;
}
@media (min-width: 768px) {
  .hero { padding: 6rem 2rem; gap: 1.5rem; }
}
@media (min-width: 1024px) {
  .hero {
    padding: 8rem 4rem;
    min-height: 80vh;
    justify-content: center;
  }
  .hero h1 { font-size: clamp(3rem, 6vw, 6rem); }
}
```

## 風格輸出對照（17 styles）

| Style | 對齊 | CTA 形式 | 視覺元素 | 禁用 |
|-------|------|---------|---------|------|
| Corporate Clean | left or split | rounded button | optional illustration right | — |
| Editorial Maximal | left + asymmetric grid | underline link | optional masthead | features grid 緊跟 |
| Minimal Float | left, huge whitespace | text link 或 outline button | none | gradient blob |
| Bento Grid | 整 hero 本身是 bento cell | inline link | bento blocks 包圍 | 三件套 |
| Dark Luxury | center 允許（用 gold accent） | gold outline | photo bg | bright accent |
| Aurora UI | center 允許（必須 user 主動指名） | gradient button 解鎖 | aurora gradient bg | — |
| Glassmorphism | center 允許 | pill 解鎖 | glass card overlay | — |
| Claymorphism | left or center | clay button | claystyle illustration | — |
| Neobrutalism | left | block button hard shadow | bold geometric | smooth gradient |
| Organic Nature | left | rounded button | organic blob | hard shadow |
| Kinetic Editorial | left, scroll-pinned | underline link | animated masthead | static layout |
| 3D Immersive | overlay on 3D scene | minimal floating button | full canvas | flat hero |
| **Swiss Editorial** | **left, grid-aligned** | **underline link, no button** | **kicker + dateline** | ❌ button, ❌ subtitle pill |
| **Magazine Longform** | **left, columned** | **underline link** | **kicker + masthead + drop cap** | ❌ button, ❌ pill |
| **Fashion / Luxury** | **asymmetric, big photo** | **tiny ALL-CAPS link** | **full-bleed photo** | ❌ button, ❌ centered |
| **Brutalist** | **default left, no padding** | **default underline link** | **no styling** | ❌ all decoration |
| **Type-First Monochrome** | **left, bleed past viewport** | **underline link only** | **oversized typography** | ❌ icons, ❌ button |

## Accessibility 必查

- [ ] `<h1>` 只一個，是 hero title
- [ ] CTA 用 `<a>`（跳頁）或 `<button>`（觸發 JS），不用 `<div onclick>`
- [ ] Hero 圖片有 `alt`（裝飾性 `alt=""`）
- [ ] CTA focus-visible 對 bg ≥ 3:1
- [ ] Touch target ≥ 44×44px
- [ ] 文字對 bg ≥ 4.5:1（深色 hero 用 photo bg 時加 backdrop overlay）

## 框架轉換重點

| Framework | 寫法 |
|-----------|------|
| React + Tailwind | `<section className="px-5 py-16 md:px-8 md:py-24 lg:px-16 lg:py-32 flex flex-col items-start gap-5">` + composable `<Hero.Title>` `<Hero.CTA>` |
| Vue + Tailwind | `<script setup>` + `<section>` + slot props 給 title/lede/cta |
| Svelte | `<script>` props + `<section class:asymmetric>` directive |
| Astro | `.astro` static render，CTA 用 `<a>` 不需 hydration |
| HTML + CSS | 直接 semantic HTML + CSS Custom Properties |

## AI Tell 自查（必跑）

- [ ] 沒有 subtitle pill（`✨ New feature` style）
- [ ] 沒有「兩個 button 並排」（一個 primary + 一個 secondary）— 只能一個 primary CTA
- [ ] 沒有「Hero 緊跟 Trusted by」（必須中間有 section spacing 或別的內容）
- [ ] 沒有「placeholder gradient bg」（除非選了 Aurora）
- [ ] 不是全置中（左對齊或非對稱優先）
