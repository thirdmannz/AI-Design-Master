# Image / Asset Strategy

> 每風格獨特的 visual asset 語言。**圖比 layout 重要** — 換攝影風格能瞬間改變整站氣質。

## 通用原則

### 1. 4 種 asset 路線

| 路線 | 適用 | 範例風格 |
|------|------|---------|
| **Photography (real)** | Editorial / brand / fashion | Magazine, Fashion, Editorial |
| **Illustration (custom)** | Tech / SaaS / playful | Corporate Clean, Bento Grid |
| **Abstract (gradient/3D/generative)** | AI / futuristic | Aurora, Glass, Claymorphism |
| **No image (typography only)** | Editorial / extreme minimal | Swiss, Type-First, Brutalist |

### 2. Image source 推薦（按品質序）

#### Photography
1. **Custom shoot** — 自己拍 / 委託，最 unique
2. **Unsplash+** — 付費，較少撞圖
3. **Pexels** — 免費，品質尚可
4. **Unsplash free** — 免費，會撞圖（要慎選）
5. ❌ **Generic stock (Shutterstock, Getty)** — typical AI tell

#### Illustration
1. **Custom commission** — 最 unique
2. **Streamline icons** — 付費，較少 lucide 撞風
3. ❌ **unDraw / Storyset / Blush** — 已成 AI tell，慎用
4. ❌ **Lucide icons** — 萬用 AI default，特定風格才用

#### Abstract
1. **Spline (3D)** — 客製 3D，最 unique
2. **Custom generative art** — p5.js / Three.js
3. **CSS-only gradient** — 無 image，省 bandwidth

### 3. 必含技術

```html
<picture>
  <source srcset="hero.avif" type="image/avif">
  <source srcset="hero.webp" type="image/webp">
  <img src="hero.jpg"
       alt="Workers reviewing architectural plans"
       width="1600"
       height="900"
       loading="lazy"
       decoding="async">
</picture>
```

### 4. Performance budget

- Hero image：≤ 200 KB (WebP/AVIF)
- Body images：≤ 100 KB each
- Total page weight：≤ 1.5 MB
- LCP image：`fetchpriority="high"`，`loading="eager"`

### 5. Aspect ratio rules

- Hero: 16:9 / 3:2 / 4:3
- Editorial: 4:5 portrait 或 3:2
- Product (e-commerce): 1:1 grid / 3:4 PDP
- Avatar: 1:1
- Always set `width` + `height` 避免 CLS

### 6. 必避免的 image AI tells

- ❌ 「Diverse smiling team in office」stock photo
- ❌ Hands typing on MacBook stock photo
- ❌ Flat illustration with 3-color palette (unDraw style)
- ❌ 「Person with laptop on beach」remote work stock
- ❌ Abstract gradient blob 萬用 hero
- ❌ Robot / AI brain illustration
- ❌ Lucide icon + brand color 三件套

---

## 每風格 image 策略（17 styles）

### Corporate Clean
- **首選**：custom illustration（minimal flat），不要 unDraw style
- **替代**：abstract pattern / brand pattern
- **Photo**：可選 — 高 quality team / office documentary
- **Unsplash keywords**：`office documentary`, `architecture clean`, `team meeting candid`
- **禁用**：unDraw flat / stock smiling team

### Editorial Maximal
- **首選**：editorial photography（彩色，自然光）
- **Unsplash keywords**：`editorial portrait`, `street scene`, `lifestyle moment`
- **可選**：Letterpress-style illustration
- **禁用**：stock business photos

### Minimal Float
- **首選**：no images 或 single hero portrait
- **Unsplash keywords**：`minimal still life`, `architecture detail`, `single object`
- **禁用**：collage / multiple images / illustration

### Bento Grid
- **首選**：mix — 每 cell 不同類型（icon / photo / chart / text）
- **Photo**：minimal documentary
- **Illustration**：geometric / abstract
- **禁用**：每 cell 都同類型 image

### Dark Luxury
- **首選**：high-quality moody photography（暗調 / dramatic light）
- **Unsplash keywords**：`moody portrait`, `architecture night`, `luxury detail`
- **Photo treatment**：高對比、低 saturation、深 shadow
- **禁用**：bright cheerful imagery

### Aurora UI ⚠️
- **首選**：abstract 3D render（Spline）/ gradient
- **CSS-only**：aurora 用 CSS conic-gradient / SVG mask
- **禁用**：real photography（會混搭得很怪）

### Glassmorphism ⚠️
- **首選**：blurred photography on backdrop + glass cards
- **Background**：moody photo with blur
- **Cards**：transparent，透出 bg
- **禁用**：illustration（不搭）

