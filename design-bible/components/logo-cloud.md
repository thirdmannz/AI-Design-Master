# Logo Cloud (Trusted By)

> 「Trusted by 10k+ teams」logo 列。**這是 AI Tell #6** — 不是所有風格都該出。

## ⚠️ AI Tell 警告

Logo cloud 在 hero 下方緊跟，是當代 SaaS 模板最常見的 AI tell。預設**只在以下情況輸出**：
- Corporate Clean
- Bento Grid
- 明確的 B2B SaaS use case

**禁出於**：
- Swiss Editorial
- Magazine Longform
- Fashion / Luxury
- Brutalist
- Type-First Monochrome

## Anatomy

- 上方 lede（"Trusted by..." / "Used by..."）
- Logo list
- 可選：count badge ("10,000+ teams")

## Canonical HTML

```html
<section class="logo-cloud" aria-label="Trusted by these companies">
  <p>Trusted by teams at</p>
  <ul>
    <li><img src="/logos/stripe.svg" alt="Stripe" width="120" height="32"></li>
    <li><img src="/logos/figma.svg" alt="Figma" width="120" height="32"></li>
    <li><img src="/logos/notion.svg" alt="Notion" width="120" height="32"></li>
  </ul>
</section>
```

## Canonical CSS

```css
.logo-cloud {
  padding: 3rem 1.25rem;
  text-align: center;
}
.logo-cloud p {
  font-size: 0.875rem;
  color: var(--color-muted);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 2rem;
}
.logo-cloud ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 2rem 3rem;
}
.logo-cloud img {
  height: 28px;
  width: auto;
  opacity: 0.6;
  filter: grayscale(100%);
  transition: opacity 0.2s, filter 0.2s;
}
.logo-cloud img:hover {
  opacity: 1;
  filter: grayscale(0);
}
```

## 風格輸出對照

| Style | 出/不出 |
|-------|--------|
| Corporate Clean | ✅ classic grayscale logo row |
| Bento Grid | ✅ bento cell with grayscale logos |
| Aurora UI | ⚠️ 解鎖 — glow on hover |
| Glassmorphism | ⚠️ 解鎖 — glass tile per logo |
| Minimal Float | ⚠️ small spacing, big margin |
| Dark Luxury | ⚠️ white logos on dark bg |
| Neobrutalism | ❌ 用 client name list 替代 |
| Editorial Maximal | ⚠️ 用 「Featured in: TechCrunch, Wired, Verge」inline text |
| **Swiss Editorial** | ❌ **禁出** — 用 numbered client list |
| **Magazine Longform** | ❌ **禁出** — 不需要 |
| **Fashion / Luxury** | ❌ **禁出** — luxury 不 cloud |
| **Brutalist** | ❌ **禁出** — 用純文字 client list |
| **Type-First Monochrome** | ❌ **禁出** — 用 typography 表達 |

## 替代方案（不用 logo cloud）

1. **Numbered client list**：「01 Stripe / 02 Notion / 03 Figma」
2. **Inline mention**：「As seen in TechCrunch, Wired, Bloomberg」
3. **Case study links**：3 個 link-style cases，不是 logo
4. **Stats reference**：「50,000 teams across 80 countries」no logos

## Accessibility 必查

- [ ] Logos 用 `<img>` with `alt` (公司名)
- [ ] Logo list 用 `<ul><li>`
- [ ] Section 有 `aria-label` 或 heading
- [ ] Grayscale filter 是視覺，不能影響語意

## AI Tell 自查

- [ ] **不要** 預設出 logo cloud — 多數風格不該有
- [ ] **不要** Hero 緊跟 logo cloud（中間要有 spacing / 別的 section）
- [ ] **不要** 「+10,000 teams」自動 mock
- [ ] 用真實合作 logo，不是假的「Stripe Figma Notion Vercel Linear」AI default 五件套
