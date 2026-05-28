<template>
  <footer class="border-t border-border py-8">
    <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-4 px-6 sm:flex-row">
      <span class="font-mono text-xs text-muted-foreground">
        © {{ year }} ronz.dev — Built with Nuxt &amp; Tailwind
      </span>

      <div class="flex items-center gap-6">
        <a v-for="link in socials" :key="link.label" :href="link.href" target="_blank" rel="noopener noreferrer"
          class="text-muted-foreground transition-colors duration-200 hover:text-foreground" :aria-label="link.label">
          <Icon :name="link.icon" class="h-4 w-4" />
        </a>

        <button type="button" aria-label="Back to top"
          class="group flex h-8 w-8 items-center justify-center rounded-full border border-border text-muted-foreground transition-all duration-300 hover:border-foreground/20 hover:text-foreground"
          @click="scrollToTop">
          <Icon name="lucide:arrow-up"
            class="h-3.5 w-3.5 transition-transform duration-300 group-hover:-translate-y-0.5" />
        </button>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
const year = new Date().getFullYear();

const socials = [
  { label: "GitHub", icon: "lucide:github", href: "https://github.com/ronz204" },
  { label: "LinkedIn", icon: "lucide:linkedin", href: "https://www.linkedin.com/in/roney-ruiz-rojas-a8a98b292" },
];

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' });
}
</script>
