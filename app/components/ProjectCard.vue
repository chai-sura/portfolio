<script setup lang="ts">
const props = defineProps<{
  title: string
  href: string
  demo?: string
  tags?: string[]
  category?: string
}>()

const catColors: Record<string, string> = {
  AI: 'oklch(72% 0.17 295)', // violet
  ML: 'oklch(76% 0.15 160)', // emerald
  Data: 'oklch(74% 0.15 235)', // blue
  Visualization: 'oklch(80% 0.14 85)', // amber
}

const catColor = computed(() => catColors[props.category ?? ''] ?? 'var(--accent)')
</script>

<template>
  <div class="group flex flex-col h-full p-5 rounded-md border-2 border-ink/15 bg-paper transition-colors hover:border-ink">
    <span
      v-if="category"
      class="font-mono-label text-[10px] font-semibold uppercase tracking-widest mb-2"
      :style="{ color: catColor }"
    >{{ category }}</span>
    <h3 class="font-display text-lg font-medium text-ink transition-colors group-hover:text-accent">
      {{ title }}
    </h3>
    <div v-if="tags?.length" class="flex flex-wrap gap-1.5 mt-2.5">
      <span
        v-for="tag in tags"
        :key="tag"
        class="font-mono-label text-[10px] font-medium uppercase tracking-widest px-2 py-1 rounded-full border border-ink/15 text-ink/60"
      >{{ tag }}</span>
    </div>
    <p class="mt-3 text-sm leading-relaxed text-ink/70 flex-1">
      <slot />
    </p>
    <div class="flex flex-wrap items-center gap-x-4 gap-y-2 mt-4">
      <a
        :href="href"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-1.5 font-mono-label text-[11px] font-medium uppercase tracking-widest text-ink hover:text-accent transition-colors"
      >
        <Icon name="i-simple-icons-github" class="size-3.5" />
        View Repository
      </a>
      <a
        v-if="demo"
        :href="demo"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-1.5 font-mono-label text-[11px] font-medium uppercase tracking-widest text-accent hover:text-ink transition-colors"
      >
        <Icon name="i-lucide-external-link" class="size-3.5" />
        Live Demo
      </a>
    </div>
  </div>
</template>
