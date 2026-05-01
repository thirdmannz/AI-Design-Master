# 🫧 Claymorphism

> 3D 黏土感，大圓角，鮮豔飽和色，擬真陰影。適合兒童產品、遊戲、教育 App、有趣的 SaaS。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Home | Traffic Productions](https://www.traffic.productions/?ref=godly) (godly)
- [Kons](https://kons.fyi/?ref=godly) (godly)
- [Umbrel - Personal home cloud and OS for self-hosting](https://umbrel.com/?ref=godly) (godly)
- [Yung Studio — Welcome!](https://www.yung.studio/?ref=godly) (godly)
- [Hypershell Energy Analytics UI – Exosuit Mobile App](https://dribbble.com/shots/27333818-Hypershell-Energy-Analytics-UI-Exosuit-Mobile-App) (dribbble)
- [Social Networking App UI Design](https://dribbble.com/shots/27330747-Social-Networking-App-UI-Design) (dribbble)
- [Travel app design](https://dribbble.com/shots/27331519-Travel-app-design) (dribbble)
- [QuickFix – Home Services Mobile App](https://dribbble.com/shots/27332307-QuickFix-Home-Services-Mobile-App) (dribbble)
- [Softbank Natural AI Phone intro](https://dribbble.com/shots/27333576-Softbank-Natural-AI-Phone-intro) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #f0f4ff;
  --color-surface: #ffffff;
  --color-text-primary: #1a1a2e;
  --color-text-secondary: #4a4a6a;
  --color-clay-pink: #ff6b9d;
  --color-clay-purple: #a855f7;
  --color-clay-blue: #3b82f6;
  --color-clay-green: #10b981;
  --color-clay-yellow: #fbbf24;
  --radius-sm: 16px;
  --radius-md: 28px;
  --radius-lg: 40px;
  --radius-pill: 9999px;
  --shadow-clay: 0 8px 0 rgba(0,0,0,0.15), 0 16px 32px rgba(0,0,0,0.1);
  --shadow-clay-sm: 0 4px 0 rgba(0,0,0,0.12), 0 8px 16px rgba(0,0,0,0.08);
  --font-display: "Nunito", sans-serif;
  --font-body: "Nunito", sans-serif;
  --spacing-section: 80px;
  --transition: all 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#f0f4ff",
      "pink": "#ff6b9d",
      "purple": "#a855f7"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(21, 21, 21)  rgb(243, 243, 243)  rgb(255, 255, 255)  rgba(255, 255, 255, 0.96)  rgb(117, 117, 117)  rgb(0, 184, 73)  rgb(245, 114, 0)  rgb(0, 139, 245)  rgb(0, 0, 0)  rgb(255, 255, 255)  rgb(227, 160, 129)  rgba(255, 255, 255, 0.62)

---

## 字體配對

- **Display**: Nunito 800  /  **Body**: Nunito 400  — 圓潤可愛
- **Display**: Fredoka One  /  **Body**: Poppins 400  — 活潑歡樂

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Claymorphism Hero -->
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

1. shadow 的第一層用純 offset (0 8px 0 rgba) 製造 3D 底部厚度感
2. 顏色要鮮豔但避免螢光 — 用 500 level 而不是 400，保持重量感
3. 元素 hover 時加 translateY(-4px) 配合 shadow 增加 — 製造按壓感

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐⭐⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐ |
