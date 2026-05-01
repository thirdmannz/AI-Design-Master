# 🌿 Organic Nature

> 大地色系、有機曲線、手繪質感。反科技，強調人情味與可持續性。適合健康品牌、有機食品、生活方式品牌。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [herding.app](https://www.herdi.ng/?ref=godly) (godly)
- [Max Yinger ☞ UI Engineer](https://yinger.dev/?ref=godly) (godly)
- [Family | Family](https://family.co/?ref=godly) (godly)
- [Branding & Web Agency | EPIC Agency](https://www.epic.net/?ref=godly) (godly)
- [Flying Papers - Home](https://www.flyingpapers.com/?ref=godly) (godly)
- [Logo archive - selection of logo marks](https://dribbble.com/shots/27333381-Logo-archive-selection-of-logo-marks) (dribbble)
- [Logo Design for Construction FinTech](https://dribbble.com/shots/27077669-Logo-Design-for-Construction-FinTech) (dribbble)
- [Gefeen Logo Design](https://dribbble.com/shots/27334139-Gefeen-Logo-Design) (dribbble)
- [Mile Square Cafe Identity Design](https://dribbble.com/shots/27329616-Mile-Square-Cafe-Identity-Design) (dribbble)
- [10 years retrospective](https://dribbble.com/shots/27331353-10-years-retrospective) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #f5f0e8;
  --color-bg-2: #ede8dc;
  --color-surface: #faf7f2;
  --color-border: #d4cbb8;
  --color-text-primary: #2c2416;
  --color-text-secondary: #5c4f3a;
  --color-sage: #8a9e7a;
  --color-terracotta: #c4714a;
  --color-earth: #a67c52;
  --color-cream: #f5f0e8;
  --color-accent: #8a9e7a;
  --radius-sm: 4px;
  --radius-md: 12px;
  --radius-lg: 60px;
  --radius-organic: 30% 70% 70% 30% / 30% 30% 70% 70%;
  --shadow-soft: 0 4px 24px rgba(44,36,22,0.1);
  --font-display: "Cormorant", serif;
  --font-body: "Jost", sans-serif;
  --font-handwritten: "Caveat", cursive;
  --spacing-section: 100px;
  --transition: all 0.4s ease;
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#f5f0e8",
      "sage": "#8a9e7a",
      "terracotta": "#c4714a",
      "earth": "#a67c52"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(28, 28, 26)  rgba(255, 253, 244, 0.596)  rgba(255, 252, 236, 0.392)  rgba(255, 255, 254, 0.92)  rgb(127, 126, 119)  rgb(22, 22, 21)  rgba(254, 254, 218, 0.055)  rgba(255, 255, 236, 0.173)  rgb(18, 19, 15)  rgb(228, 223, 218)  rgba(18, 19, 15, 0.4)  rgba(228, 223, 218, 0.2)

---

## 字體配對

- **Display**: Cormorant 500 italic  /  **Body**: Jost 300  — 自然有機高端感
- **Display**: Libre Baskerville  /  **Body**: Karla 400  — 可持續品牌感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Organic Nature Hero -->
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

1. 使用 border-radius 的不規則四值語法製造有機曲線感 (30% 70% 70% 30% / ...)
2. 加入一個手寫字體做點綴標籤，但只用一兩處
3. 圖片用老照片濾鏡 (sepia + contrast) 讓視覺更一致

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐⭐⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐ |
