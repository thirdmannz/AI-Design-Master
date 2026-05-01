# 📰 Editorial Maximal

> 雜誌排版感，大標題主導，混搭字體大小，網格突破。適合媒體品牌、設計工作室、高端部落格。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Pedro Duarte's Personal Website](https://ped.ro/?ref=godly) (godly)
- [KidSuper World](https://kidsuper.world/?ref=godly) (godly)
- [Logo archive - selection of logo marks](https://dribbble.com/shots/27333381-Logo-archive-selection-of-logo-marks) (dribbble)
- [Vitra](https://dribbble.com/shots/27333147-Vitra) (dribbble)
- [Cute Bull Logo](https://dribbble.com/shots/27334031-Cute-Bull-Logo) (dribbble)
- [Cportesano Cigars](https://dribbble.com/shots/27332668-Cportesano-Cigars) (dribbble)
- [PropTech CRM Dashboard — Partner Outreach & Deal Flow UI](https://dribbble.com/shots/27332795-PropTech-CRM-Dashboard-Partner-Outreach-Deal-Flow-UI) (dribbble)

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
rgb(17, 17, 17)  rgb(255, 255, 255)  rgb(238, 238, 238)  rgb(255, 255, 255)  rgb(0, 0, 0)  rgba(255, 255, 255, 0.9)  rgb(102, 102, 102)  #100100100  #000000  #606060  #202020  #e0e0e0

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

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐ |
| 個人作品集 | ⭐⭐⭐ |
| 電商 / 品牌 | ⭐⭐⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐ |
