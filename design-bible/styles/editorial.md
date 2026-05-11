# 📰 Editorial Maximal

> 雜誌排版感，大標題主導，混搭字體大小，網格突破。適合媒體品牌、設計工作室、高端部落格。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Pedro Duarte's Personal Website](https://ped.ro/?ref=godly) (godly)
- [Home - Emilie Aubry](https://www.emilieaubry.com/) (awwwards)
- [Sleep Well Creatives](https://sleep-well-creatives.com/) (awwwards)
- [Occupied](https://occupied.unadsgn.tw/) (awwwards)
- [Weekend MaxMara Gift Guide](https://weekend-mm-2025-gift-guide-production.monogrid.io/) (awwwards)
- [Workflow Automation Builder UIUX Design | SaaS Drag & Drop](https://dribbble.com/shots/27333638-Workflow-Automation-Builder-UIUX-Design-SaaS-Drag-Drop) (dribbble)
- [Newly ai app creation landing page web design 3d animation](https://dribbble.com/shots/27333929-Newly-ai-app-creation-landing-page-web-design-3d-animation) (dribbble)
- [AI Healthcare Website](https://dribbble.com/shots/27333724-AI-Healthcare-Website) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #ffffff;
  --color-bg-dark: #111111;
  --color-surface: #f8f8f6;
  --color-border: #e0e0da;
  --color-text-primary: #111111;
  --color-text-secondary: #555550;
  --color-accent: #ff3300;
  --color-accent-2: #0047ff;
  --radius-sm: 0px;
  --radius-md: 2px;
  --radius-lg: 4px;
  --font-display: "PP Editorial New", "Playfair Display", serif;
  --font-display-wide: "Bebel Neue", "Anton", sans-serif;
  --font-body: "Neue Haas Grotesk", "Helvetica Neue", sans-serif;
  --font-mono: "Courier New", monospace;
  --font-size-hero: clamp(4rem, 12vw, 14rem);
  --font-size-display: clamp(2rem, 5vw, 6rem);
  --spacing-section: 120px;
  --letter-spacing-hero: -0.04em;
  --transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#ffffff",
      "accent": "#ff3300",
      "text": "#111111"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(17, 17, 17)  rgb(255, 255, 255)  rgb(238, 238, 238)  rgb(0, 0, 0)  rgba(255, 255, 255, 0.08)  rgb(255, 255, 255)  rgb(254, 241, 208)  rgb(51, 51, 51)  rgb(255, 255, 255)  rgb(0, 66, 175)  rgb(69, 137, 247)  rgb(36, 81, 181)

---

## 字體配對

- **Display**: PP Editorial New Italic  /  **Body**: Neue Haas Grotesk  — 頂級設計媒體感
- **Display**: Anton 400  /  **Body**: Noto Serif 400  — 衝擊力強

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Editorial Maximal Hero -->
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

1. Hero 標題要用 clamp() 流體字體大小，最大要夠大（至少 10vw）
2. 刻意讓一個元素打破 grid 邊界（負 margin 或 absolute position）
3. 使用 mix-blend-mode: multiply 在圖片上疊加色塊，製造印刷感

---

## Accessibility 配方

**對比策略**：Body text 對 bg ≥ 7:1（editorial 標準），追求閱讀舒適。

**Focus state CSS（鍵盤焦點）**：
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
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
| 個人作品集 | ⭐⭐⭐ |
| 電商 / 品牌 | ⭐⭐⭐ |
| 行銷落地頁 | ⭐⭐⭐ |
| 企業 / B2B | ⭐⭐ |
| 媒體 / 內容 | ⭐⭐⭐ |
| 設計工作室 / Agency | ⭐⭐⭐ |

**AI 視覺指紋強度**：✅ 低
