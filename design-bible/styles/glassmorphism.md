# 🪟 Glassmorphism

> 霧面玻璃層疊感，透明度與模糊構建深度。適合 SaaS、科技產品、暗色介面。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Stripe Sessions 2026 | The global internet economy conference](https://stripe.com/sessions?ref=godly) (godly)
- [Online code, design, and project management courses • SuperHi](https://superhi.com/?ref=godly) (godly)
- [10 X Hub | Design Resources](https://10xdesigners.co/?ref=godly) (godly)
- [Logan Liffick](https://loganliffick.com/?ref=godly) (godly)
- [Wise Design](https://wise.design/?ref=godly) (godly)
- [Workflow Automation Builder UIUX Design | SaaS Drag & Drop](https://dribbble.com/shots/27333638-Workflow-Automation-Builder-UIUX-Design-SaaS-Drag-Drop) (dribbble)
- [Designer Profile - Logoarchive](https://dribbble.com/shots/27331230-Designer-Profile-Logoarchive) (dribbble)
- [Designer Profile - Logoarchive](https://dribbble.com/shots/27331230-Designer-Profile-Logoarchive) (dribbble)
- [Running Mobile App](https://dribbble.com/shots/27320453-Running-Mobile-App) (dribbble)
- [Running Mobile App](https://dribbble.com/shots/27320453-Running-Mobile-App) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #0a0a1a;
  --color-surface: rgba(255,255,255,0.08);
  --color-surface-hover: rgba(255,255,255,0.14);
  --color-border: rgba(255,255,255,0.15);
  --color-text-primary: #ffffff;
  --color-text-secondary: rgba(255,255,255,0.6);
  --color-accent: #6c63ff;
  --color-accent-glow: rgba(108,99,255,0.4);
  --blur-sm: blur(8px);
  --blur-md: blur(16px);
  --blur-lg: blur(32px);
  --radius-sm: 8px;
  --radius-md: 16px;
  --radius-lg: 24px;
  --shadow-glass: 0 8px 32px rgba(0,0,0,0.3), inset 0 1px 0 rgba(255,255,255,0.1);
  --shadow-glow: 0 0 40px rgba(108,99,255,0.3);
  --font-display: "Plus Jakarta Sans", sans-serif;
  --font-body: "Inter", sans-serif;
  --spacing-section: 120px;
  --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#0a0a1a",
      "surface": "rgba(255,255,255,0.08)",
      "accent": "#6c63ff"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(249, 247, 247)  rgb(32, 3, 60)  rgb(219, 215, 215)  rgb(255, 255, 255)  rgba(255, 255, 255, 0.15)  rgb(20, 4, 36)  rgb(136, 63, 255)  rgb(255, 255, 255)  rgb(17, 17, 24)  rgb(39, 39, 230)  rgb(0, 0, 0)  rgb(225, 237, 255)

---

## 字體配對

- **Display**: Plus Jakarta Sans 700  /  **Body**: Inter 400  — 現代科技感
- **Display**: Space Grotesk 700  /  **Body**: DM Sans 400  — 幾何精準

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Glassmorphism Hero -->
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

1. 用 backdrop-filter: blur() 而非單純透明度 — 沒有模糊的玻璃感是假的
2. 邊框用 rgba(255,255,255,0.15) 的細線，1px 夠了，不要 2px
3. 光暈（glow）要不對稱，放在卡片左上角而不是正中心

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐⭐⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐⭐ |
| 行銷落地頁 | ⭐⭐⭐ |
| 企業 / B2B | ⭐ |
