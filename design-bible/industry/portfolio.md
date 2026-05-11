# Portfolio / Personal Site Industry Bundle

> 設計師 / 工程師 / 創意人個人作品集。**最能展現 personality 的設計類型**。

## 高頻 pages

1. Home（intro + work grid）
2. Project detail
3. About / Bio
4. Contact / Hire
5. 可選：Blog / Notes
6. 可選：Resume / CV

## Home 元件組合

| 序 | 元件 | 必出 / 可選 |
|----|------|-----------|
| 1 | [Nav](../components/nav.md)（minimal） | 必出 |
| 2 | Intro / Bio statement | 必出 — 一句話說你是誰 |
| 3 | Project grid / list | 必出 |
| 4 | Now / Currently（在做什麼） | 可選 — 加分項 |
| 5 | [Footer](../components/footer.md)（contact） | 必出 |

## Project detail anatomy

```
┌─────────────────────────────────────┐
│ Back to projects                    │
│                                     │
│ Project Title                       │
│ Client · Year · Role                │
│                                     │
│ [Hero image / video]                │
│                                     │
│ Problem / Brief                     │
│ Process                             │
│ Solution / Outcome                  │
│                                     │
│ [Image] [Image]                     │
│  [Larger image]                     │
│ [Image]                             │
│                                     │
│ Credits / Team                      │
│ Next project →                      │
└─────────────────────────────────────┘
```

## 推薦風格（依職業）

| 職業 | 第一推 | 第二推 |
|------|-------|-------|
| 設計師（graphic / brand） | **Swiss Editorial**, Editorial Maximal | Brutalist |
| UI/UX 設計師 | Type-First Monochrome, Minimal Float | Swiss Editorial |
| 攝影師 | Fashion / Luxury, Magazine | Editorial Maximal |
| 插畫師 / Illustrator | Brutalist, Neobrutalism | Magazine |
| 工程師（developer） | **Brutalist**, Type-First Monochrome | Swiss Editorial |
| 寫作者 / 編輯 | Magazine Longform, Brutalist | Type-First |
| 創意工作室 | Swiss Editorial, Editorial Maximal | Kinetic Editorial |
| 動畫師 | Kinetic Editorial, 3D Immersive | Editorial Maximal |
| 建築師 | Swiss Editorial, Editorial Maximal | Magazine |

**幾乎不推**：Glass / Aurora / Clay / Bento — 看起來像 SaaS template 不像個人作品。

## 個性化原則

Portfolio **就是要不一樣**。AI tell 在 portfolio 特別致命。

### 必避免的 portfolio AI tells

1. ❌ Hero：「Hi, I'm [Name]. I'm a [Role] based in [City]」
2. ❌ Social icons 三件套（Twitter / LinkedIn / GitHub）lucide
3. ❌ 「Available for freelance ✨」pill
4. ❌ Skills tag cloud
5. ❌ Timeline 用 lucide circle dots
6. ❌ 「Get in touch」CTA 用 gradient
7. ❌ Testimonial 從 client 圓頭像 + 5 stars

### 替代寫法

| AI default | Personality 寫法 |
|-----------|------------------|
| "Hi, I'm Lin" | 一段 quote / observation about your craft |
| Social icons | inline links: "Twitter, GitHub, email" |
| "Available" pill | Footer line: "Open for selective work in 2026" |
| Skills cloud | Prose: "I work mostly in TypeScript, sometimes Rust" |
| Timeline dots | Plain numbered list with dates |
| Testimonial 5-star | Quote with full attribution |

## Project work display 策略

3 種主要 layout：

1. **Grid (3-col)** — 多項目時用
2. **Index list** — Swiss / minimal 風格，文字優先
3. **Vertical scroll** — 每 project full-bleed photo

## 內容必填

當 skill 出 portfolio 框架，主動 ask user：

- 全名 / 中文+英文
- 職業 / role description（一句）
- 城市 / location（如願公開）
- 5-10 個 projects（每個 title + brief + image）
- Bio / 長版自介（200-500 字）
- Contact methods（email / form / 社群）
- 是否 available for hire

## Now page（加分項）

很多頂級 portfolio 有 `/now` 頁：

```html
<main>
  <h1>Now</h1>
  <p>Updated 2026-05-11.</p>
  <ul>
    <li>Designing brand identity for [Client]</li>
    <li>Reading "The Pattern Language" by Christopher Alexander</li>
    <li>Living in Taipei</li>
  </ul>
</main>
```

很 personal，反 AI tell 的好方式。

## 整合 Step 1

當 user 回「個人作品集」+ 職業，skill 自動：
- 推 anti-AI 風格優先
- 詢問是否要 Now page
- 提示 personality 寫法替代
- 警告 portfolio AI tells
