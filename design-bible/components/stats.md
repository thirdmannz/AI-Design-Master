# Stats / Counter

> Numeric showcases。用 `<dl><dt><dd>` 不要 `<div>`。

## Canonical HTML

```html
<section class="stats" aria-labelledby="stats-title">
  <h2 id="stats-title">Built for scale</h2>
  <dl>
    <div>
      <dt>Deployments per day</dt>
      <dd><strong>12M+</strong></dd>
    </div>
    <div>
      <dt>Active teams</dt>
      <dd><strong>50,000</strong></dd>
    </div>
    <div>
      <dt>p99 latency</dt>
      <dd><strong>42ms</strong></dd>
    </div>
  </dl>
</section>
```

## Canonical CSS

```css
.stats dl {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
  padding: 0;
  margin: 0;
}
.stats dt {
  font-size: 0.875rem;
  color: var(--color-muted);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}
.stats dd { margin: 0.25rem 0 0; }
.stats strong {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 8vw, 5rem);
  letter-spacing: -0.03em;
  line-height: 1;
  font-feature-settings: "tnum"; /* tabular numerals */
}
@media (min-width: 768px) {
  .stats dl { grid-template-columns: repeat(3, 1fr); }
}
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Bento Grid | ✅ **首選** — bento cell 大數字 |
| Editorial Maximal | ✅ huge serif number |
| Magazine Longform | ✅ 散在 article 中 |
| Type-First Monochrome | ✅ **bleed huge number** |
| Corporate Clean | ✅ 3-col with icon |
| Aurora UI | ✅ glow number |
| Glassmorphism | ✅ glass stat tiles |
| Swiss Editorial | ✅ baseline-aligned, no card |
| **Brutalist** | ✅ **plain `<dl>` browser default** |
| **Fashion / Luxury** | ❌ ban — luxury 不誇數字 |

## Accessibility 必查

- [ ] 用 `<dl>` 不是 `<div>`
- [ ] Number 用 `<strong>`，label 用 `<dt>`
- [ ] Number 用 tabular numerals (`font-feature-settings: "tnum"`)
- [ ] 數字單位（M / K / +）跟數字同字級，SR 讀完整: "12 million plus"
- [ ] 動畫 count-up 用 `prefers-reduced-motion` 尊重

## AI Tell 自查

- [ ] **不要** 永遠 4 個 stats（3 / 5 都可以）
- [ ] **不要** 用 lucide icon 配每個 stat
- [ ] **不要** count-up animation 自動播放（accessibility 問題 + AI tell）
- [ ] **不要** stat 用 gradient text fill
