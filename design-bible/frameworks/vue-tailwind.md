# Vue + Tailwind CSS

> Vue 3 + Composition API + `<script setup>` + Tailwind utility。

## Idioms

- Single File Component `.vue`
- `<script setup>` syntax（不要 Options API）
- TypeScript (`<script setup lang="ts">`)
- File: `PascalCase.vue`
- `defineProps` + `defineEmits`

## Token 接入

`tailwind.config.ts`：

```typescript
export default {
  content: ['./src/**/*.{vue,ts,tsx}'],
  theme: {
    extend: {
      colors: {
        bg: 'var(--color-bg)',
        ink: 'var(--color-ink)',
        accent: 'var(--color-accent)',
        muted: 'var(--color-muted)',
      },
      fontFamily: {
        display: ['var(--font-display)'],
        body: ['var(--font-body)'],
      },
    },
  },
};
```

`src/style.css`：

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --color-bg: #fafaf7;
  --color-ink: #0a0a0a;
  --color-accent: #2c5fff;
}
```

## Canonical Hero 範例

```vue
<!-- src/components/Hero.vue -->
<script setup lang="ts">
defineProps<{
  title: string;
  lede: string;
  ctaHref: string;
  ctaLabel: string;
}>();
</script>

<template>
  <section
    aria-labelledby="hero-title"
    class="px-5 py-16 md:px-8 md:py-24 lg:px-16 lg:py-32 flex flex-col items-start gap-5"
  >
    <h1
      id="hero-title"
      class="font-display text-[clamp(2.25rem,8vw,3.5rem)] lg:text-[clamp(3rem,6vw,6rem)] leading-[1.05] tracking-[-0.025em] max-w-[18ch]"
    >
      {{ title }}
    </h1>
    <p class="font-body text-[1.0625rem] leading-relaxed text-muted max-w-[52ch]">
      {{ lede }}
    </p>
    <a
      :href="ctaHref"
      class="inline-flex bg-accent text-white px-6 py-3 rounded-md font-medium hover:-translate-y-0.5 transition focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-accent"
    >
      {{ ctaLabel }}
    </a>
  </section>
</template>
```

## State / Reactivity

```vue
<script setup lang="ts">
import { ref, computed } from 'vue';

const isOpen = ref(false);
const billing = ref<'monthly' | 'yearly'>('monthly');
const price = computed(() => billing.value === 'monthly' ? 24 : 240);
</script>
```

## Form 範例

```vue
<script setup lang="ts">
import { ref } from 'vue';

const email = ref('');
const error = ref('');

function submit(e: Event) {
  e.preventDefault();
  if (!email.value.includes('@')) {
    error.value = 'Invalid email';
    return;
  }
  // submit logic
}
</script>

<template>
  <form @submit="submit" novalidate>
    <label for="email">Email</label>
    <input
      id="email"
      v-model="email"
      type="email"
      required
      autocomplete="email"
      :aria-invalid="!!error"
      aria-describedby="email-error"
    />
    <span v-if="error" id="email-error" role="alert">{{ error }}</span>
    <button type="submit">Submit</button>
  </form>
</template>
```

## Recommended libraries

| Need | Lib |
|------|-----|
| Component lib | `radix-vue` 或 `Headless UI` |
| Form | `vee-validate` + `zod` |
| Icons | `lucide-vue-next`（**慎用**） |
| Animation | `motion-v` (Framer Motion port) |
| Router | Vue Router 4 |
| Meta SSR | Nuxt 3 |

## A11y 注意

- `for` 不是 `htmlFor`
- 用 native `<dialog>` 比 Headless UI dialog 更 a11y
- `<details>` 比自製 accordion 簡單
- `aria-*` 屬性都是 kebab-case (Vue 自動處理)

## Common pitfalls

- ❌ `v-html` 接 user content（XSS）
- ❌ `:key="index"` 在 v-for（用穩定 id）
- ❌ Mixing Options API + `<script setup>`
- ❌ Tailwind dynamic class: `:class="\`bg-${color}\`"`（purge 掃不到）

## Nuxt 3 (SSR / SSG)

- Auto-import components from `components/`
- Pages in `pages/`，file-based routing
- `useFetch()` 跑 SSR data
- `useHead({})` 設 meta
- `app.vue` 是 root，含 `<NuxtPage />`

## AI Tell 自查

- [ ] 不要每個 button 都 `<UButton>` 預設 variant（Nuxt UI / shadcn-vue）
- [ ] 不要用 emoji 當 icon (`<span>🚀</span>`)
- [ ] 不要 v-for 一個 features array 全部 3-col grid
