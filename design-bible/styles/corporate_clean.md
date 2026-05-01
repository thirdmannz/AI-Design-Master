# 🏢 Corporate Clean

> 企業級清潔設計，嚴謹網格，藍色信任感。適合 B2B、金融科技、企業服務、醫療健康。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Customers — Evervault](https://evervault.com/customers?ref=godly) (godly)
- [Lusion - Award Winning 3D and Interactive Web Studio](https://lusion.co/?ref=godly) (godly)
- [Untitled](https://shuttle.zip/?ref=godly) (godly)
- [Duties.xyz](https://www.duties.xyz/?ref=godly) (godly)
- [Status — Make the jump to web3](https://status.app/?ref=godly) (godly)
- [Newly ai app creation landing page web design 3d animation](https://dribbble.com/shots/27333929-Newly-ai-app-creation-landing-page-web-design-3d-animation) (dribbble)
- [Education Management Web Design](https://dribbble.com/shots/27320617-Education-Management-Web-Design) (dribbble)
- [Website Design: Call to Action (CTA) for AI-Powered Platform](https://dribbble.com/shots/27332273-Website-Design-Call-to-Action-CTA-for-AI-Powered-Platform) (dribbble)
- [Travel app design](https://dribbble.com/shots/27331519-Travel-app-design) (dribbble)
- [Travel app design](https://dribbble.com/shots/27331519-Travel-app-design) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #ffffff;
  --color-bg-subtle: #f8fafc;
  --color-surface: #ffffff;
  --color-border: #e2e8f0;
  --color-text-primary: #0f172a;
  --color-text-secondary: #475569;
  --color-text-muted: #94a3b8;
  --color-accent: #2563eb;
  --color-accent-hover: #1d4ed8;
  --color-accent-subtle: #eff6ff;
  --color-success: #059669;
  --color-warning: #d97706;
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 16px;
  --shadow-xs: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.1), 0 1px 2px rgba(0,0,0,0.06);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.06);
  --font-display: "Inter", sans-serif;
  --font-body: "Inter", sans-serif;
  --spacing-section: 80px;
  --transition: all 0.2s ease;
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#f8fafc",
      "accent": "#2563eb",
      "text": "#0f172a",
      "border": "#e2e8f0"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(1, 3, 20)  rgb(223, 225, 244)  rgb(255, 255, 255)  rgba(255, 255, 255, 0.8)  rgb(186, 188, 210)  rgba(255, 255, 255, 0.15)  rgb(0, 0, 0)  rgb(102, 51, 238)  rgb(255, 255, 255) rgb(255, 255, 255) rgb(42, 43, 58)  rgba(255, 255, 255, 0.95)  rgb(255, 255, 255)  rgb(240, 241, 250)

---

## 字體配對

- **Display**: Inter 700  /  **Body**: Inter 400  — 現代企業標準
- **Display**: IBM Plex Sans 600  /  **Body**: IBM Plex Sans 400  — 科技企業感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Corporate Clean Hero -->
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

1. 用 3 層陰影（xs, sm, md）製造視覺層次，不同 elevation 的元素用不同陰影
2. accent 色只用在真正重要的 CTA 上，其他全部靠 gray scale
3. 表格和列表的每隔一行背景用 #f8fafc，但只差 2-3% 亮度 — 很細微但很專業

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐⭐⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐⭐⭐ |
