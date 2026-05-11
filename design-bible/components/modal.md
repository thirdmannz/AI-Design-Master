# Modal / Dialog

> **用 native `<dialog>`**，不要自製 `<div role="dialog">`。

## 為什麼用 native `<dialog>`

- 自動 focus trap
- 自動 ESC 關閉
- `::backdrop` 樣式 hook
- `showModal()` / `close()` API
- Inert page 外其他內容（自動）

## Canonical HTML

```html
<dialog id="confirm" aria-labelledby="confirm-title">
  <header>
    <h2 id="confirm-title">Delete project?</h2>
    <button type="button" autofocus aria-label="Close" data-close>✕</button>
  </header>
  <p>This will permanently delete the project and all its data. This action cannot be undone.</p>
  <footer>
    <button type="button" data-close>Cancel</button>
    <button type="button" class="btn-danger">Delete</button>
  </footer>
</dialog>

<button onclick="document.getElementById('confirm').showModal()">Delete</button>
```

```js
document.querySelectorAll('[data-close]').forEach(btn =>
  btn.addEventListener('click', () => btn.closest('dialog').close())
);
```

## Canonical CSS

```css
dialog {
  border: 0;
  border-radius: var(--radius-modal, 12px);
  background: var(--color-surface);
  color: var(--color-ink);
  padding: 1.5rem;
  max-width: 28rem;
  width: calc(100% - 2rem);
  margin: auto;
  box-shadow: 0 24px 64px rgba(0,0,0,0.2);
}
dialog::backdrop {
  background: rgba(0,0,0,0.6);
  backdrop-filter: blur(4px);
}
dialog header {
  display: flex;
  justify-content: space-between;
  align-items: start;
  gap: 1rem;
}
dialog footer {
  display: flex;
  justify-content: flex-end;
  gap: 0.75rem;
  margin-top: 1.5rem;
}
```

## Mobile (bottom sheet 變體)

```css
@media (max-width: 640px) {
  dialog {
    max-width: 100%;
    width: 100%;
    margin: auto 0 0;
    border-radius: 16px 16px 0 0;
    animation: slide-up 0.3s ease-out;
  }
  @keyframes slide-up {
    from { transform: translateY(100%); }
    to { transform: translateY(0); }
  }
}
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | rounded, soft shadow |
| Glassmorphism | backdrop-blur on `::backdrop` |
| Bento Grid | bento-style modal cells |
| Neobrutalism | 2px black border + hard shadow |
| Brutalist | default browser dialog style |
| Type-First Monochrome | minimal, type-driven |
| Swiss Editorial | 1px border, no radius, baseline grid |

## Accessibility 必查（最嚴 — modal 最容易出 a11y 問題）

- [ ] 用 `<dialog>` 不是 `<div role="dialog">`
- [ ] `showModal()` 不是 `show()`（show 不 trap focus）
- [ ] `aria-labelledby` 連結 modal title
- [ ] 首個 focusable element 自動 focus（`autofocus`）
- [ ] ESC 自動關閉（native 行為）
- [ ] 關閉後焦點還給觸發 button（自製需要記住）
- [ ] Backdrop click 關閉 = 可選（destructive action 別讓）
- [ ] **不要** modal 內又開 modal（除非真的必要）

## Confirmation modal 必含

```html
<button data-close>Cancel</button>
<button class="btn-danger">Delete</button>
```

Destructive action（delete）放右邊，Cancel 左邊。Cancel 顏色 neutral。

## AI Tell 自查

- [ ] **不要** 用 `<div role="dialog">` — 用 `<dialog>` native
- [ ] **不要** 萬用「X」icon button right-top
- [ ] **不要** 「Are you sure?」+ 兩個一樣大的 button
- [ ] Destructive action 用明確動詞（"Delete" 不是 "OK"）
