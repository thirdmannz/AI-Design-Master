# Features Section

> 列出產品功能。**AI tell 重災區** — 預設輸出永遠是「3-column card grid，每個 card 一個 lucide icon + h3 + p」。要主動破這個。

## 替代版型（不是只有 3-col grid）

1. **3-column card grid**（傳統，AI default — 慎用）
2. **Numbered list**（Swiss / Magazine 適用）
3. **Bento asymmetric grid**（Bento Grid 風格）
4. **Tab/Accordion 切換**（節省垂直空間）
5. **Side-by-side（feature + 對應 illustration/screenshot）**
6. **Editorial paragraph form**（Magazine / Fashion 適用）
7. **Long-form scroll-pinned**（Kinetic）

## Canonical HTML（傳統 3-col）

```html
<section class="features" aria-labelledby="features-title">
  <h2 id="features-title">What you get</h2>
  <ul class="feature-list">
    <li>
      <h3>Fast deploys</h3>
      <p>Push to main, live in 12 seconds.</p>
    </li>
    <li>
      <h3>Type-safe everything</h3>
      <p>TypeScript-native, no escape hatches.</p>
    </li>
    <li>
      <h3>Edge-native</h3>
      <p>Runs in 30 regions by default.</p>
    </li>
  </ul>
</section>
```

> 注意：用 `<ul><li>` 不是 `<div><div>`。Features 是 list，不是裝飾。

## Canonical CSS (Mobile-first)

```css
.features { padding: 4rem 1.25rem; }
.features h2 { font-size: clamp(1.75rem, 5vw, 2.5rem); margin-bottom: 2rem; }
.feature-list {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
}
@media (min-width: 768px) {
  .features { padding: 6rem 2rem; }
  .feature-list { grid-template-columns: repeat(2, 1fr); gap: 2.5rem; }
}
@media (min-width: 1024px) {
  .features { padding: 8rem 4rem; }
  .feature-list { grid-template-columns: repeat(3, 1fr); gap: 3rem; }
}
```

## 風格輸出對照

| Style | 出 / 不出 | 形式 |
|-------|---------|------|
| Corporate Clean | ✅ | 3-col card grid（傳統 OK） |
| Bento Grid | ✅ | 4-6 cell asymmetric bento |
| Aurora UI | ✅ | 3-col with gradient glow |
| Glassmorphism | ✅ | 3-col glass cards |
| Claymorphism | ✅ | 3-col clay cards |
| Editorial Maximal | ✅ | 2-col 或 numbered list |
| Type-First Monochrome | ✅ | numbered sections, no cards |
| Minimal Float | ✅ | 2-col, very wide gap |
| Neobrutalism | ✅ | 3-col with hard shadow + uppercase |
| Dark Luxury | ✅ | 2-col side-by-side w/ photo |
| Organic Nature | ✅ | 3-col with organic blob accents |
| Kinetic Editorial | ✅ | scroll-pinned reveal one-by-one |
| 3D Immersive | ✅ | floating UI over 3D scene |
| **Swiss Editorial** | ⚠️ **替代** | **numbered index (01/02/03) — NOT 3-col card grid** |
| **Magazine Longform** | ❌ **禁出** | 改用 article paragraph form 或 editorial layout |
| **Fashion / Luxury** | ❌ **禁出** | 改用 collection grid 或 lookbook |
| **Brutalist** | ⚠️ **替代** | plain `<ul>` 或 `<dl>` — no styling |

## Accessibility 必查

- [ ] Features 用 `<ul><li>` 不是 `<div>`
- [ ] 每個 feature `<h3>` 階層連續（h2 → h3，不跳階）
- [ ] Icon 是裝飾性時 `aria-hidden="true"`
- [ ] Icon 是 SVG 內含意義時 `<svg role="img"><title>` 給名稱
- [ ] Card 整個可點時用 `<a>` 包 card 或 single button

## AI Tell 自查

- [ ] **不要** 永遠 3-col grid — 考慮 numbered list / bento / side-by-side
- [ ] **不要** 每個 feature 都配 lucide-style icon
- [ ] **不要** icon + h3 + p 三件套整齊對齊
- [ ] **不要** 用 slate-* / gray-* tailwind palette
- [ ] Feature 數量不一定要 3 個 — 5 個、7 個、9 個都可以

## 框架轉換重點

| Framework | 重點 |
|-----------|------|
| React + Tailwind | `<Feature>` 可拆 compound component（`<Feature.Icon>` `<Feature.Title>` `<Feature.Desc>`） |
| Vue + Tailwind | v-for feature in features 跑 array |
| Svelte | `{#each features as f}` |
| Astro | 從 `.md` 或 collection 讀 features，static SSR |
| HTML + CSS | hand-written list，最 brittle 但最快 |
