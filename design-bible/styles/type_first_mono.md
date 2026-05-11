# 🅰️ Type-First Monochrome

> 排版做所有 hierarchy，單色 + 巨大字級 bleed，零 gradient/glass/shadow。是當代頂級工作室最常用的「不裝飾」策略。適合 design-savvy SaaS、AI 產品、設計師 portfolio、創意工具。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [MSCHF](https://mschf.com) (manual)
- [Readymag](https://readymag.com) (manual)
- [Linear](https://linear.app) (manual)
- [Vercel Design](https://vercel.com/design) (manual)
- [Stripe Press](https://press.stripe.com) (manual)
- [Framer](https://www.framer.com) (manual)
- [Figma Design Systems](https://www.figma.com/design-systems) (manual)
- [Home | Traffic Productions](https://www.traffic.productions/?ref=godly) (godly)
- [SILENCIO ® VISUAL LANGUAGES](https://silencio.es/?ref=godly) (godly)
- [Site Not Found | Framer](https://haptic.app/?ref=godly) (godly)
- [KidSuper World](https://kidsuper.world/?ref=godly) (godly)
- [SavoirFaire©. Holistic creative studio based in NYC.](https://savoirfaire.nyc/?ref=godly) (godly)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #fafaf7;
  --color-ink: #0a0a0a;
  --color-accent: #2c5fff;
  --color-rule: rgba(10,10,10,0.1);
  --font-display: "Inter Tight", "Söhne", "GT Walsheim", system-ui, sans-serif;
  --font-body: "Inter", "Söhne", system-ui, sans-serif;
  --font-mono: "JetBrains Mono", monospace;
  --font-size-display: clamp(5rem, 14vw, 16rem);
  --font-size-h1: clamp(2.5rem, 5vw, 4.5rem);
  --font-size-body: 1.0625rem;
  --letter-spacing-display: -0.045em;
  --line-height-tight: 0.9;
  --radius-default: 0;
  --radius-image: 4px;
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
      "bg": "#fafaf7",
      "ink": "#0a0a0a",
      "accent": "#2c5fff"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(21, 21, 21)  rgb(243, 243, 243)  rgb(255, 255, 255)  rgb(0, 0, 0)  rgb(219, 218, 217)  rgb(222, 222, 221)  rgb(255, 255, 255)  rgb(0, 0, 0)  rgb(51, 51, 51)  rgb(255, 255, 255)  rgb(0, 0, 0)  rgba(255, 255, 255, 0.9)

---

## 字體配對

- **Display**: Inter Tight 800  /  **Body**: Inter 400  — 當代 design-tool 標準
- **Display**: GT Walsheim 700  /  **Body**: GT Walsheim 400  — 統一家族，high contrast
- **Display**: Söhne Breit  /  **Body**: Söhne  — 頂級工作室語言

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Type-First Monochrome Hero -->
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

1. 不用 icon — 用排版（字級對比 + 字距 + 顏色）做 hierarchy
2. 整站只有 1 個 accent 色，只用在 link hover 跟 highlighter — 不用在大面積背景
3. Display 字級故意 bleed 出 viewport（margin-left: -2vw）— AI codegen 永遠把字塞在 container 內

---

## Accessibility 配方

**對比策略**：Mono palette 對比天然高。Accent 只用在 link，underline + accent 雙重 cue。

**Focus state CSS（鍵盤焦點）**：
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 4px;
}
a:focus-visible {
  text-decoration: underline;
  text-decoration-thickness: 2px;
  text-underline-offset: 4px;
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
| SaaS / 科技產品 | ⭐⭐⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐ |
| 行銷落地頁 | ⭐⭐⭐ |
| 企業 / B2B | ⭐⭐⭐ |
| 媒體 / 內容 | ⭐⭐⭐ |
| 設計工作室 / Agency | ⭐⭐⭐ |

**AI 視覺指紋強度**：✅ 低
