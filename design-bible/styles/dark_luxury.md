# 🖤 Dark Luxury

> 深黑底色配金色/米色調，精品奢華感。適合高端品牌、奢侈品、精品餐廳、高端服務。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [UNVEIL®](https://unveil.fr/?ref=godly) (godly)
- [Stryds](https://stryds.com/?ref=godly) (godly)
- [404 - Page not found](https://ohm.studio/?ref=godly) (godly)
- [Vitra](https://dribbble.com/shots/27333147-Vitra) (dribbble)
- [Cute Bull Logo](https://dribbble.com/shots/27334031-Cute-Bull-Logo) (dribbble)
- [Logo Design for Construction FinTech](https://dribbble.com/shots/27077669-Logo-Design-for-Construction-FinTech) (dribbble)
- [Heart-in Flight ✦ Logo](https://dribbble.com/shots/27333144-Heart-in-Flight-Logo) (dribbble)
- [Heart-in Flight ✦ Logo](https://dribbble.com/shots/27333144-Heart-in-Flight-Logo) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #0c0c0a;
  --color-bg-2: #141410;
  --color-surface: #1c1c18;
  --color-border: rgba(212,175,55,0.2);
  --color-text-primary: #f5f0e8;
  --color-text-secondary: rgba(245,240,232,0.6);
  --color-gold: #d4af37;
  --color-gold-light: #e8c95a;
  --color-gold-muted: rgba(212,175,55,0.3);
  --color-accent: #d4af37;
  --radius-sm: 2px;
  --radius-md: 4px;
  --radius-lg: 8px;
  --shadow-luxury: 0 0 80px rgba(212,175,55,0.08);
  --font-display: "Cormorant Garamond", "Didot", serif;
  --font-display-alt: "Playfair Display", serif;
  --font-body: "Montserrat", sans-serif;
  --font-body-light: "Montserrat", 300, sans-serif;
  --spacing-section: 160px;
  --letter-spacing-display: 0.05em;
  --letter-spacing-ui: 0.15em;
  --transition: all 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#0c0c0a",
      "gold": "#d4af37",
      "surface": "#1c1c18"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(0, 0, 0)  rgb(16, 16, 16)  rgb(51, 51, 51)  rgb(253, 253, 253)  rgb(111, 111, 111)  rgb(166, 255, 0)  rgb(4, 1, 38)  rgb(32, 32, 32)  rgb(0, 0, 238)  rgb(61, 61, 61)  rgb(23, 23, 23)  rgb(0, 0, 0)

---

## 字體配對

- **Display**: Cormorant Garamond 300 italic  /  **Body**: Montserrat 300  — 頂級奢侈品牌
- **Display**: Playfair Display 400  /  **Body**: Lato 300  — 精品飯店感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Dark Luxury Hero -->
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

1. 用 letter-spacing: 0.15em 在小標籤和按鈕上，製造高級雜誌感
2. 金色不要用純 #FFD700，用 #d4af37（古金）更高端
3. 分隔線用 1px solid rgba(gold,0.2) 而非實線 — 精品的邊界是暗示，不是宣告

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐⭐⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐ |
