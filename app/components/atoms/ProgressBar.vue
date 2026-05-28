<template>
  <div class="fixed top-0 left-0 right-0 z-60 h-0.5 bg-transparent" aria-hidden="true">
    <div class="h-full bg-foreground/50 transition-[width] duration-100 ease-linear"
      :style="{ width: `${progress}%` }" />
  </div>
</template>

<script setup lang="ts">
const progress = ref(0);

function onScroll() {
  const scrollTop = window.scrollY;
  const docHeight = document.documentElement.scrollHeight - window.innerHeight;
  progress.value = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0;
};

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }));
onUnmounted(() => window.removeEventListener('scroll', onScroll));
</script>
