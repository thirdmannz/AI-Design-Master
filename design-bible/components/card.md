# Card

> 通用容器。**不是所有風格都該用 card**。Swiss / Magazine / Brutalist 不用 card。

## Anatomy

- 容器（border / shadow / surface）
- Heading
- Body content
- 可選：image / icon
- 可選：CTA / link

## Canonical HTML

```html
<article class="card">
  <h3>Card title</h3>
  <p>Card body content here.</p>
  <a href="/learn">Learn more</a>
</article>
```

> 用 `<article>` 如內容獨立（如 blog post card），用 `<div>` 如純 layout。

## Canonical CSS

```css
.card {
  background: var(--color-surface);
  border: 1px solid var(--color-rule);
  border-radius: var(--radius-card, 8px);
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}
.card h3 { margin: 0; font-size: 1.25rem; }
.card p { margin: 0; color: var(--color-muted); }
.card a { margin-top: auto; }
```

## 風格輸出對照

| Style | 出/不出 | 樣式 |
|-------|--------|------|
| Corporate Clean | ✅ subtle border + soft shadow |
| Bento Grid | ✅ **本就是 bento cell** |
| Glassmorphism | ✅ backdrop-blur + rgba border |
| Aurora UI | ✅ gradient border glow |
| Claymorphism | ✅ rounded clay, inset shadow |
| Neobrutalism | ✅ 2px black border + 4px hard shadow |
| Minimal Float | ✅ borderless, soft shadow |
| Dark Luxury | ✅ dark surface + thin border |
| Organic Nature | ✅ organic radius + soft shadow |
| Editorial Maximal | ⚠️ 用 article layout，避免 card |
| Kinetic Editorial | ⚠️ scroll-animated card |
| 3D Immersive | ✅ floating glass UI |
| **Swiss Editorial** | ❌ **禁出** — baseline grid 分隔 |
| **Magazine Longform** | ❌ **禁出** — article 不切 card |
| **Fashion / Luxury** | ❌ **禁出** — 用 lookbook image |
| **Brutalist** | ❌ **禁出** — 用 `<hr>` 或 plain `<article>` |
| **Type-First Monochrome** | ❌ **禁出** — typography 做 hierarchy |

## 5 種 card variants

1. **Info card**：icon + h3 + p（features）
2. **Stat card**：number + label（dashboard）
3. **Image card**：cover image + title + meta（blog）
4. **Profile card**：avatar + name + role
5. **Pricing card**：plan + price + features list

## Accessibility 必查

- [ ] Card 包 link 時用 `<a>` 包整個 card 或 single internal `<a>`，不要多個 `<a>` 競爭
- [ ] 如 card 全部可點，「Read more」link 用 `aria-label` 含 card title (e.g. `aria-label="Read more about [title]"`)
- [ ] Card image 有 `alt`
- [ ] Card 順序：image / icon → heading → body → link

## AI Tell 自查

- [ ] **不要** 永遠都 card — Swiss/Brutalist/Magazine 不該有 card
- [ ] **不要** `box-shadow: 0 2px 4px rgba(0,0,0,0.1)` 萬用陰影
- [ ] **不要** 「Floating card with subtle backdrop」 default
- [ ] Card 數量 ≠ 3（4 / 5 / 7 都可以）
