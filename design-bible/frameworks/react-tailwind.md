# React + Tailwind CSS

> 預設輸出格式。Function component + Tailwind utility classes + shadcn/ui 命名對齊。

## Idioms

- Function component, not class
- `'use client'` only when needed（form / animation / state）
- Co-locate styles via Tailwind utilities
- TypeScript by default
- File: `kebab-case.tsx`（page）/ `PascalCase.tsx`（component）
- Export named: `export function Hero()`

## 設計 token 接入 Tailwind

`tailwind.config.ts`：

```typescript
import type { Config } from 'tailwindcss';

export default {
  content: ['./app/**/*.{ts,tsx}'],
  theme: {
    extend: {
      colors: {
        bg: 'var(--color-bg)',
        ink: 'var(--color-ink)',
        muted: 'var(--color-muted)',
        accent: 'var(--color-accent)',
        rule: 'var(--color-rule)',
      },
      fontFamily: {
        display: 'var(--font-display)',
        body: 'var(--font-body)',
      },
      letterSpacing: {
        display: 'var(--letter-spacing-display)',
      },
    },
  },
} satisfies Config;
```

`app/globals.css`：

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --color-bg: #fafaf7;
  --color-ink: #0a0a0a;
  --color-accent: #2c5fff;
  /* ...rest from design system */
}
```

## Canonical Hero 範例

```tsx
// app/components/hero.tsx
export function Hero() {
  return (
    <section
      aria-labelledby="hero-title"
      className="px-5 py-16 md:px-8 md:py-24 lg:px-16 lg:py-32 flex flex-col items-start gap-5"
    >
      <h1
        id="hero-title"
        className="font-display text-[clamp(2.25rem,8vw,3.5rem)] lg:text-[clamp(3rem,6vw,6rem)] leading-[1.05] tracking-[-0.025em] max-w-[18ch]"
      >
        Build software, faster.
      </h1>
      <p className="font-body text-[1.0625rem] leading-relaxed text-muted max-w-[52ch]">
        A single platform for shipping production code.
      </p>
      <a
        href="/start"
        className="inline-flex items-center bg-accent text-white px-6 py-3 rounded-md font-medium hover:-translate-y-0.5 transition focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-accent"
      >
        Start free
      </a>
    </section>
  );
}
```

## shadcn/ui 對應命名

當 user 用 shadcn/ui 時，這些元件直接 swap：

| Our component | shadcn equiv | Notes |
|--------------|--------------|-------|
| Card | `<Card>` | `<Card><CardHeader><CardTitle>...</CardTitle></CardHeader></Card>` |
| Button | `<Button>` | variants: default / outline / ghost / destructive |
| Form | `<Form>` + react-hook-form | useForm + zod 驗證 |
| Modal | `<Dialog>` | `<DialogTrigger><DialogContent>` |
| FAQ accordion | `<Accordion>` | `type="single" collapsible` |
| Tabs | `<Tabs>` | `<TabsList><TabsTrigger><TabsContent>` |
| Dropdown nav | `<NavigationMenu>` | radix-based |
| Toast | `<Toaster>` + `useToast()` | sonner 也常用 |
| Tooltip | `<Tooltip>` | provider in layout |

## 預設依賴

```json
{
  "dependencies": {
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    "next": "^15.0.0",
    "tailwindcss": "^4.0.0"
  },
  "devDependencies": {
    "@types/react": "^19.0.0",
    "typescript": "^5.0.0"
  }
}
```

選用：
- shadcn/ui — `npx shadcn@latest init`
- Framer Motion — Kinetic / Aurora 風格動畫
- react-hook-form + zod — 表單
- lucide-react — **慎用**（典型 AI tell icon library，看風格決定）

## A11y 在 React 注意事項

- `<button>` not `<div onClick>`
- `htmlFor` 不是 `for`
- `aria-*` attributes camelCase: `ariaLabel` ❌ → `aria-label` ✓
- `tabIndex={0}` 不要亂用
- `useId()` 給動態 `id`（避免 SSR mismatch）

```tsx
import { useId } from 'react';

export function Field({ label, ...props }) {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>{label}</label>
      <input id={id} {...props} />
    </>
  );
}
```

## Common pitfalls

- ❌ Inline `style={{...}}` 拚 Tailwind — 走 utility class 為主
- ❌ Forgetting `key` in `.map()`
- ❌ `useEffect` 用來做 derived state — 用 `useMemo`
- ❌ Server component fetch 用 `useEffect` — 用 async function
- ❌ Tailwind class name 動態拼字串（'bg-' + color）— purge 會掃不到

## App Router (Next.js 15+)

- Server components by default
- `'use client'` only when needed
- Layout `<html><body>` in `app/layout.tsx`
- Tailwind globals 用 `import './globals.css'` in layout
- Metadata 用 `export const metadata = {}`

## Tailwind 4.0 注意

- `@import 'tailwindcss'` 取代 `@tailwind base/components/utilities`
- `@theme` 直接 inline 配置
- 不再需要 `tailwind.config.ts`（可選）

## AI Tell 自查（framework-specific）

- [ ] 不要 import `lucide-react` 後到處塞 icons
- [ ] 不要 button 永遠用 shadcn default variant
- [ ] 不要每個 Card 都 `<Card className="hover:shadow-lg transition">` 三件套
- [ ] 不要 `cn(className, ...)` 然後傳一堆 conditional class（Tailwind 不是越多越好）
