<template>
  <main class="relative min-h-screen w-screen overflow-x-hidden">
    <Transition name="page">
      <slot />
    </Transition>
  </main>
</template>

<style scoped>
.page-enter-active {
  transition: opacity 0.4s ease-out, filter 0.4s ease-out;
}

.page-leave-active {
  transition: opacity 0.3s ease-in, filter 0.3s ease-in;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(0.5rem);
  will-change: opacity, filter;
}
</style>
