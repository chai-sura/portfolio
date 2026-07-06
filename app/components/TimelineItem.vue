<script setup lang="ts">
defineProps<{
  date: string
  title: string
  org?: string
}>()
</script>

<template>
  <div class="relative pl-6 pb-8 last:pb-0">
    <span class="absolute -left-[6px] top-1.5 h-2.5 w-2.5 rounded-full bg-accent ring-4 ring-paper" />
    <p class="font-mono-label text-[11px] font-medium uppercase tracking-widest text-accent">
      {{ date }}
    </p>
    <h3 class="mt-1.5 font-display text-xl font-medium text-ink">
      {{ title }}
    </h3>
    <p v-if="org" class="mt-0.5 text-sm text-ink/60">
      {{ org }}
    </p>
    <div class="mt-2.5 text-sm leading-relaxed text-ink/80 [&_em]:font-semibold [&_em]:not-italic [&_em]:text-ink">
      <slot />
    </div>
  </div>
</template>
