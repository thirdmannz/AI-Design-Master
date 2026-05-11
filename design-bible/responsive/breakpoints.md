# Responsive Breakpoints

> Mobile-first. 預設樣式給 mobile，breakpoint 往上加。

## 標準 breakpoint（對齊 Tailwind）

| 名稱 | min-width | 對應裝置 |
|------|----------|---------|
| (預設) | 0 | Mobile portrait (iPhone SE 到 Pro Max) |
| `sm` | 640px | Mobile landscape, small tablet |
| `md` | 768px | iPad portrait |
| `lg` | 1024px | iPad landscape, small laptop |
| `xl` | 1280px | Standard laptop |
| `2xl` | 1536px | Large desktop |

CSS 變數：
```css
:root {
  --bp-sm: 640px;
  --bp-md: 768px;
  --bp-lg: 1024px;
  --bp-xl: 1280px;
  --bp-2xl: 1536px;
}
```

## Media query vs Container query

- **Media query**：top-level layout（hero, page grid, nav 變漢堡）
- **Container query**：可重用元件（card 在 sidebar vs main 不同寬）

```css
/* Card adapts to its container, not viewport */
.card-wrapper { container-type: inline-size; }
@container (min-width: 400px) {
  .card { display: grid; grid-template-columns: 1fr 2fr; }
}
```

## 必出三段 CSS 規則

Skill 在 Step 3 出每個元件，必須包含 ≥ 2 個 breakpoint 切換。最起碼出：

```css
/* Mobile-first (預設) */
.hero { padding: 4rem 1.25rem; font-size: clamp(2rem, 8vw, 3rem); }

/* Tablet (md, 768px) */
@media (min-width: 768px) {
  .hero { padding: 6rem 2rem; }
}

/* Desktop (lg, 1024px) */
@media (min-width: 1024px) {
  .hero { padding: 8rem 4rem; font-size: clamp(3.5rem, 6vw, 6rem); }
}
```

## 每風格的 mobile 適配規則

### Corporate Clean
- Mobile: stack 全 vertical，nav 漢堡
- Tablet: 2-column features, side-by-side hero
- Desktop: 3-column features, hero w/ illustration right

### Editorial Maximal
- Mobile: 大 headline 縮成 8vw（不要 14vw 直接 bleed），單欄
- Tablet: 引入 12-col grid
- Desktop: 完整 baseline grid + marginalia

### Glassmorphism
- Mobile: blur card 改 solid bg（行動裝置 blur 開銷大）
- Tablet+: 啟用 backdrop-filter

### Aurora UI
- Mobile: gradient blob 縮小 + 數量減少（不超過 2 個）
- Desktop: 完整 aurora animation

### Bento Grid
- Mobile: 全部 grid cell 改 1-col stack
- Tablet (md): 2-col irregular grid
- Desktop: 4-6 col asymmetric bento

### Minimal Float
- Mobile: float card 改貼齊邊緣
- Desktop: 維持留白浮動

### Neobrutalism
- Mobile: hard shadow 縮小 (4px → 2px)
- Desktop: 維持 8px hard shadow

### Claymorphism
- Mobile: round 維持，但 padding 縮
- Desktop: 完整圓潤

### Dark Luxury
- Mobile: 大 type 維持，gold accent 不變
- Desktop: 完整 spacious layout

### Organic Nature
- Mobile: 有機 blob 簡化
- Desktop: 完整 organic shape

### Kinetic Editorial
- **Mobile: 禁用 parallax / scroll-pin**（行動裝置體驗差）
- Desktop: 完整 motion

### 3D Immersive
- **Mobile: 3D scene 改 static poster image**
- Desktop: 完整 WebGL

### Swiss Editorial
- Mobile: 12-col → 4-col grid，numbered index 維持
- Tablet: 8-col
- Desktop: 12-col baseline grid

### Magazine Longform
- Mobile: drop cap 維持但縮成 3 行，marginalia 移到 inline footnote
- Tablet: marginalia 維持側邊
- Desktop: 完整跨頁配 marginalia

### Fashion / Luxury Editorial
- Mobile: full-bleed image 維持，tiny caption 不縮（已經夠小）
- Desktop: 不對稱 split, 大留白

### Brutalist / Anti-Design
- Mobile: 一切照舊（本來就 raw）
- Desktop: 一切照舊（不重做樣式）

### Type-First Monochrome
- Mobile: oversized headline 縮成 12vw，bleed 維持
- Desktop: 完整 16vw bleed

## 通用 mobile-first checklist

- [ ] Hero padding 在 mobile ≥ 1rem 左右（不要貼邊）
- [ ] Font-size 用 `clamp(min, vw, max)` 而不是 fixed
- [ ] Touch target ≥ 44×44px（button、link）
- [ ] Nav 在 < md 變漢堡或下拉
- [ ] Image 用 `<picture>` + srcset 給不同 DPR
- [ ] Form input font-size ≥ 16px（避免 iOS 自動 zoom）
- [ ] Modal 在 mobile 變 bottom sheet（看風格）
- [ ] Sticky element 不超過 vh 30%（避免擋內容）

## Container query 適用場景

- Sidebar 可變寬：card 在 sidebar 跟 main 表現不同
- 可重複使用元件：dashboard widget、product card
- 第三方嵌入：不知道父容器寬度時

## 何時用什麼

| 情境 | 工具 |
|------|------|
| 整頁 layout | Media query |
| 元件自適應父容器 | Container query |
| 字型 fluid | `clamp(min, vw, max)` |
| Grid 自動換行 | `repeat(auto-fit, minmax(280px, 1fr))` |
| Image responsive | `<picture>` + srcset |
