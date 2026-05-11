# Footer

> 頁尾。Site map + legal + social。預設多 column。Mobile stack。

## Anatomy

- Logo / wordmark + tagline
- Site links（grouped by section）
- Social links
- Newsletter signup（可選）
- Legal（copyright / terms / privacy）
- 可選：language switcher

## Canonical HTML (semantic)

```html
<footer>
  <div class="footer-top">
    <a href="/" class="logo">YourBrand</a>
    <p class="tagline">Build software, faster.</p>
  </div>

  <nav aria-label="Footer" class="footer-nav">
    <div>
      <h3>Product</h3>
      <ul>
        <li><a href="/features">Features</a></li>
        <li><a href="/pricing">Pricing</a></li>
      </ul>
    </div>
    <div>
      <h3>Company</h3>
      <ul>
        <li><a href="/about">About</a></li>
        <li><a href="/careers">Careers</a></li>
      </ul>
    </div>
    <div>
      <h3>Legal</h3>
      <ul>
        <li><a href="/terms">Terms</a></li>
        <li><a href="/privacy">Privacy</a></li>
      </ul>
    </div>
  </nav>

  <ul class="social" aria-label="Social media">
    <li><a href="https://twitter.com/x" aria-label="Twitter">𝕏</a></li>
    <li><a href="https://github.com/x" aria-label="GitHub">GH</a></li>
  </ul>

  <p class="copyright">© 2026 YourBrand</p>
</footer>
```

## Canonical CSS

```css
footer {
  padding: 4rem 1.25rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  border-top: 1px solid var(--color-rule);
}
.footer-nav { display: grid; grid-template-columns: 1fr; gap: 2rem; }
.footer-nav h3 { font-size: 0.875rem; text-transform: uppercase; letter-spacing: 0.08em; }
.footer-nav ul { list-style: none; padding: 0; display: flex; flex-direction: column; gap: 0.5rem; }
.social { display: flex; gap: 1rem; list-style: none; padding: 0; }
.copyright { font-size: 0.875rem; color: var(--color-muted); }
@media (min-width: 768px) {
  footer { padding: 6rem 2rem 2rem; }
  .footer-nav { grid-template-columns: repeat(3, 1fr); }
}
@media (min-width: 1024px) {
  footer { padding: 8rem 4rem 2rem; }
}
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | 4-col with logo + 3 link group |
| Editorial | Masthead-style with credits |
| Type-First Monochrome | huge wordmark + 1 line of small links |
| Swiss Editorial | grid-aligned, numbered, dateline-style |
| Magazine Longform | colophon (印量/字體/credit) |
| Brutalist | `<address>` + plain copyright |
| Fashion / Luxury | tiny tracked uppercase, sidebar |
| Aurora UI | gradient bg, glow accents |
| Bento Grid | bento cells for each section |

## Accessibility 必查

- [ ] `<footer>` 標籤
- [ ] Footer 內 nav 用 `<nav aria-label="Footer">` 跟 main nav 區分
- [ ] Social links 用 `aria-label` 提供 icon 名稱
- [ ] Copyright 用 `<small>` 或 `<p>`
- [ ] Newsletter form 在 footer 內也要 `<label>`

## AI Tell 自查

- [ ] **不要** 永遠 4-column（看內容多少決定）
- [ ] **不要** 「Made with ❤️ in San Francisco」
- [ ] **不要** social icons 用 lucide 整齊配色