### Claymorphism ⚠️
- **首選**：custom clay 3D illustration（Blender / Spline）
- **Unsplash**：很少適合 — 多用 illustration
- **禁用**：documentary photography

### Neobrutalism
- **首選**：bold typography 為主，少圖
- **如有圖**：raw photography / 黑白 / 沒濾鏡
- **Illustration**：粗厚線條手繪
- **禁用**：smooth illustration / gradient

### Organic Nature
- **首選**：自然攝影（戶外、植物、water）
- **Unsplash keywords**：`forest`, `botanical`, `water surface`, `natural texture`
- **Illustration**：organic 手繪（不用 vector flat）
- **Photo treatment**：自然光，warm tone

### Kinetic Editorial ⭐
- **首選**：editorial photography（large scale）
- **影片**：可用 video bg（25 sec loop）
- **Photo**：scroll-parallax 必須有高解析（≥ 2000px）
- **禁用**：stock 影片

### 3D Immersive ⭐
- **首選**：Three.js / R3F WebGL scene
- **資源**：Spline export / glTF models
- **效能**：lazy load 3D，mobile 降級為 static poster image

### Swiss Editorial ⭐
- **首選**：documentary photography（黑白 / 嚴格 grid 對齊）
- **Unsplash keywords**：`architecture documentary`, `industrial`, `editorial bw`
- **Photo treatment**：preserve original，不要濾鏡
- **禁用**：illustration / abstract / 任何裝飾

### Magazine Longform ⭐
- **首選**：editorial colored photography（故事性）
- **Unsplash keywords**：`magazine photography`, `journalism photo`, `feature story`
- **Treatment**：full-bleed allowed，配 figcaption + credit
- **禁用**：stock business / smiling team

### Fashion / Luxury Editorial ⭐
- **首選**：fashion editorial photography（high-key 或 dramatic）
- **Unsplash keywords**：`fashion editorial`, `model studio`, `lookbook`
- **Treatment**：huge full-bleed，極小 caption
- **必出**：tracked uppercase caption / credit
- **禁用**：smiling stock / corporate photos

### Brutalist / Anti-Design ⭐
- **首選**：**no images 預設** 或 low-resolution intentional
- **如有圖**：default `<img>` no styling，可能 cropped 奇怪
- **可選**：ASCII art / pure text
- **禁用**：professional photography（破壞風格）

### Type-First Monochrome ⭐
- **首選**：**no images** — typography 是唯一視覺
- **可選**：single hero portrait（黑白 / minimal）
- **禁用**：illustration / icon / multiple images

---

## Mood board 生成（M5 整合）

當 Step 2 推薦風格時，每風格附 mood board：

```markdown
## Swiss Editorial 視覺 mood

**代表網站截圖**（從 data/screenshots/）
- pentagram.com.jpg
- bureauborsche.com.jpg
- manualcreative.com.jpg

**Color palette**
- #fafaf7 (bg)
- #0a0a0a (ink)
- #2c5fff (accent)

**Typography**
- Display: Inter Tight 700
- Body: Inter 400

**Imagery style**
- Documentary photography, black and white
- Strict grid alignment
- No illustration

**Motion**
- None / instant cut
```

---

## 整合到 skill.md

當 Step 3 輸出時，按選定風格附 image guidance：

```markdown
## 視覺資源建議（基於 [style] 風格）

### 攝影
[per-style asset 策略]

### Unsplash 關鍵字（可直接搜）
- `editorial portrait` https://unsplash.com/s/photos/editorial-portrait
- `architecture documentary` https://unsplash.com/s/photos/architecture-documentary

### Placeholder URL（開發階段）
- Hero: https://picsum.photos/seed/yourbrand/1600/900
- Avatar: https://picsum.photos/seed/user1/80/80
- Product: https://picsum.photos/seed/p1/600/600

### 禁用清單（此風格）
- ❌ Stock smiling team
- ❌ unDraw illustration
- ❌ Generic Unsplash 撞圖款
```

## Skill 輸出時必檢

- [ ] 圖片 `<img>` 含 `alt`
- [ ] 圖片 `<img>` 含 `width` + `height`（防 CLS）
- [ ] 使用 `<picture>` 提供 avif / webp fallback
- [ ] Hero image `loading="eager"` + `fetchpriority="high"`
- [ ] 非 hero image `loading="lazy"`
- [ ] 推薦 image source 對應該風格
- [ ] 不推薦 unDraw / Storyset 給有 AI-aversion 風格
- [ ] 提供 placeholder URL 給 dev mode
