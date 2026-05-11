# Docs / Documentation Industry Bundle

> 技術文件 / API reference / Guides。**閱讀體驗 > 視覺花俏**。

## 高頻 pages

1. Home / Getting Started
2. Guides / Tutorials
3. API reference
4. Concepts
5. Examples / Recipes
6. Changelog
7. Search results
8. 404

## 元件組合

| 序 | 元件 | 必出 |
|----|------|------|
| 1 | [Nav](../components/nav.md)（top） | ✓ |
| 2 | [Sidebar](../components/sidebar.md)（左 nav） | ✓ |
| 3 | Search bar (with shortcut hint Cmd+K) | ✓ |
| 4 | Main content area | ✓ |
| 5 | TOC / On-this-page（右側） | 可選 |
| 6 | Breadcrumb | 可選 |
| 7 | "Edit on GitHub" link | 可選 |
| 8 | Prev / Next page nav | ✓ |
| 9 | [Footer](../components/footer.md) | ✓ |

## Docs page layout

```
┌──────────────────────────────────────────┐
│ Top nav (logo, search, GitHub link)      │
├──────┬──────────────────────────┬────────┤
│      │                          │        │
│ Side │ Main content             │ On     │
│ bar  │                          │ this   │
│      │ # Heading                │ page   │
│ - A  │ Body...                  │        │
│ - B  │ ## Section               │ - h2   │
│ -[C] │ Body...                  │ -[h2]  │
│ - D  │                          │ - h3   │
│      │ ```js                    │        │
│      │ code                     │        │
│      │ ```                      │        │
│      │                          │        │
│      │ ← Prev      Next →       │        │
└──────┴──────────────────────────┴────────┘
```

## 推薦風格

| 文件類型 | 第一推 | 第二推 |
|---------|-------|-------|
| 技術文件 / API | **Corporate Clean**, Type-First Monochrome | Swiss Editorial |
| 設計系統文件 | Swiss Editorial, Editorial Maximal | Type-First |
| 開發者工具 | **Type-First Monochrome** | Brutalist (raw) |
| 框架 / Library | Corporate Clean, Type-First | Swiss Editorial |
| 教學 / Tutorial | Magazine Longform, Editorial Maximal | Corporate Clean |

**不推**：Aurora / Glass / Clay / Bento / Kinetic — 不適合長時間閱讀。

## Code block 必查

```css
pre {
  font-family: var(--font-mono);
  font-size: 0.875rem;
  padding: 1rem 1.25rem;
  background: var(--color-surface);
  border: 1px solid var(--color-rule);
  border-radius: 6px;
  overflow-x: auto;
  line-height: 1.6;
}
code { font-family: var(--font-mono); font-size: 0.875em; }
:not(pre) > code {
  background: var(--color-surface);
  padding: 0.125em 0.375em;
  border-radius: 3px;
}
```

### Syntax highlighting

- 用 Shiki / Prism / Highlight.js
- 顏色 **不能用來傳達語意**（colorblind users）
- 提供 copy button
- Line numbers 可選

```html
<pre tabindex="0">
  <button aria-label="Copy code" data-copy>Copy</button>
  <code class="language-ts">...</code>
</pre>
```

## Search

- Cmd+K / Ctrl+K shortcut
- 用 Algolia DocSearch 或 Pagefind (static)
- Keyboard nav 結果（↑↓ + Enter）
- 高亮匹配關鍵字

```html
<button aria-haspopup="dialog" aria-label="Search (Cmd K)">
  <span>Search...</span>
  <kbd>⌘K</kbd>
</button>
```

## Callout / Admonition

```html
<aside role="note" class="callout callout--warning">
  <strong>Note:</strong> This API is deprecated in v2.0.
</aside>
```

```css
.callout {
  padding: 1rem 1.25rem;
  border-left: 3px solid var(--color-accent);
  background: var(--color-surface);
  margin: 1.5rem 0;
}
.callout--warning { border-color: var(--color-warning, #f59e0b); }
.callout--danger { border-color: var(--color-danger, #d63838); }
.callout--info { border-color: var(--color-info, var(--color-accent)); }
```

## 必避免的 Docs AI tells

1. ❌ Hero 上「Get started in 30 seconds」+ npm install copy box
2. ❌ Sidebar 用 lucide chevron icon expand
3. ❌ Code block 用 Carbon-style screenshot
4. ❌ Callout 用 emoji icon (💡 ⚠️ ❌ ✅)
5. ❌ TOC 用 chevron dot
6. ❌ Search 用 lucide search icon
7. ❌ Feature cards on docs home (用 link list)
8. ❌ Mintlify-style gradient docs

## API Reference 結構

對每個 endpoint / function：

- Name + signature
- Brief description
- Parameters table
- Return value
- Example（runnable）
- Notes / caveats
- Related links

```html
<section id="api-getUser">
  <h2><code>getUser(id)</code></h2>
  <p>Fetch a user by id.</p>

  <h3>Parameters</h3>
  <table>
    <thead>
      <tr><th>Name</th><th>Type</th><th>Required</th><th>Description</th></tr>
    </thead>
    <tbody>
      <tr><td>id</td><td>string</td><td>yes</td><td>User UUID</td></tr>
    </tbody>
  </table>

  <h3>Example</h3>
  <pre><code>const user = await getUser('abc');</code></pre>
</section>
```

## Prev / Next page navigation

```html
<nav aria-label="Page navigation" class="page-nav">
  <a href="/intro" rel="prev">← Introduction</a>
  <a href="/installation" rel="next">Installation →</a>
</nav>
```

## Accessibility 特別注意

- Code block 必須 `tabindex="0"` 讓鍵盤 user 可以 scroll horizontal
- Skip link 跳過 sidebar
- TOC 在 mobile 變 `<details>`
- Search modal 用 `<dialog>`
- Keyboard shortcuts 必須有「View shortcuts」link

## 整合 Step 1

當 user 回「文件 / docs」，skill 自動：
- 套用 sidebar + TOC layout
- 推 Type-First / Corporate Clean / Swiss
- 主動 ask 是否需要 search
- 提供 callout 元件
- 警告 docs AI tell
