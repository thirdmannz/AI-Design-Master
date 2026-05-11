# Nav

> Site navigation。預設 sticky 或 top-static。Mobile < 768px 變漢堡或 bottom-sheet。

## Anatomy

- Logo / wordmark（連 `/`）
- Primary links（3-5 個）
- 可選：CTA button（試用 / 登入）
- 可選：dark-mode toggle / language switcher
- Mobile：漢堡 button + drawer

## Canonical HTML (semantic)

```html
<nav aria-label="Primary">
  <a href="/" class="logo">YourBrand</a>
  <ul class="nav-links">
    <li><a href="/product">Product</a></li>
    <li><a href="/pricing">Pricing</a></li>
    <li><a href="/docs">Docs</a></li>
  </ul>
  <a href="/login" class="nav-cta">Log in</a>
  <button class="nav-toggle" aria-expanded="false" aria-controls="mobile-menu" aria-label="Menu">☰</button>
</nav>
```

## Canonical CSS

```css
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 1.25rem;
  gap: 1.5rem;
}
.nav-links {
  display: none;
  list-style: none;
  gap: 2rem;
  margin: 0;
  padding: 0;
}
.nav-toggle { display: block; background: transparent; border: 0; font-size: 1.5rem; }
@media (min-width: 768px) {
  .nav-links { display: flex; }
  .nav-toggle { display: none; }
  nav { padding: 1.25rem 2rem; }
}
@media (min-width: 1024px) {
  nav { padding: 1.5rem 4rem; }
}
```

## 風格輸出對照

| Style | Logo 樣式 | Links 樣式 | CTA |
|-------|----------|----------|-----|
| Corporate Clean | wordmark + accent dot | regular weight | rounded button |
| Minimal Float | thin wordmark | uppercase tracking | text link |
| Bento Grid | bento-block logo | regular | filled button |
| Aurora UI | gradient logo（解鎖） | regular | gradient button（解鎖） |
| Glassmorphism | white wordmark | regular on glass nav | pill 解鎖 |
| Neobrutalism | thick logo box | bold uppercase | hard-shadow button |
| Dark Luxury | thin serif | letter-spaced uppercase | gold outline |
| **Swiss Editorial** | **plain wordmark** | **numbered list (01, 02)** | ❌ no button — underline link only |
| **Magazine Longform** | **serif masthead** | **inline serif + dot separator** | ❌ no CTA |
| **Fashion / Luxury** | **tiny tracked uppercase** | **vertical sidebar nav** 或 **minimal top** | ❌ no CTA |
| **Brutalist** | **`<a>` plain text** | **plain underline list** | ❌ |
| **Type-First Monochrome** | **wordmark, no icon** | **bleed-aligned text** | underline link |

## Accessibility 必查

- [ ] `<nav aria-label="Primary">` 必出（多個 nav 時 label 區分）
- [ ] Logo 是 `<a href="/">` 不是 `<div onclick>`
- [ ] Links 用 `<ul><li><a>`，不要 `<div>` 包 `<a>`
- [ ] Mobile toggle button 用 `aria-expanded` + `aria-controls`
- [ ] Dropdown menu 用 `aria-haspopup` + ESC 關閉 + 焦點 trap
- [ ] Skip link 在 nav 之前
- [ ] Current page 用 `aria-current="page"`

## Mobile drawer 行為

- 點 toggle → drawer slide-in from right
- `aria-expanded="true"`
- 焦點移到 drawer 第一個 link
- ESC 或點外面關閉
- 關閉後焦點還給 toggle button

## 框架轉換重點

| Framework | 重點 |
|-----------|------|
| React + Tailwind | shadcn `<NavigationMenu>` 對應；mobile drawer 用 `<Sheet>` |
| Vue + Tailwind | `<script setup>` ref isOpen，`@click` toggle |
| Svelte | `let isOpen = false`，`{#if isOpen}` |
| Astro | static render，mobile toggle 用 inline `<script>` 或 island |
| HTML + CSS | `<details>` 做 mobile drawer（最 a11y） |

## AI Tell 自查

- [ ] 沒有「logo + 5 links + Trial button」標準三件套（要看風格決定）
- [ ] 沒有 floating glass nav（除非 Glassmorphism）
- [ ] 沒有「Try free →」CTA 配 emoji arrow
