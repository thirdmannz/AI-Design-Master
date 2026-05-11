# Table / Data Grid

> Tabular data 用 `<table>`，不用 `<div>` 模擬。Layout 不要用 `<table>`。

## Anatomy

- `<caption>`（screen reader 讀，視覺可隱藏）
- `<thead>` with `<th scope="col">`
- `<tbody>` with `<th scope="row">` if first col 是 row header
- `<tfoot>` 可選（總計等）
- 可選：sort buttons in `<th>`

## Canonical HTML

```html
<table>
  <caption>Q1 2026 revenue by region</caption>
  <thead>
    <tr>
      <th scope="col">Region</th>
      <th scope="col">Revenue</th>
      <th scope="col">YoY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">North America</th>
      <td>$2.4M</td>
      <td>+18%</td>
    </tr>
    <tr>
      <th scope="row">EMEA</th>
      <td>$1.8M</td>
      <td>+24%</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row">Total</th>
      <td>$4.2M</td>
      <td>+21%</td>
    </tr>
  </tfoot>
</table>
```

## Canonical CSS

```css
table {
  width: 100%;
  border-collapse: collapse;
  font-feature-settings: "tnum"; /* tabular numerals */
}
caption {
  text-align: left;
  font-weight: 600;
  margin-bottom: 0.75rem;
}
th, td {
  padding: 0.75rem 1rem;
  text-align: left;
  border-bottom: 1px solid var(--color-rule);
}
th { font-weight: 600; color: var(--color-muted); font-size: 0.875rem; text-transform: uppercase; letter-spacing: 0.04em; }
tbody tr:hover { background: var(--color-surface-hover, transparent); }
```

## Mobile responsive (橫向滾動 vs stack)

```css
@media (max-width: 767px) {
  .table-wrapper { overflow-x: auto; -webkit-overflow-scrolling: touch; }
  table { min-width: 600px; }
}
```

或 stack 版（每 row 變 card）：

```css
@media (max-width: 767px) {
  thead { display: none; }
  tr { display: block; padding: 1rem 0; border-bottom: 1px solid var(--color-rule); }
  td { display: block; padding: 0.25rem 0; }
  td::before { content: attr(data-label) ": "; font-weight: 600; color: var(--color-muted); }
}
```
HTML 需要 `<td data-label="Region">North America</td>`

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | ✅ 含 hover、條紋斑馬 |
| Swiss Editorial | ✅ baseline grid table，1px hairline |
| Bento Grid | ⚠️ 把每 row 變 bento cell |
| Brutalist | ✅ default browser style |
| Type-First Monochrome | ✅ tabular numerals, large |
| Magazine Longform | ✅ in-article data table |
| Aurora UI | ⚠️ 不適合 (data 不該漂浮) |
| Glassmorphism | ❌ 不適合 |
| **Fashion / Luxury** | ❌ 用 list format |

## Accessibility 必查

- [ ] `<caption>` 必出（可視覺隱藏但 SR 必讀）
- [ ] `<th scope="col">` 跟 `<th scope="row">`
- [ ] Sortable column 用 `<button>` in `<th>` + `aria-sort="ascending|descending|none"`
- [ ] 大表格分頁，每頁 10-20 row
- [ ] Caption 描述表格目的
- [ ] 數字欄位用 `text-align: right` + `font-feature-settings: "tnum"`

## Sortable header

```html
<th scope="col" aria-sort="ascending">
  <button type="button">Revenue ↑</button>
</th>
```

## AI Tell 自查

- [ ] **不要** 用 `<div role="table">` — 用 native `<table>`
- [ ] **不要** 斑馬條紋用 slate-50（用該風格 surface 變體）
- [ ] **不要** sort icon 用 lucide
- [ ] **不要** 「Showing 1-10 of 100」固定 pagination 文案
