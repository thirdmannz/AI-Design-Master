# Sidebar / Dashboard Chrome

> Dashboard / Docs / Admin 應用的左側欄。**內容 app 用 sidebar，行銷頁不要 sidebar**。

## Anatomy

- Logo / brand top
- Primary nav (sections)
- 可選：secondary nav (current section's sub-pages)
- 可選：search
- Bottom：user menu / settings

## Canonical HTML

```html
<aside class="sidebar" aria-label="Main navigation">
  <a href="/" class="logo">YourBrand</a>

  <nav>
    <ul>
      <li><a href="/dashboard" aria-current="page">Dashboard</a></li>
      <li><a href="/projects">Projects</a></li>
      <li><a href="/settings">Settings</a></li>
    </ul>
  </nav>

  <div class="sidebar-bottom">
    <button type="button" aria-haspopup="menu">
      <img src="/avatar.jpg" alt="" width="32" height="32">
      <span>Lin Chao</span>
    </button>
  </div>
</aside>
```

## Canonical CSS

```css
.sidebar {
  width: 240px;
  padding: 1.25rem;
  background: var(--color-surface);
  border-right: 1px solid var(--color-rule);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  height: 100vh;
  position: sticky;
  top: 0;
}
.sidebar nav ul { list-style: none; padding: 0; display: flex; flex-direction: column; gap: 0.25rem; }
.sidebar nav a {
  display: block;
  padding: 0.5rem 0.75rem;
  border-radius: 6px;
  color: var(--color-muted);
  text-decoration: none;
  font-size: 0.9375rem;
}
.sidebar nav a:hover { background: var(--color-surface-hover); color: var(--color-ink); }
.sidebar nav a[aria-current="page"] { background: var(--color-accent-subtle); color: var(--color-accent); font-weight: 500; }
.sidebar-bottom { margin-top: auto; }

@media (max-width: 1023px) {
  .sidebar {
    position: fixed;
    transform: translateX(-100%);
    transition: transform 0.2s;
    z-index: 100;
    box-shadow: 0 0 32px rgba(0,0,0,0.2);
  }
  .sidebar[data-open="true"] { transform: translateX(0); }
}
```

## Mobile drawer 行為

- 用 hamburger toggle in top bar
- Open: slide-in from left, focus trap
- Close: ESC / outside click

## 風格輸出對照

| Style | 形式 |
|-------|------|
| Corporate Clean | classic sidebar with hover bg |
| Bento Grid | sidebar as bento cell column |
| Swiss Editorial | numbered nav (01 / 02 / 03), no icons |
| Brutalist | plain `<ul>` browser style |
| Type-First Monochrome | huge wordmark + tracked uppercase nav |
| Aurora UI | gradient highlight on active |
| Glassmorphism | backdrop-blur sidebar |
| **Magazine Longform** | ❌ **禁出** — 不是 app context |
| **Fashion / Luxury** | ⚠️ minimal vertical nav 替代 |
| **Editorial Maximal** | ⚠️ for docs / longform navigation only |

## 子 nav（current section's children）

```html
<nav aria-label="Section">
  <h2 class="sr-only">Settings</h2>
  <ul>
    <li><a href="/settings/profile" aria-current="page">Profile</a></li>
    <li><a href="/settings/billing">Billing</a></li>
  </ul>
</nav>
```

## Accessibility 必查

- [ ] `<aside aria-label>` 標籤
- [ ] `<nav>` 內含 `<ul><li>`
- [ ] Current page 用 `aria-current="page"`
- [ ] Mobile toggle button 用 `aria-expanded` + `aria-controls`
- [ ] Skip link 跳過 sidebar 直接到 main content
- [ ] Icons 用 `aria-hidden="true"` 如有文字 label

## AI Tell 自查

- [ ] **不要** lucide icon + label 萬用 sidebar
- [ ] **不要** 「Search...」cmd+K 三件套
- [ ] **不要** 用 indigo / violet 當 active bg
- [ ] 行銷網站不該有 sidebar（除非 docs）
