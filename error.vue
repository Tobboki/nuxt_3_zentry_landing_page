<template lang="html">
  <Navbar theme="secondary" :play-audio="false" />
  <main class="h-dvh w-full bg-yellow-300 flex flex-col items-center justify-center gap-8">
    <h1 class="special-font hero-heading text-black text-center uppercase !text-[24vw]">
      oh no<b>!</b>
    </h1>
    <div class="mb-16 flex flex-col gap-8">
      <h2 class="font-general text-center uppercase">
        404 error
      </h2>
      <p class="font-robert-medium text-center !text-[1.4vw] max-w-[38rem]">
        The requested page could not be found. Explore the Homepage for more information about Zentry.
      </p>
    </div>
    <Button 
      id="back-to-home"
      title="Back To Homepage"
      container-class="!bg-black text-white px-8"
      @click="router.push('/')"
    />
  </main>
</template>

<script lang="ts" setup>
  const router = useRouter()
</script>

<style scoped lang="scss">

</style>