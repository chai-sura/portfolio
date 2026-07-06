<script setup lang="ts">
const { cover } = useAppConfig()

useSeoMeta({
  ogImage: cover,
  twitterCard: 'summary_large_image',
})
</script>

<template>
  <div>
    <Html lang="en" />
    <NuxtLoadingIndicator />
    <NuxtPage />
  </div>
</template>
