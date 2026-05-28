<template>
  <section class="relative flex min-h-screen items-center justify-center overflow-hidden" @mousemove="onMouseMove"
    @mouseleave="onMouseLeave">
    <!-- Particle Background -->
    <Particles />

    <!-- Cursor glow -->
    <div class="cursor-glow absolute inset-0 pointer-events-none transition-opacity duration-500"
      :style="cursorGlowStyle" aria-hidden="true" />

    <!-- Radial Gradient Overlay -->
    <div class="vignette absolute inset-0 pointer-events-none" aria-hidden="true" />

    <!-- Content -->
    <div class="relative z-10 mx-auto max-w-4xl px-6 text-center">
      <div class="mb-6 animate-fade-up opacity-0">
        <span
          class="inline-flex items-center gap-2 rounded-full border border-border bg-secondary/50 px-4 py-1.5 font-mono text-xs tracking-wider text-muted-foreground">
          <span class="h-1.5 w-1.5 rounded-full bg-emerald-500 animate-pulse-dot" aria-hidden="true" />
          AVAILABLE FOR WORK
        </span>
      </div>

      <h1
        class="animate-fade-up opacity-0 delay-100 text-balance text-5xl font-bold leading-[1.1] tracking-tight text-foreground sm:text-6xl md:text-7xl lg:text-8xl">
        Crafting digital
        <span class="relative inline-block">
          <span class="relative z-10">experiences</span>
          <span class="title-underline absolute -bottom-1 left-0 h-3 w-full opacity-20" aria-hidden="true" />
        </span>
      </h1>

      <p
        class="mx-auto mt-6 max-w-xl animate-fade-up opacity-0 delay-200 text-pretty text-base leading-relaxed text-muted-foreground sm:text-lg md:mt-8">
        Full-stack developer focused on building polished products with clean code
        and thoughtful design. I turn complex problems into elegant solutions.
      </p>

      <!-- Social Links -->
      <div class="mt-8 flex animate-fade-up opacity-0 delay-300 items-center justify-center gap-4 md:mt-10">
        <a v-for="link in socials" :key="link.label" :href="link.href" target="_blank" rel="noopener noreferrer"
          class="group flex h-11 w-11 items-center justify-center rounded-full border border-border bg-secondary/50 text-muted-foreground transition-all duration-300 hover:border-foreground/20 hover:text-foreground hover:bg-secondary"
          :aria-label="link.label">
          <Icon :name="link.icon" class="h-4.5 w-4.5 transition-transform duration-300 group-hover:scale-110" />
        </a>
        <a href="#contact"
          class="flex h-11 items-center gap-2 rounded-full border border-foreground/20 bg-foreground px-6 text-sm font-medium text-primary-foreground transition-all duration-300 hover:bg-foreground/90">
          Let's talk
        </a>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-fade-up opacity-0 delay-500">
      <a href="#about"
        class="group flex flex-col items-center gap-2 text-muted-foreground/50 transition-colors hover:text-muted-foreground"
        aria-label="Scroll to about section">
        <span class="text-[10px] uppercase tracking-[0.2em]">Scroll</span>
        <span class="relative h-8 w-px overflow-hidden bg-muted-foreground/20">
          <span class="scroll-line-inner absolute inset-x-0 top-0 bg-muted-foreground animate-scroll-line" />
        </span>
      </a>
    </div>
  </section>
</template>

<script lang="ts" setup>
import Particles from "~/components/atoms/Particles.vue";

interface Social {
  label: string;
  href: string;
  icon: string;
};

const socials: Social[] = [
  { label: "GitHub", href: "https://github.com/ronz204", icon: "lucide:github" },
  { label: "LinkedIn", href: "https://linkedin.com/in/roney-ruiz-rojas-a8a98b292", icon: "lucide:linkedin" },
] as const;

const mousePos = ref({ x: 0, y: 0 });
const isHovering = ref(false);

const cursorGlowStyle = computed(() => {
  if (!isHovering.value) return { opacity: 0 };
  return {
    opacity: 1,
    background: `radial-gradient(400px circle at ${mousePos.value.x}px ${mousePos.value.y}px, oklch(0.25 0 0 / 0.15), transparent 70%)`,
  };
});

function onMouseMove(e: MouseEvent) {
  const rect = (e.currentTarget as HTMLElement).getBoundingClientRect();
  mousePos.value = { x: e.clientX - rect.left, y: e.clientY - rect.top };
  isHovering.value = true;
}

function onMouseLeave() {
  isHovering.value = false;
}
</script>

<style scoped>
.vignette {
  background: radial-gradient(ellipse at 50% 50%, transparent 0%, oklch(0.07 0 0) 70%);
}

.title-underline {
  background: linear-gradient(90deg, oklch(0.75 0 0), transparent);
}

.scroll-line-inner {
  height: 100%;
}
</style>
