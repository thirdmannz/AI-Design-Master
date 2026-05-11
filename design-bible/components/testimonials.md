# Testimonials

> Customer quotes / 推薦語。**用 `<blockquote>` 不是 `<div>`**。

## Anatomy

- Quote text
- Cite (name + role + 可選 company logo / photo)
- 可選：5-star rating

## Canonical HTML

```html
<section class="testimonials" aria-labelledby="t-title">
  <h2 id="t-title">What teams say</h2>
  <ul>
    <li>
      <blockquote>
        <p>"Shipping became 3x faster. Real."</p>
      </blockquote>
      <figcaption>
        <cite>Lin Chao</cite>
        <span>VP Eng, Acme</span>
      </figcaption>
    </li>
  </ul>
</section>
```

## Canonical CSS

```css
.testimonials ul { list-style: none; padding: 0; display: grid; gap: 2rem; }
blockquote { margin: 0; }
blockquote p { font-size: 1.25rem; line-height: 1.5; quotes: """ """; }
blockquote p::before { content: open-quote; }
blockquote p::after { content: close-quote; }
figcaption { margin-top: 1rem; font-size: 0.9375rem; }
cite { font-weight: 600; font-style: normal; }
@media (min-width: 768px) { .testimonials ul { grid-template-columns: repeat(2, 1fr); } }
@media (min-width: 1024px) { .testimonials ul { grid-template-columns: repeat(3, 1fr); } }
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | ✅ 3-col card with photo + quote |
| Editorial | ✅ pull-quote style, large serif |
| Bento Grid | ✅ bento cell with quote |
| Magazine Longform | ✅ pull-quote in article |
| **Swiss Editorial** | ⚠️ **numbered, no card, baseline aligned** |
| **Brutalist** | ⚠️ **`<blockquote>` plain, no styling** |
| **Type-First Monochrome** | ⚠️ **huge quote, no avatar** |
| **Fashion / Luxury** | ❌ ban — 用 editorial review citation 替代 |

## Accessibility 必查

- [ ] `<blockquote>` not `<div>`
- [ ] `<cite>` for attribution name
- [ ] Avatar image 有 `alt` (人名)
- [ ] Rating 用 `aria-label="4 out of 5 stars"`，不要只靠 ★ 顯示

## AI Tell 自查

- [ ] **不要** 永遠 3-col with circular avatar
- [ ] **不要** 5-star 用 yellow/gold lucide icons
- [ ] **不要** 「★★★★★ 5.0」固定樣式
- [ ] 用真實名字（不要 "Sarah Johnson, CEO" template）
