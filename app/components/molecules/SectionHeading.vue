<template>
  <div class="relative mb-12 md:mb-16">
    <!-- Decorative background number -->
    <span aria-hidden="true"
      class="absolute -top-4 left-0 select-none font-mono text-[7rem] font-bold leading-none text-foreground/3 md:text-[10rem]">
      {{ rawNumber }}
    </span>

    <RevealItem>
      <span class="font-mono text-xs uppercase tracking-[0.2em] text-muted-foreground">
        {{ label }}
      </span>
    </RevealItem>
    <RevealItem :delay="100">
      <h2 class="mt-3 text-3xl font-bold tracking-tight text-foreground sm:text-4xl md:text-5xl text-balance">
        {{ title }}
      </h2>
    </RevealItem>
    <RevealItem :delay="200">
      <div class="mt-4 h-px overflow-hidden bg-foreground/10 w-16">
        <div class="h-full bg-foreground/30 w-0 transition-[width] duration-700 ease-out in-[.is-visible]:w-16"
          style="transition-delay: 400ms" />
      </div>
    </RevealItem>
  </div>
</template>

<script setup lang="ts">
import RevealItem from "~/components/atoms/RevealItem.vue";

const props = defineProps<{
  label: string;
  title: string;
}>();

// Extract the numeric part from labels like "01 / About" → "01"
const rawNumber = computed(() => props.label.split('/')[0]?.trim() ?? '');
</script>
