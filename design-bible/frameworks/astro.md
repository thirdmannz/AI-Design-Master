# Astro

> **Zero JS by default** content-first framework。Static-first，islands for interactivity。最適合 marketing site / blog / docs。

## 為什麼用 Astro

- 預設輸出純 HTML（最 a11y、最快）
- Islands architecture：只在需要互動時 hydrate
- 可混用 React / Vue / Svelte components
- File-based routing
- Markdown / MDX 一級支援

## Idioms

- `.astro` file = frontmatter + markup
- TypeScript in frontmatter
- `Astro.props` 取 props
- File: `kebab-case.astro` for pages，`PascalCase.astro` for components
- 直接 `<style>` 或 Tailwind 都可，`<script>` 在 client

## Token 接入

`src/styles/global.css`：

```css
:root {
  --color-bg: #fafaf7;
  --color-ink: #0a0a0a;
  --color-accent: #2c5fff;
  --font-display: "Inter Tight", system-ui;
  --font-body: "Inter", system-ui;
}
```

`src/layouts/Base.astro`：

```astro
---
import '../styles/global.css';
---
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width" />
    <slot name="head" />
  </head>
  <body>
    <slot />
  </body>
</html>
```

## Canonical Hero 範例

```astro
---
// src/components/Hero.astro
interface Props {
  title: string;
  lede: string;
  ctaHref: string;
  ctaLabel: string;
}

const { title, lede, ctaHref, ctaLabel } = Astro.props;
---

<section aria-labelledby="hero-title" class="hero">
  <h1 id="hero-title">{title}</h1>
  <p class="lede">{lede}</p>
  <a href={ctaHref} class="btn-primary">{ctaLabel}</a>
</section>

<style>
  .hero {
    padding: 4rem 1.25rem;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 1.25rem;
  }
  .hero h1 {
    font-family: var(--font-display);
    font-size: clamp(2.25rem, 8vw, 3.5rem);
    line-height: 1.05;
    letter-spacing: -0.025em;
    max-width: 18ch;
    margin: 0;
  }
  .btn-primary {
    background: var(--color-accent);
    color: white;
    padding: 0.875rem 2rem;
    border-radius: 6px;
    text-decoration: none;
    font-weight: 600;
  }
  @media (min-width: 768px) { .hero { padding: 6rem 2rem; } }
  @media (min-width: 1024px) {
    .hero { padding: 8rem 4rem; }
    .hero h1 { font-size: clamp(3rem, 6vw, 6rem); }
  }
</style>
```

## Pages（file-based routing）

```
src/pages/
├── index.astro              → /
├── pricing.astro            → /pricing
├── blog/
│   ├── index.astro          → /blog
│   └── [...slug].astro      → /blog/:slug
└── api/
    └── subscribe.ts         → /api/subscribe
```

## Content collections（blog posts）

```typescript
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    publishedAt: z.date(),
    author: z.string(),
    excerpt: z.string().optional(),
  }),
});

export const collections = { blog };
```

```astro
---
// src/pages/blog/index.astro
import { getCollection } from 'astro:content';
const posts = await getCollection('blog');
---

<ul>
  {posts.map(post => (
    <li>
      <a href={`/blog/${post.slug}`}>
        <time datetime={post.data.publishedAt.toISOString()}>
          {post.data.publishedAt.toLocaleDateString()}
        </time>
        <h2>{post.data.title}</h2>
      </a>
    </li>
  ))}
</ul>
```

## Islands（只在需要時 hydrate）

```astro
---
import Counter from '../components/Counter.tsx';
---

<!-- Hydrates on page load -->
<Counter client:load />

<!-- Hydrates when scrolled into view -->
<Counter client:visible />

<!-- Hydrates when idle -->
<Counter client:idle />

<!-- Server-rendered only, no JS -->
<Counter />
```

## Form 範例 (server action)

```astro
---
// src/pages/contact.astro
if (Astro.request.method === 'POST') {
  const data = await Astro.request.formData();
  const email = data.get('email');
  // send to backend / database
}
---

<form method="POST" action="/contact">
  <label for="email">Email</label>
  <input id="email" name="email" type="email" required autocomplete="email" />
  <button type="submit">Subscribe</button>
</form>
```

## Recommended setup

```bash
npm create astro@latest
npx astro add tailwind
npx astro add react  # if mixing
npx astro add mdx
```

## A11y

- Astro 默認靜態 = 最 a11y
- Native HTML 元素優先
- Islands 只在真正需要時用（form / interactive widget）
- 沒 JS user 也能用整個 site

## SEO / Meta

```astro
---
// src/layouts/Base.astro
const { title, description, ogImage } = Astro.props;
---

<head>
  <title>{title}</title>
  <meta name="description" content={description} />
  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
  <meta property="og:image" content={ogImage} />
  <meta name="twitter:card" content="summary_large_image" />
</head>
```

## AI Tell 自查

- [ ] **不要** 預設加 React island 給 static 內容
- [ ] **不要** lucide icon 在 marketing page（用 SVG inline 或字體）
- [ ] **不要** Tailwind v0-style class spam
- [ ] 善用 Astro 的「static HTML」優勢，不要把每個 widget 變 React component
