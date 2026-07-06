<script setup lang="ts">
defineProps<{
  title: string
  items: string[]
}>()
</script>

<template>
  <div>
    <p class="font-mono-label text-[11px] font-medium uppercase tracking-widest text-accent mb-3">
      {{ title }}
    </p>
    <div class="flex flex-wrap gap-2">
      <span
        v-for="item in items"
        :key="item"
        class="text-xs px-2.5 py-1 rounded-full border border-ink/15 text-ink/70"
      >{{ item }}</span>
    </div>
  </div>
</template>
