# Loading / Skeleton

> 載入狀態。**Skeleton > Spinner** 在大多數情況。Skeleton 預示 layout 不打斷感官。

## 3 種 loading strategies

1. **Skeleton screen** — 顯示 layout placeholder（最推薦）
2. **Spinner** — 短時間 (<1s) 操作（form submit）
3. **Progress bar** — 已知進度（upload）

## Skeleton canonical HTML

```html
<div class="skeleton-list" aria-busy="true" aria-label="Loading posts">
  <article class="skeleton-card">
    <div class="skeleton-line skeleton-line--meta"></div>
    <div class="skeleton-line skeleton-line--title"></div>
    <div class="skeleton-line skeleton-line--body"></div>
    <div class="skeleton-line skeleton-line--body skeleton-line--short"></div>
  </article>
</div>
```

## Skeleton CSS

```css
.skeleton-line {
  height: 1em;
  background: linear-gradient(90deg,
    var(--color-rule) 0%,
    var(--color-surface-hover, rgba(0,0,0,0.05)) 50%,
    var(--color-rule) 100%);
  background-size: 200% 100%;
  animation: skeleton-pulse 1.5s ease-in-out infinite;
  border-radius: 4px;
  margin-bottom: 0.5rem;
}
.skeleton-line--meta { width: 30%; height: 0.75em; }
.skeleton-line--title { width: 70%; height: 1.5em; }
.skeleton-line--body { width: 100%; }
.skeleton-line--short { width: 60%; }

@keyframes skeleton-pulse {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

@media (prefers-reduced-motion: reduce) {
  .skeleton-line { animation: none; }
}
```

## Spinner canonical HTML

```html
<button type="submit" aria-busy="true" disabled>
  <span class="spinner" aria-hidden="true"></span>
  <span>Saving...</span>
</button>
```

## Spinner CSS

```css
.spinner {
  display: inline-block;
  width: 1em;
  height: 1em;
  border: 2px solid currentColor;
  border-bottom-color: transparent;
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
  vertical-align: -0.15em;
  margin-right: 0.5em;
}
@keyframes spin { to { transform: rotate(360deg); } }
@media (prefers-reduced-motion: reduce) {
  .spinner { animation-duration: 3s; }
}
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Glassmorphism | shimmer effect on glass surface |
| Aurora UI | gradient shimmer |
| Bento Grid | each cell has its own skeleton |
| Brutalist | plain "Loading..." text，no animation |
| Swiss Editorial | "01 LOADING" status text |
| Type-First Monochrome | huge "Loading..." word |
| Minimal Float | gentle pulse only |

## Accessibility 必查

- [ ] `aria-busy="true"` 在 loading container
- [ ] `aria-label` 描述「正在載入什麼」
- [ ] **`prefers-reduced-motion`** 必須尊重（disable animation）
- [ ] Spinner 加文字「Loading...」，不只是視覺
- [ ] Skeleton 完成後 focus 不要被 reset

## AI Tell 自查

- [ ] **不要** 萬用「pulsing gray block」skeleton — match 實際 layout 結構
- [ ] **不要** Spinner 不配文字
- [ ] **不要** 用 lucide loader2 icon
- [ ] 短操作 < 200ms 不需要 loading state（會閃）
