# Page-Level Templates

> 跨頁面一致系統。10 個高頻頁面類型，每個含 page anatomy + 元件組合 + 風格適配。

## 1. Homepage / Front-page

### Anatomy
```
1. Nav
2. Hero
3. Social proof (logo cloud / stats) — optional
4. Features section
5. Use case / problem-solution
6. Testimonials — optional
7. Pricing teaser — optional
8. Final CTA
9. Footer
```

### Industry 變體
- SaaS: 上述全部
- E-commerce: Hero(photo) + Featured collection + Editorial moment + Newsletter + Footer
- Editorial: Front-page hero article + Section grid + Newsletter
- Portfolio: Intro + Project grid + Now + Contact
- Docs: skip — docs 通常從 `/docs` 入口，不是傳統 homepage

### 風格特例
- Magazine Longform：homepage 像雜誌封面（big lead article + minor articles below）
- Swiss Editorial：numbered sections (01 / 02 / 03)
- Type-First：oversized intro statement，幾乎沒 features section
- Brutalist：index list 顯示所有可訪問頁，沒 marketing chrome

---

## 2. Pricing

### Anatomy
```
1. Nav
2. Pricing hero (短，"Pricing")
3. Billing toggle (monthly / yearly) — if applicable
4. Plan cards (2-4 tiers)
5. Feature comparison table
6. Pricing FAQ
7. Enterprise / contact CTA
8. Footer
```

### 元件
- [pricing](../components/pricing.md)
- [table](../components/table.md) (comparison)
- [faq](../components/faq.md)
- [cta](../components/cta.md)

### Self-serve vs Enterprise
- Self-serve (< $100/mo)：tier cards + comparison table
- Enterprise：「Talk to sales」+ ROI calculator + logo cloud

---

## 3. About

### Anatomy
```
1. Nav
2. Mission statement / brand promise
3. Story / timeline
4. Team grid
5. Values / culture
6. Press / awards — optional
7. Contact CTA
8. Footer
```

### 風格特例
- Editorial / Magazine：大圖編輯版型，攝影 team 而非圓頭像 grid
- Swiss：嚴格 grid，每個 team member 一行 baseline
- Brutalist：純文字 bio + `<address>` 聯絡

---

## 4. Blog Index

### Anatomy
```
1. Nav
2. Blog header (title + description)
3. Category filter (optional)
4. Featured post (large)
5. Post grid (recent posts)
6. Pagination
7. Newsletter signup (optional)
8. Footer
```

### 元件
- [blog](../components/blog.md)

### Mobile
- Filter 變 `<select>` 或 horizontal scroll chips

---

## 5. Blog Post

### Anatomy
```
1. Nav (可選 sticky)
2. Article header (kicker + title + lede + meta)
3. Article body
4. Inline media (figures with captions)
5. Pull quote (optional)
6. Marginalia (optional)
7. Author bio
8. Related posts
9. Newsletter / CTA
10. Footer
```

### 風格特例
- **Magazine Longform**：drop cap + marginalia + pull quote 是核心特徵
- **Editorial Maximal**：kicker + lede 必出，serif body
- **Swiss Editorial**：numbered article (Article 03 / 2026)
- **Brutalist**：default browser style + `<address>` for author

### Reading optimization
- Max line width 60-75 ch
- Body font ≥ 18px on desktop
- Estimated read time（可選，但**不要 lucide clock icon**）
- TOC for long posts（>2000 字）

---

## 6. Docs Page

### Anatomy
```
1. Top nav (logo + search + GitHub link)
2. Sidebar (left)
3. Breadcrumb (top of content)
4. Page heading
5. Main content (with on-this-page TOC right)
6. Prev/next page nav
7. "Edit on GitHub" link
8. Footer
```

### 元件
- [sidebar](../components/sidebar.md)
- [table](../components/table.md) (API params)
- code blocks with copy button
- Callout / admonition (note / warning / danger)

### Mobile
- Sidebar 變 drawer (toggle from top)
- TOC 變 `<details>` at top of content

詳見 [industry/docs.md](../industry/docs.md)。

---

## 7. Landing Page (Single-purpose marketing)

### Anatomy
```
1. Minimal nav (or no nav)
2. Hero (focused on 1 message)
3. Problem statement
4. Solution (your product)
5. Benefits / features (3-5)
6. Social proof (single big testimonial)
7. Demo / video (optional)
8. Pricing or single CTA
9. FAQ
10. Footer (minimal)
```

