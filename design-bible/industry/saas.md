# SaaS / B2B Tool Industry Bundle

> SaaS 行銷網站 + 應用 chrome 的元件組合。

## 高頻 pages

1. Homepage / Landing
2. Features (single feature deep-dive)
3. Pricing
4. Customers / Case studies
5. Docs
6. Blog
7. About / Team
8. Login / Signup
9. Dashboard (app shell)
10. Settings / Billing

## Landing page 元件組合（依優先序）

| 序 | 元件 | 必出 / 可選 | 注意 |
|----|------|-----------|------|
| 1 | [Nav](../components/nav.md) | 必出 | sticky 可選 |
| 2 | [Hero](../components/hero.md) | 必出 | 一個 CTA，不要兩個 |
| 3 | [Logo cloud](../components/logo-cloud.md) | 可選（看風格） | Swiss/Brutalist 禁出 |
| 4 | [Features](../components/features.md) | 必出 | 不要永遠 3-col |
| 5 | [Testimonials](../components/testimonials.md) | 可選 | 真實 quote，不要假 |
| 6 | [Stats](../components/stats.md) | 可選 | 有真數字才放 |
| 7 | [Pricing](../components/pricing.md) | 通常出 | 看是不是 self-serve |
| 8 | [FAQ](../components/faq.md) | 可選 | sales-y 才出 |
| 9 | [CTA](../components/cta.md) | 必出 | 在 footer 之前 |
| 10 | [Footer](../components/footer.md) | 必出 | site map |

## App chrome 元件組合（登入後）

- [Sidebar](../components/sidebar.md) — 主 nav
- Top bar — user menu / notifications
- [Empty state](../components/empty-state.md) — 沒資料時
- [Loading](../components/loading.md) — skeleton 預設
- [Modal](../components/modal.md) — confirm action
- [Toast](../components/toast.md) — feedback
- [Form](../components/form.md) — settings / billing

## 推薦風格

| 子類 | 第一推 | 第二推 | 禁推 |
|------|-------|-------|------|
| 開發者工具 | **Type-First Monochrome** | Editorial Maximal | Glass/Aurora |
| AI 產品 | **Type-First Monochrome** | Corporate Clean | Aurora（除非 user 主動要） |
| 設計工具 | **Editorial Maximal** | Minimal Float, Swiss | — |
| 一般 SaaS | Corporate Clean | Type-First | Aurora 預設 |
| Dashboard 重的 | Bento Grid | Corporate Clean | Magazine（不適用） |
| Enterprise | Corporate Clean | Minimal Float | Brutalist |

## 必避免的 SaaS AI tells

1. ❌ Hero「✨ New」subtitle pill
2. ❌ 「Trusted by 10,000+ teams」緊跟 hero
3. ❌ Hero 兩個 button：「Start free」+「Book demo」
4. ❌ Features 3-col + lucide icons
5. ❌ Pricing 3-tier 中間 highlighted card
6. ❌ Testimonials 3-col 圓頭像
7. ❌ FAQ chevron accordion 配 slate-50 bg
8. ❌ CTA gradient bg + 中間白 button
9. ❌ Footer 4-col + emoji social icons
10. ❌ Inter + Lucide + slate-* 萬用組合

## Pricing page 結構

### Self-serve（≤ $100/mo）
- Hero（短）
- Plan cards (3 tier)
- Feature comparison table
- FAQ
- CTA to free trial

### Enterprise（custom）
- Hero（"Talk to sales"）
- 案例 highlight（1-2）
- ROI calculator（可選）
- Logo cloud（客戶）
- Contact form
- 不放 price 數字

## Dashboard pattern

```
┌─────────────────────────────────┐
│ TopBar (user, notifications)    │
├──┬──────────────────────────────┤
│  │                              │
│  │ Main content area            │
│  │ - Page heading               │
│  │ - Stats / KPIs               │
│  │ - Table / Chart              │
│  │                              │
│Side                             │
│bar                              │
│  │                              │
└──┴──────────────────────────────┘
```

## 內容範例 / 必填 placeholders

當 skill 出 SaaS landing page，**主動 ask user 這些 content**：

- 產品名
- 一句 value prop（≤ 12 字）
- 3-5 個 features（每個 ≤ 20 字 description）
- 1-2 個真實 testimonial（如有）
- 訂價（如已決定）
- CTA 動詞（"Start free" / "Try demo" / "Get early access"）
- 主要客戶 / 合作品牌（如有 logo）

## 整合：Step 1 加 industry-aware 題

當 user 在 Step 1 回答「SaaS / 工具」，skill 自動：
1. 套用此 bundle 的元件清單
2. 推薦此 bundle 的風格優先序
3. 主動避開 AI tell 清單上的 patterns
