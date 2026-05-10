# 🧱 Brutalist / Anti-Design

> 預設瀏覽器樣式、monospace、無圓角、無陰影、左上對齊。不是「醜」，是有意拒絕當代 SaaS 美學。適合個人作品集、實驗網站、藝術家 portfolio、技術 blog。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Craig Mod](https://craigmod.com) (manual)
- [Bloomberg Businessweek](https://www.bloomberg.com/businessweek) (manual)
- [Berkshire Hathaway](https://www.berkshirehathaway.com) (manual)
- [MSCHF](https://mschf.com) (manual)
- [Cabel](https://cabel.com) (manual)
- [James Off](https://jamesoff.net) (manual)
- [Brutalist Websites](https://brutalistwebsites.com) (manual)
- [Vercel Ship 26](https://vercel.com/ship?ref=godly) (godly)
- [Next.js Conf 2025](https://nextjs.org/conf?ref=godly) (godly)
- [ASTRODITHER — Robert Borghesi LAB — [SIGNAL. LOST. BEAUTY. FOUND. DIGITAL. CHAOS.]](https://astrodither.robertborghesi.is/) (awwwards)
- [Mobbin — UI & UX design inspiration for mobile & web apps](https://mobbin.com/?via=httpster) (httpster)
- [Quaffable Wine Label System: All Three Variants](https://dribbble.com/shots/27332666-Quaffable-Wine-Label-System-All-Three-Variants) (dribbble)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #ffffff;
  --color-ink: #000000;
  --color-accent: #0000ff;
  --color-rule: #000000;
  --font-display: "JetBrains Mono", "IBM Plex Mono", ui-monospace, monospace;
  --font-body: "JetBrains Mono", "IBM Plex Mono", ui-monospace, monospace;
  --font-serif: "Times New Roman", Times, serif;
  --font-size-display: clamp(2rem, 5vw, 4rem);
  --font-size-body: 1rem;
  --line-height-body: 1.5;
  --radius-default: 0;
  --shadow-none: none;
  --border-default: 1px solid var(--color-ink);
  --border-heavy: 2px solid var(--color-ink);
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
      "ink": "#000000",
      "accent": "#0000ff"
},
    }
  }
}
```

### 從真實網站提取的色盤
lab(0.0177803 0 0)  lab(93.736 0 0)  rgb(0, 0, 0)  lab(66.3894 -5.37798 -55.7933)  lab(0 0 0)  lab(98.144 0 -0.0000119209)  lab(7.78201 -0.0000149012 0)  lab(32.72 -0.0000149012 0)  oklab(0.960998 -0.00000965595 0.000022471 / 0.9)  lab(0 0 0 / 0.08)  rgb(255, 255, 255)  lab(47.9229 22.3147 -86.8328)

---

## 字體配對

- **Display**: JetBrains Mono 700  /  **Body**: JetBrains Mono 400  — 純 mono 反設計
- **Display**: IBM Plex Mono 700  /  **Body**: IBM Plex Sans 400  — mono 標題 + sans body
- **Display**: Times New Roman 700  /  **Body**: JetBrains Mono 400  — default browser 風格

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Brutalist / Anti-Design Hero -->
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

1. Link 用瀏覽器預設樣式（藍色 + underline），不要 hover 後變漸層
2. Form input 不要加 border-radius 跟 placeholder 淡化效果 — 直接放預設或粗黑框
3. 故意讓 heading overflow: hidden 切掉一半 — 製造張力

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
| 設計工作室 / Agency | ⭐⭐⭐ |

**AI 視覺指紋強度**：✅ 低
