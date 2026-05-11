# Motion Design System

> 每風格獨特動效語言。**Motion 是風格的延伸**，不是裝飾。Swiss 不動 / Aurora 彈簧 / Kinetic 視差 / Brutalist instant cut — 每個都該對應其視覺哲學。

## 通用原則

### 1. `prefers-reduced-motion` 必須尊重

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

### 2. Duration scale（通用）

| Token | 值 | 用途 |
|-------|-----|------|
| `--motion-instant` | `50ms` | hover state / focus state |
| `--motion-fast` | `150ms` | small UI changes (button press) |
| `--motion-base` | `250ms` | most transitions (modal in, card hover) |
| `--motion-slow` | `400ms` | section reveals |
| `--motion-page` | `800ms` | page transitions |
| `--motion-storyteller` | `1200ms+` | hero reveal, scroll-driven |

### 3. Easing tokens

```css
:root {
  /* Linear / quick / mechanical */
  --easing-linear: linear;
  --easing-quick: cubic-bezier(0.4, 0, 0.2, 1);     /* standard */

  /* Natural / organic */
  --easing-ease-out: cubic-bezier(0, 0, 0.2, 1);    /* exit */
  --easing-ease-in: cubic-bezier(0.4, 0, 1, 1);     /* enter */

  /* Bouncy / springy */
  --easing-spring: cubic-bezier(0.16, 1, 0.3, 1);   /* settled spring */
  --easing-bounce: cubic-bezier(0.34, 1.56, 0.64, 1); /* overshoot */

  /* Editorial / slow elegance */
  --easing-editorial: cubic-bezier(0.7, 0, 0.3, 1); /* slow start + end */
}
```

