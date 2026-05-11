# 📐 Swiss Editorial

> 嚴格 grid、左對齊、極簡色票（≤3色），排版做所有 hierarchy。AI 視覺語言的反義詞。適合 agency/設計工作室、企業年報、design-savvy SaaS。

---

## 代表網站 (從 Godly / Dribbble 提取)

- [Bureau Borsche](https://www.bureauborsche.com) (manual)
- [Manual Creative](https://manualcreative.com) (manual)
- [Pentagram](https://www.pentagram.com) (manual)
- [Studio Feixen](https://www.studiofeixen.ch) (manual)
- [Commission Studio](https://commission.studio) (manual)
- [Accept & Proceed](https://acceptandproceed.com) (manual)
- [Locomotive | Montreal web agency](https://locomotive.ca/en?ref=godly) (godly)
- [Mike Matas](https://mikematas.com/?ref=godly) (godly)
- [Spring/Summer | Copenhagen based digital first Design & Brand Agency](https://springsummer.dk/?ref=godly) (godly)
- [큰그림컴퍼니 - Bigpicture company](https://www.bpco.kr/?ref=godly) (godly)
- [Concrete Club Studio — Creative freelance collective based in Paris](https://concreteclub.studio/?ref=godly) (godly)
- [Skiff - Private, encrypted, secure email - 10 GB free](https://skiff.com/?ref=godly) (godly)

---

## 色盤

### CSS Tokens (`:root`)
```css
:root {
  --color-bg: #ffffff;
  --color-ink: #000000;
  --color-accent: #ff3b00;
  --color-rule: rgba(0,0,0,0.12);
  --font-display: "Söhne Breit", "Inter Tight", "Helvetica Now Display", Helvetica, sans-serif;
  --font-body: "Söhne", "Inter Tight", Helvetica, sans-serif;
  --font-mono: "JetBrains Mono", monospace;
  --letter-spacing-display: -0.04em;
  --letter-spacing-kicker: 0.12em;
  --font-size-display: clamp(4.5rem, 12vw, 14rem);
  --font-size-h1: clamp(2.5rem, 5vw, 4.5rem);
  --font-size-kicker: 0.75rem;
  --line-height-tight: 0.95;
  --radius-default: 0;
  --shadow-none: none;
  --grid-cols: 12;
  --grid-gap: 1.5rem;
  --baseline: 8px;
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
      "accent": "#ff3b00"
},
    }
  }
}
```

### 從真實網站提取的色盤
rgb(0, 0, 0)  rgb(255, 255, 255)  rgb(49, 45, 251)  rgb(0, 0, 0)  rgb(255, 255, 255)  rgb(0, 0, 0)  rgb(18, 18, 18)  rgba(255, 255, 255, 0.4)  rgb(255, 255, 255)  rgb(0, 0, 0)  rgb(64, 80, 101)  rgb(255, 255, 255)

---

## 字體配對

- **Display**: Inter Tight 800  /  **Body**: Inter Tight 400  — 當代瑞士語言
- **Display**: Helvetica Now Display 800  /  **Body**: Helvetica Now Text 400  — 經典瑞士
- **Display**: Söhne Breit  /  **Body**: Söhne  — 頂級 agency 標配

### Google Fonts 引入範例
```html
<!-- 在 <head> 加入 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
```

---

## 元件範例

### Hero Section
```html
<!-- Swiss Editorial Hero -->
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

1. 完全不用 border-radius、不用 box-shadow — 排版 + 細線 + 色塊就是全部 hierarchy
2. Kicker 永遠用 monospace + uppercase + 大字距 (0.12em)，跟 display 字成尺度對比
3. Section 之間用 1px 細線分隔（opacity 0.12），不要用 padding-only

---

## Accessibility 配方

**對比策略**：Pure black on off-white (~18:1)。AAA 標準，editorial 應有的對比。

**Focus state CSS（鍵盤焦點）**：
```css
*:focus-visible {
  outline: 1px solid var(--color-ink);
  outline-offset: 2px;
}
```

**通用要求**：
- 一頁只一個 `<h1>`，heading 階層不跳階
- 所有 `<img>` 有 `alt` 屬性
- 用 `<nav> <main> <section> <article>` 不用 `<div>` soup
- 必出 skip link（`<a href="#main" class="skip-link">Skip to content</a>`）
- Form input font-size ≥ 16px（避免 iOS auto-zoom）
- Touch target ≥ 44×44px

**參考文件**：
- [Contrast rules](../a11y/contrast-rules.md) — WCAG 對比要求
- [Semantic patterns](../a11y/semantic-patterns.md) — 元件 × HTML5 對照
- [ARIA patterns](../a11y/aria-patterns.md) — modal / tabs / menu 配方
- [Focus states](../a11y/focus-states.md) — 全 17 風格 focus CSS
- [Keyboard nav](../a11y/keyboard-nav.md) — 鍵盤導覽

---

## 適用場景

| 場景 | 匹配度 |
|------|--------|
| SaaS / 科技產品 | ⭐⭐⭐ |
| 個人作品集 | ⭐⭐⭐ |
| 電商 / 品牌 | ⭐ |
| 行銷落地頁 | ⭐ |
| 企業 / B2B | ⭐⭐⭐ |
| 媒體 / 內容 | ⭐⭐⭐ |
| 設計工作室 / Agency | ⭐⭐⭐ |

**AI 視覺指紋強度**：✅ 低
