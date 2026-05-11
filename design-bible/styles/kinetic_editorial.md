# ⚡ Kinetic Editorial

> 動態排版，滾動觸發動畫，文字和圖像的動態配合。適合互動作品集、品牌故事頁、行銷落地頁。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Atlas Card](https://atlascard.com/?ref=godly) (godly)
- [AuthKit by WorkOS](https://authkit.com/?ref=godly) (godly)
- [Digital tools for creatives – 099 Supply](https://099.supply/?ref=godly) (godly)
- [Status — Make the jump to web3](https://status.app/?ref=godly) (godly)
- [Lovi — Smart Skin Care](https://lovi.care/?ref=godly) (godly)
- [Cosmos](https://cosmos.so/?ref=godly) (godly)
- [GitHub · Change is constant. GitHub keeps you ahead. · GitHub](https://github.com/?ref=godly) (godly)
- [Eco: The Stablecoin Network That Makes Money Programmable](https://eco.com/?ref=godly) (godly)
- [AI Code](https://dribbble.com/shots/27333490-AI-Code) (dribbble)
- [Newly ai app creation landing page web design 3d animation](https://dribbble.com/shots/27333929-Newly-ai-app-creation-landing-page-web-design-3d-animation) (dribbble)
- [Charted - Color system](https://dribbble.com/shots/27332229-Charted-Color-system) (dribbble)
- [Landing Page Design for an Open-Source AI Tool](https://dribbble.com/shots/27331769-Landing-Page-Design-for-an-Open-Source-AI-Tool) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #0e0e0e;
  --color-surface: #1a1a1a;
  --color-border: #2a2a2a;
  --color-text-primary: #f0ede8;
  --color-text-secondary: rgba(240,237,232,0.6);
  --color-accent: #e8ff00;
  --color-accent-2: #ff4500;
  --radius-sm: 0px;
  --radius-md: 4px;
  --radius-lg: 8px;
  --font-display: "Syne", sans-serif;
  --font-display-wide: "Bebas Neue", sans-serif;
  --font-body: "DM Sans", sans-serif;
  --font-size-hero: clamp(5rem, 15vw, 18rem);
  --letter-spacing-hero: -0.06em;
  --spacing-section: 20vh;
  --transition-fast: all 0.15s ease;
  --transition-smooth: all 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  --transition-bounce: all 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#0e0e0e",
      "accent": "#e8ff00",
      "text": "#f0ede8"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(0, 0, 0)  rgb(248, 248, 248)  rgba(0, 0, 0, 0.32)  rgba(255, 255, 255, 0.8)  rgb(30, 30, 30)  rgb(0, 19, 145)  rgb(255, 255, 255)  rgb(128, 128, 128)  rgb(39, 39, 39)  rgb(5, 6, 15)  rgb(255, 255, 255)  rgb(216, 236, 248)

---

## 字體配對

- **Display**: Bebas Neue  /  **Body**: DM Sans 300  — 動態媒體感
- **Display**: Syne 800  /  **Body**: Syne 400  — 統一又有衝擊力

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Kinetic Editorial Hero -->
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

1. Hero 標題要大到幾乎超出螢幕，字距設 -0.06em，製造壓迫感
2. 滾動動畫用 Intersection Observer + CSS translate，不要用純 CSS animation（沒有觸發點）
3. accent 色用螢光色（電光黃 #e8ff00）但只用在一個關鍵元素上

---

## Accessibility 配方

**對比策略**：Scroll 動效中 text overlay 必有 backdrop（半透明黑底）保證對比恆定。

**Focus state CSS（鍵盤焦點）**：
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 4px;
  animation: focus-pulse 1s ease-out;
}
@keyframes focus-pulse {
  0% { outline-offset: 8px; opacity: 0; }
  100% { outline-offset: 4px; opacity: 1; }
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
| 個人作品集 | ⭐⭐⭐ |
| 電商 / 品牌 | ⭐ |
| 行銷落地頁 | ⭐⭐⭐ |
| 企業 / B2B | ⭐ |
| 媒體 / 內容 | ⭐ |
| 設計工作室 / Agency | ⭐⭐⭐ |

**AI 視覺指紋強度**：✅ 低
