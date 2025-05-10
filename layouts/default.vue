<template>
  <div class="min-h-screen flex flex-col p-4">

    <!-- Main Content Wrapper -->
    <main class="flex-grow w-full max-w-screen-xl mx-auto p-4">
      <Transition name="page">
        <slot />
      </Transition>
    </main>
  </div>
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
