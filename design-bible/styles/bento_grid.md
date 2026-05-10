# 🍱 Bento Grid

> 日式便當盒格局，模組化資訊卡片。Apple 風格的資訊展示。適合 SaaS 功能介紹、作品集、技術文件。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Carevia — Wellness Pharmacy Mobile App](https://dribbble.com/shots/27333332-Carevia-Wellness-Pharmacy-Mobile-App) (dribbble)
- [Bidirectional Slider](https://dribbble.com/shots/27333850-Bidirectional-Slider) (dribbble)
- [Dark Dashboard Finance UI](https://dribbble.com/shots/27332491-Dark-Dashboard-Finance-UI) (dribbble)
- [Billing — Untitled UI](https://dribbble.com/shots/27331481-Billing-Untitled-UI) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #f5f5f0;
  --color-surface: #ffffff;
  --color-surface-dark: #1a1a1a;
  --color-border: #e0e0db;
  --color-text-primary: #1a1a1a;
  --color-text-secondary: #666666;
  --color-accent: #007aff;
  --color-accent-2: #34c759;
  --color-accent-3: #ff9500;
  --radius-sm: 12px;
  --radius-md: 20px;
  --radius-lg: 28px;
  --gap: 12px;
  --shadow-card: 0 1px 3px rgba(0,0,0,0.08), 0 4px 12px rgba(0,0,0,0.04);
  --shadow-card-hover: 0 4px 20px rgba(0,0,0,0.12);
  --font-display: "SF Pro Display", "-apple-system", "Helvetica Neue", sans-serif;
  --font-body: "SF Pro Text", "-apple-system", "Helvetica Neue", sans-serif;
  --spacing-section: 80px;
  --transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#f5f5f0",
      "surface": "#ffffff",
      "accent": "#007aff"
},
    }
  }
}
```

### 從真實網站提取的色盤
#100100100  #e0e0e0  #202020  #808060  #404020  #a0a080  #202020  #404040  #100100100  #606060  #e0e0e0  #808080

---

## 字體配對

- **Display**: -apple-system, BlinkMacSystemFont  /  **Body**: Inter 400  — Apple 原生感
- **Display**: Geist 600  /  **Body**: Geist 400  — Vercel 現代感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Bento Grid Hero -->
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

1. 不同 grid cell 設定不同 background-color，製造色彩層次而不是全白
2. 某些 cell 要橫跨兩欄 (col-span-2)，打破完美對稱感
3. 每個 card 的 padding 要一致，但 font-size 可以不同 — 製造資訊層次

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐ |
| 行銷落地頁 | ⭐ |
| 企業 / B2B | ⭐⭐ |
| 媒體 / 內容 | ⭐ |
| 設計工作室 / Agency | ⭐⭐ |

**AI 視覺指紋強度**：⛔⛔⛔ 高 — 僅 user 主動指名 AI/futuristic 才推薦
