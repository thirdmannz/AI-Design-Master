# Plain HTML + CSS

> 純 HTML 加 CSS Custom Properties。沒框架、沒 build step。**最 a11y、最快、最久不過時**。

## 為什麼選這個

- Zero build dependencies
- 任何瀏覽器秒開（沒 JS bundle）
- 完全可被 search engine 索引
- 100% a11y if 用 semantic tags
- 適合 portfolio / blog / docs / 一次性 landing page

## 檔案結構

```
project/
├── index.html
├── about.html
├── contact.html
├── styles/
│   ├── tokens.css        ← :root variables
│   ├── reset.css         ← CSS reset
│   ├── base.css          ← typography / globals
│   └── components.css    ← .hero / .nav / .card 等
├── assets/
│   ├── logo.svg
│   └── photos/
└── 404.html
```

## Token 接入

`styles/tokens.css`：

```css
:root {
  --color-bg: #fafaf7;
  --color-ink: #0a0a0a;
  --color-muted: rgba(10,10,10,0.6);
  --color-accent: #2c5fff;
  --color-rule: rgba(10,10,10,0.1);

  --font-display: "Inter Tight", system-ui, sans-serif;
  --font-body: "Inter", system-ui, sans-serif;
  --font-mono: "JetBrains Mono", monospace;

  --bp-sm: 640px;
  --bp-md: 768px;
  --bp-lg: 1024px;

  --radius-md: 6px;
  --shadow-card: 0 8px 24px rgba(0,0,0,0.06);
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0a0a0a;
    --color-ink: #fafafa;
    --color-muted: rgba(250,250,250,0.6);
    --color-rule: rgba(255,255,255,0.1);
  }
}
```

## Reset

```css
/* styles/reset.css */
*, *::before, *::after { box-sizing: border-box; }
* { margin: 0; }
html { -moz-text-size-adjust: none; -webkit-text-size-adjust: none; text-size-adjust: none; }
body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
}
img, picture, video, canvas, svg { display: block; max-width: 100%; }
input, button, textarea, select { font: inherit; }
p, h1, h2, h3, h4, h5, h6 { overflow-wrap: break-word; }
```

## Canonical Hero 範例

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Build software, faster — YourBrand</title>
  <meta name="description" content="A single platform for shipping production code." />
  <link rel="stylesheet" href="/styles/tokens.css" />
  <link rel="stylesheet" href="/styles/reset.css" />
  <link rel="stylesheet" href="/styles/base.css" />
  <link rel="stylesheet" href="/styles/components.css" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@500;700&family=Inter:wght@400;500&display=swap" rel="stylesheet" />
</head>
<body>
  <a href="#main" class="skip-link">Skip to content</a>
  <nav aria-label="Primary">...</nav>

  <main id="main">
    <section class="hero" aria-labelledby="hero-title">
      <h1 id="hero-title">Build software, faster.</h1>
      <p class="lede">A single platform for shipping production code.</p>
      <a href="/start" class="btn-primary">Start free</a>
    </section>
  </main>

  <footer>...</footer>
</body>
</html>
```

```css
/* styles/components.css */
.skip-link {
  position: absolute;
  top: -100px;
  left: 0;
  padding: 0.75rem 1rem;
  background: var(--color-bg);
  color: var(--color-ink);
  text-decoration: underline;
  z-index: 100;
  transition: top 0.2s;
}
.skip-link:focus { top: 0; }

.hero {
  padding: 4rem 1.25rem;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 1.25rem;
}
.hero h1 {
  font-family: var(--font-display);
  font-size: clamp(2.25rem, 8vw, 3.5rem);
  line-height: 1.05;
  letter-spacing: -0.025em;
  max-width: 18ch;
}
.lede {
  font-family: var(--font-body);
  font-size: 1.0625rem;
  color: var(--color-muted);
  max-width: 52ch;
}
.btn-primary {
  display: inline-flex;
  background: var(--color-accent);
  color: white;
  padding: 0.875rem 2rem;
  border-radius: var(--radius-md);
  text-decoration: none;
  font-weight: 600;
  transition: transform 0.2s;
}
.btn-primary:hover { transform: translateY(-2px); }
.btn-primary:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 2px;
}

@media (min-width: 768px) { .hero { padding: 6rem 2rem; } }
@media (min-width: 1024px) {
  .hero { padding: 8rem 4rem; }
  .hero h1 { font-size: clamp(3rem, 6vw, 6rem); }
}
```

## Interactive widgets (沒框架)

### 漢堡 nav (用 `<details>`)

```html
<details class="mobile-nav">
  <summary aria-label="Menu">☰</summary>
  <ul>
    <li><a href="/product">Product</a></li>
    <li><a href="/pricing">Pricing</a></li>
  </ul>
</details>
```

### FAQ accordion (用 `<details>`)

```html
<details>
  <summary>How does billing work?</summary>
  <p>Monthly or yearly.</p>
</details>
```

### Modal (用 native `<dialog>`)

```html
<dialog id="confirm" aria-labelledby="t">
  <h2 id="t">Confirm</h2>
  <form method="dialog">
    <button>Cancel</button>
    <button value="ok">OK</button>
  </form>
</dialog>

<script>
  document.querySelector('[data-open="confirm"]').addEventListener('click', () =>
    document.getElementById('confirm').showModal()
  );
</script>
```

### Smooth scroll

```css
html { scroll-behavior: smooth; }
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
}
```

## Form (沒框架)

```html
<form action="/api/subscribe" method="POST" novalidate>
  <label for="email">Email</label>
  <input id="email" name="email" type="email" required autocomplete="email" />
  <button type="submit">Subscribe</button>
</form>
```

支援 PE：JS validate + 預設 server submit fallback。

## A11y 優勢

- 用 semantic HTML 自動 a11y
- 沒 JS 也能 navigate（最強 PE / fallback）
- 不會因為 hydration 出 bug
- Reader mode 友善

## 部署

- GitHub Pages / Cloudflare Pages / Netlify free tier
- 直接 drag-and-drop `index.html` + assets
- 加 `_redirects` 做 SPA-like routing (Netlify)

## AI Tell 自查

- [ ] **善用** native HTML 元件（不要重做 `<details>` `<dialog>`）
- [ ] **不要** inline `<script>` blocks 灑全頁
- [ ] **不要** CSS 用 `!important` 蓋特異性
- [ ] **不要** 萬用 `<div class="container">` 包整個 hero（用 `<section>` `<main>`）
