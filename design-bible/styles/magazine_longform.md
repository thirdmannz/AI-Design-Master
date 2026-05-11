# 📰 Magazine Longform

> dateline + kicker + lede + drop cap，serif/sans 對比，真實攝影 + 邊註。看起來像紙本雜誌的數位版。適合媒體網站、深度報導、產品 launch story、品牌故事。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [The Pudding](https://pudding.cool) (manual)
- [Pitchfork Features](https://pitchfork.com/features) (manual)
- [The Atlantic](https://www.theatlantic.com) (manual)
- [NYT Interactive](https://www.nytimes.com/interactive) (manual)
- [Harper's Magazine](https://harpers.org) (manual)
- [CHRISTOPHER IRELAND CREATIVE](https://christopherireland.net/?ref=godly) (godly)
- [Save time and money with our premium and exclusive Framer & Webflow templates.](https://www.jp.works/?ref=godly) (godly)
- [Maison Margiela Official | Clothing, Shoes & Accessories](https://www.maisonmargiela.com/?ref=godly) (godly)
- [Shopify Editions | Winter '26](https://www.shopify.com/editions/winter2026) (awwwards)
- [Logo archive - selection of logo marks](https://dribbble.com/shots/27333381-Logo-archive-selection-of-logo-marks) (dribbble)
- [Cute Bull Logo](https://dribbble.com/shots/27334031-Cute-Bull-Logo) (dribbble)
- [Heart-in Flight ✦ Logo](https://dribbble.com/shots/27333144-Heart-in-Flight-Logo) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #f7f4ed;
  --color-ink: #1a1612;
  --color-accent: #b3261e;
  --color-rule: rgba(26,22,18,0.18);
  --color-marginalia: rgba(26,22,18,0.55);
  --font-display: "GT Sectra", "Tiempos Headline", "Recoleta", "Playfair Display", serif;
  --font-body: "Söhne", "Inter Tight", "Source Sans 3", sans-serif;
  --font-marginalia: "Söhne Mono", "JetBrains Mono", monospace;
  --font-size-display: clamp(3rem, 8vw, 6rem);
  --font-size-lede: clamp(1.25rem, 2vw, 1.5rem);
  --font-size-body: 1.125rem;
  --line-height-body: 1.7;
  --measure: 65ch;
  --radius-default: 0;
  --radius-image: 2px;
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
      "bg": "#f7f4ed",
      "ink": "#1a1612",
      "accent": "#b3261e"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(242, 241, 236)  rgb(0, 0, 0)  rgba(0, 0, 0, 0.79)  rgb(255, 255, 255)  rgb(0, 0, 0) rgb(0, 0, 0) rgba(0, 0, 0, 0)  rgb(255, 255, 255)  rgb(51, 51, 51)  rgb(32, 32, 32)  rgb(255, 255, 255) rgb(255, 255, 255) rgb(0, 0, 0)  rgb(131, 131, 131)  rgb(117, 117, 117)  rgb(243, 243, 243)

---

## 字體配對

- **Display**: Playfair Display 800  /  **Body**: Source Sans 3 400  — 經典雜誌
- **Display**: GT Sectra  /  **Body**: Söhne 400  — 當代頂級
- **Display**: Recoleta 700  /  **Body**: Inter 400  — 溫暖 editorial

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Magazine Longform Hero -->
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

1. Body 寬度限制在 65ch（var --measure），不要讓段落鋪滿全寬
2. Drop cap + pull quote + marginalia 三件套用至少一個 — 紙本特徵，AI codegen 不會做
3. Display 用 serif、body 用 sans —— 跟 AI 預設「Inter+Inter」相反

---

## Accessibility 配方

**對比策略**：Body text ≥ 7:1（長文閱讀必要）。Drop cap 跟 body 同色，hierarchy 靠 size 不靠對比。

**Focus state CSS（鍵盤焦點）**：
```css
a:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  text-decoration: underline;
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
| 行銷落地頁 | ⭐⭐⭐ |
| 企業 / B2B | ⭐ |
| 媒體 / 內容 | ⭐⭐⭐ |
| 設計工作室 / Agency | ⭐⭐ |

**AI 視覺指紋強度**：✅ 低
