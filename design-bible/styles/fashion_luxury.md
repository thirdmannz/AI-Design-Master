# 👗 Fashion / Luxury

> 大圖、極小字、all-caps tracking、不對稱排版、無 card、minimal nav。文字是配角、視覺是主角。適合時尚 / 精品 / 香水 / 珠寶 / 高端餐飲品牌。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Loewe](https://www.loewe.com) (manual)
- [Jacquemus](https://www.jacquemus.com) (manual)
- [Bottega Veneta](https://www.bottegaveneta.com) (manual)
- [Aesop](https://www.aesop.com) (manual)
- [Mansur Gavriel](https://www.mansurgavriel.com) (manual)
- [Khaite](https://www.khaite.com) (manual)
- [The Extraordinary Lab | GQ](https://www.gq.com/sponsored/story/the-extraordinary-lab) (awwwards)
- [Talent Management Agency in North America - Dulcedo - Dulcedo](https://dulcedo.com/) (awwwards)
- [atomicvibe Logo Archive 01](https://dribbble.com/shots/27332138-atomicvibe-Logo-Archive-01) (dribbble)
- [Mile Square Cafe Identity Design](https://dribbble.com/shots/27329616-Mile-Square-Cafe-Identity-Design) (dribbble)
- [Cportesano Cigars](https://dribbble.com/shots/27332668-Cportesano-Cigars) (dribbble)
- [PropTech CRM Dashboard — Partner Outreach & Deal Flow UI](https://dribbble.com/shots/27332795-PropTech-CRM-Dashboard-Partner-Outreach-Deal-Flow-UI) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #f5f1eb;
  --color-ink: #181614;
  --color-accent: #8b6f47;
  --color-rule: rgba(24,22,20,0.15);
  --font-display: "Saol Display", "GT Sectra Display", "Tiempos Headline", "Cormorant Garamond", serif;
  --font-body: "Söhne", "Inter Tight", "Helvetica Now", sans-serif;
  --font-size-display: clamp(4rem, 11vw, 12rem);
  --font-size-caption: 0.7rem;
  --letter-spacing-display: -0.03em;
  --letter-spacing-caption: 0.25em;
  --line-height-tight: 0.92;
  --radius-default: 0;
  --shadow-none: none;
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#f5f1eb",
      "ink": "#181614",
      "accent": "#8b6f47"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(255, 255, 255)  rgb(3, 3, 3)  rgb(74, 85, 104)  rgb(43, 46, 53)  rgb(247, 250, 252)  rgb(45, 55, 72)  rgb(26, 26, 26)  rgb(0, 0, 0)  rgb(197, 174, 121)  rgb(10, 10, 10)  oklch(0.446 0.03 256.802)  rgb(244, 244, 244)

---

## 字體配對

- **Display**: Cormorant Garamond 500 italic  /  **Body**: Inter Tight 400  — 輕奢經典
- **Display**: Saol Display  /  **Body**: Söhne 400  — 當代精品
- **Display**: Tiempos Headline 600  /  **Body**: Helvetica Now 400  — 雜誌精品感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Fashion / Luxury Hero -->
<section class="hero">
  <h1 class="hero-title">Your Headline</h1>
  <p class="hero-sub">Supporting copy that breathes.</p>
  <a href="#" class="btn-primary">Get Started</a>
</section>
```

```css
.hero {
  background: var(--color-bg);
  padding: var(--spacing-section) 5%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.hero-title {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 6vw, 7rem);
  color: var(--color-text-primary);
  letter-spacing: -0.03em;
  line-height: 1.05;
  max-width: 14ch;
}
.hero-sub {
  font-family: var(--font-body);
  color: var(--color-text-secondary);
  font-size: 1.125rem;
  margin-top: 1.5rem;
  max-width: 50ch;
}
.btn-primary {
  display: inline-flex;
  align-items: center;
  background: var(--color-accent);
  color: #fff;
  padding: 0.875rem 2rem;
  border-radius: var(--radius-md);
  font-family: var(--font-body);
  font-weight: 600;
  margin-top: 2.5rem;
  text-decoration: none;
  transition: var(--transition);
}
.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-glass, var(--shadow-card, 0 8px 24px rgba(0,0,0,0.15)));
}
```

---

## 讓設計不像 AI 生成的 3 個關鍵

1. 文字越少越好 — 一個 hero 可能只有 3-5 個字 + tiny caption
2. 全程不出現 button — CTA 是裸文字 + arrow（SHOP THE COLLECTION →）
3. 用 mix-blend-mode: difference 讓 caption 在不同底圖上自動可讀

---

## Accessibility 配方

**對比策略**：Tiny caption 容易因為小字 fail 對比 — 字 ≥ 11px 且對比 ≥ 7:1，不要把 fashion 美學犧牲可讀性。

**Focus state CSS（鍵盤焦點）**：
```css
*:focus-visible {
  outline: 1px solid var(--color-ink);
  outline-offset: 6px;
}
```

**通用要求**：
- 一頁只一個 `<h1>`，heading 階層不跳階
- 所有 `<img>` 有 `alt` 屬性
- 用 `<nav> <main> <section> <article>` 不用 `<div>` soup
- 必出 skip link（`<a href="#main" class="skip-link">Skip to content</a>`）
- Form input font-size ≥ 16px（避免 iOS auto-zoom）
- Touch target ≥ 44×44px

**參考文件**：
- [Contrast rules](../a11y/contrast-rules.md) — WCAG 對比要求
- [Semantic patterns](../a11y/semantic-patterns.md) — 元件 × HTML5 對照
- [ARIA patterns](../a11y/aria-patterns.md) — modal / tabs / menu 配方
- [Focus states](../a11y/focus-states.md) — 全 17 風格 focus CSS
- [Keyboard nav](../a11y/keyboard-nav.md) — 鍵盤導覽

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐⭐⭐ |
| 行銷落地頁 | ⭐ |
| 企業 / B2B | ⭐ |
| 媒體 / 內容 | ⭐ |
| 設計工作室 / Agency | ⭐⭐ |

**AI 視覺指紋強度**：✅ 低
