# Blog Index / Post Card

> Blog 列表頁 + 個別文章版型。

## Blog index canonical HTML

```html
<main>
  <header>
    <h1>Blog</h1>
    <p>Notes on building software.</p>
  </header>
  <ul class="post-list">
    <li>
      <article>
        <a href="/post/foo">
          <time datetime="2026-05-01">May 1, 2026</time>
          <h2>Title here</h2>
          <p>Excerpt.</p>
        </a>
      </article>
    </li>
  </ul>
</main>
```

## Blog post canonical HTML

```html
<article>
  <header>
    <p class="kicker">Engineering</p>
    <h1>Article title</h1>
    <p class="lede">One-line summary that explains the angle.</p>
    <p class="meta">
      <time datetime="2026-05-01">May 1, 2026</time>
      <span>·</span>
      <address>By <a href="/author/lin">Lin Chao</a></address>
    </p>
  </header>
  <p>Body paragraph here.</p>
  <h2>Section heading</h2>
  <p>More body.</p>
</article>
```

## Canonical CSS (index)

```css
.post-list { list-style: none; padding: 0; display: grid; gap: 2rem; }
.post-list article a { display: block; text-decoration: none; color: inherit; }
.post-list time { font-size: 0.875rem; color: var(--color-muted); }
.post-list h2 { font-size: 1.5rem; margin: 0.5rem 0; }
@media (min-width: 768px) { .post-list { grid-template-columns: repeat(2, 1fr); } }
@media (min-width: 1024px) { .post-list { grid-template-columns: repeat(3, 1fr); } }
```

## Post body typography

```css
article { max-width: 68ch; margin: 0 auto; }
article p { font-size: 1.125rem; line-height: 1.6; }
article h2 { font-size: 1.75rem; margin-top: 2.5rem; }
article h3 { font-size: 1.375rem; margin-top: 2rem; }
.kicker { text-transform: uppercase; letter-spacing: 0.08em; font-size: 0.8125rem; color: var(--color-accent); }
.lede { font-size: 1.25rem; color: var(--color-muted); }
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Editorial Maximal | ✅ **canonical fit** — kicker + lede + serif body |
| Magazine Longform | ✅ **best fit** — drop cap, marginalia, pull quote |
| Swiss Editorial | ✅ numbered articles, baseline grid, no images |
| Type-First Monochrome | ✅ huge headlines, minimal meta |
| Corporate Clean | ⚠️ 簡化 — card grid |
| Brutalist | ✅ default browser style + `<address>` |
| Bento Grid | ⚠️ 不適合（blog 不該 bento） |
| Aurora / Glass / Clay | ❌ 不適合 blog 語境 |
| **Fashion / Luxury** | ⚠️ lookbook style，每篇 full-bleed photo |

## Magazine 特例

- Drop cap：第一段第一字 `first-letter` style
- Marginalia：`<aside>` 在 article 側邊
- Pull quote：`<blockquote>` 大字插入

```css
article p:first-of-type::first-letter {
  font-family: var(--font-display);
  font-size: 5rem;
  line-height: 1;
  float: left;
  padding: 0.5rem 0.5rem 0 0;
}
```

## Accessibility 必查

- [ ] `<article>` for each post
- [ ] `<time datetime>` machine-readable
- [ ] `<address>` for author
- [ ] `<h1>` 是 post title, `<h2>` 是 sections（不跳階）
- [ ] Code blocks 用 `<pre><code>`，syntax highlighting 不靠顏色傳達語意

## AI Tell 自查

- [ ] **不要** 永遠 「Hero image + Title + Excerpt」blog card 三件套
- [ ] **不要** 用 lucide icon 標 category
- [ ] **不要** 「3 min read」用 icon + 數字（用 plain text）
- [ ] 用 `<time>` 真實日期格式，不要「May 1, 2026」固定樣板
