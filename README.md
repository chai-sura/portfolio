# Chaitanya Sura — Portfolio

Personal portfolio of **Chaitanya Sura** — Data · AI · ML Engineer & Data Scientist (Atlanta, GA, US).

A single-page site with a fixed sidebar, scroll-spy navigation, scroll-reveal animations, an experience/education timeline, and category-labeled project cards. Built with an editorial, dark, print-inspired aesthetic.

**Live site:** https://chai-sura.github.io/portfolio/

## Tech stack

- [Nuxt 3](https://nuxt.com) (compatibility v4) + Vue 3
- [Nuxt Content](https://content.nuxt.com) — content authored in Markdown (MDC)
- [Tailwind CSS v4](https://tailwindcss.com)
- [Iconify](https://iconify.design) via `@nuxt/icon`
- Fonts: Fraunces (display), Space Grotesk (body), JetBrains Mono (labels)

## Project structure

```
app/
  app.config.ts          # social handles (github, linkedin, email)
  layouts/sidebar.vue    # fixed sidebar + scroll-spy + scroll-reveal
  pages/[...slug].vue    # renders Markdown content
  components/
    ProjectCard.vue      # category-labeled project card
    ProjectGrid.vue
    TimelineGroup.vue    # experience / education timeline
    TimelineItem.vue
    SkillsGrid.vue       # grouped skill chips
    SkillGroup.vue
  assets/css/main.css    # theme palette, fonts, reveal animation
content/
  1.index.md             # all page content (About, Experience, Projects, Skills, Education, Contact)
public/                  # profile image, favicon
.github/workflows/deploy.yml  # build + deploy to GitHub Pages
```

## Editing content

All copy lives in [`content/1.index.md`](content/1.index.md). Projects, timeline entries, and skills use MDC components (e.g. `:::project-card`, `:::timeline-item`, `:::skill-group`).

## Local development

```bash
pnpm install
pnpm dev        # http://localhost:3000
```

## Build

```bash
pnpm generate   # static output in .output/public
```

Deployment is automated: pushing to `main` triggers the GitHub Actions workflow, which builds the static site and publishes it to GitHub Pages.
