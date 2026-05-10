# 🕊️ Minimal Float

> 極致留白，元素像漂浮在空氣中。沉默而有力。適合高端作品集、奢侈品牌、設計師個人網站。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Experience email at its best - Tatem](https://tatem.com/?ref=godly) (godly)
- [Fey: Make better investments.](https://www.feyapp.com/?ref=godly) (godly)
- [THE LOOKBACK](https://tlb.betteroff.studio/) (awwwards)
- [Newly ai app creation landing page web design 3d animation](https://dribbble.com/shots/27333929-Newly-ai-app-creation-landing-page-web-design-3d-animation) (dribbble)
- [Travel app design](https://dribbble.com/shots/27331519-Travel-app-design) (dribbble)
- [QuickFix – Home Services Mobile App](https://dribbble.com/shots/27332307-QuickFix-Home-Services-Mobile-App) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #fafaf8;
  --color-surface: #ffffff;
  --color-border: #e8e8e4;
  --color-text-primary: #111111;
  --color-text-secondary: #666660;
  --color-text-muted: #aaa9a4;
  --color-accent: #111111;
  --radius-sm: 2px;
  --radius-md: 6px;
  --radius-lg: 12px;
  --shadow-float: 0 2px 40px rgba(0,0,0,0.06);
  --shadow-hover: 0 8px 60px rgba(0,0,0,0.1);
  --font-display: "Editorial New", "Playfair Display", serif;
  --font-body: "Suisse Intl", "Helvetica Neue", sans-serif;
  --spacing-section: 160px;
  --letter-spacing-display: -0.03em;
  --line-height-body: 1.8;
  --transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#fafaf8",
      "text": "#111111",
      "muted": "#aaa9a4"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(10, 10, 10)  rgba(255, 255, 255, 0.95)  rgba(255, 255, 255, 0.06)  rgba(255, 255, 255, 0.7)  rgba(255, 255, 255, 0.55)  rgba(255, 255, 255, 0.35)  rgba(255, 255, 255, 0.1)  rgba(252, 252, 252, 0.08)  rgb(0, 0, 0)  rgb(255, 255, 255)  rgba(255, 255, 255, 0.047)  rgba(255, 255, 255, 0.5)

---

## 字體配對

- **Display**: Playfair Display 300 italic  /  **Body**: Helvetica Neue 300  — 奢侈品牌感
- **Display**: Cormorant Garamond 500  /  **Body**: Inter 300  — 文學藝術感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Minimal Float Hero -->
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

1. 字距 (letter-spacing) 設為 -0.03em 讓大標題更緊湊、更像手工設計
2. 使用 serif 字體當標題 + sans-serif 當內文，製造古典×現代的對比
3. section padding 要大到讓你覺得「會不會太多留白了？」— 那才是對的

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐⭐ |
| 個人作品集 | ⭐⭐⭐ |
| 電商 / 品牌 | ⭐⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐⭐⭐ |
| 媒體 / 內容 | ⭐ |
| 設計工作室 / Agency | ⭐⭐ |

**AI 視覺指紋強度**：✅ 低
