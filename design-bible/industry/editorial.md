# Editorial / Media / Content Industry Bundle

> 媒體 / 雜誌 / 內容平台。**排版即一切**。

## 高頻 pages

1. Home（front-page / magazine cover）
2. Section（topic landing）
3. Article（single post）
4. Author profile
5. Archive / Tag listing
6. Newsletter signup
7. About / Masthead
8. Search results

## 元件組合（Article 為主）

| 序 | 元件 | 注意 |
|----|------|------|
| 1 | [Nav](../components/nav.md)（serif logo + section nav） | masthead-style |
| 2 | Article header（kicker + title + lede + meta） | 必出 |
| 3 | [Blog](../components/blog.md) post body | drop cap 可選 |
| 4 | Pull quote / marginalia | 可選 |
| 5 | Author bio block | 可選 |
| 6 | Related articles | 可選 |
| 7 | Newsletter signup | 可選 |
| 8 | [Footer](../components/footer.md)（colophon / credits） | 必出 |

## Article anatomy

```
┌─────────────────────────────────────┐
│ KICKER (section / category)         │
│                                     │
│ Article Title Goes Here Bigger      │
│                                     │
│ Lede / dek explaining the angle.    │
│                                     │
│ By Author · May 1, 2026 · 8 min     │
│                                     │
│ ─────────────────────────────       │
│                                     │
│ D ropped cap leads the first        │
│   paragraph. Body text continues    │
│   with strong vertical rhythm...    │
│                                     │
│         "Pull quote in larger       │
│          serif, italic, indent"     │
│                                     │
│ Continued body...                   │
│  ┌──────────────────┐               │
│  │ Marginalia note  │ Continued     │
│  │ in side column   │ body next     │
│  └──────────────────┘ to it...      │
└─────────────────────────────────────┘
```

## Home / Front-page

- Hero article（big photo + masthead-style title）
- Editor's picks（2-3 article cards）
- By section（latest in Politics / Tech / Culture）
- Most read
- Newsletter signup

## 推薦風格

| 內容類型 | 第一推 | 第二推 |
|---------|-------|-------|
| 長文 / 深度報導 | **Magazine Longform** | Editorial Maximal |
| 文化 / 評論 | **Magazine Longform**, Editorial | Type-First |
| 新聞 / 即時 | Corporate Clean, Editorial | Swiss Editorial |
| 設計 / 工藝 | Swiss Editorial, Editorial | Brutalist |
| 文學 / 詩 | Magazine Longform | Brutalist (default serif) |
| Tech blog | Type-First Monochrome | Editorial Maximal |

**幾乎不推**：Aurora, Glassmorphism, Claymorphism, Bento — 不符閱讀語境。

## 必出 typography 要求

- Body font ≥ 18px on desktop (16px mobile)
- Line-height 1.5-1.7
- Max line width 60-75 characters
- Vertical rhythm: paragraph spacing 一致
- Drop cap（首段第一字）作風格 cue
- Tabular numerals for stats / dates

## 必避免的 Editorial AI tells

1. ❌ Article hero 配 Unsplash stock photo（用真實攝影）
2. ❌ 「By Author Name · 8 min read · 1,234 views」固定 meta
3. ❌ 浮動 share button bar（typically AI default）
4. ❌ TOC 用 chevron icon
5. ❌ Author photo 圓頭像 + 「Twitter LinkedIn Email」三件套
6. ❌ Related posts 3-col card grid 用 lucide
7. ❌ 「Subscribe」CTA 用 gradient button
8. ❌ Newsletter modal 跳出 10 秒後

## Photography / Imagery

- 用 editorial 攝影（不要 stock illustration）
- 圖說（caption）必出，永遠 italic + smaller
- Photo credit 必出
- Black-and-white 是有效的風格選擇
- Diagrams / illustrations：手繪感 > vector flat

## Citation / Attribution

```html
<figure>
  <img src="..." alt="Workers building the bridge in 1953">
  <figcaption>
    Construction crew on the upper deck, 1953.
    <cite>Photo: Archive of NYC History.</cite>
  </figcaption>
</figure>
```

## SEO / Meta for editorial

- Open Graph image 必出（每篇文章）
- Article structured data (`<script type="application/ld+json">`)
- Author with `rel="author"`
- Publish + modified time
- Canonical URL

## 整合 Step 1

當 user 回「媒體 / 內容」，skill 自動：
- 推 Magazine Longform / Editorial Maximal
- 套用 article anatomy
- ask 攝影 / 字體偏好
- 提示 stock photo 警告
