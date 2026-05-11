# CTA Section

> Conversion-driven section。通常頁尾。**一個** primary CTA，不要兩個競爭。

## Anatomy

- Headline（短，5-8 字）
- 可選：subtitle（解釋）
- Primary CTA button / link
- 可選：social proof line（"Trusted by 10,000+ teams"）

## Canonical HTML

```html
<section class="cta" aria-labelledby="cta-title">
  <h2 id="cta-title">Ready to ship faster?</h2>
  <p>Start building in 30 seconds. No credit card.</p>
  <a href="/start" class="btn-primary">Start free</a>
</section>
```

## Canonical CSS

```css
.cta {
  padding: 6rem 1.25rem;
  text-align: left; /* 不要預設置中 */
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  align-items: flex-start;
}
.cta h2 {
  font-size: clamp(2rem, 6vw, 3.5rem);
  letter-spacing: -0.02em;
  line-height: 1.1;
  max-width: 18ch;
}
@media (min-width: 768px) { .cta { padding: 8rem 2rem; } }
@media (min-width: 1024px) { .cta { padding: 10rem 4rem; } }
```

## 風格輸出對照

| Style | 對齊 | CTA 形式 |
|-------|------|---------|
| Corporate Clean | left or split | rounded button |
| Aurora UI | center 允許 | gradient button + glow |
| Bento Grid | bento-cell CTA | filled block |
| Editorial | left + masthead-style headline | underline link |
| Type-First Monochrome | left, bleed headline | underline link only |
| Minimal Float | left, big whitespace | outline button |
| Dark Luxury | center 允許 | gold outline button |
| **Swiss Editorial** | **left, grid-aligned** | **inline underline link** |
| **Magazine Longform** | **end-of-article style** | **「Read next →」underline** |
| **Fashion / Luxury** | **asymmetric** | **tracked uppercase tiny link** |
| **Brutalist** | **default** | **plain underline `<a>`** |

## Accessibility 必查

- [ ] CTA 用 `<a>`（跳頁）或 `<button>`（觸發行為）
- [ ] CTA 文字明確（不要「Click here」/「Learn more」）
- [ ] Focus-visible 對 bg ≥ 3:1
- [ ] Touch target ≥ 44×44px

## AI Tell 自查

- [ ] **不要** 兩個 button 並排（一個 primary + 一個 secondary）
- [ ] **不要** 永遠置中（左對齊也很好）
- [ ] **不要** 「Get started for free」+ subtitle pill 三件套
- [ ] **不要** 整 section gradient bg + 中間白 button（典型 marketing AI default）
