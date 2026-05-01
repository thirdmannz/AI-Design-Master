# 🌐 3D Immersive

> 3D 渲染、WebGL、沉浸式體驗。適合遊戲、科技、高端產品展示、互動作品集。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [SILENCIO ® VISUAL LANGUAGES](https://silencio.es/?ref=godly) (godly)
- [Twingate: It's time to ditch your VPN](https://www.twingate.com/?ref=godly) (godly)
- [AuthKit by WorkOS](https://authkit.com/?ref=godly) (godly)
- [큰그림컴퍼니 - Bigpicture company](https://www.bpco.kr/?ref=godly) (godly)
- [SavoirFaire©. Holistic creative studio based in NYC.](https://savoirfaire.nyc/?ref=godly) (godly)
- [AI Code](https://dribbble.com/shots/27333490-AI-Code) (dribbble)
- [Newly ai app creation landing page web design 3d animation](https://dribbble.com/shots/27333929-Newly-ai-app-creation-landing-page-web-design-3d-animation) (dribbble)
- [Softbank Natural AI Phone intro](https://dribbble.com/shots/27333576-Softbank-Natural-AI-Phone-intro) (dribbble)
- [Bidirectional Slider](https://dribbble.com/shots/27333850-Bidirectional-Slider) (dribbble)
- [Bidirectional Slider](https://dribbble.com/shots/27333850-Bidirectional-Slider) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #000000;
  --color-bg-2: #050510;
  --color-surface: rgba(255,255,255,0.03);
  --color-border: rgba(255,255,255,0.08);
  --color-text-primary: #ffffff;
  --color-text-secondary: rgba(255,255,255,0.5);
  --color-accent: #00f0ff;
  --color-accent-2: #ff006e;
  --color-glow-cyan: rgba(0,240,255,0.4);
  --color-glow-magenta: rgba(255,0,110,0.3);
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 16px;
  --font-display: "Orbitron", sans-serif;
  --font-body: "Exo 2", sans-serif;
  --font-mono: "JetBrains Mono", monospace;
  --spacing-section: 100vh;
  --transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  --z-canvas: -1;
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#000000",
      "accent": "#00f0ff",
      "accent2": "#ff006e"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(0, 0, 0)  rgb(219, 218, 217)  rgb(222, 222, 221)  rgb(14, 15, 17)  rgb(0, 0, 0)  rgb(255, 255, 255)  rgb(182, 171, 255)  rgb(238, 243, 95)  rgb(0, 203, 170)  rgb(161, 161, 170)  rgb(141, 141, 150)  rgb(97, 98, 107)

---

## 字體配對

- **Display**: Orbitron 700  /  **Body**: Exo 2 300  — 未來科技感
- **Display**: Rajdhani 600  /  **Body**: Source Code Pro 400  — 技術沉浸感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- 3D Immersive Hero -->
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

1. Three.js canvas 設 position: fixed; z-index: -1 作為背景，內容疊在上面
2. UI 文字用少量字，讓 3D 視覺說話，避免文字密集
3. 掃描線效果 (scanline overlay) 讓 UI 感覺更有深度：background repeating-linear-gradient

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐⭐ |
| 個人作品集 | ⭐⭐ |
| 電商 / 品牌 | ⭐⭐ |
| 行銷落地頁 | ⭐⭐ |
| 企業 / B2B | ⭐ |
