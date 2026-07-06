<script setup lang="ts">
const appConfig = useAppConfig()

// Base-URL aware so the photo resolves correctly on subpath hosting (e.g. GitHub Pages)
const photo = `${useRuntimeConfig().app.baseURL}IMG_0963.jpeg`

const aboutText = 'I build production AI and data systems end to end — from data pipelines and lakehouse architecture to RAG, multi-agent LLM systems, and the evaluation harnesses that keep them reliable. My work spans finance and healthcare, across the full cycle: ingestion, modeling, retrieval, evaluation, and deployment. I care most about systems that don\'t just process information but reason about it, ground their answers in real sources, and can be trusted enough to act on.'

const sections = [
  { id: 'about', label: 'About' },
  { id: 'experience', label: 'Experience' },
  { id: 'projects', label: 'Projects' },
  { id: 'skills', label: 'Skills' },
  { id: 'contact', label: 'Contact' },
]
const active = ref('about')
const mainRef = ref<HTMLElement | null>(null)
const identityVisible = ref(false)
let revealObserver: IntersectionObserver | null = null

function onScroll() {
  let current = sections[0].id
  for (const s of sections) {
    const el = document.getElementById(s.id)
    if (el && el.getBoundingClientRect().top <= 150)
      current = s.id
  }
  active.value = current
  // Reveal the sidebar identity once the hero has been scrolled past
  identityVisible.value = window.scrollY > window.innerHeight * 0.6
}

function setupReveal() {
  const container = mainRef.value?.firstElementChild
  if (!container)
    return
  const blocks = Array.from(container.children) as HTMLElement[]
  blocks.forEach(b => b.classList.add('reveal'))
  revealObserver = new IntersectionObserver((entries) => {
    for (const entry of entries) {
      if (entry.isIntersecting) {
        entry.target.classList.add('in-view')
        revealObserver?.unobserve(entry.target)
      }
    }
  }, { rootMargin: '0px 0px -12% 0px', threshold: 0.08 })
  blocks.forEach(b => revealObserver!.observe(b))
}

onMounted(() => {
  onScroll()
  setupReveal()
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('resize', onScroll)
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('resize', onScroll)
  revealObserver?.disconnect()
})
</script>

<template>
  <div>
    <!-- Full-screen intro / hero -->
    <section
      id="intro"
      class="relative flex min-h-screen flex-col items-center justify-center px-6 text-center"
    >
      <img
        :src="photo"
        alt="Chaitanya Sura"
        class="mb-8 h-48 w-48 rounded-full border-2 border-ink object-cover sm:h-56 sm:w-56"
      >
      <p class="mb-3 font-mono-label text-xs font-medium uppercase tracking-widest text-accent">
        Hello, I'm
      </p>
      <h1 class="font-display text-5xl font-medium tracking-tight text-ink sm:text-6xl">
        Chaitanya Sura
      </h1>
      <p class="mt-6 max-w-2xl text-base leading-relaxed text-ink/70 sm:text-lg">
        {{ aboutText }}
      </p>
      <span class="absolute bottom-8 flex flex-col items-center gap-2 font-mono-label text-[10px] uppercase tracking-widest text-ink/40">
        Scroll
        <Icon name="i-lucide-chevron-down" class="size-4 animate-bounce" />
      </span>
    </section>

    <!-- Two-column: sticky identity sidebar + scrolling content -->
    <div class="w-full px-6 py-12 md:px-8 lg:flex lg:gap-12 lg:px-8 lg:py-0">
      <!-- Left sidebar -->
      <header class="lg:sticky lg:top-0 lg:flex lg:h-screen lg:max-h-screen lg:w-1/3 lg:max-w-xs lg:shrink-0 lg:flex-col lg:justify-between lg:py-24">
        <div
          class="transition-all duration-700"
          :class="identityVisible ? 'opacity-100 translate-y-0' : 'lg:opacity-0 lg:translate-y-3'"
        >
          <NuxtLink to="/">
            <h2 class="font-display text-3xl font-medium tracking-tight text-ink">
              Chaitanya Sura
            </h2>
          </NuxtLink>
          <p class="mt-3 text-base font-medium text-ink/70">
            Data · AI · ML Engineer <span class="italic text-accent">&amp;</span> Data Scientist
          </p>
          <p class="mt-3 flex items-center gap-1.5 font-mono-label text-xs uppercase tracking-widest text-ink/50">
            <Icon name="i-lucide-map-pin" class="size-3.5" />
            Atlanta, GA, US
          </p>

          <!-- Section nav with scroll-spy -->
          <nav class="mt-10 hidden lg:block">
            <ul class="space-y-3">
              <li v-for="s in sections" :key="s.id">
                <a
                  :href="`#${s.id}`"
                  class="inline-block py-1 font-mono-label text-xs font-medium uppercase tracking-widest transition-colors"
                  :class="active === s.id
                    ? 'text-accent'
                    : 'text-ink/50 hover:text-ink'"
                >{{ s.label }}</a>
              </li>
            </ul>
          </nav>
        </div>

        <!-- Socials -->
        <div
          class="mt-8 flex items-center gap-4 text-ink/50 transition-all duration-700"
          :class="identityVisible ? 'opacity-100' : 'lg:opacity-0'"
        >
          <a
            v-if="appConfig.socials?.github"
            :href="`https://github.com/${appConfig.socials.github}`"
            title="GitHub"
            class="hover:text-accent transition-colors"
          ><Icon class="size-5" name="i-simple-icons-github" /></a>
          <a
            v-if="appConfig.socials?.linkedin"
            :href="`https://linkedin.com/in/${appConfig.socials.linkedin}`"
            title="LinkedIn"
            class="hover:text-accent transition-colors"
          ><Icon class="size-5" name="i-simple-icons-linkedin" /></a>
          <a
            v-if="appConfig.socials?.email"
            :href="`mailto:${appConfig.socials.email}`"
            title="Email"
            class="hover:text-accent transition-colors"
          ><Icon class="size-5" name="i-lucide-mail" /></a>
        </div>
      </header>

      <!-- Right scrolling content -->
      <main ref="mainRef" class="prose max-w-none lg:flex-1 lg:py-24">
        <slot />
      </main>
    </div>
  </div>
</template>
