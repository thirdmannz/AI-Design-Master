# E-commerce / Brand Industry Bundle

> 品牌電商。**Fashion / Luxury / Dark Luxury / Editorial 是首推**。SaaS 風格不適合。

## 高頻 pages

1. Home / Storefront
2. Collection / Category listing (PLP)
3. Product detail page (PDP)
4. Cart
5. Checkout (multi-step)
6. Order confirmation
7. Account / Order history
8. About / Story
9. Lookbook / Editorial
10. Contact / Stores

## Home / Storefront 元件組合

| 序 | 元件 | 必出 / 可選 |
|----|------|-----------|
| 1 | [Nav](../components/nav.md) (含 cart icon) | 必出 |
| 2 | [Hero](../components/hero.md)（full-bleed photo） | 必出 |
| 3 | Featured collection grid | 必出 |
| 4 | Editorial moment（故事 / lookbook） | 可選 |
| 5 | New arrivals / Best sellers | 可選 |
| 6 | Brand mission section | 可選 |
| 7 | Newsletter signup | 可選 |
| 8 | [Footer](../components/footer.md)（含店點 / 客服） | 必出 |

## 產品 listing (PLP)

```
┌──────────────────────────────────────┐
│ Filter sidebar │ Product grid        │
│ - Category     │ ┌────┬────┬────┐    │
│ - Size         │ │ p1 │ p2 │ p3 │    │
│ - Color        │ ├────┼────┼────┤    │
│ - Price        │ │ p4 │ p5 │ p6 │    │
│                │ └────┴────┴────┘    │
│                │ Sort: [Price ▾]     │
└──────────────────────────────────────┘
```

- Filter / sort 控制
- Pagination 或 infinite scroll
- Product card：image + name + price + 可選 quick-add

## PDP（Product Detail Page）

- Image gallery（≥ 4 張，含 lifestyle）
- Product name
- Price + currency
- Variant selector（size / color）
- Add to cart button
- Description / details accordion
- Size guide modal
- Reviews（如有）
- Related products

## Cart

- Line items（image + name + variant + qty + price）
- Qty controls
- Remove
- Subtotal
- Promo code field
- Checkout CTA

## Checkout（multi-step）

1. Email (guest 或 login)
2. Shipping address
3. Shipping method
4. Payment
5. Review + confirm

每 step 進度條 / step indicator。

## 推薦風格

| 品類 | 第一推 | 第二推 |
|------|-------|-------|
| Fashion / Apparel | **Fashion / Luxury Editorial** | Editorial Maximal, Magazine |
| 美妝 | Fashion / Luxury, Organic Nature | Dark Luxury |
| 珠寶 / 高端 | **Dark Luxury**, Fashion / Luxury | Editorial |
| 家居 / 生活 | Organic Nature, Minimal Float | Magazine Longform |
| 食品 / 飲品 | Magazine Longform, Organic Nature | Editorial |
| Streetwear | Type-First Monochrome, Brutalist | Neobrutalism |
| 設計品牌 | Swiss Editorial, Magazine | Type-First |
| 科技電商 | Corporate Clean | Bento Grid |

## 必避免的 E-commerce AI tells

1. ❌ Hero 「Free shipping over $50」黃色 banner
2. ❌ 「⭐ 4.9 (1,200 reviews)」固定樣式
3. ❌ Pricing 「Was $99, now $49 ❤️」紅色 sale tag
4. ❌ 「Add to wishlist ♡」lucide heart icon
5. ❌ Product card hover 露 secondary image（OK 但別固定 timing）
6. ❌ Toast 「Added to cart!」+ 綠勾
7. ❌ Trust badge 三件套（Free shipping / Returns / Secure checkout）
8. ❌ Newsletter 「Get 10% off ✨」pill

## 替代方案（不像 AI 的 e-commerce 寫法）

| AI default | 替代 |
|-----------|------|
| ⭐⭐⭐⭐⭐ 4.9 | "Rated 4.9 by 1,200 customers" plain text |
| Sale tag | 編輯文案 ("Last reduced") |
| Heart icon save | "Save for later" link |
| Quick add button | hover-revealed "+ Add" minimal |
| Trust badges | Editorial section about quality |

## Photography is everything

- 攝影風格 **比 layout 重要**
- 用真實產品攝影，不用 mock-up
- Fashion / Luxury：full-bleed，editorial 光線
- Organic Nature：自然光，戶外
- Streetwear：直拍，文化感

## 整合 Step 1

當 user 回「電商 / 品牌」+ 子類，skill 自動：
- 套用 PLP / PDP / Checkout 元件清單
- 推薦對應風格
- 主動 ask 攝影資源
- 提示 AI tell 避免清單
