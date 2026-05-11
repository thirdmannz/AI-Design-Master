# FAQ

> Q&A list。**預設用 native `<details><summary>`**，不要自製 accordion。

## Canonical HTML (native, 最 a11y)

```html
<section class="faq" aria-labelledby="faq-title">
  <h2 id="faq-title">FAQ</h2>

  <details>
    <summary>How does billing work?</summary>
    <p>Monthly or yearly, charged on the 1st. Cancel anytime.</p>
  </details>

  <details>
    <summary>Can I self-host?</summary>
    <p>Yes, on Enterprise plan. <a href="/docs/self-host">See docs</a>.</p>
  </details>
</section>
```

## Canonical CSS

```css
.faq { padding: 4rem 1.25rem; max-width: 56rem; margin: 0 auto; }
details {
  border-bottom: 1px solid var(--color-rule);
  padding: 1.25rem 0;
}
summary {
  cursor: pointer;
  list-style: none; /* hide default ▶ */
  font-weight: 500;
  font-size: 1.125rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
summary::-webkit-details-marker { display: none; }
summary::after {
  content: "+";
  font-size: 1.5rem;
  transition: transform 0.2s;
}
details[open] summary::after { content: "−"; }
details p { margin-top: 0.75rem; color: var(--color-muted); }
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | ✅ native details with + / − indicator |
| Editorial | ✅ Q: 跟 A: 前綴 |
| Bento Grid | ✅ 2-col details |
| **Swiss Editorial** | ✅ **numbered (01: Question)** |
| **Magazine Longform** | ✅ **Q&A interview style** |
| **Brutalist** | ✅ **default browser `<details>`，零美化** |
| **Type-First Monochrome** | ✅ **huge typography Q, small A** |

## Accessibility 必查

- [ ] 預設用 `<details><summary>`（native disclosure）
- [ ] 如自製，用 `<button aria-expanded aria-controls>` + 配對 `<div id role="region">`
- [ ] Summary 是 focusable
- [ ] Enter/Space 開合
- [ ] **不要** 用 `<div onClick>` 自製，破壞鍵盤

## 自製版（需要動畫控制時）

```html
<button class="faq-trigger" aria-expanded="false" aria-controls="a-1">
  How does billing work?
</button>
<div id="a-1" role="region" hidden>
  <p>...</p>
</div>
```

## AI Tell 自查

- [ ] **不要** 全部都展開的 FAQ（mobile 太長）
- [ ] **不要** 用 chevron icon 配 lucide
- [ ] **不要** accordion with smooth gradient bg
- [ ] 內容不要每個都 "How do I X? Yes, you can!" 樣板
