# Form (Login / Signup / Contact)

> 表單。**Label 必須有，placeholder 不能當 label**。Input font-size ≥ 16px 避免 iOS auto-zoom。

## Anatomy

- `<form>` wrapper
- `<fieldset>` + `<legend>` (groups)
- `<label>` + `<input>` pairs
- Error message linked via `aria-describedby`
- Submit button (`<button type="submit">`)
- 可選：social login buttons

## Canonical HTML (Login)

```html
<form action="/login" method="post" novalidate>
  <h2>Log in</h2>

  <div class="field">
    <label for="email">Email</label>
    <input id="email" name="email" type="email" autocomplete="email" required
           aria-describedby="email-error">
    <span id="email-error" class="error" hidden></span>
  </div>

  <div class="field">
    <label for="password">Password</label>
    <input id="password" name="password" type="password" autocomplete="current-password" required
           minlength="8" aria-describedby="password-hint">
    <span id="password-hint" class="hint">At least 8 characters</span>
  </div>

  <button type="submit" class="btn-primary">Log in</button>

  <p><a href="/forgot">Forgot password?</a></p>
</form>
```

## Canonical CSS

```css
form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  max-width: 28rem;
}
.field { display: flex; flex-direction: column; gap: 0.375rem; }
label { font-weight: 500; font-size: 0.9375rem; }
input, textarea, select {
  font-size: 16px; /* 防 iOS auto-zoom */
  padding: 0.75rem 0.875rem;
  border: 1px solid var(--color-rule);
  background: var(--color-surface, var(--color-bg));
  color: var(--color-ink);
  border-radius: var(--radius-input, 6px);
  font-family: inherit;
  min-height: 44px;
}
input:focus-visible, textarea:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 2px;
  border-color: var(--color-accent);
}
.hint { font-size: 0.8125rem; color: var(--color-muted); }
.error { font-size: 0.875rem; color: var(--color-danger, #d63838); }
input[aria-invalid="true"] { border-color: var(--color-danger); }
```

## 風格輸出對照

| Style | Input 樣式 |
|-------|----------|
| Corporate Clean | rounded 6-8px, subtle border |
| Bento Grid | block-shaped, no radius |
| Aurora UI | gradient focus glow |
| Glassmorphism | glass input with backdrop-blur |
| Claymorphism | inset shadow, large radius |
| Neobrutalism | 2px black border, hard shadow on focus |
| Minimal Float | borderless underline-only |
| Editorial | underline-only, serif label |
| **Swiss Editorial** | **square 0px radius, 1px ink border, baseline aligned** |
| **Magazine Longform** | **handwritten-style underline input** |
| **Fashion / Luxury** | **tracked uppercase label, hairline border** |
| **Brutalist** | **default browser style — no custom CSS** |
| **Type-First Monochrome** | **borderless, underline only, large** |

## Accessibility 必查（最嚴）

- [ ] 每個 input 有 `<label for>`（不只是 placeholder）
- [ ] `autocomplete` 屬性正確（email / current-password / new-password / one-time-code）
- [ ] Required input 有 `required` 屬性，視覺 + SR 都能識別
- [ ] Error 用 `aria-invalid="true"` + `aria-describedby` 連結 error text
- [ ] Error 用 `role="alert"` 或 `aria-live="assertive"` 即時通知
- [ ] Submit button 用 `<button type="submit">`，不是 `<div onclick>`
- [ ] Input min-height ≥ 44px（touch target）
- [ ] Form 在 mobile 時 input font-size ≥ 16px（防 iOS zoom）
- [ ] Group radio / checkbox 用 `<fieldset><legend>`

## Password input 特別注意

- `autocomplete="current-password"` (login) / `"new-password"` (signup)
- 可選：show/hide toggle (`<button aria-label="Show password" aria-pressed="false">`)
- Minlength 顯示，不要靜默 reject

## Validation

```html
<input type="email" required
       pattern="[^@]+@[^@]+\.[^@]+"
       aria-describedby="email-error"
       aria-invalid="false">
<span id="email-error" role="alert"></span>
```

JS validation：
- 失焦驗證（不要即時 keystroke 紅字）
- Submit 時集中 list errors + 焦點移到第一個 error

## AI Tell 自查

- [ ] **不要** 用 placeholder 取代 label（placeholder 一輸入就消失）
- [ ] **不要** 「Email *」紅星，用 `<abbr title="required">*</abbr>` 或寫 "(required)"
- [ ] **不要** social login 三件套（Google / GitHub / Apple）固定順序
- [ ] **不要** 「By clicking, you agree to...」綁定 submit button
- [ ] **不要** error 用 toast / animation 通知（在 input 下方 inline）
