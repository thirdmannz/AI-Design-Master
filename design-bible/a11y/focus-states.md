# Focus States Per Style

> 每風格的 focus ring 設計。**禁止用 `outline: none` 而不補替代**。

## 通用原則

1. Focus indicator 必須對 bg ≥ 3:1 對比
2. 厚度 ≥ 2px
3. Offset ≥ 2px（離 element 邊緣有空隙）
4. 鍵盤焦點 (`:focus-visible`) 跟滑鼠 focus 分開處理
5. 不要只靠顏色 — 配合 outline / box-shadow / underline

## 通用基底（所有風格適用）

```css
*:focus { outline: none; } /* 重置 default UA */
*:focus-visible {
  outline: 2px solid var(--focus-ring-color, currentColor);
  outline-offset: 2px;
  border-radius: var(--focus-ring-radius, 2px);
}
```

## 各風格客製

### Corporate Clean
```css
--focus-ring-color: var(--color-accent);
--focus-ring-radius: 6px;
```
- 跟 button radius 一致
- 用 accent 色（藍/綠等品牌色）

### Editorial Maximal
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
}
```
- offset 大一點，呼應大留白

### Glassmorphism
```css
*:focus-visible {
  outline: 2px solid rgba(255,255,255,0.9);
  outline-offset: 2px;
  box-shadow: 0 0 0 4px rgba(var(--color-accent-rgb), 0.4);
}
```
- 雙環：內白 + 外 accent glow
- 對 frosted bg 比單色 outline 顯眼

### Aurora UI
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  box-shadow: 0 0 24px rgba(var(--color-accent-rgb), 0.4);
}
```
- Glow 對齊 aurora 美學

### Bento Grid
```css
*:focus-visible {
  outline: 2px solid var(--color-ink);
  outline-offset: -2px; /* 內 outline */
  border-radius: inherit;
}
```
- Inset focus 對 card 邊界更乾淨

### Minimal Float
```css
--focus-ring-color: var(--color-ink);
--focus-ring-radius: 12px;
```

### Neobrutalism
```css
*:focus-visible {
  outline: 3px solid var(--color-ink);
  outline-offset: 0;
  box-shadow: 4px 4px 0 var(--color-accent);
}
```
- 厚 outline + offset shadow，呼應 brutalist 美學

### Claymorphism
```css
*:focus-visible {
  outline: 3px solid var(--color-accent);
  outline-offset: 4px;
  border-radius: inherit;
}
```

### Dark Luxury
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  box-shadow: 0 0 16px rgba(var(--color-accent-rgb), 0.5);
}
```
- Dark bg 上需要 glow 提升 visibility

### Organic Nature
```css
--focus-ring-color: var(--color-accent);
--focus-ring-radius: 999px;
```

### Kinetic Editorial
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 4px;
  animation: focus-pulse 1s ease-out;
}
@keyframes focus-pulse {
  0% { outline-offset: 8px; opacity: 0; }
  100% { outline-offset: 4px; opacity: 1; }
}
```
- 風格本身就有動效，focus 也帶 micro-motion

### 3D Immersive
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  filter: drop-shadow(0 0 8px var(--color-accent));
}
```

### Swiss Editorial
```css
*:focus-visible {
  outline: 1px solid var(--color-ink);
  outline-offset: 2px;
}
```
- **薄、黑、無圓角** — Swiss 美學
- 不用 accent 色（會破壞極簡）

### Magazine Longform
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  text-decoration: underline; /* link focus 加 underline */
}
```

### Fashion / Luxury Editorial
```css
*:focus-visible {
  outline: 1px solid var(--color-ink);
  outline-offset: 6px; /* 大 offset，呼應 luxury 留白 */
}
```

### Brutalist / Anti-Design
```css
a:focus, button:focus, input:focus {
  outline: 2px solid #0000ff; /* 瀏覽器預設藍 */
  outline-offset: 0;
  background: yellow;
}
```
- **直接用瀏覽器預設**，這是風格特徵
- 不要美化

### Type-First Monochrome
```css
*:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 4px;
}
a:focus-visible {
  text-decoration: underline;
  text-decoration-thickness: 2px;
  text-underline-offset: 4px;
}
```

## Skill 自查

- [ ] 所有 button / link / input / details / summary 都有 `:focus-visible` 樣式
- [ ] 沒有 `outline: none` 沒補替代
- [ ] Focus ring 對 bg ≥ 3:1
- [ ] 鍵盤 Tab 一路按下去，每個 stop 都看得到 focus
- [ ] Focus 不被 z-index 蓋住