### 重點
- 一個 conversion goal — 不要分散
- 一個 primary CTA，整頁多次出現（但 visually same）
- 沒 navigation 到其他 marketing pages（focused conversion）

---

## 8. 404 / 500 / Error

詳見 [components/404.md](../components/404.md)。

### Anatomy
```
1. Minimal nav (or no nav)
2. Error code (large)
3. Heading: "Page not found" / "Something went wrong"
4. Explanation paragraph
5. Recovery actions: Home, Search, Contact
6. (Optional) recent posts / popular pages
7. Footer (minimal)
```

---

## 9. Auth (Login / Signup / Forgot password)

### Login anatomy
```
1. Logo (top-left or center)
2. Heading: "Log in"
3. Form: email + password
4. "Forgot password?" link
5. Submit button
6. "Sign up" link
7. (Optional) social login buttons
8. (Optional) terms / privacy footer
```

### Signup anatomy
- Same + name field + (optional) marketing opt-in
- Password strength indicator
- `autocomplete="new-password"`

### Forgot password
- Email field only
- Submit → email sent confirmation
- Don't reveal if email exists (security)

### 元件
- [form](../components/form.md)

### A11y
- `autocomplete` 屬性正確
- 「Show password」toggle 用 `<button aria-pressed>`
- Submit failure 用 `role="alert"` 通知

---

## 10. Checkout (Multi-step)

### Anatomy (4-step)
```
Step 1: Email / login (or guest)
Step 2: Shipping address
Step 3: Shipping method
Step 4: Payment + review
→ Success page
```

### Each step has
- Progress indicator (step 2 of 4)
- Order summary (right sidebar on desktop / bottom on mobile)
- Back button (回 previous step)
- Next button (validate + advance)

### Order summary
- Line items (image + name + qty + price)
- Subtotal
- Shipping
- Tax
- Total
- Promo code field

### A11y
- Step indicator 用 `<ol role="list" aria-label="Checkout progress">` + `aria-current="step"`
- Form errors collect at top + focus first error on submit
- "Place order" button 是 `<button type="submit">` not `<a>`

---

## 跨頁面一致性規則

### Token 不變
- `:root` CSS variables 在所有頁面相同
- 所有頁面 import 同一個 `globals.css`

### Component 重用
- Nav / Footer 在所有 page 相同
- Button / Card / Form / Modal 統一 style
- 不要 pricing page 一套 button、blog 一套

### Layout grid
- 統一最大寬度（max-width: 76rem for content / 90rem for full）
- 統一 vertical rhythm（section padding 變數化）
- 統一 breakpoint

### Typography scale
- 同一個 type scale 全頁
- h1 size 在 blog post / homepage / 404 不同位置但同 token

### Page transitions（如有）
- 全頁面用同一 transition timing
- `prefers-reduced-motion` 全頁同尊重

---

## 整合 Step 1 / Step 3

### Step 1 Q6 已加：
- 只要 1 個頁面 → output single page
- 2-3 個關鍵頁 → ask user 哪幾頁，依本檔出對應骨架
- 完整網站 → prioritize 3 頁先做，避免一次 dump

### Step 3 多頁輸出策略
當 user 選 2+ pages：
1. 先輸出共用 `:root` tokens（一次）
2. 共用 components (Nav / Footer / Button / Card)（一次）
3. 每 page 一個 file (page.tsx / pricing.tsx / about.tsx)
4. 每 page 只列**該頁獨有**的 section（共用元件 reference 即可）

### 風格 × 頁面 矩陣

| 頁面 | 適合風格（高） | 不適合風格 |
|------|-------------|----------|
| Homepage | 全部 | — |
| Pricing | Corporate, Type-First, Bento, Aurora | Magazine, Fashion |
| About | 全部 | — |
| Blog index/post | Editorial, Magazine, Swiss, Type-First, Brutalist | Aurora, Glass, Clay |
| Docs | Corporate, Type-First, Swiss, Brutalist | Aurora, Glass, Clay, Magazine, Fashion |
| Landing | Corporate, Magazine, Editorial, Type-First, Kinetic | — |
| 404 | 全部 | — |
| Auth | Corporate, Minimal Float, Type-First, Brutalist | Magazine, Fashion |
| Checkout | Corporate, Bento, Editorial | Brutalist, Glass |
