# Semantic HTML Patterns

> 每個元件輸出的預設標籤對照。Skill 在 Step 3 出 component code 時，必須用對應的語意標籤，不能全部都是 `<div>`。

## 元件 × Semantic tag 對照

| 元件 | 主標籤 | 子標籤 | 備註 |
|------|--------|--------|------|
| Page wrapper | `<body>` | — | — |
| Site nav | `<nav>` + `aria-label="Primary"` | `<ul><li><a>` | 不要用 `<div>` 包 link |
| Main content | `<main>` (1 per page) | — | — |
| Hero | `<section>` + `aria-labelledby` | `<h1>` | h1 一頁只有一個 |
| Features section | `<section>` + `aria-labelledby` | `<h2>` | — |
| Feature card | `<article>` 或 `<div role="group">` | `<h3>` | 有完整資訊用 article |
| Pricing | `<section>` | `<h2>`, `<ul>` for plans | plan benefits 是 `<ul>` |
| Testimonial | `<blockquote>` + `<cite>` | `<p>` | 不要用 `<div>` |
| FAQ | `<section>` + `<details><summary>` | — | native disclosure 優先 |
| CTA | `<section>` | `<a>` 或 `<button>` | 看是否導向另一頁 |
| Footer | `<footer>` | `<nav aria-label="Footer">` | — |
| Forms | `<form>` | `<fieldset><legend>`, `<label>` | label 永遠跟 input 配 |
| Input | `<input>` + `<label for>` | — | placeholder 不能當 label |
| Card | `<article>` 有獨立內容 / `<div>` 純裝飾 | `<h3>` | — |
| Table | `<table>` + `<caption>` | `<thead><th scope>` | data 用 table，不用 grid div |
| Stats | `<dl><dt><dd>` | — | 不要用 `<div>` |
| Logo cloud | `<ul>` | `<li><img alt>` | alt 要寫公司名 |
| Blog index | `<main>` + `<article>` per post | `<h2><time>` | — |
| Blog post | `<article>` | `<h1><time><address>` | author 用 address |
| Empty state | `<section role="status">` | — | screen reader 會讀 |
| 404 | `<main>` + `<h1>` | — | h1 寫 404，不寫 logo |
| Modal | `<dialog>` (native) | `<h2>` | 用 native dialog |
| Toast | `<div role="status" aria-live="polite">` | — | 即時通知用 polite |

## 規則摘要

1. **`<h1>` 每頁一個** — 通常是 hero headline
2. **Heading hierarchy 不跳階** — h1 → h2 → h3，不直接 h1 → h3
3. **Link vs Button**：跳頁面用 `<a>`，觸發動作用 `<button>`
4. **Image alt**：裝飾性 `alt=""`，內容性寫描述；不可省略 alt
5. **Form label**：每個 input 必須有 `<label>` 或 `aria-label`
6. **List**：列表狀東西（nav items、features、testimonials）一律 `<ul>`，不要 `<div>`
7. **Table**：只用於 tabular data，不用於 layout

## 風格特例

- **Brutalist**：可用 `<pre>` 包大塊純文字、`<address>` 寫聯絡，全用瀏覽器預設樣式
- **Magazine Longform**：必出 `<article>` + `<time datetime>` + `<address>` 寫 author
- **Swiss Editorial**：`<ol>` numbered index 不要 disabled list-style
- **Type-First Monochrome**：`<h1>` size 巨大但仍是 h1（不要降為 h2 配 CSS 放大）

## Skill 在 Step 3 必跑檢查

- [ ] 一頁只一個 `<h1>`
- [ ] Heading hierarchy 連續（h1→h2→h3 不跳階）
- [ ] 所有 `<img>` 有 `alt` 屬性
- [ ] 所有 form `<input>` 有 `<label>`
- [ ] Site nav 用 `<nav>` 不是 `<div>`
- [ ] 主內容區用 `<main>`
- [ ] 沒有 div soup（連續 4+ 層 `<div>` 沒語意標籤）
