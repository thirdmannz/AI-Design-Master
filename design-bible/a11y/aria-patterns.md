# ARIA Patterns

> 常用 ARIA 配方。**優先用 native HTML，ARIA 是補強不是替代**。

## 原則

1. **No ARIA > Bad ARIA**：寧可不寫，不要亂寫
2. Native `<button>` > `role="button"` on `<div>`
3. Native `<dialog>` > `role="dialog"` 包 `<div>`
4. Native `<details>` > 自製 accordion
5. ARIA 只在 native 無法表達的狀態才用（例如 expanded, selected）

## 常用配方

### Button (native)
```html
<button type="button" aria-pressed="false">Toggle</button>
```
Toggle 用 `aria-pressed`，普通 button 不用。

### Disclosure (FAQ / dropdown)

**用 native：**
```html
<details>
  <summary>Question</summary>
  <p>Answer.</p>
</details>
```

**自製版（如需動畫控制）：**
```html
<button aria-expanded="false" aria-controls="answer-1">Question</button>
<div id="answer-1" hidden>Answer.</div>
```

### Modal Dialog

**用 native `<dialog>`：**
```html
<dialog id="modal" aria-labelledby="modal-title">
  <h2 id="modal-title">Title</h2>
  <p>Body</p>
  <button autofocus>Close</button>
</dialog>
```
打開用 `.showModal()`，焦點自動 trap。

### Tabs
```html
<div role="tablist" aria-label="Sections">
  <button role="tab" aria-selected="true" aria-controls="panel-1" id="tab-1">Tab 1</button>
  <button role="tab" aria-selected="false" aria-controls="panel-2" id="tab-2">Tab 2</button>
</div>
<div role="tabpanel" id="panel-1" aria-labelledby="tab-1">Panel 1</div>
<div role="tabpanel" id="panel-2" aria-labelledby="tab-2" hidden>Panel 2</div>
```
鍵盤：左右切換 tab，Tab 進 panel。

### Menu (dropdown nav)
```html
<button aria-expanded="false" aria-haspopup="true" aria-controls="menu-1">Menu ▾</button>
<ul id="menu-1" role="menu" hidden>
  <li role="none"><a role="menuitem" href="#">Item 1</a></li>
</ul>
```

### Live region (Toast / form errors)
```html
<div role="status" aria-live="polite" aria-atomic="true">
  Form saved.
</div>
```
- `polite`：不打斷正在說話的 SR
- `assertive`：error 等緊急訊息（少用）

### Form validation
```html
<label for="email">Email</label>
<input id="email" type="email" aria-invalid="true" aria-describedby="email-error" required>
<span id="email-error" role="alert">Invalid email format.</span>
```

### Skip link
```html
<a href="#main" class="skip-link">Skip to content</a>
<main id="main">...</main>
```
CSS：`.skip-link { position: absolute; left: -9999px; } .skip-link:focus { left: 0; }`

### Image with extended description
```html
<img src="chart.png" alt="Sales chart Q1 2025" aria-describedby="chart-desc">
<p id="chart-desc">Detailed sales breakdown: Jan $10k, Feb $15k...</p>
```

### Loading state
```html
<button aria-busy="true" disabled>
  <span aria-hidden="true">⏳</span>
  Loading...
</button>
```

## 禁用 / 不要寫的

- ❌ `role="button"` on `<div>` — 直接用 `<button>`
- ❌ `aria-label="Click here"` — label 要描述目的，不是動作
- ❌ Redundant role：`<nav role="navigation">` 重複
- ❌ `tabindex="-1"` 用在所有 button — 破壞鍵盤導覽
- ❌ `aria-hidden="true"` on focusable element — focus 跑到 hidden 區
- ❌ `aria-live` 用在持續變動的內容 — 會炸 SR

## Skill 自查

- [ ] 沒有 `role="button"` 在非 `<button>` 元素
- [ ] 所有 modal 用 `<dialog>` 或正確 `role="dialog" aria-modal="true"`
- [ ] FAQ 預設用 `<details>` 不自製
- [ ] Form errors 用 `aria-describedby` + `role="alert"`
- [ ] 沒有 redundant role