### 4. Scroll-trigger threshold

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => e.target.classList.toggle('in-view', e.isIntersecting));
}, {
  threshold: 0.15,       // 元件 15% 進入 viewport 就觸發
  rootMargin: '0px 0px -10% 0px' // 提前 10% 觸發，感覺更自然
});
```

### 5. Stagger（一群元素依序進入）

```css
.feature-list > * { animation-delay: calc(var(--i) * 80ms); }
/* HTML: <li style="--i: 0"> <li style="--i: 1"> ... */
```

### 6. 必避免的 motion AI tells

- ❌ 「Hero fade up 0 → 100% opacity」萬用 entrance
- ❌ Hover scale(1.05) 萬用 card
- ❌ AOS-style data-aos="fade-up" 三件套
- ❌ Spinner 用 lucide loader2 + animate-spin
- ❌ Number count-up automatic on page load
- ❌ Gradient bg infinite slow rotation

---

## 每風格 motion 規格（17 styles）

### Corporate Clean
```css
--motion-duration: 200ms;
--motion-easing: var(--easing-quick);
/* Hover: subtle 1-2px lift, instant focus, no fancy */
```
- Card hover: `transform: translateY(-2px)` + `box-shadow` 加深
- Button: pressed effect `transform: translateY(1px)` on `:active`
- Page transition: 250ms fade

### Editorial Maximal
```css
--motion-duration: 400ms;
--motion-easing: var(--easing-editorial);
```
- Heading scroll-reveal: stagger from left, 400ms each
- Image reveal: scale 1.05 → 1 with 600ms
- Link hover: underline 從左到右 stretch in

### Minimal Float
```css
--motion-duration: 300ms;
--motion-easing: var(--easing-ease-out);
```
- 元素「漂浮」感：subtle `translateY` ±4px slow loop（呼吸感）
- Hover: 元素稍微 raise + 影子加深
- Mouse cursor: 客製 cursor follow（謹慎用）

### Bento Grid
```css
--motion-duration: 200ms;
--motion-easing: var(--easing-quick);
```
- Cell hover: `scale(1.02)` + 邊框亮起來
- 進場: stagger 80ms per cell
- Click cell: 短 `scale(0.98)` 按壓感

### Dark Luxury
```css
--motion-duration: 600ms;
--motion-easing: var(--easing-editorial);
```
- Slow elegant fades
- Gold accent 漸入（不要 bouncy）
- Photo: subtle slow zoom (Ken Burns effect)

### Aurora UI ⚠️
```css
--motion-duration: 800ms;
--motion-easing: var(--easing-spring);
```
- Aurora gradient 緩動 8s+ infinite
- Blob morphing animation (SVG path morph)
- Card hover: spring scale + glow intensify

### Glassmorphism ⚠️
```css
--motion-duration: 400ms;
--motion-easing: var(--easing-spring);
```
- Backdrop-blur 進場時從 0 → 16px
- Card 進場: 從上方滑入 + opacity
- Hover: backdrop saturation 加深

### Claymorphism ⚠️
```css
--motion-duration: 350ms;
--motion-easing: var(--easing-bounce);
```
- Button press: 明顯 inset shadow 變化
- Squishy bounce on hover
- Modal: scale(0.95) → scale(1) overshoot

### Neobrutalism
```css
--motion-duration: 100ms;
--motion-easing: var(--easing-quick);
```
- **動效要快、要硬**
- Hover: shadow 從 4px → 2px（按壓感）
- 不要 fade，用 cut transitions

### Organic Nature
```css
--motion-duration: 500ms;
--motion-easing: var(--easing-ease-out);
```
- 緩慢、自然
- Leaf 飄落 / blob 變形 keyframe
- Cursor 觸發 subtle ripple

### Kinetic Editorial ⭐
```css
--motion-duration: variable; /* 跟 scroll 綁定 */
--motion-easing: var(--easing-editorial);
```
- **這個風格本身就是 motion-driven**
- Scroll-pinned sections
- Parallax layers (slow / medium / fast)
- Type animation: letter-by-letter reveal
- 用 GSAP ScrollTrigger 或 Framer Motion scroll-linked

```css
.kinetic-hero {
  position: sticky;
  top: 0;
  height: 100vh;
}
.kinetic-text { animation-timeline: view(); animation-range: entry 0% cover 50%; }
```

### 3D Immersive
```css
--motion-duration: variable; /* 60fps WebGL */
```
- WebGL frame loop (Three.js / R3F)
- Camera 跟 mouse pan
- 物件 idle rotation (slow)
- UI overlay: 250ms fade

### Swiss Editorial ⭐
```css
--motion-duration: 50ms; /* effectively no motion */
--motion-easing: var(--easing-linear);
```
- **不動。Cut transitions 為主**
- Page load: instant
- Hover: 1-2px subtle 或 nothing
- Focus: instant outline
- 用 motion 違反 Swiss 美學 — 設計師會看出

### Magazine Longform ⭐
```css
--motion-duration: 500ms;
--motion-easing: var(--easing-editorial);
```
- Slow fade on scroll
- Drop cap: 進場 letter-by-letter（subtle）
- Image: 緩慢 reveal + caption fade
- Pull quote: 從旁邊 slide in（mobile 不做）

### Fashion / Luxury Editorial ⭐
```css
--motion-duration: 700ms;
--motion-easing: var(--easing-editorial);
```
- 緩慢、奢華
- Photo Ken Burns slow zoom
- Caption fade after photo loads
- Hover: 極微 + 慢

### Brutalist / Anti-Design ⭐
```css
/* 預設瀏覽器，零自訂 motion */
```
- **完全不要 transition**（除非 `:hover` 默認）
- 用瀏覽器 default focus / hover
- Cut transitions 為主
- 加 motion 違反風格 — Brutalist 拒絕當代 UX「polish」

### Type-First Monochrome ⭐
```css
--motion-duration: 300ms;
--motion-easing: var(--easing-editorial);
```
- 字級動效是核心：scroll-driven type scale
- Link hover: underline 從中間擴展到兩邊
- Page transition: 純 fade，250ms
- Accent 色 hover: 快速反白

---

## Framework 實作 (motion-specific libs)

| Framework | Motion lib |
|-----------|-----------|
| React | Framer Motion / motion.dev (newer) |
| Vue | motion-v / `<Transition>` |
| Svelte | 內建 `transition:` / `animate:` |
| Astro | 用上述 island 引入 |
| Plain CSS | CSS animations + `prefers-reduced-motion` |

---

## Skill 輸出時必檢

- [ ] 輸出 CSS 含 `--motion-duration` / `--motion-easing` tokens
- [ ] 含 `prefers-reduced-motion` media query
- [ ] 每個 transition 用 token 不寫死數字
- [ ] 風格 cut 對應的 motion 不亂用（Swiss 不該 bounce / Brutalist 不該 fade）
- [ ] 不用萬用 AOS-style `data-aos="fade-up"`
- [ ] Scroll-pinned 在 mobile 禁用（Kinetic 例外要顯式宣告）
