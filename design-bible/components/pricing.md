# Pricing

> Plan card grid 或 comparison table。預設 3-tier（Starter / Pro / Enterprise）。

## Anatomy

- Plan title
- Price (per period)
- 可選：billing toggle（monthly/yearly）
- Feature list（含 / 不含 用 ✓ ✗）
- CTA per plan
- 可選：「Most popular」highlight

## Canonical HTML (semantic)

```html
<section class="pricing" aria-labelledby="pricing-title">
  <h2 id="pricing-title">Pricing</h2>

  <div class="billing-toggle">
    <button type="button" aria-pressed="true">Monthly</button>
    <button type="button" aria-pressed="false">Yearly (-20%)</button>
  </div>

  <ul class="plans">
    <li class="plan">
      <h3>Starter</h3>
      <p class="price"><strong>$0</strong><span> / mo</span></p>
      <ul class="plan-features">
        <li>Up to 3 projects</li>
        <li>Community support</li>
      </ul>
      <a href="/start" class="btn-outline">Start free</a>
    </li>
    <li class="plan plan--popular" aria-label="Pro plan, most popular">
      <p class="badge">Most popular</p>
      <h3>Pro</h3>
      <p class="price"><strong>$24</strong><span> / mo</span></p>
      <ul class="plan-features">
        <li>Unlimited projects</li>
        <li>Email support</li>
      </ul>
      <a href="/checkout" class="btn-primary">Start trial</a>
    </li>
    <li class="plan">
      <h3>Enterprise</h3>
      <p class="price"><strong>Custom</strong></p>
      <ul class="plan-features">
        <li>SSO + audit log</li>
        <li>Dedicated support</li>
      </ul>
      <a href="/contact" class="btn-outline">Contact sales</a>
    </li>
  </ul>
</section>
```

## Canonical CSS

```css
.pricing { padding: 4rem 1.25rem; }
.plans {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}
.plan {
  border: 1px solid var(--color-rule);
  padding: 2rem 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.plan--popular { border-color: var(--color-accent); border-width: 2px; }
.price strong { font-size: 2.5rem; font-family: var(--font-display); }
.plan-features { list-style: none; padding: 0; }
.plan-features li::before { content: "→ "; }
@media (min-width: 768px) { .plans { grid-template-columns: repeat(2, 1fr); } }
@media (min-width: 1024px) { .plans { grid-template-columns: repeat(3, 1fr); } }
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | ✅ 3-col card with popular highlight |
| Aurora UI | ✅ glow on popular card |
| Glassmorphism | ✅ glass cards |
| Bento Grid | ✅ 3-cell bento layout |
| Claymorphism | ✅ rounded clay cards |
| Type-First Monochrome | ✅ left-aligned, no cards, numbered (01 Starter / 02 Pro) |
| Editorial | ✅ table form, no cards |
| Corporate Clean (B2B) | ✅ comparison matrix |
| **Swiss Editorial** | ⚠️ **table form, baseline-aligned, numbered, no card** |
| **Magazine Longform** | ❌ **禁出** — magazine 不賣 SaaS |
| **Fashion / Luxury** | ❌ **禁出** — 改用 lookbook |
| **Brutalist** | ⚠️ plain `<table>` + raw `<form>` to subscribe |
| **Type-First Monochrome** | ✅ huge numbered tiers, no card border |

## Pricing comparison table（B2B 變體）

```html
<table>
  <caption>Plans comparison</caption>
  <thead>
    <tr>
      <th scope="col">Feature</th>
      <th scope="col">Starter</th>
      <th scope="col">Pro</th>
      <th scope="col">Enterprise</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Projects</th>
      <td>3</td><td>Unlimited</td><td>Unlimited</td>
    </tr>
    <tr>
      <th scope="row">SSO</th>
      <td>—</td><td>—</td><td>✓</td>
    </tr>
  </tbody>
</table>
```

## Accessibility 必查

- [ ] Plans 是 `<ul><li>` (list) 不是 `<div>`
- [ ] Price 用 `<strong>` 標重點，數字 + unit 拆 element
- [ ] Billing toggle 用 `<button aria-pressed>` not radio
- [ ] Comparison table 用 `<table>` 真的 tabular data
- [ ] 「Most popular」用 `aria-label` 不是只靠視覺
- [ ] CTA 每個 plan 一個（不要連續 3 個一樣的 button label）

## AI Tell 自查

- [ ] **不要** 「中間 card 比較大 + 漸層邊框」AI default
- [ ] **不要** ✓ 用 emerald-500 / ✗ 用 red-500（用 ink/muted）
- [ ] **不要** 「Save 20%」用黃色 badge pill
- [ ] **不要** 永遠 3 tier — 2 tier、4 tier、單 tier 都可以

## 框架轉換重點

| Framework | 重點 |
|-----------|------|
| React + Tailwind | shadcn `<Card>` 對應；billing state 用 `useState` |
| Vue + Tailwind | `v-model="billing"` |
| Svelte | `let billing = 'monthly'` |
| Astro | content collection 讀 plans yaml |
| HTML + CSS | hand-write，no JS for static pricing |
