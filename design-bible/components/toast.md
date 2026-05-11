# Toast / Notification

> 暫時性通知。**用 `aria-live="polite"`**，不要 assertive 除非緊急。

## Canonical HTML

```html
<div class="toast-region" aria-live="polite" aria-atomic="false">
  <div class="toast" role="status">
    <p>Project saved.</p>
    <button type="button" aria-label="Dismiss">✕</button>
  </div>
</div>
```

## 兩種 toast

- **Success / Info**：`role="status"` + `aria-live="polite"`（不打斷 SR）
- **Error / Critical**：`role="alert"` + `aria-live="assertive"`（立即打斷）

## Canonical CSS

```css
.toast-region {
  position: fixed;
  bottom: 1.5rem;
  right: 1.5rem;
  z-index: 1000;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  max-width: calc(100vw - 3rem);
}
.toast {
  background: var(--color-surface);
  color: var(--color-ink);
  border: 1px solid var(--color-rule);
  border-radius: var(--radius-toast, 8px);
  padding: 0.875rem 1rem;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  box-shadow: 0 8px 24px rgba(0,0,0,0.1);
  animation: toast-in 0.3s ease-out;
}
.toast--success { border-left: 3px solid var(--color-success, #16a34a); }
.toast--error { border-left: 3px solid var(--color-danger, #d63838); }
@keyframes toast-in {
  from { transform: translateY(100%); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}
@media (prefers-reduced-motion: reduce) {
  .toast { animation: none; }
}
@media (max-width: 640px) {
  .toast-region { bottom: 0; right: 0; left: 0; padding: 0.5rem; }
}
```

## 風格輸出對照

| Style | 位置 / 形式 |
|-------|----------|
| Corporate Clean | bottom-right, soft shadow |
| Bento Grid | bento cell-style toast |
| Glassmorphism | backdrop-blur glass toast |
| Brutalist | plain text in top, no animation |
| Swiss Editorial | top-fixed banner, 1px border |
| Type-First Monochrome | inline message, no popup |

## Auto-dismiss timing

- Info / success：3-5 秒
- Warning：5-7 秒
- Error / action required：**不自動消失**（user 必須關）

## Accessibility 必查

- [ ] `role="status"` + `aria-live="polite"` 為 success
- [ ] `role="alert"` + `aria-live="assertive"` 為 error only
- [ ] **不要** `aria-live="assertive"` 用在所有 toast（會打斷 SR）
- [ ] Dismiss button 用 `aria-label="Dismiss"` 或 "Close [message]"
- [ ] Auto-dismiss timer **必須在 hover 時 pause**
- [ ] **prefers-reduced-motion** 尊重（disable slide-in）
- [ ] 多 toast 時 stack，不互蓋

## AI Tell 自查

- [ ] **不要** 用 lucide check-circle / x-circle icon
- [ ] **不要** 萬用 emerald-500 success / red-500 error
- [ ] **不要** toast 永遠 bottom-right（top-right / top-center 也可，看風格）
- [ ] Toast 內容明確（"Saved" 不是 "Success!"）
