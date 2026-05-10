# 🔩 Neobrutalism

> 粗框線、高對比色塊、生猛排版。反精緻，強調個性與直接。適合作品集、創意工具、反叛品牌。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Kaleido Grafik / We partner with visionary clients to create beautiful digital experiences by fusing thoughtful design with playful thinking.](https://kaleidografik.com/?ref=godly) (godly)
- [Interactive Money Museum in Dallas | MoMoney](https://www.museumofmoney.com/) (awwwards)
- [Vibrant Wellness | Interactive Digital Health Experience](https://vibrant.noomoagency.com/) (awwwards)
- [Logo For Matcha Bar](https://dribbble.com/shots/27330638-Logo-For-Matcha-Bar) (dribbble)
- [Distressed Badges](https://dribbble.com/shots/27332571-Distressed-Badges) (dribbble)
- [MX Sport Monogram Emblem](https://dribbble.com/shots/27243664-MX-Sport-Monogram-Emblem) (dribbble)
- [Logo Archive — Recent Works 2025/26](https://dribbble.com/shots/27332232-Logo-Archive-Recent-Works-2025-26) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #fffef0;
  --color-surface: #ffffff;
  --color-border: #000000;
  --color-text-primary: #0d0d0d;
  --color-text-secondary: #333333;
  --color-accent: #ff4d00;
  --color-accent-2: #ffde00;
  --color-accent-3: #00b4d8;
  --border-width: 2px;
  --border-heavy: 3px;
  --radius-sm: 0px;
  --radius-md: 4px;
  --radius-lg: 8px;
  --shadow-brutal: 4px 4px 0px #000000;
  --shadow-brutal-lg: 8px 8px 0px #000000;
  --shadow-brutal-hover: 6px 6px 0px #000000;
  --font-display: "Space Grotesk", sans-serif;
  --font-body: "Inconsolata", monospace;
  --spacing-section: 80px;
  --transition: all 0.1s ease;
}
```

### Tailwind Config 對應
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
      "bg": "#fffef0",
      "accent": "#ff4d00",
      "border": "#000000"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(236, 234, 229)  rgb(0, 0, 0)  rgba(0, 0, 0, 0.5)  rgb(255, 255, 255)  rgb(0, 0, 0) rgb(0, 0, 0) rgba(0, 0, 0, 0)  rgb(255, 245, 221)  rgb(17, 17, 17)  lab(90.952 0 -0.0000119209)  rgb(255, 255, 255)  rgb(244, 242, 66)  rgb(0, 0, 244)  oklab(0.177637 0.00000810623 0.00000356138 / 0.6)

---

## 字體配對

- **Display**: Space Grotesk 800  /  **Body**: Inconsolata 400  — 技術感粗礦
- **Display**: Archivo Black  /  **Body**: Archivo 400  — 統一家族，衝擊感

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Neobrutalism Hero -->
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

1. box-shadow 用純黑色偏移而非模糊 (4px 4px 0 #000) — 這是新野蠻主義的靈魂
2. 排版要有意識地「不對齊」某個元素，製造張力
3. 按鈕 hover 時把 shadow 縮小 (4px→2px) 製造按壓感

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐ |
| 個人作品集 | ⭐⭐⭐ |
| 電商 / 品牌 | ⭐ |
| 行銷落地頁 | ⭐ |
| 企業 / B2B | ⭐ |
| 媒體 / 內容 | ⭐ |
| 設計工作室 / Agency | ⭐⭐ |

**AI 視覺指紋強度**：⚠️ 中
