# 🌌 Aurora UI

> 暗色底上的彩色漸層光暈，像極光或宇宙星雲。適合 AI 產品、科技新創、創意工具。

---

## 代表網站 (從 Godly / Dribbble 提取)

*(Run scraper to populate with real examples)*

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #060612;
  --color-bg-2: #0d0d20;
  --color-surface: rgba(255,255,255,0.05);
  --color-border: rgba(255,255,255,0.1);
  --color-text-primary: #ffffff;
  --color-text-secondary: rgba(255,255,255,0.65);
  --color-aurora-1: #7c3aed;
  --color-aurora-2: #2563eb;
  --color-aurora-3: #059669;
  --color-aurora-4: #db2777;
  --gradient-aurora: radial-gradient(ellipse at 20% 50%, rgba(124,58,237,0.3) 0%, transparent 60%), radial-gradient(ellipse at 80% 20%, rgba(37,99,235,0.25) 0%, transparent 60%), radial-gradient(ellipse at 60% 80%, rgba(5,150,105,0.2) 0%, transparent 50%);
  --gradient-cta: linear-gradient(135deg, #7c3aed, #2563eb);
  --radius-sm: 8px;
  --radius-md: 16px;
  --radius-lg: 24px;
  --shadow-aurora: 0 0 120px rgba(124,58,237,0.15);
  --font-display: "Syne", sans-serif;
  --font-body: "Inter", sans-serif;
  --spacing-section: 120px;
  --transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#060612",
      "aurora1": "#7c3aed",
      "aurora2": "#2563eb",
      "aurora3": "#059669"
},
    }
  }
}
```

### 從真實網站提取的色盤
*(From scraped sites)*

---

## 字體配對

- **Display**: Syne 700  /  **Body**: Inter 400  — AI 科技前衛感
- **Display**: Clash Display 600  /  **Body**: General Sans 400  — 新銳品牌感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Aurora UI Hero -->
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

1. 光暈 (radial-gradient) 要用多個，位置不對稱，有的要超出畫面
2. 不要讓所有文字都是純白 — 次要文字用 rgba(255,255,255,0.65) 製造層次
3. CTA 按鈕的漸層方向要和背景光暈相反，製造視覺對比

---

## Accessibility 配方

**對比策略**：Gradient bg 上 text 必須有 solid color fallback。Aurora blob 後面別放 body text。

**Focus state CSS（鍵盤焦點）**：
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  box-shadow: 0 0 24px rgba(var(--color-accent-rgb), 0.4);
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
| SaaS / 科技產品 | ⭐⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐ |
| 媒體 / 內容 | ⭐ |
| 設計工作室 / Agency | ⭐⭐ |

**AI 視覺指紋強度**：⛔⛔⛔ 高 — 僅 user 主動指名 AI/futuristic 才推薦
