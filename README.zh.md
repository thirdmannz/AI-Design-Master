# 🎨 AI Design Master

> 一個 Claude Code skill，讓你設計出不像 AI 生成的網站 — 基於 **godly.website** 和 **dribbble.com** 的真實設計模式。

這個 skill 包含 **12 種專業設計風格**，每種都有完整的 CSS token、字體搭配、元件範例，以及「讓設計不像AI生成」的具體技巧 — 從 131 個真實網站和 320 個設計作品中提煉而來。

[English →](README.md)

---

## ✨ 功能

- **12 種設計風格** — 從 Glassmorphism 到 Neobrutalism，每種都有完整 CSS 變數、字體搭配和元件範例
- **新設計模式** — 回答 3 個問題，獲得完整的設計系統
- **Revamp 模式** — 分析你的現有程式碼，診斷設計問題，輸出逐元件遷移指南
- **「不像AI」原則** — 讓網站看起來像手工設計的具體技巧
- **框架無關** — 適用於 React、Vue、Next.js、plain HTML/CSS 或 Tailwind

---

## 🚀 安裝方式

**1. Clone 或下載這個 repo**
```bash
git clone https://github.com/thirdmannz/AI-Design-Master.git
```

**2. 將 skill 檔案複製到 Claude Code skills 目錄**

macOS / Linux：
```bash
cp skill.md ~/.claude/skills/design.md
```

Windows：
```powershell
copy skill.md %USERPROFILE%\.claude\skills\design.md
```

**3. 完成。** 在任何專案目錄開啟 Claude Code，輸入 `/design`。

---

## 🎯 使用方法

### 設計新網站

```
/design
```

Claude 會問你 3 個問題：
1. 網站類型？（SaaS / 作品集 / 電商 / 落地頁 / 部落格 / B2B / 遊戲）
2. 目標受眾？（科技用戶 / 創意工作者 / 企業客戶 / 一般消費者 / Z世代）
3. 要傳達什麼感受？（專業 / 大膽 / 溫暖 / 奢華 / 俐落現代）

然後推薦 2-3 個風格，並輸出：
- 完整的 `:root {}` CSS token 組
- Google Fonts `<link>` 標籤
- Tailwind config 版本
- Hero、Nav、Card、Button、Footer CSS
- 3 個具體的「不像AI生成」實作提示

### Revamp 現有網站

在你的專案目錄執行 `/design`，選擇 **「Revamp 現有網站」**。

Claude 會：
1. **掃描** 你的 CSS、HTML、JSX、Vue、config 檔案
2. **診斷** 目前的設計問題（通用色彩、不一致的 spacing、AI 感陰影）
3. **推薦** 最佳升級方向
4. **輸出** 逐元件的遷移指南，包含 Before/After CSS 對比

---

## 🎨 12 種設計風格

| # | 風格 | 適合 |
|---|------|------|
| 🪟 | **Glassmorphism（霧面玻璃）** | SaaS、AI 產品、暗色介面 |
| 🔩 | **Neobrutalism（新野蠻主義）** | 作品集、創意工具、反叛品牌 |
| 🕊️ | **Minimal Float（極簡漂浮）** | 奢侈品牌、高端作品集 |
| 🍱 | **Bento Grid（便當格）** | SaaS 功能頁、App 官網 |
| 🖤 | **Dark Luxury（暗黑奢華）** | 精品品牌、奢侈品、高端餐廳 |
| 🌌 | **Aurora UI（極光介面）** | AI 產品、科技新創、創意工具 |
| 🫧 | **Claymorphism（黏土感）** | 教育 App、遊戲、趣味 SaaS |
| 🌿 | **Organic Nature（有機自然）** | 健康品牌、有機食品、wellness |
| 📰 | **Editorial Maximal（雜誌排版）** | 媒體品牌、設計工作室 |
| 🏢 | **Corporate Clean（企業清潔）** | B2B、金融科技、企業服務 |
| ⚡ | **Kinetic Editorial（動態排版）** | 品牌故事頁、互動作品集 |
| 🌐 | **3D Immersive（沉浸式3D）** | 遊戲官網、高端產品展示 |

每種風格包含：
- 完整 CSS custom properties（`:root {}`）
- Tailwind config 版本
- Google Fonts 字體搭配建議
- Hero、Card、Button 元件範例
- 3 個「不像AI生成」的具體技巧

---

## 💡 讓設計不像 AI 生成的原則

這個 skill 教你的具體技巧：

- **標題負字距**（`-0.03em`）— AI 預設字距讓字母太鬆散
- **非純白背景**（`#fafaf8` 而非 `#fff`）— 增加質感
- **不對稱光暈** — 光源放在角落，不要正中心
- **三層陰影系統** — xs、sm、md 對應不同 UI 層次
- **`clamp()` 流體字體** — Hero 字體大小自適應螢幕
- **有機圓角語法** — `30% 70% 70% 30% / 30% 30% 70% 70%` 製造自然曲線
- **刻意打破網格** — 讓一個元素超出 grid 邊界製造張力

---

## 📁 檔案結構

```
AI-Design-Master/
├── skill.md                    ← 安裝到 ~/.claude/skills/design.md
├── design-bible/
│   └── styles/
│       ├── glassmorphism.md    ← 每種風格的詳細參考
│       ├── neobrutalism.md
│       ├── minimal_float.md
│       └── ... (12 個風格)
└── data/
    └── design-bible.json       ← 編譯後的設計資料庫
```

---

## 🔧 需求

- [Claude Code](https://claude.ai/code)（CLI 或桌面版）
- 無其他相依 — skill 完全透過 Claude 運行

---

## 📖 風格選擇速查表

| 網站類型 | 優先推薦 | 備選 |
|---------|---------|------|
| SaaS / 工具 | Aurora UI、Glassmorphism | Bento Grid、Corporate Clean |
| 個人作品集 | Minimal Float、Neobrutalism | Editorial、Kinetic |
| 電商 / 品牌 | Organic Nature、Dark Luxury | Claymorphism、Editorial |
| 行銷落地頁 | Aurora UI、Kinetic Editorial | Glassmorphism、Bento Grid |
| 企業 / B2B | Corporate Clean、Minimal Float | Bento Grid |
| 遊戲 / 互動 | 3D Immersive、Kinetic Editorial | Neobrutalism |
| 健康 / 生活 | Organic Nature、Minimal Float | Claymorphism |
| AI 產品 | Aurora UI、Glassmorphism | Bento Grid |

---

## 🤝 貢獻

發現好的設計模式沒有收錄？歡迎開 PR 加到 `design-bible/styles/`。

---

## 📄 授權

MIT — 個人和商業專案皆可自由使用。

---

*設計知識來源：[godly.website](https://godly.website) 和 [dribbble.com](https://dribbble.com)*
