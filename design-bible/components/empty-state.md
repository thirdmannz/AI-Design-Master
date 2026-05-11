# Empty State

> 沒資料時的畫面。**不是錯誤**，是「還沒開始」。寫好 empty state 是 product polish 的重點。

## Anatomy

- 簡短 headline（解釋為什麼空）
- 1-2 句解釋
- Primary action（CTA）
- 可選：illustration / icon

## Canonical HTML

```html
<section class="empty-state" role="status" aria-labelledby="empty-title">
  <h2 id="empty-title">No projects yet</h2>
  <p>Create your first project to get started.</p>
  <a href="/new" class="btn-primary">Create project</a>
</section>
```

注意 `role="status"`：SR 會讀，但不打斷使用。

## Canonical CSS

```css
.empty-state {
  padding: 4rem 1.25rem;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  max-width: 32rem;
  margin: 0 auto;
}
.empty-state h2 { font-size: 1.5rem; margin: 0; }
.empty-state p { color: var(--color-muted); margin: 0; }
```

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | center, illustration + CTA |
| Bento Grid | bento cell empty state |
| Brutalist | plain text + default underline link |
| Type-First Monochrome | big typography "Empty" + tiny CTA |
| Editorial Maximal | "Nothing here yet." + 解釋 |
| Swiss Editorial | left-aligned, numbered next step |
| Minimal Float | huge whitespace + tiny CTA |

## Accessibility 必查

- [ ] `role="status"` 為 SR 提示
- [ ] 不用 `aria-live="assertive"` 因為這不是緊急
- [ ] Illustration `aria-hidden="true"` 如純裝飾
- [ ] CTA 文字明確（不要「Click here」）

## 不同情境 messages

| 情境 | Heading | Body |
|------|---------|------|
| Brand new user | "Welcome" | "Start by creating X" |
| Filter returns 0 | "No matches" | "Try removing some filters" |
| Search no results | "Nothing found" | "Try different keywords" |
| Cleared all items | "All clear" | "You're caught up" |

## AI Tell 自查

- [ ] **不要** 永遠 illustration + 「No data」+ button 三件套
- [ ] **不要** 用 SVG plant / box / folder lucide-style illustration
- [ ] **不要** 「Get started」一律當 CTA — 用情境化動詞
- [ ] 不同情境用不同文案（不是萬用「No items」）
