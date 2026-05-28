<template>
  <ProgressBar />
  <header class="fixed top-0 left-0 right-0 z-50 transition-all duration-500"
    :class="scrolled ? 'bg-background/80 backdrop-blur-xl border-b border-border' : 'bg-transparent'">

    <nav class="mx-auto flex max-w-6xl items-center justify-between px-6 py-4">
      <a href="#" class="text-lg font-semibold tracking-tight text-foreground transition-opacity hover:opacity-70">
        ronz<span class="text-muted-foreground">.dev</span>
      </a>

      <!-- Desktop nav -->
      <ul class="hidden items-center gap-8 md:flex">
        <li v-for="link in links" :key="link.href">
          <a :href="link.href" class="text-sm transition-colors duration-300" :class="activeSection === link.sectionId
            ? 'text-foreground'
            : 'text-muted-foreground hover:text-foreground'">
            {{ link.label }}
          </a>
        </li>
      </ul>

      <!-- Mobile hamburger -->
      <button
        class="flex h-9 w-9 items-center justify-center rounded-md border border-border text-muted-foreground transition-colors hover:text-foreground md:hidden"
        :aria-label="mobileOpen ? 'Close menu' : 'Open menu'" :aria-expanded="mobileOpen"
        @click="mobileOpen = !mobileOpen">
        <Icon :name="mobileOpen ? 'lucide:x' : 'lucide:menu'" class="h-4 w-4" />
      </button>
    </nav>

    <!-- Mobile menu panel -->
    <Transition enter-active-class="transition-all duration-300 ease-out" enter-from-class="opacity-0 -translate-y-2"
      enter-to-class="opacity-100 translate-y-0" leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0" leave-to-class="opacity-0 -translate-y-2">
      <div v-if="mobileOpen" class="border-b border-border bg-background/95 backdrop-blur-xl md:hidden">
        <ul class="mx-auto max-w-6xl space-y-1 px-6 py-4">
          <li v-for="link in links" :key="link.href">
            <a :href="link.href" class="block rounded-md px-3 py-2 text-sm transition-colors duration-200" :class="activeSection === link.sectionId
              ? 'bg-secondary text-foreground'
              : 'text-muted-foreground hover:bg-secondary/50 hover:text-foreground'" @click="mobileOpen = false">
              {{ link.label }}
            </a>
          </li>
        </ul>
      </div>
    </Transition>
  </header>
</template>

<script setup lang="ts">
import ProgressBar from "~/components/atoms/ProgressBar.vue";

interface Link {
  href: string;
  label: string;
  sectionId: string;
};

const links: Link[] = [
  { href: "#about", label: "About", sectionId: "about" },
  { href: "#experience", label: "Experience", sectionId: "experience" },
  { href: "#projects", label: "Projects", sectionId: "projects" },
  { href: "#contact", label: "Contact", sectionId: "contact" },
];

const scrolled = ref(false);
const mobileOpen = ref(false);
const activeSection = ref('');

const onScroll = () => { scrolled.value = window.scrollY > 50 };

let sectionObserver: IntersectionObserver | null = null;

onMounted(() => {
  window.addEventListener("scroll", onScroll, { passive: true });

  sectionObserver = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id;
        }
      }
    },
    { threshold: 0.3, rootMargin: '-10% 0px -60% 0px' }
  );

  links.forEach(({ sectionId }) => {
    const el = document.getElementById(sectionId);
    if (el) sectionObserver!.observe(el);
  });
});

onUnmounted(() => {
  window.removeEventListener("scroll", onScroll);
  sectionObserver?.disconnect();
});
</script>
