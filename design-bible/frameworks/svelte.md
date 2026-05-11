# Svelte (4 / 5)

> Compiler-driven framework，zero runtime overhead。可搭 Tailwind 或 scoped CSS。

## Idioms

- `.svelte` file = `<script>` + markup + `<style>`
- TypeScript：`<script lang="ts">`
- Component props 用 `export let` (Svelte 4) 或 `$props()` (Svelte 5 runes)
- Scoped CSS by default
- File: `PascalCase.svelte`

## Token 接入（scoped CSS 或 Tailwind 都可）

### 方式 A：CSS Custom Properties + scoped

```svelte
<style>
  .hero {
    background: var(--color-bg);
    padding: 4rem 1.25rem;
  }
  .hero h1 {
    font-family: var(--font-display);
    font-size: clamp(2.25rem, 8vw, 3.5rem);
  }
  @media (min-width: 768px) {
    .hero { padding: 6rem 2rem; }
  }
</style>
```

### 方式 B：Tailwind

`tailwind.config.ts` 配置同 React 版。

```svelte
<section class="px-5 py-16 md:px-8 md:py-24 flex flex-col items-start gap-5">
```

## Canonical Hero 範例 (Svelte 5 runes)

```svelte
<!-- src/lib/Hero.svelte -->
<script lang="ts">
  let { title, lede, ctaHref, ctaLabel }: {
    title: string;
    lede: string;
    ctaHref: string;
    ctaLabel: string;
  } = $props();
</script>

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
  .lede {
    font-family: var(--font-body);
    color: var(--color-muted);
    max-width: 52ch;
  }
  .btn-primary {
    background: var(--color-accent);
    color: white;
    padding: 0.875rem 2rem;
    border-radius: 6px;
    text-decoration: none;
    font-weight: 600;
  }
  @media (min-width: 768px) {
    .hero { padding: 6rem 2rem; }
  }
  @media (min-width: 1024px) {
    .hero { padding: 8rem 4rem; }
    .hero h1 { font-size: clamp(3rem, 6vw, 6rem); }
  }
</style>
```

## State (Svelte 5 runes)

```svelte
<script lang="ts">
  let count = $state(0);
  let doubled = $derived(count * 2);

  $effect(() => {
    console.log(`count is ${count}`);
  });
</script>
```

## Form 範例

```svelte
<script lang="ts">
  let email = $state('');
  let error = $state('');

  function submit(e: SubmitEvent) {
    e.preventDefault();
    if (!email.includes('@')) error = 'Invalid email';
  }
</script>

<form on:submit={submit} novalidate>
  <label for="email">Email</label>
  <input
    id="email"
    bind:value={email}
    type="email"
    required
    autocomplete="email"
    aria-invalid={!!error}
    aria-describedby="email-error"
  />
  {#if error}
    <span id="email-error" role="alert">{error}</span>
  {/if}
  <button type="submit">Submit</button>
</form>
```

## Conditional / Loops

```svelte
{#if showModal}
  <dialog open>...</dialog>
{/if}

{#each items as item (item.id)}
  <li>{item.name}</li>
{/each}
```

## SvelteKit (SSR / SSG)

- `+page.svelte` 是 page
- `+layout.svelte` 是 layout
- `+page.server.ts` 跑 SSR loader
- `+page.ts` 跑 universal loader
- Form actions via `<form action="?/createPost">`

## Recommended libraries

| Need | Lib |
|------|-----|
| UI primitives | `bits-ui` 或 `melt-ui`（radix-style） |
| Form validation | `sveltekit-superforms` + `zod` |
| Icons | `@lucide/svelte`（**慎用**） |
| Animation | Svelte 內建 `transition:fade` |
| Headless | `melt-ui` |

## A11y

- Svelte compiler 內建 a11y warnings（`<img>` 沒 alt 會警告）
- 不要 disable warnings — 修正 root cause
- `bind:value` 不破壞 a11y
- 用 native `<dialog>`

## Common pitfalls

- ❌ Svelte 4 `export let` + Svelte 5 `$props()` 混用
- ❌ `on:click` 在 Svelte 5 改成 `onclick`
- ❌ `slot` 在 Svelte 5 改成 `{@render children()}` + snippet
- ❌ Tailwind class purge 動態拼接

## AI Tell 自查

- [ ] 不要 `transition:fly` 萬用 motion
- [ ] 不要每個 button 都 `import { Button } from $lib/ui`（同質化）
- [ ] 不要 lucide-svelte icon spam
